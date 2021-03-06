---
title: 使用 b2clogin.com | Microsoft Docs
description: 了解如何使用 b2clogin.com 而不是 login.microsoftonline.com。
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/29/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 6ad0a5d59b28bf48742c9e1be89b51d2301dd582
ms.sourcegitcommit: 63613e4c7edf1b1875a2974a29ab2a8ce5d90e3b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2018
ms.locfileid: "43189284"
---
# <a name="using-b2clogincom"></a>使用 b2clogin.com

>[!IMPORTANT]
>此功能以公共预览版提供。 
>

现在，你可以选择使用带有 `<YourTenantName>.b2clogin.com` 的 Azure AD B2C 服务，而不是使用 `login.microsoftonline.com`。  这样做有诸多好处：
* 将不再与其他 Microsoft 产品共享相同的 Cookie 标头大小限制。
* 可以在 URL 中删除对 Microsoft 的所有引用（可以将 `<YourTenantName>.onmicrosoft.com` 替换为你的租户 ID）。 例如：`https://<tenantname>.b2clogin.com/tfp/<tenantID>/<policyname>/v2.0/.well-known/openid-configuration`。

 为了利用 b2clogin.com，你需要设置以下某些内容：

1. 对于“立即运行终结点”，请确保使用的是 `<YourTenantName>.b2clogin.com` 而不是 `login.microsoftonline.com`。
2. 如果使用的是 MSAL，则需要设置 `validateauthority=false`。  这是因为令牌颁发者成为 `<YourTenantName>.b2clogin.com`。
