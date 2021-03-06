---
title: Azure Active Directory 代码示例 | Microsoft Docs
description: 提供可用 Azure Active Directory（V2 终结点）代码示例的索引，这些示例按方案进行组织。
services: active-directory
documentationcenter: dev-center-name
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/24/2018
ms.author: celested
ms.reviewer: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e76097c0d0cbaf14f2fc2b1a407bc2d320a2091d
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46964377"
---
# <a name="azure-active-directory-code-samples-v2-endpoint"></a>Azure Active Directory 代码示例（V2 终结点）

[!INCLUDE [active-directory-develop-applies-v2-msal](../../../includes/active-directory-develop-applies-v2-msal.md)]

可以使用 Microsoft Azure Active Directory (Azure AD)：

- 向 Web 应用程序和 Web API 添加身份验证和授权。
- 要求使用访问令牌来访问受保护的 Web API。

本文简要介绍 Azure AD V2 终结点示例并提供指向这些示例的链接。 这些示例将展示其工作原理以及可以在应用程序中使用的代码片段。 在代码示例页上，可以找到在要求、安装和设置方面提供帮助的详细自述主题。 代码中的注释可帮助你理解关键部分。

> [!NOTE]
> 如果对 V1 示例感兴趣，请参阅 [Azure AD 代码示例（V1 终结点）](sample-v1-code.md)。

若要了解每种示例类型的基本方案，请参阅 [Azure Active Directory v2.0 终结点的应用类型](v2-app-types.md)。

你也可以为 GitHub 上的示例做出补充。 若要了解如何操作，请参阅 [Microsoft Azure Active Directory 示例和文档](https://github.com/Azure-Samples?page=3&query=active-directory)。

## <a name="single-page-applications-spa"></a>单页应用程序 (SPA)

此示例展示了如何编写受 Azure AD 保护的单页应用程序。 这些示例使用 MSAL.js 的其中一种风格：[用于 JavaScript 的 Microsoft 身份验证库](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-core)、[用于 Angular 的 Microsoft 身份验证库](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular)、[用于 AngularJS 的 Microsoft 身份验证库](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angularjs)

 平台 |  调用 Microsoft Graph
 -------- |  ---------------------
![JavaScript](media/sample-v2-code/logo_js.png) JavaScript (msal.js)  | [javascript-graphapi-web-v2](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2)
![Angular JS](media/sample-v2-code/logo_angular.png) JavaScript (msal AngularJS) | [MsalAngularjsDemoApp](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-angularjs/samples/MsalAngularjsDemoApp)
![Angular](media/sample-v2-code/logo_angular.png) JavaScript (msal Angular) | [MSALAngularDemoApp](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-angular/samples/MSALAngularDemoApp)

## <a name="web-applications"></a>Web 应用程序

以下示例演示了将用户登录的 Web 应用。 一些示例还演示了使用用户标识调用 Microsoft Graph 或你自己的 Web API 的应用程序。

 平台 | 仅让用户登录 | 让用户登录并调用 Microsoft Graph
 -------- | ------------------- | ---------------------------------
![ASP.NET](media/sample-v2-code/logo_NETframework.png)<p/> ASP.NET | [appmodelv2-webapp-openIDConnect-dotNet](https://GitHub.com/AzureAdQuickstarts/AppModelv2-WebApp-OpenIDConnect-DotNet) <p/> [dotnet-webapp-openidconnect-v2](https://GitHub.com/azure-samples/active-directory-dotnet-webapp-openidconnect-v2)  |              [aspnet-connect-rest-sample](https://github.com/microsoftgraph/aspnet-connect-rest-sample)
![ASP.NET](media/sample-v2-code/logo_NETcore.png)<p/>ASP.NET Core 2.0 | [aspnetcore-webapp-openidconnect-v2](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2) |              [aspnetcore-connect-sample](https://github.com/microsoftgraph/aspnetcore-connect-sample)
![Node.js](media/sample-v2-code/logo_nodejs.png)  |                   | [AppModelv2-WebApp-OpenIDConnect-nodejs](https://github.com/azureadquickstarts/appmodelv2-webapp-openidconnect-nodejs)
![Ruby](media/sample-v2-code/logo_ruby.png) |                   | [ruby-connect-rest-sample](https://github.com/microsoftgraph/ruby-connect-rest-sample)

## <a name="desktop-and-mobile-public-client-apps"></a>桌面和移动公共客户端应用

以下示例展示了以用户身份使用交互式登录访问 Microsoft Graph 或你自己的 Web API 的公共客户端应用程序（桌面/移动应用程序）。 所有这些客户端应用程序均使用 MicroSoft 身份验证库 (MSAL)

客户端应用程序 | 平台 | 调用 Microsoft Graph | 调用 ASP.NET Core 2.0 Web API
------------------ | -------- |  -------------------- | -------------------------
桌面 (WPF)      | ![.NET/C#](media/sample-v2-code/logo_NET.png) | [dotnet-desktop-msgraph-v2](http://github.com/azure-samples/active-directory-dotnet-desktop-msgraph-v2) <p/> [dotnet-admin-restricted-scopes-v2](https://github.com/azure-samples/active-directory-dotnet-admin-restricted-scopes-v2) | [dotnet-native-aspnetcore-v2](https://GitHub.com/azure-samples/active-directory-dotnet-native-aspnetcore-v2)
移动 (UWP)   | ![.NET/C# (UWP)](media/sample-v2-code/logo_windows.png) | [dotnet-native-uwp-v2](https://github.com/azure-samples/active-directory-dotnet-native-uwp-v2) |
移动（Android、iOS、UWP）   | ![.NET/C# (Xamarin)](media/sample-v2-code/logo_xamarin.png) | [xamarin-native-v2](https://Github.com/azure-samples/active-directory-xamarin-native-v2) |
移动 (iOS)       | ![iOS / Objective C 或 swift](media/sample-v2-code/logo_iOS.png) | [ios-swift-native-v2](https://github.com/azure-samples/active-directory-ios-swift-native-v2) <p/> [ios-native-nxoauth2-v2](https://github.com/azure-samples/active-directory-ios-native-nxoauth2-v2) |
移动 (Android)   | ![Android / Java](media/sample-v2-code/logo_Android.png) |   [android-native-v2](https://github.com/azure-samples/active-directory-android-native-v2 ) |

## <a name="daemon-applications"></a>守护程序应用程序

下面的示例是一个应用程序，它使用自己的标识（没有用户）访问 Microsoft Graph。

客户端应用程序 | 平台 | 流/授权 | 调用 Microsoft Graph
------------------ | -------- | ---------- | --------------------
Web 应用 | ![ASP.NET](media/sample-v2-code/logo_NETframework.png)<p/> ASP.NET  | 客户端凭据 | [dotnet-daemon-v2](https://github.com/azure-samples/active-directory-dotnet-daemon-v2)

> 显示桌面守护应用程序的示例位于待办事项列表中。

## <a name="web-apis"></a>Web API

以下示例展示了如何使用 Azure AD V2 终结点保护 Web API。 此 API 由 WPF 应用程序执行（但可以由任何应用程序实际调用）

平台 | 示例
 -------- | -------------------
![.NET/C#](media/sample-v2-code/logo_NET.png) | [dotnet-native-aspnetcore-v2](https://GitHub.com/azure-samples/active-directory-dotnet-native-aspnetcore-v2)

## <a name="other-microsoft-graph-samples"></a>其他 Microsoft Graph 示例

若要了解演示 Microsoft Graph API 的各种使用模式（包括向 Azure AD 进行身份验证）的[示例](https://github.com/microsoftgraph/msgraph-community-samples/tree/master/samples#aspnet)和教程，请参阅 [Microsoft Graph Community samples & tutorials](https://github.com/microsoftgraph/msgraph-community-samples)（Microsoft Graph 社区示例和教程）。

## <a name="see-also"></a>另请参阅

[Azure Active Directory 开发人员指南](azure-ad-developers-guide.md)

[Azure AD 图形 API 概念和参考](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Azure AD 图形 API 帮助程序库](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
