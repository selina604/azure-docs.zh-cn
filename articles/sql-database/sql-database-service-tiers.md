---
title: Azure SQL 数据库购买模型 | Microsoft Docs
description: 了解 Azure SQL 数据库的购买模型。
services: sql-database
author: CarlRabeler
ms.service: sql-database
ms.custom: DBs & servers
ms.topic: conceptual
ms.date: 08/17/2018
manager: craigg
ms.author: carlrab
ms.openlocfilehash: 5fcdf02fe75905fb3e492671ba44adb65dfd0da7
ms.sourcegitcommit: 3f8f973f095f6f878aa3e2383db0d296365a4b18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "42141456"
---
# <a name="azure-sql-database-purchasing-models-and-resources"></a>Azure SQL 数据库购买模型和资源 

使用 Azure SQL 数据库，可以轻松购买适合你的性能和成本要求的完全托管的 PaaS 数据库引擎。 你可以根据 Azure SQL 数据库的部署模型选择适合你的需求的购买模型： 
 - [Azure SQL 数据库](sql-database-technical-overview.md)中的[逻辑服务器](sql-database-logical-servers.md)为计算、存储和 IO 资源提供了两种购买模型：基于 DTU 的购买模型和[基于 vCore 的购买模型](sql-database-service-tiers-vcore.md)。 
 - Azure SQL 数据库中的[托管实例](sql-database-managed-instance.md)仅提供了[基于 vCore 的购买模型](sql-database-service-tiers-vcore.md)。

以下表格和图表对这两种购买模型做了对比。

|**购买模型**|**说明**|**最适用于**|
|---|---|---|
|基于 DTU 的模型|此模型基于计算、存储和 IO 资源的捆绑度量。 单一数据库的性能级别以数据库事务单位 (DTU) 表示，弹性池则以弹性数据库事务单位 (eDTU) 表示。 有关 DTU 和 eDTU 的详细信息，请参阅[什么是 DTU 和 eDTU？](sql-database-service-tiers.md#what-are-database-transaction-units-dtus)|最适合希望获得简单预配置资源选项的客户。| 
|基于 vCore 的模型|此模型允许单独选择计算和存储资源。 此外，它还允许使用面向 SQL Server 的 Azure 混合权益来节省成本。|最适合注重灵活性、控制度和透明度的客户。|
||||  

![定价模型](./media/sql-database-service-tiers/pricing-model.png)

## <a name="vcore-based-purchasing-model"></a>基于 vCore 的购买模型 

虚拟核心表示通过一个选项提供的逻辑 CPU，该选项允许在硬件的层代和硬件的物理特性（例如，核心数、内存、存储大小）之间进行选择。 基于 vCore 的购买模型提供单项资源消耗的灵活性、控制度和透明度，并提供简单明了的方法将本地工作负荷要求转换到云。 此模型允许根据工作负荷需求来选择计算、内存和存储。 在基于 vCore 的购买模型中，客户可为[单一数据库](sql-database-single-database-scale.md)、[托管实例](sql-database-managed-instance.md)和[弹性池](sql-database-elastic-pool.md)选择“[常规用途](sql-database-high-availability.md#standardgeneral-purpose-availability)”或“[业务关键](sql-database-high-availability.md#premiumbusiness-critical-availability)”服务层。 

使用基于 vCore 的购买模型，可以单独选择计算和存储资源，匹配本地性能，以及优化价格。 在基于 vCore 的购买模型中，客户的费用包括：
- 计算（服务层 + vCore 数目和内存量 + 硬件层代）*
- 数据和日志存储的类型与数量 
- IO 数量** - 仅适用于[逻辑服务器](sql-database-logical-servers.md)
- 备份存储 (RA-GRS)** 

\* 在初始公共预览版中，第 4 代逻辑 CPU 基于 Intel E5-2673 v3 (Haswell) 2.4-GHz 处理器。

\*\* 在预览版期间，备份和 IO 免费使用 7 天。

> [!IMPORTANT]
> 计算、IO、数据和日志存储按数据库或弹性池收费。 备份存储按每个数据库收费。 有关托管实例费用的详细信息，请参阅 [Azure SQL 数据库托管实例](sql-database-managed-instance.md)。
> **区域限制：** 基于 vCore 的购买模型在以下区域尚不可用：西欧、法国中部、英国南部、英国西部和澳大利亚东南部。

如果数据库或弹性池消耗的 DTU 超过 300 个，则转换到 vCore 可以降低成本。 可以使用所选的 API 或 Azure 门户进行转换，无需停机。 但是，不一定非要转换。 如果 DTU 购买模型满足性能和业务需求，应继续使用它。 如果决定从 DTU 模型转换到 vCore 模型，应该根据以下经验法则选择性能级别：标准层中的每 100 个 DTU 至少需要常规用途层中的 1 个 vCore，高级层中的每 125 个 DTU 至少需要业务关键层中的 1 个 vCore。

## <a name="dtu-based-purchasing-model"></a>基于 DTU 的购买模型

数据库事务单位 (DTU) 表示 CPU、内存、读取和写入的混合度量。 基于 DTU 的购买模型提供一组预配置的计算资源套件和随附的存储，以促成不同级别的应用程序性能。 偏爱预配置套件简易性和每月定价付款的客户，可能会发现基于 DTU 的模型更适合解决其需求。 在基于 DTU 的购买模型中，客户可为[单一数据库](sql-database-single-database-scale.md)和[弹性池](sql-database-elastic-pool.md)选择“基本”、“标准”或“高级”服务层。 此购买模型在[托管实例](sql-database-managed-instance.md)中不可用。

### <a name="what-are-database-transaction-units-dtus"></a>数据库事务单位 (DTU) 的定义是？
对于[服务层](sql-database-single-database-scale.md)内特定性能级别的单个 Azure SQL 数据库，Microsoft 保证该数据库（独立于 Azure 云中的任何其他数据库）可获得一定级别的资源，从而提供可预测的性能级别。 此资源量是以若干数据库事务单位或 DTU 计算的，是计算资源、存储资源和 IO 资源的捆绑度量值。 这些资源之间的比例最初由 [OLTP 基准工作负荷](sql-database-benchmark-overview.md)确定，该工作负荷是一种典型的真实 OLTP 工作负荷。 工作负荷超过任何以上资源量时，吞吐量将受到限制，从而导致性能下降和超时。 工作负荷使用的资源不会影响 Azure 云中其他 SQL 数据库可用的资源，而其他工作负荷使用的资源也不会影响用户自己的 SQL 数据库可用的资源。

![边界框](./media/sql-database-what-is-a-dtu/bounding-box.png)

要了解 Azure SQL 数据库在不同性能级别和服务层之间的资源相对数量，DTU 将最为有用。 例如，提高数据库的性能级别可使 DTU 加倍，这等同于使该数据库可用的资源集增加一倍。 例如，具有 1750 个 DTU 的高级 P11 数据库提供的 DTU 计算能力是具有 5 个 DTU 的基本数据库的 350 倍。  

若要更深入了解工作负荷的资源 (DTU) 消耗，请使用 [Azure SQL 数据库 Query Performance Insight](sql-database-query-performance.md)：

- 按 CPU/持续时间/执行计数确定热门查询，可以对这些查询进行调整来提高性能。 例如，IO 密集型查询可能会受益于使用[内存中优化技术](sql-database-in-memory.md)，以便在某个特定服务层和性能级别更好地利用可用内存。
- 深入了解查询详情，查看其文本和资源使用历史记录。
- 访问性能优化建议可显示 [SQL 数据库顾问](sql-database-advisor.md)执行的操作。

### <a name="what-are-elastic-database-transaction-units-edtus"></a>弹性数据库事务单位 (eDTU) 的定义是？
可将数据库放在 SQL 数据库服务器上的[弹性池](sql-database-elastic-pool.md)中，该服务器在这些数据库之间共享资源池，而不必为 SQL 数据库提供一组始终可用的专用资源 (DTU)，因为有时可能并不需要。 弹性池中的共享资源用弹性数据库事务单位或 eDTU 度量。 弹性池提供一种简单的低成本高效益的解决方案，用于管理使用模式变化很大且不可预测的多个数据库的性能目标。 弹性池可保证不出现一个数据库使用池中所有资源的情况，同时确保池中的每个数据库始终可以使用最少量的必需资源。 

![SQL 数据库简介：按层和级别统计的 eDTU](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

为池提供的 eDTU 的数量和价格是固定的。 在弹性池中，单个数据库能够在配置的边界范围内灵活自动缩放。 负载较重的数据库消耗较多的 eDTU 来满足需求。 负载较轻的数据库消耗较少的 eDTU。 无负载的数据库不消耗任何 eDTU。 为整个池而不是每个数据库预配资源可以简化管理任务，使池的预算可预测。

可以对现有池增加额外的 eDTU，这不会造成数据库关闭，也不会影响池中的数据库。 同样，随时可以从现有池中删除不再需要的额外 eDTU。 可以在池中添加或删除数据库，或者限制重负载数据库的 eDTU 用量，以便为其他数据库预留 eDTU。 如果可以预见到某个数据库的资源利用率不高，可将其移出池，并使用所需的可预测资源量将它配置为单一数据库。

### <a name="how-can-i-determine-the-number-of-dtus-needed-by-my-workload"></a>如何确定工作负荷所需的 DTU 数？
如果打算将现有的本地或 SQL Server 虚拟机工作负荷迁移到 Azure SQL 数据库，可以使用 [DTU 计算器](http://dtucalculator.azurewebsites.net/) 来估计所需的 DTU 数。 对于现有的 Azure SQL 数据库工作负荷，可以使用 [SQL 数据库 Query Performance Insight](sql-database-query-performance.md) 来了解数据库资源使用量 (DTU)，更深入地了解如何优化工作负荷。 也可以使用 [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV 查看最近一小时的资源消耗。 目录视图 [sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) 也可显示最近 14 天的资源消耗，不过，五分钟平均值的准确性较低。

### <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>如何知道是否可以从资源的弹性池受益？
池适合具有特定使用模式的大量数据库。 对于给定的数据库，此模式的特征是低平均使用量与相对不频繁的使用高峰。 SQL数据库自动评估现有 SQL 数据库服务器中数据库的历史资源使用率，并在 Azure 门户中推荐适当的池配置。 有关详细信息，请参阅[何时使用弹性池？](sql-database-elastic-pool.md)


## <a name="next-steps"></a>后续步骤

- 若要了解基于 vCore 的购买模型，请参阅[基于 vCore 的购买模型](sql-database-service-tiers-vcore.md)
- 有关基于 DTU 的购买模型，请参阅[基于 DTU 的购买模型](sql-database-service-tiers-dtu.md)。
