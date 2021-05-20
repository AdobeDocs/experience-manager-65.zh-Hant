---
title: 將規則編輯器存取權授予給所選的使用者群組
seo-title: 將規則編輯器存取權授予給所選的使用者群組
description: 授予對規則編輯器的限制存取權以選取使用者群組。
seo-description: 授予對規則編輯器的限制存取權以選取使用者群組。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: 適用性表單
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 8%

---

# 將規則編輯器存取權授予給所選的使用者群組{#grant-rule-editor-access-to-select-user-groups}

## 概覽 {#overview}

您可能有不同類型的使用者，具備與適用性Forms搭配使用的不同技能。 雖然專家使用者可能擁有使用指令碼和複雜規則的適當知識，但可能有基本層級的使用者，他們只需要使用最適化表單的版面和基本屬性。

AEM Forms可讓您根據使用者的角色或功能，限制使用者的規則編輯器存取權。 在適用性Forms組態服務設定中，您可以指定可檢視及存取規則編輯器的[使用者群組](/help/sites-administering/security.md)。

## 指定可訪問規則編輯器{#specify-user-groups-that-can-access-rule-editor}的用戶組

1. 以管理員身分登入AEM Forms。
1. 在製作例項中，按一下「![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具![槌子](assets/hammer.png) >操作> Web Console」。 Web控制台在新窗口中開啟。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到並按一下&#x200B;**[!UICONTROL 適用性表單和互動式通信Web通道配置]**。 **[!UICONTROL 隨即出現「最適化表單」和「互動式通訊Web通]** 道配置」對話框。請勿變更任何值，然後按一下「**儲存**」。

   它會在CRX-repository中建立檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理員身分登入CRXDE。 開啟檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config進行編輯。
1. 使用以下屬性指定可訪問規則編輯器的組的名稱（例如，RuleEditorsUserGroup），然後按一下&#x200B;**Save All**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定逗號分隔值的清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當不屬於指定使用者群組的使用者（此處為RuleEditorsUserGroup）點選欄位時，元件工具列中的「編輯規則」圖示(![edit-rules1](assets/edit-rules1.png))不可供她使用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器存取權的使用者可看見的元件工具列

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   無法存取規則編輯器的使用者可看到的元件工具列

   有關向組添加用戶的說明，請參閱[用戶管理和安全性](/help/sites-administering/security.md)。
