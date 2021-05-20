---
title: 啟用表單入口網站元件
seo-title: 啟用表單入口網站元件
description: 現成可用的Forms Portal元件已停用。 啟用Document Services和Document Services述詞群組，以啟用Forms Portal元件。
seo-description: 現成可用的Forms Portal元件已停用。 啟用Document Services和Document Services述詞群組，以啟用Forms Portal元件。
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: 表單入口網站
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# 啟用表單入口元件{#enabling-forms-portal-components}

現成可用的表單入口網站元件無法使用。 若要讓元件顯示在AEM sidekick的可用元件清單中，請執行下列步驟：

1. 登入您網站的製作例項，並開啟AEM Sites頁面。

1. 對於使用靜態模板的頁面，請執行以下步驟：

   1. 在頁首中，點選![Canvas-drop-down](assets/canvas-drop-down.png) > **Design**&#x200B;以在「設計」模式中開啟頁面。
   1. 點選任何元件（具有藍色邊框），然後點選![欄位層級](assets/field-level.png)以選取包含目前元件的段落系統。
   1. 在段落系統中，點選![settings_icon](assets/settings_icon.png)以開啟段落系統的「編輯」對話框。
   1. 從&#x200B;**[!UICONTROL 允許的元件]**&#x200B;清單中，啟用&#x200B;**[!UICONTROL Document Services]**&#x200B;和&#x200B;**[!UICONTROL Document Services謂詞]**&#x200B;元件的複選框。 點選&#x200B;**[!UICONTROL 確定]**。

1. 對於使用動態範本的頁面，請執行下列步驟：

   1. 在頁首中，點選![properties](assets/properties.png) > **編輯範本**&#x200B;以開啟頁面的範本。
   1. 點選「 **版面容器** 」，然後點選「 ![ FeedManagement](/help/forms/using/assets/feedmanagement.png) 」。 在「**允許的元件**」頁簽中，啟用「**文檔服務和文檔服務謂語**」選項，然後點選「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」。

>[!NOTE]
>
>您也可以選取元件，從這些類別中啟用特定元件。 如需有關元件及其使用方式的詳細資訊，請參閱[建立表單入口網頁](/help/forms/using/creating-form-portal-page.md)和[在頁面](/help/forms/using/embedding-link-component-page.md)中內嵌連結元件。

現在，元件瀏覽器中提供了文檔服務和文檔服務謂詞元件類別。 所有使用相同範本的頁面都會啟用元件。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
