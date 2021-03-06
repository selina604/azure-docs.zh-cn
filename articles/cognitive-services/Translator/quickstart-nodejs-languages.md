---
title: 文本翻译使用 Node.js 获取支持的语言 | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: 在本快速入门中，你将获得翻译、音译和查询字典支持的语言列表以及在认知服务中将文本翻译 API 与 Node.js 配合使用的示例。
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/21/2018
ms.author: nolachar
ms.openlocfilehash: dd37aab3707c6f06b8cc2e942366e19746694252
ms.sourcegitcommit: 65b399eb756acde21e4da85862d92d98bf9eba86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2018
ms.locfileid: "43768673"
---
# <a name="quickstart-get-supported-languages-with-nodejs"></a>快速入门：使用 Node.js 获取支持的语言

在本快速入门中，你将获得翻译、音译和查询字典支持的语言列表以及使用文本翻译 API 的示例。

## <a name="prerequisites"></a>先决条件

需要使用 [Node.js 6](https://nodejs.org/en/download/) 运行此代码。

若要使用文本翻译 API，还需要订阅密钥；请参阅[如何注册文本翻译 API](translator-text-how-to-signup.md)。

## <a name="languages-request"></a>Languages 请求

以下代码使用 [Languages](./reference/v3-0-languages.md) 方法获取翻译、音译、查询字典支持的语言列表和示例。

1. 在喜欢使用的代码编辑器中新建一个 Node.js 项目。
2. 添加以下提供的代码。
3. 使用对订阅有效的访问密钥替换 `subscriptionKey` 值。
4. 运行该程序。

```javascript
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'api.cognitive.microsofttranslator.com';
let path = '/languages?api-version=3.0';

let output_path = 'output.txt';
let ws = fs.createWriteStream(output_path);

let response_handler = function (response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
        let json = JSON.stringify(JSON.parse(body), null, 4);
        ws.write (json);
        ws.close ();
        console.log("File written.");

    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let GetLanguages = function () {
    let request_params = {
        method : 'GET',
        hostname : host,
        path : path,
        headers : {
            'Ocp-Apim-Subscription-Key' : subscriptionKey,
        }
    };

    let req = https.request (request_params, response_handler);
    req.end ();
}

GetLanguages ();
```

## <a name="languages-response"></a>Languages 响应

在 JSON 中返回成功的响应，如以下示例所示：

```json
{
  "translation": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr"
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl"
    },
...
  },
  "transliteration": {
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "scripts": [
        {
          "code": "Arab",
          "name": "Arabic",
          "nativeName": "العربية",
          "dir": "rtl",
          "toScripts": [
            {
              "code": "Latn",
              "name": "Latin",
              "nativeName": "اللاتينية",
              "dir": "ltr"
            }
          ]
        },
        {
          "code": "Latn",
          "name": "Latin",
          "nativeName": "اللاتينية",
          "dir": "ltr",
          "toScripts": [
            {
              "code": "Arab",
              "name": "Arabic",
              "nativeName": "العربية",
              "dir": "rtl"
            }
          ]
        }
      ]
    },
...
  },
  "dictionary": {
    "af": {
      "name": "Afrikaans",
      "nativeName": "Afrikaans",
      "dir": "ltr",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
    "ar": {
      "name": "Arabic",
      "nativeName": "العربية",
      "dir": "rtl",
      "translations": [
        {
          "name": "English",
          "nativeName": "English",
          "dir": "ltr",
          "code": "en"
        }
      ]
    },
...
  }
}
```

## <a name="next-steps"></a>后续步骤

浏览此快速入门的示例代码和其他内容，包括翻译和音译，以及 GitHub 上的其他示例文本翻译项目。

> [!div class="nextstepaction"]
> [浏览 GitHub 上的 Node.js 示例](https://aka.ms/TranslatorGitHub?type=&language=javascript)
