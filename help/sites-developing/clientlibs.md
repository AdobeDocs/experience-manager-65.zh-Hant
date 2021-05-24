---
title: 使用用戶端端程式庫
seo-title: 使用用戶端端程式庫
description: AEM提供用戶端程式庫資料夾，可讓您將用戶端程式碼儲存在存放庫中、將其組織為類別，以及定義將每類程式碼提供給用戶端的時間和方式
seo-description: AEM提供用戶端程式庫資料夾，可讓您將用戶端程式碼儲存在存放庫中、將其組織為類別，以及定義將每類程式碼提供給用戶端的時間和方式
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 0%

---

# 使用用戶端端程式庫{#using-client-side-libraries}

現代網站嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 組織並最佳化此程式碼的服務可能是個複雜的問題。

為了解決此問題，AEM提供&#x200B;**用戶端程式庫資料夾**，可讓您將用戶端程式碼儲存在存放庫中、將其組織為類別，以及定義將每類程式碼提供給用戶端的時間和方式。 然後，用戶端資料庫系統會負責在您的最終網頁中產生正確的連結，以載入正確的程式碼。

## 用戶端程式庫在AEM中的運作方式{#how-client-side-libraries-work-in-aem}

在頁面的HTML中包含用戶端程式庫（即JS或CSS檔案）的標準方式，只是在該頁面的JSP中包含`<script>`或`<link>`標籤，並包含相關檔案的路徑。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

雖然此方法適用於AEM，但在頁面及其組成元件變得複雜時，可能會導致問題。 在這種情況下，最終HTML輸出中可能會包含相同JS程式庫的多個副本。 為避免此問題並允許用戶端程式庫的邏輯組織，AEM使用&#x200B;**用戶端程式庫資料夾**。

客戶端庫資料夾是`cq:ClientLibraryFolder`類型的儲存庫節點。 [CND標籤法](https://jackrabbit.apache.org/node-type-notation.html)中的定義是

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

預設情況下，`cq:ClientLibraryFolder`節點可以放置在儲存庫的`/apps`、`/libs`和`/etc`子樹中的任意位置(這些預設值以及其他設定可通過[系統控制台](https://localhost:4502/system/console/configMgr)的&#x200B;**AdobeGranite HTML庫管理器**&#x200B;面板進行控制)。

每個`cq:ClientLibraryFolder`都會填入一組JS和/或CSS檔案，以及一些支援檔案（請參閱下方）。 `cq:ClientLibraryFolder`的屬性配置如下：

* `categories`:識別今秋JS和/或CSS檔案集所屬的類 `cq:ClientLibraryFolder` 別。`categories`屬性為多值，可讓程式庫資料夾成為多個類別的一部分（請參閱下方，了解其效用）。

* `dependencies`:這是此庫資料夾所依賴的其他客戶端庫類別的清單。例如，給定兩個`cq:ClientLibraryFolder`節點`F`和`G`，如果`F`中的檔案需要`G`中的另一個檔案才能正常工作，則`G`中的`categories`中至少一個應位於`F`的`dependencies`中。

* `embed`:用於從其他程式庫中內嵌程式碼。如果節點F內嵌節點G和H，則產生的HTML會是節點G和H的內容集中。
* `allowProxy`:如果用戶端程式庫位於 `/apps`下方，此屬性可透過Proxy Servlet存取。請參閱下面的[查找客戶端庫資料夾和使用代理客戶端庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。

## 引用客戶端庫{#referencing-client-side-libraries}

由於HTL是開發AEM網站的慣用技術，因此HTL應用於在AEM中納入用戶端程式庫。 但是，也可以使用JSP執行此操作。

### 使用HTL {#using-htl}

在HTL中，用戶端程式庫會透過AEM提供的協助範本載入，可透過[ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)存取。 此檔案中提供三個模板，可通過[ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)調用：

* **css**  — 僅載入所參考用戶端資料庫的CSS檔案。
* **js**  — 僅載入所參考用戶端程式庫的JavaScript檔案。
* **all**  — 載入所參考用戶端程式庫（包括CSS和JavaScript）的所有檔案。

每個幫助程式模板都需要一個`categories`選項來引用所需的客戶端庫。 該選項可以是字串值的陣列，或包含逗號分隔值清單的字串。

有關詳細資訊和用法的示例，請參閱文檔[HTML模板語言快速入門](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)。

### 使用JSP {#using-jsp}

將`ui:includeClientLib`標籤添加到JSP代碼中，以向生成的HTML頁中的客戶端庫添加連結。 若要參考程式庫，請使用`ui:includeClientLib`節點的`categories`屬性值。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如，`/etc/clientlibs/foundation/jquery`節點為類型`cq:ClientLibraryFolder`，類別屬性為值`cq.jquery`。 JSP檔案中的以下代碼引用庫：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

產生的HTML頁面包含下列程式碼：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

如需完整資訊，包括篩選JS、CSS或主題程式庫的屬性，請參閱[ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)。

>[!CAUTION]
>
>`<cq:includeClientLib>`，過去通常用於包含用戶端程式庫，自AEM 5.6起即已棄用。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 應如上所述使用。

## 建立客戶端庫資料夾{#creating-client-library-folders}

建立`cq:ClientLibraryFolder`節點以定義JavaScript和階層式樣式表程式庫，並使其可用於HTML頁面。 使用節點的`categories`屬性來識別其所屬的程式庫類別。

節點包含一或多個執行階段會合併為單一JS和/或CSS檔案的來源檔案。 生成的檔案的名稱是副檔名為`.js`或`.css`的節點名。 例如，名為`cq.jquery`的庫節點會產生名為`cq.jquery.js`或`cq.jquery.css`的生成檔案。

用戶端程式庫資料夾包含下列項目：

* 要合併的JS和/或CSS來源檔案。
* 支援CSS樣式的資源，例如影像檔案。

   **注意：** 您可以使用子資料夾來組織來源檔案。
* 一個`js.txt`檔案和/或一個`css.txt`檔案，用於標識要合併到生成的JS和/或CSS檔案中的源檔案。

![clientlibarch](assets/clientlibarch.png)

有關介面工具集的客戶端庫特定需求的資訊，請參閱[使用和擴展介面工具集](/help/sites-developing/widgets.md)。

Web客戶端必須具有訪問`cq:ClientLibraryFolder`節點的權限。 您也可以從存放庫的安全區域公開程式庫（請參閱下方的「從其他程式庫內嵌程式碼」）。

### 在/lib {#overriding-libraries-in-lib}中覆蓋庫

位於`/apps`下的客戶端庫資料夾優先於位於`/libs`中的同名資料夾。 例如，`/apps/cq/ui/widgets`優先於`/libs/cq/ui/widgets`。 當這些程式庫屬於相同類別時，會使用`/apps`下方的程式庫。

### 找到客戶端庫資料夾並使用代理客戶端庫Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在舊版中，用戶端程式庫資料夾位於存放庫的`/etc/clientlibs`下方。 目前仍支援此功能，但建議現在將用戶端程式庫置於`/apps`下。 這是為了在其他指令碼附近找到客戶端庫，這些指令碼通常位於`/apps`和`/libs`下。

>[!NOTE]
>
>客戶端庫資料夾下的靜態資源必須位於名為&#x200B;*resources*&#x200B;的資料夾中。 如果您在資料夾&#x200B;*resources*&#x200B;下沒有靜態資源（例如影像），則無法在發佈執行個體上參照該資源。 以下是範例：https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>為了更好地將代碼與內容和配置隔離，建議在`/apps`下找到客戶端庫，並利用`/etc.clientlibs`屬性來公開它們。`allowProxy`

為了存取`/apps`下的用戶端程式庫，需使用代理伺服器。 ACL仍在客戶端庫資料夾上強制執行，但如果`allowProxy`屬性設定為`true`，則servlet允許通過`/etc.clientlibs/`讀取內容。

靜態資源位於客戶端庫資料夾下的資源下，則只能通過代理訪問。

例如：

* `/apps/myproject/clientlibs/foo`中有clientlib
* `/apps/myprojects/clientlibs/foo/resources/icon.png`中有靜態影像

然後，將`foo`上的`allowProxy`屬性設為true。

* 然後，您可以請求`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然後，您可以透過`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`參考影像

>[!CAUTION]
>
>使用代理用戶端程式庫時，AEM Dispatcher設定可能需要更新，以確保允許具有擴充用戶端的URI。

>[!CAUTION]
>
>Adobe建議在`/apps`下找到客戶端庫，並使用代理Servlet使其可用。 但請記住，最佳實務仍要求公用網站不得包含直接透過`/apps`或`/libs`路徑提供的任何內容。

### 建立客戶端庫資料夾{#create-a-client-library-folder}

1. 在網頁瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 選擇要查找客戶端庫資料夾的資料夾，然後按一下&#x200B;**「建立」>「建立節點」**。
1. 輸入庫檔案的名稱，並在「類型」清單中選擇`cq:ClientLibraryFolder`。 按一下&#x200B;**OK**，然後按一下&#x200B;**Save All**。
1. 要指定庫所屬的類別或類別，請選擇`cq:ClientLibraryFolder`節點，添加以下屬性，然後按一下&#x200B;**保存全部**:

   * 名稱：類別
   * 類型：字串
   * 值：類別名稱
   * 多重：選擇

1. 通過任何方法將源檔案添加到庫資料夾。 例如，使用WebDav客戶端來複製檔案，或建立檔案並手動編寫內容。

   **注意：** 您可以視需要在子資料夾中組織來源檔案。

1. 選擇客戶端庫資料夾，然後按一下&#x200B;**建立>建立檔案**。
1. 在檔案名框中，鍵入以下檔案名之一，然後按一下「確定」：

   * **`js.txt`:** 使用此檔案名稱產生JavaScript檔案。
   * **`css.txt`:** 使用此檔案名生成級聯樣式表。

1. 開啟檔案並鍵入以下文本以標識源檔案路徑的根：

   `#base=*[root]*`

   將* `[root]`*替換為包含源檔案的資料夾的路徑（相對於TXT檔案）。 例如，當源檔案與TXT檔案位於同一資料夾時，請使用以下文本：

   `#base=.`

   下列程式碼會將根設定為`cq:ClientLibraryFolder`節點下方名為mobile的資料夾：

   `#base=mobile`

1. 在`#base=[root]`下的行中，鍵入源檔案相對於根的路徑。 將每個檔案名放在單獨的一行。
1. 按一下「**全部保存**」。

### 連結到依賴項{#linking-to-dependencies}

當用戶端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 在JSP中，引用客戶端庫資料夾的`ui:includeClientLib`標籤會使HTML代碼包含到生成的庫檔案的連結以及依賴項。

相依性必須是另一個`cq:ClientLibraryFolder`。 若要識別相依性，請使用下列屬性將屬性新增至您的`cq:ClientLibraryFolder`節點：

* **名稱：** 相依性
* **類型：** 字串[]
* **值：** 目前程式庫資料夾所仰賴之cq:ClientLibraryFolder節點的categories屬性值。

例如， / `etc/clientlibs/myclientlibs/publicmain`與`cq.jquery`程式庫有相依性。 引用主客戶端庫的JSP將生成包含以下代碼的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他庫{#embedding-code-from-other-libraries}嵌入代碼

您可以將用戶端程式庫的程式碼內嵌至另一個用戶端程式庫。 在執行階段，內嵌程式庫產生的JS和CSS檔案會包含內嵌程式庫的程式碼。

嵌入代碼對於提供對儲存在儲存庫安全區域中的庫的訪問非常有用。

#### 應用程式專用客戶端庫資料夾{#app-specific-client-library-folders}

最好將所有與應用程式相關的檔案保留在`/app`以下的應用程式資料夾中。 拒絕網站訪客存取`/app`資料夾也是最佳作法。 要滿足這兩種最佳做法，請在`/etc`資料夾下建立一個客戶端庫資料夾，該資料夾嵌入位於`/app`下的客戶端庫。

使用categories屬性來識別要內嵌的用戶端程式庫資料夾。 若要內嵌程式庫，請使用下列屬性，將屬性新增至內嵌`cq:ClientLibraryFolder`節點：

* **名稱：** 內嵌
* **類型：** 字串[]
* **值：** 要嵌入的節點的categories屬 `cq:ClientLibraryFolder` 性的值。

#### 使用內嵌來最小化請求{#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現，您的發佈例項為一般頁面產生的最終HTML包含相對大量的`<script>`元素，尤其是如果您的網站使用用戶端內容資訊進行分析或鎖定目標時。 例如，在非最佳化的專案中，您可能會在頁面的HTML中找到下列系列的`<script>`元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在這種情況下，將所有必要的用戶端程式庫程式碼合併到單一檔案中，以減少頁面載入時來回請求的數量，會是很實用的作法。 若要這麼做，您可以使用`cq:ClientLibraryFolder`節點的embed屬性，將所需的程式庫`embed`整合至應用程式專用的用戶端程式庫。

AEM包含下列用戶端程式庫類別。 您應僅內嵌特定網站運作所需的內容。 但是，**您應維護此處列出的順序**:

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

#### CSS檔案{#paths-in-css-files}中的路徑

內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫`/etc/client/libraries/myclientlibs/publicmain`內嵌`/apps/myapp/clientlib`用戶端程式庫：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

`main.css`檔案包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain`節點生成的CSS檔案使用原始影像的URL包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 使用特定行動群組的資料庫{#using-a-library-for-specific-mobile-groups}

使用用戶端程式庫資料夾的`channels`屬性來識別使用程式庫的行動群組。 當針對不同裝置功能設計相同類別的程式庫時， `channels`屬性很實用。

要將客戶端庫資料夾與設備組關聯，請將屬性添加到`cq:ClientLibraryFolder`節點，該節點具有以下屬性：

* **名稱：** 頻道
* **類型：** 字串[]
* **值：** 行動群組的名稱。若要從群組中排除程式庫資料夾，請在名稱前加上感嘆號(&quot;!&quot;)。

例如，下表列出了`cq.widgets`類別中每個客戶端庫資料夾的`channels`屬性值：

| 客戶端庫資料夾 | channels屬性的值 |
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

## 使用前置處理器{#using-preprocessors}

AEM支援可插拔的前置處理器，並隨附支援[YUI壓縮器](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor)（適用於CSS和JavaScript）和[Google關閉編譯器(GCC)](https://developers.google.com/closure/compiler/)(適用於JavaScript，將YUI設定為AEM預設預處理器)。

可插拔預處理器允許靈活使用，包括：

* 定義可處理指令碼源的指令碼處理器
* 處理器可配置選項
* 處理器可用於縮制，但也可用於非縮制的情況
* clientlib可定義要使用的處理器

>[!NOTE]
>
>依預設，AEM會使用YUI壓縮器。 如需已知問題的清單，請參閱[YUI壓縮機GitHub檔案](https://github.com/yui/yuicompressor/issues)。 切換至特定客戶端的GCC壓縮機可解決使用UI時觀察到的一些問題。

>[!CAUTION]
>
>請勿將縮制的程式庫放入用戶端程式庫。 請改為提供原始程式庫，如果需要縮制，請使用前置處理器的選項。

### 使用狀況 {#usage}

您可以選擇為每個客戶端庫或系統範圍配置前置處理器配置。

* 在clientlibrary節點上新增多值屬性`cssProcessor`和`jsProcessor`

* 或者，透過&#x200B;**HTML Library Manager** OSGi設定定義系統預設配置

clientlib節點上的預處理器配置優先於OSGI配置。

### 格式和範例{#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### CSS縮制和GCC for JS {#yui-compressor-for-css-minification-and-gcc-for-js}的UI壓縮器

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 鍵入指令碼以預處理，然後GCC到縮制和模糊化{#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他GCC選項{#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有關GCC選項的詳細資訊，請參見[GCC文檔](https://developers.google.com/closure/compiler/docs/compilation_levels)。

### 設定系統預設縮制符{#set-system-default-minifier}

在AEM中，YUI設為預設縮制碼。 要將此更改為GCC，請執行以下步驟。

1. 前往[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)前往Apache Felix Config Manager
1. 尋找並編輯&#x200B;**AdobeGranite HTML程式庫管理員**。
1. 啟用&#x200B;**Minify**&#x200B;選項（如果尚未啟用）。
1. 將值&#x200B;**JS處理器預設配置**&#x200B;設定為`min:gcc`。

   如果以分號(例如`min:gcc;obfuscate=true`。

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

## 調試工具{#debugging-tools}

AEM提供數種工具，用於偵錯和測試用戶端程式庫資料夾。

### 請參閱嵌入的檔案{#see-embedded-files}

若要追蹤內嵌程式碼的來源，或確保內嵌的用戶端程式庫能產生預期的結果，您可以在執行階段查看內嵌的檔案名稱。 若要查看檔案名稱，請將`debugClientLibs=true`參數附加至網頁的URL。 產生的程式庫包含`@import`陳述式，而非內嵌程式碼。

在上一個[從其他庫嵌入代碼](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)部分的示例中， `/etc/client/libraries/myclientlibs/publicmain`客戶端庫資料夾嵌入`/apps/myapp/clientlib`客戶端庫資料夾。 將參數附加到網頁會在網頁的原始碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟`publicmain.css`檔案會顯示下列程式碼：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL中：

   `?debugClientLibs=true`
1. 頁面載入時，檢視頁面來源。
1. 按一下作為連結元素的href提供的連結，以開啟檔案並檢視原始碼。

### 發現客戶端庫{#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs`元件生成有關係統上所有客戶端庫資料夾的資訊頁。 `/libs/granite/ui/content/dumplibs`節點將元件作為資源類型。 若要開啟頁面，請使用下列URL（視需要變更主機和連接埠）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

資訊包括程式庫路徑和類型（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和管道中的程式庫。

### 請參閱生成的輸出{#see-generated-output}

`dumplibs`元件包含測試選擇器，用於顯示為`ui:includeClientLib`標籤生成的原始碼。 頁面包含不同js、css和主題屬性組合的程式碼。

1. 使用下列其中一種方法開啟「測試輸出」頁面：

   * 從`dumplibs.html`頁面，按一下&#x200B;**按一下這裡以輸出測試**&#x200B;文字中的連結。

   * 在網頁瀏覽器中開啟下列URL（視需要使用不同的主機和連接埠）:

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   預設頁面顯示沒有類別屬性值之標籤的輸出。

1. 若要查看類別的輸出，請輸入客戶端庫的`categories`屬性的值，然後按一下&#x200B;**Submit Query**。

## 為開發和生產配置程式庫處理{#configuring-library-handling-for-development-and-production}

HTML Library Manager服務會處理`cq:ClientLibraryFolder`標籤，並在執行階段產生程式庫。 環境、開發或生產的類型會決定您應如何設定服務：

* 提高安全性：停用除錯
* 提高效能：移除空白字元並壓縮程式庫。
* 改善可讀性：包含空白字元且不壓縮。

有關配置服務的資訊，請參閱[AEM HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)。
