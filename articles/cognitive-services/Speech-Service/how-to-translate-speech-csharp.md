---
title: 使用适用于 C# 的语音 SDK 转换语音
titleSuffix: Microsoft Cognitive Services
description: 展示了如何使用适用于 C# 的语音 SDK 转换语音。
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.technology: Speech
ms.topic: article
ms.date: 09/24/2018
ms.author: wolfma
ms.openlocfilehash: 32cbfada359fb39e71abdf1b9ab892a7cd407cc2
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46996666"
---
# <a name="translate-speech-with-the-cognitive-services-speech-sdk-for-c"></a>使用适用于 C# 的认知服务语音 SDK 翻译语音

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-how-to-translate-speech-selector.md)]

[!INCLUDE [Introduction](../../../includes/cognitive-services-speech-service-how-to-translate-speech-intro.md)]

[!INCLUDE [Introduction to top-level declarations](../../../includes/cognitive-services-speech-service-how-to-toplevel-declarations.md)]

[!code-csharp[Top-level declarations](~/samples-cognitive-services-speech-sdk/samples/csharp/sharedcontent/console/translation_samples.cs#toplevel)]

[!INCLUDE [Introduction to using a microphone](../../../includes/cognitive-services-speech-service-how-to-translate-speech-microphone.md)]

[!code-csharp[Translation from a microphone](~/samples-cognitive-services-speech-sdk/samples/csharp/sharedcontent/console/translation_samples.cs#TranslationWithMicrophoneAsync)]

[!INCLUDE [Introduction to using a file](../../../includes/cognitive-services-speech-service-how-to-translate-speech-file.md)]

[!code-csharp[Translation from file input](~/samples-cognitive-services-speech-sdk/samples/csharp/sharedcontent/console/translation_samples.cs#TranslationWithFileAsync)]

[!INCLUDE [Download the sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
在 samples/csharp/sharedcontent/console 文件夹中查找本文中使用的代码。

## <a name="next-steps"></a>后续步骤

- [如何识别语音](how-to-recognize-speech-csharp.md)
- [如何从语音中识别意向](how-to-recognize-intents-from-speech-csharp.md)
