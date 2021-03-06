---
title: 如何使用 Azure 门户管理用户分配的托管标识
description: 分步说明如何创建、列出和删除用户分配的托管标识以及如何为其分配角色。
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/16/2018
ms.author: daveba
ms.openlocfilehash: bdbe15a85ad4d2ef6918b7ab7e16942edde5096e
ms.sourcegitcommit: ad08b2db50d63c8f550575d2e7bb9a0852efb12f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47220313"
---
# <a name="create-list-delete-or-assign-a-role-to-a-user-assigned-managed-identity-using-the-azure-portal"></a>使用 Azure 门户创建、列出和删除用户分配的托管标识以及为其分配角色

[!INCLUDE [preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Azure 资源的托管标识在 Azure Active Directory 中为 Azure 服务提供了一个托管标识。 此标识可用于向支持 Azure AD 身份验证的服务进行身份验证，这样就无需在代码中输入凭据了。 

本文介绍如何使用 Azure 门户创建、列出和删除用户分配的托管标识以及如何为其分配角色。

## <a name="prerequisites"></a>先决条件

- 如果不熟悉 Azure 资源的托管标识，请查阅[概述部分](overview.md)。 请务必了解[系统分配的托管标识与用户分配的托管标识之间的差异](overview.md#how-does-it-work)。
- 如果没有 Azure 帐户，请在继续前[注册免费帐户](https://azure.microsoft.com/free/)。
- 若要执行本文中的管理操作，帐户需要分配以下角色：
    - [托管标识参与者](/azure/role-based-access-control/built-in-roles#managed-identity-contributor)角色，可以创建、读取（列出）、更新和删除用户分配的托管标识。
    - [托管标识操作员](/azure/role-based-access-control/built-in-roles#managed-identity-operator)角色，可以读取（列出）用户分配的托管标识的属性。

## <a name="create-a-user-assigned-managed-identity"></a>创建用户分配的托管标识

1. 使用与 Azure 订阅关联的帐户登录 [Azure 门户](https://portal.azure.com)，以创建用户分配的托管标识。
2. 在搜索框中，键入托管标识，然后在“服务”下单击“托管标识”。
3. 单击“添加”，然后在“创建用户分配的托管标识”窗格下的以下字段中输入值：
   - **资源名称**：这是用户分配的托管标识的名称，例如 UAI1。
   - **订阅**：选择要在其下创建用户分配的托管标识的订阅
   - **资源组**：新建一个包含用户分配的托管标识的资源组，或者选择“使用现有项”，在现有资源组中创建用户分配的托管标识。
   - **位置**：选择用于部署用户分配的托管标识的位置，例如“美国西部”。
4. 单击“创建”。

![创建用户分配的托管标识](./media/how-to-manage-ua-identity-portal/create-user-assigned-managed-identity-portal.png)

## <a name="list-user-assigned-managed-identities"></a>列出用户分配的托管标识

1. 使用与 Azure 订阅关联的帐户登录 [Azure 门户](https://portal.azure.com)，以列出用户分配的托管标识。
2. 在搜索框中，键入托管标识，然后在“服务”下单击“托管标识”。
3. 这会返回一个列表，其中包含订阅中的用户分配的托管标识。  要查看用户分配的托管标识的详细信息，请单击其名称。

![列出用户分配的托管标识](./media/how-to-manage-ua-identity-portal/list-user-assigned-managed-identity-portal.png)

## <a name="delete-a-user-assigned-managed-identity"></a>删除用户分配的托管标识

1. 使用与 Azure 订阅关联的帐户登录 [Azure 门户](https://portal.azure.com)，以删除用户分配的托管标识。
2. 选择用户分配的托管标识，然后单击“删除”。
3. 在确认框中选择“是”。

![删除用户分配的托管标识](./media/how-to-manage-ua-identity-portal/delete-user-assigned-managed-identity-portal.png)

## <a name="assign-a-role-to-a-user-assigned-managed-identity"></a>为用户分配的托管标识分配角色 

1. 使用与 Azure 订阅关联的帐户登录 [Azure 门户](https://portal.azure.com)，以列出用户分配的托管标识。
2. 在搜索框中，键入托管标识，然后在“服务”下单击“托管标识”。
3. 这会返回一个列表，其中包含订阅中的用户分配的托管标识。  选择要为其分配角色的用户分配托管标识。
4. 选择“访问控制(IAM)”，并选择“添加”。

   ![用户分配的托管标识启动](./media/how-to-manage-ua-identity-portal/assign-role-screenshot1.png)

5. 在“添加权限”边栏选项卡中，配置以下值，然后单击“保存”：
   - **角色** - 要分配的角色
   - **将访问权限分配到** - 要将用户分配的托管标识分配到的资源
   - **选择** - 要将访问权限分配到的成员
   
   ![用户分配的托管标识 IAM](./media/how-to-manage-ua-identity-portal/assign-role-screenshot2.png)  