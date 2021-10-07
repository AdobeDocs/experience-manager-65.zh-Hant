---
title: 貢獻AEM
seo-title: Contributing to AEM
description: AEM的開發遵循了在大型開放原始碼項目中通常採用的行之有效的方法
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 0%

---

# 貢獻AEM{#contributing-to-aem}

## 開發方法 {#development-methodology}

AEM是依照大型開放原始碼專案中常用的實證方法而開發。 AEM技術堆疊中的許多核心元素實際上都維持為作用中的開放原始碼專案，例如Sling和Jackrabbit，這是Apache Software Foundation的貢獻者。 AEM中呈現此精神的一個主要方面是，我們鼓勵您利用現有的郵寄清單和線上論壇，與開發團隊直接互動。

如果您要貢獻AEM的元件，應像貢獻開放原始碼專案時一樣熟悉AEM，並像要貢獻此專案時一樣與現有核心團隊溝通。

## 必要體驗 {#required-experience}

HyperText傳輸協定(HTTP)是我們所做的一切的核心。 因此，在對AEM作出貢獻之前，您應該對HTTP有深入的了解，最好能夠編寫具有線程池的多線程HTTP伺服器的Java實施。 您也應該了解HTTP/1.1保持運作的行為，並且應深入了解伺服器/用戶端與JavaScript的互動，尤其是AJAX所代表的非同步互動樣式。

因為頁面活力和互動式內容是WM體驗的關鍵，因此您必須對文檔對象模型及其在響應事件時進行程式設計操作的潛力有相當深入的了解。 您應該具備一些相關知識，例如對多個瀏覽器檔案（例如使用iframe）進行即時DOM操作和拖放行為。

那麼，在最高層面，您應該對以下事項有紮實的了解：

* [HTTP/1.1協定](https://www.ietf.org/rfc/rfc2616.txt)
* HTML(優選[HTML5](https://dev.w3.org/html5/spec/Overview.html))
* 級聯樣式表
* 可擴展標籤語言(XML)
* 非同步JavaScript和XML(AJAX)設計模式
* JavaScript物件標籤法(JSON)
* 文檔對象模型
* 有狀態與無狀態互動
* [統一資源標識符](https://www.ietf.org/rfc/rfc2396.txt)
* 瀏覽器Cookie
* 和其他現代網路開發概念

Adobe Experience Manager的技術堆疊是以[Apache Felix](https://felix.apache.org/)具有[Apache Sling](https://sling.apache.org/site/index.html)網頁架構的OSGI容器為基礎，並內嵌以[Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html)為基礎的Java內容存放庫([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html))。 您應熟悉這些個別專案，以及您要貢獻內容區域中使用的任何其他開放原始碼元件（例如Apache Lucene）。

## 部落知識 {#tribal-knowledge}

某些概念和指導原則深深地植根於前日文化。 本節列出您應注意的「深入內嵌DNA」問題。

### 一切都是內容 {#everything-is-content}

內容不僅包含Web應用程式持續存在的所有資料。 程式碼、程式庫、指令碼、範本、HTML、CSS、影像和各種成品、任何項目和所有項目都會保存在內容存放庫中，並透過封裝管理器和封裝共用以封裝形式匯入/匯出。

### 大衛的模型 {#david-s-model}

在Java內容儲存庫中建立內容模型的方式，需要的思維方式與在關係世界中建立資料模型的軟體行業中的常見做法完全不同。 對於任何進入內容管理的新來者而言，JCR方式是[David的模型：內容模型](https://wiki.apache.org/jackrabbit/DavidsModel)的指南。

### RESTnitys {#restfulness}

REST方法在我們的工作中根深蒂固。 這意味著，除其他外，避免有狀態的交互，並記住URI是內容和服務的最終地址。

REST(REpresentational State Transfer)是指萬維網所基於的軟體體系結構風格。 它描述了使Web工作的關鍵要素，因此為如何設計基於Web的軟體提供了一套原則。 因此，在設計要在網路上使用的API時，遵循這些「最佳實務」是明智的。

因為REST為我們所做的許多工作提供了指導性理念，因此您應認為必須精通RESTful設計的原則。 從[羅伊·菲爾丁的論文](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)開始，是一個很好的起點。

### Sling要求解決方法 {#sling-request-resolution}

要了解AEM的一個關鍵方面是傳入請求如何與內容和應用程式行為相關、內容存放庫中的內容結構，以及AEM在何處尋找應用程式邏輯以處理請求。 了解Apache [Sling URL分解](https://sling.apache.org/site/url-decomposition.html)及其強制REST架構樣式及其無狀態、可快取和分層系統限制的方式。

要了解Apache Sling請求解析的主要方面，是請求如何主要對應至內容存放庫中的特定資源、請求的其他屬性，以及這些內容物件的屬性，如何判斷要叫用哪個應用程式代碼來轉譯內容，以及/apps中的程式碼如何覆寫/libs中的程式碼。

### 快速入門 {#quickstart}

沒有第三步：要安裝和運行，只需下載並按兩下Quickstart JAR檔案即可。 沒有第三步。 任何其他可選功能只需從Package Share安裝適當的套件即可。

小型快速入門：將Quickstart JAR檔案的大小保持在最小。 智慧、最佳化地使用程式庫，移動選用功能以封裝共用。

更快的啟動時間：當您進行可能影響啟動時間的變更時，請確定變短，而不是變長。

### 精簡與平均 {#lean-and-mean}

我們偏好輕巧、小巧、快速、優雅的程式碼和項目。 「夠好」不夠好。

代碼重用：我們基於OSGi的產品架構和「一切都是內容」的理念意味著，我們擁有異常好的機會來重複使用代碼和成品。 我們盡量利用這一事實來保持功能的輕薄。

松耦合：我們更喜歡鬆散耦合的互動，而不是緊緊的依賴和「不想要的親密」。 松耦合還允許更多代碼重用。

### 不要破壞演示 {#don-t-break-the-demo}

熟悉最常顯示在示範中的示範指令碼和產品功能。 請至少了解，您不應破壞「示範指令碼」功能。 核心產品應一律為示範就緒，即使在開發期間亦然。

### 可靠性設計 {#design-for-reliability}

我們致力以失敗軟式方式設計和編碼功能，以免（例如）單一DOM元素的問題不會導致整個頁面無法呈現。 換句話說：製造致命的東西。 讓其他一切都能生存下來。 讓產品「原諒」

### 異常是新常態 {#abnormal-is-the-new-normal}

不依賴關閉掛接，確保啟動時清理。 異常終止是正常終止。

`shutdown == kill -9 == power outage`

### 為彈性聚類做好準備 {#be-ready-for-elastic-clustering}

始終準備進行彈性聚類，總是假設存在聚類。 一般而言，遵守內容存放庫中的所有內容，都表示內建叢集支援。

### 後向相容性設計 {#design-for-backward-compatibility}

您所做的任何事都不應破壞客戶的舊代碼。 請僅考慮`/libs`包含可在升級期間更新的產品代碼。 存放庫的`/apps`區段是專案程式碼，而`/etc`區段包含需要保留的自訂設定。 通常，請勿覆寫`/apps`、`/content`和`/home`中的任何內容。 升級後，舊專案程式碼、設定和內容應可繼續如升級前所做般運作。

設計回溯相容性還可確保升級體驗與初始安裝的簡單性相符。 只需停止AEM、取代Quickstart JAR檔案並重新啟動AEMacain即可。 隨著安裝基礎的快速增長，升級效率將成為一項日益顯著的優勢。

雖然現有API可在較新時或應該標示為已過時，但功能較完善的API可取代，但在先前5.x版本中公開的所有API都必須保持功能，因為它們可能正在自訂應用程式程式碼中使用。 不應移除此類API。

對於內容結構和使用者體驗的一般一致性，也應謹記回溯相容性。

## 核心概念 {#core-concepts}

**製作例項**  — 基於安全性、控管和其他原因，生產網站通常會將AEM的例項分為製作和發佈例項。如需部署架構（包括製作/發佈例項）的詳細資訊，請參閱AEM例項相關檔案。

**快取、油炸和烘焙**  — 傳統上，烤和油炸的概念是不同Web內容管理系統之間的重要區別。在CMS術語中，「烘焙」是指在發佈時將資料提交至靜態檔案的概念，而「煎炸」是指在請求時（即及時）處理資料以進行最終演示的概念。

**叢集和負載平衡**  — 為了提高可用性並改善生產環境的效能，通常會結合多個製作和/或發佈執行個體（放入叢集），方法是讓不同的使用者群組都能使用這些執行個體，或在Dispatcher設定後進行負載平衡。

還可以結合內容儲存庫的多個實例來建立&#x200B;*高可用性* JCR解決方案，然後可與您的AEM解決方案整合，以最大限度地保護系統免受硬體和軟體故障的影響。 如需詳細資訊，請參閱[建議部署](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) 。

**元件**  — 在AEM中，元件是物件類型，通常可從Sidekick等項目拖放來建立例項。因此，例如隨AEM提供的現成元件包括文字、標題、Tag Cloud、輪播、影像和清單元件，這些元件都可在執行階段從Sidekick取得。

**內容尋找器**  — 在製作模式中，「內容尋找器」是頁面左側的特殊面板（框架），根據您在頂端選取的索引標籤，可顯示影像、檔案、Flash資產、頁面、段落或存放庫資源清單，您可從「內容尋找器」將這些資源拖放至您正在使用的頁面（位於右側）。

**數位資產**  — 在AEM中，數位資產通常為影像和多媒體檔案。如需詳細資訊，請參閱在DAM中使用數位資產。

**Dispatcher**  - Dispatcher既是快取與負載平衡工具，也提供特定安全性保障。

**ExtJS Widget**  - AEM中大部分的使用者介面元素都會使用ExtJS，這是以JavaScript撰寫的協力廠商Widget程式庫。ExtJS提供高效能、可自訂的UI Widget，以及設計精良且可擴充的元件模型。

**JCR、Java Content Repository**  - Java Content Repository規範(JSR-283)提供了抽象資料模型和應用程式設計介面，用於實現大規模可擴展的NoSQL資料儲存庫，該儲存庫將檔案系統和對象資料庫的功能結合在一起。雖然您不需要詳盡了解JSR-283，但您應花時間熟悉JCR的基本功能及其基礎資料模型，因為JCR是AEM的「一切都是內容」理念的源泉。

JCR本質上是一個節點和屬性的系統，節點可以從其他節點繼承，所有內容都儲存為屬性&#x200B;*values*。 請注意，除了一般繼承外，JCR還允許「mixin」節點的概念，這可以建立多個繼承的模型。

JCR有許多預定義的節點類型和屬性類型，但一般而言，鍵入系統相當靈活，而且（事實上）JCR的優勢之一是它允許以同樣的簡便方式儲存/管理結構化和非結構化內容。 也就是說，JCR可以容納高結構化資料，但也可以容納任意的動態資料結構而不受模式約束。

JCR的Java API的JavaDoc為[此處](http://jackrabbit.apache.org/jcr/jcr-api.html)。

在嘗試讀取JavaDoc或JCR規格本身之前，您可能想要查看由Adobe Experience Services實作的JCR的[這個高階說明](/help/sites-developing/the-basics.md#java-content-repository)。

**Multi-Site Manager(MSM)**  - AEM的MSM功能可協助客戶處理多語言和跨國內容，讓客戶在集中品牌與本地化內容之間取得平衡。

**OSGi**  - OSGi是以服務為基礎的執行階段技術，為AEM中模組化Java開發提供基礎。此架構不僅為程式碼資源（稱為套件）提供高度動態（且安全）的分類和執行環境，還可完整控制套件所公開各種服務的可見性和生命週期。 服務註冊表為考慮生命週期動態（和版本要求）的套件組合提供合作模型。 OSGi解決了應用程式伺服器希望解決的許多問題，但是卻以輕量、高度動態的方式解決了這些問題，例如，使熱部署服務（使新代碼立即可用而無需重新啟動伺服器）成為可能。

**Parsys, Paragh System**  — 段落系統(parsys)是複合元件，可讓作者將不同類型的元件新增至頁面，並包含其他段落元件。每個段落類型都以元件的形式表示。 段落制度本身也是一個組成部分，它包含其他段落部分。

**微內核**  — 儲存庫中的每個工作區都可單獨配置，以通過特定微內核（管理資料讀寫的類）儲存其資料。同樣，儲存庫範圍的版本儲存也可以獨立配置為使用特定微內核。 有許多不同的微內核可用，能夠以各種檔案格式或關係資料庫儲存資料。 (例如，存在MongoDB、DB2或Oracle的持久性管理器)AEM的預設微內核是TarMK（請參閱下面的進一步資訊）。

**發佈例項**  — 基於安全性、控管和其他原因，生產網站通常會將AEM的例項分為製作和發佈例項。如需部署架構（包括製作/發佈例項）的詳細資訊，請參閱AEM例項相關檔案。

**快速啟動**  — 與其他許多程式不同，您使用單個「快速啟動」自解壓JAR檔案來安裝AEM。第一次按兩下JAR檔案時，將自動安裝您需要的所有內容。 快速入門JAR包括CRX儲存庫（包括管理設施）、虛擬儲存庫服務、索引和搜索服務、工作流服務、安全性和Web伺服器所需的所有檔案，以及CQ Servlet引擎(CQSE)和所有AEM服務。 沒有其他檔案可以安裝：快速入門是獨立的。

第一次啟動Quickstart時，它會在後台建立整個符合JCR的儲存庫，這可能需要幾分鐘的時間。 在初次啟動後，隨後的啟動速度要快得多，因為儲存庫基礎架構已經建立。

許多啟動選項(例如作用中的連接埠號，以及相關的AEM例項是發佈例項還是製作例項；更多)可通過適當更名Quickstart檔案來控制。 要查看這方面的選項清單，請在命令行上運行帶有「 — help」的JAR:

```shell
java -jar <quickstartfilename>.jar -help
```

**復寫代理**  — 復寫代理是AEM的中心，作為用於從作者發佈（啟動）內容至發佈環境的機制；從Dispatcher快取排清內容；將使用者產生的內容（例如，表單輸入）從發佈環境傳回至製作環境。

**支架**  — 透過支架，您可以建立表單（支架），其欄位可反映您所需頁面的結構，然後使用此表單根據此結構輕鬆建立頁面。

**區段**  — 網站訪客來到網站時有不同的興趣和目標。了解訪客的目標並滿足其期望是線上行銷的重要成功先決條件。 分段透過分析訪客的詳細資料並加以特徵化，有助於達成此目標。

**Sidekick**  - Sidekick是顯示在可編輯頁面上的浮動視窗，可從中拖曳新元件，並執行套用至頁面的動作。

**Site Catalyst**  -SiteCatalyst可讓行銷人員在一個位置測量、分析和最佳化來自多個行銷管道之所有線上活動的整合資料。您可以使用Adobe SiteCatalyst來分析AEM網站的資料。

**Tar Storage(TarMK)**  - TarMK是AEM中的預設永續性系統。雖然AEM可配置為使用不同的持久系統（如MongoDB），但TarMK具有某些優點，即它針對典型JCR使用案例進行效能優化（因此速度非常快），使用行業標準資料格式，並且可以快速輕鬆地備份。

**範本**  — 在AEM中，範本會指定特定類型的頁面。它定義頁面的結構（同時通常也指定縮圖影像和各種屬性）。 例如，您可能有不同的產品頁面、網站地圖和聯絡資訊範本。

**工作流程**  - AEM工作流程系統可建立涉及頁面或資產的自動化流程。
