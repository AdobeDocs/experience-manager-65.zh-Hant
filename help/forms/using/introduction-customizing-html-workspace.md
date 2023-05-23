---
title: 自定義表單工AEM作區簡介
seo-title: Introduction to Customizing AEM form workspace
description: 快速介紹，包括概念和技術資訊，以自定義LiveCycleAEM Forms工作區以進行流程管理。
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# 自定義表單工AEM作區簡介{#introduction-to-customizing-aem-form-workspace}

表AEM單工作區提供了修改其介面的表示語義和功能的功能。 下面介紹了更改樣式、佈局、格式、品牌和核心功能的自定義類型。

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

自定義工作區的示例

## 自定義類型 {#types-of-customizations}

AEM Forms工作區支援多種自定義以更新用戶介面的佈局、外觀、功能等。 這些自定義涉及更新以下一個或多個內容：

* 用戶介面的外觀
* 使用語義自定義功能
* 在其他應用程式中重新使用HTML元件

### 用戶介面更改 {#user-interface-changes}

可以更改AEM Forms工作區的外觀、佈局和其它表示語義。 通過自定義CSS、HTML模板和JavaScript™檔案來更改工作區。 所有預設檔案都在預設安裝中提供。

最常用的步驟在 [AEM Forms工作區定製的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)。 有關此類自定義的特定示例（包括詳細步驟），請參閱本文末尾的相關文章。

#### 瞭解樣式表 {#understanding-the-style-sheet}

在自定義工作區之前，請熟悉/libs/ws/css/style.css上AEM Forms提供的預設樣式表。

要自定義工作區，建議您熟悉/libs/ws/css資料夾中的現有樣式表style.css。 下面介紹了幾個主要部分。

<table>
 <tbody>
  <tr>
   <th><p>CSS元素</p> </th>
   <th><p>已修改用戶介面元件</p> </th>
  </tr>
  <tr>
   <td><p>#頁首</p> </td>
   <td><p>AEM Forms工作區標題</p> </td>
  </tr>
  <tr>
   <td><p>.category清單</p> </td>
   <td><p>類別清單</p> </td>
  </tr>
  <tr>
   <td><p>.category清單.header</p> </td>
   <td><p>類別清單的標題</p> </td>
  </tr>
  <tr>
   <td><p>.類別，.filters</p> </td>
   <td><p>類別清單下的空格</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>類別</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover,.category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>所選類別和滑鼠懸停於類別樣式上</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool、categoryListBar .content</p> </td>
   <td><p>開始進程頁（已關閉的類別清單）</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool、filterListBar .content</p> </td>
   <td><p>要執行的頁面（關閉的篩選器清單）</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool、processNameListBar .content</p> </td>
   <td><p>跟蹤頁（已關閉的進程名清單）</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList、.tasklist</p> </td>
   <td><p>起始點清單或任務清單</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header、.tasklist .header</p> </td>
   <td><p>起始點清單或任務清單的標題</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected,.task.selected</p> </td>
   <td><p>所選起始點或任務</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>所選起始點或任務的說明</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>任務區域</p> </td>
  </tr>
  <tr>
   <td><p>#header.drop</p> </td>
   <td><p>標題中的用戶下拉清單</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>排序任務下拉清單</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms工作區的外觀借用了CSS的外觀。 通過自定義CSS，可以更改工作區的演示語義，如字型、顏色、品牌和佈局。

CSS自定義的頂級步驟包括：

* 建立CSS檔案。
* 將樣式項添加到此CSS。 有關詳細資訊，請參閱瞭解CSS樣式。
* 更新其引用 `html.jsp`。

有關執行這些自定義的確切步驟，請參見 [AEM Forms工作區定製的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)。 AEM Forms工作區附帶的CSS檔案位於/libs/ws/css/。 對於與CSS相關的自定義項，請使用 [發運包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)。 有關與CSS相關的自定義的特定示例，請參閱本文末尾的相關幫助主題。

#### 影像 {#image}

您可以自定義AEM Forms工作區以添加用戶的頭像或添加組織的徽標。 對於這些自定義項，請使用 [發運包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)。

對映像進行自定義的頂級步驟是：

* 安裝和配置WebDAV。
* 添加新映像。
* 添加與添加的影像對應的新樣式。
* 連結到中的新CSS檔案 `html.jsp` 的子菜單。

要開始自定義AEM Forms工作區中的映像，請按照 [AEM Forms工作區定製的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)。 有關與映像相關的自定義的特定示例，請參閱本文末尾的相關幫助主題。

#### HTML模板 {#html-template}

HTML模板有助於定義工作區用戶介面的外觀和佈局。 通過更新預設HTML模板，可以自定義佈局預設用戶介面。

對HTML模板進行自定義的頂級步驟是：

* 在用戶建立的資料夾中，建立所需預設檔案的副本。
* 在用戶定義的資料夾中添加新模板。
* 對複製的檔案進行相關更新，如新模板的路徑。

有關此類自定義的特定示例，請參閱本文末尾提供的「幫助」主題。 在 [發運包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) 或 [開發包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，具體取決於要自定義的模板。

### 語義變化 {#semantic-changes}

要修改AEM Forms工作區功能，請更改JavaScript原始碼。 對核心功能的修改標籤為「語義更改」。 可修改作為AEM Forms工作區原始碼一部分提供的模型、視圖和模板。

進行語義更改以修改AEM Forms工作區功能的頂級步驟包括：

* 在用戶建立的資料夾中，製作相應預設檔案的副本。
* 在用戶定義的資料夾中添加新模型和視圖。
* 進行相關更新，如更新預設JavaScript檔案中新添加的模型和視圖的路徑。
* 精簡包以優化效能。

有關作為原始碼一部分的元件的詳細概念資訊，請參見 [可重用元件的說明](/help/forms/using/description-reusable-components.md)。 對於這些自定義項，請使用開發包。

### 可重用元件 {#reusable-components}

由於AEM Forms工作區是基於元件的軟體，因此可以輕鬆定制和重用。 您可以輕鬆將工作區元件與Web應用程式整合。

有關更多概念性資訊，請參見 [可重用元件的說明](/help/forms/using/description-reusable-components.md) 有關使用元件的說明，請參見 [在Web應用程式中整合AEM Forms工作區元件](/help/forms/using/description-reusable-components.md)。

## 正在生成AEM Forms工作區代碼 {#building-html-workspace-code}

### SDK包 {#sdk-package}

包包含AEM Forms工作區的原始碼。 包可在以下位置獲得： `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`。

它主要用於定制，因為它提供了生成以下內容的功能：

* 發運、調試和開發配置檔案的CRX包（在下文中提到） [CRX包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p))。
* 自定義代碼的精簡版本（用於語義更改）。

#### WS內容 {#ws-content}

* 客戶端包：

   * src — 包含建立CRX節點所需的工件。
   * pom.xml — 為各種配置檔案生成部署包的指令碼WS-Deploy包

* 客戶端 — html:

   * 程式集 — 包含指令碼用於建立AEM Forms工作區SDK的zip.xml。
   * src/main/webapp -

      * css — 包含AEM Forms工作區的樣式表。
      * images — 包含在AEM Forms工作區中使用的影像。
      * js:

         * libs — 包含在AEM Forms工作區中使用的所有第三方庫。
         * 許可證 — 包含HTML和JS檔案的許可證以及將這些許可證前置詞為相應源檔案的代碼。
         * 迷你符 — 用於customizedJavaScript代碼的組合、縮小和更新。
         * resourcejs_optimizer — 用於JavaScript源的組合、縮小和更新。
         * resource_generator — 用於生成register.js和modelcontrollerpath.js。
         * 運行時：

            * 初始值設定項 — 包含初始值設定項.js，用於初始化AEM Forms工作區中使用的主幹視圖和模型。
            * models — 包含AEM Forms工作區中所有元件的主幹模型。
            * routes — 包含JavaScript檔案和HTML檔案，這些檔案在AEM Forms工作區中載入啟動進程、操作、跟蹤和首選項。
            * services — 包含在AEM Forms工作區中使用的service.js。 所有伺服器調用都通過service.js進行。
            * 模板 — 包含所有模板，即HTMLAEM Forms工作區中所有視圖的檔案。
            * util — 包含在AEM Forms工作區中使用的所有實用程式檔案(javascript)。
            * views — 包含AEM Forms工作區中所有元件的主幹視圖。
         * main.js
         * router.js
      * libs/ws:pdf.html和pluginPing.pdf用於在AEM Forms工作區中載入PDF forms，而WSNextAdapter.swf用於在AEM Forms工作區中載入SWF表單和指南。
      * 區域設定：

         * de-DE — 包含德語的translation.json。
         * en-US — 包含英語的translation.json。
         * fr-FR — 包含法語的translation.json。
         * ja-JP — 包含日語的translation.json。
         * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。
      * html.jsp
      * GET.jsp




### CRX包 {#crx-package}

CRX軟體包可以部署在CRX™儲存庫中。 可在以下位置獲得 `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`。

此軟體包可以使用下面介紹的三個配置檔案構建。

| **設定檔** | **說明** | **使用狀況** |
|---|---|---|
| 發運配置檔案 | 此配置檔案使用精簡建立可能最小大小的CRX包。 這個包最有效。 所有JavaScript™檔案都合併並精簡為單個JS檔案。 | 在JS檔案中不需要進一步的語義更改時，請使用此配置檔案。 |
| 調試配置檔案 | 此配置檔案建立中等效率的CRX包。 包的大小略高於使用發運配置檔案建立的包。 此包將大部分JavaScript檔案合併到單個JS檔案中。 | 使用此配置檔案進行調試。 |
| 開發配置檔案 | 此配置檔案會建立最大可能大小的CRX包。 所有JavaScript檔案都可單獨使用，因為它們在SDK包中。 | 在合併語義更改時使用此配置檔案。 |

#### 發運配置檔案 {#ship-profile}

#### 命令 {#command}

* mvn clean -P在發送給客戶端的源軟體包的client-pkg資料夾上發貨安裝。
* 發運配置檔案命令執行僅在64位JVM上工作。

#### WS內容 {#ws-content-1}

* css — 包含style.css、ie.css和jquery-ui.css。
* images — 包含所有影像。
* js:

   * libs:

      * require — 包含require.js。
      * jqueruyi — 包含jquery.ui.datepicker.ja.js。
   * 運行時：

      * 模板 — 包含所有模板，即HTMLAEM Forms工作區中所有元件的檔案。
   * main.js（合併、精簡和簡化）。
   * registry.js



* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 區域設定 — 包含.content.xml。
* 區域設定：

   * de-DE — 包含德語的translation.json。
   * en-US — 包含英語的translation.json。
   * fr-FR — 包含法語的translation.json。
   * ja-JP — 包含日語的translation.json。
   * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。

* 索引 — 包含.content.xml
* profile — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy_xml

#### 調試配置檔案 {#debug-profile}

#### 命令 {#command-1}

* mvn clean -P調試安裝在client-pkg上
* 調試配置檔案命令執行僅在64位JVM上工作。

#### WS內容 {#ws-content-2}

* css — 包含style.css、ie.css和jqueri-ui.css。
* images — 包含所有影像。
* js:

   * libs:

      * require — 包含require.js。
      * jqueruyi — 包含jquery.ui.datepicker.ja.js。
   * 運行時：

      * 模板 — 包含所有模板，即HTMLAEM Forms工作區中所有元件的檔案。
   * main.js（合併）。
   * registry.js



* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 區域設定 — 包含.content.xml。
* 區域設定：

   * de-DE — 包含德語的translation.json。
   * en-US — 包含英語的translation.json。
   * fr-FR — 包含法語的translation.json。
   * ja-JP — 包含日語的translation.json。
   * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。

* 索引 — 包含.content.xml
* profile — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy_xml

#### 開發配置檔案 {#dev-profile}

#### 命令 {#command-2}

mvn clean -P Dev安裝在client-pkg上

#### WS內容 {#ws-content-3}

* css — 包含style.css、ie.css和jqueri-ui.css。
* images — 包含所有影像。
* js:

   * libs — 包含在AEM Forms工作區中使用的所有庫。
   * require — 包含require.js
   * jqueruyi — 包含jquery.ui.datepicker.ja.js
   * 運行時：

      * 初始值設定項 — 包含初始值設定項.js和modelcontrollerpath.js。
      * models — 包含AEM Forms工作區中所有元件的模型。
      * routes — 包含JavaScript檔案和HTML檔案，這些檔案在AEM Forms工作區中載入啟動進程、操作、跟蹤和首選項。
      * services — 包含在AEM Forms工作區中使用的service.js。
      * 模板 — 包含所有模板，即HTMLAEM Forms工作區中所有元件的檔案。
      * util — 包含在AEM Forms工作區中使用的所有實用程式檔案(JavaScript)。
      * views — 包含AEM Forms工作區中所有元件的視圖。
   * main.js
   * registry.js
   * router.js


* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 區域設定 — 包含.content.xml。
* 區域設定：

   * de-DE — 包含德語的translation.json。
   * en-US — 包含英語的translation.json。
   * fr-FR — 包含法語的translation.json。
   * ja-JP — 包含日語的translation.json。
   * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。

* 索引 — 包含.content.xml
* profile — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy_xml
