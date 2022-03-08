---
title: OSGi配置設定
seo-title: OSGi Configuration Settings
description: 本文詳細介紹了與項目實施相關的OSGi配置設定（根據捆綁包列出）。 該清單是一項准則，並非詳盡無遺。
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
source-git-commit: 9a3f26b6709461a911e833f7e340d11c759c7dae
workflow-type: tm+mt
source-wordcount: '3558'
ht-degree: 0%

---

# OSGi配置設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 是技術層面的一個基本要AEM素。 它用於控制複合束及其AEM結構。

OSGi &quot;*提供了標準化基元，允許應用程式由小型、可重用和協作的元件構建。 這些元件可以組合成應用程式並部署*。

這允許輕鬆管理捆綁包，因為它們可以單獨停止、安裝和啟動。 互依關係將自動處理。 每個OSGi元件(請參見 [OSGi規範](https://www.osgi.org/Specifications/HomePage))包含在各種捆綁包中。 使用時，AEM有幾種方法管理此類捆綁包的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

以下OSGi配置設定（根據捆綁包列出）與項目實施相關。 並非所有列出的設定都需要調整，有些設定可幫助您瞭解操作AEM方式。

>[!CAUTION]
>
>該清單旨在作為准則，並非詳盡無遺。 未列出所有束，也未列出某些束的所有參數。
>
>所需的配置因項目而異。
>
>請參閱Web控制台，瞭解所用值和有關參數的詳細資訊。

>[!NOTE]
>
>OSGi配置差異工具， [工AEM具](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)，可用於列出預設OSGi配置。

>[!NOTE]
>
>在中的特定功能區域可能需要進一步捆綁包AEM。 在這些情況下，可以在與相應功能相關的頁面上找到配置詳細資訊。

**復AEM制事件偵聽器** 配置：

* 的 **運行模式**，其中複製事件將分發到偵聽器。 例如，如果定義為作者，則系統將「啟動」複製。

* 運行模式 **發佈** 如果項目代碼在發佈環境中處理複製事件（反向複製），則需要添加。 例如，當調度程式用於從發佈環境刷新時，或當標準複製到其他發佈實例時。

**資AEM料庫更改偵聽器** 配置：

* 的 **路徑**，用於偵聽準備分發的儲存庫事件的位置。

**CRX Sling客戶端儲存庫** 配置對基礎內容儲存庫的訪問。

* 的 **管理員密碼** 應在安裝後更改以確保 [安全](/help/sites-administering/security-checklist.md) 你的例子。
* 其他更改不應是必需的，而且必須謹慎，因為它們可能影響對儲存庫的訪問。

**維客郵件服務** 為Wiki發送的電子郵件配置電子郵件設定。

**Apache Felix OSGi管理控制台** 配置：

* **插件**，要在 **Apache Felix Web管理控制台** 作為頂級菜單項。 禁用您不需要的任何內容，因為每個內容都需要空間和資源。

>[!CAUTION]
>
>請確保配置以下內容：
>
>**用戶名** 和 **密碼**，用於訪問Apache Felix Web管理控制台本身的憑據。
>初始安裝後必須更改密碼，以確保 [安全](/help/sites-administering/security-checklist.md) 你的例子。

>[!NOTE]
>
>在儲存庫可用之前，應根據啟動時的需要使用Felix控制台進行此配置。

**Apache Sling可自定義請求資料記錄器** 配置：

* **記錄程式名稱** 和 **日誌格式** 配置請求和訪問記錄的位置和格式(預設值： `request.log`)。 在分析與Web鏈相關的效能或調試功能時，此日誌檔案至關重要。
這與 [Apache Sling請求記錄器](#apacheslingrequestlogger)。

有關詳細資訊，請參閱 [記AEM錄](/help/sites-deploying/configure-logging.md) 和 [Sling日誌記錄](https://sling.apache.org/site/logging.html)。

**Apache Sling事件線程池** 配置：

* **最小池大小** 和 **最大池大小**，用於保存事件線程的池大小。

* **隊列大小**，如果池已用完，則線程隊列的最大大小。
建議的值為 `-1` 將隊列設定為無限制；如果設定了限制，則超出限制時可能會發生損失。

* 更改這些設定有助於在事件數量較多的情況下實現效能；例如，DAM或AEMWorkflow的使用量很大。
* 應使用test建立特定於方案的值。
* 這些設定可能會影響實例的效能，因此不要在沒有原因和適當考慮的情況下更改它們。

**Apache SlingGETServlet** 配置呈現的某些方面：

* **自動索引** 啟用/禁用目錄呈現以進行瀏覽。
* **啟用** （或禁用）預設格式副本，如 **HMTL**。 **純文字檔案**。 **JSON** 或 **XML**。
不應禁用JSON。

>[!NOTE]
>
>如果您在中運行，則會自動為生產實例配AEM置此設定 [生產就緒模式](/help/sites-administering/production-ready.md)。

**Apache Sling Java指令碼處理程式** 將.java檔案編譯為指令碼(servlet)的設定配置為。

某些設定可能會影響效能，應盡可能禁用這些設定，尤其是對於生產實例。

* S **源虛擬機** 和 **目標虛擬機**，將JDK版本定義為用作運行時JVM的版本

* 對於生產實例：

   * 禁用 **生成調試資訊**

**Apache Sling JCR安裝程式** 這些參數可能不需要配置，但在開發或調試時可能有助於瞭解。 例如，安裝資料夾對於檢入/檢出或建立包非常有用。

* **安裝資料夾名稱regexp** 和 **安裝資料夾的最大層次結構深度**  — 指定搜索儲存庫資料夾的位置和深度以查找要安裝的資源。 使用通配符時(如。*/install將搜索所有相應匹配項，例如， `/libs/sling/install` 和 `/libs/cq/core/install`。

* **搜索路徑**,jcrinstall搜索要安裝的資源的路徑清單，以及一個表示該路徑的加權因子的數字。

**Apache Sling作業事件處理程式** 配置管理作業計畫的參數：

* **重試間隔**。 **最大重試次數**。 **最大並行作業數**。 **確認等待時間**&#x200B;其中包括：

* 更改這些設定可以提高大量作業情況下的效能；例如，大量使用AEMDAM和工作流。
* 應使用test建立特定於方案的值。
* 不要無故更改這些設定，只要經過適當考慮後更改。

**Apache Sling JSP指令碼處理程式** 為JSP指令碼處理程式配置與效能相關的設定。 要提高效能，應盡可能禁用。

特別是生產實例：

* 禁用 **生成調試資訊**
* 禁用 **保留生成的Java**
* 禁用 **映射內容**
* 禁用 **顯示源片段**

>[!NOTE]
>
>如果您在中運行，則會自動為生產實例配AEM置此設定 [生產就緒模式](/help/sites-administering/production-ready.md)。

**Apache Sling日誌記錄配置** 配置：

* **日誌級別** 和 **日誌檔案**，以定義中央日誌配置的位置和日誌級別(error.log)。 級別可設定為以下級別之一 `DEBUG`。 `INFO`。 `WARN`。 `ERROR` 和 `FATAL`。

* **日誌檔案數** 和 **日誌檔案閾值** 定義日誌檔案的大小和版本旋轉。

* **消息模式** 定義日誌消息的格式。

有關詳細資訊，請參閱 [記AEM錄](/help/sites-deploying/configure-logging.md#global-logging) 和 [Sling日誌記錄](https://sling.apache.org/site/logging.html)。

**Apache Sling日誌記錄記錄器配置（工廠配置）** 配置：

* **日誌級別**。 **日誌檔案** 和 **消息格式** 定義日誌檔案和消息的詳細資訊。

* **記錄器** 定義類別；例如，僅記錄com.day.cq的日誌。

* 使用 **工廠配置**，可以添加任何數量的其他配置以滿足所需的各種日誌級別和類別。
* 這種配置在開發過程中很有幫助；例如，將特定服務的TRACE消息記錄到特定日誌檔案中。
* 此類配置在生產環境中非常有用；例如，將有關特定服務的消息記錄到單個日誌檔案中，以便更方便地進行監視。

有關詳細資訊，請參閱 [記AEM錄](/help/sites-deploying/configure-logging.md) 和 [Sling日誌記錄](https://sling.apache.org/site/logging.html)。

**Apache Sling日誌記錄寫入程式配置（工廠配置）** 配置：

* **日誌檔案** 定義日誌檔案的存在。
* **日誌檔案數** 來修改標籤元素的屬性。

* 該寫入程式可由 **Apache Sling日誌記錄器配置** 配置。

* 這種配置在開發過程中很有幫助；例如，將特定服務的TRACE消息記錄到特定日誌檔案中。
* 此類配置在生產環境中非常有用；例如，將有關特定服務的消息記錄到單個日誌檔案中，以便更方便地進行監視。

有關詳細資訊，請參閱 [記AEM錄](/help/sites-deploying/configure-logging.md) 和 [Sling日誌記錄](https://sling.apache.org/site/logging.html)。

**Apache Sling主Servlet** 配置：

* **每個請求的呼叫數** 和 **遞歸深度** 以保護系統免受無限遞歸和過多指令碼調用的影響。

**Apache Sling MIME類型服務** 配置：

* **MIME類型** 將項目所需的內容添加到系統。 這允許 `GET` 檔案上的請求，以設定用於連結檔案類型和應用程式的正確內容類型標頭。

**Apache Sling引用篩選器** 要解決CRX WebDAV和Apache Sling中的跨站點請求偽造(CSRF)的已知安全問題，您需要配置引用過濾器。

引用篩選器服務是OSGi服務，允許您配置：

* 應過濾哪些http方法
* 是否允許空的引用器標頭
* 以及除伺服器主機外允許的伺服器清單。

查看 [安全檢查表 — 跨站點請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 的上界。

>[!NOTE]
>
>Apache Sling引用過濾器取決於快速修復軟體包的安裝。

**Apache Sling請求記錄器** 配置：

* 定義請求記錄方式的各種參數。
* **啟用請求日誌**，以啟用或禁用。

* **啟用訪問日誌**，以啟用或禁用。

這與 [Apache Sling可自定義請求資料記錄器](#apacheslingcustomizablerequestdatalogger)。

有關詳細資訊，請參閱 [記AEM錄](/help/sites-deploying/configure-logging.md) 和 [Sling日誌記錄](https://sling.apache.org/site/logging.html)。

**Apache Sling資源解析器工廠** 配置Sling資源解決的中心方面：

* **資源搜索路徑**(s)，添加任何項目特定路徑（但不刪除） `/libs` 或 `/apps`)。

* **虛擬URL** 定義虛榮型URL映射。

* **URL映射** 定義任何別名；例如，從 `/content` 至 `/`。

* **映射位置**，映射器配置外部化於 `/etc/map`。

* 使用本地安裝(例如，使用 `https://localhost:4502/system/console/jcrresolver`)以確定哪個資源解析程式處於活動狀態。

有關詳細資訊，請參閱： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution)。

>[!CAUTION]
>
>特別是，必須在儲存庫中配置這些選項。
>
>否則，對 **URL映射** 下次啟動時，使用Felix控AEM制台可能會被覆蓋。

**Apache Sling Servlet/指令碼解析器和錯誤處理程式** Sling Servlet和指令碼解析器具有多個任務：

1. 它用作 `ServletResolver` 選擇要調用的Servlet或指令碼來處理請求。

1. 它充當 `SlingScriptResolver`。

1. 它通過實施 `ErrorHandler` 介面使用與用於解析請求處理servlet和指令碼相同的算法來選擇錯誤處理servlet和指令碼。

可以設定各種參數，包括：

* **執行路徑** 列出了搜索可執行指令碼的路徑；通過配置特定路徑，您可以限制可以執行哪些指令碼。 如果未配置路徑，則使用預設值( `/` = root)，這允許執行所有指令碼。
如果配置的路徑值以斜槓結尾，則搜索整個子樹。 如果沒有這樣的尾斜槓，則指令碼只有在完全匹配時才執行。

* **指令碼用戶**  — 此可選屬性可以指定用於讀取指令碼的儲存庫用戶帳戶。 如果未指定帳戶， `admin` 預設情況下使用用戶。

* **預設擴展** 將使用預設行為的擴展的清單。 這意味著資源類型的最後一個路徑段可以用作指令碼名稱。

**Day Commons GFX字型助手** 在渲染圖形時，可以使用DrawText嵌入文本。 為此，您還可以安裝您自己的字型：

* 定義 **字型路徑** 要搜索的項目特定字型。
比如說， `/apps/myapp/fonts`。

**Apache HTTP元件代理配置** 使用Apache HTTP客戶端（在建立HTTP時使用）的所有代碼的代理配置；例如，在複製時。

建立新配置時，不要更改工廠配置，而是使用此處提供的配置管理器為此元件建立新工廠配置： **https://localhost:4502/system/console/configMgr/**。 在中提供代理配置 **org.apache.http.proxyconfigurator。**

>[!NOTE]
>
>在AEM6.0和更早版本中，代理已在Day Commons HTTP客戶端中配置。 自AEM6.1及更高版本起，代理配置已移至「Apache HTTP Components Proxy Configuration」（Apache HTTP Components代理配置），而不是「Day Commons HTTP Client」（日公域HTTP客戶端）配置。

**第CQ天反垃圾郵件** 配置使用的反垃圾郵件服務(Akismet)。 這要求您註冊：

* **提供者**
* **API密鑰**
* **註冊的URL**

**Adobe花崗岩HTML庫經理** 將此配置為控制客戶端庫（css或js）的處理；比如，如何看待底層結構。

* 對於生產實例：

   * 啟用 **微型** （刪除CRLF和空格字元）。
   * 啟用 **吉普** （允許使用一個請求對檔案進行壓縮和訪問）。
   * 禁用 **調試**
   * 禁用 **計時**

* 對於JS開發（特別是當防火牆調試時）:

   * 禁用 **微型**
   * 啟用 **調試** 將檔案分離以進行調試並與firebug一起使用。
   * 啟用 **計時** 對時機的興趣。
   * 啟用 **調試** 控制台，查看JS控制台日誌消息。

>[!CAUTION]
>
>更改任一項的設定時 **微型** 或 **吉普** 您還需要刪除 `/var/clientlibs`。 這是客戶端的快取版本，將在下次請求時重新生成。

>[!NOTE]
>
>如果您在中運行，則會自動為生產實例配AEM置此設定 [生產就緒模式](/help/sites-administering/production-ready.md)。

**第CQ HTTP標頭身份驗證處理程式** HTTP請求的基本身份驗證方法的系統範圍設定。

使用時 [關閉的用戶組](/help/sites-administering/cug.md) 您可以配置（其中包括）:

* **HTTP領域**
* 的 **預設登錄頁**

**第CQ天連結檢查器服務** 檢查並在必要時配置：

* **計畫程式期間** 定義自動檢查外部連結的間隔。

* 檢查 **鏈路容差間隔錯誤** 不成功的外部連結被認為損壞的時間段。
* **連結檢查覆蓋模式**，以定義要從連結檢查中排除的任何路徑。

**第CQ天連結檢查器任務** 配置單個連結檢查器任務（檢查外部連結的任務）的設定：

* 檢查中定義的間隔 **良好連結Test間隔** 和 **錯誤的連結Test間隔**

* 檢查連結時外部訪問所需的與Internet訪問代理和NTLM相關的各種參數。

**第CQ天郵件服務** 配置郵件伺服器的主機名和訪問詳細資訊。 請參閱「配置郵件服務」部分。

**第CQ MCM新聞簡報** 配置新聞稿中使用的各種設定。

**第CQ天根映射** 配置：

* **目標路徑** 定義請求到的位置 `/`」。

在中有兩個可用的UIAEM:

* 啟用觸摸的UI是標準UI
* 已棄用的經典UI仍然完全可操作

使AEM用根映射可以將要具有的UI配置為實例的預設值：

* 要將啟用觸摸的UI作為預設UI，請 **目標路徑** 應指向：

   ```
      /projects.html
   ```

* 將傳統UI作為預設UI **目標路徑** 應指向：

   ```
      /welcome.html
   ```

>[!NOTE]
>
>在標準安裝時，觸摸優化UI是預設UI。

**Adobe花崗岩SSO驗證處理程式** 配置單一登錄(SSO)詳細資訊；在企業作者設定中通常需要這些功能，通常與LDAP結合使用。

可以使用各種配置屬性：

* **路徑**
此身份驗證處理程式處於活動狀態的路徑。 如果此參數為空，則禁用驗證處理程式。 例如，路徑/將使驗證處理程式用於整個儲存庫。

* **服務排名**
OSGi Framework Service Ranking值用於指示調用此服務所使用的順序。 這是 
`int` 值，其中值越高，優先順序越高。
預設值為 `0`.

* **標題名稱**
可能包含用戶ID的標頭的名稱。

* **Cookie名稱**
可能包含用戶ID的Cookie的名稱。

* **參數名稱**
可能提供用戶ID的請求參數的名稱。

* **用戶映射**
對於選定用戶，從HTTP請求提取的用戶名可以替換為憑據對象中的另一個用戶名。 此處定義了映射。 如果用戶名 
`admin` 顯示在映射的任一側，將忽略映射。 請注意，字元&quot;=&quot;必須用前導字&quot;\&quot;轉義。

* **格式**
指示提供用戶ID的格式。 使用:

   * `Basic` 如果用戶ID以HTTP基本身份驗證格式編碼
   * `AsIs` 如果用戶ID是以純文字檔案提供的，或應按原樣使用任何規則運算式應用的值或任何規則運算式

**第CQ WCM日調試篩選器** 這在開發時非常有用，因為它允許在訪問頁面時使用尾碼，如？debug=layout。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout將提供開發人員可能感興趣的佈局資訊。

* 在生產實例上禁用此功能，以確保效能和安全性。

**第CQ WCM篩選器** 配置：

* **WCM模式**以定義預設模式。
* 在作者實例上，這可能是 `edit`。 `disable,preview` 或 `analytics`。
其它模式可以從側鍵或尾碼訪問 `?wcmmode=disabled` 可用於模擬生產環境。

* 在發佈實例上，必須將其設定為 `disabled` 以確保不能訪問其他模式。

>[!NOTE]
>
>如果您在中運行，則會自動為生產實例配AEM置此設定 [生產就緒模式](/help/sites-administering/production-ready.md)。

**第CQ WCM連結檢查器配置器** 配置：

* **重寫配置清單** 為基於內容的連結檢查器配置指定位置清單。 配置可以基於運行模式；這對於區分作者和發佈環境非常重要，因為連結檢查器設定可能不同。

**第CQ WCM頁面管理器工廠** 配置：

* **頁子樹激活檢查** 用戶（沒有複製權限）刪除或移動頁面（即使頁面未激活）。

**第CQ WCM頁處理器** 配置：

* **路徑**，系統在觸發頁面修改之前偵聽的位置清單 `jcr:Event`。

**Adobe頁面印象跟蹤器** 對於作者實例配置：

* **sling.auth要求**:將此屬性的值設定為 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此配置將允許對跟蹤服務進行匿名請求。

>[!NOTE]
>
>請參閱 [頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions) 的子菜單。

**第CQ WCM天頁統計資訊** 對於發佈實例配置：

* **發送資料的URL** 配置用於跟蹤頁面統計資訊的URL（如果跟蹤程式請求通過調度程式，該URL至關重要）;例如，預設值為 `https://localhost:4502/libs/wcm/stats/tracker`。

* **已啟用跟蹤指令碼** 啟用( `true`)或禁用( `false`)跟蹤指令碼包含在頁面中。 預設值為 `false`.

>[!NOTE]
>
>請參閱 [頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions) 的子菜單。

**第CQ WCM版本管理器** 控制是否以及如何在系統中管理版本：

* **激活時建立版本**，在標準安裝中啟用
* **啟用清除**

* **清除路徑**，搜索操作將搜索的路徑
* **隱式版本化路徑**，隱式版本控制處於活動狀態的路徑。

* **最大版本時間**，版本的最大年齡（以天為單位）

* **最大編號版本**，要保留的最大版本數

請參閱 [版本清除](/help/sites-deploying/version-purging.md) 的子菜單。

**第CQ天工作流電子郵件通知服務** 為工作流發送的通知配置電子郵件設定。

**CQ重寫器HTML解析器工廠**

控制CQ重寫器的HTML分析器。

* **要處理的附加標籤**  — 可以添加或刪除要由解析器處理的HTML標籤。 預設情況下，將處理以下標籤：A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD。
* **保留駱駝案例**  — 預設情況下，HTML分析器將駝峰（例如eBay）中的屬性轉換為低峰（例如ebay）。 您可以關閉此選項以保留駝峰案例屬性。 這在使用諸如Angular2等前沿框架時是有用的。

**日公共JDBC連接池** 配置對用作內容源的外部資料庫的訪問。

這是工廠配置，因此可以配置多個實例。

**Adobe CQ媒體DPS會話服務** 管理DPS會話以與發佈一起使用。

特別是，您可以定義 `dps.session.service.url.name`:預設值設定為 [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN重寫器** 必須確AEM保與CDN之間的通信，以便以安全的方式將資產/二進位檔案遞送給最終用戶。 這涉及兩個任務：

* 最初(或在緩AEM存中過期後)通過CDN訪問資源。
* 安全地訪問在CDN中快取的資源，因為一旦資源在CDN中快取，請求將不會轉到AEMCDN中，應從CDN為所有有權訪問該資源的用戶提供服務。

提AEM供了將內部資產URL重寫到外部CDN URL的重寫器。 它重寫要傳遞到CDN的連結，包括JWS簽名和過期時間，以允許安全訪問資產。 此功能將用於作者實例。

總體流程如下：

1. 用戶使用資AEM產驗證並請求頁面。
1. 請求的頁面包含類似於 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 重寫器將連結轉換為包含JWS簽名的CDN URL:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然後，用戶的瀏覽器將資產請求轉發到CDN伺服器
1. 應將CDN配置為將請求與AEMCDN一起轉發 `cdn_sign` 的下界。
1. 驗證處理程式驗證 `cdn_sign` 參數並返回資產到CDN，然後將其交付給用戶

用戶瀏覽器、CDN之間的流，可AEM以如下顯示。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>當前僅為作者實例啟AEM用此功能。

**CDNConfigServiceImpl** 提供CDN配置

通過提供CDN重寫功能，可以啟用CDN重寫功能 **CDN分發域名** 在com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的配置中。

該服務還包含其他配置選項，如啟用/禁用CDN重寫、執行CDN重寫的路徑前置詞、TTL值和協定（HTTP或HTTPS）。

**CDNRewriter** 用於將內部影像URL重寫到CDN URL的重寫器

的 **標籤屬性** 可以定義com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的值，以便只重寫選擇性影像連結。
