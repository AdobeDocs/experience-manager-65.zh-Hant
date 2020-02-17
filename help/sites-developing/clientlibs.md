---
title: 使用用戶端程式庫
seo-title: 使用用戶端程式庫
description: AEM提供「用戶端程式庫檔案夾」，可讓您將用戶端程式碼儲存在儲存庫中、將它組織成類別，並定義將每個程式碼類別提供給用戶端的時間和方式
seo-description: AEM提供「用戶端程式庫檔案夾」，可讓您將用戶端程式碼儲存在儲存庫中、將它組織成類別，並定義將每個程式碼類別提供給用戶端的時間和方式
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 使用用戶端程式庫{#using-client-side-libraries}

現代網站嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 組織並最佳化此程式碼的服務可能是個複雜的問題。

為協助處理此問題，AEM提供「用戶端程式庫資料夾 ****」，可讓您將用戶端程式碼儲存在儲存庫中、將它組織為類別，並定義將每類程式碼提供給用戶端的時間和方式。 然後用戶端程式庫系統會負責在您的最終網頁中產生正確的連結，以載入正確的程式碼。

## 用戶端程式庫在AEM中的運作方式 {#how-client-side-libraries-work-in-aem}

在頁面的HTML中包含用戶端資料庫（即JS或CSS檔案）的標準方式，就是在該頁面的JSP中包含 `<script>` or `<link>` 標籤，其中包含該檔案的路徑。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

雖然此方法適用於AEM，但當頁面及其組成元件變得複雜時，可能會導致問題。 在這類情況下，相同JS程式庫的多份副本可能會納入最終HTML輸出。 若要避免此情況，並允許用戶端程式庫的邏輯組織，AEM會使 **用用戶端程式庫資料夾**。

客戶端庫資料夾是類型的儲存庫節點 `cq:ClientLibraryFolder`。 CND符號中的定 [義是](https://jackrabbit.apache.org/node-type-notation.html)

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

預設情況下， `cq:ClientLibraryFolder` 節點可以放置在儲存庫的子樹中(這些預設值和其他設定可以通過 `/apps`System Console的 `/libs` Adobe Granite HTML Library Manager `/etc` ****[](https://localhost:4502/system/console/configMgr)panel控制)。

每 `cq:ClientLibraryFolder` 個檔案都會填入一組JS和／或CSS檔案，以及一些支援檔案（請參閱下面）。 屬性的配 `cq:ClientLibraryFolder` 置如下：

* `categories`:識別今秋JS和／或CSS檔案集所屬的 `cq:ClientLibraryFolder` 類別。 屬 `categories` 性是多值的，可讓資料庫資料夾成為多個類別的一部分（如需這項功能的實用方法，請參閱以下）。

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。 例如，給定兩個 `cq:ClientLibraryFolder` 節點 `F` ，如果檔案中的某個檔案需要另一個檔案才能 `G`正常工作，則至少該檔案中的一個應屬於 `F``G``categories``G``dependencies``F`Jame。

* `embed`:用於從其他程式庫內嵌程式碼。 如果節點F嵌入節點G和H，則產生的HTML將是節點G和H的內容集中。
* `allowProxy`:如果客戶端庫位於下 `/apps`面，則此屬性允許通過代理Servlet訪問它。 請參 [閱下面的查找客戶端庫資料夾和使用代理客戶端庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 。

## 參考用戶端程式庫 {#referencing-client-side-libraries}

由於HTL是開發AEM網站的偏好技術，因此應使用HTL在AEM中包含用戶端程式庫。 但是，也可以使用JSP來執行此操作。

### 使用HTL {#using-htl}

在HTL中，用戶端程式庫會透過AEM提供的輔助範本載入，您可透過此範本存取 [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)。 此檔案中提供3個範本，可透過下列方式呼叫 [`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** —— 僅載入參考用戶端程式庫的CSS檔案。
* **js** —— 僅載入參考用戶端程式庫的JavaScript檔案。
* **all** —— 載入參考用戶端程式庫（包括CSS和JavaScript）的所有檔案。

每個幫助模板都需要一 `categories` 個用於引用所需客戶端庫的選項。 該選項可以是字串值陣列或包含逗號分隔值清單的字串。

如需詳細資訊和使用範例，請參閱HTML范 [本語言快速入門檔案](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

將標籤 `ui:includeClientLib` 新增至JSP程式碼，以新增連結至產生之HTML頁面中的用戶端程式庫。 要引用庫，請使用節點屬 `categories` 性的 `ui:includeClientLib` 值。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，節 `/etc/clientlibs/foundation/jquery` 點的類型為 `cq:ClientLibraryFolder` 類別屬性值 `cq.jquery`。 JSP檔案中的以下代碼引用庫：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

產生的HTML頁面包含下列程式碼：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

如需完整資訊，包括篩選JS、CSS或主題程式庫的屬性，請參 [閱ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`，過去常用來包含用戶端程式庫的AEM 5.6版已過時。應 [ 如 `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 上文所述使用。

## 建立客戶端庫資料夾 {#creating-client-library-folders}

建立節點 `cq:ClientLibraryFolder` 以定義JavaScript和階層式樣式表程式庫，並讓它們可用於HTML頁面。 使用節 `categories` 點的屬性來識別其所屬的庫類別。

節點包含一或多個在執行時期會合併為單一JS和／或CSS檔案的來源檔案。 生成的檔案的名稱是具有或檔案名副檔名的節 `.js` 點 `.css` 名稱。 例如，名為的庫節點 `cq.jquery` 將生成名為或的 `cq.jquery.js` 檔案 `cq.jquery.css`。

客戶端庫資料夾包含以下項目：

* 要合併的JS和／或CSS來源檔案。
* 支援CSS樣式的資源，例如影像檔案。

   **** 注意：您可以使用子檔案夾來組織來源檔案。
* 一個 `js.txt` 檔案和／或一個 `css.txt` 檔案，用於標識要合併到生成的JS和／或CSS檔案中的源檔案。

![clientlibarch](assets/clientlibarch.png)

如需Widget用戶端程式庫特定需求的詳細資訊，請參 [閱使用和擴充Widget](/help/sites-developing/widgets.md)。

Web客戶端必須具有訪問節點的 `cq:ClientLibraryFolder` 權限。 您也可以從儲存庫的安全區域中顯示庫（請參閱下面的「從其他庫嵌入代碼」）。

### 覆蓋/lib中的庫 {#overriding-libraries-in-lib}

位於以下的客戶端庫 `/apps` 資料夾優先於位於中的同名資料夾 `/libs`。 例如，優先 `/apps/cq/ui/widgets` 於 `/libs/cq/ui/widgets`。 當這些程式庫屬於相同類別時，會使用下 `/apps` 列程式庫。

### 查找客戶機庫資料夾和使用代理客戶機庫Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在舊版中，客戶端庫資料夾位於儲存庫 `/etc/clientlibs` 的下方。 這仍受支援，不過建議現在用戶端程式庫位於下方 `/apps`。 這是在其他指令碼附近找到用戶端程式庫，這些指令碼通常位於 `/apps` 和 `/libs`下。

>[!NOTE]
>
>客戶端庫資料夾下的靜態資源必須位於名為resources的文 *件夾*。 如果您在資料夾資源下方沒有靜態資源（例如影像） **，則無法在發佈例項上參考它。 以下是範例：https://localhost:4503/etc.clientlibs/geometrixx/components/clinetlibs/resources/example.gif

>[!NOTE]
>
>為了更好地將程式碼與內容和設定隔離，建議您在下方找出用戶端程式庫， `/apps` 並運用屬性 `/etc.clientlibs` 來公開它 `allowProxy` 們。

為了能夠訪問所在的客 `/apps` 戶端庫，使用代理伺服器。 ACL仍在客戶端庫資料夾上強制執行，但是，如果將屬性設定為，則Servlet允許 `/etc.clientlibs/` 通 `allowProxy` 過讀取內容 `true`。

如果靜態資源位於客戶端庫資料夾下的資源下，則只能通過代理訪問該資源。

例如：

* 您在 `/apps/myproject/clientlibs/foo`
* 您的靜態影像位於 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然後，將 `allowProxy` 屬性設 `foo` 為true。

* 然後，您可以要求 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然後，您可以透過 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>當使用proxied用戶端程式庫時，AEM Dispatcher組態可能需要更新，以確保允許具有擴充用戶端libs的URI。

>[!CAUTION]
>
>Adobe建議在下方找到用戶端程 `/apps` 式庫，並使用proxy servlet加以使用。 但請記住，最佳實務仍要求公共網站不要包含任何直接透過或路徑提供的 `/apps` 內 `/libs` 容。

### 建立客戶端庫資料夾 {#create-a-client-library-folder}

1. 在網頁瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 選擇要在其中找到客戶端庫資料夾的資料夾，然後按一下「創 **建」>「建立節點」**。
1. 輸入庫檔案的名稱，然後在「類型」(Type)清單中選擇 `cq:ClientLibraryFolder`。 按一 **下「確定** 」，然後按一 **下「全部儲存」**。
1. 要指定庫所屬的類別或類別，請選擇節點，添加 `cq:ClientLibraryFolder` 以下屬性，然後按一下「全 **部保存**:

   * 名稱：類別
   * 類型：字串
   * 值：類別名稱
   * 多重：選擇

1. 以任何方式將來源檔案新增至程式庫資料夾。 例如，使用WebDav用戶端來複製檔案，或建立檔案並手動編寫內容。

   **** 注意：您可視需要在子檔案夾中組織來源檔案。

1. 選擇客戶端庫資料夾，然後按一下「 **建立」>「建立檔案」**。
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下確定：

   * **`js.txt`**:使用此檔案名稱來產生JavaScript檔案。
   * **`css.txt`**:使用此檔案名生成級聯樣式表。

1. 開啟檔案並輸入下列文字，以識別來源檔案路徑的根目錄：

   `#base=*[root]*`

   將* `[root]`*替換為包含源檔案（相對於TXT檔案）的資料夾的路徑。 例如，當源檔案與TXT檔案位於同一資料夾時，請使用以下文本：

   `#base=.`

   下列程式碼會將根目錄設為節點下方名為mobile的資 `cq:ClientLibraryFolder` 料夾：

   `#base=mobile`

1. 在下面的行 `#base=[root]`中，鍵入源檔案相對於根檔案的路徑。 將每個檔案名稱放在單獨的行上。
1. 按一下「 **全部儲存**」。

### 連結至相依項 {#linking-to-dependencies}

當用戶端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 在JSP中，引用 `ui:includeClientLib` 用戶端程式庫資料夾的標籤會使HTML程式碼包含您產生之程式庫檔案的連結以及相依性。

相依性必須是另一個 `cq:ClientLibraryFolder`。 要標識相依性，請使用以下屬性將屬 `cq:ClientLibraryFolder` 性添加到節點：

* **** 名稱：依賴性
* **** 類型：字串[]
* **** 值：當前庫資料夾所依賴的cq:ClientLibraryFolder節點的categories屬性的值。

例如，/ `etc/clientlibs/myclientlibs/publicmain` 對庫有相依 `cq.jquery` 性。 引用主客戶端庫的JSP將生成包含以下代碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他程式庫內嵌程式碼 {#embedding-code-from-other-libraries}

您可以將用戶端程式庫的程式碼內嵌至另一個用戶端程式庫。 在執行時期，內嵌程式庫產生的JS和CSS檔案包含內嵌程式庫的程式碼。

嵌入代碼對於提供對儲存在儲存庫的安全區域中的庫的訪問非常有用。

#### 應用程式專用的用戶端程式庫資料夾 {#app-specific-client-library-folders}

最好將所有與應用程式相關的檔案保留在下方的應用程式資料夾中 `/app`。 也是拒絕網站訪客存取資料夾的最佳 `/app` 做法。 為滿足這兩種最佳做法，請在內嵌下方用戶端程式庫的 `/etc` 資料夾下方建立用戶端程式庫資料夾 `/app`。

使用categories屬性來識別要內嵌的用戶端程式庫資料夾。 要嵌入庫，請使用以下屬性屬性將屬 `cq:ClientLibraryFolder` 性添加到嵌入節點：

* **** 名稱：嵌入
* **** 類型：字串[]
* **** 值：要嵌入的節點的類別屬 `cq:ClientLibraryFolder` 性的值。

#### 使用內嵌功能將要求降至最低 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現，您的發佈例項為典型頁面產生的最終HTML包含相當多的元素，尤其是當您的網站使用用戶端內容資訊進行分析或定位時。 `<script>` 例如，在未最佳化的專案中，您可能會在頁面的HTML中 `<script>` 找到下列系列元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/underscore.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在這種情況下，將所有必要的用戶端程式庫程式碼結合到單一檔案中，以減少頁面載入時的來回請求數，是很有用的。 若要這麼做，您可 `embed` 以使用節點的embed屬性，將必要的程式庫放入應用程式專用的用戶端程 `cq:ClientLibraryFolder` 式庫。

AEM包含下列用戶端程式庫類別。 您只應嵌入特定網站運作所需的內容。 不過， **您應維護下列訂單**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS檔案中的路徑 {#paths-in-css-files}

當您內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫會嵌入 `/etc/client/libraries/myclientlibs/publicmain` 用戶端程 `/apps/myapp/clientlib` 式庫：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

檔 `main.css` 案包含下列樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

節點生成的CSS `publicmain` 檔案使用原始影像的URL包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 使用特定行動群組的程式庫 {#using-a-library-for-specific-mobile-groups}

使用用戶 `channels` 端程式庫資料夾的屬性來識別使用程式庫的行動群組。 當相 `channels` 同類別的程式庫針對不同的裝置功能而設計時，此屬性很實用。

要將客戶端庫資料夾與設備組關聯，請使用以下屬性將屬 `cq:ClientLibraryFolder` 性添加到節點：

* **** 名稱：頻道
* **** 類型：字串[]
* **** 值：行動群組的名稱。 若要從群組排除程式庫資料夾，請在名稱前加上驚嘆號(&quot;!&quot;)。

例如，下表列出了類別中每個客戶 `channels` 端庫資料夾的屬性 `cq.widgets` 值：

| 用戶端程式庫資料夾 | 渠道屬性的值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[無值]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## 使用預處理器 {#using-preprocessors}

AEM允許可插拔的預處理器，並隨附支援CSS和JavaScript的 [UYI Complasor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) ，以及 [Google Closure Compiler(GCC)](https://developers.google.com/closure/compiler/) for JavaScript，而UY已設定為AEM的預處理器。

可插拔的預處理器允許靈活使用，包括：

* 定義可處理指令碼源的指令碼處理器
* 處理器可配置選項
* 處理器可用於微型化，但也可用於非微型化的情況
* clientlib可以定義要使用哪個處理器

>[!NOTE]
>
>依預設，AEM會使用UYI壓縮器。 如需已 [知問題的清單](https://github.com/yui/yuicompressor/issues) ，請參閱UIY壓縮程式GitHub檔案。 切換至特定客戶端的GCC壓縮機可解決使用UY時觀察到的一些問題。

>[!CAUTION]
>
>請勿將精簡的程式庫放在用戶端程式庫中。 請改為提供原始程式庫，如果需要精簡，請使用預處理器的選項。

### 使用狀況 {#usage}

您可以選擇根據客戶端庫或整個系統配置預處理器配置。

* 在clientlibrary節點上新 `cssProcessor` 增 `jsProcessor` 多值屬性

* 或者，透過 **HTML Library Manager** OSGi組態定義系統預設組態

clientlib節點上的預處理器配置優先於OSGI配置。

### 格式與範例 {#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### UYI壓縮器，用於CSS精簡化和GCC for JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 先輸入預處理的指令碼，再輸入GCC以進行微處理和模糊處理 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他GCC選項 {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有關GCC選項的詳細資訊，請參見 [GCC文檔](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 設定系統預設精簡器 {#set-system-default-minifier}

UYI在AEM中設為預設微調字元。 要將此更改為GCC，請執行以下步驟。

1. 請至Apache Felix Config Manager，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 尋找並編輯 **Adobe Granite HTML Library Manager**。
1. 啟用 **Minify** 選項（如果尚未啟用）。
1. 將「 **JS處理器預設設定」值設為**`min:gcc`。

   若以分號(例如 `min:gcc;obfuscate=true`。

1. 按一 **下「儲存** 」以儲存變更。

## 除錯工具 {#debugging-tools}

AEM提供數種工具來除錯和測試用戶端程式庫資料夾。

### 請參閱內嵌檔案 {#see-embedded-files}

若要追蹤內嵌程式碼的來源，或確保內嵌用戶端程式庫產生預期的結果，您可以在執行時期看到內嵌的檔案名稱。 若要查看檔案名稱，請將 `debugClientLibs=true` 參數附加至網頁的URL。 產生的程式庫包含 `@import` 陳述式，而非內嵌程式碼。

在上一個「從其他程式庫 [內嵌代碼」區段的範例中](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) ，用戶端程式庫 `/etc/client/libraries/myclientlibs/publicmain` 資料夾會內嵌用戶 `/apps/myapp/clientlib` 端程式庫資料夾。 將參數附加到網頁會在網頁的原始碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟檔 `publicmain.css` 案會顯示下列程式碼：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL:

   `?debugClientLibs=true`
1. 頁面載入時，請檢視頁面來源。
1. 按一下作為連結元素href提供的連結，以開啟檔案並檢視原始碼。

### Discover用戶端程式庫 {#discover-client-libraries}

組 `/libs/cq/ui/components/dumplibs/dumplibs` 件生成有關係統上所有客戶端庫資料夾的資訊頁。 節 `/libs/cq/ui/content/dumplibs` 點將元件作為資源類型。 若要開啟頁面，請使用下列URL（視需要使用不同的主機和連接埠）:

[https://localhost:4502/libs/cq/ui/content/dumplibs.test.html](https://localhost:4502/libs/cq/ui/content/dumplibs.test.html)

這些資訊包括程式庫路徑和類型（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和頻道中的程式庫。

### 請參閱產生的輸出 {#see-generated-output}

元 `dumplibs` 件包含測試選擇器，顯示為標籤產生的原始 `ui:includeClientLib` 碼。 頁面包含js、css和主題屬性不同組合的程式碼。

1. 使用下列其中一種方法來開啟「測試輸出」頁面：

   * 在頁面 `dumplibs.html` 上，按一下「按一下這裡 **以輸出測試」文字中的連結** 。

   * 在網頁瀏覽器中開啟下列URL（視需要使用不同的主機和連接埠）:

      [https://localhost:4502/libs/cq/ui/content/dumplibs.html](https://localhost:4502/libs/cq/ui/content/dumplibs.html)
   預設頁面顯示沒有類別屬性值之標籤的輸出。

1. 若要查看類別的輸出，請鍵入用戶端程式庫屬性的值，然後按一 `categories` 下「提 **交查詢」**。

## 為開發和生產配置庫處理 {#configuring-library-handling-for-development-and-production}

HTML Library manager服務會在執行 `cq:ClientLibraryFolder` 時期處理標籤並產生程式庫。 環境類型、開發或生產類型決定了您應如何配置服務：

* 提高安全性：停用除錯
* 提高效能：移除空白字元並壓縮程式庫。
* 改善可讀性：包含空格且不壓縮。

如需設定服務的詳細資訊，請參 [閱「AEM HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)」。
