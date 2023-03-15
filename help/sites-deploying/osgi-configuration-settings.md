---
title: OSGi組態設定
seo-title: OSGi Configuration Settings
description: 本文詳細說明與專案實作相關的OSGi組態設定（依套件組合列出）。 清單可作為指引，並非詳盡無遺。
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: 73fba5249a05b0bdb9871a6e19c6bed10a7e7e4b
workflow-type: tm+mt
source-wordcount: '3476'
ht-degree: 0%

---

# OSGi組態設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 是AEM技術堆疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

OSGi &quot;*提供標準化基元，允許從小型、可重複使用和協作的元件構建應用程式。 這些元件可組成應用程式並部署*」。

這樣可以輕鬆管理捆綁包，因為它們可以單獨停止、安裝和啟動。 會自動處理互依性。 每個OSGi元件(請參閱 [OSGi規範](https://www.osgi.org/Specifications/HomePage))包含在其中一個不同套件組合中。 使用AEM時，有數種方法可管理這類套件組合的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

下列OSGi組態設定（根據套件組合列出）與專案實作相關。 並非所有列出的設定都需要調整，有些設定可協助您了解AEM的運作方式。

>[!CAUTION]
>
>清單旨在作為指引，並非詳盡無遺。 並非所有套件組合都列出，某些套件組合的所有參數也未列出。
>
>所需的設定因專案而異。
>
>請參閱Web主控台，以取得所用值和參數的詳細資訊。

>[!NOTE]
>
>OSGi配置差異工具， [AEM工具](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)，可用來列出預設OSGi設定。

>[!NOTE]
>
>特定功能區域在AEM中可能需要進一步的套件組合。 在這些情況下，可在與適當功能相關的頁面上找到設定詳細資料。

**AEM復寫事件接聽程式** 配置：

* 此 **執行模式**，複製事件將分發給偵聽器。 例如，如果定義為作者，則此系統將「啟動」復寫。

* 執行模式 **發佈** 如果專案程式碼在發佈環境中處理復寫事件（反向復寫），則需要新增。 例如，當使用Dispatcher排清發佈環境，或發生標準復寫至其他發佈例項時。

**AEM Repository更改偵聽器** 配置：

* 此 **路徑**，監聽存放庫事件以供分發的位置。

**CRX Sling用戶端存放庫** 配置對基礎內容儲存庫的訪問。

* 此 **管理員密碼** 安裝後應進行變更，以確保 [安全](/help/sites-administering/security-checklist.md) 例項。
* 其他變更則不必執行，且必須謹慎處理，因為這些變更可能會影響存放庫的存取權。

**Apache Felix OSGi Management Console** 配置：

* **外掛程式**，主要導覽項目（主控台外掛程式）可在 **Apache Felix Web Management Console** 作為頂級菜單項。 停用您不需要的任何項目，因為每個項目都需要空間和資源。

>[!CAUTION]
>
>請務必設定下列項目：
>
>**使用者名稱** 和 **密碼**，此為存取Apache Felix Web Management Console本身的憑證。
>密碼必須在初始安裝後更改，以確保 [安全](/help/sites-administering/security-checklist.md) 例項。

>[!NOTE]
>
>啟動時需使用Felix Console才能進行此設定，存放庫才可使用。

**Apache Sling Customized Request Data Logger** 配置：

* **記錄器名稱** 和 **記錄格式** 設定請求和存取記錄的位置和格式(預設值： `request.log`)。 分析與Web鏈相關的效能或調試功能時，此日誌檔案是必不可少的。
這已與 [Apache Sling Request Logger](#apacheslingrequestlogger).

如需詳細資訊，請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/site/logging.html).

**Apache Sling事件線程池** 配置：

* **最小池大小** 和 **最大池大小**，用於保存事件線程的池的大小。

* **隊列大小**，如果池已用盡，則線程隊列的最大大小。
建議的值為 `-1` 因為這把隊列設定為「無限」；如果設定了限制，則超過限制時可能會發生損失。

* 變更這些設定有助於在發生大量事件的情況下執行；例如，大量使用AEM DAM或工作流程。
* 應使用測試來建立藍本的特定值。
* 這些設定可能會影響執行個體的效能，因此請勿無故變更，並給予適當考量。

**Apache SlingGETServlet** 設定轉譯的某些方面：

* **自動索引** 啟用/禁用瀏覽的目錄呈現。
* **啟用** （或停用）預設轉譯，例如 **HTML**, **純文字**, **JSON** 或 **XML**.
您不應停用JSON。

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Apache Sling Java指令碼處理常式** 配置.java檔案編譯為指令碼(servlet)的設定。

某些設定可能會影響效能，應盡可能停用這些設定，尤其是生產執行個體。

* **源VM** 和 **目標VM**，請將JDK版本定義為執行階段JVM

* 針對生產執行個體：

   * disable **產生除錯資訊**

**Apache Sling JCR安裝程式** 這些參數可能不需要設定，但在開發或除錯時可能有助於了解。 例如，安裝資料夾對於簽入/簽出或建立包很有用。

* **安裝資料夾名稱regexp** 和 **安裝資料夾的最大層次結構深度**  — 指定在何處和到哪個深度搜索儲存庫資料夾以查找要安裝的資源。 使用萬用字元時(如中。&#42;/install)會搜尋所有適當的相符項目，例如 `/libs/sling/install` 和 `/libs/cq/core/install`.

* **搜尋路徑**, jcrinstall會搜尋要安裝的資源的路徑清單，以及表示該路徑之加權因數的數字。

**Apache Sling作業事件處理常式** 配置管理作業調度的參數：

* **重試間隔**, **最大重試次數**, **最大並行作業數**, **確認等待時間**，其中包括。

* 更改這些設定可以改善大量作業的情況下的效能；例如，大量使用AEM DAM和工作流程。
* 應使用測試來建立藍本的特定值。
* 請勿無故變更這些設定，僅在適當考慮後變更。

**Apache Sling JSP指令碼處理常式** 為JSP指令碼處理程式配置與效能相關的設定。 要提高效能，應盡可能禁用。

尤其適用於生產執行個體：

* disable **產生除錯資訊**
* disable **保留生成的Java**
* disable **對應內容**
* disable **顯示來源片段**

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Apache Sling記錄設定** 配置：

* **記錄層級** 和 **記錄檔**，定義中央記錄設定的位置和記錄層級(error.log)。 該級別可設定為 `DEBUG`, `INFO`, `WARN`, `ERROR` 和 `FATAL`.

* **日誌檔案數** 和 **記錄檔臨界值** 定義日誌檔案的大小和版本旋轉。

* **訊息模式** 定義日誌消息的格式。

如需詳細資訊，請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md#global-logging) 和 [Sling記錄](https://sling.apache.org/site/logging.html).

**Apache Sling Logging Logger Configuration(Factory Configuration)** 配置：

* **記錄層級**, **記錄檔** 和 **訊息格式** 定義日誌檔案和消息的詳細資訊。

* **記錄器** 定義類別；例如，僅記錄com.day.cq。

* 使用 **工廠配置**，可以新增任何數量的其他設定，以符合所需的各種記錄層級和類別。
* 這類設定在開發期間很有幫助；例如，在特定日誌檔案中記錄特定服務的TRACE消息。
* 這類設定在生產環境中很有用；例如，將特定服務的相關訊息記錄到個別記錄檔中，以便更輕鬆進行監控。

如需詳細資訊，請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/site/logging.html).

**Apache Sling記錄撰寫器設定（工廠設定）** 配置：

* **記錄檔** 定義日誌檔案的存在。
* **日誌檔案數** 來定義版本旋轉。

* 此寫入器可由 **Apache Sling Logging Logger Configuration** 設定。

* 這類設定在開發期間很有幫助；例如，在特定日誌檔案中記錄特定服務的TRACE消息。
* 這類設定在生產環境中很有用；例如，將特定服務的相關訊息記錄到個別記錄檔中，以便更輕鬆進行監控。

如需詳細資訊，請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/site/logging.html).

**Apache Sling主要Servlet** 配置：

* **每個請求的呼叫數** 和 **遞歸深度** 以保護您的系統，避免無限遞回和過多的指令碼呼叫。

**Apache Sling MIME Type Service** 配置：

* **MIME類型** 將專案所需的項目新增至系統。 這可讓 `GET` 請求設定正確的內容類型標題，以連結檔案類型和應用程式。

**Apache Sling反向連結篩選器** 若要解決CRX WebDAV和Apache Sling中跨網站請求偽造(CSRF)的已知安全性問題，您需要設定反向連結篩選器。

反向連結篩選服務是OSGi服務，可讓您設定：

* 應篩選哪些http方法
* 是否允許空的反向連結標題
* 以及除伺服器主機外允許的伺服器清單。

請參閱 [安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 以取得詳細資訊。

>[!NOTE]
>
>Apache Sling Referrer Filter取決於快速修正套件的安裝。

**Apache Sling Request Logger** 配置：

* 定義要求記錄方式的各種參數。
* **啟用請求日誌**，以啟用或停用。

* **啟用訪問日誌**，以啟用或停用。

這已與 [Apache Sling Customized Request Data Logger](#apacheslingcustomizablerequestdatalogger).

如需詳細資訊，請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver Factory** 設定Sling資源解決的中心層面：

* **資源搜索路徑**(s)，新增任何專案特定路徑(但不會移除 `/libs` 或 `/apps`)。

* **虛擬URL** 定義虛名URL對應。

* **URL對應** 定義任何別名；例如，從 `/content` to `/`.

* **映射位置**，中外部化的映射器設定 `/etc/map`.

* 使用本機安裝(例如，使用 `https://localhost:4502/system/console/jcrresolver`)，以判斷哪個資源解析器作用中。

如需詳細資訊，請參閱： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>尤其是必須在存放庫中設定這些選項。
>
>否則，對 **URL對應** 使用Felix主控台時，AEM可能會在下次啟動時覆寫。

**Apache Sling Servlet/指令碼解析器和錯誤處理常式** Sling Servlet和指令碼解析器有多項工作：

1. 它會作為 `ServletResolver` ，選擇要調用以處理請求的Servlet或指令碼。

1. 其作用為 `SlingScriptResolver`.

1. 它可透過實作 `ErrorHandler` 介面使用相同的演算法來選取錯誤處理servlet和指令碼，如同用來解析請求處理servlet和指令碼一樣。

可設定各種參數，包括：

* **執行路徑** 列出了搜索可執行指令碼的路徑；透過設定特定路徑，您可以限制可執行的指令碼。 如果未配置任何路徑，則使用預設值( `/` =root)，則可執行所有指令碼。
如果配置的路徑值以斜線結尾，則搜索整個子樹。 若沒有這類尾隨斜線，則只有在指令碼完全相符時，才會執行指令碼。

* **指令碼用戶**  — 此可選屬性可指定用於讀取指令碼的儲存庫用戶帳戶。 如果未指定帳戶，則 `admin` 預設會使用使用者。

* **預設擴充功能** 將使用預設行為的擴充功能清單。 這表示資源類型的最後一個路徑區段可作為指令碼名稱使用。

**Apache HTTP元件代理配置** 使用Apache HTTP用戶端，在進行HTTP時使用的所有程式碼的代理設定；例如在復寫時。

建立新配置時，請勿更改工廠配置，而是使用此處提供的配置管理器為此元件建立新的工廠配置： **https://localhost:4502/system/console/configMgr/**. 代理配置可在 **org.apache.http.proxyconfigurator。**

>[!NOTE]
>
>在AEM 6.0及舊版中，Proxy是在Day Commons HTTP Client中設定。 自AEM 6.1和更新版本起，Proxy設定已移至「Apache HTTP元件Proxy設定」，而非「Day Commons HTTP Client」設定。

**Day CQ反垃圾郵件** 設定使用的反垃圾郵件服務(Akismet)。 這需要您註冊：

* **提供者**
* **API金鑰**
* **註冊URL**

**AdobeGraniteHTML程式庫管理員** 設定此項以控制用戶端程式庫（css或js）的處理；包括如何看見基礎結構。

* 針對生產執行個體：

   * 啟用 **Minify** （移除CRLF和空格字元）。
   * 啟用 **Gzip** （允許使用一個請求對檔案進行gzippe和訪問）。
   * disable **除錯**
   * disable **計時**

* 針對JS開發（尤其是進行除錯/除錯時）:

   * disable **Minify**
   * 啟用 **除錯** 區隔檔案以進行除錯，並與firebug搭配使用。
   * 啟用 **計時** 就是對時間感興趣。
   * 啟用 **除錯** 主控台，查看JS主控台記錄訊息。

>[!CAUTION]
>
>變更 **Minify** 或 **Gzip** 您也需要刪除clientlibs快取的內容。 請參閱 [知識庫文章](https://helpx.adobe.com/ca/experience-manager/kb/How-to-force-a-recompilation-of-all-Sling-scripts-jsps-java-sightly-on-AEM-6-4.html) 以取得詳細資訊。

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Day CQ HTTP標題驗證處理常式** HTTP要求的基本驗證方法的系統範圍設定。

使用時 [關閉的使用者群組](/help/sites-administering/cug.md) 您可以設定（其中包括）:

* **HTTP領域**
* 此 **預設登入頁面**

**日CQ連結檢查程式服務** 檢查並視需要進行設定：

* **排程器期間** 定義要自動檢查外部連結的間隔。

* 檢查 **鏈路容差間隔錯誤** 在此期間，失敗的外部連結會被視為錯誤。
* **連結檢查覆蓋模式**，定義要從連結檢查中排除的任何路徑。

**日CQ連結檢查程式任務** 配置單個連結檢查程式任務（檢查外部連結的任務）的設定：

* 檢查中定義的間隔 **良好的連結測試間隔** 和 **鏈路測試間隔錯誤**

* 檢查連結時外部訪問所需的與Internet訪問代理和NTLM相關的各種參數。

**Day CQ Mail Service** 配置郵件伺服器的主機名和訪問詳細資訊。 請參閱設定郵件服務一節。

**Day CQ MCM電子報** 配置電子報使用的各種設定。

**日CQ根對應** 配置：

* **目標路徑** 定義請求「 `/`」。

AEM中有兩個可用的UI:

* 觸控式UI是標準UI
* 已棄用的傳統UI仍可完全運作

使用AEM根對應，您可以設定要用來作為執行個體預設的UI:

* 若要將啟用觸控的UI設為預設UI，請 **目標路徑** 應指向：

   ```shell
      /projects.html
   ```

* 若要將傳統UI設為預設UI，請 **目標路徑** 應指向：

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>在標準安裝時，觸控最佳化UI為預設UI。

**AdobeGranite SSO驗證處理常式** 配置單一登錄(SSO)詳細資訊；企業作者設定中通常需要這些項目，通常與LDAP搭配使用。

提供各種配置屬性：

* **路徑**
此身份驗證處理程式處於活動狀態的路徑。 如果此參數留空，則會停用驗證處理常式。 例如，路徑/會使驗證處理常式用於整個存放庫。

* **服務排名**
OSGi Framework服務排名值用於指示用於調用此服務的順序。 這是 
`int` 值中值越高，優先順序越高。
預設值為 `0`.

* **標題名稱**
可能包含使用者ID之標題的名稱。

* **Cookie名稱**
可能包含使用者ID之Cookie的名稱。

* **參數名稱**
可能提供使用者ID之請求參數的名稱。

* **使用者對應**
對於選取的使用者，從HTTP要求擷取的使用者名稱可以取代為憑證物件中的不同名稱。 此處定義對應。 如果使用者名稱 
`admin` 會顯示在地圖的兩側，而會忽略對應。 請注意，字元&quot;=&quot;必須以前導的&quot;\&quot;逸出。

* **格式**
指出提供使用者ID的格式。 使用:

   * `Basic` 如果使用HTTP基本驗證格式來編碼使用者ID
   * `AsIs` 如果使用者ID是以純文字提供，或應以原樣或任何規則運算式使用套用的值

**Day CQ WCM除錯篩選器** 在開發時，這個用法很有用，因為它允許在存取頁面時使用尾碼，例如？debug=layout。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout將提供開發人員可能感興趣的版面資訊。

* 在生產執行個體上停用此功能以確保效能和安全性。

**Day CQ WCM篩選器** 配置：

* **WCM模式**以定義預設模式。
* 在製作例項上，這可能 `edit`, `disable,preview` 或 `analytics`.
其他模式可從sidekick或尾碼存取 `?wcmmode=disabled` 可用來模擬生產環境。

* 在發佈例項上，此值必須設為 `disabled` 以確保無法存取其他模式。

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Day CQ WCM連結檢查程式設定器** 配置：

* **重寫配置清單** ，指定基於內容的連結檢查程式配置的位置清單。 配置可以基於運行模式；這對於區分製作環境和發佈環境很重要，因為linkchecker設定可能不同。

**Day CQ WCM頁面管理器工廠** 配置：

* **頁面子樹狀結構啟動檢查** （沒有復寫權限）來刪除或移動頁面（即使頁面未啟動）。

**Day CQ WCM頁面處理器** 配置：

* **路徑**，系統會在觸發前監聽頁面修改的位置清單 `jcr:Event`.

**Adobe頁面曝光次數追蹤器** 針對製作例項進行設定：

* **sling.auth.requirements**:將此屬性的值設定為 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此設定將允許匿名請求至追蹤服務。

>[!NOTE]
>
>請參閱 [頁面曝光數](/help/sites-deploying/configuring.md#enabling-page-impressions) 以取得更多資訊。

**Day CQ WCM頁面統計資料** 發佈例項設定：

* **要傳送資料的URL** 設定用來追蹤頁面統計資料的URL（如果追蹤器請求經過dispatcher，則此為重要）;例如，預設為 `https://localhost:4502/libs/wcm/stats/tracker`.

* **已啟用追蹤指令碼** 啟用( `true`)或禁用( `false`)將追蹤指令碼納入頁面中。 預設值為 `false`。

>[!NOTE]
>
>請參閱 [頁面曝光數](/help/sites-deploying/configuring.md#enabling-page-impressions) 以取得更多資訊。

**Day CQ WCM Version Manager** 控制是否在您的系統中管理版本以及如何管理版本：

* **在啟動時建立版本**，在標準安裝中啟用
* **啟用清除**

* **清除路徑**，則搜尋動作將搜尋的路徑
* **隱式版本設定路徑**，隱式版本設定作用中的路徑。

* **最大版本年齡**，版本的最大年齡（以天為單位）

* **最大數量版本**，要保留的版本數上限

請參閱 [版本清除](/help/sites-deploying/version-purging.md) 以取得更多資訊。

**Day CQ工作流程電子郵件通知服務** 配置由工作流發送通知的電子郵件設定。

**CQ重寫器HTML解析器工廠**

控制CQ重寫器的HTML剖析器。

* **要處理的其他標籤**  — 您可以新增或移除要由剖析器處理的HTML標籤。 依預設，會處理下列標籤：A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD。
* **保留駝峰大小寫**  — 依預設，HTML剖析器會將駝峰式大小寫（例如eBay）的屬性轉換為小寫式（例如eBay）。 您可以關閉此選項以保留駝峰大小寫屬性。 這在使用前端架構(例如Angular2)時相當實用。

**Day Commons JDBC連接池** 配置對用作內容源的外部資料庫的訪問。

這是工廠配置，因此可以配置多個實例。

**CDN重寫器** 必須確保AEM與CDN之間的通訊，以安全的方式將資產/二進位檔傳送給使用者。 這包括兩項任務：

* 第一次（或快取中的過期後）透過CDN從AEM存取資源。
* 安全地存取CDN中快取的資源，因為在CDN中快取資源後，請求就不會傳至AEM，而所有可存取該資源的使用者都應從CDN提供服務。

AEM提供重新寫入程式，可將內部資產URL重新寫入外部CDN URL。 它會重寫要傳遞至CDN的連結，包括JWS簽章和過期時間，以便安全地存取資產。 此功能將用於製作執行個體。

整體流程如下：

1. 使用者向AEM驗證，並使用資產要求頁面。
1. 請求的頁面包含類似 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 重寫程式會將連結轉換為包含JWS簽名的CDN URL:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然後，使用者的瀏覽器會將資產請求轉送至CDN伺服器
1. CDN應已設定成將請求連同 `cdn_sign` 參數。
1. 驗證處理常式會驗證 `cdn_sign` 參數並將資產傳回至CDN，然後再傳送給使用者

使用者瀏覽器、CDN和AEM之間的流量可視化如下。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能目前僅針對AEM製作例項啟用。

**CDNConfigServiceImpl** 提供CDN設定

CDN重寫功能可借由提供 **CDN分發域名** 在com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的配置中。

此服務也包含其他設定選項，例如啟用/停用CDN重新寫入、執行CDN重新寫入的路徑前置詞、TTL值，以及通訊協定（HTTP或HTTPS）。

**CDNRewriter** 將內部影像URL重新寫入CDN URL的重寫器

此 **標籤屬性** com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的值可以定義，以便僅重寫選擇性影像連結。
