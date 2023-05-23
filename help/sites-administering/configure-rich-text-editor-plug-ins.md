---
title: 配置RTF編輯器插件
description: 瞭解如何配置Adobe Experience Manager富格文本編輯器插件以啟用各個功能。
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
source-git-commit: 11cda989e6a28428f03a269c407a7672e6eab747
workflow-type: tm+mt
source-wordcount: '4406'
ht-degree: 2%

---


# 配置RTF編輯器插件 {#configure-the-rich-text-editor-plug-ins}

RTE功能可通過一系列插件提供，每個插件都具有features屬性。 可以配置features屬性以啟用或禁用一個或多個RTE功能。 本文介紹如何具體配置RTE插件。

有關其他RTE配置的詳細資訊，請參見 [配置RTF編輯器](/help/sites-administering/rich-text-editor.md)。

>[!NOTE]
>
>使用CRXDE Lite時，建議使用 [!UICONTROL 全部保存] 的雙曲餘切值。

## 激活插件並配置features屬性 {#activateplugin}

要激活插件，請執行以下步驟。 只有在首次配置插件時才需要一些步驟，因為相應的節點不存在。

預設情況下， `format`。 `link`。 `list`。 `justify`, `control` 插件及其所有功能都在RTE中啟用。

>[!NOTE]
>
>各 `rtePlugins` 節點稱為 `<rtePlugins-node>` 避免在本文中重複。

1. 使用CRXDE Lite，查找項目的文本元件。
1. 建立的父節點 `<rtePlugins-node>` 如果不存在，則在配置任何RTE插件之前：

   * 根據元件，父節點為：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 備用配置節點： `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 屬於以下類型： **jcr:primaryType** `cq:Widget`
   * 兩者都具有以下屬性：

      * **名稱** `name`
      * **類型** `String`
      * **值** `./text`


1. 根據要配置的介面，建立節點 `<rtePlugins-node>`，如果不存在：

   * **名稱** `rtePlugins`
   * **類型** `nt:unstructured`

1. 在下面，為要激活的每個插件建立一個節點：

   * **類型** `nt:unstructured`
   * **名稱** 所需插件的插件ID

激活插件後，請遵循以下准則配置 `features` 屬性。

|  | 啟用所有功能 | 啟用幾個特定功能 | 禁用所有功能 |
|---|---|---|---|
| 名稱 | 特徵 | 特徵 | 特徵 |
| 類型 | 字串 | 字串[] (多字串；將「類型」設定為「字串」，然後按一下「多個在CRXDE Lite」) | 字串 |
| 值 | `*` （星號） | 設定為一個或多個特徵值 | - |

## 瞭解findreplace插件 {#findreplace}

的 `findreplace` 插件不需要任何配置。 它不在盒子裡。

使用替換功能時，應與查找字串同時輸入要替換的替換字串。 但是，您仍可以按一下「查找」在替換字串之前搜索該字串。 如果在按一下「查找」後輸入替換字串，則搜索將重置為文本的開頭。

按一下「查找」(find)和「替換」(replace)對話框時，該對話框將變為透明，按一下「替換」(replace)時，該對話框將變為不透明。 這允許作者審閱作者將替換的文本。 如果用戶按一下「全部替換」，則對話框將關閉並顯示已進行的替換數。

## 配置貼上模式 {#paste-modes}

使用RTE時，作者可以按以下三種模式之一貼上內容：

* **瀏覽器模式**:使用瀏覽器的預設貼上實現貼上文本。 它不是推薦的方法，因為它可能會引入不需要的標籤。

* **純文字檔案模式**:將剪貼簿內容貼上為純文字檔案。 它在插入之前從複製的內容中刪除所有樣式和格式元素 [!DNL Experience Manager] 元件。

* **MS Word模式**:從MS Word複製時，使用格式貼上文本（包括表）。 不支援從其他源（如網頁或MS Excel）複製和貼上文本，並且只保留部分格式。

### 配置RTE工具欄上可用的「貼上」選項  {#configure-paste-options-available-on-the-rte-toolbar}

您可以在RTE工具欄中為作者提供以下三個表徵圖中的一些、全部或全部：

* **[!UICONTROL 貼上(Ctrl+V)]**:可以預配置為與上述三種貼上模式之一對應。

* **[!UICONTROL 貼上為文本]**:提供純文字檔案模式功能。

* **[!UICONTROL 從Word貼上]**:提供MS Word模式功能。

要配置RTE以顯示所需的表徵圖，請執行以下步驟。

1. 導航到元件，例如 `/apps/<myProject>/components/text`。
1. 導航到節點 `rtePlugins/edit`。 請參閱 [激活插件](#activateplugin) 的子菜單。
1. 建立 `features` 屬性 `edit` 並添加一個或多個功能。 保存所有更改。

### 配置「貼上」(Ctrl+V)表徵圖和快捷方式的行為 {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

可以預配置 **[!UICONTROL 貼上(Ctrl+V)]** 表徵圖。 此配置還定義了作者用於貼上內容的鍵盤快捷鍵Ctrl+V的行為。

配置允許以下三種類型的使用案例：

* 使用瀏覽器的預設貼上實現貼上文本。 它不是推薦的方法，因為它可能會引入不需要的標籤。 配置使用 `browser` 下。

* 將剪貼簿內容貼上為純文字檔案。 在插入元件之前，它會從複製的內容中刪除所有樣式和格式AEM元素。 配置使用 `plaintext` 下。

* 從MS Word複製時，使用格式貼上文本（包括表）。 不支援從其他源（如網頁或MS Excel）複製和貼上文本，並且只保留部分格式。 配置使用 `wordhtml` 下。

1. 在元件中，導航到 `<rtePlugins-node>/edit` 的下界。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參見 [激活插件](#activateplugin)。
1. 在 `edit` 節點使用以下詳細資訊建立屬性：

   * **名稱** `defaultPasteMode`
   * **類型** `String`
   * **值** 所需的貼上模式之一 `browser`。 `plaintext`或 `wordhtml`。

### 配置貼上內容時允許的格式 {#pasteformats}

貼上為Microsoft詞(`paste-wordhtml`)模式，以便您可以明確定義從其他程式(如MicrosoftWord)粘AEM貼時允許使用哪些樣式。

例如，如果貼上時只允許使用粗體格式和清單，AEM則可以過濾掉其它格式。 這稱為可配置的貼上過濾，可針對以下兩項執行：

* [文字](#paste-modes)
* [連結](#linkstyles)

對於連結，您還可以定義自動接受的協定。

要配置將文本從另一個程式貼上到時允許AEM使用的格式：

1. 在元件中，導航到該節點 `<rtePlugins-node>/edit`。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 在 `edit` 保存HTML貼上規則的節點：

   * **名稱** `htmlPasteRules`
   * **類型** `nt:unstructured`

1. 在下面建立節點 `htmlPasteRules`，以保存所允許的基本格式的詳細資訊：

   * **名稱** `allowBasics`
   * **類型** `nt:unstructured`

1. 要控制接受的單個格式，請在 `allowBasics` 節點：

   * **名稱** `bold`
   * **名稱** `italic`
   * **名稱** `underline`
   * **名稱** `anchor` （對於連結和命名錨點）
   * **名稱** `image`

   所有屬性均為 **類型** `Boolean`，因此在適當的情況下 **值** 您可以選擇或刪除複選標籤以啟用或禁用功能。

   >[!NOTE]
   >
   >如果未明確定義，則使用預設值true並接受格式。

1. 其它格式也可以使用一系列其它屬性或節點來定義，這些屬性或節點也應用於 `htmlPasteRules` 的下界。 保存所有更改。

可以使用以下屬性 `htmlPasteRules`。

| 屬性 | 類型 | 說明 |
|---|---|---|
| `allowBlockTags` | 字串 | 定義允許的塊標籤清單。 幾個可能的塊標籤包括： <ul> <li>標題(h1、h2、h3)</li> <li>第(p)段</li> <li>清單(ol、ul)</li> <li>表（表）</li> </ul> |
| `fallbackBlockTag` | 字串 | 定義用於任何塊的塊標籤，該塊標籤不包含在 `allowBlockTags`。 `p` 在大多數情況下都足夠。 |
| 表 | nt:unstructured | 定義貼上表時的行為。 此節點必須具有屬性 `allow` （類型布爾型），以定義是否允許貼上表。 如果允許設定為 `false`，必須指定屬性 `ignoreMode` （鍵入字串）以定義如何處理貼上的表內容。 有效值 `ignoreMode` 為： <ul> <li>`remove`:刪除表內容。</li> <li>`paragraph`:將表單元格轉換為段落。</li> </ul> |
| list | nt:unstructured | 定義貼上清單時的行為。 必須具有屬性 `allow` （鍵入布爾值），以定義是否允許貼上清單。 如果 `allow` 設定為 `false`，必須指定屬性 `ignoreMode` （鍵入字串）以定義如何處理貼上的任何清單內容。 有效值 `ignoreMode` 為： <ul><li> `remove`:刪除清單內容。</li> <li>`paragraph`:將清單項轉換為段落。</li> </ul> |

有效示例 `htmlPasteRules` 結構如下。

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

## 配置文本樣式 {#textstyles}

作者可應用「樣式」來更改部分文本的外觀。 這些樣式基於您在CSS樣式表中預定義的CSS類。 程式化內容封入 `span` 標籤使用 `class` 屬性，以引用CSS類。 比如說， `<span class=monospaced>Monospaced Text Here</span>`。

首次啟用「樣式」插件時，不提供預設的「樣式」。 彈出清單為空。 要向作者提供「樣式」，請執行以下操作：

* 啟用「樣式」(Style)下拉選擇器。
* 指定樣式表的位置。
* 指定可從「樣式」(Style)下拉清單中選擇的單個樣式。

對於以後的配置，例如要添加更多樣式，請僅按照說明參考新樣式表並指定其他樣式。

>[!NOTE]
>
>可以為 [表或表單元格](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)。 這些配置需要單獨的過程。

### 啟用「樣式」下拉選擇器清單 {#styleselectorlist}

這是通過啟用樣式插件來完成的。

1. 在元件中，導航到該節點 `<rtePlugins-node>/styles`。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 建立 `features` 屬性 `styles` 節點：

   * **名稱** `features`
   * **類型** `String`
   * **值** `*` （星號）

1. 保存所有更改。

>[!NOTE]
>
>啟用「樣式」插件後，「樣式」(Style)下拉清單將顯示在編輯對話框中。 但是，由於未配置任何樣式，因此清單為空。

### 指定樣式表位置 {#locationofstylesheet}

然後，指定要參照的樣式表的位置：

1. 導航到文本元件的根節點，例如 `/apps/<myProject>/components/text`。
1. 添加屬性 `externalStyleSheets` 到的父節點 `<rtePlugins-node>`:

   * **名稱** `externalStyleSheets`
   * **類型** `String[]` (多字串；按一下 **多** 在CRXDE中)
   * **值** 要包括的每個樣式表的路徑和檔案名。 使用儲存庫路徑。

   >[!NOTE]
   >
   >可以隨時添加對附加樣式表的參照。

1. 保存所有更改。

>[!NOTE]
>
>在對話框（經典UI）中使用RTE時，您可能需要指定為富格文本編輯而優化的樣式表。 由於技術限制，CSS上下文在編輯器中丟失，因此您可能希望模擬此上下文以改進WYSIWYG體驗。
>
>富格文本編輯器使用ID為 `CQrte` 它可用於提供不同的樣式以供查看和編輯：
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### 在彈出式清單中指定可用樣式 {#stylesindropdown}

1. 在元件定義中，導航到節點 `<rtePlugins-node>/styles`，在中建立 [啟用樣式下拉選擇器](#styleselectorlist)。
1. 節點下 `styles`，建立新節點(也稱為 `styles`)以保留可用清單：

   * **名稱** `styles`
   * **類型** `cq:WidgetCollection`

1. 在 `styles` 表示單個樣式的節點：

   * **名稱**，可以指定名稱，但應適合樣式
   * **類型** `nt:unstructured`

1. 添加屬性 `cssName` 到此節點以引用CSS類：

   * **名稱** `cssName`
   * **類型** `String`
   * **值** CSS類的名稱(前面沒有「。」;比如說， `cssClass` 而不是 `.cssClass`)

1. 添加屬性 `text` 到同一節點；這定義了選擇框中顯示的文本：

   * **名稱** `text`
   * **類型** `String`
   * **值** 樣式描述；的子菜單。

1. 儲存變更。

   對每個所需樣式重複上述步驟。

### 配置RTE以便在日語中使用最佳換詞符 {#jpwordwrap}

使用編AEM寫日語內容的作者可以將樣式應用於字元，以避免在不需要分段時換行。 這允許作者在期望的位置讓句子中斷。 此功能的樣式基於CSS樣式表中預定義的CSS類。

>[!NOTE]
>
>此功能至少需AEM要6.5 Service Pack 1。

要建立作者可以應用於日文文本的樣式，請執行以下步驟：

1. 在「樣式」節點下建立新節點。 請參閱 [指定新樣式](#stylesindropdown)。
   * 名稱: `jpn-word-wrap`
   * 類型: `nt:unstructure`

1. 添加屬性 `cssName` 以引用CSS類。 此類名是日文換行功能的保留名稱。
   * 名稱: `cssName`
   * 類型: `String`
   * 值： `jpn-word-wrap` (沒有前面的 `.`)

1. 將屬性文本添加到同一節點。 值是作者在選擇樣式時看到的樣式的名稱。
   * 名稱： `text`
*類型： 
`String`
   * 值: `Japanese word-wrap`

1. 建立樣式表並指定其路徑。 請參閱 [指定樣式表的位置](#locationofstylesheet)。 將以下內容添加到樣式表。 根據需要更改背景顏色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![使作者可以使用日文換行功能的樣式表](assets/rte_jpwordwrap_stylesheet.jpg)

## 配置段落格式 {#paraformats}

在RTE中創作的任何文本都放置在塊標籤中，預設值為 `<p>`。 通過啟用 `paraformat` 插件，您可以使用下拉選擇清單指定可分配給段落的其他塊標籤。 段落格式通過分配正確的塊標籤來確定段落類型。 作者可以使用「格式」(Format)選擇器選擇並分配它們。 示例塊標籤包括標準段落 &lt;p> 和標題 &lt;h1>。 &lt;h2>等等。

>[!CAUTION]
>
>此插件不適用於具有複雜結構的內容，如清單或表。

>[!NOTE]
>
>如果塊標籤，例如 &lt;hr> 標籤，無法分配給段落，它不是paraformat插件的有效使用案例。

首次啟用「段落格式」插件時，不提供預設的段落格式。 彈出清單為空。 要向作者提供段落格式，請執行以下操作：

* 啟用「格式」(Format)下拉選擇器清單。
* 指定可從下拉清單中選擇為段落格式的塊標籤。

對於以後（重新）的配置，例如要添加更多格式，請僅遵循說明的相關部分。

### 啟用「格式」下拉選擇器 {#formatselectorlist}

首先啟用參數格式插件：

1. 在元件中，導航到該節點 `<rtePlugins-node>/paraformat`。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 建立 `features` 屬性 `paraformat` 節點：

   * **名稱** `features`
   * **類型** `String`
   * **值** `*` （星號）

>[!NOTE]
如果插件未進一步配置，則會啟用以下預設格式：
* 段落 ( `<p>`)
* 標題 1 ( `<h1>`)
* 標題 2 ( `<h2>`)
* 標題 3 ( `<h3>`)
>


>[!CAUTION]
配置RTE的段落格式時，不要刪除段落標籤 &lt;p> 的子菜單。 如果 `<p>` 標籤被刪除，內容作者無法選擇 **段落格式** 選項。

### 指定可用的段落格式 {#paraformatsindropdown}

段落格式可供以下人士選擇：

1. 在元件定義中，導航到節點 `<rtePlugins-node>/paraformat`，在中建立 [啟用格式下拉選擇器](#styleselectorlist)。
1. 在 `paraformat` 節點建立新節點，以保存格式清單：

   * **名稱** `formats`
   * **類型** `cq:WidgetCollection`

1. 在 `formats` 節點，它保存單個格式的詳細資訊：

   * **名稱**，可以指定名稱，但它應適用於格式（例如myparaph、myheading1）。
   * **類型** `nt:unstructured`

1. 向此節點添加屬性以定義使用的塊標籤：

   * **名稱** `tag`
   * **類型** `String`
   * **值** 格式的塊標籤；例如：p、h1、h2等。

      不需要輸入定界尖括弧。

1. 在同一節點中添加另一個屬性，以便說明性文本顯示在下拉清單中：

   * **名稱** `description`
   * **類型** `String`
   * **值** 此格式的描述性文本；例如，段落、標題1、標題2等。 此文本顯示在「格式」選擇清單中。

1. 儲存變更。

   對每個所需格式重複步驟。

>[!CAUTION]
如果定義自定義格式，則預設格式(`<p>`。 `<h1>`。 `<h2>`, `<h3>`)。 重新建立 `<p>` 格式，因為它是預設格式。

## 配置特殊字元 {#spchar}

在標準安AEM裝中， `misctools` 為特殊字元啟用插件(`specialchars`)預設選擇立即可用；例如，版權和商標符號。

您可以配置RTE，使您自己選擇的字元可用；要麼定義不同的字元，要麼定義整個序列。

>[!CAUTION]
添加自己的特殊字元將覆蓋預設選擇。 如果需要，請（重新）在您自己的選擇中定義這些字元。

### 定義單個字元 {#definesinglechar}

1. 在元件中，導航到該節點 `<rtePlugins-node>/misctools`。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 建立 `features` 屬性 `misctools` 節點：

   * **名稱** `features`
   * **類型** `String[]`
   * **值** `specialchars`

          或 `String / *` 應用此插件的所有功能)

1. 下 `misctools` 建立一個節點以保存特殊字元配置：

   * **名稱** `specialCharsConfig`
   * **類型** `nt:unstructured`

1. 下 `specialCharsConfig` 建立另一個節點以保存字元清單：

   * **名稱** `chars`
   * **類型** `nt:unstructured`

1. 下 `chars` 添加新節點以保存單個字元定義：

   * **名稱** 可以指定名稱，但應反映字元；比如一半。
   * **類型** `nt:unstructured`

1. 在此節點中添加以下屬性：

   * **名稱** `entity`
   * **類型** `String`
   * **值** HTML表示所需字元；比如說， `&189;` 半份。

1. 儲存變更。

在CRXDE中，保存屬性後，將顯示表示的字元。 請參閱下面的「一半」示例。 重複上述步驟，使作者可以使用更多特殊字元。

![在CRXDE中，添加一個字元以在RTE工具欄中使用](assets/chlimage_1-106.png "在CRXDE中，添加一個字元以在RTE工具欄中使用")

### 定義字元範圍 {#definerangechar}

1. 使用步驟1到步驟3 [定義單個字元](#definesinglechar)。
1. 下 `chars` 添加新節點以保存字元範圍的定義：

   * **名稱** 可以指定名稱，但應反映字元範圍；比如鉛筆。
   * **類型** `nt:unstructured`

1. 在此節點下（根據特殊字元範圍命名）添加以下兩個屬性：

   * **名稱** `rangeStart`

      **類型** `Long`
      **值** 這樣 [Unicode](https://unicode.org/) 表示（小數）

   * **名稱** `rangeEnd`

      **類型** `Long`
      **值** 這樣 [Unicode](https://unicode.org/) 範圍中最後一個字元的表示（小數）

1. 儲存變更。

   例如，定義介於9998 - 10000之間的範圍時，將提供以下字元。

   ![在CRXDE中，定義要在RTE中提供的字元範圍](assets/chlimage_1-107.png)

   *圖：在CRXDE中，定義要在RTE中提供的字元範圍*

   ![RTE中提供的特殊字元將在彈出窗口中顯示給作者](assets/rtepencil.png "RTE中提供的特殊字元將在彈出窗口中顯示給作者")

## 配置表樣式 {#tablestyles}

樣式通常應用於文本，但也可以在表格或幾個表格單元格上應用一組單獨的樣式。 在「單元格屬性」或「表格屬性」對話框的「樣式」選擇器框中，作者可使用此類樣式。 當編輯文本元件（或衍生）中的表，而不是標準的「表」元件中的表時，這些樣式可用。

>[!NOTE]
您只能為傳統用戶介面定義表和單元格的樣式。

>[!NOTE]
在RTE元件中或從RTE元件中複製和貼上表取決於瀏覽器。 不是所有瀏覽器都支援開箱即用。 根據表結構和瀏覽器，可能會得到不同的結果。 例如，在Mozilla Firefox的Classic UI和Touch UI中，在RTE元件中複製和貼上表時，不會保留表的佈局。

1. 在元件中導航到節點 `<rtePlugins-node>/table`。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 建立 `features` 屬性 `table` 節點：

   * **名稱** `features`
   * **類型** `String`
   * **值** `*` （星號）

   >[!NOTE]
   如果不想啟用所有表功能，可以建立 `features` 屬性：
   * **類型** `String[]`
   * **值**(s)下列其中一項或兩者：
      * `table` 允許編輯表格屬性；包括樣式。
      * `cellprops` 允許編輯單元格屬性，包括樣式。


1. 定義CSS樣式表的位置以引用這些樣式表。 請參閱 [指定樣式表的位置](#locationofstylesheet) 與定義 [文本樣式](#textstyles)。 如果定義了其它樣式，則可以定義位置。
1. 在 `table` 節點建立以下新節點（根據需要）:

   * 定義整個表格的樣式(可在 **表屬性**):

      * **名稱** `tableStyles`
      * **類型** `cq:WidgetCollection`
   * 定義單個單元格的樣式(可在 **單元格屬性**):

      * **名稱** `cellStyles`
      * **類型** `cq:WidgetCollection`


1. 建立新節點(位於 `tableStyles` 或 `cellStyles` 節點（如適用）表示單個樣式：

   * **名稱** 可以指定名稱，但應反映樣式。
   * **類型** `nt:unstructured`

1. 在此節點上建立以下屬性：

   * 定義要引用的CSS樣式

      * **名稱** `cssName`
      * **類型** `String`
      * **值** CSS類的名稱(前面沒有 `.`，例如， `cssClass` 而不是 `.cssClass`)
   * 定義要在下拉選擇器中顯示的描述性文本

      * **名稱** `text`
      * **類型** `String`
      * **值** 要出現在選擇清單中的文本


1. 保存所有更改。

對每個所需樣式重複上述步驟。

### 在表中配置隱藏的標頭以便訪問 {#hiddenheader}

有時，您可以在列標題中建立不帶可視文本的資料表，假定標題的用途由列與其他列的可視關係所隱含。 在這種情況下，有必要在標題單元格中的單元格中提供隱藏的內文，以允許螢幕閱讀器和其他輔助技術幫助具有各種需求的讀者瞭解該欄的目的。

為了增強此類場景中的可訪問性，RTE支援隱藏的頭單元格。 此外，它還提供與表中隱藏的標頭相關的配置設定。 這些設定允許您在編輯和預覽模式下對隱藏的標題應用CSS樣式。 要幫助作者在編輯模式下識別隱藏的標題，請在代碼中包括以下參數：

* `hiddenHeaderEditingCSS`:指定編輯RTE時在隱藏標題單元格上應用的CSS類的名稱。
* `hiddenHeaderEditingStyle`:指定在編輯RTE時應用於隱藏標題單元格的樣式字串。

如果在代碼中同時指定CSS和「樣式」字串，則CSS類優先於樣式字串，並可能覆蓋「樣式」字串所做的任何配置更改。

要幫助作者在預覽模式下對隱藏的標題應用CSS，可以在代碼中包含以下參數：

* `hiddenHeaderClassName`:指定在預覽模式下應用於隱藏標題單元格的CSS類的名稱。
* `hiddenHeaderStyle`:指定在預覽模式下應用於隱藏標題單元格的樣式字串。

如果在代碼中同時指定CSS和「樣式」字串，則CSS類優先於樣式字串，並可能覆蓋「樣式」字串所做的任何配置更改。

## 為拼寫檢查器添加詞典 {#adddict}

激活拼寫檢查插件後，RTE將使用字典來處理每種適當的語言。 然後根據網站的語言選擇，即採用子樹的語言屬性或從URL中提取語言；例如。 這樣 `/en/` 分支被檢查為英文， `/de/` 德語。

>[!NOTE]
消息 `Spell checking failed` 查看是否嘗試檢查未安裝的語言。 標準詞典位於 `/libs/cq/spellchecker/dictionaries`以及相應的自述檔案。 不要修改檔案。

標準安裝AEM包含美國英語詞典(`en_us`)和英語(`en_gb`)。 要添加更多詞典，請執行以下步驟。

1. 導航到該頁 [https://extensions.openoffice.org/](https://extensions.openoffice.org/)。

1. 執行下列操作之一以查找您選擇的語言的詞典：

   * 搜索您選擇的語言的詞典。 在字典頁面上，找到指向原始源或作者網頁的連結。 在此頁面上找到v2.x的字典檔案。
   * 在以下位置搜索v2.x字典檔案 [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries)。

1. 下載包含拼寫定義的存檔。 提取檔案系統上的存檔內容。

   >[!CAUTION]
   僅字典 `MySpell` 支援OpenOffice.org v2.0.1或更低版本的格式。 由於字典現在是存檔檔案，建議在下載後驗證存檔檔案。

1. 找到.aff和.dic檔案。 將檔案名保留為小寫。 比如說， `de_de.aff` 和 `de_de.dic`。
1. 將.aff和.dic檔案載入到儲存庫中，位於 `/apps/cq/spellchecker/dictionaries`。

>[!NOTE]
RTE拼寫檢查器可以按需使用。 當您開始鍵入文本時，它不會自動運行。 要運行拼寫檢查器，請按一下 [!UICONTROL 拼寫檢查器] 的子菜單。 RTE檢查單詞的拼寫並突出顯示拼錯的單詞。
如果合併拼寫檢查器建議的任何更改，則文本的狀態將不再突出顯示。 要運行拼寫檢查器，請再次點擊/按一下「拼寫檢查器」按鈕。

## 配置撤消和重做操作的歷史記錄大小 {#undohistory}

RTE允許作者撤消或重做幾次最後的編輯。 預設情況下，50個編輯儲存在歷史記錄中。 您可以根據需要配置此值。

1. 在元件中導航到節點 `<rtePlugins-node>/undo`。 如果這些節點不存在，請建立它們。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 在 `undo` 節點建立屬性：

   * **名稱** `maxUndoSteps`
   * **類型** `Long`
   * **值** 要在歷史記錄中保存的撤消步驟數。 預設值為50。 使用 `0` 完全禁用撤消/重做。

1. 儲存變更。

## 配置頁籤大小 {#tabsize}

在任何文本中按制表符時，都會插入預定義數的空格；預設情況下，這是三個非中斷空格和一個空格。

要定義標籤大小，請執行以下操作：

1. 在元件中，導航到該節點 `<rtePlugins-node>/keys`。 如果節點不存在，則建立這些節點。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 在 `keys` 節點建立屬性：

   * **名稱** `tabSize`
   * **類型** `String`
   * **值** 用於制表符的空格字元數

1. 儲存變更。

## 設定縮進邊距 {#indentmargin}

啟用縮進（預設）時，可以定義縮進大小：

>[!NOTE]
此縮進大小僅應用於文本的段落（塊）;不影響實際清單的縮進。

1. 在元件中導航到節點 `<rtePlugins-node>/lists`。 如果這些節點不存在，請建立它們。 有關詳細資訊，請參閱 [激活插件](#activateplugin)。
1. 在 `lists` 節點建立 `identSize` 參數：

   * **名稱**: `identSize`
   * **類型**: `Long`
   * **值**:縮進邊距所需的像素數。

## 配置可編輯空間的高度 {#editablespace}

>[!NOTE]
僅當在對話框中使用RTE時（在傳統UI中不是就地編輯），才適用此選項。

可定義元件對話框中顯示的可編輯空間的高度：

1. 在 `../items/text` 節點（在元件的對話框定義中），建立新屬性：

   * **名稱** `height`
   * **類型** `Long`
   * **值** 編輯畫布的高度（以像素為單位）。

   >[!NOTE]
   這不會更改對話框窗口的高度。

1. 儲存變更。

## 配置連結的樣式和協定 {#linkstyles}

在中添加連結AEM時，可以定義：

* 要使用的CSS樣式
* 自動接受協定

要配置如何從其他程式AEM添加連結，請定義HTML規則。

1. 使用CRXDE Lite，查找項目的文本元件。
1. 在與 `<rtePlugins-node>`，即在的父節點下建立節點 `<rtePlugins-node>`:

   * **名稱** `htmlRules`
   * **類型** `nt:unstructured`

   >[!NOTE]
   的 `../items/text` 節點具有以下屬性：
   * **名稱** `xtype`
   * **類型** `String`
   * **值** `richtext`

   位置 `../items/text` 節點可能會隨對話框的結構而變化；兩個例子 `/apps/myProject>/components/text/dialog/items/text` 和 `/apps/<myProject>/components/text/dialog/items/panel/items/text`。

1. 下 `htmlRules`，可以建立新節點。

   * **名稱** `links`
   * **類型** `nt:unstructured`

1. 在 `links` 節點根據需要定義屬性：

   * 內部連結的CSS樣式：

      * **名稱** `cssInternal`
      * **類型** `String`
      * **值** CSS類的名稱(前面沒有「。」;比如說， `cssClass` 而不是 `.cssClass`)
   * 外部連結的CSS樣式

      * **名稱** `cssExternal`
      * **類型** `String`
      * **值** CSS類的名稱(前面沒有「。」;比如說， `cssClass` 而不是 `.cssClass`)
   * 有效陣列 **協定**。 支援的協定 `http://`。 `https://`。 `file://`, `mailto:`。

      * **名稱** `protocols`
      * **類型** `String[]`
      * **值**(s)一個或多個協定
   * **預設協定** （類型屬性） **字串**):用戶未顯式指定協定時使用的協定。

      * **名稱** `defaultProtocol`
      * **類型** `String`
      * **值**&#x200B;一個或多個預設協定
   * 如何處理連結的目標屬性的定義。 建立新節點：

      * **名稱** `targetConfig`
      * **類型** `nt:unstructured`

      在節點上 `targetConfig`:定義所需屬性：

      * 指定目標模式：

         * **名稱** `mode`
         * **類型** `String`)
         * **值**(s):

            * `auto`:意味著選擇了自動目標

               (由 `targetExternal` 外部連結或 `targetInternal` )。

            * `manual`:不適用於此上下文
            * `blank`:不適用於此上下文
      * 內部連結的目標：

         * **名稱** `targetInternal`
         * **類型** `String`
         * **值** 內部連結的目標(僅在模式為 `auto`)
      * 外部連結的目標：

         * **名稱** `targetExternal`
         * **類型** `String`
         * **值** 外部連結的目標(僅在模式為 `auto`)。








1. 保存所有更改。
