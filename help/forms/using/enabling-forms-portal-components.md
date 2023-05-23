---
title: 啟用表單門戶元件
seo-title: Enabling forms portal components
description: 開箱即用，已禁用Forms門戶元件。 啟用文檔服務和文檔服務謂片語以啟用Forms門戶元件。
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 啟用表單門戶元件 {#enabling-forms-portal-components}

現成，表單門戶元件不可用。 要使元件出現在旁鍵中可用元件的列AEM表中，請執行以下步驟：

1. 登錄到您網站的作者實例並開啟一個AEM Sites頁。

1. 對於使用靜態模板的頁面，請執行以下步驟：

   1. 在頁眉中，點擊 ![畫布下拉清單](assets/canvas-drop-down.png) > **設計** 以「設計」模式開啟頁面。
   1. 點擊任何元件（帶藍色邊框），然後點擊 ![欄位級](assets/field-level.png) 的子菜單。
   1. 在段落系統中，點擊 ![設定表徵圖](assets/settings_icon.png) 開啟段落系統的「編輯」對話框。
   1. 從 **[!UICONTROL 允許的元件]**，啟用複選框 **[!UICONTROL 文檔服務]** 和 **[!UICONTROL 文檔服務謂語]** 元件。 點擊 **[!UICONTROL 確定]**。

1. 對於使用動態模板的頁面，請執行以下步驟：

   1. 在頁眉中，點擊 ![屬性](assets/properties.png) > **編輯模板** 開啟頁面的模板。
   1. 點擊 **佈局容器** 點擊 ![源管理](/help/forms/using/assets/feedmanagement.png)。 在 **允許的元件** 頁籤 **文檔服務和文檔服務謂語** 選項，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

>[!NOTE]
>
>也可以通過選擇元件從這些類別中啟用特定元件。 有關元件及其用法的詳細資訊，請參閱 [建立表單門戶頁](/help/forms/using/creating-form-portal-page.md) 和 [在頁面中嵌入連結元件](/help/forms/using/embedding-link-component-page.md)。

現在，「文檔服務」和「文檔服務謂語」元件類別在元件瀏覽器中可用。 對使用相同模板的所有頁面啟用元件。

## 相關文章

* [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單門戶頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自定義草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定義表單門戶元件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
