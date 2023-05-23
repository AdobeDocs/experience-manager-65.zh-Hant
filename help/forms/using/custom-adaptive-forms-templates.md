---
title: 建立自定義自適應表單模板
seo-title: Creating a custom adaptive form template
description: 本文介紹如何建立自定義自適應表單模板。
seo-description: This article describes how to create custom adaptive form templates.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# 建立自定義自適應表單模板{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms引入了動態模板。 您可以使用AEM Sites模板編輯器 [建立或編輯動態模板](../../forms/using/template-editor.md)。 下文中提到的模板是靜態模板。 預設安裝中不提供這些。 [安裝相容性包](../../forms/using/compatibility-package.md) 獲取環境中的模板。

## 必備條件 {#prerequisites}

* 了AEM解 [頁面模板](/help/sites-authoring/templates.md) 和 [自適應表單創作](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 了AEM解 [客戶端庫](/help/sites-developing/clientlibs.md)

## 自適應表單模板 {#adaptive-form-template}

自適應表單模板是專AEM門的頁面模板，具有某些用於建立自適應表單的屬性和內容結構。 模板具有預配置的佈局、樣式和基本的初始內容結構。

建立表單後，對原始模板內容結構的任何更改都不會反映在表單中。

## 預設自適應表單模板 {#default-adaptive-form-templates}

QuickStartAEM提供了以下自適應表單模板：

* 調查模板：允許您使用配置了多列的響應佈局建立單頁自適應表單。 佈局根據要顯示窗體的各種螢幕的尺寸自動調整。
* 簡單註冊模板：允許您使用嚮導佈局建立多步自適應窗體。 在此佈局中，可以為每個步驟指定一個步驟完成表達式，該表達式在嚮導繼續執行下一步之前進行驗證。
* 頁籤式登記模板：允許您使用左側的頁籤佈局建立多頁籤自適應表單，在此可以按任意順序訪問頁籤。
* 高級註冊模板：用於建立具有多個頁籤和嚮導的窗體。 它使用左側的頁籤佈局，允許您按任意順序訪問頁籤。 它使用Adobe Document Cloud設計服務進行簽名和驗證。
* 空白模板：允許您建立沒有任何頁眉、頁腳和初始內容的表單。 可以添加元件，如文本框、按鈕和影像。 空白模板允許您建立一個表單 [嵌AEM入網頁](/help/forms/using/embed-adaptive-form-aem-sites.md)。

這些模板 `sling:resourceType` 屬性集到相應的頁元件。 頁元件呈現包含自適應表單容器的CQ頁，該自適應表單容器再呈現自適應表單。

下表枚舉了模板和頁面元件之間的關聯：

<table>
 <tbody>
  <tr>
   <td><p><strong>範本</strong></p> </td>
   <td><p><strong>頁面元件</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabedenrolls</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advandentrolls</p> </td>
  </tr>
 </tbody>
</table>

## 使用模板編輯器建立自適應表單模板 {#creating-an-adaptive-form-template-using-template-editor}

可以使用模板編輯器指定自適應表單的結構和初始內容。 例如，您希望所有表單作者在註冊表單中只有幾個文本框、導航按鈕和提交按鈕。 您可以建立模板，作者可以使用該模板建立與其他登記表單一致的表單。 模AEM板編輯器允許您：

* 在結構層中添加表單的頁眉和頁腳元件
* 提供窗體的初始內容。
* 指定主題。
* 指定提交、重置和導航等操作。

有關詳細資訊，請參見 [模板編輯器](../../forms/using/template-editor.md)。

## 從CRXDE建立自適應表單模板 {#creating-an-adaptive-form-template-from-crxde}

您可以建立模板並使用它建立自適應表單，而不是使用可用模板。 自定義模板基於引用自適應表單容器和頁面元素（如頁眉和頁腳）的各種頁面元件。

您可以使用網站的基本頁面元件建立這些元件。 或者，可以擴展自適應表單的頁面元件，該頁面元件使用框外模板。

執行以下步驟以建立自定義模板，如simpleEnrollmentTemplate。

1. 導航到創作實例上的CRXDE Lite。

1. 在/apps目錄下，為應用程式建立資料夾結構。 例如，如果應用程式名是mycompany，則建立具有此名稱的資料夾。 通常，應用程式資料夾包含元件、配置、模板、src和安裝目錄。 在此示例中，建立元件、配置和模板資料夾。

1. 導航到資料夾/libs/fd/af/templates。
1. 複製 `simpleEnrollmentTemplate` 的下界。
1. 導航到資料夾/apps/mycompany/templates。 按一下右鍵它，然後選擇 **[!UICONTROL 貼上]**。
1. 如有必要，請更名複製的模板節點。 例如，將其更名為註冊模板。

1. 導航到位置/apps/mycompany/templates/enrollment-template。

1. 修改 `jcr:title` 和 `jcr:description` 屬性 `jcr:content` 節點，將模板與複製的模板區分開。

1. 的 `jcr:content` 已修改模板的節點包含 `guideContainer` 和 `guideformtitle` 元件。 `guideContainer` 是容納自適應窗體的容器。 的 `guideformtitle` 元件顯示應用程式名稱、說明等。

   而不是 `guideformtitle`，可以包括自定義元件或 `parsys` 元件。 例如，刪除 `guideformtitle`，並添加自定義元件或 `parsys` 元件節點。 確保 `sling:resourceType` 元件的屬性引用元件，並在頁面中定義 `component.jsp` 的子菜單。

1. 導航到/apps/mycompany/templates/enrollment-template/jcr:content的位置。

1. 開啟 **[!UICONTROL 屬性]** 的 `cq:designPath` 屬性。

1. 現在，為 `cq:Page` 的雙曲餘切值。

## 建立自適應表單頁元件 {#create-an-adaptive-form-page-component}

自定義模板與預設模板的樣式相同，因為模板引用頁面元件/libs/fd/af/components/page/base。 可以將元件引用作為屬性 `sling:resourceType` 在節點/apps/mycompany/templates/enrollment-template/jcr:content上定義。 由於基礎是核心產品元件，因此不要修改此元件。

1. 導航到節點/apps/mycompany/templates/enrollment-template/jcr:content並修改屬性值 `sling:resourceType` 到/apps/mycompany/components/page/enrollment頁
1. 將節點/libs/fd/af/components/page/base複製到資料夾/apps/mycompany/components/page。

1. 將複製的元件更名為 `enrollmentpage`。

1. **（僅當您已有內容頁時）** 如果您有現有的 `contentpage`元件。 如果您沒有 `contentpage`元件，您可以 `resourceSuperType`指向OOTB基頁的屬性。

   1. 對於 `enrollmentpage` 節點，設定屬性的值 `sling:resourceSuperType` 到mycompany/components/page/content頁。 的 `contentpage` 元件是站點的基頁元件。 其他頁面元件可以擴展它。 刪除下面的指令碼檔案 `enrollmentpage`除外 `head.jsp`。 `content.jsp`, `library.jsp`。 的 `sling:resourceSuperType` 元件， `contentpage` 在本例中，包括所有此類指令碼。 頁眉（包括導航欄和頁腳）從 `contentpage` 元件。

   1. 開啟檔案 `head.jsp`。

      JSP檔案包含行 `<cq.include script="library.jsp"/>`。

      的 `library.jsp` 檔案包含 `guide.theme.simpleEnrollment` 客戶端庫，其中包含自適應表單的樣式。

      頁面元件 `enrollmentpage` 有獨家 `head.jsp` 替換 `head.jsp` 檔案 `contentpage` 元件。

   1. 在 `head.jsp` 檔案 `contentpage` 元件 `head.jsp` 檔案 `enrollmentpage` 元件。
   1. 在 `content.jsp` 指令碼中，您可以添加附加的頁面內容或對頁面呈現時包括的其他元件的引用。 例如，如果添加了自定義元件 `applicationformheader`，確保在JSP檔案中為元件添加以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同樣，如果添加 `parsys` 元件在模板節點結構中，還包括自定義元件。

## 建立自適應表單客戶端庫 {#creating-an-adaptive-form-client-library}

的 `head.jsp` 檔案 `enrollmentpage` 新模板的元件包括客戶端庫 `guide.theme.simpleEnrollment`。 預設模板還使用此客戶端庫。 使用以下方法更改新模板中的樣式：

* 定義自定義主題並替換預設主題 `guide.theme.simpleEnrollment` 的下界。
* 在/etc/designs/mycompany下定義新的客戶端庫。 在jsp頁中預設主題項後包括客戶端庫。 在此客戶端庫中包括所有被覆蓋的樣式和其他Java指令碼檔案。

>[!NOTE]
>
>主題是指包含在用於呈現自適應表單的頁面元件中的客戶端庫。 客戶端庫主要控制自適應表單的外觀。
