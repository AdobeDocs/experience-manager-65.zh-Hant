---
title: OSGi配置設定
seo-title: OSGi配置設定
description: 本文詳細說明與專案實作相關的OSGi組態設定（依照套件列出）。 這份清單是一項准則，並非詳盡無遺。
seo-description: 本文詳細說明與專案實作相關的OSGi組態設定（依照套件列出）。 這份清單是一項准則，並非詳盡無遺。
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: 設定
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# OSGi配置設定{#osgi-configuration-settings}

[](https://www.osgi.org/) OSG是OSG技術中的一個基本元AEM素。它用於控制複合束及其AEM配置。

OSGi &quot;*提供標準化的基元，可讓應用程式由小型、可重複使用和協作的元件來建立。 這些元件可以組成到應用程式並部署*&quot;。

這樣可以輕鬆管理捆綁包，因為它們可以單獨停止、安裝和啟動。 互依關係會自動處理。 每個OSGi元件（請參見[OSGi規範](https://www.osgi.org/Specifications/HomePage)）都包含在各種束之一中。 使用時，有AEM幾種方法可管理此類捆綁的配置設定；如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

下列OSGi組態設定（依照套件列出）與專案實作相關。 並非所有列出的設定都需要調整，有些設定會提及以協助您瞭解運作AEM方式。

>[!CAUTION]
>
>這份清單旨在作為一項准則，並非詳盡無遺。 並非所有束都列出，也並非某些束的所有參數都列出。
>
>所需的設定會因專案而異。
>
>請參閱Web主控台，以取得所用值和參數的詳細資訊。

>[!NOTE]
>
>OSGi配置比較工具是[AEM Tools](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)的一部分，可用於列出預設的OSGi配置。

>[!NOTE]
>
>在中的特定功能領域可能需要進一步的組合AEM。 在這些情況下，可在與適當功能相關的頁面上找到配置詳細資訊。

**AEM複製事件監** 聽器配置：

* **運行模式** ，其中複製事件將分發到偵聽程式。 例如，如果定義為作者，則此系統將「啟動」複製。

* 如果項目代碼在發佈環境中處理複製事件（反向複製），則需要添加運行模式&#x200B;**publish**。 例如，當調度程式用於從發佈環境刷新時，或當發生到其他發佈實例的標準複製時。

**AEM資料庫更改** 偵聽器配置：

* **路徑**&#x200B;是要監聽儲存庫事件以便分發的位置。

**CRX Sling Client** Repository設定對基礎內容存放庫的存取權。

* 安裝後應變更&#x200B;**管理密碼**，以確保實例的[安全性](/help/sites-administering/security-checklist.md)。
* 其他更改不應該是必要的，而且必須小心，因為它們可能影響對儲存庫的訪問。

**Wiki郵件服** 務為Wiki發送的電子郵件配置電子郵件設定。

**Apache Felix OSGi管理控** 制台設定：

* **外掛程式**，主導覽項目（主控台外掛程式）可在 **Apache Felix Web Management** Console的頂層功能表項目中取得。停用您不需要的任何項目，因為每個項目都需要空間和資源。

>[!CAUTION]
>
>請務必設定下列項目：
>
>**User** Name and  **Password**，用於訪問Apache Felix Web Management Console本身的認證。
>初始安裝後必須更改密碼，以確保實例的[security](/help/sites-administering/security-checklist.md)。

>[!NOTE]
>
>啟動時，應視需要使用Felix Console進行此設定——儲存庫才可使用。

**Apache Sling Customized Request Data** LoggerConfigure:

* **Logger** Nameand  **Log** Formatto configure the location and format of request and access logging(default: `request.log`)。在分析與Web鏈相關的效能或調試功能時，此日誌檔案是必不可少的。
這與[Apache Sling Request Logger](#apacheslingrequestlogger)配對。

如需詳細資訊，請參閱AEM[Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Eventing Thread** PoolConfigure:

* **最小池** 大小 **和最大池大小**，用於保存事件線程的池大小。

* **隊列大小**，即當池用完時線程隊列的最大大小。建議的值為`-1`，因為這會將佇列設為無限制；如果設定了限制，則超出限制時可能會發生損失。

* 變更這些設定有助於在發生大量事件的情況下提供效能；例如，大量使AEM用DAM或工作流程。
* 應使用測試建立藍本的特定值。
* 這些設定會影響執行個體的效能，因此請勿在沒有理由和適當考量的情況下變更執行個體。

**Apache SlingGET** Servlet設定轉譯的某些方面：

* **自動** 索引，啟用／停用瀏覽的目錄轉換。
* **啟用** （或停用）預設轉譯，例如 **HMTL**、 **純文字**、 **** JSON或 **** XML。您不應停用JSON。

>[!NOTE]
>
>如果您在[生產就緒模式AEM](/help/sites-administering/production-ready.md)中運行，則會自動為生產實例配置此設定。

**Apache Sling Java Script** Handler設定。java檔案編譯為指令碼(servlet)的設定。

某些設定可能會影響效能，但應盡可能停用這些設定，尤其是針對生產執行個體。

* S **源VM**&#x200B;和&#x200B;**目標VM**，將JDK版本定義為用作運行時JVM

* 對於生產實例：

   * 停用&#x200B;**產生除錯資訊**

**Apache Sling JCR** Installer這些參數可能不需要設定，但在開發或除錯時可能很有用。例如，安裝資料夾對於簽入／簽出或建立軟體包非常有用。

* **安裝資料夾名** 稱regexpand  **Max hierarchy depth of install folders**  —— 指定在何處和向哪個深度搜索儲存庫資料夾以查找要安裝的資源。使用萬用字元時(如中。*/install)會搜尋所有適當的相符項目，例如`/libs/sling/install`和`/libs/cq/core/install`。

* **Search Path**（搜索路徑）,jcrinstall搜索要安裝的資源的路徑清單，以及一個表示該路徑加權系數的數字。

**Apache Sling Job Event** Handler設定管理工作排程的參數：

* **重試間隔**、最 **大重試次數**、最大並行作業數 **、**&#x200B;確認等待時間 ****，以及其他。

* 更改這些設定可以改進具有大量作業的場景的效能；例如，大量使用AEMDAM和工作流程。
* 應使用測試建立藍本的特定值。
* 請勿無故變更這些設定，但必須經過適當考慮才變更。

**Apache Sling JSP指令碼處** 理常式設定JSP指令碼處理常式的效能相關設定。為了改善效能，您應盡可能停用。

尤其是生產例項：

* 停用&#x200B;**產生除錯資訊**
* 禁用&#x200B;**保留生成的Java**
* 禁用&#x200B;**映射內容**
* 禁用&#x200B;**顯示源片段**

>[!NOTE]
>
>如果您在[生產就緒模式AEM](/help/sites-administering/production-ready.md)中運行，則會自動為生產實例配置此設定。

**Apache Sling Logging** ConfigurationConfigure:

* **記** 錄級 **別記錄檔**，以定義中央記錄設定(error.log)的位置和記錄層級。該級別可設定為`DEBUG`、`INFO`、`WARN`、`ERROR`和`FATAL`之一。

* **「日誌文** 件和日 **志檔案** 閾值數」，用於定義日誌檔案的大小和版本旋轉。

* **消息** 模式定義日誌消息的格式。

如需詳細資訊，請參閱AEM[Logging](/help/sites-deploying/configure-logging.md#global-logging)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Logging Logger Configuration(Factory Configuration)** Configure:

* **日誌級別**、日 **志文** 件和消 **** 息格式定義日誌檔案和消息的詳細資訊。

* **** Logger要定義類別；例如，僅記錄com.day.cq的記錄。

* 通過使用&#x200B;**工廠配置**，可以添加任意數量的附加配置以滿足所需的各種日誌級別和類別。
* 這類配置在開發過程中很有幫助；例如，在特定日誌檔案中記錄特定服務的TRACE消息。
* 這種配置在生產環境中非常有用；例如，將有關特定服務的消息記錄到單個日誌檔案中，以便更方便地進行監視。

如需詳細資訊，請參閱AEM[Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Logging Writer Configuration(Factory Configuration)** Configure:

* **日誌** 檔案：定義日誌檔案的存在性。
* **定義版本** 旋轉的日誌檔案數。

* The writer can be used by a **Apache Sling Logging Logger Configuration** configuration.

* 這類配置在開發過程中很有幫助；例如，在特定日誌檔案中記錄特定服務的TRACE消息。
* 這種配置在生產環境中非常有用；例如，將有關特定服務的消息記錄到單個日誌檔案中，以便更方便地進行監視。

如需詳細資訊，請參閱AEM[Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Main** ServletConfigure:

* **每個請求和遞回** 深度的 **呼** 叫數，可保護您的系統不受無限遞回和過多的指令碼呼叫。

**Apache Sling MIME Type** ServiceConfigure:

* **MIME類** 型，將項目所需的類型添加到系統中。這可讓檔案上的`GET`要求設定正確的內容類型標題，以連結檔案類型和應用程式。

**Apache Sling Referrer** Filter若要解決CRX WebDAV和Apache Sling中跨網站要求偽造(CSRF)的已知安全性問題，您必須設定反向連結篩選器。

反向連結篩選服務是一項OSGi服務，可讓您設定：

* 哪些http方法應加以篩選
* 是否允許空的反向連結標題
* 以及除伺服器主機外允許的伺服器清單。

如需詳細資訊，請參閱[安全性檢查清單——跨網站偽造要求問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。

>[!NOTE]
>
>Apache Sling Referrer Filter取決於快速修正套件的安裝。

**Apache Sling Request** LoggerConfigure:

* 定義請求記錄方式的各種參數。
* **啟用請求記錄**，以啟用或停用。

* **啟用訪問日誌**，以啟用或禁用。

這與[Apache Sling Customized Request Data Logger](#apacheslingcustomizablerequestdatalogger)配對。

如需詳細資訊，請參閱AEM[Logging](/help/sites-deploying/configure-logging.md)和[Sling Logging](https://sling.apache.org/site/logging.html)。

**Apache Sling Resource Resolver** Factory設定Sling資源解析度的中央層面：

* **資源搜索路徑**，添加任何項目特定路徑(但不刪除 `/libs` 或 `/apps`)。

* **虛擬** URL來定義虛名的URL對應。

* **URL映** 射以定義任何別名；例如，從 `/content` 到 `/`。

* **映射位置**，中外部化的映射器配置 `/etc/map`。

* 使用本地安裝（例如，使用`https://localhost:4502/system/console/jcrresolver`）確定哪個資源解析器處於活動狀態。

如需詳細資訊，請參閱：[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)。

>[!CAUTION]
>
>特別是，必須在儲存庫中配置這些選項。
>
>否則，使用Felix控制台對&#x200B;**URL Mappings**&#x200B;所做的變更可能會在下次啟AEM動時被覆寫。

**Apache Sling Servlet/Script Resolver和Error** HandlerThe Sling Servlet和Script Resolver有多項工作：

1. 它用作`ServletResolver`以選擇要調用的Servlet或指令碼來處理請求。

1. 它充當`SlingScriptResolver`。

1. 它通過使用與用於解決請求處理servlet和指令碼相同的算法實施`ErrorHandler`介面來管理錯誤處理。

可設定各種參數，包括：

* **執行** 路徑會滑移路徑以搜尋可執行指令碼；通過配置特定路徑，您可以限制可以執行的指令碼。如果未配置路徑，則使用預設路徑(`/` = root)，則允許執行所有指令碼。
如果已配置的路徑值以斜線結尾，則搜索整個子樹。 若沒有這樣的尾隨斜線，則只有在指令碼完全符合時才會執行它。

* **指令碼用戶** -此可選屬性可以指定用於讀取指令碼的儲存庫用戶帳戶。如果未指定帳戶，則預設使用`admin`用戶。

* **預設** 擴充功能將使用預設行為的擴充功能清單。這表示資源類型的最後一個路徑段可用作指令碼名稱。

**Day Commons GFX Font** Helper當轉換圖形時，您可以使用DrawText嵌入文字。為此，您也可以安裝您自己的字型：

* 定義要搜索項目特定字型的&#x200B;**字型路徑**。
例如，`/apps/myapp/fonts`。

**Apache HTTP Components Proxy** Configuration使用Apache HTTP用戶端（用於建立HTTP時）的所有程式碼的Proxy組態；例如，在複製時。

建立新配置時，請勿更改工廠配置，而是使用此處提供的配置管理器為此元件建立新工廠配置：**https://localhost:4502/system/console/configMgr/**。 代理配置在&#x200B;**org.apache.http.proxyconfigurator中可用。**

>[!NOTE]
>
>在AEM6.0及舊版中，Proxy是在Day Commons HTTP Client中設定。 自AEM6.1和更新版本起，代理設定已移至「Apache HTTP Components Proxy Configuration」，而非「Day Commons HTTP Client」設定。

**Day CQ** Antispam配置使用的反垃圾郵件服務(Akismet)。您必須註冊：

* **提供者**
* **API金鑰**
* **註冊的URL**

**AdobeGranite HTML Library** Manager設定此設定以控制用戶端程式庫（css或js）的處理；例如，包括如何看待基礎結構。

* 對於生產實例：

   * 啟用&#x200B;**Minify**（以移除CRLF和空白字元）。
   * 啟用&#x200B;**Gzip**（允許使用一個請求對檔案進行壓縮和訪問）。
   * 停用&#x200B;**除錯**
   * 停用&#x200B;**計時**

* 針對JS開發（尤其是當防火牆／除錯時）:

   * 禁用&#x200B;**Minify**
   * 啟用&#x200B;**Debug**&#x200B;以分隔檔案以進行除錯，並與firebug搭配使用。
   * 如果對計時感興趣，請啟用&#x200B;**計時**。
   * 啟用&#x200B;**Debug**&#x200B;主控台以檢視JS主控台記錄訊息。

>[!CAUTION]
>
>變更&#x200B;**Minify**&#x200B;或&#x200B;**Gzip**&#x200B;的設定時，您也需要刪除`/var/clientlibs`的內容。 這是clientlibs的快取版本，將在下次要求時重建。

>[!NOTE]
>
>如果您在[生產就緒模式AEM](/help/sites-administering/production-ready.md)中運行，則會自動為生產實例配置此設定。

**Day CQ HTTP Header Authentication** Handler HTTP請求的基本驗證方法的系統寬設定。

使用[關閉的用戶組](/help/sites-administering/cug.md)時，您可以配置（其中包括）:

* **HTTP領域**
* **預設登入頁面**

**Day CQ Link Checker** ServiceCheck，並視需要設定：

* **排程** 器週期：定義自動檢查外部連結的間隔。

* 檢查&#x200B;**鏈路容差間隔**&#x200B;中，在此期間之後，失敗的外部鏈路被認為是錯誤的。
* **「連結檢查覆寫模式**」，以定義任何要排除在連結檢查之外的路徑。

**Day CQ Link Checker任** 務配置單個連結檢查器任務（檢查外部連結的任務）的設定：

* 檢查&#x200B;**良好鏈路測試間隔**&#x200B;和&#x200B;**壞鏈路測試間隔**&#x200B;中定義的間隔

* 檢查連結時，外部訪問所需的與Internet訪問代理和NTLM相關的各種參數。

**Day CQ Mail** Service為郵件伺服器配置主機名和訪問詳細資訊。請參閱「配置郵件服務」部分。

**Day CQ MCM電子報** 設定電子報中使用的各種設定。

**日CQ根映** 射配置：

* **定位** 路徑，以定義「」請求將重新導 `/`向至何處。

以下提供兩個UIAEM:

* 觸控式使用者介面是標準使用者介面
* 淘汰的傳統UI仍可完全運作

使用AEM根對應，您可以設定您要擁有的UI做為例項的預設值：

* 若要讓觸控式UI做為預設UI,**目標路徑**&#x200B;應指向：

   ```
      /projects.html
   ```

* 要將傳統UI作為預設UI,**目標路徑**&#x200B;應指向：

   ```
      /welcome.html
   ```

>[!NOTE]
>
>標準安裝時，觸控最佳化UI為預設UI。

**AdobeGranite SSO驗證處** 理常式設定單一登入(SSO)詳細資訊；在企業作者設定中通常需要這些功能，通常與LDAP搭配使用。

可使用各種配置屬性：

* **此驗**
證處理常式處於活動狀態的PathPath。如果此參數留空，驗證處理常式會停用。 例如，路徑／會使驗證處理常式用於整個資料庫。

* **服務**
排名OSGi Framework服務排名值用於指示調用此服務所用的順序。這是 
`int` 值，其中值越高，表示優先順序越高。預設值為 `0`.

* **標題**
名稱可能包含使用者ID的標題名稱。

* **Cookie名**
稱可能包含使用者ID的Cookie名稱。

* **參**
數名稱可能提供使用者ID的請求參數名稱。

* **用**
戶映射對於選定用戶，從HTTP請求提取的用戶名可以替換為憑據對象中的不同用戶名。此處定義了映射。 如果用戶名 
`admin` 顯示在地圖的任一側，則會忽略對應。請注意，字元&quot;=&quot;必須以前導&quot;\&quot;逸出。

* **格**
式指出提供使用者ID的格式。使用：

   * `Basic` 如果使用者ID編碼為HTTP基本驗證格式
   * `AsIs` 如果使用者ID是以純文字提供，或任何規則運算式套用值應以原樣使用或任何規則運算式

**Day CQ WCM Debug** Filter這在開發時很有用，因為它允許在存取頁面時使用字尾，例如？debug=layout。例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout將提供開發人員可能感興趣的版面資訊。

* 在生產實例上禁用此功能，以確保效能和安全性。

**日CQ WCM篩** 選設定：

* **WCM模式**以定義預設模式。
* 在作者實例上，此值可能為`edit`、`disable,preview`或`analytics`。
其他模式可從sidekick存取，或使用尾碼`?wcmmode=disabled`來模擬生產環境。

* 在發佈實例上，必須將此值設定為`disabled` ，以確保不能訪問其他模式。

>[!NOTE]
>
>如果您在[生產就緒模式AEM](/help/sites-administering/production-ready.md)中運行，則會自動為生產實例配置此設定。

**CQ WCM Link Checker Configurator(日CQ WCM連結檢查器配** 置器)配置：

* **重寫配置** 清單，以指定基於內容的連結檢查器配置的位置清單。配置可以基於運行模式；這對於區分作者和發佈環境很重要，因為連結檢查器設定可能不同。

**第CQ天WCM頁面處理** 器配置：

* **路徑**，即系統在觸發頁面之前監聽頁面修改的位置清單 `jcr:Event`。

**Adobe頁面印象** 追蹤器針對作者例項設定：

* **sling.auth.requirements**:將此屬性的值設定為  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此設定將允許追蹤服務的匿名要求。

>[!NOTE]
>
>如需詳細資訊，請參閱[頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions)。

**Day CQ WCM Page** Statistics針對發佈例項設定：

* **傳送資料的URL** 會設定用於追蹤頁面統計資料的URL（如果追蹤器要求經過發送器，此點至關重要）;例如，預設值為 `https://localhost:4502/libs/wcm/stats/tracker`。

* **啟用追** 蹤指令碼以啟用( `true`)或停用( `false`)頁面上包含追蹤指令碼。預設值為 `false`.

>[!NOTE]
>
>如需詳細資訊，請參閱[頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions)。

**Day CQ WCM Version** ManagerControl（Day CQ WCM Version Manager控制是否以及如何在系統中管理版本）:

* **在啟動時建立版本**，在標準安裝中啟用
* **啟用清除**

* **清除路徑**，即搜索操作將搜索的路徑
* **隱式版本化路徑**，即隱式版本化處於活動狀態的路徑。

* **最大版本年齡**，版本的最大年齡（以天為單位）

* **最大版本數**，要保留的最大版本數

如需詳細資訊，請參閱[版本清除](/help/sites-deploying/version-purging.md)。

**Day CQ Workflow Email Notification** Service為工作流程傳送的通知設定電子郵件設定。

**Day CQSE HTTP** Service控制CQ Servlet引擎：

* **NIO for HTTP, **是否使用NIO for HTTP。 預設為true。 僅在啟用HTTP時使用。
* **連線逾時，**連線逾時（以毫秒為單位）。 此屬性同時適用於HTTP和HTTPS連接。 預設為60秒。

* **啟用HTTPS,** 是否啟用HTTPS。預設為false。
* **Session Timeout**, Default lifetime of an HTTP session specified in minutes.如果逾時為0或更少，則作業不會逾時。 預設為10分鐘。
* **除錯記錄**，是否要寫入DEBUG級別消息。預設為false。
* **請求緩衝區大小**，請求的緩衝區大小（以位元組為單位）。預設值為8KB。
* **最大線程數**，用於處理請求的線程數。預設值為200。

以下屬性僅在啟用HTTPS時適用。

* **HTTPS Port**，監聽HTTPS要求的埠。預設為 433.
* **NIO for HTTPS**，是否使用NIO for HTTP。預設為NIO for HTTP屬性的值。
* **密鑰**&#x200B;庫，用於HTTPS的密鑰庫的絕對路徑。若已啟用HTTPS，則此為必要項目。
* **密鑰庫密碼**，用於訪問密鑰庫的密碼。
* **密鑰別名**，密鑰庫中密鑰的別名。
* **密鑰密碼**，用於解鎖密鑰庫中的密鑰的密碼。
* **用戶端憑證**，用戶端提供有效憑證的要求。預設為無。

如需SSL相關選項的詳細資訊，請參閱[啟用HTTP Over SSL](/help/sites-administering/ssl-by-default.md)，以及如何為CQSE啟用HTTPS的完整說明。

**CQ重寫器HTML剖析器工廠**

控制CQ重寫器的HTML剖析器。

* **要處理的附加標籤** -您可以添加或刪除要由解析器處理的HTML標籤。依預設，會處理下列標籤：A,IMG，區域，表單，基礎，連結，指令碼，正文，HEAD。
* **保留駝峰大小寫** -依預設，HTML剖析器會將駝峰大小寫的屬性（例如eBay）轉換為小寫（例如ebay）。您可以關閉此選項以保留駝峰大小寫屬性。 這在使用前端架構(例如Angular2)時很有用。

**日公域JDBC連接池** 配置對用作內容源的外部資料庫的訪問。

這是工廠配置，因此可以配置多個實例。

**Adobe CQ媒體DPS工作階** 段服務管理DPS工作階段以搭配出版物使用。

您尤其可以定義`dps.session.service.url.name`:default set to [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN重** 新寫入器AEM必須確保與CDN之間的通訊，以安全的方式將資產／二進位檔傳送給使用者。這包括兩項任務：

* 首次(或在快取中AEM過期後)透過CDN存取資源。
* 安全地存取在CDN中快取的資源，因為一旦在CDN中快取資源，請求就不會移至，而AEM且所有可存取該資源的使用者都應從CDN中提供服務。

提AEM供重寫器，可將內部資產URL重寫至外部CDN URL。 它會重寫要傳遞至CDN的連結，包括JWS簽章和過期時間，以便安全地存取資產。 此功能將用於作者實例。

總體流程如下：

1. 使用者驗證AEM並要求具有資產的頁面。
1. 請求的頁面包含類似`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`的資產
1. 重新寫入器會轉換包含JWS簽名之CDN URL的連結：
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然後，使用者的瀏覽器會將資產要求轉送至CDN伺服器
1. CDN應設定為將請求AEM與`cdn_sign`參數一起轉送。
1. 驗證處理常式會驗證`cdn_sign`參數，並將資產傳回CDN，然後再傳送給使用者

使用者瀏覽器、CDN和之間的流量可AEM以視覺化如下。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能目前僅針對作者例項啟AEM用。

**** CDNConfigServiceImpl提供CDN配置

在com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的配置中提供&#x200B;**CDN分發域名**，可啟用CDN重寫功能。

此服務也包含其他設定選項，例如啟用／停用CDN重寫、執行CDN重寫的路徑字首、TTL值和通訊協定（HTTP或HTTPS）。

**CDNRewriter** 將內部影像URL重寫為CDN URL的重寫器

com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的&#x200B;**標籤屬性**&#x200B;值可以定義，以便僅重寫選擇性影像連結。
