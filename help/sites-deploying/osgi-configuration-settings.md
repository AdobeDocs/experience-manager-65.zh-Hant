---
title: OSGi組態設定
seo-title: OSGi組態設定
description: 本文詳細說明與專案實作相關的OSGi組態設定（依套件組合列出）。 清單可作為指引，並非詳盡無遺。
seo-description: 本文詳細說明與專案實作相關的OSGi組態設定（依套件組合列出）。 清單可作為指引，並非詳盡無遺。
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: 設定
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: ca66c0655bcd878644e275fc8f7a41b38110beae
workflow-type: tm+mt
source-wordcount: '3561'
ht-degree: 0%

---

# OSGi配置設定{#osgi-configuration-settings}

[](https://www.osgi.org/) OSG是AEM技術堆疊中的基本元素。它可用來控制AEM的複合套件組合及其設定。

OSGi &quot;*提供了標準化的基元，這些基元允許從小型、可重複使用和協作的元件構建應用程式。 這些元件可以組成應用程式並部署*&quot;。

這樣可以輕鬆管理捆綁包，因為它們可以單獨停止、安裝和啟動。 會自動處理互依性。 每個OSGi元件（請參閱[OSGi規範](https://www.osgi.org/Specifications/HomePage)）都包含在各種套件中。 使用AEM時，有數種方法可管理這類套件組合的組態設定；如需詳細資訊和建議實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。

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
>OSGi配置差異工具是[AEM工具](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)的一部分，可用於列出預設OSGi配置。

>[!NOTE]
>
>特定功能區域在AEM中可能需要進一步的套件組合。 在這些情況下，可在與適當功能相關的頁面上找到設定詳細資料。

**AEM複製事件監** 聽程式配置：

* **運行模式**，將在其中將複製事件分發給偵聽器。 例如，如果定義為作者，則此系統將「啟動」復寫。

* 如果專案程式碼在發佈環境中處理復寫事件（反向復寫），則需要新增執行模式&#x200B;**publish**。 例如，當使用Dispatcher排清發佈環境，或發生標準復寫至其他發佈例項時。

**AEM Repository更改監** 聽程式配置：

* **路徑**，要監聽可供分發的儲存庫事件的位置。

**CRX Sling用戶端存** 放庫設定基礎內容存放庫的存取權。

* 安裝後應變更&#x200B;**管理密碼**，以確保執行個體的[安全性](/help/sites-administering/security-checklist.md)。
* 其他變更則不必執行，且必須謹慎處理，因為這些變更可能會影響存放庫的存取權。

**Wiki郵件服** 務配置由Wiki發送的電子郵件的電子郵件設定。

**Apache Felix OSGi Management** Console設定：

* **外掛程式**，主要導覽項目（主控台外掛程式）可在Apache Felix Web Management主控台 **的頂層** 功能表項目中取得。停用您不需要的任何項目，因為每個項目都需要空間和資源。

>[!CAUTION]
>
>請務必設定下列項目：
>
>**使** 用者 **名稱和密碼**，此為存取Apache Felix Web Management Console本身的憑證。
>初始安裝後必須更改密碼，以確保實例的[security](/help/sites-administering/security-checklist.md)。

>[!NOTE]
>
>啟動時需使用Felix Console才能進行此設定，存放庫才可使用。

**Apache Sling可自訂請求資料記** 錄器配置：

* **記錄** 器名 **稱** 和記錄格式，以設定請求和存取記錄的位置和格式(預設值： `request.log`)。分析與Web鏈相關的效能或調試功能時，此日誌檔案是必不可少的。
這與[Apache Sling Request Logger](#apacheslingrequestlogger)成對。

如需詳細資訊，請參閱[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling事件線程池** 配置：

* **最小池** 大小 **和最大池大小**，用於保存事件線程的池的大小。

* **隊列大小**，即池耗盡時線程隊列的最大大小。建議的值為`-1`，因為這會將佇列設為「無限制」；如果設定了限制，則超過限制時可能會發生損失。

* 變更這些設定有助於在發生大量事件的情況下執行；例如，大量使用AEM DAM或工作流程。
* 應使用測試來建立藍本的特定值。
* 這些設定可能會影響執行個體的效能，因此請勿無故變更，並給予適當考量。

**Apache SlingGET** Servlet設定轉譯的某些方面：

* **自動** 索引，啟用/停用瀏覽的目錄呈現。
* **啟用** （或停用）預設轉譯，例如 **HMTL**、 **純文字**、 **** JSON **或XML**。您不應停用JSON。

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中運行AEM，則會自動為生產實例配置此設定。

**Apache Sling Java Script處** 理常式配置.java檔案編譯為指令碼(servlet)的設定。

某些設定可能會影響效能，應盡可能停用這些設定，尤其是生產執行個體。

* S **源VM**&#x200B;和&#x200B;**目標VM**，將JDK版本定義為用作運行時JVM的版本

* 針對生產執行個體：

   * 禁用&#x200B;**生成調試資訊**

**Apache Sling JCR安** 裝程式這些參數可能不需要設定，但在開發或除錯時，這些參數很實用。例如，安裝資料夾對於簽入/簽出或建立包很有用。

* **安裝資料夾** 名稱重 **新展開安裝資料夾的最大層次結構深度**  — 指定在何處和到哪個深度搜索儲存庫資料夾以查找要安裝的資源。使用萬用字元時(如中。*/install)會搜尋所有適當的相符項目，例如`/libs/sling/install`和`/libs/cq/core/install`。

* **搜尋路徑**,jcrinstall會搜尋要安裝的資源的路徑清單，以及表示該路徑之加權系數的數字。

**Apache Sling Job Event Handler** 配置管理作業調度的參數：

* **重試間隔**、 **最大重試次數**、 **最大並行作業**、 **確認等待時間**&#x200B;等。

* 更改這些設定可以改善大量作業的情況下的效能；例如，大量使用AEM DAM和工作流程。
* 應使用測試來建立藍本的特定值。
* 請勿無故變更這些設定，僅在適當考慮後變更。

**Apache Sling JSP指令碼處** 理程式配置JSP指令碼處理程式的效能相關設定。要提高效能，應盡可能禁用。

尤其適用於生產執行個體：

* 禁用&#x200B;**生成調試資訊**
* 禁用&#x200B;**保留生成的Java**
* 禁用&#x200B;**映射內容**
* 禁用&#x200B;**顯示源片段**

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中運行AEM，則會自動為生產實例配置此設定。

**Apache Sling記錄** 設定：

* **記** 錄層 **級記錄檔**，以定義中央記錄設定(error.log)的位置和記錄層級。該級別可設定為`DEBUG`、`INFO`、`WARN`、`ERROR`和`FATAL`之一。

* **「日誌檔** 案數」和 **「日** 志檔案閾值數」，用於定義日誌檔案的大小和版本旋轉。

* **消** 息模式定義日誌消息的格式。

如需詳細資訊，請參閱[AEM Logging](/help/sites-deploying/configure-logging.md#global-logging)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Logging Logger Configuration(Factory Configuration)** Configure:

* **日誌級別**、日 **志檔** 案和 **消息** 格式以定義日誌檔案和消息的詳細資訊。

* **** 記錄以定義類別；例如，僅記錄com.day.cq。

* 通過使用&#x200B;**工廠配置**，可以添加任意數量的附加配置，以滿足所需的各種日誌級別和類別。
* 這類設定在開發期間很有幫助；例如，在特定日誌檔案中記錄特定服務的TRACE消息。
* 這類設定在生產環境中很有用；例如，將特定服務的相關訊息記錄到個別記錄檔中，以便更輕鬆進行監控。

如需詳細資訊，請參閱[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling記錄撰寫器設定（工廠設定）** 設定：

* **日** 志檔案，定義日誌檔案的存在。
* **要定義版本** 旋轉的日誌檔案數。

* 該寫入程式可由&#x200B;**Apache Sling Logging Logger Configuration**&#x200B;配置使用。

* 這類設定在開發期間很有幫助；例如，在特定日誌檔案中記錄特定服務的TRACE消息。
* 這類設定在生產環境中很有用；例如，將特定服務的相關訊息記錄到個別記錄檔中，以便更輕鬆進行監控。

如需詳細資訊，請參閱[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling主要** ServletConfigure:

* **每個請求和遞** 回的調 **用數** ，可保護您的系統免受無限遞回和過多指令碼調用的影響。

**Apache Sling MIME Type** ServiceConfigure:

* **MIME** 類型，用於將項目所需的類型添加到系統。這允許檔案上的`GET`請求設定用於連結檔案類型和應用程式的正確內容類型標頭。

**Apache Sling Referrer** Filter解決CRX WebDAV和Apache Sling中跨網站請求偽造(CSRF)的已知安全性問題，您需要設定Referrer篩選器。

反向連結篩選服務是OSGi服務，可讓您設定：

* 應篩選哪些http方法
* 是否允許空的反向連結標題
* 以及除伺服器主機外允許的伺服器清單。

如需詳細資訊，請參閱[安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 。

>[!NOTE]
>
>Apache Sling Referrer Filter取決於快速修正套件的安裝。

**Apache Sling Request** LoggerConfigure:

* 定義要求記錄方式的各種參數。
* **啟用「請求記錄**」，以啟用或停用。

* **啟用訪問日誌**，以啟用或禁用。

這會與[Apache Sling Customided Request Data Logger](#apacheslingcustomizablerequestdatalogger)成對。

如需詳細資訊，請參閱[AEM Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Resource Resolver Factory** 設定Sling資源解析的中心環節：

* **資源搜尋路徑**，新增任何專案特定路徑(但不移除 `/libs` 或 `/apps`)。

* **虛擬** URL可定義虛名URL對應。

* **定義** 任何別名的URL映射；例如從到 `/content` 的 `/`。

* **對應位置**，中外部化的對應程式設 `/etc/map`定。

* 使用本機安裝（例如，使用`https://localhost:4502/system/console/jcrresolver`）來判斷哪個資源解析器處於活動狀態。

如需詳細資訊，請參閱：[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)。

>[!CAUTION]
>
>尤其是必須在存放庫中設定這些選項。
>
>否則，使用Felix控制台對&#x200B;**URL對應**&#x200B;所做的變更，可能會在下次啟動時由AEM覆寫。

**Apache Sling Servlet/Script解析程式和錯誤處** 理程式Sling Servlet和指令碼解析程式有多項工作：

1. 它可作為`ServletResolver`來選取要呼叫以處理請求的Servlet或指令碼。

1. 其作用為`SlingScriptResolver`。

1. 它透過使用相同演算法實作`ErrorHandler`介面來管理錯誤處理，以選取錯誤處理servlet和指令碼，如同用來解析請求處理servlet和指令碼。

可設定各種參數，包括：

* **執行** 路徑會滑動路徑，以搜尋可執行指令碼；透過設定特定路徑，您可以限制可執行的指令碼。如果未配置任何路徑，則使用預設值(`/` = root)，這允許執行所有指令碼。
如果配置的路徑值以斜線結尾，則搜索整個子樹。 若沒有這類尾隨斜線，則只有在指令碼完全相符時，才會執行指令碼。

* **指令碼用戶**  — 此可選屬性可指定用於讀取指令碼的儲存庫用戶帳戶。如果未指定任何帳戶，則預設使用`admin`用戶。

* **預** 設擴充功能將使用預設行為的擴充功能清單。這表示資源類型的最後一個路徑區段可作為指令碼名稱使用。

**Day Commons GFX字型幫** 助程式在呈現圖形時，可以使用DrawText嵌入文本。為此，您也可以安裝您自己的字型：

* 定義要搜索項目特定字型的&#x200B;**字型路徑**。
例如， `/apps/myapp/fonts`。

**使用Apache HTTP** 用戶端的所有代碼的Apache HTTP元件Proxy設定Proxy設定（用於執行HTTP時）;例如在復寫時。

建立新配置時，請勿更改工廠配置，而是使用此處提供的配置管理器為此元件建立新的工廠配置：**https://localhost:4502/system/console/configMgr/**。 代理配置在&#x200B;**org.apache.http.proxyconfigurator中可用。**

>[!NOTE]
>
>在AEM 6.0及舊版中，Proxy是在Day Commons HTTP Client中設定。 自AEM 6.1和更新版本起，Proxy設定已移至「Apache HTTP元件Proxy設定」，而非「Day Commons HTTP Client」設定。

**Day CQ** Antispam配置使用的反垃圾郵件服務(Akismet)。這需要您註冊：

* **提供者**
* **API金鑰**
* **註冊URL**

**AdobeGranite HTML程式庫管** 理器設定此設定以控制用戶端程式庫（css或js）的處理；包括如何看見基礎結構。

* 針對生產執行個體：

   * 啟用&#x200B;**Minify**（移除CRLF和空格字元）。
   * 啟用&#x200B;**Gzip**（允許使用一個請求對檔案進行gzip和訪問）。
   * 停用&#x200B;**除錯**
   * 禁用&#x200B;**計時**

* 針對JS開發（尤其是進行除錯/除錯時）:

   * 停用&#x200B;**Minify**
   * 啟用&#x200B;**Debug**&#x200B;以區隔檔案以進行除錯並與firebug搭配使用。
   * 如果對計時感興趣，請啟用&#x200B;**計時**。
   * 啟用&#x200B;**Debug**&#x200B;控制台以查看JS控制台日誌消息。

>[!CAUTION]
>
>變更&#x200B;**Minify**&#x200B;或&#x200B;**Gzip**&#x200B;的設定時，您也需要刪除`/var/clientlibs`的內容。 這是clientlib的快取版本，下次請求時將重新建置。

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中運行AEM，則會自動為生產實例配置此設定。

**Day CQ HTTP標頭驗證處** 理程式HTTP請求的基本驗證方法的全系統設定。

使用[封閉的使用者群組](/help/sites-administering/cug.md)時，您可以進行設定（其中包括）:

* **HTTP領域**
* **預設登入頁面**

**日CQ連結檢查程** 式服務檢查，並視需要設定：

* **排程** 器週期，定義要自動檢查外部連結的間隔。

* 檢查&#x200B;**Bad Link Tolerance Interval**，以了解在此期間之後，失敗的外部連結被認為是壞的。
* **連結檢查覆蓋模式**，以定義要從連結檢查中排除的任何路徑。

**日CQ連結檢查程** 式任務配置單個連結檢查程式任務（檢查外部連結的任務）的設定：

* 檢查&#x200B;**良好連結測試間隔**&#x200B;和&#x200B;**壞連結測試間隔**&#x200B;中定義的間隔

* 檢查連結時外部訪問所需的與Internet訪問代理和NTLM相關的各種參數。

**Day CQ Mail Service** 配置郵件伺服器的主機名和訪問詳細資訊。請參閱設定郵件服務一節。

**Day CQ MCM電** 子報配置電子報使用的各種設定。

**日CQ根對** 應設定：

* **定** 位路徑，以定義要將「 `/`」的請求重新導向至的位置。

AEM中有兩個可用的UI:

* 觸控式UI是標準UI
* 且過時的傳統UI仍可完全運作

使用AEM根對應，您可以設定要用來作為執行個體預設的UI:

* 若要將觸控式UI設為預設UI,**Target路徑**&#x200B;應指向：

   ```
      /projects.html
   ```

* 若要將傳統UI設為預設UI,**目標路徑**&#x200B;應指向：

   ```
      /welcome.html
   ```

>[!NOTE]
>
>在標準安裝時，觸控最佳化UI為預設UI。

**AdobeGranite SSO驗證處** 理程式配置單一登錄(SSO)詳細資訊；企業作者設定中通常需要這些項目，通常與LDAP搭配使用。

提供各種配置屬性：

* ****
此驗證處理常式的PathPath。如果此參數留空，則會停用驗證處理常式。 例如，路徑/會使驗證處理常式用於整個存放庫。

* **服務**
排名OSGi框架服務排名值用於指示用於調用此服務的順序。這是 
`int` 值中值越高，優先順序越高。預設值為 `0`.

* **標**
題名稱可能包含使用者ID之標題的名稱。

* **Cookie**
名稱可能包含使用者ID之Cookie的名稱。

* **參**
數名稱可能提供使用者ID之請求參數的名稱。

* **User**
Map對於所選用戶，從HTTP請求中提取的用戶名可以替換為憑據對象中的其他用戶名。此處定義對應。 如果使用者名稱 
`admin` 會顯示在地圖的兩側，而會忽略對應。請注意，字元&quot;=&quot;必須以前導的&quot;\&quot;逸出。

* ****
格式指示提供用戶ID的格式。使用：

   * `Basic` 如果使用HTTP基本驗證格式來編碼使用者ID
   * `AsIs` 如果使用者ID是以純文字提供，或應以原樣或任何規則運算式使用套用的值

**Day CQ WCM除錯篩** 選器開發時，這很實用，因為它允許在存取頁面時使用尾碼，例如？debug=layout。例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout將提供開發人員可能感興趣的版面資訊。

* 在生產執行個體上停用此功能以確保效能和安全性。

**Day CQ WCM** FilterConfigure:

* **WCM模式**以定義預設模式。
* 在製作例項上，這可能是`edit`、`disable,preview`或`analytics`。
其他模式可從sidekick存取，或尾碼`?wcmmode=disabled`可用來模擬生產環境。

* 在發佈執行個體上，必須將此值設為`disabled`，以確保無法存取其他模式。

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中運行AEM，則會自動為生產實例配置此設定。

**Day CQ WCM連結檢查程式設定** 器配置：

* **重寫配置** 清單，以指定基於內容的連結檢查程式配置的位置清單。配置可以基於運行模式；這對於區分製作環境和發佈環境很重要，因為linkchecker設定可能不同。

**Day CQ WCM頁面處理** 器配置：

* **路徑**，即系統在觸發前監聽頁面修改的位置清 `jcr:Event`單。

**Adobe頁面曝光** 次數追蹤器針對製作例項進行設定：

* **sling.auth.requirements**:將此屬性的值設定為  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此設定將允許匿名請求至追蹤服務。

>[!NOTE]
>
>如需詳細資訊，請參閱[頁面曝光數](/help/sites-deploying/configuring.md#enabling-page-impressions) 。

**Day CQ WCM頁面統計資** 料發佈例項的設定：

* **傳送資料的** URL，會設定用來追蹤頁面統計資料的URL（如果追蹤器請求經過Dispatcher，則此為重要）;例如，預設值為 `https://localhost:4502/libs/wcm/stats/tracker`。

* **追蹤指** 令碼可啟用( `true`)或停用( `false`)將追蹤指令碼納入頁面。預設值為 `false`.

>[!NOTE]
>
>如需詳細資訊，請參閱[頁面曝光數](/help/sites-deploying/configuring.md#enabling-page-impressions) 。

**Day CQ WCM Version ManagerControl(Day CQ WCM版** 本管理器控制是否及如何在您的系統中管理版本：

* **在啟動時建立版本**，在標準安裝中啟用
* **啟用清除**

* **清除路徑**，即搜尋動作將搜尋的路徑
* **隱式版本設定路徑**，即隱式版本設定處於活動狀態的路徑。

* **最大版本年齡**，版本的最大年齡（以天為單位）

* **最大版本數**，要保留的最大版本數

如需詳細資訊，請參閱[版本清除](/help/sites-deploying/version-purging.md) 。

**Day CQ工作流程電子郵件通** 知服務配置由工作流程傳送之通知的電子郵件設定。

**CQ重寫器HTML剖析器工廠**

控制CQ重寫器的HTML剖析器。

* **要處理的其他標籤**  — 您可以新增或移除要由剖析器處理的HTML標籤。依預設，會處理下列標籤：A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD。
* **保留駝峰式大小寫**  — 依預設，HTML剖析器會將駝峰式大小寫的屬性（例如eBay）轉換為小寫（例如eBay）。您可以關閉此選項以保留駝峰大小寫屬性。 這在使用前端架構(例如Angular2)時相當實用。

**Day Commons JDBC連接** 池配置對用作內容源的外部資料庫的訪問。

這是工廠配置，因此可以配置多個實例。

**Adobe CQ Media DPS工作階段** 服務管理DPS工作階段以用於出版物。

您尤其可以定義`dps.session.service.url.name`:預設值設為[https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN重** 寫器必須確保AEM與CDN之間的通訊，以安全的方式將資產/二進位檔傳送給使用者。這包括兩項任務：

* 第一次（或快取中的過期後）透過CDN從AEM存取資源。
* 安全地存取CDN中快取的資源，因為在CDN中快取資源後，請求就不會傳至AEM，而所有可存取該資源的使用者都應從CDN提供服務。

AEM提供重新寫入程式，可將內部資產URL重新寫入外部CDN URL。 它會重寫要傳遞至CDN的連結，包括JWS簽章和過期時間，以便安全地存取資產。 此功能將用於製作執行個體。

整體流程如下：

1. 使用者向AEM驗證，並使用資產要求頁面。
1. 請求的頁面包含類似`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`的資產
1. 重寫程式會將連結轉換為包含JWS簽名的CDN URL:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然後，使用者的瀏覽器會將資產請求轉送至CDN伺服器
1. CDN應已設定為將要求連同`cdn_sign`參數轉送至AEM。
1. 驗證處理常式會驗證`cdn_sign`參數，並將資產傳回CDN，然後傳送給使用者

使用者瀏覽器、CDN和AEM之間的流量可視化如下。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能目前僅針對AEM製作例項啟用。

**** CDNonfigServiceImpl提供CDN配置

在com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的設定中提供&#x200B;**CDN分發域名**，即可啟用CDN重新寫入功能。

此服務也包含其他設定選項，例如啟用/停用CDN重新寫入、執行CDN重新寫入的路徑前置詞、TTL值，以及通訊協定（HTTP或HTTPS）。

**** CDNRewriter將內部影像URL重新寫入CDN URL

com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的&#x200B;**標籤屬性**&#x200B;值可以定義，以便僅重寫選擇性影像連結。
