---
title: SEO和URL管理最佳實務
seo-title: SEO和URL管理最佳實務
description: 瞭解SEO最佳實務和建議，以便在AEM實作上達成這些目標。
seo-description: 瞭解SEO最佳實務和建議，以便在AEM實作上達成這些目標。
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7

---


# SEO和URL管理最佳實務{#seo-and-url-management-best-practices}

搜尋引擎最佳化(SEO)已成為許多行銷人員最關心的問題。 因此，許多AEM專案都需要解決SEO問題。

本檔案首先說明在AEM實 [作上達成這些目標的一些](#seo-best-practices) SEO最佳實務和建議。 然後，本文檔將更深入探討第一節中提出的 [一些更複雜的實作](#aem-configurations) 步驟。

## SEO最佳實務 {#seo-best-practices}

本節說明一些一般的SEO最佳實務。

### URL {#urls}

在URL方面，有一些公認的最佳實務。

在您的AEM專案中，評估URL時，請自問：

「如果使用者要檢視此URL，而頁面上沒有任何內容，他們能否描述此頁面是什麼？」

如果答案為是，則URL很可能適用於搜尋引擎。

以下是有關如何建構SEO之URL的一般提示：

* 使用連字型大小來分隔字詞。

   * 使用連字型大小(-)作為分隔符來命名頁面。
   * 避免使用駝峰大小寫、底線和空格。

* 盡可能避免使用查詢參數。 如有需要，請限制為兩個或兩個以下。

   * 使用目錄結構來指示資訊體系結構（如果可用）。
   * 如果目錄結構不是選項，請在URL中使用Sling選擇器，而非查詢字串。 除了它們提供的SEO值外，sling選擇器也會讓頁面可供分派程式快取。

* URL的人性化程度越高越好；在URL中顯示關鍵字會大幅提升值。

   * 在頁面上使用選擇器時，偏好提供語義值的選擇器。
   * 如果人無法讀取您的URL，搜尋引擎也無法讀取。
   * 例如：
      `mybrand.com/products/product-detail.product-category.product-name.html`
優先於 `mybrand.com/products/product-detail.1234.html`

* 盡可能避免子網域，因為搜尋引擎會將子網域視為不同的實體，將網站的SEO值分割。

   * 請改用第一層子路徑。 例如，使用 `es.mybrand.com/home.html`代替 `www.mybrand.com/es/home.html`。

   * 根據本准則，規劃內容階層以符合內容呈現方式。

* URL中的關鍵字效能會隨著URL長度和關鍵字位置的增加而降低。 換句話說，較短就更好。

   * 使用URL縮短技術和AEM提供的功能來移除不必要的URL片段。
   * 例如， `mybrand.com/en/myPage.html` 優先於 `mybrand.com/content/my-brand/en/myPage.html`。

* 使用標準URL。

   * 當URL可從不同路徑或使用不同參數或選擇器提供時，請務必在頁面 `rel=canonical` 上使用標籤。

   * 這可納入AEM範本的程式碼中。

* 盡可能將URL與頁面標題相符。

   * 應鼓勵內容作者遵循此慣例。

* 支援URL要求不區分大小寫。

   * 將調度程式配置為將所有入站請求重寫為小寫字母。
   * 訓練內容作者使用小寫字母建立所有頁面。

* 請確定每個頁面都只從一個通訊協定提供。

   * 有時，網站會在使用者 `http` 進入頁面（例如結帳或登入表格）後，才可供其切換至 `https`。 當從此頁面連結時，如果使用者可返回頁面並 `http` 透過存取頁面，搜尋引擎 `https`會將這些頁面當成兩個獨立頁面來追蹤。

   * Google目前偏好頁 `https` 面而非 `http` 頁面。 因此，它通常讓每個人的生活更輕鬆，為整個網站服務 `https`。

### Server configuration {#server-configuration}

就伺服器組態而言，您可執行下列步驟，以確保只搜尋正確的內容：

* 使用文 `robots.txt` 件來阻止任何不應編製索引的內容的搜索。

   * 封鎖 **測試環境** 上的所有編目。

* 啟動具有更新URL的新網站時，請實作301重新導向，以確保您現有的SEO排名不會遺失。
* 加入您網站的首頁。
* 建置XML網站地圖，讓搜尋引擎更輕鬆地搜尋內容。 請確定包含行動及／或回應式網站的行動網站地圖。

## AEM Configurations {#aem-configurations}

本節說明設定AEM以遵循這些SEO建議所需的實施步驟。

### 使用Sling選擇器 {#using-sling-selectors}

以前，使用查詢參數是建立企業Web應用程式時普遍接受的做法。

近年來的趨勢是移除這些URL，讓URL更容易閱讀。 在許多平台上，這包括在網頁伺服器或內容傳送網路(CDN)上實作重新導向，但Sling讓這項作業變得簡單明瞭。 Sling選擇器：

* 改善URL可讀性。
* 讓您在調度器上快取頁面，通常會提高安全性。
* 允許您直接處理內容，而不是擁有檢索內容的通用servlet。 這將授予您應用到儲存庫的ACL和應用到調度程式的篩選器的好處。

#### 使用servlet的選擇器 {#using-selectors-for-servlets}

AEM為我們提供兩種編寫servlet的選項：

* **bin** servlet
* **Sling** servlets

下列範例說明如何註冊同時遵循這兩種模式的servlet，以及使用Sling servlet所獲益處。

#### Bin servlet（向下一級） {#bin-servlets-one-level-down}

**Bin** servlet遵循許多開發人員習慣於使用J2EE程式設計的模式。 Servlet會在特定路徑註冊，在AEM通常位於下方的情況下， `/bin`您會從查詢字串擷取所需的請求參數。

此類servlet的SCR注釋如下所示：

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

然後，通過方法中包含的對 `SlingHttpServletRequest` 像從查詢字串中提取參 `doGet` 數；例如：

```
String myParam = req.getParameter("myParam");
```

所使用的產生URL如下所示：

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

這種方法需要考慮以下幾點：

* URL本身會遺失SEO值。 存取網站（包括搜尋引擎）的使用者不會從URL收到任何語義值，因為URL代表程式化路徑，而非內容階層。
* URL中存在查詢參數意味著調度程式將無法快取響應。
* 如果要保護此servlet的安全，您需要在servlet中實施自己的自定義安全邏輯。
* 必須（小心）配置調度程式才能公開 `/bin/myApp/myServlet`。 僅僅公開 `/bin` 即可存取某些不應對網站訪客開放的servlet。

#### Sling servlets（向下一級） {#sling-servlets-one-level-down}

**Sling** servlets可讓您以相反的方式註冊您的servlet。 您不需要編址servlet並指定您希望servlet根據查詢參數呈現的內容，而是需要指定您想要的內容，並指定應根據Sling選擇器來呈現內容的servlet。

此類servlet的SCR注釋如下所示：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

在這種情況下，URL地址（資源的實例）在Servlet中 `myPageType` 可自動訪問的資源。 若要存取，請致電：

```
Resource myPage = req.getResource();
```

所使用的產生URL如下所示：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

此方法的優點包括：

* 您可以將SEO值加入網站階層和頁面名稱中所呈現的語義。
* 由於沒有查詢參數，因此調度程式可以快取響應。 此外，對已定址頁面進行的任何更新會在頁面被激活時使此快取失效。
* 當用戶嘗試訪 `/content/my-brand/my-page` 問此servlet時，應用到的所有ACL都將生效。
* 調度程式已配置為將此內容作為服務網站的函式。 不需要額外的設定。

### URL重寫 {#url-rewriting}

在AEM中，您的所有網頁都會儲存在下方 `/content/my-brand/my-content`。 雖然從資料庫資料管理的角度來看，這可能很有用，但並不一定是您希望客戶查看網站的方式，而且可能與SEO指引相衝突，以盡可能縮短URL。 此外，您可能是從相同的AEM例項和不同的網域名稱，為多個網站提供服務。

本節將檢視AEM中可用來管理這些URL的選項，並以更易讀和SEO友好的方式呈現給使用者。

#### 虛名URL {#vanity-urls}

如果作者想要從第二個位置存取頁面以用於促銷目的，AEM的虛名URL（逐頁定義）可能會很有用。 若要新增頁面的虛名URL，請在 **Sites** Console中導覽至該頁面，並編輯頁面屬性。 在「基本 **** 」索引標籤底部，您會看到可新增虛名URL的區段。 請記住，透過多個URL存取頁面會分割頁面的SEO值，因此應將標準URL標籤新增至頁面，以避免此問題。

#### 本地化頁面名稱 {#localized-page-names}

您可能想要向翻譯內容的使用者顯示本地化的頁面名稱。 例如：

* 而不是讓講西班牙語的使用者導覽至：
   `www.mydomain.com/es/home.html`

* URL最好：
   `www.mydomain.com/es/casa.html`.

AEM平台上許多可用的本地化工具都需要讓不同地區的頁面名稱相符，才能讓內容保持同步。

酒店 `sling:alias` 讓您擁有我們的蛋糕，也可以享用。 `sling:alias` 可以作為屬性添加到任何資源，以允許該資源的別名。 在上例中，您會有：

* JCR中的頁面：
   `…/es/home`

* 然後新增屬性至：
   `sling:alias` = `casa`

這可讓AEM轉譯工具（例如多網站管理員）繼續維持以下關係：

* `/en/home`

* `/es/home`

同時允許使用者以其原生語言與頁面名稱互動。

>[!NOTE]
>
>在編 `sling:alias` 輯頁面屬性時，可使用 [Alias屬性來設定屬性](/help/sites-authoring/editing-page-properties.md#advanced)。

#### /etc/map {#etc-map}

在標準AEM安裝中：

* 用於OSGi配置
   **Apache Sling Resource Resolver Factory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 屬性
   **對應位置** ( `resource.resolver.map.location`)

* defaults to `/etc/map`.

您可以在此位置新增對應定義，以對應傳入請求、重寫AEM中頁面上的URL，或兩者。

要建立新映射，請在或下的 `sling:Mapping` 此位置中建立新 `/http` 節點 `/https`。 AEM會根據 `sling:match` 此節點 `sling:internalRedirect` 上設定的和屬性，將符合的URL的所有流量重新導向至屬性中指定的 `internalRedirect` 值。

雖然這是官方AEM和Sling檔案中記錄的方法，但與直接使用的選項相比，此實作提供的規則運算式支援在範圍上有限 `SlingResourceResolver` 。 此外，以這種方式實施映射可能會導致發送程式快取失效的問題。

以下是此問題發生的範例：

1. 使用者瀏覽您的網站並提出要求 `https://www.mydomain.com/my-page.html`
1. 調度程式將此請求轉發到發佈伺服器。
1. 使用 `/etc/map`時，發佈伺服器會解析此請求， `/content/my-brand/my-page` 並轉譯頁面。

1. 調度程式在中快取響 `/my-page.html` 應，並將響應返回給用戶。
1. 內容作者會變更此頁面並加以啟動。
1. 調度器刷新代理髮送失效請求 `/content/my-brand/my-page`**。**由於調度程式在此路徑上沒有快取頁面，因此舊內容將保持快取並過時。

有些方法可設定自訂的分派清單規則，將較短的URL對應至較長的URL，以便快取失效。

不過，管理這個問題的方法也比較簡單：

1. **SlingResourceResolver規則**

   使用Web主控台（例如localhost:4502/system/console/configMgr），您可以設定Sling資源解析程式：

   * **Apache Sling Resource Resolver Factory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   建議您建立將URL縮短為規則運算式所需的映射，然後在您建立的OsgiConfignode下定義這 `config.publish`些設定。

   您不需在中定義您 `/etc/map`的映射，而是可以直接指派給屬性 **URL映射** ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在這個簡單範例中，您會從 `/content/my-brand/` 任何URL的開頭移除它。

   這會轉換URL:

   * 從 `/content/my-brand/my-page.html`
   * to just `/my-page.html`
   這符合建議的將URL盡量短的做法。

1. **對應頁面上的URL輸出**

   在Apache Sling Resource Resolver中定義映射後，您需要在元件中使用這些映射，以確保您在頁面上輸出的URL簡短且整齊。 您可以使用的map函式來完成此操作 `ResourceResolver`。

   例如，如果您實作的自訂導覽元件會列出目前頁面的子系，則可使用如下對應方法：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

目前，您已實作映射與元件中的邏輯，以便在將URL輸出至我們的頁面時使用這些映射。

拼圖的最後一塊，是當這些縮短的URL進入調度程式時，它們就會 `mod_rewrite` 在其中運作。 使用URL的最大優 `mod_rewrite` 點是，URL在傳送到調度器模 *塊之前* ，會映射回其長格式。 這表示分派器會從發佈伺服器要求長URL，並據以快取它。 因此，來自發佈伺服器的任何調度器清除請求都可以成功使此內容無效。

要實施這些規則，可以在 `RewriteRule` Apache HTTP server配置的虛擬主機下添加元素。 如果您想從前例展開縮短的URL，則可實作如下的規則：

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 標準URL標籤 {#canonical-url-tags}

標準URL標籤是置入HTML檔案標題的連結標籤，可釐清搜尋引擎在建立內容索引時應如何處理頁面。 他們提供的好處是，即使頁面的URL可能包含差異，也能確保（不同版本的）頁面的索引相同。

例如，如果網站要提供適合印表機的頁面版本，搜尋引擎可能會將此頁面與一般頁面版本分開建立索引。 標準標籤會告訴搜尋引擎它們是相同的。

範例：

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

兩者都會將下列標籤套用至頁面的標題：

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

可以 `href` 是相對的或絕對的。 程式碼應包含在頁面標籤中，以判斷頁面的標準URL並輸出此標籤。

### 配置分發程式以區分大小寫 {#configuring-the-dispatcher-for-case-insensitivity}

最佳實務是使用小寫字母來支援所有頁面。 但是，當使用者使用其URL中的大寫字母存取您的網站時，您不希望使用者取得404。 因此，Adobe建議您在Apache HTTP Server設定中新增重寫規則，將所有傳入的URL對應至小寫。 此外，內容作者必須接受訓練，才能建立其小寫名稱的頁面。

要配置Apache以強制所有入站通信量使用小寫，請將以下內容添加到配 `vhost` 置中：

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

此外，將下列項目新增至檔案的最上 `htaccess` 方：

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 實作robots.txt以保護開發環境 {#implementing-robots-txt-to-protect-development-environments}

搜尋引 *擎* ，在搜尋您的網站 `robots.txt` 之前，應先檢查您網站根目錄中是否有檔案。 這裡應該強調，因為雖然Google、Yahoo或Bing等主要搜尋引擎都尊重這一點，但有些外國搜尋引擎卻不尊重。

封鎖對整個網站的存取最簡單的方式，是將名為根網站的檔 `robots.txt` 案置於下列內容：

```xml
User-agent: *
Disallow: /
```

或者，在即時環境中，您可以選擇不允許某些不希望建立索引的路徑。

將檔案置於網站根 `robots.txt` 目錄時的注意事項是，分派程式清除請求可能會清除此檔案，而URL映射可能會將網站根目錄置於與Apache HTTP Server設定中所定義的 `DOCROOT` 不同之處。 因此，通常將此檔案放置在作者例項的根目錄上，並複製到發佈例項。

### 在AEM上建立XML網站地圖 {#building-an-xml-sitemap-on-aem}

Crawler使用XML網站地圖，以更好地瞭解網站的結構。 雖然無法保證提供網站地圖可改善SEO排名，但這是一項經商同意的最佳實務。 您可以手動維護網站伺服器上的XML檔案以用作網站地圖，但建議以程式設計方式產生網站地圖，以確保當作者建立新內容時，網站地圖會自動反映其變更。

若要以程式設計方式產生sitemap，請註冊Sling Servlet監聽呼 `sitemap.xml` 叫。 然後，Servlet可以使用通過servlet API提供的資源查看當前頁及其子頁，輸出XML。 然後，XML將在調度程式中快取。 此位置應在檔案的sitemap屬性中引 `robots.txt` 用。 此外，需要實作自訂的清除規則，以確保每當啟動新頁面時，都能清除此檔案。

>[!NOTE]
>
>您可以註冊Sling Servlet，以監聽具有副檔名 `sitemap` 的選取器 `xml`。 這將導致Servlet在任何請求URL時處理請求，該URL會結束於：
>    `/<path-to>/page.sitemap.xml`
然後，您就可以從請求中取得請求的資源，並使用JCR API從內容樹中的該點產生網站地圖。
這樣做的好處是，當您有多個網站從同一個實例中提供服務時。 請求將產 `/content/siteA.sitemap.xml` 生網站地圖，而請 `siteA` 求將產生網站地圖，而不需 `/content/siteB.sitemap.xml``siteB` 要編寫其他程式碼。

### 建立舊版URL的301重新導向 {#creating-redirects-for-legacy-urls}

在以新結構啟動網站時，在Apache HTTP server中實作和測試301重新導向很重要，原因有二：

* 舊版URL已累積了一段時間的SEO值。 透過實作重新導向，搜尋引擎可將此值套用至新URL。
* 您網站的使用者可能已建立這些頁面的書籤。 透過實作重新導向，您可以確定將使用者導向新網站上最符合他們嘗試在舊網站上瀏覽位置的頁面。

請務必檢查後面的其他資源區段，以取得實作301重新導向的指示，以及測試重新導向是否如預期般運作的工具。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱下列其他資源：

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

