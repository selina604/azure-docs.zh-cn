---
title: Azure Active Directory 中的管理员角色权限 | Microsoft Docs
description: 管理员角色可以添加用户、分配管理角色、重置用户密码、管理用户许可证，或者管理域。
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 09/25/2018
ms.author: curtand
ms.reviewer: vincesm
ms.custom: it-pro
ms.openlocfilehash: 293d8376d83d729588aab0aeaa1040d9b3e5e0b5
ms.sourcegitcommit: 5b8d9dc7c50a26d8f085a10c7281683ea2da9c10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47182274"
---
# <a name="administrator-role-permissions-in-azure-active-directory"></a>Azure Active Directory 中的管理员角色权限

使用 Azure Active Directory (Azure AD) 时，可以指定不同的管理员来执行不同的功能。 可以在 Azure AD 门户中指定管理员用于执行各种任务，例如，添加或更改用户、分配管理角色、重置用户密码、管理用户许可证，以及管理域名。

全局管理员有权使用所有管理功能。 默认情况下，系统会将注册 Azure 订阅的人员指派为目录的全局管理员角色。 只有全局管理员可以委托管理员角色。

## <a name="assign-or-remove-administrator-roles"></a>分配或删除管理员角色

若要了解如何在 Azure Active Directory 中向用户分配管理角色，请参阅[在 Azure Active Directory 中查看和分配管理员角色](directory-manage-roles-portal.md)。

## <a name="available-roles"></a>可用的角色

提供以下管理员角色：

* **[应用程序管理员](#application-administrator)**：此角色中的用户可以创建和管理企业应用程序、应用程序注册和应用程序代理设置的所有方面。 此角色还可以同意委派权限，以及除 Microsoft Graph 和 Azure AD Graph 之外的应用程序权限。 在创建新应用程序注册或企业应用程序时，不会将此角色的成员添加为所有者。

* **[应用程序开发人员](#application-developer)**：在将设置“用户可以注册应用程序”设置为“否”时，此角色中的用户可以创建应用程序注册。 在设置“用户可以同意应用代表他们访问公司数据”设置为“否”时，此角色还使成员能够代表自己授予同意。 在创建新应用程序注册或企业应用程序时，会将此角色的成员添加为所有者。

* **[计费管理员](#billing-administrator)**：进行采购、管理订阅、管理支持票证并监视服务运行状况。

* **[云应用程序管理员](#cloud-application-administrator)**：此角色中的用户具有与应用程序管理员角色相同的权限，但不包括管理应用程序代理的权限。 此角色授予创建和管理企业应用程序和应用程序注册的所有方面的权限。 此角色还可以同意委派权限，以及除 Microsoft Graph 和 Azure AD Graph 之外的应用程序权限。 在创建新应用程序注册或企业应用程序时，不会将此角色的成员添加为所有者。

* **[云设备管理员](#cloud-device-administrator)**：充当此角色的用户可以在 Azure AD 中启用、禁用和删除设备，并可以在 Azure 门户中读取 Windows 10 BitLocker 密钥（如果有）。 该角色不能授予设备上其他任何属性的管理权限。

* **[合规性管理员](#compliance-administrator)**：拥有此角色的用户具有 Office 365 安全与合规中心和 Exchange 管理中心中的管理权限。 有关详细信息，请参阅 [About Office 365 admin roles](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)（关于 Office 365 管理员角色）。

* **[条件访问管理员](#conditional-access-administrator)**：具有此角色的用户可以管理 Azure Active Directory 条件访问设置。
  > [!NOTE]
  > 若要在 Azure 中部署 Exchange ActiveSync 条件访问策略，用户还必须是全局管理员。
  
* **[设备管理员](#device-administrators)**：此角色只能作为[设备设置](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/DevicesMenuBlade/DeviceSettings/menuId/)中的其他本地管理员进行分配。 拥有此角色的用户成为所有已加入 Azure Active Directory 的 Windows 10 设备上的本地计算机管理员。 他们无权管理 Azure Active Directory 中的设备对象。 

* **[目录读取者](#directory-readers)**：这是一个遗留的角色，分配给不支持[许可框架](../develop/quickstart-v1-integrate-apps-with-azure-ad.md)的应用程序。 不应将它分配给任何用户。

* **[目录同步帐户](#directory-synchronization-accounts)**：请勿使用。 此角色自动分配给 Azure AD Connect 服务，不可用于其他任何用途。

* **[目录写入者](#directory-writers)**：这是一个遗留的角色，分配给不支持[许可框架](../develop/quickstart-v1-integrate-apps-with-azure-ad.md)的应用程序。 不应将它分配给任何用户。

* **[Dynamics 365 服务管理员/CRM 服务管理员](#dynamics-365-service-administrator)**：具有此角色的用户在 Microsoft Dynamics 365 Online（如果存在此服务）中拥有全局权限，并可以管理支持票证和监视服务运行状况。 有关详细信息，请参阅[使用服务管理员角色管理租户](https://docs.microsoft.com/dynamics365/customer-engagement/admin/use-service-admin-role-manage-tenant)。

* **[Exchange 服务管理员](#exchange-service-administrator)**：具有此角色的用户在 Microsoft Exchange Online（如果存在此服务）中拥有全局权限。 有关详细信息，请参阅 [About Office 365 admin roles](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)（关于 Office 365 管理员角色）。

* **[全局管理员/公司管理员](#company-administrator)**：具有此角色的用户有权访问 Azure Active Directory 以及使用 Azure Active Directory 标识的服务（例如 Exchange Online、SharePoint Online 和 Skype for Business Online）中的所有管理功能。 注册 Azure Active Directory 租户的人员将成为全局管理员。 只有全局管理员才能分配其他管理员角色。 公司中可以有多个全局管理员。 全局管理员可以为任何用户和所有其他管理员重置密码。

  > [!NOTE]
  > 在 Microsoft 图形 API、Azure AD 图形 API 和 Azure AD PowerShell 中，此角色标识为“公司管理员”。 它是 [Azure 门户](https://portal.azure.com)中的“全局管理员”。
  >
  >

* **[来宾邀请者](#guest-inviter)**：此角色中的用户可以管理 Azure Active Directory B2B 来宾用户邀请当“成员可以邀请”用户设置设置为“否”。 [关于 Azure AD B2B 协作](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)中提供了有关 B2B 协作的详细信息。 它不包括任何其他权限。

* **[信息保护管理员](#information-protection-administrator)**：具有此角色的用户拥有 Azure 信息保护服务中的所有权限。 此角色可以配置 Azure 信息保护策略的标签、管理保护模板，以及激活保护。 此角色不会授予 Identity Protection Center、Privileged Identity Management、监视 Office 365 服务运行状况或 Office 365 安全与合规中心的权限。

* **[Intune 服务管理员](#intune-service-administrator)**：具有此角色的用户在 Microsoft Intune Online（如果存在此服务）中拥有全局权限。 此外，此角色包含管理以关联策略，以及创建和管理组的用户和设备的能力。 有关详细信息，请参阅[使用 Microsoft Intune 进行基于角色的管理控制 (RBAC)](https://docs.microsoft.com/intune/role-based-access-control)

* **[许可证管理员](#license-administrator)**：具有此角色的用户可以添加、删除和更新用户、组（使用基于组的许可）的许可分配，以及管理用户的使用位置。 该角色不授予在使用位置之外购买或管理订阅、创建或管理组，或者创建或管理用户的权限。

* **[消息中心读取者](#message-center-reader)**：具有此角色的用户可以在其组织的 [Office 365 消息中心](https://support.office.com/article/Message-center-in-Office-365-38FB3333-BFCC-4340-A37B-DEDA509C2093)内，监视 Exchange、Intune 和 Microsoft Teams 等已配置服务的通知和公告运行状况更新。 消息中心读者会收到包含帖子和最新动态的每周电子邮件摘要，并能在 Office 365 内共享消息中心帖子。 在 Azure AD 中，分配到此角色的用户对 Azure AD 服务只拥有只读访问权限，如用户和组。 

* **[合作伙伴层 1 支持](#partner-tier1-support)**：请勿使用。 此角色已弃用，并将从 Azure AD 中删除。 此角色仅供少数 Microsoft 转售合作伙伴使用，不适用于一般用途。

* **[合作伙伴层 2 支持](#partner-tier2-support)**：请勿使用。 此角色已弃用，并将从 Azure AD 中删除。 此角色仅供少数 Microsoft 转售合作伙伴使用，不适用于一般用途。

* **[密码管理员/支持管理员](#helpdesk-administrator)**：具有此角色的用户可以更改密码、使刷新令牌失效、管理服务请求和监视服务运行状况。 支持管理员只能为用户和其他支持管理员更改密码和使刷新令牌失效。 使刷新令牌失效会强制用户重新登录。

  > [!NOTE]
  > 在 Microsoft 图形 API、Azure AD 图形 API 和 Azure AD PowerShell 中，此角色标识为“支持管理员”。 它是 [Azure 门户](https://portal.azure.com/)中的“密码管理员”。
  >
  >
  
* **[Power BI 服务管理员](#power-bi-service-administrator)**：具有此角色的用户在 Microsoft Power BI（如果存在此服务）中拥有全局权限，并可以管理支持票证和监视服务运行状况。 有关详细信息，请参阅[了解 Power BI 管理员角色](https://docs.microsoft.com/power-bi/service-admin-role)。

* **[特权角色管理员](#privileged-role-administrator)**：具有此角色的用户可以管理角色分配以及 Azure AD Privileged Identity Management 内的 Azure Active Directory。 此外，此角色允许 Privileged Identity Management 的所有方面。

* **[报告读取者](#reports-reader)**：具有此角色的用户可以在 Office 365 管理中心查看使用情况报告数据和报告仪表板，在 PowerBI 中查看采用上下文包。 此外，此角色还提供对 Azure AD 中的登录报告和活动以及 Microsoft Graph 报告 API 返回的数据的访问权限。 分配到“报告读者”角色的用户只能访问相关使用情况和采用指标。 它们没有任何管理员权限，无法配置设置或访问产品特定的管理中心（如 Exchange）。 

* **[安全管理员](#security-administrator)**：具有此角色的用户具有“安全读取者”角色的所有只读权限，以及能够管理与安全相关的服务配置的能力：Azure Active Directory Identity Protection、Azure 信息保护和 Office 365 安全与合规中心。 [Office 365 安全与合规中心](https://support.office.com/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1)提供了有关 Office 365 权限的详细信息。
  
  | In | 有权执行的操作 |
  | --- | --- |
  | Identity Protection Center |<ul><li>安全读取者角色的所有权限。<li>此外，还能够执行除了重置密码以外的所有 IPC 操作。 |
  | Privileged Identity Management |<ul><li>安全读取者角色的所有权限。<li>**不能**管理 Azure AD 角色成员身份或设置。 |
  | <p>监视 Office 365 服务运行状况</p><p>Office 365 安全与合规中心 |<ul><li>安全读取者角色的所有权限。<li>可以配置高级威胁防护功能中的所有设置（恶意软件和病毒保护、恶意 URL 配置、URL 跟踪等）。 |
  
* **[安全读取者](#security-reader)**：具有此角色的用户具有全局只读访问权限，包括 Azure Active Directory、Identity Protection、Privileged Identity Management，以及能够读取 Azure Active Directory 登录报告和审核日志中的所有信息。 角色还授予 Office 365 安全与合规中心的只读权限。 [Office 365 安全与合规中心](https://support.office.com/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1)提供了有关 Office 365 权限的详细信息。

  | In | 有权执行的操作 |
  | --- | --- |
  | Identity Protection Center |读取安全功能的所有安全报告和设置信息<ul><li>反垃圾邮件<li>加密<li>数据丢失预防<li>反恶意软件<li>高级威胁防护<li>防网络钓鱼<li>邮件流规则 |
  | Privileged Identity Management |<p>以只读方式访问 Azure AD PIM 中所显示的一切信息：Azure AD 角色分配的策略和报告、安全审阅，以及在未来还可通过读取来访问 Azure AD 角色分配以外的方案的策略数据和报告。<p>**不能**注册 Azure AD PIM 或对其进行任何更改。 担任此角色的人员可以在 PIM 的门户中或通过 PowerShell，为其他角色（例如，全局管理员或特权角色管理员）的候选用户激活角色。 |
  | <p>监视 Office 365 服务运行状况</p><p>Office 365 安全与合规中心</p> |<ul><li>读取和管理警报<li>读取安全策略<li>读取威胁情报、云应用发现以及搜索和调查中的隔离区<li>读取所有报告 |

* **[服务支持管理员](#service-support-administrator)**：具有此角色的用户可以打开支持请求与 Microsoft Azure 和 Office 365 服务和服务仪表板和消息中心在 Azure 门户和 Office 365 管理门户中的视图。 有关详细信息，请参阅 [About Office 365 admin roles](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)（关于 Office 365 管理员角色）。

* **[SharePoint 服务管理员](#sharepoint-service-administrator)**：具有此角色的用户在 Microsoft SharePoint Online（如果存在此服务）中拥有全局权限，并可以管理支持票证和监视服务运行状况。 有关详细信息，请参阅 [About Office 365 admin roles](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)（关于 Office 365 管理员角色）。

* **[Skype for Business/Lync 服务管理员](#skype-for-business-administrator)**：具有此角色的用户具有 Microsoft Skype for Business 中的全局权限，以及管理 Azure Active Directory 中的特定于 Skype 的用户属性。 此外，此角色可授予管理支持票证、监视服务运行状况以及访问 Teams 和 Skype for Business 管理中心的能力。 帐户必须获取 Teams 许可证，否则无法运行 Teams PowerShell cmdlet。 有关详细信息，请参阅[关于 Skype for Business 管理员角色](https://support.office.com/article/about-the-skype-for-business-admin-role-aeb35bda-93fc-49b1-ac2c-c74fbeb737b5)；有关 Teams 许可信息，请参阅 [Skype for Business 和 Microsoft Teams 附加许可](https://docs.microsoft.com/skypeforbusiness/skype-for-business-and-microsoft-teams-add-on-licensing/skype-for-business-and-microsoft-teams-add-on-licensing)

  > [!NOTE]
  > 在 Microsoft 图形 API、Azure AD 图形 API 和 Azure AD PowerShell 中，此角色标识为“Lync 服务管理员”。 它是 [Azure 门户](https://portal.azure.com/)中的“Skype for Business 服务管理员”。
  >
  >

* **[Teams 通信管理员](#teams-communications-administrator)**：充当此角色的用户可以管理 Microsoft Teams 工作负荷的语音与电话相关方面。 这包括用于分配电话号码的管理工具、语音和会议策略，以及通话分析工具集的完全访问权限。

* **[Teams 通信支持工程师](#teams-communications-support-engineer)**：充当此角色的用户可以使用 Microsoft Teams 和 Skype for Business 管理中心的用户通话故障排除工具，来排查 Microsoft Teams 和 Skype for Business 中的通信问题。 充当此角色的用户可以查看所有参与方的完整通话记录信息。

* **[Teams 通信支持专家](#teams-communications-support-specialist)**：充当此角色的用户可以使用 Microsoft Teams 和 Skype for Business 管理中心的用户通话故障排除工具，来排查 Microsoft Teams 和 Skype for Business 中的通信问题。 充当此角色的用户只能查看他们所查找的特定用户的通话中的用户详细信息。

* **[Teams 服务管理员](#teams-service-administrator)**：充当此角色的用户可以通过 Microsoft Teams 和 Skype for Business 管理中心以及相应的 PowerShell 模块来管理 Microsoft Teams 工作负荷的所有方面。 这包括（但不限于）与电话、消息、会议和 Teams 自身相关的所有管理工具。 此角色还授予管理 Office 365 组的能力。

* **[用户帐户管理员](#user-account-administrator)**：具有此角色的用户可以创建和管理用户和组的所有方面。 此外，此角色包括管理支持票证的功能，并监视服务运行状况。 适用某些限制。 例如，此角色不允许删除全局管理员。 用户帐户管理员只能更改用户、支持管理员和其他用户帐户管理员的密码以及使刷新令牌失效。 使刷新令牌失效会强制用户重新登录。

| 有权执行的操作 | 无权执行的操作 |
| --- | --- |
| <p>查看公司信息和用户信息</p><p>管理 Office 支持票证</p><p>只能为用户、支持管理员和其他用户帐户管理员更改密码</p><p>创建和管理用户视图</p><p>创建、编辑和删除用户与组，以及管理用户许可证，但有限制。 他/她不能删除全局管理员或创建其他管理员。</p> |<p>为 Office 产品执行计费和采购操作</p><p>管理域</p><p>管理公司信息</p><p>向其他人委派管理角色</p><p>使用目录同步</p><p>启用或禁用多重身份验证</p><p>查看审核日志</p> |

下表描述 Azure Active Directory 中授予每个角色的特定权限。 某些角色可能在 Azure Active Directory 外部的 Microsoft 服务中拥有其他权限。

## <a name="adhoc-license-administrator"></a>即席许可证管理员
可以创建和管理应用注册和企业应用的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/domains/default/read | 读取 Azure Active Directory 中域的基本属性。 |
| microsoft.aad.directory/groups/appRoleAssignments/read | 读取 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/read | 读取 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/memberOf/read | 读取 Azure Active Directory 中的 groups.memberOf 属性。 |
| microsoft.aad.directory/groups/members/read | 读取 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/read | 读取 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/settings/read | 读取 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中 oAuth2PermissionGrants 的基本属性。 |
| microsoft.aad.directory/oAuth2PermissionGrants/update | 更新 Azure Active Directory 中的 oAuth2PermissionGrants。 |
| microsoft.aad.directory/organization/default/read | 读取 Azure Active Directory 中组织的基本属性。 |
| microsoft.aad.directory/organization/trustedCAsForPasswordlessAuth/read | 读取 Azure Active Directory 中的 organization.trustedCAsForPasswordlessAuth 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.directory/users/appRoleAssignments/read | 读取 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/default/read | 读取 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/directReports/read | 读取 Azure Active Directory 中的 users.directReports 属性。 |
| microsoft.aad.directory/users/invitedBy/read | 读取 Azure Active Directory 中的 users.invitedBy 属性。 |
| microsoft.aad.directory/users/invitedUsers/read | 读取 Azure Active Directory 中的 users.invitedUsers 属性。 |
| microsoft.aad.directory/users/manager/read | 读取 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/memberOf/read | 读取 Azure Active Directory 中的 users.memberOf 属性。 |
| microsoft.aad.directory/users/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 users.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/users/ownedDevices/read | 读取 Azure Active Directory 中的 users.ownedDevices 属性。 |
| microsoft.aad.directory/users/ownedObjects/read | 读取 Azure Active Directory 中的 users.ownedObjects 属性。 |
| microsoft.aad.directory/users/registeredDevices/read | 读取 Azure Active Directory 中的 users.registeredDevices 属性。 |

## <a name="application-administrator"></a>应用程序管理员
可以创建和管理应用注册和企业应用的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/applications/audience/update | 更新 Azure Active Directory 中的 applications.audience 属性。 |
| microsoft.aad.directory/applications/authentication/update | 更新 Azure Active Directory 中的 applications.authentication 属性。 |
| microsoft.aad.directory/applications/default/update | 更新 Azure Active Directory 中应用程序的基本属性。 |
| microsoft.aad.directory/applications/create | 在 Azure Active Directory 中创建应用程序。 |
| microsoft.aad.directory/applications/credentials/update | 更新 Azure Active Directory 中的 applications.credentials 属性。 |
| microsoft.aad.directory/applications/delete | 删除 Azure Active Directory 中的应用程序。 |
| microsoft.aad.directory/applications/owners/update | 更新 Azure Active Directory 中的 applications.owners 属性。 |
| microsoft.aad.directory/applications/permissions/update | 更新 Azure Active Directory 中的 applications.permissions 属性。 |
| microsoft.aad.directory/applications/policies/update | 更新 Azure Active Directory 中的 applications.policies 属性。 |
| microsoft.aad.directory/appRoleAssignments/create | 在 Azure Active Directory 中创建 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/read | 读取 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/update | 更新 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/delete | 删除 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/policies/applicationConfiguration/default/read | 读取 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/default/update | 更新 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/create | 在 Azure Active Directory 中创建策略。 |
| microsoft.aad.directory/policies/applicationConfiguration/delete | 删除 Azure Active Directory 中的策略。 |
| microsoft.aad.directory/policies/applicationConfiguration/owners/read | 读取 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/owners/update | 更新 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/policyAppliedTo/read | 读取 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/servicePrincipals/default/update | 更新 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/create | 在 Azure Active Directory 中创建 servicePrincipals。 |
| microsoft.aad.directory/servicePrincipals/delete | 删除 Azure Active Directory 中的 servicePrincipals。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/owners/update | 更新 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/update | 更新 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.reports/allEntities/read | 读取 Azure AD 报告。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="application-developer"></a>应用程序开发人员
可以创建独立于�用户可以注册应用程序�设置的应用程序注册。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/applications/createAsOwner | 在 Azure Active Directory 中创建应用程序。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/appRoleAssignments/createAsOwner | 在 Azure Active Directory 中创建 appRoleAssignments。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/oAuth2PermissionGrants/createAsOwner | 在 Azure Active Directory 中创建 oAuth2PermissionGrants。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/servicePrincipals/createAsOwner | 在 Azure Active Directory 中创建 servicePrincipals。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |

## <a name="billing-administrator"></a>计费管理员
可以执行与常见计费相关的任务，例如更新付款信息。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/organization/default/update | 更新 Azure Active Directory 中组织的基本属性。 |
| microsoft.aad.directory/organization/trustedCAsForPasswordlessAuth/update | 更新 Azure Active Directory 中的 organization.trustedCAsForPasswordlessAuth 属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.commerce.billing/allEntities/allTasks | 管理 Office 365 计费的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="cloud-application-administrator"></a>云应用管理员
可以创建和管理应用注册和企业应用的所有方面，应用代理除外。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/applications/audience/update | 更新 Azure Active Directory 中的 applications.audience 属性。 |
| microsoft.aad.directory/applications/authentication/update | 更新 Azure Active Directory 中的 applications.authentication 属性。 |
| microsoft.aad.directory/applications/default/update | 更新 Azure Active Directory 中应用程序的基本属性。 |
| microsoft.aad.directory/applications/create | 在 Azure Active Directory 中创建应用程序。 |
| microsoft.aad.directory/applications/credentials/update | 更新 Azure Active Directory 中的 applications.credentials 属性。 |
| microsoft.aad.directory/applications/delete | 删除 Azure Active Directory 中的应用程序。 |
| microsoft.aad.directory/applications/owners/update | 更新 Azure Active Directory 中的 applications.owners 属性。 |
| microsoft.aad.directory/applications/permissions/update | 更新 Azure Active Directory 中的 applications.permissions 属性。 |
| microsoft.aad.directory/applications/policies/update | 更新 Azure Active Directory 中的 applications.policies 属性。 |
| microsoft.aad.directory/appRoleAssignments/create | 在 Azure Active Directory 中创建 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/update | 更新 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/delete | 删除 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/policies/applicationConfiguration/create | 在 Azure Active Directory 中创建策略。 |
| microsoft.aad.directory/policies/applicationConfiguration/default/read | 读取 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/default/update | 更新 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/delete | 删除 Azure Active Directory 中的策略。 |
| microsoft.aad.directory/policies/applicationConfiguration/owners/read | 读取 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/owners/update | 更新 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/policies/applicationConfiguration/policyAppliedTo/read | 读取 Azure Active Directory 中的 policies.applicationConfiguration 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/default/update | 更新 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/create | 在 Azure Active Directory 中创建 servicePrincipals。 |
| microsoft.aad.directory/servicePrincipals/delete | 删除 Azure Active Directory 中的 servicePrincipals。 |
| microsoft.aad.directory/servicePrincipals/owners/update | 更新 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/update | 更新 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.reports/allEntities/read | 读取 Azure AD 报告。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="cloud-device-administrator"></a>云设备管理员
用于在 Azure AD 中管理设备的完全访问权限。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/devices/delete | 删除 Azure Active Directory 中的设备。 |
| microsoft.aad.directory/devices/disable | 禁用 Azure Active Directory 中的设备。 |
| microsoft.aad.directory/devices/enable | 启用 Azure Active Directory 中的设备。 |
| microsoft.aad.reports/allEntities/read | 读取 Azure AD 报告。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |

## <a name="company-administrator"></a>公司管理员
可以管理 Azure AD 和使用 Azure AD 标识的 Microsoft 服务的所有方面。

  > [!NOTE]
  > 此角色从角色中继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/administrativeUnits/allProperties/allTasks | 创建和删除 administrativeUnits，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/applications/allProperties/allTasks | 创建和删除应用程序，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/appRoleAssignments/allProperties/allTasks | 创建和删除 appRoleAssignments，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/contacts/allProperties/allTasks | 创建和删除联系人，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/contracts/allProperties/allTasks | 创建和删除协定，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/devices/allProperties/allTasks | 创建和删除设备，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/directoryRoles/allProperties/allTasks | 创建和删除 directoryRoles，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/directoryRoleTemplates/allProperties/allTasks | 创建和删除 directoryRoleTemplates，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/domains/allProperties/allTasks | 创建和删除域，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/groups/allProperties/allTasks | 创建和删除组，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/groupSettings/allProperties/allTasks | 创建和删除 groupSettings，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/groupSettingTemplates/allProperties/allTasks | 创建和删除 groupSettingTemplates，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/loginTenantBranding/allProperties/allTasks | 创建和删除 loginTenantBranding，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/oAuth2PermissionGrants/allProperties/allTasks | 创建和删除 oAuth2PermissionGrants，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/organization/allProperties/allTasks | 创建和删除组织，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/policies/allProperties/allTasks | 创建和删除策略，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/roleAssignments/allProperties/allTasks | 创建和删除 roleAssignments，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/roleDefinitions/allProperties/allTasks | 创建和删除 roleDefinitions，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/scopedRoleMemberships/allProperties/allTasks | 创建和删除 scopedRoleMemberships，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/serviceAction/activateService | 可以在 Azure Active Directory 中执行 Activateservice 服务操作 |
| microsoft.aad.directory/serviceAction/disableDirectoryFeature | 可以在 Azure Active Directory 中执行 Disabledirectoryfeature 服务操作 |
| microsoft.aad.directory/serviceAction/enableDirectoryFeature | 可以在 Azure Active Directory 中执行 Enabledirectoryfeature 服务操作 |
| microsoft.aad.directory/serviceAction/getAvailableExtentionProperties | 可以在 Azure Active Directory 中执行 Getavailableextentionproperties 服务操作 |
| microsoft.aad.directory/servicePrincipals/allProperties/allTasks | 创建和删除 servicePrincipals，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/subscribedSkus/allProperties/allTasks | 创建和删除 subscribedSkus，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directory/users/allProperties/allTasks | 创建和删除用户，然后读取和更新 Azure Active Directory 中的所有属性。 |
| microsoft.aad.directorySync/allEntities/allTasks | 在 Azure AD Connect 中执行所有操作。 |
| microsoft.aad.identityProtection/allEntities/allTasks | 创建和删除所有资源，然后读取和更新 microsoft.aad.identityProtection 中的标准属性。 |
| microsoft.aad.privilegedIdentityManagement/allEntities/read | 读取 microsoft.aad.privilegedIdentityManagement 中的所有资源。 |
| microsoft.aad.reports/allEntities/allTasks | 读取和配置 Azure AD 报告。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.informationProtection/allEntities/allTasks | 管理 Azure 信息保护的各个方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.commerce.billing/allEntities/allTasks | 管理 Office 365 计费的各个方面。 |
| microsoft.intune/allEntities/allTasks | 管理 Intune 的各个方面。 |
| microsoft.office365.complianceManager/allEntities/allTasks | 管理 Office 365 合规性管理器的各个方面 |
| microsoft.office365.exchange/allEntities/allTasks | 管理 Exchange Online 的各个方面。 |
| microsoft.office365.lockbox/allEntities/allTasks | 管理 Office 365 客户密码箱的各个方面 |
| microsoft.powerApps.powerBI/allEntities/allTasks | 管理 Power BI 的各个方面。 |
| microsoft.office365.protectionCenter/allEntities/allTasks | 管理 Office 365 防护中心的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.sharepoint/allEntities/allTasks | 创建和删除所有资源，然后读取和更新 microsoft.office365.sharepoint 中的标准属性。 |
| microsoft.office365.skypeForBusiness/allEntities/allTasks | 管理 Skype for Business Online 的各个方面。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |
| microsoft.powerApps.dynamics365/allEntities/allTasks | 管理 Dynamics 365 的各个方面。 |

## <a name="compliance-administrator"></a>符合性管理员
可以读取和管理 Azure AD 和 Office 365 中的符合性配置和报表。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.complianceManager/allEntities/allTasks | 管理 Office 365 合规性管理器的各个方面 |
| microsoft.office365.exchange/allEntities/allTasks | 管理 Exchange Online 的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.sharepoint/allEntities/allTasks | 创建和删除所有资源，然后读取和更新 microsoft.office365.sharepoint 中的标准属性。 |
| microsoft.office365.skypeForBusiness/allEntities/allTasks | 管理 Skype for Business Online 的各个方面。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="conditional-access-administrator"></a>条件访问管理员
可以管理条件访问功能。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/policies/conditionalAccess/default/read | 读取 Azure Active Directory 中的 policies.conditionalAccess 属性。 |
| microsoft.aad.directory/policies/conditionalAccess/default/update | 更新 Azure Active Directory 中的 policies.conditionalAccess 属性。 |
| microsoft.aad.directory/policies/conditionalAccess/create | 在 Azure Active Directory 中创建策略。 |
| microsoft.aad.directory/policies/conditionalAccess/delete | 删除 Azure Active Directory 中的策略。 |
| microsoft.aad.directory/policies/conditionalAccess/owners/read | 读取 Azure Active Directory 中的 policies.conditionalAccess 属性。 |
| microsoft.aad.directory/policies/conditionalAccess/owners/update | 更新 Azure Active Directory 中的 policies.conditionalAccess 属性。 |
| microsoft.aad.directory/policies/conditionalAccess/policiesAppliedTo/read | 读取 Azure Active Directory 中的 policies.conditionalAccess 属性。 |

## <a name="customer-lockbox-access-approver"></a>客户密码箱访问审批者
可以批准 Microsoft 支持人员访问客户组织数据的请求。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.office365.lockbox/allEntities/allTasks | 管理 Office 365 客户密码箱的各个方面 |

## <a name="device-administrators"></a>设备管理员
此角色的成员将添加到已加入 Azure AD 的设备上的本地管理员组。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/groupSettings/default/read | 读取 Azure Active Directory 中 groupSettings 的基本属性。 |
| microsoft.aad.directory/groupSettingTemplates/default/read | 读取 Azure Active Directory 中 groupSettingTemplates 的基本属性。 |

## <a name="device-managers"></a>设备管理器
可以批准 Microsoft 支持人员访问客户组织数据的请求。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/devices/default/read | 读取 Azure Active Directory 中设备的基本属性。 |
| microsoft.aad.directory/devices/default/update | 更新 Azure Active Directory 中设备的基本属性。 |
| microsoft.aad.directory/devices/memberOf/read | 读取 Azure Active Directory 中的 devices.memberOf 属性。 |
| microsoft.aad.directory/devices/registeredOwners/read | 读取 Azure Active Directory 中的 devices.registeredOwners 属性。 |
| microsoft.aad.directory/devices/registeredOwners/update | 更新 Azure Active Directory 中的 devices.registeredOwners 属性。 |
| microsoft.aad.directory/devices/registeredUsers/read | 读取 Azure Active Directory 中的 devices.registeredUsers 属性。 |
| microsoft.aad.directory/devices/registeredUsers/update | 更新 Azure Active Directory 中的 devices.registeredUsers 属性。 |

## <a name="directory-readers"></a>目录读者
可以读取基本目录信息。 授予应用程序访问权限

  > [!NOTE]
  > 此角色从角色中继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/administrativeUnits/default/read | 读取 Azure Active Directory 中 administrativeUnits 的基本属性。 |
| microsoft.aad.directory/administrativeUnits/members/read | 读取 Azure Active Directory 中的 administrativeUnits.members 属性。 |
Azure Active Directory。 |
| microsoft.aad.directory/applications/default/read | 读取 Azure Active Directory 中应用程序的基本属性。 |
| microsoft.aad.directory/applications/owners/read | 读取 Azure Active Directory 中的 applications.owners 属性。 |
| microsoft.aad.directory/contacts/default/read | 读取 Azure Active Directory 中联系人的基本属性。 |
| microsoft.aad.directory/contacts/memberOf/read | 读取 Azure Active Directory 中的 contacts.memberOf 属性。 |
| microsoft.aad.directory/contracts/default/read | 读取 Azure Active Directory 中协定的基本属性。 |
| microsoft.aad.directory/devices/default/read | 读取 Azure Active Directory 中设备的基本属性。 |
| microsoft.aad.directory/devices/memberOf/read | 读取 Azure Active Directory 中的 devices.memberOf 属性。 |
| microsoft.aad.directory/devices/registeredOwners/read | 读取 Azure Active Directory 中的 devices.registeredOwners 属性。 |
| microsoft.aad.directory/devices/registeredUsers/read | 读取 Azure Active Directory 中的 devices.registeredUsers 属性。 |
| microsoft.aad.directory/directoryRoles/default/read | 读取 Azure Active Directory 中 directoryRoles 的基本属性。 |
| microsoft.aad.directory/directoryRoles/eligibleMembers/read | 读取 Azure Active Directory 中的 directoryRoles.eligibleMembers 属性。 |
| microsoft.aad.directory/directoryRoles/members/read | 读取 Azure Active Directory 中的 directoryRoles.members 属性。 |
| microsoft.aad.directory/domains/default/read | 读取 Azure Active Directory 中域的基本属性。 |
| microsoft.aad.directory/groups/appRoleAssignments/read | 读取 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/read | 读取 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/memberOf/read | 读取 Azure Active Directory 中的 groups.memberOf 属性。 |
| microsoft.aad.directory/groups/members/read | 读取 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/read | 读取 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/settings/read | 读取 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/groupSettings/default/read | 读取 Azure Active Directory 中 groupSettings 的基本属性。 |
| microsoft.aad.directory/groupSettingTemplates/default/read | 读取 Azure Active Directory 中 groupSettingTemplates 的基本属性。 |
| microsoft.aad.directory/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中 oAuth2PermissionGrants 的基本属性。 |
| microsoft.aad.directory/organization/default/read | 读取 Azure Active Directory 中组织的基本属性。 |
| microsoft.aad.directory/organization/trustedCAsForPasswordlessAuth/read | 读取 Azure Active Directory 中的 organization.trustedCAsForPasswordlessAuth 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/read | 读取 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/read | 读取 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/default/read | 读取 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/memberOf/read | 读取 Azure Active Directory 中的 servicePrincipals.memberOf 属性。 |
| microsoft.aad.directory/servicePrincipals/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 servicePrincipals.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/servicePrincipals/ownedObjects/read | 读取 Azure Active Directory 中的 servicePrincipals.ownedObjects 属性。 |
| microsoft.aad.directory/servicePrincipals/owners/read | 读取 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/read | 读取 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directory/subscribedSkus/default/read | 读取 Azure Active Directory 中 subscribedSkus 的基本属性。 |
| microsoft.aad.directory/users/appRoleAssignments/read | 读取 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/default/read | 读取 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/directReports/read | 读取 Azure Active Directory 中的 users.directReports 属性。 |
| microsoft.aad.directory/users/invitedBy/read | 读取 Azure Active Directory 中的 users.invitedBy 属性。 |
| microsoft.aad.directory/users/invitedUsers/read | 读取 Azure Active Directory 中的 users.invitedUsers 属性。 |
| microsoft.aad.directory/users/manager/read | 读取 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/memberOf/read | 读取 Azure Active Directory 中的 users.memberOf 属性。 |
| microsoft.aad.directory/users/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 users.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/users/ownedDevices/read | 读取 Azure Active Directory 中的 users.ownedDevices 属性。 |
| microsoft.aad.directory/users/ownedObjects/read | 读取 Azure Active Directory 中的 users.ownedObjects 属性。 |
| microsoft.aad.directory/users/registeredDevices/read | 读取 Azure Active Directory 中的 users.registeredDevices 属性。 |

## <a name="directory-synchronization-accounts"></a>目录同步帐户
仅供 Azure AD Connect 服务使用。

  > [!NOTE]
  > 此角色从角色中继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/organization/dirSync/update | 更新 Azure Active Directory 中的 organization.dirSync 属性。 |
| microsoft.aad.directory/policies/create | 在 Azure Active Directory 中创建策略。 |
| microsoft.aad.directory/policies/delete | 删除 Azure Active Directory 中的策略。 |
| microsoft.aad.directory/policies/default/read | 读取 Azure Active Directory 中策略的基本属性。 |
| microsoft.aad.directory/policies/default/update | 更新 Azure Active Directory 中策略的基本属性。 |
| microsoft.aad.directory/policies/owners/read | 读取 Azure Active Directory 中的 policies.owners 属性。 |
| microsoft.aad.directory/policies/owners/update | 更新 Azure Active Directory 中的 policies.owners 属性。 |
| microsoft.aad.directory/policies/policiesAppliedTo/read | 读取 Azure Active Directory 中的 policies.policiesAppliedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/read | 读取 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/read | 读取 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/default/read | 读取 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/default/update | 更新 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/create | 在 Azure Active Directory 中创建 servicePrincipals。 |
| microsoft.aad.directory/servicePrincipals/memberOf/read | 读取 Azure Active Directory 中的 servicePrincipals.memberOf 属性。 |
| microsoft.aad.directory/servicePrincipals/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 servicePrincipals.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/servicePrincipals/owners/read | 读取 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/owners/update | 更新 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/ownedObjects/read | 读取 Azure Active Directory 中的 servicePrincipals.ownedObjects 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/read | 读取 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/update | 更新 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directorySync/allEntities/allTasks | 在 Azure AD Connect 中执行所有操作。 |

## <a name="directory-writers"></a>目录编写人员
可以读取和写入基本目录信息。 授予应用程序访问权限

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/groups/create | 在 Azure Active Directory 中创建组。 |
| microsoft.aad.directory/groups/createAsOwner | 在 Azure Active Directory 中创建组。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/groups/appRoleAssignments/update | 更新 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/update | 更新 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/members/update | 更新 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/update | 更新 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/settings/update | 更新 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/groupSettings/default/update | 更新 Azure Active Directory 中 groupSettings 的基本属性。 |
| microsoft.aad.directory/groupSettings/create | 在 Azure Active Directory 中创建 groupSettings 属性。 |
| microsoft.aad.directory/groupSettings/delete | 删除 Azure Active Directory 中的 groupSettings。 |
| microsoft.aad.directory/users/appRoleAssignments/update | 更新 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.directory/users/default/update | 更新 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/invalidateAllRefreshTokens | 使 Azure Active Directory 中的所有用户刷新令牌无效。 |
| microsoft.aad.directory/users/manager/update | 更新 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/userPrincipalName/update | 更新 Azure Active Directory 中的 users.userPrincipalName 属性。 |

## <a name="dynamics-365-administrator"></a>Dynamics 365 管理员
可以管理 Dynamics 365 产品的所有方面。 前称为 CRM 服务管理员。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.powerApps.dynamics365/allEntities/allTasks | 管理 Dynamics 365 的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="exchange-service-administrator"></a>Exchange 服务管理员
可以管理 Exchange 产品的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.exchange/allEntities/allTasks | 管理 Exchange Online 的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="guest"></a>来宾
来宾用户的默认角色。 可以读取一组有限的目录信息。

  > [!NOTE]
  > 此角色从“用户”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/applications/default/read | 读取 Azure Active Directory 中应用程序的基本属性。 |
| microsoft.aad.directory/applications/owners/read | 读取 Azure Active Directory 中的 applications.owners 属性。 |
| microsoft.aad.directory/domains/default/read | 读取 Azure Active Directory 中域的基本属性。 |
| microsoft.aad.directory/groups/appRoleAssignments/read | 读取 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/read | 读取 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/memberOf/read | 读取 Azure Active Directory 中的 groups.memberOf 属性。 |
| microsoft.aad.directory/groups/members/read | 读取 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/read | 读取 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/settings/read | 读取 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/organization/basicProfile/read | 读取 Azure Active Directory 中的基本组织配置文件信息。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/read | 读取 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/read | 读取 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/default/read | 读取 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/memberOf/read | 读取 Azure Active Directory 中的 servicePrincipals.memberOf 属性。 |
| microsoft.aad.directory/servicePrincipals/members/read | 读取 Azure Active Directory 中的 servicePrincipals.members 属性。 |
| microsoft.aad.directory/servicePrincipals/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 servicePrincipals.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/servicePrincipals/owners/read | 读取 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/ownedObjects/read | 读取 Azure Active Directory 中的 servicePrincipals.ownedObjects 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/read | 读取 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directory/users/basicProfile/read | 读取 Azure Active Directory 中的 users.basicProfile 属性。 |
| microsoft.aad.directory/users/appRoleAssignments/read | 读取 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/default/read | 读取 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/directReports/read | 读取 Azure Active Directory 中的 users.directReports 属性。 |
| microsoft.aad.directory/users/eligibleMemberOf/read | 读取 Azure Active Directory 中的 users.eligibleMemberOf 属性。 |
| microsoft.aad.directory/users/invitedBy/read | 读取 Azure Active Directory 中的 users.invitedBy 属性。 |
| microsoft.aad.directory/users/invitedUsers/read | 读取 Azure Active Directory 中的 users.invitedUsers 属性。 |
| microsoft.aad.directory/users/manager/read | 读取 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/memberOf/read | 读取 Azure Active Directory 中的 users.memberOf 属性。 |
| microsoft.aad.directory/users/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 users.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/users/ownedDevices/read | 读取 Azure Active Directory 中的 users.ownedDevices 属性。 |
| microsoft.aad.directory/users/ownedObjects/read | 读取 Azure Active Directory 中的 users.ownedObjects 属性。 |
| microsoft.aad.directory/users/password/update | 更新 Azure Active Directory 中所有用户的密码。 有关详细信息，请参阅联机文档。 |
| microsoft.aad.directory/users/pendingMemberOf/read | 读取 Azure Active Directory 中的 users.pendingMemberOf 属性。 |
| microsoft.aad.directory/users/registeredDevices/read | 读取 Azure Active Directory 中的 users.registeredDevices 属性。 |
| microsoft.aad.directory/users/scopedAdministratorOf/read | 读取 Azure Active Directory 中的 users.scopedAdministratorOf 属性。 |

## <a name="guest-inviter"></a>来宾邀请者
可以独立于“成员可以邀请来宾”设置来邀请来宾用户。

  > [!NOTE]
  > 此角色从“用户”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/users/appRoleAssignments/read | 读取 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/default/read | 读取 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/directReports/read | 读取 Azure Active Directory 中的 users.directReports 属性。 |
| microsoft.aad.directory/users/invitedBy/read | 读取 Azure Active Directory 中的 users.invitedBy 属性。 |
| microsoft.aad.directory/users/inviteGuest | 邀请 Azure Active Directory 中的来宾用户。 |
| microsoft.aad.directory/users/invitedUsers/read | 读取 Azure Active Directory 中的 users.invitedUsers 属性。 |
| microsoft.aad.directory/users/manager/read | 读取 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/memberOf/read | 读取 Azure Active Directory 中的 users.memberOf 属性。 |
| microsoft.aad.directory/users/oAuth2PermissionGrants/default/read | 读取 Azure Active Directory 中的 users.oAuth2PermissionGrants 属性。 |
| microsoft.aad.directory/users/ownedDevices/read | 读取 Azure Active Directory 中的 users.ownedDevices 属性。 |
| microsoft.aad.directory/users/ownedObjects/read | 读取 Azure Active Directory 中的 users.ownedObjects 属性。 |
| microsoft.aad.directory/users/registeredDevices/read | 读取 Azure Active Directory 中的 users.registeredDevices 属性。 |

## <a name="helpdesk-administrator"></a>支持管理员
可以重置非管理员和支持理员的密码。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/users/invalidateAllRefreshTokens | 使 Azure Active Directory 中的所有用户刷新令牌无效。 |
| microsoft.aad.directory/users/password/update | 更新 Azure Active Directory 中所有用户的密码。 有关详细信息，请参阅联机文档。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="information-protection-administrator"></a>信息保护管理员
可以管理 Azure 信息保护产品的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.informationProtection/allEntities/allTasks | 管理 Azure 信息保护的各个方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="intune-service-administrator"></a>Intune 服务管理员
可以管理 Intune 产品的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/contacts/default/update | 更新 Azure Active Directory 中联系人的基本属性。 |
| microsoft.aad.directory/contacts/create | 在 Azure Active Directory 中创建联系人。 |
| microsoft.aad.directory/contacts/delete | 删除 Azure Active Directory 中的联系人。 |
| microsoft.aad.directory/devices/default/update | 更新 Azure Active Directory 中设备的基本属性。 |
| microsoft.aad.directory/devices/create | 在 Azure Active Directory 中创建设备。 |
| microsoft.aad.directory/devices/delete | 删除 Azure Active Directory 中的设备。 |
| microsoft.aad.directory/devices/registeredOwners/update | 更新 Azure Active Directory 中的 devices.registeredOwners 属性。 |
| microsoft.aad.directory/devices/registeredUsers/update | 更新 Azure Active Directory 中的 devices.registeredUsers 属性。 |
| microsoft.aad.directory/groups/appRoleAssignments/update | 更新 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/update | 更新 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/create | 在 Azure Active Directory 中创建组。 |
| microsoft.aad.directory/groups/createAsOwner | 在 Azure Active Directory 中创建组。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/groups/delete | 删除 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/hiddenMembers/read | 读取 Azure Active Directory 中的 groups.hiddenMembers 属性。 |
| microsoft.aad.directory/groups/members/update | 更新 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/update | 更新 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/restore | 还原 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/settings/update | 更新 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/users/appRoleAssignments/update | 更新 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/default/update | 更新 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/manager/update | 更新 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.intune/allEntities/allTasks | 管理 Intune 的各个方面。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="license-administrator"></a>许可证管理员
可以管理用户和组的产品许可证。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.directory/users/usageLocation/update | 更新 Azure Active Directory 中的 users.usageLocation 属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |

## <a name="message-center-reader"></a>消息中心读取者
只能在 Office 365 消息中心查看其组织的消息和更新。 

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.accessmessagecenter/allEntities/allTasks | 创建和删除所有资源，然后读取和更新消息中心中的标准属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |

## <a name="partner-tier1-support"></a>合作伙伴一线支持人员
不要使用 - 不适用于常规用途。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/contacts/default/update | 更新 Azure Active Directory 中联系人的基本属性。 |
| microsoft.aad.directory/contacts/create | 在 Azure Active Directory 中创建联系人。 |
| microsoft.aad.directory/contacts/delete | 删除 Azure Active Directory 中的联系人。 |
| microsoft.aad.directory/groups/create | 在 Azure Active Directory 中创建组。 |
| microsoft.aad.directory/groups/createAsOwner | 在 Azure Active Directory 中创建组。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/groups/members/update | 更新 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/update | 更新 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/users/appRoleAssignments/update | 更新 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.directory/users/default/update | 更新 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/delete | 删除 Azure Active Directory 中的用户。 |
| microsoft.aad.directory/users/invalidateAllRefreshTokens | 使 Azure Active Directory 中的所有用户刷新令牌无效。 |
| microsoft.aad.directory/users/manager/update | 更新 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/password/update | 更新 Azure Active Directory 中所有用户的密码。 有关详细信息，请参阅联机文档。 |
| microsoft.aad.directory/users/restore | 还原 Azure Active Directory 中已删除的用户。 |
| microsoft.aad.directory/users/userPrincipalName/update | 更新 Azure Active Directory 中的 users.userPrincipalName 属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="partner-tier2-support"></a>合作伙伴二线支持人员
不要使用 - 不适用于常规用途。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/contacts/default/update | 更新 Azure Active Directory 中联系人的基本属性。 |
| microsoft.aad.directory/contacts/create | 在 Azure Active Directory 中创建联系人。 |
| microsoft.aad.directory/contacts/delete | 删除 Azure Active Directory 中的联系人。 |
| microsoft.aad.directory/domains/allTasks | 创建和删除域，然后读取和更新 Azure Active Directory 中的标准属性。 |
| microsoft.aad.directory/groups/create | 在 Azure Active Directory 中创建组。 |
| microsoft.aad.directory/groups/delete | 删除 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/members/update | 更新 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/restore | 还原 Azure Active Directory 中的组。 |
| microsoft.aad.directory/organization/default/update | 更新 Azure Active Directory 中组织的基本属性。 |
| microsoft.aad.directory/organization/trustedCAsForPasswordlessAuth/update | 更新 Azure Active Directory 中的 organization.trustedCAsForPasswordlessAuth 属性。 |
| microsoft.aad.directory/users/appRoleAssignments/update | 更新 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.directory/users/default/update | 更新 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/delete | 删除 Azure Active Directory 中的用户。 |
| microsoft.aad.directory/users/invalidateAllRefreshTokens | 使 Azure Active Directory 中的所有用户刷新令牌无效。 |
| microsoft.aad.directory/users/manager/update | 更新 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/password/update | 更新 Azure Active Directory 中所有用户的密码。 有关详细信息，请参阅联机文档。 |
| microsoft.aad.directory/users/restore | 还原 Azure Active Directory 中已删除的用户。 |
| microsoft.aad.directory/users/userPrincipalName/update | 更新 Azure Active Directory 中的 users.userPrincipalName 属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="power-bi-service-administrator"></a>Power BI 服务管理员
可以管理 Power BI 产品的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.powerApps.powerBI/allEntities/allTasks | 管理 Power BI 的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="privileged-role-administrator"></a>特权角色管理员
可以管理 Azure AD 中的角色分配

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/directoryRoles/update | 更新 Azure Active Directory 中的 directoryRoles。 |
| microsoft.aad.privilegedIdentityManagement/allEntities/allTasks | 创建和删除所有资源，然后读取和更新 microsoft.aad.privilegedIdentityManagement 中的标准属性。 |

## <a name="reports-reader"></a>报告读者
可以读取登录和审核报告。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.reports/allEntities/read | 读取 Azure AD 报告。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.usageReports/allEntities/read | 阅读 Office 365 使用情况报告。 |

## <a name="security-administrator"></a>安全管理员
可以读取安全信息和报告

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/applications/policies/update | 更新 Azure Active Directory 中的 applications.policies 属性。 |
| microsoft.aad.directory/policies/default/update | 更新 Azure Active Directory 中策略的基本属性。 |
| microsoft.aad.directory/policies/create | 在 Azure Active Directory 中创建策略。 |
| microsoft.aad.directory/policies/delete | 删除 Azure Active Directory 中的策略。 |
| microsoft.aad.directory/policies/owners/update | 更新 Azure Active Directory 中的 policies.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/update | 更新 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.identityProtection/allEntities/read | 读取 microsoft.aad.identityProtection 中的所有资源。 |
| microsoft.aad.identityProtection/allEntities/update | 更新 microsoft.aad.identityProtection 中的所有资源。 |
| microsoft.aad.privilegedIdentityManagement/allEntities/read | 读取 microsoft.aad.privilegedIdentityManagement 中的所有资源。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.protectionCenter/allEntities/read | 读取 Office 365 防护中心的各个方面。 |
| microsoft.office365.protectionCenter/allEntities/update | 更新 microsoft.office365.protectionCenter 中的所有资源。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |

## <a name="security-reader"></a>安全读取者
可以读取 Azure AD 和 Office 365 中的安全信息和报表。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.identityProtection/allEntities/read | 读取 microsoft.aad.identityProtection 中的所有资源。 |
| microsoft.aad.privilegedIdentityManagement/allEntities/read | 读取 microsoft.aad.privilegedIdentityManagement 中的所有资源。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.protectionCenter/allEntities/read | 读取 Office 365 防护中心的各个方面。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |

## <a name="service-support-administrator"></a>服务支持管理员
可以读取服务运行状况信息和管理支持票证。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="sharepoint-service-administrator"></a>SharePoint 服务管理员
可以管理 SharePoint 服务的所有方面。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.sharepoint/allEntities/allTasks | 创建和删除所有资源，然后读取和更新 microsoft.office365.sharepoint 中的标准属性。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="skype-for-business-administrator"></a>Skype for Business 管理员
可以管理 Skype for Business 产品的所有方面。 前称为 Lync 服务管理员。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.skypeForBusiness/allEntities/allTasks | 管理 Skype for Business Online 的各个方面。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="teams-communications-administrator"></a>Teams 通信管理员
可以管理 Microsoft Teams 服务中的通话和会议功能。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/policies/basic/read | 读取 Azure Active Directory 中策略的基本属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |
| microsoft.office365.usageReports/allEntities/read | 阅读 Office 365 使用情况报告。 |

## <a name="teams-communications-support-engineer"></a>Teams 通信支持工程师
可以使用高级工具排查 Teams 中的通信问题。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/policies/basic/read | 读取 Azure Active Directory 中策略的基本属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |

## <a name="teams-communications-support-specialist"></a>Teams 通信支持专家
可以使用基本工具排查 Teams 中的通信问题。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/policies/basic/read | 读取 Azure Active Directory 中策略的基本属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |

## <a name="teams-service-administrator"></a>Teams 服务管理员
可以管理 Microsoft Teams 服务。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

  > [!NOTE]
  > 此角色拥有 Azure Active Directory 外部的其他权限。 有关详细信息，请参阅上面的角色说明。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/groups/hiddenMembers/read | 读取 Azure Active Directory 中的 groups.hiddenMembers 属性。 |
| microsoft.aad.directory/policies/basic/read | 读取 Azure Active Directory 中策略的基本属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |
| microsoft.office365.usageReports/allEntities/read | 阅读 Office 365 使用情况报告。 |

## <a name="user-account-administrator"></a>用户帐户管理员
可以管理用户与组的所有方面

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/appRoleAssignments/create | 在 Azure Active Directory 中创建 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/delete | 删除 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/appRoleAssignments/update | 更新 Azure Active Directory 中的 appRoleAssignments。 |
| microsoft.aad.directory/contacts/default/update | 更新 Azure Active Directory 中联系人的基本属性。 |
| microsoft.aad.directory/contacts/create | 在 Azure Active Directory 中创建联系人。 |
| microsoft.aad.directory/contacts/delete | 删除 Azure Active Directory 中的联系人。 |
| microsoft.aad.directory/groups/appRoleAssignments/update | 更新 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/update | 更新 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/create | 在 Azure Active Directory 中创建组。 |
| microsoft.aad.directory/groups/createAsOwner | 在 Azure Active Directory 中创建组。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/groups/delete | 删除 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/hiddenMembers/read | 读取 Azure Active Directory 中的 groups.hiddenMembers 属性。 |
| microsoft.aad.directory/groups/members/update | 更新 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/update | 更新 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/restore | 还原 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/settings/update | 更新 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/users/appRoleAssignments/update | 更新 Azure Active Directory 中的 users.appRoleAssignments 属性。 |
| microsoft.aad.directory/users/assignLicense | 管理 Azure Active Directory 中用户的许可证。 |
| microsoft.aad.directory/users/default/update | 更新 Azure Active Directory 中用户的基本属性。 |
| microsoft.aad.directory/users/create | 在 Azure Active Directory 中创建用户。 |
| microsoft.aad.directory/users/delete | 删除 Azure Active Directory 中的用户。 |
| microsoft.aad.directory/users/invalidateAllRefreshTokens | 使 Azure Active Directory 中的所有用户刷新令牌无效。 |
| microsoft.aad.directory/users/manager/update | 更新 Azure Active Directory 中的 users.manager 属性。 |
| microsoft.aad.directory/users/password/update | 更新 Azure Active Directory 中所有用户的密码。 有关详细信息，请参阅联机文档。 |
| microsoft.aad.directory/users/restore | 还原 Azure Active Directory 中已删除的用户。 |
| microsoft.aad.directory/users/userPrincipalName/update | 更新 Azure Active Directory 中的 users.userPrincipalName 属性。 |
| microsoft.azure.accessService/allEntities/allTasks | 管理 Azure 访问服务的所有方面。 |
| microsoft.azure.serviceHealth/allEntities/allTasks | 读取和配置 Azure 服务运行状况。 |
| microsoft.azure.supportTickets/allEntities/allTasks | 创建和管理 Azure 支持票证。 |
| microsoft.office365.serviceHealth/allEntities/allTasks | 读取和配置 Office 365 服务运行状况。 |
| microsoft.office365.supportTickets/allEntities/allTasks | 创建和管理 Office 365 支持票证。 |

## <a name="user"></a>用户
成员用户的默认角色。 可以读取所有目录信息并写入一组有限的目录信息。

  > [!NOTE]
  > 此角色从“目录读取者”角色继承其他权限。
  >
  >

| **操作** | **说明** |
| --- | --- |
| microsoft.aad.directory/applications/createAsOwner | 在 Azure Active Directory 中创建应用程序。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/groups/default/read | 读取 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/createAsOwner | 在 Azure Active Directory 中创建组。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/oAuth2PermissionGrants/create | 在 Azure Active Directory 中创建 oAuth2PermissionGrants。 |
| microsoft.aad.directory/oAuth2PermissionGrants/delete | 删除 Azure Active Directory 中的 oAuth2PermissionGrants。 |
| microsoft.aad.directory/oAuth2PermissionGrants/update | 更新 Azure Active Directory 中的 oAuth2PermissionGrants。 |
| microsoft.aad.directory/servicePrincipals/createAsOwner | 在 Azure Active Directory 中创建 servicePrincipals。 添加创建者作为第一个所有者，创建的对象根据创建者的 250 个创建对象配额计数。 |
| microsoft.aad.directory/users/activateServicePlan | Azure Active Directory 中的 Activateserviceplan 用户。 |
| microsoft.aad.directory/users/inviteGuest | 邀请 Azure Active Directory 中的来宾用户。 |
| microsoft.aad.directory/applications/default/update | 更新 Azure Active Directory 中应用程序的基本属性。 |
| microsoft.aad.directory/applications/delete | 删除 Azure Active Directory 中的应用程序。 |
| microsoft.aad.directory/applications/owners/update | 更新 Azure Active Directory 中的 applications.owners 属性。 |
| microsoft.aad.directory/applications/permissions/update | 更新 Azure Active Directory 中的 applications.permissions 属性。 |
| microsoft.aad.directory/applications/policies/update | 更新 Azure Active Directory 中的 applications.policies 属性。 |
| microsoft.aad.directory/applications/restore | 还原 Azure Active Directory 中的应用程序。 |
| microsoft.aad.directory/devices/disable | 禁用 Azure Active Directory 中的设备。 |
| microsoft.aad.directory/groups/appRoleAssignments/update | 更新 Azure Active Directory 中的 groups.appRoleAssignments 属性。 |
| microsoft.aad.directory/groups/default/update | 更新 Azure Active Directory 中组的基本属性。 |
| microsoft.aad.directory/groups/delete | 删除 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/dynamicMembershipRule/update | 更新 Azure Active Directory 中的 groups.dynamicMembershipRule 属性。 |
| microsoft.aad.directory/groups/members/update | 更新 Azure Active Directory 中的 groups.members 属性。 |
| microsoft.aad.directory/groups/owners/update | 更新 Azure Active Directory 中的 groups.owners 属性。 |
| microsoft.aad.directory/groups/restore | 还原 Azure Active Directory 中的组。 |
| microsoft.aad.directory/groups/settings/update | 更新 Azure Active Directory 中的 groups.settings 属性。 |
| microsoft.aad.directory/policies/default/update | 更新 Azure Active Directory 中策略的基本属性。 |
| microsoft.aad.directory/policies/delete | 删除 Azure Active Directory 中的策略。 |
| microsoft.aad.directory/policies/owners/update | 更新 Azure Active Directory 中的 policies.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignedTo/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignedTo 属性。 |
| microsoft.aad.directory/servicePrincipals/appRoleAssignments/update | 更新 Azure Active Directory 中的 servicePrincipals.appRoleAssignments 属性。 |
| microsoft.aad.directory/servicePrincipals/default/update | 更新 Azure Active Directory 中 servicePrincipals 的基本属性。 |
| microsoft.aad.directory/servicePrincipals/delete | 删除 Azure Active Directory 中的 servicePrincipals。 |
| microsoft.aad.directory/servicePrincipals/owners/update | 更新 Azure Active Directory 中的 servicePrincipals.owners 属性。 |
| microsoft.aad.directory/servicePrincipals/policies/update | 更新 Azure Active Directory 中的 servicePrincipals.policies 属性。 |
| microsoft.aad.directory/users/changePassword | 更改 Azure Active Directory 中所有用户的密码。 有关详细信息，请参阅联机文档。 |
| microsoft.aad.directory/users/invalidateAllRefreshTokens | 使 Azure Active Directory 中的所有用户刷新令牌无效。 |
| microsoft.aad.directory/users/basicProfile/update | 更新 Azure Active Directory 中的 users.basicProfile 属性。 |
| microsoft.aad.directory/users/mobile/update | 更新 Azure Active Directory 中的 users.mobile 属性。 |
| microsoft.aad.directory/users/searchableDeviceKey/update | 更新 Azure Active Directory 中的 users.searchableDeviceKey 属性。 |

## <a name="deprecated-roles"></a>已弃用的角色

不应使用以下角色。 这些角色已弃用，并将从 Azure AD 中删除。

* 即席许可证管理员
* 设备联接
* 设备管理器
* 设备用户
* 经电子邮件验证的用户创建者
* 邮箱管理员
* 工作区设备联接

## <a name="next-steps"></a>后续步骤

* 若要详细了解如何将用户分配为 Azure 订阅的管理员，请参阅[使用 RBAC 和 Azure 门户管理访问权限](../../role-based-access-control/role-assignments-portal.md)
* 若要了解有关如何在 Microsoft Azure 中控制资源访问的详细信息，请参阅 [了解 Azure 中的资源访问权限](../../role-based-access-control/rbac-and-directory-admin-roles.md)
* 有关 Azure Active Directory 如何与 Azure 订阅相关联的详细信息，请参阅 [How Azure subscriptions are associated with Azure Active Directory](../fundamentals/active-directory-how-subscriptions-associated-directory.md)（Azure 订阅与 Azure Active Directory 的关联方式）
