---
title: 使用 Node.js 在语言理解(LUIS) 中分析自然语言文本 - 认知服务 - Azure 认知服务 | Microsoft Docs
description: 本快速入门使用可用的公共 LUIS 应用从会话文本中确定用户的意向。 使用 Node.js 将用户的意向作为文本发送到公共应用的 HTTP 预测终结点。 在终结点处，LUIS 应用公共应用的模型来分析自然语言文本的含义，确定总体意向并提取与应用的主题域相关的数据。
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: b85b8ef19d4cc46d80d600d1cb4404edd71e2374
ms.sourcegitcommit: 2d961702f23e63ee63eddf52086e0c8573aec8dd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2018
ms.locfileid: "44158001"
---
# <a name="quickstart-analyze-text-using-nodejs"></a>快速入门：使用 Node.js 分析文本

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

## <a name="prerequisites"></a>先决条件

* [Node.js](https://nodejs.org/) 编程语言 
* [Visual Studio Code](https://code.visualstudio.com/)
* 公共应用 ID：df67dcdb-c37d-46af-88e1-8b97951ca1c2


> [!NOTE] 
> [LUIS-Samples Github 存储库](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/analyze-text/node)中提供了完整的 Node.js 解决方案。

## <a name="get-luis-key"></a>获取 LUIS 密钥

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a>使用浏览器分析文本

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-nodejs"></a>使用 Node.js 分析文本

可以使用 Node.js 来访问上一步骤中浏览器窗口显示的相同结果。

1. 复制以下代码片段：

   [!code-nodejs[Console app code that calls a LUIS endpoint for Node.js](~/samples-luis/documentation-samples/quickstarts/analyze-text/node/call-endpoint.js)]

2. 创建包含以下文本的 `.env` 文件，或者在系统环境中设置以下变量：

    ```CMD
    LUIS_APP_ID=df67dcdb-c37d-46af-88e1-8b97951ca1c2
    LUIS_ENDPOINT_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    ```

3. 将 `LUIS_ENDPOINT_KEY` 环境变量设置为你的密钥。

4. 通过在命令行上运行以下命令来安装依赖项：`npm install`。

5. 通过 `npm start` 运行代码。 其中会显示前面在浏览器窗口中显示的相同值。

## <a name="luis-keys"></a>LUIS 密钥

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a>清理资源

删除 Node.js 文件。

## <a name="next-steps"></a>后续步骤
> [!div class="nextstepaction"]
> [添加表达](luis-get-started-node-add-utterance.md)