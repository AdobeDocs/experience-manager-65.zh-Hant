---
title: 啟用表單入口網站元件
description: 現成可用的Forms Portal元件已停用。 啟用Document Services和Document Services述詞群組以啟用Forms Portal元件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 4%

---

# 啟用表單入口網站元件 {#enabling-forms-portal-components}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

Forms Portal元件是現成可用的元件。 若要讓元件出現在AEM sidekick的可用元件清單中，請執行以下步驟：

1. 登入網站的作者執行個體並開啟AEM Sites頁面。

1. 對於使用靜態範本的頁面，請執行下列步驟：

   1. 在頁面標頭中，選取![畫佈下拉式清單](assets/canvas-drop-down.png) > **設計**，以設計模式開啟頁面。
   1. 選取任何元件（使用藍色邊框），然後選取![欄位層級](assets/field-level.png)，以選取包含目前元件的段落系統。
   1. 在段落系統中，選取![settings_icon](assets/settings_icon.png)以開啟段落系統的編輯對話方塊。
   1. 從&#x200B;**[!UICONTROL 允許的元件]**&#x200B;清單中，啟用&#x200B;**[!UICONTROL 檔案服務]**&#x200B;和&#x200B;**[!UICONTROL 檔案服務述詞]**&#x200B;元件的核取方塊。 選取&#x200B;**[!UICONTROL 確定]**。

1. 對於使用動態範本的頁面，請執行下列步驟：

   1. 在頁面標頭中，選取![屬性](assets/properties.png) > **編輯範本**&#x200B;以開啟頁面的範本。
   1. 選取&#x200B;**配置容器**&#x200B;並選取![FeedManagement](/help/forms/using/assets/feedmanagement.png)。 在&#x200B;**允許的元件**&#x200B;索引標籤中，啟用&#x200B;**Document Services和Document Services述詞**&#x200B;選項，並選取![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

>[!NOTE]
>
>您也可以選取元件，以啟用這些類別中的特定元件。 如需有關元件及其使用方式的詳細資訊，請參閱[建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)以及[在頁面中嵌入連結元件](/help/forms/using/embedding-link-component-page.md)。

現在，元件瀏覽器中提供Document Services和Document Services述詞元件類別。 這些元件會針對使用相同範本的所有頁面啟用。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂Forms Portal元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
