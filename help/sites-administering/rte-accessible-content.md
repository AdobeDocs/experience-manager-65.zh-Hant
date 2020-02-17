---
title: 配置RTE以生成可訪問站點
description: 瞭解如何設定AEM Rich Text Editor以製作具協助工具的網站。
uuid: 87539fee-3ecc-49f4-af3d-8dde72399c28
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ff0f006d-461c-4cc4-b6eb-d665f3f3b498
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# 配置RTE以生成可訪問站點 {#configuring-rte-for-producing-accessible-sites}

AEM支援兩者：

* 標準協助工具功能，包括影像的替代文字
* 以及使用富格文字編輯器(RTE)的元件建立內容時可存取的其他功能

內容作者可使用RTE的功能在將內容新增至頁面時提供協助工具資訊。 這包括通過標題和段落元素添加結構資訊。

您可以 [為元件配置RTE插件](#configuring-the-plugin-features) ，以配置和自定義這些功能。 例如，外掛程 `paraformat` 式可讓您新增其他區塊層級的語義元素，包括將支援的標題層級數擴充至基本 `H1`, `H2` 並依預設 `H3` 提供。

RTE可在觸控式和傳統UI的多種元件中使用。 但是，使用RTE的主要元件是 **Text** 。

AEM **中的Text** （文字）元件可供觸控式和傳統UI使用。 下列影像顯示已啟用多種增效模組的豐富型文字編輯器，包括 `paraformat`:

* 啟 **用觸控** UI中的Text元件：

   ![在觸控式UI中以全螢幕模式顯示的文字元件(RTE)。](assets/chlimage_1-206.png)

* 傳統 **UI中的** Text元件：

   ![在傳統UI中編輯文本元件的對話框(RTE)。](assets/chlimage_1-207.png)

>[!NOTE]
>
>傳統UI和觸控式UI中可用的RTE功能有所不同。 如需詳細資訊，請參閱
>
>* [外掛程式及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)
>* [外掛程式及其功能——啟用觸控的UI](/help/sites-administering/rich-text-editor.md#aboutplugins)
>



## 設定外掛程式功能 {#configuring-the-plugin-features}

有關配置RTE的完整說明可在「配置富 [格文本編輯器」頁上獲得](/help/sites-administering/rich-text-editor.md) 。 這涵蓋所有問題，包括關鍵步驟：

* [外掛程式及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)
* [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [啟動外掛程式並設定功能屬性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [配置RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

透過在CRXDE Lite的適當子 `rtePlugins` 分支中設定外掛程式（請參閱下圖），您就可啟動該外掛程式的所有或特定功能。

![CRXDE Lite，顯示範例rtePlugin。](assets/chlimage_1-208.png)

### 示例——指定RTE選擇欄位中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語義塊格式可通過以下方式提供供選擇：

1. 根據RTE，確定並導航到配 [置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [啟用「段落選擇」欄位](/help/sites-administering/rich-text-editor.md);啟動 [外掛程式](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在「段落選取」欄位中指定您想要使用的格式](/help/sites-administering/rich-text-editor.md)。
1. 然後，內容作者可從RTE中的選擇欄位使用段落格式。 可以訪問這些檔案：

   * 使用啟用觸控的UI中的段落戳記圖示。
   * 使用 **Classic** UI中的「格式」欄位（快顯選取器）。

AEM透過段落格式選項在RTE中提供結構元素，為開發可存取的內容提供了良好的基礎。 內容作者無法使用RTE格式化字型大小或顏色或其他相關屬性，因而無法建立內嵌格式。 而必須選取適當的結構元素，例如標題，並使用從「樣式」選項中選擇的全域樣式。 這可確保清晰的標籤、更適合使用自己樣式表瀏覽的使用者以及正確結構化內容的選項。

## 原始碼編輯功能的使用 {#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現有必要檢查並調整使用RTE建立的HTML原始碼。 例如，在RTE中建立的一部分內容可能需要額外的標籤，以確保符合WCAG 2.0。這可以通過RTE的源 [編輯](/help/sites-administering/rich-text-editor.md#aboutplugins) 選項來完成。 您可以在外掛 [ 程 `sourceedit` 式上指定 `misctools` 功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。

>[!CAUTION]
>
>請小心 `sourceedit` 使用功能。 輸入錯誤和／或不支援的功能會導致更多問題。

## 新增對其他HTML元素和屬性的支援 {#adding-support-for-additional-html-elements-and-attributes}

若要進一步擴充AEM的協助功能，可以使用其他元素和屬性來擴充以RTE(例如 **Text** 和 **Table** components)為基礎的現有元件。

以下過程說明如何使用 **Caption元素擴展Table****** （表）元件，該元素向輔助技術用戶提供有關資料表的資訊：

### 示例——將標題添加到表屬性對話框 {#example-adding-the-caption-to-the-table-properties-dialog}

在的建構函 `TablePropertiesDialog`式中，新增用於編輯標題的其他文字輸入欄位。 請注意， `itemId` 必須設 `caption` 定為（亦即DOM屬性的名稱）才能自動處理其內容。

在 **表中** ，必須將屬性明確設定或從DOM元素中刪除。 值由對象中的對話框傳 `config` 遞。 請注意，DOM屬性應使用對應的方法來設 `CQ.form.rte.Common` 定／移除( `com` 是捷徑 `CQ.form.rte.Common`)，以避免瀏覽器實作中常見的錯誤。

>[!NOTE]
>
>此程式僅適用於傳統UI。

### 逐步指示 {#step-by-step-instructions}

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

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. 開啟下列檔案以進行編輯（按兩下以開啟）:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在方 `constructor` 法中，行讀取前：

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

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. 在方法結尾處新增下列程 `transferConfigToTable` 式碼：

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

1. 使用「全部儲 **存……」儲存變更**

>[!NOTE]
>
>純文字欄位並非標題元素值允許的唯一輸入類型。 任何透過其方法提供標題值的ExtJS介面工具集 `getValue()` 都可使用。
>
>若要新增編輯功能，以取得其他元素和屬性，請確定兩者：
>
>* 每 `itemId` 個對應欄位的屬性會設為適當DOM屬性(`TablePropertiesDialog`)的名稱。
>* 在DOM元素上明確設定和／或移除屬性(`Table`)。


>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [建立可存取的內容（WCAG 2.0符合性）](/help/sites-authoring/creating-accessible-content.md)

