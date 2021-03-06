---
title: 开始在 Node 中使用 Azure 中继混合连接 Websocket | Microsoft Docs
description: 为 Azure 中继混合连接 Websocket 编写 Node.js 控制台应用程序
services: service-bus-relay
documentationcenter: node
author: spelluru
manager: timlt
editor: ''
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 05/02/2018
ms.author: spelluru
ms.openlocfilehash: 25e9095561f72583bad86aa96b64a412e0983ab6
ms.sourcegitcommit: cb61439cf0ae2a3f4b07a98da4df258bfb479845
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2018
ms.locfileid: "43702351"
---
# <a name="get-started-with-relay-hybrid-connections-websockets-in-node"></a>开始在 Node 中使用中继混合连接 Websocket

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

本教程简单介绍了 [Azure 中继混合连接](relay-what-is-it.md#hybrid-connections) Websocket 功能，同时介绍了如何使用 Node.js 创建客户端应用程序，以便将 Websocket 消息发送到相应的侦听器应用程序。

## <a name="what-will-be-accomplished"></a>将要完成的任务

由于混合连接要求客户端和服务器组件，请在本教程中创建两个控制台应用程序。 下面是相关步骤：

1. 使用 Azure 门户创建中继命名空间。
2. 使用 Azure 门户创建混合连接。
3. 编写服务器控制台应用程序用于接收消息。
4. 编写客户端控制台应用程序用于发送消息。

## <a name="prerequisites"></a>先决条件

1. [Node.js](https://nodejs.org/en/)。
2. Azure 订阅。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a>1.使用 Azure 门户创建命名空间

如果已创建中继命名空间，请跳转到[使用 Azure 门户创建混合连接](#2-create-a-hybrid-connection-using-the-azure-portal)部分。

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a>2.使用 Azure 门户创建混合连接

如果已创建混合连接，请跳转到[创建服务器应用程序](#3-create-a-server-application-listener)部分。

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3.创建服务器应用程序（侦听程序）

若要侦听和接收来自中继的消息，请编写 Node.js 控制台应用程序。

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4.创建客户端应用程序（发送程序）

若要将消息发送到中继，请编写 Node.js 控制台应用程序。

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a>5.运行应用程序

1. 运行服务器应用程序：在 Node.js 命令提示符处，键入 `node listener.js`。
2. 运行客户端应用程序：在 Node.js 命令提示符处键入 `node sender.js`，然后输入某些文本。
3. 确保服务器应用程序控制台输出了客户端应用程序中输入的文本。

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

祝贺你，现已使用 Node.js 创建端到端混合连接应用程序！

## <a name="next-steps"></a>后续步骤

* [中继常见问题](relay-faq.md)
* [创建命名空间](relay-create-namespace-portal.md)
* [.NET 入门](relay-hybrid-connections-dotnet-get-started.md)
* [节点入门](relay-hybrid-connections-node-get-started.md)

