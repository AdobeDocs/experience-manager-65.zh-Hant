---
title: 自訂Forms Portal元件的範本
description: 瞭解AEM Forms使用者介面如何讓使用者將中繼資料新增至表單。 自訂中繼資料可強化使用者在表單列出和搜尋時的體驗。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---

# 自訂Forms Portal元件的範本{#customizing-templates-for-forms-portal-components}

## 先決條件 {#prerequisites}

[管理表單中繼資料](../../forms/using/manage-form-metadata.md)

HTML和CSS的工作知識

## 概觀 {#overview}

AEM Forms使用者介面可讓您將中繼資料新增至任何表單。 自訂中繼資料可增強使用者在列出和搜尋組織表單時的體驗。

Forms入口網站可讓您在表單清單中使用自訂中繼資料。 為資產建立自訂範本時，您可以修改其版面，並在CSS樣式集中使用自訂中繼資料。

請務必遵守下列步驟，以建立各種Forms Portal元件的自訂範本。

## 建立自訂範本 {#creating-a-nbsp-custom-template}

1. 在/apps下建立sling：Folder節點

   新增「fpContentType」屬性。 根據您為其定義自訂範本的元件，指定適當的屬性值。

   * 搜尋和清單元件： &quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交元件：

      * 草稿區段： /libs/fd/fp/draftsTemplate
      * 提交區段：/libs/fd/fp/submissionsTemplate

   * 連結元件： /libs/fd/fp/linkTemplate

   新增您要在選取版面配置範本時顯示的標題。

   >[!NOTE]
   >
   >標題可以不同於您建立的sling：Folder的節點名稱。

   以下影像說明「搜尋和製表器」元件的組態。
   ![建立sling：Folder](assets/1.png)

1. 在此資料夾中建立檔案template.html，以便用作自訂範本。
1. 寫入自訂範本並使用如下所述的自訂中繼資料。

## 工作範例 {#working-example}

以下是自訂範本的範例實作，其中Forms入口網站為Search &amp; Lister元件取得自訂Geometrixx政府卡配置。

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

任何Forms Portal元件的自訂範本包含可重複及不可重複的專案。 可重複專案是基本列示實體。 可重複專案的範例為「搜尋與清單製作者」、「草稿與提交」以及「連結」元件。

Forms Portal提供預留位置語法，以顯示自訂/現成可用的中繼資料。 顯示表單、草稿或提交的結果之後，就會填入預留位置。

若要包含可重複的專案，請設定屬性的值 **資料可重複** 至 **true**.

*在所討論的範例中，自訂範本的頂端存在兩個Div元素。 第一個具有「__FP_boxes-container」CSS類別，可作為所清單單的容器元素。 第二個是「__FP_boxes」CSS類別，是基本實體的範本，在此例中為「表單」。 此&#x200B;**資料可重複**Div元素中存在的屬性具有值&#x200B;**true**.*

每個預留位置都有一個專屬的現成可用中繼資料集。 若要在表單的特定位置顯示自訂中繼資料，請新增 **${metadata_prop} 屬性** 在那兒。

*在此範例中，中繼資料屬性用於多個例項。 例如，它被用於&#x200B;**說明**，**名稱**，**formUrl**，**htmlStyle**，**pdfUrl**，**pdf樣式**、和&#x200B;**路徑**以規定的方式進行。*

## 現成可用的中繼資料 {#out-of-the-box-metadata}

各種Forms Portal元件提供專屬的開箱即用中繼資料集，供您用於清單。

### 搜尋與清單元件 {#search-amp-lister-component}

* **標題：** 表單標題
* **名稱**：表單名稱（大多與標題相同）
* **說明**：表單說明
* **formUrl**：將表單轉譯為HTML的URL
* **pdfUrl**：將表單轉譯為PDF的URL
* **assetType**：資產型別。 有效值包括 **表單**， **PDF表單**， **列印表單**、和 **最適化表單**

* **htmlStyle**&amp; **pdf樣式**：顯示呈現時分別使用的HTML圖示和PDF圖示樣式。 有效值為&quot;**__FP_display_none**」或空白。

>[!NOTE]
>
>請記得在自訂樣式表中使用__FP_display_none類別。

* **downloadUrl**：下載資產的URL。

支援本地化、排序和使用使用者介面上的設定屬性（僅限搜尋和製表者）：

1. **本地化支援**：若要本地化任何靜態文字，請使用屬性 `${localize-YOUR_TEXT}` 並提供當地語系化的值（如果尚未存在）。
   *在所討論的範例中，屬性 `${localize-Apply}` 和 `${localize-Download}` 用於將套用和下載文字當地語系化。*

1. **排序支援**：按一下HTML元素來排序搜尋結果。 若要在表格配置中實施排序，請在特定表格標頭上新增「data-sortKey」屬性。 此外，將其值新增為您要排序的中繼資料。
例如，對於格線檢視中的「Title」標頭，「data-sortKey」標頭的值為「title」。 按一下標題，以便排序特定欄中的值。

1. **使用設定屬性**：搜尋與清單元件具有數個可在使用者介面上使用的設定。 例如，若要顯示透過編輯對話方塊儲存的HTML工具提示文字，請使用 `${config-htmlLinkText}` 屬性。 **同樣地，對於PDF工具提示文字，請使用** `${config-pdfLinkText}` 屬性。

### 連結元件 {#link-component}

* **標題：** 表單標題
* **formUrl**：將表單轉譯為HTML的URL
* **目標**：連結的目標屬性。 有效值為「_blank」和「_self」。
* **連結文字**：連結標題

### 草稿和提交元件 {#drafts-amp-submissions-component}

* **路徑**：草稿/提交中繼資料節點的路徑。 將其與。HTML副檔名用作URL，以便您開啟草稿或提交。
* **contextPath**：AEM執行個體的內容路徑
* **第一字母**：最適化表單標題的第一個字母（大寫），已儲存為草稿或提交。
* **formName**：最適化表單的標題，已儲存為草稿或已提交。
* **draftID**：所列出草稿的ID （僅用於草稿區段的範本中）。
* **submitID**：列出之提交的ID （僅用於提交區段的範本中）。
* **狀態**：已提交表單的狀態。 （僅用於「提交」區段的範本）。
* **說明**：與草稿或提交專案相關的最適化表單說明。
* **diffTime**：目前時間和草稿的最後儲存動作之間的差異。 或者，也可以選擇目前時間與上次提交之提交動作之間的差異。
* **iconclass**：用於顯示草稿/提交內容的第一字母的CSS類別。 Forms Portal包含下列類別，提供各種不同色彩的背景。
* **所有者**：建立草稿/提交的使用者。
* **今天**：在中建立草稿或提交的日期 `DD:MM:YYYY` 格式。
* **TimeNow**：在中建立草稿或提交專案的時間 `HH:MM:SS` 24小時格式

*注意：*

1. 針對「草稿與提交」元件下「草稿」區段中的刪除選項，將CSS類別命名為「__FP_deleteDraft」。 此外，將屬性「draftID」與值納入 **${draftID}**，即對應草稿的草稿識別碼。

1. 在建立開啟草稿和提交作業的連結時，您可以指定 **${path}.html** 作為 **href** 錨點標籤的屬性。

![草稿與提交節點](assets/raw-image-with-index.png)

**A**. 容器元素

**B.** 具有固定階層的「路徑」中繼資料，可取得針對每個表單儲存的縮圖。

**C.** 用於每個表單的範本區段的可重複資料屬性

**D.** 本地化「套用」字串

**E.** 使用設定屬性pdfLinkText

**F.** 使用「pdfUrl」中繼資料

## 秘訣、技巧和已知問題 {#tips-tricks-and-known-issues}

1. 請勿在任何自訂範本中使用單引號(&#39;)。
1. 對於自訂中繼資料，請將此屬性儲存在 **jcr：content/metadata** 僅限節點。 如果您將其儲存在任何其他位置，Forms Portal將無法顯示中繼資料。
1. 確認任何自訂中繼資料或現有中繼資料的名稱不含冒號( ： )。 如果出現提示，您無法在使用者介面中顯示。
1. **資料可重複** 對於以下專案沒有任何意義： **連結** 元件。 Adobe建議您避免在連結元件的範本中使用此屬性。

## 相關文章

* [啟用Forms Portal元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立Forms入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂Forms Portal元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
