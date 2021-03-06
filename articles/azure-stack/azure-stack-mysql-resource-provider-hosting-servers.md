---
title: Azure Stack 上的 MySQL 宿主服务器 | Microsoft Docs
description: 如何添加 MySQL 实例以通过 MySQL 适配器资源提供程序进行预配
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2018
ms.author: jeffgilb
ms.reviewer: quying
ms.openlocfilehash: 72824e5afb9f8d77c2f7d3bd01e6ff2035e95a95
ms.sourcegitcommit: 1981c65544e642958917a5ffa2b09d6b7345475d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2018
ms.locfileid: "48237258"
---
# <a name="add-hosting-servers-for-the-mysql-resource-provider"></a>为 MySQL 资源提供程序添加托管服务器

可以在 [Azure Stack](azure-stack-poc.md) 中的虚拟机 (VM) 上或者在 Azure Stack 环境外部的 VM 上托管 MySQL 实例，前提是 MySQL 资源提供程序能够连接到该实例。

> [!NOTE]
> 应在 MySQL 资源提供程序服务器上创建 MySQL 数据库。 MySQL 资源提供程序应默认提供商订阅中创建，而应计费的用户订阅中创建 MySQL 宿主服务器。 资源提供程序服务器不应承载用户数据库。

可以将 MySQL 版本 5.6、5.7 和 8.0 用于宿主服务器。 MySQL RP 不支持 caching_sha2_password 身份验证；下一版本会添加此功能。 必须将 MySQL 8.0 服务器配置为使用 mysql_native_password。 也支持 MariaDB。

## <a name="connect-to-a-mysql-hosting-server"></a>连接到 MySQL 宿主服务器

确保已准备好拥有管理特权的帐户的凭据。 若要添加宿主服务器，请执行以下步骤：

1. 以服务管理员的身份登录到 Azure Stack 操作员门户。
2. 选择“所有服务”。
3. 下**管理资源**类别中，选择**MySQL 宿主服务器** > **+ 添加**。 此时会打开“添加 MySQL 宿主服务器”对话框，如以下屏幕捕获所示。

   ![配置宿主服务器](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

4. 提供 MySQL 服务器实例的连接详细信息。

   * 对于“MySQL 宿主服务器名称”，请提供完全限定域名 (FQDN) 或有效的 IPv4 地址。 请勿使用短 VM 名称。
   * 未提供默认的 MySQL 实例，因此需指定“宿主服务器的大小(GB)”。 输入接近数据库服务器容量的大小。
   * 保留“订阅”的默认设置。
   * 对于“资源组”，请创建新组或使用现有组。

   > [!NOTE]
   > 如果租户和管理 Azure 资源管理器可以访问 MySQL 实例，则可让资源提供程序控制此实例。 但是，**必须**专门将 SQL 实例分配给资源提供程序。

5. 选择“SKU”，打开“创建 SKU”对话框。

   ![创建 MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)

   SKU **名称**应反映 SKU 的属性，这样用户就能将其数据库部署到适当的 SKU。

6. 选择“确定”以创建 SKU。
> [!NOTE]
> SKU 最长可能需要在一小时后才显示在门户中。 在部署并运行 SKU 之前，无法创建数据库。

7. 在“添加 MySQL 宿主服务器”下，选择“创建”。

添加服务器时，请将它们分配给新的或现有的 SKU，以区分服务套餐。 例如，可以通过一个 MySQL 企业实例来提供增加的数据库和自动备份。 可以将此高性能服务器保留给组织中的不同部门。

## <a name="security-considerations-for-mysql"></a>MySQL 安全注意事项

以下信息适用于 RP 和 MySQL 宿主服务器：

* 确保将所有宿主服务器配置为使用 TLS 1.2 进行通信。 请参阅 [Configuring MySQL to Use Encrypted Connections](https://dev.mysql.com/doc/refman/5.7/en/using-encrypted-connections.html)（将 MySQL 配置为使用加密连接）。
* 部署[透明数据加密](https://dev.mysql.com/doc/mysql-secure-deployment-guide/5.7/en/secure-deployment-data-encryption.html)。
* MySQL RP 不支持 caching_sha2_password 身份验证。

## <a name="increase-backend-database-capacity"></a>提高后端数据库容量

可以在 Azure Stack 门户中部署更多的 MySQL 服务器，以便提高后端数据库容量。 将这些服务器添加到新的或现有的 SKU。 如果向现有的 SKU 添加服务器，请确保该服务器的特征与 SKU 中其他服务器的特征相同。

## <a name="make-mysql-database-servers-available-to-your-users"></a>将 MySQL 数据库服务器提供给用户使用

创建计划和套餐，使用户能够使用 MySQL 数据库服务器。 将 Microsoft.MySqlAdapter 服务添加到计划，并创建新配额。 MySQL 不允许限制数据库的大小。

## <a name="next-steps"></a>后续步骤

[创建 MySQL 数据库](azure-stack-mysql-resource-provider-databases.md)