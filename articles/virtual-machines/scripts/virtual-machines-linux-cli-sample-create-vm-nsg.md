---
title: Azure CLI 脚本示例 - 使用内部和外部 NSG 创建两个 VM | Microsoft 文档
description: Azure CLI 脚本示例 - 使用内部和外部 NSG 创建两个 VM
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1d5ac97b0a086f982a87e89b5142c9df950ca55d
ms.sourcegitcommit: aa988666476c05787afc84db94cfa50bc6852520
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2018
ms.locfileid: "37932470"
---
# <a name="secure-network-traffic-between-virtual-machines"></a>保护虚拟机之间的网络流量

此脚本创建两个虚拟机，并保护这两个虚拟机的传入流量。 一个虚拟机可在 Internet 上访问，其网络安全组 (NSG) 配置为允许端口 22 和端口 80 上的流量。 第二个虚拟机无法在 Internet 上访问，其 NSG 配置为仅允许来自第一个虚拟机的流量。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>示例脚本

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>清理部署

运行以下命令来删除资源组、VM 和所有相关资源。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令创建资源组、虚拟机和所有相关资源。 表中的每条命令均链接到特定于命令的文档。

| 命令 | 说明 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | 创建用于存储所有资源的资源组。 |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | 创建 Azure 虚拟网络和子网。 |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#az_network_vnet_subnet_create) | 创建子网。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#az_vm_create) | 创建虚拟机并将其连接到网卡、虚拟网络、子网和 NSG。 此命令还指定要使用的虚拟机映像和管理凭据。  |
| [az network nsg rule list](https://docs.microsoft.com/cli/azure/network/nsg/rule#az_network_nsg_rule_list) | 返回有关网络安全组规则的信息。 在此示例中，规则名称存储在变量中，以便以后在脚本中使用。 |
| [az network nsg rule update](https://docs.microsoft.com/cli/azure/network/nsg/rule#az_network_nsg_rule_update) | 更新 NSG 规则。 在本例中，将更新后端规则，仅从前端子网传递流量。 |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | 删除资源组，包括所有嵌套的资源。 |

## <a name="next-steps"></a>后续步骤

有关 Azure CLI 的详细信息，请参阅 [Azure CLI 文档](https://docs.microsoft.com/cli/azure)。

可以在 [Azure Linux VM 文档](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他虚拟机 CLI 脚本示例。
