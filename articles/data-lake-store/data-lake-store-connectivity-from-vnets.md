---
title: 从 VNET 连接到 Azure Data Lake Store | Microsoft Docs
description: 从 Azure VNET 连接到 Azure Data Lake Store
services: data-lake-store,data-catalog
documentationcenter: ''
author: esung22
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: elsung
ms.openlocfilehash: 4086ef6ce2a95e0467eda61116ac002cf53610b5
ms.sourcegitcommit: ea5193f0729e85e2ddb11bb6d4516958510fd14c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36300784"
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>从 Azure VNET 中的 VM 访问 Azure Data Lake Store
Azure Data Lake Store 是一种在公共 Internet IP 地址上运行的 PaaS 服务。 可以连接到公共 Internet 的服务器通常也可连接到 Azure Data Lake Store 终结点。 默认情况下，Azure VNET 中的所有 VM 都可以访问 Internet，从而可访问 Azure Data Lake Store。 但是，可以将 VNET 中的 VM 配置为无法访问 Internet。 对于此类 VM，对 Azure Data Lake Store 的访问也受到限制。 可以使用以下任何方法在 Azure VNET 中阻止 VM 的公共 Internet 访问：

* 配置网络安全组 (NSG)
* 配置用户定义的路由 (UDR)
* 使用 ExpressRoute 阻止对 Internet 的访问时，通过 BGP（行业标准动态路由协议）交换路由

本文介绍如何从 Azure VM 启用对 Azure Data Lake Store 的访问，这些 VM 仅限于使用上述三种方法之一访问资源。

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a>从连接受限的 VM 启用与 Azure Data Lake Store 的连接
要从此类 VM 访问 Azure Data Lake Store，必须将其配置为访问 Azure Data Lake Store 帐户可用的 IP 地址。 可通过解析帐户的 DNS 名称 (`<account>.azuredatalakestore.net`) 来识别 Data Lake Store 帐户的 IP 地址。 可以使用如 nslookup 等工具解析帐户的 DNS 名称。 在计算机上打开命令提示符并运行以下命令：

    nslookup mydatastore.azuredatalakestore.net

输出如下所示。 **地址**属性的值是与 Data Lake Store 帐户关联的 IP 地址。

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>使用 NSG 启用受限 VM 的连接
使用 NSG 规则阻止对 Internet 的访问时，可创建另一个允许访问 Data Lake Store IP 地址的 NSG。 有关 NSG 规则的详细信息，请参阅[网络安全组概述](../virtual-network/security-overview.md)。 有关如何创建 NSG 的说明，请参阅[如何创建网络安全组](../virtual-network/tutorial-filter-network-traffic.md)。

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>使用 UDR 或 ExpressRoute 启用受限 VM 的连接
路由（UDR 或 BGP 交换的路由）用于阻止对 Internet 的访问时，需要配置特殊的路由，以便此类子网中的 VM 可以访问 Data Lake Store 终结点。 有关详细信息，请参阅[用户定义路由概述](../virtual-network/virtual-networks-udr-overview.md)。 有关创建 UDR 的说明，请参阅[在 Resource Manager 中创建 UDR](../virtual-network/tutorial-create-route-table-powershell.md)。

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>使用 ExpressRoute 启用受限 VM 的连接
配置 ExpressRoute 线路后，本地服务器可以通过公共对等互连访问 Data Lake Store。 有关为公共对等互连配置 ExpressRoute 的详细信息，请参阅[ ExpressRoute 常见问题解答](../expressroute/expressroute-faqs.md)。

## <a name="see-also"></a>另请参阅
* [Overview of Azure Data Lake Store](data-lake-store-overview.md)
* [保护 Azure Data Lake Store 中存储的数据](data-lake-store-security-overview.md)

