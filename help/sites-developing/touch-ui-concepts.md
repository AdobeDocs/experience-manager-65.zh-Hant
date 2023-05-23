---
title: 啟用觸摸AEM的UI的概念
seo-title: Concepts of the AEM Touch-Enabled UI
description: 通過AEM5.6Adobe，為作者環境引入了一種新的觸控優化用戶介面，並設計了響應性設計
seo-description: With AEM 5.6 Adobe introduced a new touch-optimized UI with responsive design for the author environment
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 1%

---

# 啟用觸摸AEM的UI的概念{#concepts-of-the-aem-touch-enabled-ui}

具AEM有觸摸式用戶介面 [響應設計](/help/sites-authoring/responsive-layout.md) 適用於設計為在觸摸和台式機設備上運行的作者環境。

>[!NOTE]
>
>啟用觸摸的UI是標準UIAEM。 標準UI已棄AEM用6.4。

啟用觸摸的UI包括：

* 套件標題：
   * 顯示徽標
   * 提供指向全局導航的連結
   * 提供指向其他一般操作的連結；如搜索、幫助、Marketing Cloud解決方案、通知和用戶設定。
* 左滑軌（在需要時顯示並可高速顯示），可顯示：
   * 時間軸
   * 引用
   * 篩選條件
* 導航標頭，它同樣與上下文相關，可顯示：
   * 指示當前正在使用哪個控制台和/或您在該控制台中的位置
   * 左滑軌的選擇
   * 階層連結
   * 訪問適當 **建立** 動作
   * 查看選擇
* 內容區域：
   * 列出內容項（無論是頁面、資產、論壇帖子等）
   * 可以根據請求格式化，例如列、卡或清單
   * 使用響應設計（顯示器根據設備和/或窗口大小自動調整大小）
   * 使用無限滾動（不再分頁，所有項都在一個窗口中列出）

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>幾乎所AEM有功能都移植到了啟用觸摸的UI。 但是，在某些有限情況下，功能將恢復為經典UI。 請參閱 [觸摸UI功能狀態](/help/release-notes/touch-ui-features-status.md) 的子菜單。

通過Adobe設計的觸摸式用戶介面，可跨多個產品提供用戶體驗的一致性。 它基於：

* **珊瑚UI** (CUI)實現Adobe的視覺樣式，用於啟用觸摸的用戶介面。 Coral UI提供您的產品/項目/ Web應用程式採用UI可視樣式所需的一切。
* **花崗岩UI** 元件是使用Coral UI構建的。

啟用觸摸的UI的基本原則是：

* 移動優先（考慮台式機）
* 響應性設計
* 上下文相關顯示
* 可重用
* 包括嵌入式參考文檔
* 包括嵌入式test
* 自底向上設計，以確保這些原則適用於每個元素和元件

有關啟用觸摸的UI結構的進一步概述，請參閱文章 [啟用觸摸AEM的UI的結構](/help/sites-developing/touch-ui-structure.md)。

## 技AEM術堆棧 {#aem-technology-stack}

將AEMGranite平台用作基礎，Granite平台包括Java內容儲存庫。

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

花崗岩是Adobe的Open Web堆棧，提供各種元件，包括：

* 應用程式啟動程式
* OSGi框架，所有部署都部署在該框架中
* 若干OSGi簡編服務，以支援建築應用
* 提供各種日誌API的全面日誌框架
* JCR API規範的CRX儲存庫實現
* Apache Sling Web框架
* 當前CRX產品的其他部件

>[!NOTE]
>
>花崗岩作為Adobe內的開放式開發項目運行：對規則、討論和問題的貢獻來自整個公司。
>
>但花崗岩 **不** 開源項目。 它主要基於幾個開源項目（尤其是Apache Sling、Felix、Jackrabbit和Lucene），但Adobe在公共項目和內部項目之間划出了一條清晰的界線。

## 花崗岩UI {#granite-ui}

花崗岩工程平台還提供了基礎UI框架。 其主要目標是：

* 提供粒度UI小部件
* 實現UI概念並說明最佳做法（長清單呈現、清單篩選、對象CRUD、CUD嚮導……）
* 提供可擴展且基於插件的管理UI

這些要求符合：

* 尊重「移動優先」
* 可擴展
* 易於覆蓋

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[獲取檔案](assets/graniteui.pdf)
花崗岩介面：

* 使用Sling的REST風格體系結構
* 實施旨在構建以內容為中心的Web應用程式的元件庫
* 提供粒度UI小部件
* 提供預設的標準化UI
* 可擴展
* 專為移動和台式機設備設計（首先考慮移動）
* 可用於任何基於花崗岩的平台/產品/項目；AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [花崗岩UI基礎元件](#granite-ui-foundation-components)
此基礎元件庫可供其他庫使用或擴展。
* [花崗岩UI管理元件](#granite-ui-administration-components)

### 客戶端與伺服器端 {#client-side-vs-server-side}

Granite UI中的客戶端與伺服器通信由超文本而不是對象組成，因此不需要客戶端瞭解業務邏輯

* 伺服器用語義資料豐富了HTML
* 客戶端通過超媒體（交互）豐富超文本

![chlimage_1-83](assets/chlimage_1-83.png)

#### 客戶端 {#client-side}

這使用HTML辭彙的擴展，以便作者能夠表達他們打算構建互動式Webapp的意圖。 這是一種類似的方法 [韋阿里亞](https://www.w3.org/TR/wai-aria/) 和 [微格式](https://microformats.org/)。

它主要由JS代碼和CSS代碼解釋的交互模式（例如非同步提交表單）的集合組成，這些模式在客戶端運行。 客戶端的作用是增強標籤（作為伺服器提供的超媒體功能）的交互性。

客戶端獨立於任何伺服器技術。 只要伺服器提供適當的標籤，客戶端就可以完成其角色。

目前，JS和CSS代碼以Granite的形式傳送 [客戶端](/help/sites-developing/clientlibs.md) 在類別下：

`granite.ui.foundation and granite.ui.foundation.admin`

這些內容作為內容包的一部分提供：

`granite.ui.content`

#### 伺服器端 {#server-side}

這由使作者能夠 *編* 網路應用很快。 開發人員開發元件，將元件組裝成webapp。 伺服器端的作用是為客戶端提供超媒體可負擔（標籤）。

目前，這些元件位於Granite儲存庫中，地址為：

`/libs/granite/ui/components/foundation`

此內容作為內容包的一部分提供：

`granite.ui.content`

### 與經典UI的區別 {#differences-with-the-classic-ui}

Granite UI和ExtJS（用於經典UI）之間的差異也值得關注：

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>花崗岩UI</strong></td>
  </tr>
  <tr>
   <td>遠程過程調用<br /> </td>
   <td>狀態轉換</td>
  </tr>
  <tr>
   <td>資料傳輸對象</td>
   <td>超媒體</td>
  </tr>
  <tr>
   <td>客戶端知道伺服器內部</td>
   <td>客戶端不知道內部</td>
  </tr>
  <tr>
   <td>"胖客戶"</td>
   <td>"瘦客戶機"</td>
  </tr>
  <tr>
   <td>專用客戶端庫</td>
   <td>通用客戶端庫</td>
  </tr>
 </tbody>
</table>

### 花崗岩UI基礎元件 {#granite-ui-foundation-components}

的 [花崗岩UI地基元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 提供構建任何UI所需的基本構建塊。 其中包括：

* 按鈕
* 超連結
* 使用者頭像

可在以下位置找到基礎元件：

`/libs/granite/ui/components/foundation`

此庫包含每個Coral元素的Granite UI元件。 元件是內容驅動的，其配置駐留在儲存庫中。 這使得不用手寫HTML標籤就能合成Granite UI應用程式。

用途:

* 用於HTML元素的元件模型
* 組分組合物
* 自動設備和功能測試

實施:

* 基於儲存庫的合成和配置
* 利用花崗岩平台提供的測試設施
* JSP模板

此基礎元件庫可供其他庫使用或擴展。

### ExtJS和相應花崗岩UI元件 {#extjs-and-corresponding-granite-ui-components}

升級ExtJS代碼以使用Granite UI時，以下清單提供了ExtJS類型和節點類型及其等效的Granite UI資源類型的方便概述。

| **ExtJS xtype** | **花崗岩UI資源類型** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **節點類型** | **花崗岩UI資源類型** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### 花崗岩UI管理元件 {#granite-ui-administration-components}

的 [花崗岩UI管理元件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 在基礎元件上構建，以提供任何管理應用程式都可以實現的通用構造塊。 其中包括：

* 全局導航欄
* 軌（骨架）
* 搜索面板

用途:

* 管理應用程式的統一外觀
* Rad管理應用程式

實施:

* 使用基礎元件的預定義元件
* 元件可以定制

## 珊瑚UI {#coral-ui}

CoralUI.pdf

[獲取檔案](assets/coralui.pdf)
Coral UI(CUI)是Adobe的視覺風格在啟用觸摸的UI中的實現，旨在提供多種產品中用戶體驗的一致性。 Coral UI提供了創作環境中使用的視覺樣式所需的一切。

>[!CAUTION]
>
>Coral UI是一個UI庫，可供AEM客戶在其產品許可使用範圍內構建應用程式和Web介面。
>
>僅允許使用Coral UI:
>
>
>* 當它已發運並捆綁在一起AEM。
>* 用於擴展創作環境的現有UI。
>* Adobe公司宣傳資料、廣告和演示。
>* Adobe標籤應用程式的UI（字型不能隨時用於其他用途）。
>* 有少量自定義。
>
>應避免在以下位置使用Coral UI:
>
>* 文檔和其他與Adobe無關的項目。
>* 內容建立環境（前面的項目可能由其他項目生成）。
>* 未明確連接到Adobe的應用程式/元件/網頁。
>


Coral UI是用於開發Web應用程式的構建塊的集合。

![chlimage_1-84](assets/chlimage_1-84.png)

每個模組從開始設計為模組化，根據其主要角色形成一個不同的層。 儘管這些層設計為相互支援，但如果需要，也可以獨立使用。 這使Coral在任何可HTML的環境中都能實現用戶體驗。

對於Coral UI，不必強制使用特定開發模式和/或平台。 Coral的主要目標是提供統一且乾淨的HTML5標籤，與發出該標籤的實際方法無關。 這可能用於客戶端或伺服器端呈現、模板、JSP、PHP甚至AdobeFlashRIA應用程式 — 僅舉幾個例子。

### HTML元素 — 標籤層 {#html-elements-the-markup-layer}

HTML元素為所有基本UI元素（包括導航欄、按鈕、菜單、導軌等）提供共同的外觀。

在最基本的級別，HTML元素是具有專用類名的HTML標籤。 更複雜的元素可以由多個標籤組成，它們彼此嵌套（以特定方式）。

CSS用於提供實際外觀。 為了能夠容易地定制外觀（例如，對於品牌推廣），實際樣式值被聲明為由 [減](https://lesscss.org/) 運行時預處理器。

用途:

* 為基本的UI元素提供通用的外觀
* 提供預設網格系統

實施:

* HTML標籤，其樣式受 [引導](https://twitter.github.com/bootstrap/)
* 類在LESS檔案中定義
* 表徵圖定義為字型空格

例如，標注：

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

顯示為：

![chlimage_1-85](assets/chlimage_1-85.png)

外觀在LESS中定義，它通過專用類名與元素綁定（為簡便起見，以下提取已縮短）:

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

實際值在LESS變數檔案中定義（為了簡便起見，已縮短以下提取）:

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 元素插件 {#element-plugins}

許多HTML元素需要顯示某種動態行為，如開啟和關閉彈出菜單。 這是元素插件的角色，它通過使用JavaScript操作DOM來完成此類任務。

插件為：

* 設計為在特定DOM元素上操作。 例如，對話框插件需要查找 `DIV class=dialog`
* 一般性。 例如，佈局管理器為任何 `DIV` 或 `LI` 元素

可以通過以下任一方法使用參數自定義插件行為：

* 通過javascript調用傳遞參數
* 使用專用 `data-*` 與HTML標籤關聯的屬性

儘管開發人員可以為任何插件選擇最佳方法，但經驗法則是：

* `data-*` 與HTML佈局相關的選項的屬性。 例如，要指定列數
* 與資料相關的功能的API選項/類。 例如，構造要顯示的項清單

同樣的概念用於實現表單驗證。 對於要驗證的元素，必須將所需的輸入表單指定為自定義 `data-*` 屬性。 然後，此屬性將用作驗證插件的選項。

>[!NOTE]
>
>HTML5 — 本機表單驗證應盡可能使用和/或展開。

用途:

* 為HTML元素提供動態行為
* 提供純CSS不可能的自定義佈局
* 執行表單驗證
* 執行高級DOM操作

實施:

* jQuery插件，與特定DOM元素關聯
* 使用 `data-*` 自定義行為的屬性

示例標注的提取(注意指定為data-&#42; 屬性):

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

調用jQuery插件：

```
$(‘.cards’).cardlayout ();
```

這將顯示為：

![chlimage_1-86](assets/chlimage_1-86.png)

的 `cardLayout` 插件列出了 `UL` 元素，並考慮父項的寬度。

### HTML元素小部件 {#html-elements-widgets}

小部件將一個或多個基本元素與Javascript插件組合，以形成「更高級別」的UI元素。 它們可以實現比單個元素更複雜的行為，也可以實現更複雜的外觀和感覺。 標籤選取器或滑軌小部件就是很好的示例。

小部件可以觸發和偵聽自定義事件，以與頁面上的其他小部件協作。 某些小部件實際上是使用CoralHTML元素的本機jQuery小部件。

用途:

* 實現顯示複雜行為的更高級別UI元素
* 觸發和處理事件

實施:

* jQuery插件+HTML標籤
* 可利用客戶端/伺服器端模板

示例標注為：

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

調用jQuery插件（帶選項）:

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

插件發出HTML標籤（此標籤使用基本元素，這些元素可能在內部使用其他插件）:

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

這將顯示為：

![chlimage_1-87](assets/chlimage_1-87.png)

### 實用程式庫 {#utility-library}

此庫是Javascript幫助程式插件和/或函式的集合，這些插件和/或函式包括：

* UI獨立
* 但對於構建功能齊全的Web應用程式至關重要

這些包括XSS處理和事件匯流排。

儘管HTML元素插件和小部件可能依賴於實用程式庫提供的功能，但實用程式庫不能對元素和小部件本身有任何硬依賴關係。

用途:

* 提供通用功能
* 事件匯流排實現
* 客戶端模板
* XSS

實施:

* jQuery插件或符合AMD的JavaScript模組
