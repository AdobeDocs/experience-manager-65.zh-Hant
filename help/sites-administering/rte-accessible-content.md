---
title: 設定RTF編輯器以建立無障礙的網頁和網站。
description: 設定RTF編輯器以建立無障礙的網頁和網站。
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# 設定RTE以建立無障礙的網頁和網站 {#configure-rte-for-accessibility}

Adobe Experience Manager支援許多符合各種協助工具標準的協助工具功能。 此外，開發人員可以自訂或擴充功能，協助您使用使用RTF編輯器(RTE)的Experience Manager元件來建立無障礙內容。

在設計網頁並將內容新增至頁面時，內容開發人員和作者可使用RTE的功能來提供協助工具的相關資訊。 例如，透過標題和段落元素新增結構資訊。

若要設定和自訂這些功能，請[設定元件的RTE外掛程式](#configure-the-plugin-features)。 例如，`paraformat`外掛程式可讓您新增其他區塊層級語意元素，包括擴充支援的標題層級數目，超出預設提供的基本`H1`、`H2`和`H3`。

RTE提供多種元件供觸控式使用者介面和傳統使用者介面使用。 不過，使用RTE的主要元件是可用於兩個介面的&#x200B;**Text**&#x200B;元件。 下列影像顯示啟用一系列外掛程式的RTE，包括`paraformat`：

在觸控式UI中![全熒幕模式的文字元件(RTE)。](assets/chlimage_1-206.png)

*圖：觸控式使用者介面中的文字元件。*

![在傳統UI中編輯文字元件的對話方塊(RTE)。](assets/chlimage_1-207.png)

*圖：傳統使用者介面中的文字元件。*

如需各種介面中可用的RTE功能之間的差異，請參閱[外掛程式及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。

## 設定外掛程式功能 {#configure-the-plugin-features}

如需設定RTE的完整指示，請參閱[設定RTF編輯器](/help/sites-administering/rich-text-editor.md)頁面。 這涵蓋所有問題，包括關鍵步驟：

* [外掛程式與功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。
* [組態位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
* [啟動外掛程式並設定功能屬性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
* [設定RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。

藉由在CRXDE Lite中適當的`rtePlugins`子分支內設定外掛程式，您可以為該外掛程式啟動所有或特定功能。

![CRXDE Lite顯示rtePlugin範例。](assets/chlimage_1-208.png)

### 範例 — 指定RTE選取欄位中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語意區塊格式可能可供下列使用者選取：

1. 根據您的RTE，決定並導覽至[設定位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用段落選擇欄位](/help/sites-administering/rich-text-editor.md)；方法是啟動[外掛程式](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在[段落]選取欄位中指定您要使用的格式](/help/sites-administering/rich-text-editor.md)。
1. 然後，內容作者可以從RTE的選擇欄位中使用段落格式。 這些檔案可存取：

   * 使用觸控式UI中的段落枕邊圖示。
   * 使用傳統UI中的&#x200B;**Format**&#x200B;欄位（彈出式選取器）。

透過RTE中透過段落格式選項提供的結構元素，AEM為開發無障礙內容提供了良好的基礎。 內容作者無法使用RTE來格式化字型大小、顏色或其他相關屬性，因而無法建立內嵌格式。 相反地，他們必須選取適當的結構元素（例如標題），並使用從「樣式」選項中選擇的全域樣式。 這可確保為使用自己的樣式表和正確結構內容瀏覽的使用者提供乾淨的標示，以及更豐富的選項。

## 使用來源編輯功能 {#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現必須檢查並調整使用RTE建立的HTML原始碼。 例如，在RTE內建立的內容片段可能需要額外的標籤，以確保符合WCAG 2.0。您可以使用RTE的[來源編輯](/help/sites-administering/rich-text-editor.md#aboutplugins)選項來完成此操作。 您可以在`misctools`外掛程式[&#128279;](/help/sites-administering/rich-text-editor.md#aboutplugins)上指定`sourceedit`功能。

>[!CAUTION]
>
>請謹慎使用`sourceedit`功能。 輸入錯誤和/或不支援的功能可能會造成更多問題。

## 新增對更多HTML元素和屬性的支援 {#add-support-for-more-html-elements-and-attributes}

若要進一步擴充AEM的協助工具功能，您可以利用其他元素和屬性，以RTE為基礎擴充現有元件（例如&#x200B;**Text**&#x200B;和&#x200B;**Table**&#x200B;元件）。

下列程式說明如何使用&#x200B;**Caption**&#x200B;元素來擴充&#x200B;**Table**&#x200B;元件，該元素將資料表的相關資訊提供給輔助技術使用者：

### 範例 — 將標題加入表格屬性對話方塊中 {#example-adding-the-caption-to-the-table-properties-dialog}

在`TablePropertiesDialog`的建構函式中，新增用於編輯註解的額外文字輸入欄位。 請注意，`itemId`必須設為`caption` （即DOM屬性的名稱）才能自動處理其內容。

在&#x200B;**Table**&#x200B;中，明確設定或移除DOM專案的屬性。 此值由`config`物件中的對話方塊傳遞。 請注意，應使用對應的`CQ.form.rte.Common`方法來設定/移除DOM屬性（`com`是`CQ.form.rte.Common`的捷徑），以避免瀏覽器實作中的常見陷阱。

>[!NOTE]
>
>此程式僅適用於Classic使用者介面。

### 範例 — 在文字中使用強調時建立無障礙HTML {#create-accessible-html-for-text}

RTE可以使用`strong`和`em`標籤來取代`b`和`i`。 將下列節點新增為對話方塊中`uiSettings`和`rtePlugins`節點的同層級。

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
   >如果中間資料夾尚不存在，您可能需要建立這些資料夾。

1. 複製:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   至:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`。

1. 開啟下列檔案進行編輯（按兩下即可開啟）：

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在`constructor`方法中，行讀取之前：

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

1. 在`transferConfigToTable`方法的結尾新增下列程式碼：

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

1. 使用&#x200B;**全部儲存……**&#x200B;儲存您的變更

>[!NOTE]
>
>純文字欄位不是註解元素值允許的唯一輸入型別。 您可以使用任何ExtJS Widget，透過其`getValue()`方法提供註解值。
>
>若要為其他元素和屬性新增編輯功能，請確定兩者：
>
>* 每個對應欄位的`itemId`屬性設定為適當DOM屬性(`TablePropertiesDialog`)的名稱。
>* 已明確在DOM元素上設定和/或移除屬性(`Table`)。

>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [建立可存取的內容（符合WCAG 2.0）](/help/sites-authoring/creating-accessible-content.md)
