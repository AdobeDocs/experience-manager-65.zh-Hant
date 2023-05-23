---
title: 將規則編輯器存取權授予給所選的使用者群組
seo-title: Grant rule editor access to select user groups
description: 授予對規則編輯器的受限訪問權限以選擇用戶組。
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 6%

---

# 將規則編輯器存取權授予給所選的使用者群組{#grant-rule-editor-access-to-select-user-groups}

## 概觀 {#overview}

您可能有不同類型的用戶，這些用戶擁有與Adaptive Forms協作的不同技能。 雖然專家用戶可能擁有使用指令碼和複雜規則的正確知識，但可能有基本級用戶只需要使用自適應表單的佈局和基本屬性。

AEM Forms允許您根據用戶的角色或功能限制規則編輯器對用戶的訪問。 在自適應Forms配置服務設定中，可以指定 [用戶組](/help/sites-administering/security.md) 可以查看和訪問規則編輯器。

## 指定可以訪問規則編輯器的用戶組 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理員身份登錄到AEM Forms。
1. 在作者實例中，按一下 ![adobeexperience manager](assets/adobeexperiencemanager.png)Adobe Experience Manager>工具 ![錘](assets/hammer.png) >操作> Web控制台。 Web控制台將在新窗口中開啟。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到並按一下 **[!UICONTROL 自適應形式與交互通信Web通道配置]**。 **[!UICONTROL 自適應形式與交互通信Web通道配置]** 對話框。 不更改任何值，然後按一下 **保存**。

   它在CRX-repository中建立檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理員身份登錄到CRXDE。 開啟檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config進行編輯。
1. 使用以下屬性指定可以訪問規則編輯器的組的名稱（例如，RuleEditorsUserGroup），然後按一下 **全部保存**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要啟用對多個組的訪問，請指定逗號分隔值的清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當不屬於指定用戶組的用戶（此處為RuleEditorsUserGroup）點擊某個欄位時，「編輯規則」表徵圖( ![編輯規則1](assets/edit-rules1.png))在元件工具欄中不可用：

   ![元件儲存器](assets/componentstoolbarwithre.png)

   具有規則編輯器訪問權限的用戶可見的元件工具欄

   ![構件](assets/componentstoolbarwithoutre.png)

   對沒有規則編輯器訪問權限的用戶可見的元件工具欄

   有關向組添加用戶的說明，請參見 [用戶管理和安全](/help/sites-administering/security.md)。
