---
title: 對AEM貢獻
seo-title: 對AEM貢獻
description: AEM是依據大型開放原始碼專案中常用的證實可行方法所開發
seo-description: AEM是依據大型開放原始碼專案中常用的證實可行方法所開發
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 對AEM貢獻{#contributing-to-aem}

## 開發方法 {#development-methodology}

AEM是依據大型開放原始碼專案中常見的證實可行方法所開發。 事實上，AEM技術堆疊中的許多核心元素都維持為主動開放原始碼專案，例如Sling和Jackrabbit，這些專案是Apache Software Foundation的貢獻者。 AEM中呈現此精神的主要方面，是建議您使用可用的郵寄清單和線上論壇，以直接與開發團隊互動。

如果您要貢獻AEM的元件，您應像貢獻開放原始碼專案時一樣熟悉AEM，並像您打算為此類專案貢獻時一樣與現有核心團隊溝通。

## 所需體驗 {#required-experience}

超文本傳輸協定(HTTP)是我們所做一切的核心。 因此，在對AEM做貢獻之前，您應該對HTTP有深入的瞭解，最理想的情況是，您可以在具有執行緒集區的情況下，編寫自己的多執行緒HTTP伺服器Java實作。 您也應瞭解HTTP/1.1的「保持活動」行為，並深入瞭解伺服器／用戶端與JavaScript的互動，尤其是AJAX所呈現的非同步互動樣式。

由於頁面活力和互動式內容是WM體驗的關鍵，因此您必須對「檔案物件模型」及其在回應事件時的程式化控制潛力有相當深入的瞭解。 例如，您應該對多個瀏覽器檔案（例如使用iframe）上的即時DOM操作和拖放行為有一定的知識。

那麼，在最高層面，您應該對以下幾點有紮實的瞭解：

* [HTTP/1.1通訊協定](https://www.ietf.org/rfc/rfc2616.txt)
* HTML(最好 [是HTML5](https://dev.w3.org/html5/spec/Overview.html))
* 階層式樣式表
* 可擴充標籤語言(XML)
* 非同步JavaScript和XML(AJAX)設計模式
* JavaScript物件符號(JSON)
* 文檔對象模型
* 狀態式與無狀態互動
* [統一資源標識符](https://www.ietf.org/rfc/rfc2396.txt)
* 瀏覽器Cookie
* 和其他現代網路開發概念

Adobe Experience manager的技術堆疊是以 [Apache Felix](https://felix.apache.org/) OSGI容器與 [Apache Sling](https://sling.apache.org/site/index.html) web framework為基礎，並內嵌以Apache Jackrabbit Ackrabbit Chorgbit Content Repository([](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)[](https://jackrabbit.apache.org/jcr-api.html)JCR)。 您應熟悉這些個別專案，以及您要貢獻的區域中使用的任何其他開放原始碼元件（例如Apache Lucene）。

## 部落知識 {#tribal-knowledge}

某些概念和指導原則在前日文化中根深蒂固。 本節列出您應注意的「深入內嵌DNA」問題。

### 一切都是內容 {#everything-is-content}

內容不僅包含Web應用程式持續存在的所有資料。 程式碼、程式庫、指令碼、範本、HTML、CSS、影像和各種物件，一切都會保存在內容儲存庫中，並透過Package Manager和Package Share以套件的形式匯入／匯出。

### David&#39;s Model {#david-s-model}

在Java內容儲存庫中建立內容模型的方式，需要與軟體產業在關係世界中建立資料模型時的常見做法完全不同的思考方式。 JCR方式對於任何新進內容管理人員而言，必 [要的閱讀方式是David&#39;s Model:內容建模指南](https://wiki.apache.org/jackrabbit/DavidsModel)。

### 休息 {#restfulness}

REST方針已深植於我們的工作之中。 這意味著，除其他外，避免有狀態的交互，並記住URI是內容和服務的最終地址。

REST（REpresentational State Transfer，簡稱REST）是指World Wide web所基礎的軟體體系結構樣式。 它說明了使Web運作的關鍵要素，因此為如何設計基於Web的軟體提供了一套原則。 當設計要在網路上使用的API時，遵循這些「最佳實務」是明智的。

由於REST提供了我們許多工作背後的指導理念，因此您應認為必須熟悉REST風格設計的原則。 從羅伊·菲爾丁的論 [文開始說](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)。

### Sling Request Resolution {#sling-request-resolution}

要瞭解AEM的主要方面是傳入請求如何與內容和應用程式行為相關、內容存放庫中的內容結構，以及AEM在何處尋找應用程式邏輯來處理請求。 瞭解Apache [Sling URL分解](https://sling.apache.org/site/url-decomposition.html) ，以及它執行REST架構樣式及其無狀態、可快取和分層系統限制的方式。

要瞭解Apache Sling請求解析度的主要方面是，請求主要如何對應至內容存放庫中的特定資源、請求的其他屬性以及這些內容物件的屬性，如何決定要呼叫哪些應用程式碼來轉換內容，以及/apps中的程式碼如何覆寫/libs中的程式碼。

### 快速入門 {#quickstart}

沒有步驟三：要安裝和運行，只需下載並按兩下Quickstart JAR檔案。 沒有第三步。 任何其他可選功能都只需要從Package Share安裝適當的套件。

小型快速入門：將快速啟動JAR檔案的大小保持在最小。 智慧、最佳化地使用程式庫，移動選用功能以封裝共用。

更快的啟動時間：當您進行可能影響啟動時間的變更時，請確定變更會縮短，而非延長。

### 精益求精 {#lean-and-mean}

我們偏好輕巧、小巧、快速且精美的程式碼和專案。 「夠好」還不夠好。

程式碼重複使用：我們以OSGi為基礎的產品架構，以及「一切就是內容」的理念，意味著我們有絕佳的機會重複使用程式碼和產品。 我們盡量利用這個事實，保持功能的精簡和均衡。

松耦合：我們更青睞鬆散耦合的互動，而非緊密依賴和「不想要的親密關係」。 鬆散的耦合也可讓程式碼重複使用。

### 不要破壞示範程式 {#don-t-break-the-demo}

熟悉示範程式中最常顯示的示範指令碼和產品功能。 瞭解您至少不應中斷「示範指令碼」功能。 核心產品應隨時都可進行示範，即使在開發期間亦然。

### 可靠性設計 {#design-for-reliability}

我們致力於以失敗軟體方式設計和編碼功能，以便（例如）單一DOM元素的問題不會造成整個頁面無法轉換。 換句話說：製造致命的東西。 讓其他一切都能生存。 讓產品「寬容」。

### 異常是新常態 {#abnormal-is-the-new-normal}

不要依賴關閉掛接，確保啟動時清理。 異常終止是正常終止。

`shutdown == kill -9 == power outage`

### 準備好進行彈性聚類 {#be-ready-for-elastic-clustering}

隨時準備進行彈性聚類，始終假設存在聚類。 一般而言，遵守內容儲存庫中的一切意味著內建叢集支援。

### 向後相容性設計 {#design-for-backward-compatibility}

您所做的一切都不應破壞客戶的舊程式碼。 請考慮 `/libs` 僅包含可在升級期間更新的產品代碼。 儲存 `/apps` 庫的部分是項目代碼，該部分 `/etc` 包含需要保留的自定義配置。 通常，請勿覆寫和 `/apps`中的 `/content` 任何內 `/home`容。 升級後，舊專案程式碼、組態和內容應繼續運作，就像升級前所做的一樣。

為向後相容而設計，也可確保升級體驗符合初始安裝的簡單性。 只要停止AEM、取代Quickstart JAR檔案，並啟動AEMagain，就夠了。 隨著安裝群的快速成長，升級效率將日益顯著。

雖然現有的API可在較新時或應該標示為已停用，但更好的功能會取代它們，但在舊版5.x版本中公開的所有API都必須保持運作，因為它們可能正用於自訂應用程式碼中。 不應移除此類API。

在內容結構與使用者體驗的一致性方面，也應牢記向後相容性。

## 核心概念 {#core-concepts}

**作者例項** -通常為了安全性、治理和其他原因，生產網站會將AEM的例項分為「作者」和「發佈」例項。 如需部署架構（包括作者／發佈例項）的詳細資訊，請參閱「AEM例項」相關檔案。

**快取、煎炸和烘焙** -傳統上，烘焙和煎炸的概念是不同Web內容管理系統之間的重要區別。 在CMS術語中，「烘焙」是指在發佈時將資料提交至靜態檔案的概念，而「煎炸」則指在要求時處理資料以進行最終呈現的概念（即即及時）。

**叢集與負載平衡** -為了提高生產環境的可用性並改善其效能，通常會將多個作者與／或發佈例項（整合至叢集）結合，方法是讓不同的使用者群組使用這些例項，或是在Dispatcher組態後進行負載平衡。

您也可以結合內容儲存庫的多個執行個體來建立高可用性 ** JCR解決方案，然後與您的AEM解決方案整合，以針對硬體和軟體故障提供最大的保護。 如需詳 [細資訊](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) ，請參閱建議的部署。

**Component** —— 在AEM中，Component是物件類型，通常可從Sidekick等拖放來建立其例項。 例如，隨附AEM的現成可用元件包括「文字」、「標題」、「標籤雲端」、「轉盤」、「影像」和「清單」元件，這些元件都可從Sidekickat執行時期取得。

**內容搜尋器** -在製作模式中，內容搜尋器是頁面左側的特殊面板（畫格），根據您在頂端選取的標籤，可顯示影像、檔案、Flash資產、頁面、段落或儲存庫資源清單，您可從Content Finder拖放至您正在處理的頁面（位於右側）。

**數位資產** -在AEM中，數位資產（通常）是影像和多媒體檔案。 如需詳細資訊，請參閱「在DAM中使用數位資產」。

**Dispatcher** - Dispatcher既是快取和負載平衡工具，也提供了某些安全性保障。

**ExtJS Widgets** - AEM中大部分的使用者介面元素都使用ExtJS，這是以JavaScript編寫的協力廠商Widget程式庫。 ExtJS具備高效能、可自訂的UI Widget和設計精良且可擴充的元件模型。

**JCR,Java Content Repository** - Java Content Repository規範(JSR-283)提供了抽象資料模型和應用程式寫程式介面，用於實現結合檔案系統和對象資料庫的功能的可擴展的NoSQL資料儲存庫。 雖然您不需要詳盡地瞭解JSR-283，但您應該花點時間熟悉JCR的基本功能及其基礎的資料模型，因為JCR是AEM的「一切就是內容」哲學的可能。

JCR本質上是一個節點和屬性的系統，節點可以從其他節點繼承，所有內容都儲存為屬 *性值*。 請注意，除了普通繼承外，JCR還允許「mixin」節點的概念，它允許對多個繼承進行建模。

JCR具有許多預定義的節點類型和屬性類型，但通常鍵入系統相當靈活，而且（事實上）JCR的優勢之一是它允許以同樣簡單的方式儲存／管理結構化和非結構化內容。 也就是說，JCR可以容納高結構化的資料，但也可以容納任意的動態資料結構，而沒有模式約束。

JCR的Java API適用的JavaDoc就在這 [里](http://jackrabbit.apache.org/jcr/jcr-api.html)。

在嘗試閱讀JavaDoc或JCR規格本身之前，您可能想要檢視由Adobe Experience services實 [施的JCR的這個高階說明](/help/sites-developing/the-basics.md#java-content-repository) 。

**Multi-Site Manager(MSM)** - AEM的MSM功能可協助客戶處理多語言和跨國內容，讓他們在集中品牌與本地化內容之間取得平衡。

**OSGi** - OSGi是以服務為基礎的執行時期技術，為AEM中的模組化Java開發提供基礎。 此架構不僅為程式碼資源（稱為搭售）提供高度動態（且安全）的類別載入和執行環境，還能完全控制搭售所揭露的各種服務的可見性和生命週期。 服務註冊表為考慮生命週期動態（和版本要求）的捆綁包提供了合作模型。 OSGi解決了許多應用程式伺服器原本要解決的問題，但是以輕量型、高動態的方式解決，例如，讓熱部署服務（讓新程式碼立即可用，而不需重新啟動伺服器）成為可能。

**Parsys, Paragraph System** —— 段落系統(parsys)是一種複合元件，允許作者將不同類型的元件添加到頁面並包含其他段落元件。 每個段落類型都表示為元件。 段落系統本身也是一個組成部分，其中包含其他段落部分。

**Microkernel** —— 儲存庫中的每個工作區都可以單獨配置，以通過特定微內核（管理資料讀寫的類）儲存其資料。 同樣地，整個儲存庫版本儲存也可以獨立配置為使用特定微內核。 有許多不同的微內核，能夠以各種檔案格式或關係資料庫儲存資料。 （例如，MongoDB、DB2或Oracle有永續性管理器）AEM的預設微內核是TarMK（請參閱下面的進一步說明）。

**發佈例項** -出於安全性、治理和其他原因，生產網站通常會將AEM的例項分為「作者」和「發佈」例項。 如需部署架構（包括作者／發佈例項）的詳細資訊，請參閱「AEM例項」相關檔案。

**Quickstart** —— 與許多其他程式不同，您使用單一「Quickstart」自解壓JAR檔案來安裝AEM。 首次按兩下JAR檔案時，將自動安裝所需的所有內容。 快速入門JAR包含CRX儲存庫（包括管理設施）、虛擬儲存庫服務、索引與搜尋服務、工作流程服務、安全性和Web伺服器所需的所有檔案，以及CQ Servlet引擎(CQSE)和所有AEM服務。 沒有其他檔案可以安裝：快速入門是自成一體的。

首次啟動快速入門時，它會在後台建立一個與JCR相容的整個儲存庫，需要幾分鐘的時間。 在初次啟動後，隨後的初創公司會更快，因為儲存庫基礎架構已經到位。

許多啟動選項(例如作用中的埠號，以及相關的AEM例項是否應為「發佈」例項，還是「作者」例項；等等)可通過適當更名快速啟動檔案來控制。 要查看相關選項清單，請在命令行上運行帶有&quot;-help&quot;的JAR:

```shell
java -jar <quickstartfilename>.jar -help
```

**複製代理** -複製代理是AEM的中心，作為將內容從作者發佈（啟動）至發佈環境的機制；從Dispatcher快取中刷新內容；將使用者產生的內容（例如，表單輸入）從「發佈」環境傳回至「作者」環境。

**支架** -您可以使用支架建立表單（支架），其中欄位可反映您所要的頁面結構，然後使用此表單輕鬆建立以此結構為基礎的頁面。

**區段** -網站訪客在進入網站時有不同的興趣和目標。 瞭解訪客的目標並滿足其期望是線上行銷的重要成功先決條件。 區段可透過分析和表徵訪客的詳細資料，協助達成此目標。

**Sidekick** - Sidekick是浮動視窗，會顯示在可編輯的頁面上，可從中拖曳新元件，並執行套用至頁面的動作。

**Site Catalyst** - SiteCatalyst為行銷人員提供一個位置，可測量、分析和最佳化來自多個行銷通道上所有線上活動的整合資料。 您可以使用Adobe SiteCatalyst來分析AEM網站的資料。

**Tar Storage(TarMK)** - TarMK是AEM中的預設永續性系統。 雖然AEM可設定為使用不同的永續性系統（例如MongoDB），但TarMK具有特定優點，因為它針對一般的JCR使用案例進行效能最佳化（因此速度非常快）、使用業界標準資料格式，而且可快速且輕鬆地備份。

**範本** -在AEM中，範本會指定特定頁面類型。 它定義頁面的結構（同時通常也指定縮圖影像和各種屬性）。 例如，您可能有個別的產品頁面、網站地圖和連絡資訊範本。

**Workflow** - AEM Workflow系統可讓您建立包含頁面或資產的自動化程式。
