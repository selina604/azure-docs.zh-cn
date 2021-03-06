---
title: 加密 Azure 中 Linux VM 上的磁盘 | Microsoft 文档
description: 如何使用 Azure CLI 加密 Linux VM 上的虚拟磁盘以增强安全性
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/31/2018
ms.author: cynthn
ms.openlocfilehash: 044486424f8bcc9d66998f775154eff9c52e7d1b
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46981223"
---
# <a name="how-to-encrypt-a-linux-virtual-machine-in-azure"></a>如何加密 Azure 中的 Linux 虚拟机

为了增强虚拟机 (VM) 的安全性以及合规性，可以加密虚拟磁盘和 VM 本身。 VM 是使用 Azure Key Vault 中受保护的加密密钥进行加密的。 可以控制这些加密密钥，以及审核对它们的使用。 本文介绍如何使用 Azure CLI 加密 Linux VM 上的虚拟磁盘。 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果选择在本地安装并使用 CLI，本文要求运行 Azure CLI 2.0.30 或更高版本。 运行 `az --version` 即可查找版本。 如果需要进行安装或升级，请参阅[安装 Azure CLI]( /cli/azure/install-azure-cli)。

## <a name="overview-of-disk-encryption"></a>磁盘加密概述
Linux VM 上的虚拟磁盘是使用 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt) 静态加密的。 加密 Azure 中的虚拟磁盘不会产生费用。 使用软件保护将加密密钥存储在 Azure 密钥保管库中，或者，可在已通过 FIPS 140-2 级别 2 标准认证的硬件安全模块 (HSM) 中导入或生成密钥。 可以控制这些加密密钥，以及审核对它们的使用。 这些加密密钥用于加密和解密附加到 VM 的虚拟磁盘。 打开和关闭 VM 时，Azure Active Directory 服务主体将提供一个安全机制用于颁发这些加密密钥。

加密 VM 的过程如下：

1. 在 Azure 密钥保管库中创建加密密钥。
2. 配置可用于加密磁盘的加密密钥。
3. 若要从 Azure Key Vault 中读取加密密钥，可创建具有相应权限的 Azure Active Directory 服务主体。
4. 发出加密虚拟磁盘的命令，指定要使用的 Azure Active Directory 服务主体和相应的加密密钥。
5. Azure Active Directory 服务主体将从 Azure Key Vault 请求所需的加密密钥。
6. 使用提供的加密密钥加密虚拟磁盘。

## <a name="encryption-process"></a>加密过程
磁盘加密依赖于以下附加组件：

* **Azure 密钥保管库** - 用于保护磁盘加密/解密过程中使用的加密密钥和机密。
  * 可以使用现有的 Azure 密钥保管库（如果有）。 不需要专门使用某个密钥保管库来加密磁盘。
  * 要将管理边界和密钥可见性隔离开来，可以创建专用的密钥保管库。
* **Azure Active Directory** - 处理所需加密密钥的安全交换，以及对请求的操作执行的身份验证。
  * 通常，可以使用现有的 Azure Active Directory 实例来容装应用程序。
  * 服务主体提供了安全机制，可用于请求和获取相应的加密密钥。 实际并不需要开发与 Azure Active Directory 集成的应用程序。

## <a name="requirements-and-limitations"></a>要求和限制
磁盘加密支持的方案和要求

* 以下 Linux 服务器 SKU - Ubuntu、CentOS、SUSE、SUSE Linux Enterprise Server (SLES) 和 Red Hat Enterprise Linux。
* 所有资源（例如密钥保管库、存储帐户和 VM）必须在同一个 Azure 区域和订阅中。
* 标准 A、D、DS、G、GS 等系列的 VM。
* 在已加密的 Linux VM 上更新加密密钥。

以下方案目前不支持磁盘加密：

* 基本层 VM。
* 使用经典部署模型创建的 VM。
* 在 Linux VM 上禁用 OS 磁盘加密。
* 使用自定义 Linux 映像。

有关支持的方案和限制的详细信息，请参阅 [IaaS VM 的 Azure 磁盘加密](../../security/azure-security-disk-encryption.md)


## <a name="create-an-azure-key-vault-and-keys"></a>创建 Azure Key Vault 和密钥
在以下示例中，请将示例参数名称替换为自己的值。 示例参数名称包括 myResourceGroup、myKey 和 myVM。

第一步是创建用于存储加密密钥的 Azure 密钥保管库。 Azure 密钥保管库可以存储能够在应用程序和服务中安全实现的密钥、机密或密码。 对于虚拟磁盘加密，可以使用密钥保管库来存储用于加密或解密虚拟磁盘的加密密钥。

在 Azure 订阅中使用 [az provider register](/cli/azure/provider#az-provider-register) 启用 Azure Key Vault 提供程序，并使用 [az group create](/cli/azure/group#az-group-create) 创建一个资源组。 以下示例在 `eastus` 位置创建名为 myResourceGroup 的资源组：

```azurecli-interactive
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

包含加密密钥和关联的计算资源（例如存储和 VM 本身）的 Azure 密钥保管库必须位于同一区域。 使用 [az keyvault create](/cli/azure/keyvault#az-keyvault-create) 创建 Azure Key Vault，并启用 Key Vaul，将其用于磁盘加密。 指定 keyvault_name 的唯一 Key Vault 名称，如下所示：

```azurecli-interactive
keyvault_name=myuniquekeyvaultname
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

可以使用软件或硬件安全模型 (HSM) 保护来存储加密密钥。 使用 HSM 时需要高级密钥保管库。 与用于存储受软件保护的密钥的标准密钥保管库不同，创建高级密钥保管库会产生额外的费用。 要创建高级密钥保管库，请在前一步骤中，将 `--sku Premium` 添加到命令。 由于创建的是标准 Key Vault，以下示例使用受软件保护的密钥。

对于这两种保护模型，在启动 VM 解密虚拟磁盘时，都需要向 Azure 平台授予请求加密密钥的访问权限。 使用 [az keyvault key create](/cli/azure/keyvault/key#az-keyvault-key-create) 在 Key Vault 中创建加密密钥。 以下示例创建名为 myKey 的密钥：

```azurecli-interactive
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-an-azure-active-directory-service-principal"></a>创建 Azure Active Directory 服务主体
加密或解密虚拟磁盘时，将指定一个帐户来处理身份验证，以及从 Key Vault 交换加密密钥。 此帐户（Azure Active Directory 服务主体）允许 Azure 平台代表 VM 请求相应的加密密钥。 订阅中提供了一个默认的 Azure Active Directory 实例，不过，许多组织使用专用的 Azure Active Directory 目录。

通过将 Azure Active Directory 与 [az ad sp create-for-rbac](/cli/azure/ad/sp#az-ad-sp-create-for-rbac) 配合使用创建服务主体。 以下示例读入服务主体和密码的值，供在稍后的命令中使用：

```azurecli-interactive
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

只有创建服务主体时，才会显示密码。 如果需要，可查看并记录密码 (`echo $sp_password`)。 可以使用 [az ad sp list](/cli/azure/ad/sp#az-ad-sp-list) 列出服务主体并使用 [az ad sp show](/cli/azure/ad/sp#az-ad-sp-show) 查看特定服务主体的详细信息。

要成功加密或解密虚拟磁盘，必须将 Key Vault 中存储的加密密钥的权限设置为允许 Azure Active Directory 服务主体读取密钥。 使用 [az keyvault set-policy](/cli/azure/keyvault#az-keyvault-set-policy) 在 Key Vault 上设置权限。 在以下示例中，服务主体 ID 由上一个命令提供：

```azurecli-interactive
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-a-virtual-machine"></a>创建虚拟机
使用 [az vm create](/cli/azure/vm#az-vm-create) 创建 VM 并附加一个 5Gb 数据磁盘。 只有特定市场映像才支持磁盘加密。 以下示例使用 Ubuntu 16.04 LTS 映像创建一个名为 myVM 的 VM：

```azurecli-interactive
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

使用上一命令输出中显示的 *publicIpAddress* 通过 SSH 连接到 VM。 创建分区和文件系统，并安装数据磁盘。 有关详细信息，请参阅[连接 Linux VM 以安装新磁盘](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)。 关闭 SSH 会话。


## <a name="encrypt-the-virtual-machine"></a>加密虚拟机
要加密虚拟磁盘，可将前面的所有组件合并在一起：

1. 指定 Azure Active Directory 服务主体和密码。
2. 指定用于存储加密磁盘元数据的密钥保管库。
3. 指定用于实际加密和解密的加密密钥。
4. 指定是要加密 OS 磁盘、数据磁盘还是所有磁盘。

使用 [az vm encryption enable](/cli/azure/vm/encryption#az-vm-encryption-enable) 加密 VM。 以下示例使用之前的 [az ad sp create-for-rbac](/cli/azure/ad/sp#az-ad-sp-create-for-rbac) 命令中的 *$sp_id* 和 *$sp_password* 变量：

```azurecli-interactive
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

需要一段时间才能完成磁盘加密过程。 使用 [az vm encryption show](/cli/azure/vm/encryption#az-vm-encryption-show) 监视过程状态：

```azurecli-interactive
az vm encryption show --resource-group myResourceGroup --name myVM
```

输出类似于下面截断的示例：

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress"
]
```

请等待，直到 OS 磁盘的状态报告“VMRestartPending”，并使用 [az vm restart](/cli/azure/vm#az-vm-restart) 重启 VM：

```azurecli-interactive
az vm restart --resource-group myResourceGroup --name myVM
```

磁盘加密过程会在启动过程中完成，因此请等待几分钟后再使用 [az vm encryption show](/cli/azure/vm/encryption#az-vm-encryption-show) 查看加密状态：

```azurecli-interactive
az vm encryption show --resource-group myResourceGroup --name myVM
```

现在，状态应将 OS 磁盘和数据磁盘均报告为“Encrypted”。


## <a name="add-additional-data-disks"></a>添加更多数据磁盘
加密数据磁盘后，可将更多的虚拟磁盘添加到 VM 并将其加密。 例如，按如下所示将另一个虚拟磁盘添加到 VM：

```azurecli-interactive
az vm disk attach \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --disk myDataDisk \
    --new \
    --size-gb 5
```

重新运行命令以加密虚拟磁盘，如下所示：

```azurecli-interactive
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>后续步骤
* 有关管理 Azure 密钥保管库的详细信息，包括删除加密密钥和保管库，请参阅 [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md)（使用 CLI 管理密钥保管库）。
* 有关磁盘加密的详细信息，例如准备要上载到 Azure 的已加密自定义 VM，请参阅 [Azure Disk Encryption](../../security/azure-security-disk-encryption.md)\（Azure 磁盘加密）。
