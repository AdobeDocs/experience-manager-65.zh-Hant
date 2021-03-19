---
title: 將規則編輯器存取權授予給所選的使用者群組
seo-title: 將規則編輯器存取權授予給所選的使用者群組
description: 授予對規則編輯器的限制訪問權以選擇用戶組。
seo-description: 授予對規則編輯器的限制訪問權以選擇用戶組。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 8%

---


# 將規則編輯器存取權授予給所選的使用者群組{#grant-rule-editor-access-to-select-user-groups}

## 概覽 {#overview}

您可能有不同類型的使用者，具備不同的技能，可與Adaptive Forms合作。 雖然專家使用者可能擁有使用指令碼和複雜規則的適當知識，但是可能有基本層級使用者需要只使用最適化表單的版面配置和基本屬性。

AEM Forms允許您根據用戶的角色或功能限制規則編輯器對用戶的訪問。 在「最適化Forms配置服務」設定中，您可以指定[用戶組](/help/sites-administering/security.md)，以查看和訪問規則編輯器。

## 指定可存取規則編輯器{#specify-user-groups-that-can-access-rule-editor}的使用者群組

1. 以管理員身份登錄AEM Forms。
1. 在作者例項中，按一下「![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager>工具![hammer](assets/hammer.png) >作業> Web Console」。 「Web控制台」在新視窗中開啟。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到並按一下&#x200B;**[!UICONTROL 自適應表單和互動式通信Web通道配置]**。 **[!UICONTROL 出現「Adaptive Form and Interactive Communication Web Channel]** Configuration（自適應表單和互動式通信Web通道配置）」對話框。請勿變更任何值，然後按一下「儲存」。****

   它在CRX-repository中建立一個檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理員身份登錄CRXDE。 開啟檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config以進行編輯。
1. 使用下列屬性指定可存取規則編輯器的群組名稱（例如，RuleEditorsUserGroup），然後按一下「全部儲存」。****

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定逗號分隔值的清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當非指定使用者群組的使用者（此處為RuleEditorsUserGroup）點選欄位時，在元件工具列中，「編輯規則」圖示(![edit-rules1](assets/edit-rules1.png))不適用於她：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器訪問權限的用戶可見的元件工具欄

   ![元件stoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   對沒有規則編輯器訪問權限的用戶可見的元件工具欄

   有關向組添加用戶的說明，請參閱[用戶管理和安全](/help/sites-administering/security.md)。

