---
title: 定价和计费 - Azure 逻辑应用 | Microsoft Docs
description: 了解 Azure 逻辑应用的定价和计费原理
services: logic-apps
ms.service: logic-apps
ms.suite: logic-apps
author: kevinlam1
ms.author: klam
ms.reviewer: estfan, LADocs
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.topic: article
ms.date: 09/24/2018
ms.openlocfilehash: b75fba2ba0e9fa922b1252378e0bab326cada7d2
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46974300"
---
# <a name="pricing-model-for-azure-logic-apps"></a>Azure 逻辑应用的定价模型

可以在云中使用 Azure 逻辑应用创建和运行可自动缩放的集成工作流。 下面是有关逻辑应用计费和定价方式的详细信息。 

<a name="consumption-pricing"></a>

## <a name="consumption-pricing-model"></a>消耗量定价模型

对于通过使用公共或“全局”逻辑应用服务创建的新逻辑应用，只需根据自己的使用量付费即可。 这些逻辑应用使用基于消耗量的计划和定价模型，这意味着，将会计量逻辑应用执行的所有操作。 逻辑应用定义中的每个步骤都是一个操作，包括触发器、控制流步骤、对内置操作的调用，以及对连接器的调用。 有关详细信息，请参阅[逻辑应用定价](https://azure.microsoft.com/pricing/details/logic-apps)。

<a name="fixed-pricing"></a>

## <a name="fixed-pricing-model"></a>固定定价模型

> [!NOTE]
> 集成服务环境位于个人预览版中。 若要请求访问权限，[请在此处创建加入请求](https://aka.ms/iseprivatepreview)。

对于使用[*集成服务环境* (ISE)](../logic-apps/connect-virtual-network-vnet-isolated-environment-overview.md) 创建的新逻辑应用（使用专用资源的专用独立逻辑应用实例），需为内置操作和标有 ISE 的标准连接器支付固定月度价格。 ISE 包括一个免费的企业连接器，而其他企业连接器基于企业消耗量价格收费。 有关详细信息，请参阅[逻辑应用定价](https://azure.microsoft.com/pricing/details/logic-apps)。

<a name="triggers"></a>

## <a name="triggers"></a>触发器

触发器是发生特定事件时创建逻辑应用实例的特殊操作。 触发器以不同方式起作用，从而影响逻辑应用的计量方式。

* **轮询触发器** - 此触发器持续检查终结点是否收到满足创建逻辑应用实例和启动工作流的条件的消息。 每个轮询请求算作一次执行并进行计量，即使未创建任何逻辑应用实例也是如此。 若要指定轮询间隔，请通过逻辑应用程序设计器设置触发器。

  [!INCLUDE [logic-apps-polling-trigger-non-standard-metering](../../includes/logic-apps-polling-trigger-non-standard-metering.md)]

* **Webhook 触发器** – 此触发器等待客户端向特定的终结点发送请求。 发送到 webhook 终结点的每个请求都会计为操作执行。 例如，请求和 HTTP Webhook 触发器都是 Webhook 触发器。

* **定期触发器** – 此触发器基于在触发器中设置的重复间隔创建逻辑应用实例。 例如，可以设置每隔三天运行的，或者根据更复杂的计划运行的定期触发器。

可以在“触发器历史记录”部分下的逻辑应用“概述”窗格中找到触发器执行。

## <a name="actions"></a>操作

内置操作（例如，调用 HTTP、Azure Functions 或 API 管理的操作，以及控制流步骤）被计量为本机操作，具有各自的类型。 调用[连接器](https://docs.microsoft.com/connectors)的操作为“ApiConnection”类型。 这些连接器分类为标准或企业连接器，根据各自的[定价][pricing]进行计量。 

所有成功和不成功的运行操作统计且计量为操作执行。 但是，由于不满足条件而跳过的操作或者由于逻辑应用在完成之前已终止而未运行的操作不会统计为操作执行。 已禁用的逻辑应用无法实例化新实例，因此，在禁用后不会产生费用

> [!NOTE]
> 禁用逻辑应用后，当前正在运行的实例可能需要在一段时间之后才会完全停止。

在循环中运行的操作根据循环中的每个周期统计。 例如，“for each”循环中用于处理包含 10 个项的列表的单个操作的统计方式是：将列表项数 (10) 乘以循环中的操作数 (1) 加上一个用于启动循环的操作。 因此，对于本示例，计算公式是 (10 * 1) + 1，即 11 个操作执行。

## <a name="integration-account-usage"></a>集成帐户使用情况

基于消耗量的使用情况包括一个[集成帐户](logic-apps-enterprise-integration-create-integration-account.md)，可用于免费浏览、开发和测试逻辑应用中的 [B2B/EDI](logic-apps-enterprise-integration-b2b.md) 和 [XML 处理](logic-apps-enterprise-integration-xml.md)功能。 你可以为每个区域配置一个集成帐户，并存储[特定数量的项目](../logic-apps/logic-apps-limits-and-config.md)，如 EDI 贸易合作伙伴和协议、地图、架构、程序集、证书和批处理配置。

逻辑应用还以支持的逻辑应用 SLA 提供基本和标准集成帐户。 如果只想使用消息处理，或要充当与大型企业实体建立贸易合作关系的小型企业合作伙伴，可以使用基本集成帐户。 标准集成帐户支持更复杂的 B2B 关系，并增加了可以管理的实体数。 有关详细信息，请参阅 [Azure 定价](https://azure.microsoft.com/pricing/details/logic-apps)。

## <a name="next-steps"></a>后续步骤

* [了解有关逻辑应用的详细信息][whatis]
* [创建第一个逻辑应用][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-overview.md
[create]: quickstart-create-first-logic-app-workflow.md

