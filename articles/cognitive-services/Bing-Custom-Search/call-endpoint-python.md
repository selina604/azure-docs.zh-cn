---
title: 使用 Python 调用终结点 - 必应自定义搜索 - Microsoft 认知服务
description: 本快速入门演示如何通过使用 Python 调用必应自定义搜索终结点来从自定义搜索实例中请求搜索结果。
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 05/07/2018
ms.author: v-brapel
ms.openlocfilehash: 3666e92372e9bed80e5c0c7991dcac730cebb588
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46967585"
---
# <a name="call-bing-custom-search-endpoint-python"></a>调用必应自定义搜索终结点 (Python)

本快速入门演示如何使用 Python 调用必应自定义搜索终结点来从自定义搜索实例中请求搜索结果。 

## <a name="prerequisites"></a>先决条件

若要完成本快速入门，你需要：

- 现成的自定义搜索实例。 请参阅[创建第一个必应自定义搜索实例](quick-start.md)。
- 安装 [Python](https://www.python.org/)。
- 订阅密钥。 可以在激活[免费试用版](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search)时获取订阅密钥，也可以使用 Azure 仪表板中的付费订阅密钥（请参阅[认知服务 API 帐户](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account)）。    


## <a name="run-the-code"></a>运行代码

若要运行该示例，请遵循以下步骤：

1. 为代码创建文件夹。  
  
2. 从管理员命令提示符或终端处导航至刚刚创建的文件夹。  
  
3. 安装 requests python 模块：  
  
    <pre>
    pip install pipenv
    pipenv install requests
    </pre>  
      
4. 在创建的文件夹中创建 BingCustomSearch.py 文件，并将以下代码复制到其中。 将“YOUR-SUBSCRIPTION-KEY”和“YOUR-CUSTOM-CONFIG-ID”分别替换为订阅密钥和配置 ID。  
  
    ``` Python
    import json
    import requests
    
    subscriptionKey = "YOUR-SUBSCRIPTION-KEY"
    customConfigId = "YOUR-CUSTOM-CONFIG-ID"
    searchTerm = "microsoft"
    
    url = 'https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search?q=' + searchTerm + '&customconfig=' + customConfigId
    r = requests.get(url, headers={'Ocp-Apim-Subscription-Key': subscriptionKey})
    print(r.text)
    ```  
  
7. 使用以下命令运行代码。  
  
    ```
    python BingCustomSearch.py
    ```

## <a name="next-steps"></a>后续步骤
- [配置托管 UI 体验](./hosted-ui.md)
- [使用修饰标记来突出显示文本](./hit-highlighting.md)
- [网页](./page-webpages.md)
