---
title: 授予規則編輯器對選定用戶組的訪問權限
seo-title: 授予規則編輯器對選定用戶組的訪問權限
description: 授予對規則編輯器的限制訪問權以選擇用戶組。
seo-description: 授予對規則編輯器的限制訪問權以選擇用戶組。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 授予規則編輯器對選定用戶組的訪問權限{#grant-rule-editor-access-to-select-user-groups}

## 概覽 {#overview}

您可能有不同類型的使用者，具備不同的技巧，可搭配使用Adaptive Forms。 雖然專家使用者可能擁有使用指令碼和複雜規則的適當知識，但是可能有基本層級使用者需要只使用最適化表單的版面配置和基本屬性。

AEM Forms可讓您根據使用者的角色或函式，限制規則編輯器的存取權。 在Adaptive Forms Configuration service設定中，您可以指定可以查 [看和訪問規則編輯器](/help/sites-administering/security.md) 的用戶組。

## 指定可存取規則編輯器的使用者群組 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理員身分登入AEM Forms。
1. 在作者例項中，按一 ![](assets/adobeexperiencemanager.png)下「Adobe Experience Manager >工具槌 ![子](assets/hammer.png) >作業> Web Console」。 「Web控制台」在新視窗中開啟。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到並按一下 **Adaptive Form Configuration Service**。 **此時將顯示Adaptive Form Configuration Service** （最適化表單配置服務）對話框。 請勿變更任何值，然後按一下「 **儲存**」。

   它在CRX-repository中建立一個檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理員身份登錄CRXDE。 開啟檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config以進行編輯。
1. 使用下列屬性指定可存取規則編輯器的群組名稱（例如，RuleEditorsUserGroup），然後按一下「全 **部儲存**」。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定逗號分隔值的清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![建立使用者](assets/create_user_new.png)

   現在，當非指定使用者群組（此處為RuleEditorsUserGroup）的使用者點選欄位時，在元件工具列中無法使用編輯規則圖示( ![edit-rules1](assets/edit-rules1.png)):

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器訪問權限的用戶可見的元件工具欄

   ![元件stoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   對沒有規則編輯器訪問權限的用戶可見的元件工具欄

   如需將使用者新增至群組的指示，請參 [閱使用者管理與安全性](/help/sites-administering/security.md)。

