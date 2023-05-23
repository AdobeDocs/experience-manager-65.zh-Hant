---
title: 使用用戶端程式庫
seo-title: Using Client-Side Libraries
description: 提AEM供客戶端庫資料夾，允許您將客戶端代碼儲存在儲存庫中，將其組織成類別，並定義將每類代碼提供給客戶端的時間和方式
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 7ceee6819618d785f04029b9ac1c6f763995b3ac
workflow-type: tm+mt
source-wordcount: '2861'
ht-degree: 1%

---

# 使用用戶端程式庫{#using-client-side-libraries}

現代網站在複雜的JavaScript和CSS代碼驅動下，嚴重依賴客戶端處理。 組織和優化此代碼的服務可能是一個複雜的問題。

為幫助處理此問題，提供 **客戶端庫資料夾**，允許您將客戶端代碼儲存在儲存庫中，將其組織為類別，並定義將每類代碼提供給客戶端的時間和方式。 然後，客戶端庫系統會注意在最終網頁中生成正確的連結以載入正確的代碼。

## 客戶端庫在Web服務中的工AEM作 {#how-client-side-libraries-work-in-aem}

在頁面HTML中包含客戶端庫（即JS或CSS檔案）的標準方法只是包括 `<script>` 或 `<link>` 該頁的JSP中的標籤，包含有關檔案的路徑。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

雖然這種方法在AEM應用中，但當頁面及其組成部分變得複雜時，它會導致問題。 在這種情況下，同一聯署材料庫的多個副本有可能被納入最終HTML輸出。 避免這種情況並允許對客戶端庫使用的邏輯AEM組織 **客戶端庫資料夾**。

客戶端庫資料夾是類型的儲存庫節點 `cq:ClientLibraryFolder`。 這是 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html) 是

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

預設情況下， `cq:ClientLibraryFolder` 節點可以放在任意位置 `/apps`。 `/libs` 和 `/etc` 儲存庫的子樹(這些預設值和其他設定可以通過 **Adobe花崗岩HTML庫經理** 的 [系統控制台](https://localhost:4502/system/console/configMgr))。

每個 `cq:ClientLibraryFolder` 將填充一組JS和/或CSS檔案，以及幾個支援檔案（請參閱下面）。 屬性 `cq:ClientLibraryFolder` 配置如下：

* `categories`:標識此內的JS和/或CSS檔案集的類別 `cq:ClientLibraryFolder` 摔倒。 的 `categories` 屬性是多值的，它允許庫資料夾成為多個類別的一部分（有關此類別可能有用的資訊，請參閱下面）。

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。 例如，給出兩個 `cq:ClientLibraryFolder` 節點 `F` 和 `G`，如果檔案在 `F` 需要另一個檔案 `G` 為了能正常工作，那麼 `categories` 共 `G` 應該是 `dependencies` 共 `F`。

* `embed`:用於從其他庫中嵌入代碼。 如果節點F嵌入節點G和H，則所得HTML將是來自節點G和H的內容的集中。
* `allowProxy`:如果客戶端庫位於 `/apps`，此屬性允許通過代理servlet訪問它。 請參閱 [查找客戶端庫資料夾並使用代理客戶端庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下。

## 引用客戶端庫 {#referencing-client-side-libraries}

由於HTL是開發站點的首選技術AEM，因此應使用HTL將客戶端庫包括在AEM中。 但是，也可以使用JSP來執行此操作。

### 使用HTL {#using-htl}

在HTL中，客戶端庫通過由提供的幫助模板載入AEM，該幫助模板可通過 [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)。 此檔案中提供了三個模板，可通過 [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **cs**  — 僅載入被引用的客戶端庫的CSS檔案。
* **j**  — 僅載入引用的客戶端庫的JavaScript檔案。
* **全部**  — 載入所引用的客戶端庫（CSS和JavaScript）的所有檔案。

每個 helper 範本都需要 `categories` 選項來參照所需的用戶端程式庫。 這個選項可以是字串值陣列，或是包含逗號分隔值清單的字串。

有關使用情況的詳細資訊和示例，請參閱文檔 [HTML模板語言入門](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

添加 `ui:includeClientLib` 標籤到JSP代碼，以在生成的HTML頁中添加到客戶端庫的連結。 要引用庫，請使用 `categories` 屬性 `ui:includeClientLib` 的下界。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如， `/etc/clientlibs/foundation/jquery` 節點的類型 `cq:ClientLibraryFolder` 具有值屬性的類別 `cq.jquery`。 JSP檔案中的以下代碼引用了庫：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成的HTML頁包含以下代碼：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

有關完整資訊，包括篩選JS、CSS或主題庫的屬性，請參見 [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`，過去常用於包括客戶端庫，自5.6以AEM來已棄用。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 應如上文詳述。

## 建立客戶端庫資料夾 {#creating-client-library-folders}

建立 `cq:ClientLibraryFolder` 節點，以定義JavaScript和級聯樣式表庫，並使它們可用於HTML頁。 使用 `categories` 用於標識其所屬庫類別的節點的屬性。

該節點包含一個或多個源檔案，在運行時，這些檔案合併到單個JS和/或CSS檔案中。 生成的檔案的名稱是節點名稱，其中 `.js` 或 `.css` 檔案副檔名。 例如，名為 `cq.jquery` 生成名為 `cq.jquery.js` 或 `cq.jquery.css`。

客戶端庫資料夾包含以下項：

* 要合併的JS和/或CSS源檔案。
* 支援CSS樣式的資源，如影像檔案。

   **注：** 可以使用子資料夾來組織源檔案。
* 一 `js.txt` 檔案和/或一個 `css.txt` 標識要合併到生成的JS和/或CSS檔案中的源檔案的檔案。

![客戶端](assets/clientlibarch.png)

有關小部件的客戶端庫特定要求的資訊，請參見 [使用和擴展小部件](/help/sites-developing/widgets.md)。

Web客戶端必須具有訪問 `cq:ClientLibraryFolder` 的下界。 您還可以從儲存庫的安全區域中顯示庫（請參閱下面的「從其他庫嵌入代碼」）。

### 覆蓋/lib中的庫 {#overriding-libraries-in-lib}

位於下面的客戶端庫資料夾 `/apps` 優先於同樣位於的同名資料夾 `/libs`。 比如說， `/apps/cq/ui/widgets` 優先於 `/libs/cq/ui/widgets`。 當這些庫屬於同一類別時，下面的庫 `/apps` 的子菜單。

### 查找客戶端庫資料夾並使用代理客戶端庫Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在以前的版本中，客戶端庫資料夾位於以下位置 `/etc/clientlibs` 的下界。 這仍受支援，但建議現在將客戶端庫位於 `/apps`。 這是在其他指令碼附近查找客戶端庫，這些指令碼通常在下面找到 `/apps` 和 `/libs`。

>[!NOTE]
>
>客戶端庫資料夾下的靜態資源必須位於名為 *資源*。 如果資料夾下沒有靜態資源（如影像） *資源*，無法在發佈實例上引用它。 下面是一個示例：https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>為了更好地將代碼與內容和配置隔離，建議在 `/apps` 曝光 `/etc.clientlibs` 通過利用 `allowProxy` 屬性。

為了在 `/apps` 若要訪問，請使用代理伺服器。 ACL仍在客戶端庫資料夾上強制實施，但Servlet允許通過 `/etc.clientlibs/` 的 `allowProxy` 屬性設定為 `true`。

僅當靜態資源位於客戶端庫資料夾下的資源下方時，才能通過代理訪問它。

例如：

* 您在 `/apps/myproject/clientlibs/foo`
* 您在 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然後，您 `allowProxy` 屬性 `foo` 是真的。

* 然後，您可以請求 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然後，可通過 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>使用代理客戶端庫時，AEM Dispatcher配置可能需要更新以確保允許具有擴展客戶端庫的URI。

>[!CAUTION]
>
>Adobe建議在 `/apps` 並使用代理Servlet提供。 但請記住，最佳做法仍然要求公共站點不要包含任何直接通過 `/apps` 或 `/libs` 路徑。

### 建立客戶端庫資料夾 {#create-a-client-library-folder}

1. 在Web瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 選擇要查找客戶端庫資料夾的資料夾，然後按一下 **「建立」>「建立節點」**。
1. 輸入庫檔案的名稱，並在「類型」(Type)清單中選擇 `cq:ClientLibraryFolder`。 按一下 **確定** 然後按一下 **全部保存**。
1. 要指定庫所屬的類別或類別，請選擇 `cq:ClientLibraryFolder` 節點，添加以下屬性，然後按一下 **全部保存**:

   * 名稱：類別
   * 類型：字串
   * 值：類別名稱
   * 多：選擇

1. 通過任何方式將源檔案添加到庫資料夾中。 例如，使用WebDav客戶端複製檔案，或建立檔案並手動創作內容。

   **注：** 如果需要，可以在子資料夾中組織源檔案。

1. 選擇客戶端庫資料夾，然後按一下 **建立>建立檔案**。
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下「確定」：

   * **`js.txt`:** 使用此檔案名生成JavaScript檔案。
   * **`css.txt`:** 使用此檔案名可生成級聯樣式表。

1. 開啟檔案並鍵入以下文本以標識源檔案路徑的根：

   `#base=*[root]*`

   替換* `[root]`*與TXT檔案相對的資料夾路徑。 例如，當源檔案與TXT檔案位於同一資料夾中時，請使用以下文本：

   `#base=.`

   以下代碼將根目錄設定為位於以下位置的名為mobile的資料夾 `cq:ClientLibraryFolder` 節點：

   `#base=mobile`

1. 在下面的行上 `#base=[root]`，鍵入源檔案相對於根目錄的路徑。 將每個檔案名置於單獨的行上。
1. 按一下 **全部保存**。

### 連結到依賴項 {#linking-to-dependencies}

當客戶端庫資料夾中的代碼引用其他庫時，將其他庫標識為依賴項。 在JSP中， `ui:includeClientLib` 引用客戶端庫資料夾的標籤會導致HTML代碼包含到生成的庫檔案的連結以及依賴關係。

依賴項必須是另一個 `cq:ClientLibraryFolder`。 要確定依賴項，請向 `cq:ClientLibraryFolder` 具有以下屬性的節點：

* **名稱：** 依賴
* **類型：** 字串[]
* **值：** 當前庫資料夾所依賴的cq:ClientLibraryFolder節點的categories屬性的值。

例如，/ `etc/clientlibs/myclientlibs/publicmain` 對 `cq.jquery` 的下界。 引用主客戶端庫的JSP生成包含以下代碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他庫中嵌入代碼 {#embedding-code-from-other-libraries}

您可以將代碼從客戶端庫嵌入到另一個客戶端庫。 在運行時，嵌入庫的生成JS和CSS檔案包括嵌入庫的代碼。

嵌入代碼對於提供對儲存在儲存庫的安全區域中的庫的訪問是有用的。

#### 特定於應用的客戶端庫資料夾 {#app-specific-client-library-folders}

最好將所有與應用程式相關的檔案保留在以下應用程式資料夾中 `/apps`。 拒絕網站訪問者訪問 `/apps` 的子菜單。 要滿足這兩種最佳做法，請在下面建立一個客戶端庫資料夾 `/apps`，並使其可通過代理servlet訪問，如下所述 [查找客戶端庫資料夾並使用代理客戶端庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。

使用categories屬性標識要嵌入的客戶端庫資料夾。 要嵌入庫，請向嵌入添加屬性 `cq:ClientLibraryFolder` 節點，使用以下屬性屬性：

* **名稱：** 嵌入
* **類型：** 字串[]
* **值：** 的類別屬性的值 `cq:ClientLibraryFolder` 要嵌入的節點。

#### 使用嵌入最小化請求 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現發佈實例為典型頁面生成的最終HTML包含相對大量 `<script>` 元素，特別是當您的站點使用客戶端上下文資訊進行分析或目標時。 例如，在未優化的項目中，您可能會找到以下系列 `<script>` HTML中的元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在這種情況下，將所有所需的客戶端庫代碼合併到單個檔案中是非常有用的，因此減少了頁面負載上來回請求的數量。 為此，您可以 `embed` 使用應用程式的embed屬性將所需的庫放入特定於應用程式的客戶端庫 `cq:ClientLibraryFolder` 的下界。

以下客戶端庫類別隨附AEM。 您只應嵌入特定站點運行所需的內容。 但是， **您應該維護此處列出的訂單**:

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

嵌入CSS檔案時，生成的CSS代碼使用與嵌入庫相關的資源的路徑。 例如，可公開訪問的庫 `/etc/client/libraries/myclientlibs/publicmain` 嵌入 `/apps/myapp/clientlib` 客戶端庫：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

的 `main.css` 檔案包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS檔案 `publicmain` 節點使用原始影像的URL生成包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 為特定移動組使用庫 {#using-a-library-for-specific-mobile-groups}

使用 `channels` 客戶端庫資料夾的屬性，以標識使用該庫的移動組。 的 `channels` 當為不同的設備功能設計同一類別的庫時，屬性非常有用。

要將客戶端庫資料夾與設備組關聯，請向 `cq:ClientLibraryFolder` 具有以下屬性的節點：

* **名稱：** 通道
* **類型：** 字串[]
* **值：** 移動組的名稱。 要從組中排除庫資料夾，請在名稱前加感嘆號(「！」)。

例如，下表列出了 `channels` 每個客戶端庫資料夾的屬性 `cq.widgets` 類別：

| 客戶端庫資料夾 | 通道屬性值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## 使用預處理器 {#using-preprocessors}

允AEM許可插拔的預處理器，並支援 [YUI壓縮機](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 用於CSS和JavaScript和 [Google關閉編譯器(GCC)](https://developers.google.com/closure/compiler/) 將UIY設定為預設預AEM處理器的JavaScript。

可插拔預處理器允許靈活使用，包括：

* 定義可處理指令碼源的ScriptProcessor
* 處理器可配置為選項
* 處理器可用於微型化，也可用於非微型化案例
* 客戶端庫可以定義要使用的處理器

>[!NOTE]
>
>預設情況下，AEM使用YUI壓縮程式。 查看 [UIY壓縮程式GitHub文檔](https://github.com/yui/yuicompressor/issues) 清單。 切換到特定客戶端的GCC壓縮器可解決使用UYI時觀察到的一些問題。

>[!CAUTION]
>
>不要在客戶端庫中放置精簡庫。 而是提供原始庫，如果需要進行精簡，則使用預處理器的選項。

### 使用狀況 {#usage}

您可以選擇按客戶端庫或系統範圍配置預處理器配置。

* 添加多值屬性 `cssProcessor` 和 `jsProcessor` 在客戶端庫節點上

* 或通過 **HTML庫管理器** OSGi配置

客戶端庫節點上的預處理程式配置優先於OSGI配置。

### 格式和示例 {#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### UYI壓縮機用於CSS縮小和GCC用於JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript預處理，然後GCC細化和模糊處理 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

### 設定系統預設迷你器 {#set-system-default-minifier}

UIY在中設定為預設管理符AEM。 要將此更改為GCC，請執行以下步驟。

1. 轉至Apache Felix Config Manager(位於 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 查找和編輯 **Adobe花崗岩HTML庫經理**。
1. 啟用 **微型** 選項（如果尚未啟用）。
1. 設定值 **JS處理器預設配置** 至 `min:gcc`。

   如果用分號(如 `min:gcc;obfuscate=true`。

1. 按一下 **保存** 的子菜單。

## 調試工具 {#debugging-tools}

提AEM供了幾種調試和測試客戶端庫資料夾的工具。

### 請參閱嵌入式檔案 {#see-embedded-files}

要跟蹤嵌入式代碼的源，或確保嵌入式客戶端庫生成預期結果，可以查看運行時嵌入的檔案的名稱。 要查看檔案名，請追加 `debugClientLibs=true` 的URL。 生成的庫包含 `@import` 語句而不是嵌入代碼。

在上一個示例中 [從其他庫中嵌入代碼](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) 的子菜單。 `/etc/client/libraries/myclientlibs/publicmain` 客戶端庫資料夾嵌入 `/apps/myapp/clientlib` 客戶端庫資料夾。 將參數附加到網頁會在網頁的原始碼中生成以下連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟 `publicmain.css` 檔案顯示以下代碼：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web瀏覽器的地址框中，將以下文本添加到HTML的URL:

   `?debugClientLibs=true`
1. 載入頁面時，查看頁面源。
1. 按一下作為連結元素的href提供的連結以開啟檔案並查看原始碼。

### 發現客戶端庫 {#discover-client-libraries}

的 `/libs/cq/granite/components/dumplibs/dumplibs` 元件生成關於系統上所有客戶端庫資料夾的資訊頁面。 的 `/libs/granite/ui/content/dumplibs` 節點將元件作為資源類型。 要開啟該頁，請使用以下URL（根據需要更改主機和埠）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

該資訊包括庫路徑和類型（CSS或JS）以及庫屬性的值，如類別和依賴項。 該頁上的後續表顯示了每個類別和通道中的庫。

### 請參閱生成的輸出 {#see-generated-output}

的 `dumplibs` 元件包括test選擇器，該選擇器顯示為 `ui:includeClientLib` 標籤。 該頁包括js、css和主題屬性的不同組合的代碼。

1. 使用以下方法之一開啟「Test輸出」頁：

   * 從 `dumplibs.html` 中，按一下 **按一下這裡進行輸出測試** 的子菜單。

   * 在Web瀏覽器中開啟以下URL（根據需要使用其他主機和埠）:

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   預設頁顯示類別屬性沒有值的標籤的輸出。

1. 要查看類別的輸出，請鍵入客戶端庫的 `categories` 屬性，按一下 **提交查詢**。

## 為開發和生產配置庫處理 {#configuring-library-handling-for-development-and-production}

HTML庫管理器服務進程 `cq:ClientLibraryFolder` 標籤並在運行時生成庫。 環境、開發或生產的類型決定了您應如何配置服務：

* 提高安全性：禁用調試
* 提高效能：刪除空白並壓縮庫。
* 提高可讀性：包括空白，不壓縮。

有關配置服務的資訊，請參見 [AEMHTML庫管理器](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
