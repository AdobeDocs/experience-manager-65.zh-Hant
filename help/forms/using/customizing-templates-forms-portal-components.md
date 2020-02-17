---
title: 自訂表單入口元件的範本
seo-title: 自訂表單入口元件的範本
description: 在表單清單中顯示自訂中繼資料
seo-description: 在表單清單中顯示自訂中繼資料
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
translation-type: tm+mt
source-git-commit: 13cc8ba8fda8fa0e5fac6bb92d1d4fc4849492eb

---


# 自訂表單入口元件的範本{#customizing-templates-for-forms-portal-components}

## 必備條件 {#prerequisites}

[管理表單中繼資料](../../forms/using/manage-form-metadata.md)

HTML和CSS的使用知識

## 概覽 {#overview}

AEM Forms使用者介面可讓您將中繼資料新增至任何表格。 自訂中繼資料可增強使用者體驗，同時列出和搜尋組織的表單。

表單入口網站可讓您在表單清單中使用自訂中繼資料。 建立資產的自訂範本時，您可以修改其版面配置，並搭配CSS樣式集使用自訂中繼資料。

執行下列步驟，為各種Forms Portal元件建立自訂範本。

## Creating a custom template {#creating-a-nbsp-custom-template}

1. 在/apps下建立sling:Folder節點

   新增&quot;fpContentType&quot;屬性。 根據要為其定義自定義模板的元件，為屬性指定適當的值。

   * Search &amp; Lister元件：&quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交元件：

      * 草稿部分：/libs/fd/fp/draftsTemplate
      * 提交部分：/libs/fd/fp/submissionsTemplate
   * 連結元件：/libs/fd/fp/linkTemplate
   新增您要在選取版面範本時顯示的標題。

   *注意：標題可以與您建立的sling:Folder節點名稱不同。*
   *下圖描述了Search &amp; Lister元件的配置。* 建 ![立sling:Folder](assets/1.png)

1. 在此資料夾中建立檔案template.html，做為自訂範本。
1. 撰寫自訂範本，並使用自訂中繼資料，如下所述。

## 工作範例 {#working-example}

以下是自訂範本的範例實作，Forms Portal會在此範本中取得Search &amp; Lister元件的自訂Geometrixx Gov Card Layout。

```mxml
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## 自訂範本的技術規格 {#technical-specifications-for-custom-templates}

任何Forms Portal元件的自訂範本都包含可重複和非可重複的項目。 可重複項是列出的基本實體。 可重複項目的範例包括Search &amp; Lister、Drafts &amp; Submissions和Link元件。

Forms Portal提供位置持有人顯示自訂/OOTB中繼資料的語法。 預留位置會在顯示表單、草稿或提交結果後填入。

要包括可重複條目，請將屬性data-repeatable的 **值配置****為true**。

*在所討論的範例中，自訂範本的頂端有兩個Div元素。 第一個CSS類別具有&quot;_FP_boxes-container&quot; CSS類別，可當成列出表單的容器元素。 第二個具有&quot;__FP_boxes&quot; CSS類是基本實體的範本，在本例中為表單。 Div元&#x200B;**素中顯示的**data-repeatable屬性具有值&#x200B;**true**。*

每個預留位置都有專屬的OOTB中繼資料集。 若要在表單上的特定位置顯示自訂中繼資料，請在 **該位置新增${metadata_prop}屬性** 。

*在此範例中，中繼資料屬性用於多個例項。 例如，它用於&#x200B;**描述**、**name、**formUrl **、**htmlStyle Url、****************pdfUrlStylePdf、PdfStylePdf和LathPath中，以規定的方式使用。*

## 立即可用的中繼資料 {#out-of-the-box-metadata}

各種Forms Portal元件提供可供列出的專屬OOTB中繼資料集。

### Search &amp; Lister元件 {#search-amp-lister-component}

* **** 標題：表單標題
* **名稱**:表單名稱（大多與標題相同）
* **說明**:表單說明
* **formUrl**:將表單轉譯為HTML的URL
* **pdfUrl**:將表單轉譯為PDF的URL
* **assetType**:資產的類型。 有效值包 **括表單**、**PDF表單**、 **列印表單**&#x200B;和 **最適化表單**

* **htmlStyle**&#x200B;與 **pdfStyle**:HTML和PDF圖示的顯示樣式，分別用於轉譯。 有效值為&#x200B;**&quot;__FP_display_none**&quot;或空白。

   **** 注意：請記得在自訂樣式表中使用__FP_display_none類

* **downloadUrl**:下載資產的URL。

在使用者介面上支援本地化、排序和使用設定屬性（僅限搜尋與清單）:

1. **本地化支援**:若要本地化任何靜態文字，請 `${localize-YOUR_TEXT}` 使用屬性，並讓本地化值可用（如果尚未存在）。
   *在所討論的示例中，屬性`${localize-Apply}`和用`${localize-Download}`於本地化「應用」和「下載」文本。*

1. **支援排序**:按一下HTML元素以排序搜尋結果。 若要在表版面中實作排序，請在特定表格標題上新增「data-sortKey」屬性。 此外，請將其值新增為您要排序的中繼資料。
例如，對於格線檢視中的「標題」標題，「data-sortKey」標題的值是「title」。 按一下標題，以排序特定欄中的值。

1. **使用配置屬性**:Search &amp; Lister元件有數種可在使用者介面上使用的組態。 例如，要顯示通過編輯對話框保存的HTML工具提示文本，請使用屬 `${config-htmlLinkText}` 性。 **同樣地，對於PDF工具提示文本，請使用**`${config-pdfLinkText}` 屬性。

### 連結元件 {#link-component}

* **** 標題：表單標題
* **formUrl**:將表單轉譯為HTML的URL
* **目標**:連結的Target屬性。 有效值為&quot;_blank&quot;和&quot;_self&quot;。
* **linkText**:連結標題

### 草稿與提交元件 {#drafts-amp-submissions-component}

* **路徑**:草稿／提交元資料節點的路徑。 將它與。HTML副檔名搭配使用，做為URL以開啟草稿或提交。
* **contextPath**:AEM例項的內容路徑
* **firstLetter**:最適化表單標題的首字母（大寫），已儲存為草稿或已提交。
* **formName**:最適化表單的標題，已儲存為草稿或已提交。
* **draftID**:列出的草稿的ID（僅用於「草稿」部分的模板）。
* **submitID**:列出的提交ID（僅用於「提交」部分的模板）。
* **狀態**:已提交表單的狀態。 （僅在「提交」區段的範本中使用）。
* **說明**:與草稿或提交相關的最適化表單說明。
* **diffTime**:當前時間與草稿上次保存操作之間的差異。 或者，目前時間與上次提交動作之間的差異。
* **iconClass**:用於顯示草稿／提交的第一個字母的CSS類。 Forms Portal包含下列類別，提供各種彩色背景。
* **擁有者**:建立草稿／提交的用戶。
* **今天**:以DD:MM:YYYY格式建立草稿或提交的日期。
* **TimeNow**:以HH:MM:SS 24小時格式建立草稿或提交的時間

*注意:*

1. 對於「草稿與提交」元件下「草稿」區段中的刪除選項，請為CSS類別命名為&quot;__FP_deleteDraft&quot;。 此外，請加入&quot;draftID&quot;屬性，其值為 **${draftID}**，此為對應草稿的草稿ID。

1. 在建立開啟草稿和提交的連結時，您可以指定 **${path}.html** ，作為錨記 **href** 屬性的值。

![「草稿和提交」節點](assets/raw-image-with-index.png)

**A**. 容器元素

**** B.具有固定階層的「路徑」中繼資料，以取得每個表單所儲存的縮圖。

**C.** Data-repeatable屬性，用於每個表單的模板部分

**** D.若要本地化&quot;Apply&quot;字串

**** E.使用設定屬性pdfLinkText

**** F.使用「pdfUrl」中繼資料

## 秘訣、訣竅和已知問題 {#tips-tricks-and-known-issues}

1. 請勿在任何自訂範本中使用單引號(&#39;)。
1. 若為自訂中繼資料，請將此屬性僅儲 **存在jcr:content/metadata** 節點上。 如果您將其儲存在任何其他位置，Forms Portal將無法顯示中繼資料。
1. 請確定任何自訂中繼資料或現有中繼資料的名稱不包含冒號(:)。 如果是，您無法在使用者介面上顯示。
1. **data-repeatable** 對於Link元件沒有任何 **意義** 。 Adobe建議您避免在連結元件的範本中使用此屬性。

## 相關文章

* [啟用表單入口元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網頁](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表格簡介](/help/forms/using/introduction-publishing-forms.md)