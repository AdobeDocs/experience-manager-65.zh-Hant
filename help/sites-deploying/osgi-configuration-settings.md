---
title: OSGi組態設定
description: 本文會詳細說明與專案實作相關的OSGi組態設定（根據套件列示）。 此清單可作為指引，並非詳盡無遺。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 0%

---

# OSGi組態設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/)是AEM技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

OSGi「*」提供標準化的原語，允許使用小型、可重複使用且協同合作的元件來建構應用程式。 這些元件可組成應用程式並部署*。

此功能可讓您在個別停止、安裝和啟動套件組合時，輕鬆管理套件組合。 系統會自動處理相依性。 每個OSGi元件（請參閱[OSGi規格](https://docs.osgi.org/specification/)）都包含在其中一個不同套件組合中。 使用AEM時，有數種方法可管理這類套裝的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

下列OSGi組態設定（根據套件組合列出）與專案實作相關。 並非列出的所有設定都需要調整，有些是為了協助您瞭解AEM的運作方式。

>[!CAUTION]
>
>此清單旨在作為指引，並非詳盡無遺。 並非所有套件組合都列出，也不是某些已列出的套件組合的所有引數。
>
>所需的設定因專案而異。
>
>請參閱Web主控台，以取得使用的值以及引數的詳細資訊。

>[!NOTE]
>
>[AEM Tools](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html)的OSGi Configuration Diff工具可用來列出預設的OSGi設定。

>[!NOTE]
>
>AEM中的特定功能區域可能需要其他套件組合。 在這些情況下，您可以在與適當功能相關的頁面上找到設定詳細資訊。

**AEM復寫事件接聽程式**&#x200B;設定：

* **執行模式**，其中復寫事件會分發給接聽程式。 例如，如果定義為作者，則是「起始」復寫的系統。

* 如果專案程式碼在發佈環境中處理復寫事件（反向復寫），請新增執行模式&#x200B;**發佈**。 例如，當使用Dispatcher從發佈環境排清時，或當發生對其他發佈執行個體的標準復寫時。

**AEM存放庫變更接聽程式**&#x200B;設定：

* **路徑**，用來接聽準備發佈的存放庫事件的位置。

**CRX Sling使用者端存放庫**&#x200B;設定對基礎內容存放庫的存取權。

* **管理員密碼**&#x200B;應在安裝後變更，以確保您執行個體的[安全性](/help/sites-administering/security-checklist.md)。
* 其他變更可能影響到對存放庫的存取，因此應謹慎處理。

**Apache Felix OSGi管理主控台**&#x200B;設定：

* **外掛程式**，主要導覽專案（主控台外掛程式）可在&#x200B;**Apache Felix Web Management Console**&#x200B;中以頂層功能表專案的形式使用。 停用不需要的任何專案，因為每個專案都需要空間和資源。

>[!CAUTION]
>
>請務必設定下列專案：
>
>**使用者名稱**&#x200B;和&#x200B;**密碼**，用於存取Apache Felix Web Management Console本身的認證。
>密碼必須在初始安裝後變更，以確保執行個體的[安全性](/help/sites-administering/security-checklist.md)。

>[!NOTE]
>
>在啟動時（在存放庫可用之前），應視需要使用Felix主控台進行此設定。

**Apache Sling可自訂要求資料記錄器**&#x200B;設定：

* **記錄器名稱**&#x200B;和&#x200B;**記錄格式**&#x200B;以設定要求與存取記錄的位置和格式（預設值： `request.log`）。 在分析與網頁鏈相關的效能或偵錯功能時，此記錄檔是必要的。 它與[Apache Sling要求記錄器](#apacheslingrequestlogger)配對。

請參閱[AEM記錄](/help/sites-deploying/configure-logging.md)和[Sling記錄](https://sling.apache.org/documentation/development/logging.html)。

**Apache Sling事件執行緒集區**&#x200B;設定：

* **最小集區大小**&#x200B;和&#x200B;**最大集區大小**，用來儲存事件執行緒的集區大小。

* **佇列大小**，如果集區已耗盡，則執行緒佇列的大小上限。
建議值為`-1`，因為它將佇列設定為無限制。 如果設定了限制，超過限制時可能會發生損失。

* 變更這些設定可以在具有大量事件的情境中協助效能。 例如，使用大量的AEM DAM或工作流程。
* 您情境的特定值應使用測試來建立。
* 這些設定可能會影響執行個體的效能，因此請勿無故變更，也請勿不當考慮。

**Apache SlingGETServlet**&#x200B;設定轉譯的某些層面：

* **自動索引**&#x200B;以啟用/停用目錄呈現以進行瀏覽。
* **啟用** （或停用）預設轉譯，例如&#x200B;**HTML**、**純文字**、**JSON**&#x200B;或&#x200B;**XML**。
請勿停用JSON。

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中執行AEM，系統會自動為生產執行個體設定此設定。

**Apache Sling JavaScript處理常式**&#x200B;設定以指令碼(servlet)編譯.java檔案的設定。

某些設定可能會影響效能。 請儘可能停用這些設定，尤其是生產執行個體。

* **Source VM**&#x200B;和&#x200B;**目標VM**，定義用作執行階段JVM的JDK版本

* 對於生產執行個體：

   * 停用&#x200B;**產生偵錯資訊**

**Apache Sling JCR安裝程式**&#x200B;這些引數可能不需要設定，但在開發或偵錯時可能很有用。 例如，安裝資料夾對於入庫或出庫或建立封裝非常有用。

* **安裝資料夾名稱regexp**&#x200B;和&#x200B;**安裝資料夾的最大階層深度** — 指定搜尋存放庫資料夾的位置和深度，以尋找要安裝的資源。 當使用萬用字元時（如中）。&#42;/install)已搜尋所有適當的相符專案，例如`/libs/sling/install`和`/libs/cq/core/install`。

* **搜尋路徑**，jcrinstall會搜尋要安裝的資源的路徑清單，以及表示該路徑加權因子的數字。

**Apache Sling作業事件處理常式**&#x200B;設定管理作業排程的引數：

* **重試間隔**、**重試次數上限**、**平行工作數目上限**、**認可等待時間**&#x200B;等等。

* 變更這些設定可以在具有大量工作的情境中改善效能；例如，大量使用AEM DAM和工作流程。
* 您情境的特定值應使用測試來建立。
* 請勿無故變更這些設定，只有在經過適當考慮後才會變更。

**Apache Sling JSP指令碼處理常式**&#x200B;設定JSP指令碼處理常式的效能相關設定。 若要改善效能，請儘可能停用。

尤其在生產執行個體中：

* 停用&#x200B;**產生偵錯資訊**
* 停用&#x200B;**保留產生的Java™**
* 停用&#x200B;**對應的內容**
* 停用&#x200B;**顯示Source片段**

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中執行AEM，系統會自動為生產執行個體設定此設定。

**Apache Sling記錄設定**&#x200B;設定：

* **記錄層級**&#x200B;和&#x200B;**記錄檔**，以定義中央記錄組態(error.log)的位置和記錄層級。 層級可以設定為`DEBUG`、`INFO`、`WARN`、`ERROR`和`FATAL`其中之一。

* **記錄檔數目**&#x200B;和&#x200B;**記錄檔閾值**，以定義記錄檔的大小和版本輪換。

* **訊息模式**&#x200B;定義記錄訊息的格式。

請參閱[AEM記錄](/help/sites-deploying/configure-logging.md#global-logging)和[Sling記錄](https://sling.apache.org/documentation/development/logging.html)。

**Apache Sling記錄記錄器設定（工廠設定）**&#x200B;設定：

* **記錄層級**、**記錄檔**&#x200B;和&#x200B;**訊息格式**&#x200B;以定義記錄檔和訊息的詳細資料。

* **記錄器**&#x200B;以定義類別；例如，僅記錄com.day.cq。

* 使用&#x200B;**工廠組態**，可以新增任何數量的額外組態，以符合所需的各種記錄層級和類別。
* 在開發期間，這類設定很有幫助；例如，在特定記錄檔中記錄特定服務的TRACE訊息。
* 在生產環境中，這類設定很有幫助；例如，將特定服務的相關訊息記錄到個別記錄檔中，以便更輕鬆地進行監視。

請參閱[AEM記錄](/help/sites-deploying/configure-logging.md)和[Sling記錄](https://sling.apache.org/documentation/development/logging.html)。

**Apache Sling記錄寫入器設定（工廠設定）**&#x200B;設定：

* **記錄檔**&#x200B;以定義記錄檔是否存在。
* **記錄檔數目**&#x200B;以定義版本輪換。

* **Apache Sling記錄記錄器組態**&#x200B;組態可以使用寫入器。

* 在開發期間，這類設定很有幫助；例如，在特定記錄檔中記錄特定服務的TRACE訊息。
* 在生產環境中，這類設定很有幫助；例如，將特定服務的相關訊息記錄到個別記錄檔中，以便更輕鬆地進行監視。

請參閱[AEM記錄](/help/sites-deploying/configure-logging.md)和[Sling記錄](https://sling.apache.org/documentation/development/logging.html)。

**Apache Sling主要Servlet**&#x200B;設定：

* **每個要求的呼叫數**&#x200B;和&#x200B;**遞回深度**，可保護您的系統不受無限遞回和過多的指令碼呼叫的影響。

**Apache Sling MIME型別服務**&#x200B;設定：

* **MIME型別**，以將專案所需的型別新增至系統。 如此可讓檔案上的`GET`要求設定連結檔案型別和應用程式的正確內容型別標頭。

**Apache Sling反向連結篩選器**&#x200B;若要解決CRX WebDAV和Apache Sling中跨網站請求偽造(CSRF)的已知安全性問題，您必須設定反向連結篩選器。

反向連結篩選服務是OSGi服務，可讓您設定：

* 應該篩選哪些http方法
* 是否允許空的反向連結標題
* 以及除了伺服器主機以外可允許的伺服器清單。

如需詳細資訊，請參閱[安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。

>[!NOTE]
>
>Apache Sling反向連結篩選取決於快速修正套件的安裝。

**Apache Sling請求記錄器**&#x200B;設定：

* 定義記錄請求方式的多個引數。
* **啟用要求記錄檔**，以啟用或停用。

* **啟用存取記錄檔**，以啟用或停用。

與[Apache Sling可自訂的請求資料記錄器](#apacheslingcustomizablerequestdatalogger)配對。

請參閱[AEM記錄](/help/sites-deploying/configure-logging.md)和[Sling記錄](https://sling.apache.org/documentation/development/logging.html)。

**Apache Sling Resource Resolver Factory**&#x200B;設定Sling資源解析的核心層面：

* **資源搜尋路徑**，新增任何專案特定路徑（但不移除`/libs`或`/apps`）。

* **虛擬URL**&#x200B;以定義虛名URL對應。

* **URL對應**&#x200B;以定義任何別名。 例如，從`/content`到`/`。

* **對應位置**，對應程式組態已在`/etc/map`外部化。

* 使用您的本機安裝（例如，使用`https://localhost:4502/system/console/jcrresolver`）來判斷哪一個資源解析程式作用中。

請參閱： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)。

>[!CAUTION]
>
>在存放庫中設定這些選項。
>
>否則，下次啟動時，AEM可能會覆寫使用Felix主控台對&#x200B;**URL對應**&#x200B;所做的變更。

**Apache Sling Servlet/指令碼解析程式和錯誤處理常式** Sling Servlet和指令碼解析程式有多個工作：

1. 它用作`ServletResolver`，以選取要呼叫以處理請求的Servlet或指令碼。

1. 它充當`SlingScriptResolver`。

1. 它使用相同的演演算法來實作`ErrorHandler`介面，以選取用於解決要求處理servlet和指令碼的錯誤處理servlet和指令碼，藉此管理錯誤處理。

您可以設定各種引數，包括：

* **執行路徑** — 列出搜尋可執行指令碼的路徑。 透過設定特定路徑，您可以限制可以執行的指令碼。 如果未設定路徑，則會使用預設值( `/` = root)，允許執行所有指令碼。
如果設定的路徑值以斜線結尾，則會搜尋整個子樹。 如果沒有這類結尾斜線，指令碼只有在完全相符時才執行。

* **指令碼使用者** — 此選擇性屬性可指定讀取指令碼所使用的存放庫使用者帳戶。 如果未指定帳戶，則預設會使用`admin`使用者。

* **預設擴充功能** — 使用預設行為的擴充功能清單。 資源型別的最後一個路徑區段可作為指令碼名稱使用。

**Apache HTTP元件Proxy組態** — 使用Apache HTTP使用者端的所有程式碼的Proxy組態，在建立HTTP時使用。 例如，在復寫上。

建立組態時，請勿變更工廠組態。 請改用此處提供的組態管理員來建立此元件的工廠組態： **https://localhost:4502/system/console/configMgr/**。 **org.apache.http.proxyconfigurator.**&#x200B;中提供Proxy設定

>[!NOTE]
>
>在AEM 6.0及舊版中，Proxy是在Day Commons HTTP Client中設定。 截至AEM 6.1和更新版本，Proxy設定已移至「Apache HTTP元件Proxy設定」而非「Day Commons HTTP Client」設定。

**Day CQ Antispam**&#x200B;設定使用的反垃圾郵件服務(Akismet)。 此功能需要您註冊下列專案：

* **提供者**
* **API金鑰**
* **已登入的URL**

**AdobeGraniteHTML程式庫管理員**&#x200B;設定以控制使用者端程式庫（css或js）的處理，例如包括基礎結構的顯示方式。

* 對於生產執行個體：

   * 啟用&#x200B;**最小化** （移除CRLF和空白字元）。
   * 啟用&#x200B;**Gzip** （允許透過一個要求來壓縮及存取檔案）。
   * 停用&#x200B;**偵錯**
   * 停用&#x200B;**計時**

* 若為JS開發（尤其是在firebugging/debugging時）：

   * 停用&#x200B;**最小化**
   * 啟用&#x200B;**Debug**&#x200B;以分隔檔案以進行偵錯，並與fire bug搭配使用。
   * 如果想要計時，請啟用&#x200B;**計時**。
   * 啟用&#x200B;**偵錯**&#x200B;主控台以檢視JS主控台記錄訊息。

>[!CAUTION]
>
>變更&#x200B;**Minify**&#x200B;或&#x200B;**Gzip**&#x200B;的設定時，請刪除clientlibs快取的內容。 如需詳細資訊，請參閱[知識庫文章](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html)。

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中執行AEM，系統會自動為生產執行個體設定此設定。

**Day CQ HTTP Header Authentication Handler** HTTP要求之基本驗證方法的全系統設定。

使用[已關閉的使用者群組](/help/sites-administering/cug.md)時，您可以設定下列專案：

* **HTTP領域**
* **預設登入頁面**

**天CQ連結檢查器服務**&#x200B;檢查，並視需要設定：

* **排程器週期**，定義自動檢查外部連結的間隔。

* 檢查&#x200B;**錯誤的連結容許間隔**，檢視不成功的外部連結在哪個時段之後被視為錯誤。
* **連結檢查覆寫模式**，定義要從連結檢查排除的任何路徑。

**天CQ連結檢查器工作**&#x200B;設定單一連結檢查器工作（檢查外部連結的工作）的設定：

* 檢查&#x200B;**良好連結測試間隔**&#x200B;和&#x200B;**錯誤連結測試間隔**&#x200B;中定義的間隔

* 檢查連結時，與外部存取所需的網際網路存取代理和NTLM相關的各種引數。

**Day CQ Mail Service**&#x200B;設定郵件伺服器的主機名稱和存取詳細資料。 請參閱設定郵件服務區段。

**Day CQ MCM Newsletter**&#x200B;設定與Newsletter搭配使用的各種設定。

**Day CQ根對應**&#x200B;設定：

* **目標路徑**，以定義將「`/`」的請求重新導向至何處。

AEM中有兩個可用的UI：

* 觸控式UI是標準UI
* 且已棄用的傳統UI仍可完全運作

使用AEM根對應，您可以設定您要設為執行個體預設的UI：

* 若要以觸控式UI作為預設UI，**Target路徑**&#x200B;應指向下列專案：

  ```shell
     /projects.html
  ```

* 若要以傳統UI作為預設UI，**Target路徑**&#x200B;應指向下列專案：

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>在標準安裝中，觸控最佳化的UI是預設的UI。

**AdobeGranite SSO驗證處理常式** — 設定SSO （單一登入）詳細資料。 這些詳細資訊通常需要用於企業作者設定，通常使用LDAP。

有多種組態屬性可供使用：

* **路徑**
此驗證處理常式的作用中路徑。 如果此引數留空，則會停用驗證處理常式。 例如，路徑/會導致驗證處理常式用於整個存放庫。

* **服務排名**
OSGi框架服務排名值用於表示呼叫此服務所用的順序。 此值是`int`值，其中較高的值代表較高的優先順序。
預設值為`0`。

* **標頭名稱**
可能包含使用者ID的標頭名稱。

* **Cookie名稱**
可能包含使用者ID的Cookie名稱。

* **引數名稱**
可能提供使用者ID的要求引數名稱。

* **使用者地圖**
對於選取的使用者，從HTTP請求擷取的使用者名稱可以憑證物件中的其他名稱取代。 對應會在此處定義。 如果使用者名稱`admin`出現在地圖的兩側，則會忽略對應。 字元「=」必須以前導字元「\」逸出。

* **格式**
表示提供使用者ID的格式。 使用：

   * 如果使用者ID是以HTTP基本驗證格式編碼，`Basic`
   * 如果以純文字提供使用者ID，或任何套用的規則運算式值應該依原樣或任何規則運算式使用，則值為`AsIs`

**Day CQ WCM Debug Filter**&#x200B;這在開發時非常有用，因為它允許存取頁面時使用尾碼，例如？debug=layout。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout提供開發人員可能感興趣的版面配置資訊。

* 為確保效能和安全性，請在生產執行個體上停用。

**Day CQ WCM篩選器**&#x200B;設定：

* **WCM模式**&#x200B;以定義預設模式。
* 在作者執行個體上，此模式可能是`edit`、`disable,preview`或`analytics`。
其他模式可從sidekick存取，或字尾`?wcmmode=disabled`可用於模擬生產環境。

* 在發佈執行個體上，此模式必須設定為`disabled`以確保沒有其他模式可供存取。

>[!NOTE]
>
>如果您在[生產就緒模式](/help/sites-administering/production-ready.md)中執行AEM，系統會自動為生產執行個體設定此設定。

**Day CQ WCM連結檢查器設定器**&#x200B;設定：

* **重寫組態清單**，以指定內容連結檢查器組態的位置清單。 這些設定可以根據執行模式。 由於連結檢查器設定可能不同，因此此事實對於區分製作和發佈環境很重要。

**Day CQ WCM Page Manager Factory**&#x200B;設定：

* **頁面子樹狀結構啟用檢查**，讓使用者（沒有復寫許可權）刪除或移動頁面（即使頁面未啟用）。

**Day CQ WCM Page Processor**&#x200B;設定：

* **路徑**，在觸發`jcr:Event`之前，系統監聽頁面修改的位置清單。

**Adobe頁面曝光數追蹤器**&#x200B;對於作者執行個體，請設定如下：

* **sling.auth.requirements**：將此屬性的值設定為`-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此設定允許向追蹤服務提出匿名請求。

>[!NOTE]
>
>如需詳細資訊，請參閱[頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions)。

**Day CQ WCM頁面統計資料**&#x200B;針對發佈執行個體設定：

* 用於傳送資料的&#x200B;**URL**&#x200B;用於設定用於追蹤頁面統計資料的URL (如果追蹤器要求通過Dispatcher則很重要)；例如，預設值為`https://localhost:4502/libs/wcm/stats/tracker`。

* **追蹤指令碼已啟用**，以啟用(`true`)或停用(`false`)在頁面上包含追蹤指令碼。 預設值為 `false`。

>[!NOTE]
>
>如需詳細資訊，請參閱[頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions)。

**Day CQ WCM Version Manager**&#x200B;控制系統中是否管理版本以及管理版本的方式：

* **啟動時建立版本**，已在標準安裝中啟用
* **啟用清除**

* **清除路徑**，搜尋動作搜尋的路徑。
* **隱含版本設定路徑**，隱含版本設定為作用中的路徑。

* **最大版本期限**，版本的最大期限（以天為單位）

* **版本數目上限**，要保留的版本數目上限

如需詳細資訊，請參閱[版本清除](/help/sites-deploying/version-purging.md)。

**Day CQ工作流程電子郵件通知服務**&#x200B;設定工作流程所傳送通知的電子郵件設定。

**CQ重寫程式HTML剖析器Factory**

控制CQ重寫程式的HTML剖析器。

* **要處理的其他標籤** — 您可以新增或移除剖析器要處理的HTML標籤。 預設會處理下列標籤：A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD。
* **保留駝峰式大小寫** — 依預設，HTML剖析器會將駝峰式大小寫的屬性（例如`eBay`）轉換為小寫（例如`ebay`）。 您可以關閉此設定以保留駝峰式大小寫屬性。 使用前端架構(例如Angular2)時，此設定相當實用。

**Day Commons JDBC連線集區**&#x200B;設定對作為內容來源的外部資料庫的存取權。

工廠組態，因此可以設定多個執行個體。

**CDN重寫程式** AEM與CDN之間的通訊必須確定，才能以安全的方式將資產/二進位檔傳送給一般使用者。 此程式涉及下列兩項工作：

* 第一次（或在快取中的資源過期後）透過CDN從AEM存取資源。
* 安全地存取在CDN中快取的資源。 在CDN中快取資源後，要求不會前往AEM，而上有權存取該資源的所有使用者應該會從CDN提供服務。

AEM提供重寫程式，可將內部資產URL重寫至外部CDN URL。 它會重寫要傳遞至CDN的連結，包括JWS簽名和到期時間，以允許安全地存取資產。 此功能將用於編寫執行個體。

整體流程如下：

1. 使用者透過AEM進行驗證並請求包含資產的頁面。
1. 請求的頁面包含類似於`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`的資產
1. 重寫程式會將連結轉換為包含JWS簽名的CDN URL：
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 之後，使用者的瀏覽器會將資產請求轉送至CDN伺服器
1. CDN應設定為將要求連同`cdn_sign`引數轉送至AEM。
1. 驗證處理常式會驗證`cdn_sign`引數，並將資產傳回CDN，再傳送給使用者

使用者的瀏覽器、CDN和AEM之間的流量視覺化如下所示。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能僅對AEM作者執行個體啟用。

**CDNConfigServiceImpl**&#x200B;提供CDN設定

在com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的設定中提供&#x200B;**CDN發佈網域名稱**，即可啟用CDN重寫功能。

此服務也包含其他設定選項，例如啟用/停用CDN重新寫入、執行CDN重新寫入的路徑首碼、TTL值和通訊協定（HTTP或HTTPS）。

**CDNRewriter**&#x200B;將內部影像URL重寫為CDN URL的重寫程式

可以定義com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的&#x200B;**標籤屬性**&#x200B;值，以便只重寫選擇性影像連結。
