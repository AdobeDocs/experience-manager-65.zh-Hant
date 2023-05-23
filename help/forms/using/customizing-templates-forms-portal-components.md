---
title: 自定義表單門戶元件的模板
seo-title: Customizing templates for forms portal components
description: 在窗體清單中顯示自定義元資料
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

# 自定義表單門戶元件的模板{#customizing-templates-for-forms-portal-components}

## 必備條件 {#prerequisites}

[管理表單元資料](../../forms/using/manage-form-metadata.md)

HTML和CSS的工作知識

## 概觀 {#overview}

AEM Forms用戶介面允許您向任何表單添加元資料。 自定義元資料可在列出和搜索組織表單時增強用戶體驗。

Forms門戶允許您在表單清單中使用自定義元資料。 在為資產建立自定義模板時，可以修改其佈局並使用CSS樣式集的自定義元資料。

執行以下步驟，為各種Forms門戶元件建立自定義模板。

## 建立自定義模板 {#creating-a-nbsp-custom-template}

1. 在/apps下建立sling:Folder節點

   添加&quot;fpContentType&quot;屬性。 根據要為其定義自定義模板的元件，為屬性指定相應的值。

   * Search &amp; Lister元件：&quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交元件：

      * 草稿部分：/libs/fd/fp/drafts模板
      * 提交部分：/libs/fd/fp/submissions模板
   * 連結元件：/libs/fd/fp/linkTemplate

   添加在選擇佈局模板時要顯示的標題。

   >[!NOTE]
   >
   >標題可以不同於您建立的sling:Folder的節點名稱。

   下圖描述了Search &amp; Lister元件的配置。
   ![建立sling：資料夾](assets/1.png)

1. 在此資料夾中建立檔案template.html作為自定義模板。
1. 編寫自定義模板並使用自定義元資料，如下所述。

## 工作示例 {#working-example}

以下是自定義模板的示例實現，其中Forms門戶為Search &amp; Lister元件獲取了自定義GeometrixxGov卡佈局。

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

## 自定義模板的技術規範 {#technical-specifications-for-custom-templates}

任何Forms門戶元件的自定義模板都包括可重複和非可重複的條目。 可重複項是要列出的基本實體。 可重複條目的示例包括Search &amp; Lister、Drafts &amp; Submissions和Link元件。

Forms門戶為佔位符提供了顯示自定義/OOTB元資料的語法。 在顯示表單、草稿或提交結果後填充佔位符。

要包括可重複項，請配置屬性的值 **資料可重複** 至 **真**。

*在所討論的示例中，自定義模板頂部有兩個Div元素。 第一個CSS類具有&quot;__FP_boxes-container&quot; CSS類，它用作列出的表單的容器元素。 第二個具有「__FP_boxes」 CSS類，是基本圖元的模板，在本例中為「表單」。 的&#x200B;**資料可重複**Div元素中存在的屬性具有&#x200B;**真**。*

每個佔位符都有一個排它的OOTB元資料集。 要在窗體上的特定位置顯示自定義元資料，請添加 **${metadata_prop屬性** 在那兒。

*在示例中，元資料屬性用於多個實例。 例如，它用於&#x200B;**描述**。**名稱**。**窗體URL**。**html樣式**。**pdf URL**。**pdf樣式**,**路徑**按規定的方式。*

## 現成的元資料 {#out-of-the-box-metadata}

各種Forms門戶元件提供可用於清單的OOTB元資料的獨有集。

### Search &amp; Lister元件 {#search-amp-lister-component}

* **標題：** 窗體標題
* **名稱**:表單的名稱（大多與標題相同）
* **描述**:窗體的說明
* **窗體URL**:將表單呈現為HTML的URL
* **pdf URL**:將表單呈現為PDF的URL
* **資產類型**:資產的類型。 有效值包括 **窗體**。**PDF窗體**。 **打印表單**, **自適應窗體**

* **html樣式**&amp; **pdf樣式**:用於渲染的HTML和PDF表徵圖的顯示樣式。 有效值為&quot;**__FP_display_none**&#x200B;或為空。

>[!NOTE]
>
>切記在自定義樣式表中使用__FP_display_none類。

* **下載URL**:下載資產的URL。

在用戶介面上支援本地化、排序和使用配置屬性（僅限搜索和Lister）:

1. **本地化支援**:要本地化任何靜態文本，請使用屬性 `${localize-YOUR_TEXT}` 並使本地化值可用（如果尚不存在）。
   *在討論的示例中，屬性 `${localize-Apply}` 和 `${localize-Download}` 用於本地化「應用」和「下載」文本。*

1. **支援排序**:按一下HTML元素對搜索結果進行排序。 要在表佈局中實現排序，請在特定表標題上添加「data-sortKey」屬性。 此外，將其值添加為要排序的元資料。
例如，對於網格視圖中的「Title」標題，「data-sortKey」標題的值為「title」。 按一下標題以對特定列中的值進行排序。

1. **使用配置屬性**:Search &amp; Lister元件有幾種可在用戶介面上使用的配置。 例如，要顯示通過編輯對話框保存的HTML工具提示文本，請使用 `${config-htmlLinkText}` 屬性。 **同樣，對於PDF工具提示文本，使用** `${config-pdfLinkText}` 屬性。

### 連結元件 {#link-component}

* **標題：** 窗體標題
* **窗體URL**:將表單呈現為HTML的URL
* **目標**:連結的目標屬性。 有效值為&quot;_blank&quot;和&quot;_self&quot;。
* **連結文本**:連結標題

### 草稿和提交元件 {#drafts-amp-submissions-component}

* **路徑**:草稿/提交元資料節點的路徑。 將其與。HTML副檔名一起用作URL以開啟草稿或提交。
* **上下文路徑**:實例的上下文路AEM徑
* **首字母**:自適應表單標題的首字母（大寫），已保存為草稿或已提交。
* **表單名稱**:自適應表單的標題，已保存為「草稿」或已提交。
* **草稿ID**:列出的拔模的ID(僅在「拔模」(Draft)部分的模板中使用)。
* **提交ID**:列出的提交的ID（僅在「提交」部分的模板中使用）。
* **狀態**:已提交表單的狀態。 （僅在「提交」部分的模板中使用）。
* **描述**:與草稿或提交關聯的自適應表單的說明。
* **diffTime**:當前時間與草稿上次保存操作之間的差異。 或者，當前時間與上次提交操作之間的差異。
* **表徵圖類**:用於顯示草稿/提交的第一個字母的CSS類。 Forms門戶包括以下各類，它們提供各種有色背景。
* **所有者**:建立草稿/提交的用戶。
* **今天**:以DD建立草稿或提交日期:MM:YYYY格式。
* **時間立即**:以HH表示的草稿或提交的建立時間:MM:SS 24小時格式

*注意:*

1. 對於「草稿和提交」元件下「草稿」部分的刪除選項，請將CSS類命名為「__FP_deleteDraft」。 此外，還包含屬性&quot;draftID&quot;和值 **${draftID}**，即相應拔模的拔模id。

1. 在建立連結以開啟草稿和提交時，可以指定 **${path.html** 值 **href** 錨點標籤的屬性。

![「草稿和提交」節點](assets/raw-image-with-index.png)

**A**. 容器元件

**B** 具有固定層次結構的「path」元資料，以獲取為每個表單儲存的縮略圖。

**C.** 用於每個表單的模板節的資料可重複屬性

**D** 本地化「應用」字串

**E.** 使用配置屬性pdfLinkText

**F.** 使用「pdfUrl」元資料

## 提示、技巧和已知問題 {#tips-tricks-and-known-issues}

1. 請勿在任何自定義模板中使用單引號(&#39;)。
1. 對於自定義元資料，將此屬性儲存在 **jcr：內容/元資料** 僅節點。 如果將其儲存在其他位置，Forms門戶將無法顯示元資料。
1. 確保任何自定義元資料或現有元資料的名稱不包含冒號(:)。 如果出現，則無法在用戶介面上顯示。
1. **資料可重複** 對一個 **連結** 元件。 Adobe建議您避免在連結元件的模板中使用此屬性。

## 相關文章

* [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單門戶頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自定義草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定義表單門戶元件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
