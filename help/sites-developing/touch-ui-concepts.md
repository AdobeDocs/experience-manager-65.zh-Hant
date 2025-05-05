---
title: Adobe Experience Manager觸控式UI的概念
description: Adobe在Adobe Experience Manager 5.6中推出了全新觸控最佳化UI，搭配回應式設計，適合製作環境
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2147'
ht-degree: 1%

---

# Adobe Experience Manager觸控式UI的概念{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager (AEM)提供觸控式UI，其中[回應式設計](/help/sites-authoring/responsive-layout.md)適用於製作環境，可在觸控式和桌上型裝置上運作。

>[!NOTE]
>
>觸控式UI是AEM的標準UI。 AEM 6.4已棄用傳統UI。

觸控式UI包含：

* 套裝標題：
   * 顯示標誌
   * 提供全域導覽的連結
   * 提供其他一般動作的連結；例如搜尋、說明、Experience Cloud解決方案、通知和使用者設定。
* 左側邊欄（需要時顯示且可隱藏），其中可顯示：
   * 時間表
   * 參考
   * 篩選條件
* 導覽標頭(同樣是內容感應式，可顯示：
   * 指出您目前正在使用哪個主控台，或您的位置，或同時使用兩者
   * 左側邊欄的選取專案
   * 導覽列
   * 存取適當的&#x200B;**建立**&#x200B;動作
   * 檢視選取專案
* 內容區域：
   * 列出內容專案（無論是頁面、資產、論壇帖子等）
   * 可依要求格式化，例如，欄、卡片或清單
   * 使用回應式設計（顯示器會根據您的裝置和/或視窗大小自動調整大小）
   * 使用無限捲動（不再分頁，所有專案都列在一個視窗中）

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>幾乎所有的AEM功能皆已移植至觸控式UI。 但是，在某些有限的情況下，功能會回覆為傳統UI。 如需詳細資訊，請參閱[觸控式UI功能狀態](/help/release-notes/touch-ui-features-status.md)。

Adobe將觸控式UI設計為可提供跨多個產品的一致性使用者體驗。 其依據為：

* **Coral UI** (CUI)針對觸控式UI實作Adobe的視覺樣式。 Coral UI提供產品/專案/Web應用程式採用UI視覺樣式所需的一切。
* **Granite UI**&#x200B;元件是使用Coral UI建置。

觸控式UI的基本原則為：

* 行動優先（以桌上型電腦為主）
* 回應式設計
* 內容相關顯示
* 可重複使用
* 包含內嵌參考檔案
* 包含內嵌測試
* 由下而上的設計，確保這些原則套用至每個元素和元件

如需觸控式UI結構的詳細概觀，請參閱[AEM觸控式UI的結構](/help/sites-developing/touch-ui-structure.md)。

## AEM技術棧疊 {#aem-technology-stack}

AEM以Granite平台為基礎，Granite平台包含Java™內容存放庫等。

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite是Adobe的Open Web棧疊，提供各種元件，包括：

* 應用程式啟動器
* 所有內容皆部署至的OSGi框架
* 支援建置應用程式的若干OSGi簡編服務
* 提供各種記錄API的完整記錄架構
* JCR API規格的CRX存放庫實作
* Apache Sling Web架構
* 目前CRX產品的其他部分

>[!NOTE]
>
>Granite在Adobe中以開放開發專案的方式執行：對程式碼、討論和問題的貢獻來自整個公司。
>
>不過，Granite **不是**&#x200B;開放原始碼專案。 它在很大程度上取決於幾個開放原始碼專案（尤其是Apache Sling、Felix、Jackrabbit和Lucene），但Adobe在公開和內部之間劃清了界限。

## Granite UI {#granite-ui}

Granite工程平台也提供基礎UI架構。 其主要目標是：

* 提供精細的UI Widget
* 實施UI概念並說明最佳實務（長清單呈現、清單篩選、物件CRUD、CUD精靈……）
* 提供可擴充的外掛程式式管理UI

這些符合需求：

* 尊重「行動優先」
* 可擴充
* 輕鬆覆寫

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[取得檔案](assets/graniteui.pdf)
Granite UI：

* 使用Sling的RESTful架構
* 實作元件程式庫，用於建置以內容為中心的網頁應用程式
* 提供精細的UI Widget
* 提供預設的標準化UI
* 可擴充
* 專為行動裝置和桌上型裝置設計（以行動裝置為優先）
* 可用於任何Granite型平台/產品/專案；例如AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI Foundation元件](#granite-ui-foundation-components)
此基礎元件程式庫可供其他程式庫使用或擴充。
* [Granite UI管理元件](#granite-ui-administration-components)

### 使用者端與伺服器端 {#client-side-vs-server-side}

Granite UI中的使用者端 — 伺服器通訊是由超文字組成，而非物件，因此使用者端不需要瞭解商業邏輯

* 伺服器使用語意資料豐富HTML
* 使用者端使用超媒體（互動）豐富超文字

![chlimage_1-83](assets/chlimage_1-83.png)

#### 使用者端 {#client-side}

這會使用HTML辭彙的擴充功能，讓作者可表達建立互動式Web應用程式的意向。 這是[WAI-ARIA](https://www.w3.org/TR/wai-aria/)和[微格式](https://microformats.org/)的類似方法。

它主要由使用者端執行的JS和CSS程式碼所解譯的互動模式（例如，非同步提交表單）集合組成。 使用者端的角色是增強互動的標籤（由伺服器提供作為超媒體提供）。

使用者端不受任何伺服器技術的限制。 只要伺服器提供適當的標籤，使用者端就可以履行其角色。

目前JS和CSS程式碼會以Granite [clientlibs](/help/sites-developing/clientlibs.md)傳遞，位於類別下：

`granite.ui.foundation and granite.ui.foundation.admin`

這些內容會在內容套件中提供：

`granite.ui.content`

#### 伺服器端 {#server-side}

這是由Sling元件的集合所組成，可讓作者快速&#x200B;*撰寫*&#x200B;一個Web應用程式。 開發人員會開發元件，而作者會將元件組合成網頁應用程式。 伺服器端的角色是為使用者端提供超媒體可供性（標籤）。

目前，元件位於Granite存放庫中：

`/libs/granite/ui/components/foundation`

這會作為內容套件的一部分提供：

`granite.ui.content`

### 與傳統UI的差異 {#differences-with-the-classic-ui}

Granite UI和ExtJS （用於傳統UI）之間的差異也令人感興趣：

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>遠端程式呼叫<br /> </td>
   <td>狀態轉換</td>
  </tr>
  <tr>
   <td>資料傳輸物件</td>
   <td>超媒體</td>
  </tr>
  <tr>
   <td>使用者端知道伺服器內部</td>
   <td>使用者端不知道內部網路</td>
  </tr>
  <tr>
   <td>「胖使用者端」</td>
   <td>「精簡型使用者端」</td>
  </tr>
  <tr>
   <td>專門的使用者端程式庫</td>
   <td>通用使用者端程式庫</td>
  </tr>
 </tbody>
</table>

### Granite UI Foundation元件 {#granite-ui-foundation-components}

[Granite UI基礎元件](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)提供建置任何UI所需的基本建置區塊。 其中包括：

* 按鈕
* 超連結
* 用戶頭像

基礎元件可在下列位置找到：

`/libs/granite/ui/components/foundation`

此程式庫包含每個Coral元素的Granite UI元件。 元件是內容驅動的，其組態位於存放庫中。 如此一來，您就可以撰寫一個Granite UI應用程式，而無需手動撰寫HTML標籤。

用途：

* HTML元素的元件模型
* 元件組合
* 自動單元與功能測試

實作：

* 存放庫型構成和設定
* 使用Granite平台提供的測試設施
* JSP範本

此基礎元件程式庫可供其他程式庫使用或擴充。

### ExtJS和對應的Granite UI元件 {#extjs-and-corresponding-granite-ui-components}

升級ExtJS程式碼以使用Granite UI時，下列清單可提供ExtJS xtype和節點型別及其同等的Granite UI資源型別的便利概述。

| **ExtJS xtype** | **Granite UI資源型別** |
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
| `tags` | `granite/ui/components/foundation/form/autocomplete` `cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **節點型別** | **Granite UI資源型別** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container` `granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Granite UI管理元件 {#granite-ui-administration-components}

[Granite UI管理元件](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)建置在基礎元件上，以提供任何管理應用程式都可以實作的通用建置區塊。 其中包括：

* 全域導覽列
* 邊欄（骨架）
* 搜尋面板

用途：

* 統一的管理應用程式外觀
* 管理應用程式的RAD

實作：

* 使用基礎元件的預先定義元件
* 元件可自訂

## Coral UI {#coral-ui}

CoralUI.pdf

[取得檔案](assets/coralui.pdf)
Coral UI (CUI)是Adobe視覺樣式的實作，適用於觸控式UI，旨在為多個產品的使用者體驗提供一致性。 Coral UI提供您採用製作環境所使用的視覺樣式所需的一切。

>[!CAUTION]
>
>Coral UI是一個UI程式庫，可供AEM客戶在其授權使用產品的範圍內建置應用程式和Web介面。
>
>僅允許使用Coral UI：
>
>
>* 當它出貨並與AEM捆綁時。
>* 用於擴充編寫環境的現有UI時。
>* Adobe企業附屬資料、廣告和簡報。
>* Adobe品牌應用程式的UI （字型不能隨時用於其他用途）。
>* 進行微幅自訂。
>
>在下列情況下應避免使用Coral UI：
>
>* 與Adobe無關的檔案和其他專案。
>* 內容建立環境（前述專案可能由其他人產生）。
>* 未明確連線到Adobe的應用程式/元件/網頁。
>

Coral UI是開發Web應用程式的建置區塊集合。

![chlimage_1-84](assets/chlimage_1-84.png)

從一開始就是模組化的，每個模組都會根據其主要角色形成不同的階層。 雖然這些圖層的設計目的就是要互相支援，但如果需要，也可以單獨使用。 如此一來，您就可以在任何具備HTML功能的環境中實作Coral的使用者體驗。

使用Coral UI時，不需要強制使用特定開發模型和/或平台。 Coral的主要目標是提供統一且乾淨的HTML5標籤，與用來發出此標籤的實際方法無關。 這可用於使用者端或伺服器端轉譯、範本、JSP、PHP或甚至AdobeFlashRIA應用程式 — 僅舉幾例。

### HTML元素 — 標籤層 {#html-elements-the-markup-layer}

HTML元素提供所有基本UI元素（包括導覽列、按鈕、功能表、邊欄等）的共同外觀。

在最基本的層級，HTML元素是具有專用類別名稱的HTML標籤。 更複雜的元素可由多個標籤組成，彼此巢狀內嵌（以特定方式）。

CSS是用來提供實際的外觀和風格。 為了能夠輕鬆自訂外觀（例如，品牌化的情況），實際樣式值會宣告為變數，在執行階段由[LESS](https://lesscss.org/)前置處理器展開。

用途：

* 提供基本的UI元素以及常見的外觀
* 提供預設的格點系統

實作：

* 具有靈感來自[Bootstrap](https://twitter.github.com/bootstrap/)之樣式的HTML標籤
* 類別是在LESS檔案中定義
* 圖示定義為字型拼字

例如，標籤：

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

顯示為：

![chlimage_1-85](assets/chlimage_1-85.png)

外觀和感覺在LESS中定義，以專屬類別名稱繫結至元素（為了簡潔起見，已縮短下列擷取）：

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

實際值是在LESS變數檔案中定義（為了簡潔起見，已縮短下列擷取）：

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 元素外掛程式 {#element-plugins}

許多HTML元素需要表現出某種動態行為，例如開啟和關閉彈出式選單。 這是元素外掛程式的角色，可透過使用JavaScript操控DOM來完成這類工作。

外掛程式為：

* 設計用於操作特定DOM元素。 例如，對話方塊外掛程式預期會找到`DIV class=dialog`
* 本質上是通用的。 例如，配置管理員會為`DIV`或`LI`個元素的任何清單提供配置

若要使用引數自訂外掛程式的行為，您可以：

* 以JavaScript呼叫傳遞引數
* 使用與HTML標籤關聯的專用`data-*`屬性

雖然開發人員可以為任何外掛程式選取最佳方法，但經驗法則是：

* 與HTML配置相關之選項的`data-*`屬性。 例如，指定欄數
* 與資料相關功能的API選項/類別。 例如，建構要顯示的專案清單

相同的概念可用於實施表單驗證。 對於要驗證的元素，您必須指定必要的輸入表單作為自訂`data-*`屬性。 此屬性接著會作為驗證外掛程式的選項。

>[!NOTE]
>
>應儘可能使用HTML5原生表單驗證並/或加以擴充。

用途：

* 提供HTML元素的動態行為
* 提供純CSS所無法提供的自訂版面
* 執行表單驗證
* 執行進階DOM操作

實作：

* jQuery外掛程式，繫結至特定DOM元素
* 使用`data-*`屬性來自訂行為

範例標籤的擷取（請注意指定為資料 — &#42;屬性的選項）：

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

對jQuery外掛程式的呼叫：

```
$('.cards').cardlayout ();
```

這顯示為：

![chlimage_1-86](assets/chlimage_1-86.png)

`cardLayout`外掛程式會根據元素各自的高度並考量父項的寬度，來配置括住的`UL`元素。

### HTML元素Widget {#html-elements-widgets}

Widget會將一或多個基本元素與JavaScript外掛程式結合，以形成「較高層級」UI元素。 這些元素可以實作更複雜的行為，以及比單一元素所能提供的更複雜的外觀和風格。 標籤選擇器或邊欄Widget是很好的範例。

Widget可以觸發並監聽自訂事件，以便與頁面上的其他Widget合作。 某些Widget是使用CoralHTML元素的原生jQuery Widget。

用途：

* 實作展示複雜行為的較高層級UI元素
* 觸發和處理事件

實作：

* jQuery外掛程式+HTML標籤
* 可以使用使用者端/伺服器端範本

範例標籤為：

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

對jQuery外掛程式的呼叫（含選項）：

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

外掛程式會發出HTML標籤（此標籤使用基本元素，這些元素可能在內部使用其他外掛程式）：

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

這顯示為：

![chlimage_1-87](assets/chlimage_1-87.png)

### 公用程式庫 {#utility-library}

此程式庫是下列JavaScript協助程式外掛程式和/或函式的集合：

* 獨立於UI
* 然而，這對於建立完整功能的網頁應用程式至關重要

其中包括XSS處理和事件匯流排。

雖然HTML元素外掛程式和Widget可能會依賴公用程式庫提供的功能，但公用程式庫無法對元素或Widget本身有任何硬性相依性。

用途：

* 提供通用功能
* 事件匯流排實施
* 使用者端範本
* XSS

實作：

* jQuery外掛程式或符合AMD標準的JavaScript模組
