---
title: 將規則編輯器存取權授予給所選的使用者群組
description: 將受限制的存取權授與規則編輯器，以選取使用者群組。
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 15%

---

# 將規則編輯器存取權授予給所選的使用者群組{#grant-rule-editor-access-to-select-user-groups}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文介紹使用基礎元件製作最適化Forms的舊方法。 </span>

## 概觀 {#overview}

您可能有不同型別的使用者，他們具有適用最適化Forms的各種技能。 雖然專家使用者可能擁有使用指令碼和複雜規則的正確知識，但可能有基本級使用者只需要使用最適化表單的版面和基本屬性。

AEM Forms可讓您根據使用者的角色或職能，限制使用者的規則編輯器存取權。 在最適化Forms組態服務設定中，您可以指定 [使用者群組](/help/sites-administering/security.md) 可檢視及存取規則編輯器的使用者。

## 指定可存取規則編輯器的使用者群組 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理員身分登入AEM Forms。
1. 在作者執行個體中，按一下 ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具 ![錘子](assets/hammer.png) >作業> Web主控台。 Web主控台會在新視窗中開啟。

   ![1-2](assets/1-2.png)

1. 在Web主控台視窗中，找到並按一下 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]**. **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 對話方塊隨即顯示。 不要變更任何值，然後按一下 **儲存**.

   它會在CRX-repository中建立檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 。

1. 以管理員身分登入CRXDE。 開啟檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config進行編輯。
1. 使用以下屬性來指定可存取規則編輯器的群組名稱（例如RuleEditorsUserGroup），然後按一下 **全部儲存**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定以逗號分隔的值清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當不屬於指定使用者群組（此處RuleEditorsUserGroup）的使用者點選欄位時，編輯規則圖示( ![edit-rules1](assets/edit-rules1.png))在元件工具列中無法使用：

   ![componentstolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器存取許可權的使用者看得見的元件工具列

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   沒有規則編輯器存取許可權的使用者看得見的元件工具列

   如需將使用者新增至群組的說明，請參閱 [使用者管理與安全性](/help/sites-administering/security.md).
