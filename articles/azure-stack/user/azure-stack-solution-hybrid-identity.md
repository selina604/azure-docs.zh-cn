---
title: 为 Azure 和 Azure Stack 应用程序配置混合云标识 | Microsoft Docs
description: 了解如何为 Azure 和 Azure Stack 应用程序配置混合云标识。
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/28/2018
ms.author: mabrigg
ms.reviewer: Anjay.Ajodha
ms.openlocfilehash: 7cea11f448f20ace2dd50454834e60ce3a3c3b70
ms.sourcegitcommit: 5843352f71f756458ba84c31f4b66b6a082e53df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47584262"
---
# <a name="tutorial-configure-hybrid-cloud-identity-for-azure-and-azure-stack-applications"></a>教程： 配置 Azure 和 Azure Stack 的应用程序的混合云标识

*适用于：Azure Stack 集成系统和 Azure Stack 开发工具包*

了解如何为 Azure 和 Azure Stack 应用程序配置混合云标识。

有两个选项可用来向全球 Azure 和 Azure Stack 中的应用程序授予访问权限。

 * 当 Azure Stack 与 Internet 建立了不间断的连接时，可以使用 Azure Active Directory (Azure AD)。
 * 当 Azure Stack 从 Internet 断开了连接时，可以使用 Azure Directory 联合身份验证服务 (AD FS)。

使用服务主体向 Azure Stack 应用程序授予访问权限，以便在 Azure Stack 中使用 Azure 资源管理器进行部署或配置。

在本教程中，我们将构建一个示例环境来完成以下任务：

> [!div class="checklist"]
> - 在全球 Azure 和 Azure Stack 中建立一个混合标识
> - 检索用于访问 Azure Stack API 的令牌。

必须拥有 Azure Stack 操作员权限才能完成本教程中的步骤。

> [!Tip]  
> ![混合 pillars.png](./media/azure-stack-solution-cloud-burst/hybrid-pillars.png)  
> Microsoft Azure Stack 是 Azure 的扩展。 Azure Stack 提供的敏捷性和创新的云计算到您的本地环境并启用唯一的混合云，可用于生成和部署混合应用任意位置。  
> 
> 本白皮书[混合应用程序的设计注意事项](https://aka.ms/hybrid-cloud-applications-pillars)的设计、 部署和操作混合评审 （放置、 可伸缩性、 可用性、 复原能力、 可管理性和安全性） 的软件质量的构成要素应用程序。 设计注意事项，帮助您优化混合应用程序设计，最大程度减少在生产环境中的挑战。


## <a name="create-a-service-principal-for-azure-ad-in-the-portal"></a>在门户中创建适用于 Azure AD 的服务主体

如果已使用 Azure AD 部署 Azure Stack 作为标识存储，则可以创建服务主体，就像对 Azure 所做的那样。 [创建服务主体](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-azure-ad)一文介绍了如何通过门户执行这些步骤。 在开始之前，请检查是否拥有[所需的 Azure AD 权限](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions)。

## <a name="create-a-service-principal-for-ad-fs-using-powershell"></a>使用 PowerShell 创建适用于 AD FS 的服务主体

如果已使用 AD FS 部署 Azure Stack，则可以使用 PowerShell 创建服务主体、为角色分配访问权限以及使用该标识从 PowerShell 登录。 [创建 AD FS 的服务主体](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-ad-fs)介绍了如何使用 PowerShell 执行所需的步骤。

## <a name="using-the-azure-stack-api"></a>使用 Azure Stack API

[Azure Stack API](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-rest-api-use) 教程演练了检索令牌来访问 Azure Stack API 的过程。

## <a name="connect-to-azure-stack-using-powershell"></a>使用 Powershell 连接到 Azure Stack

[在 Azure Stack 中使用 PowerShell 启动并运行](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-configure-quickstart)快速入门演练了安装 Azure PowerShell 并连接到 Azure Stack 安装所要执行的步骤。

### <a name="prerequisites"></a>必备组件

一个通过你可以访问的订阅连接到 Azure Active Directory 的 Azure Stack 安装。 如果没有 Azure Stack 安装，可以使用这些说明来安装 [Azure Stack 开发工具包](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy)。

#### <a name="connect-to-azure-stack-using-code"></a>使用代码连接到 Azure Stack

若要使用代码连接到 Azure Stack，请使用 Azure 资源管理器终结点 API 来获取 Azure Stack 安装的身份验证和 Graph 终结点，然后使用 REST 请求进行身份验证。 可在 [GitHub](https://github.com/shriramnat/HybridARMApplication) 中找到示例客户端应用程序。

>[!Note]
>除非所选语言的 Azure SDK 支持 Azure API 配置文件，否则 SDK 可能无法与 Azure Stack 一起使用。 有关 Azure API 配置文件的详细信息，请参阅[管理 API 版本配置文件](https://docs.microsoft.com/da-dk/azure/azure-stack/user/azure-stack-version-profiles)一文。

## <a name="next-steps"></a>后续步骤

 - 若要详细了解 Azure Stack 如何处理标识，请参阅 [Azure Stack 的标识体系结构](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-architecture)。
 - 若要了解有关 Azure 云模式的详细信息，请参阅[云设计模式](https://docs.microsoft.com/azure/architecture/patterns)。
