---
title: SEO和URL管理最佳實踐
seo-title: SEO and URL Management Best Practices
description: 瞭解SEO最佳實踐和建議，以在實施中AEM實現這些。
seo-description: Learn about SEO best practices and recommendations for achieving these on an AEM implementation.
topic-tags: managing
content-type: reference
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3802'
ht-degree: 75%

---

# SEO和URL管理最佳實踐{#seo-and-url-management-best-practices}

搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，許多項目需要解決徐工機構的AEM擔憂。

本文件首先會說明在 AEM 實作中達成上述目標的幾項 [SEO 最佳作法](#seo-best-practices)與建議。接著，本文件會於第一節中再深入探討幾項更[複雜的實作步驟](#aem-configurations)。

## SEO 最佳作法 {#seo-best-practices}

本節說明幾項一般 SEO 最佳作法。

### URL {#urls}

處理 URL 時，業界有一些普遍接受的最佳作法。

在評估 AEM 專案的 URL 時，請先自問以下問題：

「如果用戶要查看此URL，而沒有看到頁面上的任何內容，他們能描述此頁面是什麼嗎？」

如果答案是可以，則此 URL 在搜尋引擎中很可能成效良好。

以下為幾項針對 SEO 建構 URL 的常見訣竅：

* 使用連字號來分隔字詞。

   * 請將連字號當作分隔符號來命名網頁。
   * 避免使用駝峰式大小寫、底線和空格。

* 可行的話，避免使用查詢參數。如需使用，請不要超過兩個。

   * 如果可用，請使用目錄結構來指示資訊架構。
   * 如果無法使用目錄結構，請在 URL 中使用 Sling 選擇器，而非查詢字串。除了可提供 SEO 值，Sling 選擇器也會使網頁可供 Dispatcher 進行快取。

* URL 越容易透過字面理解越好；如果 URL 中存在關鍵字，SEO 值會大幅提升。

   * 在網頁上使用選擇器時，建議使用提供語意值的選取器。
   * 如果使用者無法透過字面理解您的 URL，則搜尋引擎也無法。
   * 例如：
      `mybrand.com/products/product-detail.product-category.product-name.html`
比  更適合 
`mybrand.com/products/product-detail.1234.html`

* 盡可能避免子網域，因為搜尋引擎會將子網域視為不同的實體，進而分割網站的 SEO 值。

   * 請使用第一層子路徑。舉例來說，請避免使用 `es.mybrand.com/home.html`，改用 `www.mybrand.com/es/home.html`。

   * 請根據本指引規劃內容階層，以便符合內容呈現方式。

* URL 的長度和關鍵字的位置增加，URL 中關鍵字的有效性就會降低。換句話說，URL 越短越好。

   * 請使用 AEM 提供的 URL 縮短技術和功能來移除不必要的 URL 片段。
   * 舉例來說，`mybrand.com/en/myPage.html` 比 `mybrand.com/content/my-brand/en/myPage.html` 更適合。

* 使用標準 URL。

   * 如果 URL 可從不同路徑或透過不同參數或選擇器運作，請務必在網頁上使用 `rel=canonical` 標籤。

   * 此標籤可納入 AEM 範本的程式碼中。

* 盡可能使 URL 與網頁標題相符。

   * 建議內容作者遵循這項作法。

* 支援在 URL 請求中不區分大小寫。

   * 將 Dispatcher 設定為將所有傳入請求重新寫入為小寫字母。
   * 請訓練內容作者使用小寫字母來建立所有網頁。

* 每個網頁都必須只經由一個通訊協定來提供。

   * 有時，網站會透過 `http` 提供，直到使用者以結帳或登入形式抵達網頁後，才會切換為透過 `https` 提供。從這個頁面連結時，如果使用者可返回 `http` 頁面並透過 `https` 存取，搜尋引擎會將這些頁面當成兩個獨立頁面來追蹤。

   * 目前 Google 偏好使用 `https` 頁面，而非 `http` 頁面。因為這個原因，透過 `https` 提供整個網站通常才能讓每個人的生活更便利。

### 伺服器設定 {#server-configuration}

進行伺服器設定時，您可以執行下列步驟，確保系統只對正確的內容進行編目：

* 使用 `robots.txt` 檔案來阻止系統對任何不應納入索引的內容進行編目。

   * 封鎖測試環境上的&#x200B;**所有**&#x200B;編目動作。

* 如果要啟動的新網站有更新過的 URL，請實作 301 重新導向，確保現有的 SEO 排名不會遺失。
* 加入您網站的 Favicon。
* 實作 XML Sitemap，讓搜尋引擎更容易對您的內容進行編目。請務必加入行動 Sitemap 供行動及/或回應式網站使用。

## AEM 設定 {#aem-configurations}

本節說明設定 AEM 的所需實作步驟，以便遵循上述 SEO 建議。

### 使用 Sling 選擇器 {#using-sling-selectors}

過去，業界在建置企業網路應用程式時普遍使用查詢參數。

但近年來，趨勢已改為移除這些參數，以便讓 URL 從字面上更易於理解。在許多平台上，這種趨勢包括在網頁伺服器或內容傳遞網路 (CDN) 上實作重新導向，但 Sling 可讓這項作業變得簡單明瞭。Sling 選擇器：

* 改善 URL 可讀性。
* 讓您在 Dispatcher 上對網頁進行快取，且通常可提高安全性。
* 您可以直接處理內容，而不是採用一般 servlet 來擷取內容。此特性可讓您將 ACL 的優勢應用在存放庫，並將篩選器應用在 Dispatcher。

#### 針對 servlet 使用選擇器 {#using-selectors-for-servlets}

AEM 提供兩種編寫 servlet 的選項：

* **bin** servlet
* **Sling** servlet

下列範例說明如何註冊同時符合以下兩種模式的 servlet，以及使用 Sling servlet 所獲的益處。

#### Bin servlet (向下一個層級) {#bin-servlets-one-level-down}

**Bin** servlet 符合許多開發人員在 J2EE 程式設計中慣用的模式。Servlet 會註冊於特定路徑，這種情況下 AEM 通常位於 `/bin` 下，而您必須從查詢字串擷取所需請求參數。

此類 servlet 的 SCR 注釋如下所示：

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

您接著會透過 `doGet` 方法中所包含的 `SlingHttpServletRequest` 物件從查詢字串中擷取參數；舉例來說：

```
String myParam = req.getParameter("myParam");
```

最後產生的所用 URL 如下所示：

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

採用這種方法需要考量以下幾點：

* URL 本身會遺失 SEO 值。存取網站 (包括搜尋引擎) 的使用者不會從 URL 收到任何語意值，因為 URL 代表程式設計路徑，而非內容階層。
* URL 中存在查詢參數，代表 Dispatcher 將無法對回應進行快取。
* 如果要保護此 servlet 的安全，您需要在 servlet 中實作自己的自訂安全邏輯。
* Dispatcher 必須經過審慎設定以公開 `/bin/myApp/myServlet`。僅僅公開 `/bin`，會使網站訪客可存取不應向他們開放的特定 servlet。

#### Sling servlet (向下一個層級) {#sling-servlets-one-level-down}

**Sling** servlet 可讓您以相反的方式註冊 servlet。您不需要指定 servlet 位址並指定要讓 servlet 根據查詢參數轉譯的內容，僅需指出您想要的內容，並指定應根據 Sling 選擇器轉譯內容的 servlet。

此類 servlet 的 SCR 注釋如下所示：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

在這種情況下，URL 所處理的資源 (`myPageType` 資源的例項) 可在 servlet 中自動供訪客存取。如要存取該資源，請呼叫：

```
Resource myPage = req.getResource();
```

最後產生的所用 URL 如下所示：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

此方法的優點包括：

* 您可以控制經由網站階層和網頁名稱中所呈現語意而獲得的 SEO 值。
* 由於不存在查詢參數，因此 Dispatcher 可以對回應進行快取。此外，已定址網頁一經啟用，對該網頁所做的任何更新都會使這個快取失效。
* 如有使用者嘗試存取此 servlet，套用到 `/content/my-brand/my-page` 的所有 ACL 都會生效。
* Dispatcher 將會已預先設定為將此內容當作為網站供應內容的函式來提供，無需額外設定。

### URL 重新寫入 {#url-rewriting}

在 AEM 中，所有網頁都儲存在下方 `/content/my-brand/my-content`。雖然從存放庫資料管理的角度來看，這樣的設定很實用，但卻未必是您希望客戶看到網站的方式，而且可能與 SEO 指導方針有衝突，不符合盡可能縮短 URL 的原則。此外，您可能會從同一個 AEM 例項及不同網域名稱為多個網站供應內容。

本節將說明在 AEM 管理這些 URL 並且以更容易從字面理解的 SEO 建議方法向使用者呈現的可用選項。

#### 虛名 URL {#vanity-urls}

如果作者為了推銷目的而想要讓某個網頁可從第二個位置存取，採用以逐頁方式定義的 AEM 虛名 URL 也許是個好方法。若要新增網頁的虛名 URL，請在&#x200B;**網站**&#x200B;控制台導覽至該頁面，並編輯頁面屬性。在&#x200B;**基本**&#x200B;標籤底部，您會看到可新增虛名 URL 的區段。別忘了，如果某個網頁可透過多個 URL 存取，該頁的 SEO 值就會遭到分割，因此您應將標準 URL 標籤新增至該頁才能避免此問題。

#### 本地化的網頁名稱 {#localized-page-names}

建議向翻譯內容的使用者顯示本地化的網頁名稱 。例如：

* 與其讓講西班牙語的使用者導覽至：
   `www.mydomain.com/es/home.html`

* 建議讓 URL 顯示為：
   `www.mydomain.com/es/casa.html`。

本地化網頁名稱時會面對的困難是，許多 AEM 平台上可用的本地化工具都需要不同位置的網頁有相符的名稱，才能讓內容保持同步。

`sling:alias` 屬性不僅讓您看得到好處，也享用得到好處。您可以在任何資源中將 `sling:alias` 新增為屬性，允許資源使用別名。在上一個範例中：

* 原本在 JCR 的網頁是：
   `…/es/home`

* 新增屬性後變成：
   `sling:alias` = `casa`

這樣一來，AEM 翻譯工具 (例如多網站管理員) 就能繼續維護以下兩者的關聯性：

* `/en/home`

* `/es/home`

同時允許使用者以自己的原生語言與網頁名稱互動。

>[!NOTE]
>
>[在編輯網頁屬性時，您可使用別名屬性](/help/sites-authoring/editing-page-properties.md#advanced)來設定 `sling:alias` 屬性。

#### /etc/map {#etc-map}

在標準的 AEM 配置中：

* OSGi 設定為
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 屬性為
   **對應位置** ( `resource.resolver.map.location`)

* 預設為 `/etc/map`。

您可以在此位置新增對應定義，以便對應傳入請求、重新寫入 AEM 中的網頁 URL，或兩者皆執行。

如要建立新對應，則在此位置的 `/http` 或 `/https` 之下建立新 `sling:Mapping` 節點。AEM 會根據設定在此節點上的 `sling:match` 和 `sling:internalRedirect` 屬性，將相符 URL 的所有流量重新導向至在 `internalRedirect` 屬性指定的值。

雖然上述方法已記錄在官方 AEM 和 Sling 文件中，但與直接使用 `SlingResourceResolver` 時的可用選項相比，這種實作方法支援的規則運算式卻範圍有限。此外，以這種方式實作對應可能會導致 Dispatcher 快取失效的問題。

以下是此問題發生的例子：

1. 使用者造訪您的網站並請求 `https://www.mydomain.com/my-page.html`
1. Dispatcher 將此請求轉發到發佈伺服器。
1. 發佈伺服器使用 `/etc/map` 將此請求解析到 `/content/my-brand/my-page`，並轉譯網頁。

1. Dispatcher 在 `/my-page.html` 對回應進行快取，並將回應回傳給使用者。
1. 內容作者對此網頁作出變更並加以啟用。
1. Dispatcher 排清代理程式傳送 `/content/my-brand/my-page`**的無效請求。** 由於 Dispatcher 在此路徑上沒有經過快取的網頁，因此系統會維持對舊內容進行快取，導致內容過時。

有些方法可以設定自訂發送排清規則，針對快取失效將較短的 URL 對應至較長的 URL。

不過，另外也有更簡單的方法可用於管理這個問題：

1. **SlingResourceResolver 規則**

   您可以使用 Web 控制台 (例如 localhost:4502/system/console/configMgr) 設定 Sling Resource Resolver：

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`。
   建議您建置所需對應來將 URL 縮短為規則運算式，然後在包含在您所建置項目的 OsgiConfignode `config.publish` 下定義這些設定。

   您不必在 `/etc/map` 定義對應，因為這些對應可以直接指派給屬性&#x200B;**URL 對應** ( `resource.resolver.mapping`)：

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在這個簡單範例中，您會從任何存在 `/content/my-brand/` 的 URL 開頭中將之移除。

   於是 URL 會：

   * 從 `/content/my-brand/my-page.html`
   * 轉換成 `/my-page.html`

   這個結果就符合將 URL 盡量縮短的建議做法。

1. **在網頁上對應 URL 輸出**

   在 Apache Sling Resource Resolver 中定義對應後，您必須在元件中使用這些對應，確保您輸出在網頁上的 URL 簡短且整齊。您可以使用 `ResourceResolver` 的對應函式來完成此操作。

   舉例來說，如果您要實作一項自訂導覽元件來列出目前頁面的子項，則可使用如下對應方法：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

至此，您已與元件中的邏輯一併實作完成對應，以便在將 URL 輸出至頁面時使用這些對應。

最後一個步驟，就是在這些縮短的 URL 進入 `mod_rewrite` 會發揮作用的 Dispatcher 時處理這些 URL。使用 `mod_rewrite` 的最大優點，就是 URL 在傳送到 Dispatcher 模組&#x200B;*之前*&#x200B;會先重新對應到原本的較長格式。也就是說，Dispatcher 會從發佈伺服器請求長 URL 並加以進行快取。因此，任何來自發佈伺服器的 Dispatcher 排清請求都可以成功使該內容無效。

要實作這些規則，您可以在 Apache HTTP 伺服器設定的虛擬主機下新增 `RewriteRule` 元素。如果您想要拉長上個範例中縮短的 URL，則可實作如下規則：

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 標準 URL 標籤 {#canonical-url-tags}

標準 URL 標籤是放置在 HTML 文件開頭的連結標籤，可釐清搜尋引擎在建立內容索引時應如何處理網頁。它們可帶來的好處是，即使連向網頁的 URL 可能有些差異，也可確保系統對其他版本的網頁建立相同索引。

舉例來說，如果網站想要提供適合列印的網頁版本，搜尋引擎可能會對此版本與一般版本分開建立索引。但標準標籤會告訴搜尋引擎兩者是相同版本。

範例：

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

兩者都會在網頁開頭套用下列標籤：

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

`href` 可以是相對或絕對的值。程式碼應包含在網頁標記中，以便判斷網頁的標準 URL 並輸出此標籤。

### 將 Dispatcher 設定為不區分大小寫 {#configuring-the-dispatcher-for-case-insensitivity}

使用小寫字母來提供所有網頁是建議的最佳作法。但是，您也不應讓使用者在 URL 中輸入大寫字母來存取網站時，收到 404 錯誤訊息。因此，Adobe 建議您在 Apache HTTP 伺服器設定中新增重新寫入規則，以便將所有傳入的 URL 對應至小寫。此外，內容作者必須接受訓練以小寫名稱建立網頁。

如要設定 Apache 以強制所有轉入流量都轉換為小寫，請將以下內容新增到 `vhost` 設定中：

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

此外，將下列內容新增至 `htaccess` 檔案的最上方：

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 實作 robots.txt 以保護開發環境 {#implementing-robots-txt-to-protect-development-environments}

搜尋引擎在對網站進行編目之前，*必須*&#x200B;先檢查網站的根目錄中是否有 `robots.txt` 檔案。我們在此強調「必須」，是因為雖然 Google、Yahoo 或 Bing 等主流搜尋引擎都會這麼做，但有些外國搜尋引擎卻並不如此。

封鎖使用者存取整個網站的最簡單方式，是將名為 `robots.txt` 的檔案置於網站根目錄中，且含有以下內容：

```xml
User-agent: *
Disallow: /
```

或者，您可以在即時環境中選擇不允許某些不希望建立索引的路徑。

將 `robots.txt` 檔案置於網站根目錄時應注意，Dispatcher 排清請求可能會清除此檔案，且 URL 對應可能會將網站根目錄置於與 Apache HTTP 伺服器設定中已定義的 `DOCROOT` 不同之處。因此，常見的方式是將此檔案放置在根目錄的作者例項上，並複製到發佈例項。

### 在 AEM 上建置 XML Sitemap {#building-an-xml-sitemap-on-aem}

編目程式可透過 XML Sitemap 加強瞭解網站的結構。雖然提供 Sitemap 並不保證可改善 SEO 排名，但這是一項普遍採用的最佳作法。您可以手動在網頁伺服器上維護 XML 檔案，以便將它當作 Sitemap 使用，但建議以程式設計方式產生 Sitemap，確保當作者建立新內容時，Sitemap 會自動反映變更。

使AEM用 [Apache Sling Sitemap模組](https://github.com/apache/sling-org-apache-sling-sitemap) 生成XML站點集，它為開發人員和編輯器提供了多種選項，使站點XML站點地圖保持最新。

>[!NOTE]
>
> 自Adobe Experience Manager6.5.11.0版起，此功能可作為產品功能使用。
> 
> 對於較舊版本，您可以自行註冊Sling Servlet，以偵聽 `sitemap.xml` 調用並使用通過servlet API提供的資源查找當前頁面及其子體以輸出sitemap.xml檔案。

Apache Sling Sitemap模組區分頂層站點地圖和嵌套站點地圖，這兩者都是為具有 `sling:sitemapRoot` 屬性設定為 `true`。 通常，使用樹的頂級站點地圖路徑（即沒有其他站點地圖根祖先的資源）上的選擇器來呈現站點。 此頂級站點地圖根還顯示站點地圖索引，該索引通常是站點所有者在搜索引擎的配置門戶中配置或添加到站點的索引 `robots.txt`。

例如，請考慮在以下位置定義頂級站點地圖根的站點 `my-page` 和嵌套站點地圖根 `my-page/news`，為新聞子樹中的頁面生成專用站點地圖。 因此，相關的URL

* https://www.mydomain.com/my-brand/my-page.sitemap-index.xml
* https://www.mydomain.com/my-brand/my-page.sitemap.xml
* https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html

>[!NOTE]
>
> 選擇器 `sitemap` 和 `sitemap-index` 可能會干擾自定義實現。 如果不想使用產品功能，請配置您自己的Servlet，使用 `service.ranking` 高於0。

在預設配置中，「頁面屬性」對話框提供了將頁面標籤為站點地圖根的選項，因此，如上所述，將生成其自身及其子體的站點地圖。 此行為由 `SitemapGenerator` 可通過添加替代實現來擴展介面。 但是，由於重新生成XML站點的頻率高度取決於內容創作工作流和工作負載，因此產品不會發運任何 `SitemapScheduler` 配置。 這樣，該功能就可以有效地選擇加入。

為了啟用生成XML模板的後台作業 `SitemapScheduler` 必須配置。 為此，請為PID建立OSGI配置 `org.apache.sling.sitemap.impl.SitemapScheduler`。 調度程式表達式 `0 0 0 * * ?` 可以用作起點，在午夜每天重新生成一次所有XMLsitemap。

![Apache Sling Sitemap — 計畫程式](assets/sling-sitemap-scheduler.png)

站點地圖生成作業可以在作者和發佈層實例上運行。 在大多數情況下，建議在發佈層實例上運行生成，因為只能在該處生成適當的規範URL（因為通常只在發佈層實例上存在Sling資源映射規則）。 但是，可以通過實現用於生成規範URL的外部化機制的自定義實現 [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html) 。 如果自定義實現能夠在作者層實例上生成站點地圖的規範URL，則 `SitemapScheduler` 可以為作者運行模式配置，並且XML sitemap生成工作負載可以分佈在作者服務群集的實例中。 在此方案中，在處理尚未發佈、已修改或僅對受限用戶組可見的內容時必須特別小心。

AEM Sites包含預設 `SitemapGenerator` 遍歷一樹頁以生成站點地圖。 它已預配置為僅輸出站點的規範URL和任何語言替代項（如果可用）。 如果需要，還可以將其配置為包括頁面的上次修改日期。 為此，啟用 _添加上次修改時間_ 選項 _AdobeAEMSEO — 頁面樹站點地圖生成器_ 配置並選擇 _上次修改的源_。 在發佈層上生成Sitemap時，建議使用 `cq:lastModified` 日期。

![AdobeAEMSEO — 頁面樹站點地圖生成器配置](assets/sling-sitemap-pagetreegenerator.png)

要限制站點地圖的內容，可在需要時實現以下服務介面：

* 這樣 [站點地圖頁面篩選器](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) 可實現為隱藏由AEM Sites特定站點地圖生成器生成的XML站點集中的頁面
* a [站點地圖產品篩選器](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) 或 [站點地圖類別篩選器](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) 可以實現從由XML生成的XML站點中篩選產品或類別 [商業整合框架](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html) 特定站點地圖生成器

如果預設實現不適用於特定的使用情形，或者如果擴展點不夠靈活，則自定義 `SitemapGenerator` 可實施以完全控制所生成站點地圖的內容。 以下示例說明如何利用預設實現的AEM Sites邏輯來執行此操作。 它使用 [資源樹站點地圖生成器](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) 作為遍歷頁面樹的起點：

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, etc
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

此外，為XML站點集實現的功能也可用於不同的使用情形，例如將規範連結或語言替代添加到頁面的首部。 請參閱 [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) 的子菜單。

### 為舊版 URL 建立 301 重新導向 {#creating-redirects-for-legacy-urls}

以新結構啟動網站時，務必在 Apache HTTP 伺服器中實作並測試 301 重新導向，理由有二：

* 舊版 URL 已累積一段時間的 SEO 值了。實作重新導向，搜尋引擎才可將此值套用至新 URL。
* 您的網站使用者可能已建立連向這些網頁的書籤了。實作重新導向，您才能確實將使用者導向新網站上與他們在嘗試進入舊網站時所前往位置最相符的網頁。

請務必參閱下方的其他資源章節，瞭解實作 301 重新導向的操作指示，並以工具測試重新導向是否如期運作。

## 其他資源 {#additional-resources}

如需詳細資訊，請參考下列其他資源：

* [資源映射](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
