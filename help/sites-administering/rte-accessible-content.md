---
title: 設定Rich Text Editor以建立可存取的網頁和網站。
description: 設定Rich Text Editor以建立可存取的網頁和網站。
contentOwner: AG
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# 配置RTE以建立可訪問的網頁和站點{#configure-rte-for-accessibility}

Adobe Experience Manager支援符合各種協助工具標準的多種協助工具功能。 此外，開發人員可自訂或擴充功能，以提供使用Rich Text Editor(RTE)的Experience Manager元件來建立可存取內容的功能。

當設計網頁並將內容新增至頁面時，內容開發人員和作者可使用RTE的功能來提供協助工具相關資訊。 例如，透過標題和段落元素新增結構資訊。

要配置和自定義這些功能，請[為元件配置RTE插件](#configure-the-plugin-features)。 例如，`paraformat`外掛程式可讓您新增其他區塊層級的語義元素，包括將支援的標題層級數擴充至預設提供的基本`H1`、`H2`和`H3`。

RTE可用於Touch-enabled用戶介面和Classic用戶介面的多種元件。 但是，使用RTE的主要元件是&#x200B;**Text**&#x200B;元件，它可用於兩個介面。 以下影像顯示啟用了一系列插件的RTE，包括`paraformat` :

![在觸控式UI中以全螢幕模式顯示的文字元件(RTE)。](assets/chlimage_1-206.png)

*圖：啟用觸控的使用者介面中的文字元件。*

![在傳統UI中編輯文本元件的對話框(RTE)。](assets/chlimage_1-207.png)

*圖：Classic使用者介面中的Text元件。*

有關各種介面中可用的RTE功能之間的差異，請參見[插件及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。

## 設定外掛程式功能{#configure-the-plugin-features}

有關配置RTE的完整說明，請參見[配置Rich Text Editor](/help/sites-administering/rich-text-editor.md)頁。 這涵蓋所有問題，包括關鍵步驟：

* [外掛程式和功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。
* [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
* [啟動外掛程式並設定features屬性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
* [配置RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。

在CRXDE Lite中的適當`rtePlugins`子分支中設定外掛程式，即可啟動該外掛程式的所有或特定功能。

![CRXDE Lite，顯示範例rtePlugin。](assets/chlimage_1-208.png)

### 示例——指定RTE選擇欄位{#example-specifying-paragraph-formats-available-in-rte-selection-field}中可用的段落格式

新的語義塊格式可通過以下方式提供供選擇：

1. 根據RTE，確定並導航至[配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用「段落選擇」欄位](/help/sites-administering/rich-text-editor.md);啟動 [外掛程式](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在「段落選取」欄位中指定您想要使用的格式](/help/sites-administering/rich-text-editor.md)。
1. 然後，內容作者可從RTE中的選擇欄位使用段落格式。 可以訪問這些檔案：

   * 使用啟用觸控的UI中的段落戳記圖示。
   * 使用Classic UI中的&#x200B;**Format**&#x200B;欄位（快顯選取器）。

AEM透過段落格式選項在RTE中提供結構元素，為開發可存取的內容提供了良好的基礎。 內容作者無法使用RTE格式化字型大小或顏色或其他相關屬性，因而無法建立內嵌格式。 而必須選取適當的結構元素，例如標題，並使用從「樣式」選項中選擇的全域樣式。 這可確保清晰的標籤、更適合使用自己樣式表瀏覽的使用者以及正確結構化內容的選項。

## 使用源編輯功能{#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現有必要檢查並調整使用RTE建立的HTML原始碼。 例如，在RTE中建立的一部分內容可能需要額外的標籤，以確保符合WCAG 2.0。這可以通過RTE的[源edit](/help/sites-administering/rich-text-editor.md#aboutplugins)選項來完成。 您可以在`misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins)上指定[ `sourceedit`功能。

>[!CAUTION]
>
>小心使用`sourceedit`功能。 輸入錯誤和／或不支援的功能會導致更多問題。

## 新增對更多HTML元素和屬性的支援{#add-support-for-more-html-elements-and-attributes}

為了進一步擴充AEM的協助功能，可以以RTE為基礎（例如&#x200B;**Text**&#x200B;和&#x200B;**Table**&#x200B;元件）來擴充現有元件，並附加元素和屬性。

以下過程說明如何使用&#x200B;**Caption**&#x200B;元素擴展&#x200B;**Table**&#x200B;元件，該元素向輔助技術用戶提供有關資料表的資訊：

### 示例——將標題添加到「表屬性」對話框{#example-adding-the-caption-to-the-table-properties-dialog}

在`TablePropertiesDialog`的建構函式中，新增用於編輯標題的其他文字輸入欄位。 請注意，`itemId`必須設為`caption`（亦即DOM屬性的名稱），才能自動處理其內容。

在&#x200B;**Table**&#x200B;中，將屬性顯式設定或從DOM元素中刪除。 值由`config`對象中的對話框傳遞。 請注意，應使用相應的`CQ.form.rte.Common`方法（`com`是`CQ.form.rte.Common`的捷徑）來設定／移除DOM屬性，以避免瀏覽器實作中常見的缺陷。

>[!NOTE]
>
>此過程僅適用於Classic用戶介面。

### 範例——在文字{#create-accessible-html-for-text}中使用強調功能時建立可存取的HTML

RTE可以使用`strong`和`em`標籤來取代`b`和`i`。 將以下節點作為同級添加到對話框中的`uiSettings`和`rtePlugins`節點。

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

### 逐步指示{#step-by-step-instructions}

1. 啟動CRXDE Lite。 例如：[http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 複製:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   至:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >如果中間資料夾不存在，則可能需要建立中間資料夾。

1. 複製:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   至:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`。

1. 開啟下列檔案以進行編輯（按兩下以開啟）:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在`constructor`方法中，行讀取前：

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

1. 在`transferConfigToTable`方法的結尾添加以下代碼：

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

1. 使用&#x200B;**全部保存……**&#x200B;保存更改

>[!NOTE]
>
>純文字欄位並非標題元素值允許的唯一輸入類型。 您可以使用任何ExtJS介面工具集，透過其`getValue()`方法提供標題的值。
>
>若要新增編輯功能，以取得其他元素和屬性，請確定兩者：
>
>* 每個對應欄位的`itemId`屬性會設為適當DOM屬性的名稱(`TablePropertiesDialog`)。
>* 在DOM元素上顯式地設定和／或刪除屬性(`Table`)。


>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [建立可存取的內容（WCAG 2.0符合性）](/help/sites-authoring/creating-accessible-content.md)

