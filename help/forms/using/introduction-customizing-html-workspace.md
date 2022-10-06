---
title: 自訂AEM表單工作區簡介
seo-title: Introduction to Customizing AEM form workspace
description: 快速簡介，內含概念與技術資訊，可自訂LiveCycleAEM Forms工作區以進行流程管理。
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

# 自訂AEM表單工作區簡介{#introduction-to-customizing-aem-form-workspace}

AEM form workspace提供修改其介面的呈現語義和功能的功能。 以下說明可變更樣式、版面、格式、品牌和核心功能的自訂類型。

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

自訂工作區的範例

## 自訂類型 {#types-of-customizations}

AEM Forms工作區支援多種自訂功能，以更新使用者介面的版面、外觀、功能等。 這些自訂項目包括更新下列其中一或多個項目：

* 用戶介面的外觀
* 使用語義自定義的功能
* 在其他應用程式中重複使用HTML元件

### 使用者介面變更 {#user-interface-changes}

您可以變更AEM Forms工作區的外觀、版面配置和其他呈現語意。 透過自訂CSS、HTML範本和JavaScript™檔案來變更工作區。 所有預設檔案都在預設安裝中提供。

最常適用的步驟涵蓋於 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md). 如需這類自訂的特定範例，包括詳細步驟，請參閱本文結尾的相關文章。

#### 了解樣式表 {#understanding-the-style-sheet}

在自訂工作區之前，請詳閱AEM Forms提供的預設樣式表，網址為/libs/ws/css/style.css。

若要自訂工作區，建議您熟悉位於/libs/ws/css資料夾中的現有樣式表style.css。 以下說明幾個顯著元件。

<table>
 <tbody>
  <tr>
   <th><p>CSS元素</p> </th>
   <th><p>修改用戶介面元件</p> </th>
  </tr>
  <tr>
   <td><p>#頁首</p> </td>
   <td><p>AEM Forms工作區標題</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>類別清單</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>類別清單的標題</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>類別清單下方的空格</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>類別</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>選定的類別和滑鼠移到類別樣式上</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>「啟動流程」頁（已關閉的類別清單）</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>執行頁面（關閉的篩選器清單）</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>追蹤頁面（關閉的程式名稱清單）</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>起始點清單或任務清單</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>起始點清單或任務清單的標題</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>所選起始點或任務</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected.description, .task.selected.description</p> </td>
   <td><p>所選起始點或任務的說明</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>任務區</p> </td>
  </tr>
  <tr>
   <td><p>#header.dropdown</p> </td>
   <td><p>標題中的使用者下拉式清單</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>排序任務下拉式清單</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms工作區的外觀借用了CSS的外觀。 通過自定義CSS，您可以更改工作區的演示語義，如字型、顏色、品牌和佈局。

CSS自訂的頂層步驟為：

* 建立CSS檔案。
* 新增樣式項目至此CSS。 如需詳細資訊，請參閱了解CSS樣式。
* 在 `html.jsp`.

如需這些自訂的確切步驟，請參閱 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md). AEM Forms工作區隨附的CSS檔案位於/libs/ws/css/。 如需CSS相關的自訂，請使用 [發運包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). 如需CSS相關自訂的特定範例，請參閱本文結尾的相關說明主題。

#### 影像 {#image}

您可以自訂AEM Forms工作區，以新增使用者的變身，或新增組織的標誌。 對於這些自訂項目，請使用 [發運包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

自訂影像的頂層步驟為：

* 安裝和配置WebDAV。
* 新增影像。
* 新增與新增的影像對應的新樣式。
* 連結至 `html.jsp` 檔案。

若要開始自訂AEM Forms工作區中的影像，請遵循 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md). 如需影像相關自訂的特定範例，請參閱本文結尾的相關說明主題。

#### HTML範本 {#html-template}

HTML範本有助於定義工作區使用者介面的外觀和版面。 更新預設HTML範本後，您可以自訂版面預設使用者介面。

自訂HTML範本的頂層步驟為：

* 在用戶建立的資料夾中，建立所需預設檔案的副本。
* 在使用者定義的資料夾中新增範本。
* 對複製的檔案（如新範本的路徑）進行相關更新。

如需這類自訂的特定範例，請參閱本文結尾提供的說明主題。 在 [發運包](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) 或 [開發套件](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，視要自訂的範本而定。

### 語義變化 {#semantic-changes}

若要修改AEM Forms工作區功能，請變更JavaScript原始碼。 核心功能中的修改會標示為「語義變更」。 您可以修改作為AEM Forms工作區原始碼一部分提供的模型、檢視和範本。

進行語義變更以修改AEM Forms工作區功能的頂層步驟為：

* 在用戶建立的資料夾中，建立相應預設檔案的副本。
* 在用戶定義的資料夾中添加新模型和視圖。
* 進行相關更新，例如更新預設JavaScript檔案中新增模型和檢視的路徑。
* 縮小套件以最佳化效能。

如需原始碼中元件的詳細概念資訊，請參閱 [可重複使用元件的說明](/help/forms/using/description-reusable-components.md). 對於這些自訂項目，請使用開發套件。

### 可重複使用的元件 {#reusable-components}

由於AEM Forms工作區是以元件為基礎的軟體，因此可輕鬆自訂及重複使用。 您可以輕鬆將工作區元件與網頁應用程式整合。

如需更多概念資訊，請參閱 [可重複使用元件的說明](/help/forms/using/description-reusable-components.md) 如需有關使用元件的說明，請參閱 [將AEM Forms工作區元件整合至網頁應用程式](/help/forms/using/description-reusable-components.md).

## 建立AEM Forms工作區程式碼 {#building-html-workspace-code}

### SDK套件 {#sdk-package}

套件包含AEM Forms工作區的原始碼。 此套件可於 `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

主要用於自訂，因為它提供產生下列內容的功能：

* 發運、除錯和開發設定檔的CRX套件(如下所述： [CRX套件](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p))。
* 自訂程式碼的縮製版本（用於語義變更）。

#### WS內容 {#ws-content}

* client-pkg:

   * src — 包含建立CRX節點所需的成品。
   * pom.xml — 為各種配置檔案生成部署包的指令碼WS-Deploy包

* client-html:

   * assembly — 包含指令碼用於建立AEM Forms工作區SDK的zip.xml。
   * src/main/webapp -

      * css — 包含AEM Forms工作區的樣式表。
      * 影像 — 包含AEM Forms工作區中使用的影像。
      * js:

         * libs — 包含AEM Forms工作區中使用的所有協力廠商程式庫。
         * 許可證 — 包含HTML和JS檔案的許可證，以及為這些許可證加上前置詞的代碼。
         * 縮制器 — 用於自訂JavaScript程式碼的組合、縮制和縮制。
         * resourcejs_optimizer — 用於JavaScript來源的組合、縮制和升級。
         * resource_generator — 用於生成register.js和modelcontrollerpath.js。
         * 執行階段：

            * 初始值設定項 — 包含初始化主幹視圖和AEM Forms工作區中使用的模型時使用的初始值設定項.js。
            * 模型 — 包含AEM Forms工作區中所有元件的骨幹模型。
            * routes — 包含JavaScript檔案和HTML檔案，這些檔案和檔案載入AEM Forms工作區中的啟動進程、操作、跟蹤和首選項。
            * 服務 — 包含AEM Forms工作區中使用的service.js。 所有伺服器呼叫都是透過service.js進行。
            * 範本 — 包含所有範本，即AEM Forms工作區中所有檢視的HTML檔案。
            * util — 包含AEM Forms工作區中使用的所有公用程式檔案(javascript)。
            * 檢視 — 包含AEM Forms工作區中所有元件的骨幹檢視。
         * main.js
         * router.js
      * libs/ws:pdf.html和pluginPing.pdf用於載入AEM Forms工作區中的PDF forms，而WSNextAdapter.swf用於載入AEM Forms工作區中的SWF表單和參考線。
      * 區域設定：

         * de-DE — 包含德文版的translation.json 。
         * en-US — 包含英文的translation.json 。
         * fr-FR — 包含法文的translation.json 。
         * ja-JP — 包含日文版的translation.json。
         * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。
      * html.jsp
      * GET.jsp




### CRX套件 {#crx-package}

CRX套件可部署在CRX™存放庫上。 可於 `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

可使用下列三個設定檔來建立此套件。

| **設定檔** | **說明** | **使用狀況** |
|---|---|---|
| 發運配置檔案 | 此設定檔會使用縮制功能，建立盡可能小的CRX套件。 這個包最有效。 所有JavaScript™檔案皆會合併並縮制為單一JS檔案。 | 若JS檔案中不需要進一步的語意變更，請使用此設定檔。 |
| 除錯設定檔 | 此配置檔案將建立中等效率的CRX包。 包的大小比使用發運配置檔案建立的包稍大。 此套件將大部分的JavaScript檔案合併為單一JS檔案。 | 使用此配置檔案進行調試。 |
| 開發設定檔 | 此配置檔案會建立最大可能大小的CRX包。 所有JavaScript檔案均可個別使用，如同SDK套件中一樣。 | 納入語義變更時，請使用此設定檔。 |

#### 發運配置檔案 {#ship-profile}

#### 命令 {#command}

* mvn clean -P發運安裝在發運到客戶端的源包的client-pkg資料夾上。
* 發運配置檔案命令僅在64位JVM上工作。

#### WS內容 {#ws-content-1}

* css — 包含style.css、ie.css和jquery-ui.css。
* 影像 — 包含所有影像。
* js:

   * libs:

      * require — 包含require.js。
      * jqueryui — 包含jquery.ui.datepicker.ja.js。
   * 執行階段：

      * 範本 — 包含所有範本，即AEM Forms工作區中所有元件的HTML檔案。
   * main.js（結合、縮制和縮制）。
   * registry.js



* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 地區 — 包含.content.xml。
* 區域設定：

   * de-DE — 包含德文版的translation.json 。
   * en-US — 包含英文的translation.json 。
   * fr-FR — 包含法文的translation.json 。
   * ja-JP — 包含日文版的translation.json。
   * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。

* 索引 — 包含.content.xml
* profile — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 除錯設定檔 {#debug-profile}

#### 命令 {#command-1}

* mvn clean -P在client-pkg上安裝調試
* 調試配置檔案命令僅在64位JVM上工作。

#### WS內容 {#ws-content-2}

* css — 包含style.css、ie.css和jquery-ui.css。
* 影像 — 包含所有影像。
* js:

   * libs:

      * require — 包含require.js。
      * jqueryui — 包含jquery.ui.datepicker.ja.js。
   * 執行階段：

      * 範本 — 包含所有範本，即AEM Forms工作區中所有元件的HTML檔案。
   * main.js（結合）。
   * registry.js



* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 地區 — 包含.content.xml。
* 區域設定：

   * de-DE — 包含德文版的translation.json 。
   * en-US — 包含英文的translation.json 。
   * fr-FR — 包含法文的translation.json 。
   * ja-JP — 包含日文版的translation.json。
   * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。

* 索引 — 包含.content.xml
* profile — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 開發設定檔 {#dev-profile}

#### 命令 {#command-2}

mvn clean -P Dev安裝在client-pkg上

#### WS內容 {#ws-content-3}

* css — 包含style.css、ie.css和jquery-ui.css。
* 影像 — 包含所有影像。
* js:

   * libs — 包含AEM Forms工作區中使用的所有程式庫。
   * require — 包含require.js
   * jqueryui — 包含jquery.ui.datepicker.ja.js
   * 執行階段：

      * 初始值設定項 — 包含初始值設定項.js和modelcontrollerpath.js。
      * 模型 — 包含AEM Forms工作區中所有元件的模型。
      * routes — 包含JavaScript檔案和HTML檔案，這些檔案和檔案載入AEM Forms工作區中的啟動進程、操作、跟蹤和首選項。
      * 服務 — 包含AEM Forms工作區中使用的service.js。
      * 範本 — 包含所有範本，即AEM Forms工作區中所有元件的HTML檔案。
      * util — 包含AEM Forms工作區中使用的所有公用程式檔案(JavaScript)。
      * 檢視 — 包含AEM Forms工作區中所有元件的檢視。
   * main.js
   * registry.js
   * router.js


* libs:

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 地區 — 包含.content.xml。
* 區域設定：

   * de-DE — 包含德文版的translation.json 。
   * en-US — 包含英文的translation.json 。
   * fr-FR — 包含法文的translation.json 。
   * ja-JP — 包含日文版的translation.json。
   * html.jsp — 包含用於查找當前瀏覽器區域設定的代碼。

* 索引 — 包含.content.xml
* profile — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
