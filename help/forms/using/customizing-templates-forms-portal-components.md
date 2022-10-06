---
title: 自訂表單入口網站元件的範本
seo-title: Customizing templates for forms portal components
description: 以表單清單顯示自訂中繼資料
seo-description: Display custom metadata in form listing
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# 自訂表單入口網站元件的範本{#customizing-templates-for-forms-portal-components}

## 必備條件 {#prerequisites}

[管理表單中繼資料](../../forms/using/manage-form-metadata.md)

HTML和CSS的工作知識

## 總覽 {#overview}

AEM Forms使用者介面可讓您將中繼資料新增至任何表單。 自訂中繼資料可增強使用者體驗，同時列出和搜尋您組織的表單。

Forms Portal可讓您在表單清單中使用自訂中繼資料。 為資產建立自訂範本時，您可以修改其版面，並搭配您的CSS樣式集使用自訂中繼資料。

執行下列步驟，為各種Forms Portal元件建立自訂範本。

## 建立自訂範本 {#creating-a-nbsp-custom-template}

1. 在/apps底下建立sling:Folder節點

   新增「fpContentType」屬性。 根據要為其定義自定義模板的元件，為屬性指定適當的值。

   * Search &amp; Lister元件：&quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交元件：

      * 草稿部分：/libs/fd/fp/draftsTemplate
      * 提交部分：/libs/fd/fp/submissionsTemplate
   * 連結元件：/libs/fd/fp/linkTemplate

   新增您要在選取版面範本時顯示的標題。

   >[!NOTE]
   >
   >標題可能與您建立的sling:Folder的節點名稱不同。

   下圖描述了Search &amp; Lister元件的配置。
   ![建立Sling:Folder](assets/1.png)

1. 在此資料夾中建立檔案template.html作為自訂範本。
1. 撰寫自訂範本，並使用自訂中繼資料，如下所述。

## 工作範例 {#working-example}

以下是自訂範本的範例實作，Forms Portal會取得Search &amp; Lister元件的自訂Geometrixx政府卡版面。

```html
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

任何Forms Portal元件的自訂範本都包含可重複和非可重複的項目。 可重複的項是要列出的基本實體。 可重複項目的範例包括Search &amp; Lister、Drafts &amp; Submissions和Link元件。

Forms Portal提供放置器顯示自訂/OOTB中繼資料的語法。 顯示表單、草稿或提交結果後，會填入預留位置。

若要包含可重複的項目，請設定屬性的值 **資料可重複** to **true**.

*在討論的範例中，自訂範本的頂端有兩個Div元素。 第一個類別搭配「__FP_boxes-container」CSS類別，可作為所清單單的容器元素。 第二個包含「__FP_boxes」CSS類是基本實體的範本，在此例中為「表單」。 此&#x200B;**資料可重複**「Div」元素中存在的屬性具有值&#x200B;**true**.*

每個佔位符都有一個專用的OOTB元資料集。 若要在表單上的特定位置顯示自訂中繼資料，請新增 **${metadata_prop}屬性** 在那裡。

*在範例中，中繼資料屬性用於多個例項。 例如，它用於&#x200B;**說明**,**名稱**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**，和&#x200B;**路徑**按規定的方式。*

## 現成可用的中繼資料 {#out-of-the-box-metadata}

各種Forms入口網站元件提供專屬的OOTB中繼資料集，供您列出。

### Search&amp;Lister元件 {#search-amp-lister-component}

* **標題：** 表單標題
* **名稱**:表單名稱（大多與標題相同）
* **說明**:表單說明
* **formUrl**:將表單轉譯為HTML的URL
* **pdfUrl**:將表單轉譯為PDF的URL
* **assetType**:資產的類型。 有效值包括 **表單**,**PDF表單**, **打印表單**，和 **適用性表單**

* **htmlStyle**&amp; **pdfStyle**:用於呈現的HTML和PDF表徵圖的顯示樣式。 有效值為「**__FP_display_none**「或空白。

>[!NOTE]
>
>請記得在自訂樣式表中使用__FP_display_none類。

* **downloadUrl**:下載資產的URL。

在使用者介面上支援本地化、排序及使用設定屬性（僅限搜尋和清單）:

1. **本地化支援**:若要將任何靜態文字本地化，請使用屬性 `${localize-YOUR_TEXT}` 並讓本地化值可供使用（如果尚未存在）。
   *在討論的範例中，屬性 `${localize-Apply}` 和 `${localize-Download}` 用於本地化「套用」和「下載」文字。*

1. **支援排序**:按一下HTML元素以排序搜尋結果。 若要在表格版面中實施排序，請在特定表格標題上新增「data-sortKey」屬性。 此外，將其值新增為您要排序的中繼資料。
例如，對於格線檢視中的「Title」標題，「data-sortKey」標題的值為「title」。 按一下標題以排序特定欄中的值。

1. **使用配置屬性**:Search &amp; Lister元件有數個可在使用者介面上使用的設定。 例如，要顯示通過編輯對話框保存的HTML工具提示文本，請使用 `${config-htmlLinkText}` 屬性。 **同樣地，對於PDF工具提示文本，請使用** `${config-pdfLinkText}` 屬性。

### 連結元件 {#link-component}

* **標題：** 表單標題
* **formUrl**:將表單轉譯為HTML的URL
* **目標**:連結的Target屬性。 有效值為「_blank」和「_self」。
* **linkText**:連結標題

### 草稿和提交元件 {#drafts-amp-submissions-component}

* **路徑**:草稿/提交中繼資料節點的路徑。 將其與。HTML副檔名搭配使用，作為URL以開啟草稿或提交。
* **contextPath**:AEM例項的內容路徑
* **firstLetter**:適用性表單標題的首字母（大寫），已儲存為草稿或提交。
* **formName**:最適化表單的標題，會儲存為草稿或提交。
* **draftID**:所列草稿的ID（僅用於「草稿」部分的模板）。
* **submitID**:所列提交的ID（僅用於「提交」區段的範本）。
* **狀態**:已提交表單的狀態。 （僅用於「提交」區段的範本）。
* **說明**:與草稿或提交相關的最適化表單說明。
* **diffTime**:草稿的目前時間與上次儲存動作之間的差異。 或者，提交的目前時間與上次提交動作之間的差異。
* **iconClass**:CSS類別，用來顯示草稿/提交的第一個字母。 Forms Portal包含下列類別，提供不同的彩色背景。
* **所有者**:建立草稿/提交的使用者。
* **今天**:DD中草稿或提交的建立日期:MM:YYYY格式。
* **TimeNow**:以HH格式建立草稿或提交的時間:MM:24小時格式

*注意:*

1. 對於「草稿與提交」元件下「草稿」區段中的刪除選項，將CSS類別命名為「__FP_deleteDraft」。 此外，也納入「draftID」屬性與值 **${draftID}**，即對應草稿的草稿id。

1. 建立連結以開啟草稿和提交時，您可以指定 **${path}.html** 作為 **href** 屬性。

![草稿和提交節點](assets/raw-image-with-index.png)

**A**. 容器元素

**B.** 具有固定階層的「路徑」中繼資料，以取得為每個表單儲存的縮圖。

**C.** 用於每個表單的模板部分的資料可重複屬性

**D.** 本地化「應用」字串

**E.** 使用設定屬性pdfLinkText

**F.** 使用「pdfUrl」中繼資料

## 提示、秘訣和已知問題 {#tips-tricks-and-known-issues}

1. 請勿在任何自訂範本中使用單引號(&#39;)。
1. 若為自訂中繼資料，請將此屬性儲存在 **jcr:content/metadata** 僅節點。 如果您將其儲存在任何其他位置，Forms Portal將無法顯示中繼資料。
1. 請確定任何自訂中繼資料或現有中繼資料的名稱不包含冒號(:)。 若有，則無法在使用者介面上顯示。
1. **資料可重複** 對 **連結** 元件。 Adobe建議您避免在連結元件的範本中使用此屬性。

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
