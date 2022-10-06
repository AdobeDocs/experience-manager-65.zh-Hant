---
title: 配置RTF編輯器以建立可訪問的網頁和網站。
description: 配置RTF編輯器以建立可訪問的網頁和網站。
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 配置RTE以建立可訪問的網頁和網站 {#configure-rte-for-accessibility}

Adobe Experience Manager支援符合各種無障礙標準的無障礙功能。 此外，開發人員可以自訂或擴充功能，提供功能，協助使用使用RTF編輯器(RTE)的Experience Manager元件來建立無障礙內容。

設計網頁並將內容新增至頁面時，內容開發人員和作者可使用RTE的功能，提供無障礙相關資訊。 例如，通過標題和段落元素添加結構資訊。

要配置和定制這些功能， [設定RTE外掛程式](#configure-the-plugin-features) （元件）。 例如， `paraformat` 外掛程式可讓您新增其他區塊層級語意元素，包括將支援的標題層級數量擴展至基本 `H1`, `H2`，和 `H3` 預設提供。

RTE提供多種元件，適用於觸控式使用者介面和傳統使用者介面。 不過，使用RTE的主要元件為 **文字** 兩個介面都可用的元件。 下列影像顯示啟用了一系列外掛程式的RTE，包括 `paraformat`:

![觸控式UI中以全螢幕模式顯示的文字元件(RTE)。](assets/chlimage_1-206.png)

*圖：觸控式使用者介面中的文字元件。*

![在傳統UI中編輯文字元件的對話方塊(RTE)。](assets/chlimage_1-207.png)

*圖：傳統使用者介面中的文字元件。*

有關各種介面中可用的RTE功能之間的差異，請參見 [外掛程式及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins).

## 設定外掛程式功能 {#configure-the-plugin-features}

如需設定RTE的完整指示，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md) 頁面。 涵蓋所有問題，包括關鍵步驟：

* [外掛程式和功能](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [啟動外掛程式並設定features屬性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [設定RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

在適當的 `rtePlugins` CRXDE Lite的子分支中，您可以啟用該外掛程式的所有或特定功能。

![CRXDE Lite顯示範例rtePlugin。](assets/chlimage_1-208.png)

### 示例 — 指定RTE選擇欄位中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語義塊格式可通過以下方式提供供選擇：

1. 視您的RTE而定，決定並導覽至 [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [啟用「段落」選擇欄位](/help/sites-administering/rich-text-editor.md);by [啟用外掛程式](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [在「段落」選擇欄位中指定要提供的格式](/help/sites-administering/rich-text-editor.md).
1. 然後，內容作者可從RTE中的選取欄位使用段落格式。 可存取：

   * 在觸控式UI中使用段落垂直圖示。
   * 使用 **格式** 欄位（快顯選取器）。

透過段落格式選項，在RTE中提供結構元素，AEM為開發無障礙內容提供了良好的基礎。 內容作者無法使用RTE來設定字型大小、顏色或其他相關屬性的格式，因而無法建立內嵌格式。 相反，它們必須選取適當的結構元素，例如標題，並使用從樣式選項中選擇的全域樣式。 這可確保標籤簡潔，為使用自己的樣式表和正確結構化內容瀏覽的用戶提供更多選項。

## 使用源編輯功能 {#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現必須檢查並調整使用RTE建立的HTML原始碼。 例如，在RTE中建立的內容片段可能需要額外的標籤，以確保符合WCAG 2.0。這可以使用 [來源編輯](/help/sites-administering/rich-text-editor.md#aboutplugins) 選項。 您可以指定 [ `sourceedit` 功能 `misctools` 外掛程式](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>使用 `sourceedit` 特徵。 輸入錯誤和/或不支援的功能可能會導致更多問題。

## 新增對更多HTML元素和屬性的支援 {#add-support-for-more-html-elements-and-attributes}

若要進一步擴充AEM的協助工具功能，您可以根據RTE擴充現有元件(例如 **文字** 和 **表格** 元件)，以及其他元素和屬性。

下列程式說明如何擴充 **表格** 元件 **註解** 為輔助技術使用者提供資料表格相關資訊的元素：

### 示例 — 將標題添加到表屬性對話框 {#example-adding-the-caption-to-the-table-properties-dialog}

在 `TablePropertiesDialog`，添加用於編輯標題的附加文本輸入欄位。 請注意 `itemId` 必須設為 `caption` （即DOM屬性的名稱）以自動處理其內容。

在 **表格**，請明確設定或將屬性移除為DOM元素或從中移除。 值會由 `config` 物件。 請注意，DOM屬性應使用對應的 `CQ.form.rte.Common` 方法( `com` 是 `CQ.form.rte.Common`)，以避免瀏覽器實作的常見陷阱。

>[!NOTE]
>
>此程式僅適用於傳統用戶介面。

### 範例 — 在文字中使用強調時建立無障礙HTML {#create-accessible-html-for-text}

RTE可使用 `strong` 和 `em` 標籤取代 `b` 和 `i`. 將下列節點新增為 `uiSettings` 和 `rtePlugins` 中的節點。

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### 逐步指示 {#step-by-step-instructions}

1. 開始CRXDE Lite。 例如： [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 複製:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   至:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >如果中間資料夾尚未存在，則可能需要建立這些資料夾。

1. 複製:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   至:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`。

1. 開啟下列檔案以進行編輯（按兩下開啟）:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在 `constructor` 方法，在讀取行之前：

   ```
   var dialogRef = this;
   ```

   新增下列程式碼：

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 開啟下列檔案：

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`。

1. 在 `transferConfigToTable` 方法：

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. 使用 **全部保存……**

>[!NOTE]
>
>純文字欄位並非字幕元素值允許的唯一輸入類型。 您可以使用任何ExtJS Widget，透過其提供註解的值 `getValue()` 方法。
>
>若要新增其他元素和屬性的編輯功能，請確定兩者：
>
>* 此 `itemId` 每個對應欄位的屬性會設為適當DOM屬性的名稱(`TablePropertiesDialog`)。
>* 已在DOM元素上明確設定和/或移除屬性(`Table`)。


>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [建立可存取的內容（符合WCAG 2.0）](/help/sites-authoring/creating-accessible-content.md)

