---
title: 配置富格文本編輯器以建立可訪問的網頁和站點。
description: 配置富格文本編輯器以建立可訪問的網頁和站點。
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 配置RTE以建立可訪問的網頁和站點 {#configure-rte-for-accessibility}

Adobe Experience Manager支援符合各種無障礙標準的標準無障礙功能。 此外，開發人員可以自定義或擴展功能，以提供一些功能，這些功能使用使用RTE(RTE)的Experience Manager元件幫助建立可訪問的內容。

在設計網頁和向網頁添加內容時，內容開發者和作者可以使用RTE的功能來提供與輔助功能相關的資訊。 例如，通過標題和段落元素添加結構資訊。

要配置和定制這些功能， [配置RTE插件](#configure-the-plugin-features) 的子菜單。 例如， `paraformat` 插件允許您添加附加的塊級語義元素，包括擴展支援的標題級別數，超出基本 `H1`。 `H2`, `H3` 預設提供。

RTE可在支援觸摸的用戶介面和經典用戶介面的各種元件中使用。 但是，使用RTE的主要元件是 **文本** 可用於兩個介面的元件。 以下影像顯示啟用了一系列插件的RTE，包括 `paraformat`:

![啟用觸摸的UI中全屏模式的文本元件(RTE)。](assets/chlimage_1-206.png)

*圖：啟用觸摸的用戶介面中的「文本」元件。*

![在傳統UI中編輯文本元件的對話框(RTE)。](assets/chlimage_1-207.png)

*圖：Classic用戶介面中的Text元件。*

有關各種介面中可用的RTE功能之間的差異，請參見 [插件及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。

## 配置插件功能 {#configure-the-plugin-features}

有關配置RTE的完整說明，請參見 [配置RTF編輯器](/help/sites-administering/rich-text-editor.md) 的子菜單。 這涵蓋所有問題，包括關鍵步驟：

* [插件和功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。
* [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
* [激活插件並配置功能屬性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
* [配置RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。

通過在適當的 `rtePlugins` 在CRXDE Lite中的子分支，您可以激活該插件的所有功能或特定功能。

![CRXDE Lite，顯示一個rtePlugin示例。](assets/chlimage_1-208.png)

### 示例 — 指定RTE選擇欄位中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語義塊格式可通過以下方式可供選擇：

1. 根據RTE，確定並導航到 [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用「段落選擇」欄位](/help/sites-administering/rich-text-editor.md);按 [激活插件](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在「段落選擇」欄位中指定要使用的格式](/help/sites-administering/rich-text-editor.md)。
1. 然後，從RTE的選擇欄位中，內容作者可以使用段落格式。 可訪問：

   * 使用啟用觸摸的用戶介面中的段落標尾表徵圖。
   * 使用 **格式** 欄位（彈出式選擇器）。

在RTE中通過段落格式選項提供了結構性元素AEM，為開發可訪問內容提供了良好基礎。 內容作者不能使用RTE格式化字型大小、顏色或其他相關屬性，從而阻止建立內嵌格式。 相反，它們必須選擇相應的結構元素，如標題，並使用從「樣式」(Styles)選項中選擇的全局樣式。 這確保了清晰的標籤，為使用自己的樣式表瀏覽的用戶提供了更好的選項，並確保了正確的結構化內容。

## 源編輯功能的使用 {#use-of-the-source-edit-feature}

在某些情況下，內容作者將發現有必要檢查和調整使用RTE建立的HTML原始碼。 例如，在RTE中建立的某一內容可能需要附加標籤，以確保符合WCAG 2.0。這可以通過 [源編輯](/help/sites-administering/rich-text-editor.md#aboutplugins) 選項。 可以指定 [ `sourceedit` 功能 `misctools` 插件](/help/sites-administering/rich-text-editor.md#aboutplugins)。

>[!CAUTION]
>
>使用 `sourceedit` 特寫。 鍵入錯誤和/或不受支援的功能可能會帶來更多問題。

## 添加對更多HTML元素和屬性的支援 {#add-support-for-more-html-elements-and-attributes}

為了進一步擴展其可AEM訪問性特徵，可以基於RTE擴展現有元件(例如 **文本** 和 **表格** 元件)。

以下過程說明了如何擴展 **表格** 具有 **標題** 向輔助技術用戶提供有關資料表資訊的元素：

### 示例 — 將標題添加到「表屬性」對話框 {#example-adding-the-caption-to-the-table-properties-dialog}

在的建構子中 `TablePropertiesDialog`，添加用於編輯標題的附加文本輸入欄位。 請注意 `itemId` 必須設定為 `caption` （即DOM屬性的名稱）以自動處理其內容。

在 **表格**，將屬性顯式設定或從DOM元素中刪除。 該值通過 `config` 的雙曲餘切值。 請注意，應使用相應的 `CQ.form.rte.Common` 方法( `com` 是 `CQ.form.rte.Common`)以避免瀏覽器實現中的常見錯誤。

>[!NOTE]
>
>此過程僅適用於Classic用戶介面。

### 示例 — 在文本中使用強調時建立可訪問HTML {#create-accessible-html-for-text}

RTE可以使用 `strong` 和 `em` 標籤代替 `b` 和 `i`。 將以下節點作為同級添加到 `uiSettings` 和 `rtePlugins` 的子菜單。

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

### 逐步說明 {#step-by-step-instructions}

1. 啟動CRXDE Lite。 例如： [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
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

1. 開啟以下檔案進行編輯（按兩下開啟）:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在 `constructor` 方法，在讀取行之前：

   ```
   var dialogRef = this;
   ```

   添加以下代碼：

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 開啟以下檔案：

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
>純文字檔案欄位不是字幕元素值允許的唯一輸入類型。 可以使用任何ExtJS構件，該構件通過其 `getValue()` 的雙曲餘切值。
>
>要為其他元素和屬性添加編輯功能，請確保兩者都：
>
>* 的 `itemId` 將每個相應欄位的屬性設定為相應DOM屬性的名稱(`TablePropertiesDialog`)。
>* 在DOM元素上顯式設定和/或刪除該屬性(`Table`)。


>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [建立可訪問內容（WCAG 2.0一致性）](/help/sites-authoring/creating-accessible-content.md)

