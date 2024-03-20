---
title: 協助撰寫AEM
description: AEM的開發遵循大型開放原始碼專案中經常使用的公認方法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2635'
ht-degree: 0%

---

# 協助撰寫AEM{#contributing-to-aem}

## 開發方法 {#development-methodology}

AEM的開發遵循大型開放原始碼專案中經常使用的公認方法。 AEM技術棧疊中的許多核心元素實際上是作為活躍的開放原始碼專案來維護的，例如Sling和Jackrabbit，這些專案都有貢獻於Apache Software Foundation。 此精神的一個主要方面出現在AEM中，即建議您使用可用的郵寄清單和線上論壇，與開發團隊直接互動。

如果您要協助撰寫AEM的元件，請像協助撰寫開放原始碼專案時一樣熟悉AEM，並像您打算協助撰寫這類專案一樣與現有核心團隊溝通。

## 所需體驗 {#required-experience}

HyperText傳輸通訊協定(HTTP)是我們所有工作的核心。 因此，在為AEM貢獻內容之前，您應該對HTTP有深入的瞭解，最好是能夠撰寫您自己的具有執行緒集區的多執行緒HTTP伺服器Java™實作。 您也應該瞭解HTTP/1.1保持連線行為，並且您應該深入瞭解伺服器端/使用者端與JavaScript的互動，特別是AJAX所代表的非同步互動樣式。

由於頁面動態和互動式內容是WM體驗的關鍵，因此您必須相當深入地瞭解檔案物件模型，及其回應事件的程式化操作的潛力。 您應該具備一些知識，例如即時DOM操作和在多個瀏覽器檔案上拖放的行為（例如使用iframe）。

在最高層級中，您應該對以下內容有深入的瞭解：

* 此 [http/1.1通訊協定](https://www.ietf.org/rfc/rfc2616.txt)
* HTML(最好是 [HTML5](https://html.spec.whatwg.org/))
* 階層式樣式表
* 可延伸標籤語言(XML)
* 非同步JavaScript和XML (AJAX)設計模式
* JavaScript物件標籤法(JSON)
* 檔案物件模型
* 有狀態與無狀態互動
* [統一資源識別碼](https://www.ietf.org/rfc/rfc2396.txt)
* 瀏覽器Cookie
* 和其他現代Web開發概念

Adobe Experience Manager的技術棧疊是根據 [Apache Felix](https://felix.apache.org/documentation/index.html) 具有的OSGI容器 [Apache Sling](https://sling.apache.org/index.html) 網頁框架並內嵌Java™內容存放庫([JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html))根據 [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/jcr-api.html). 請詳閱這些個別專案，以及您打算協助撰寫之區域中所使用的任何其他開放原始碼元件（例如Apache Lucene）。

## 部落知識 {#tribal-knowledge}

某些概念和指導原則已深深植根於舊日文化中。 本節列出您應留意的一些「深入的DNA嵌入」問題。

### 一切都是內容 {#everything-is-content}

內容不僅包含網頁應用程式儲存的所有資料。 程式碼、程式庫、指令碼、範本、HTML、CSS、影像和各種成品、任何專案及所有內容都會保留在內容存放庫中，並透過封裝管理程式和封裝共用以封裝形式匯入/匯出。

### David模型 {#david-s-model}

在Java™ Content Repository中模型化內容的方式，需要一種與軟體產業在關聯式世界中資料模型化的常見做法完全不同的思維方式。 對於任何內容管理的新手來說，JCR方法的關鍵讀數為 [David模型：內容模型指南](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTful {#restfulness}

REST方法深深根植於我們的作業中。 也就是說，除了其他以外，應避免狀態式互動，並記住URI是內容與服務的明確位址。

REST (REpresentational State Transfer)是指全球資訊網所依據的軟體架構樣式。 它描述了讓Web運作的關鍵元素，因此提供了一組設計網頁型軟體的原則。 因此，在設計要透過網路使用的API時，遵循這些「最佳實務」是明智的。

由於REST提供了我們許多工作的指導理念，您應該認為精通RESTful設計原則至關重要。 開始的好地方 [羅伊·菲爾丁的論文](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Sling請求解析 {#sling-request-resolution}

瞭解AEM的一個重要面向是傳入要求如何與內容和應用程式行為相關、內容在內容存放庫中的結構方式，以及AEM尋找處理要求的應用程式邏輯的位置。 瞭解Apache [Sling URL分解](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html) 以及強制執行REST架構樣式及其無狀態、可快取及階層式系統限制的方式。

要瞭解Apache Sling請求解析度的關鍵方面是，請求如何主要對應到內容存放庫中的特定資源、請求的其他屬性以及這些內容物件的屬性如何決定叫用哪個應用程式程式碼來呈現內容，以及/apps中的程式碼如何覆寫/libs中的程式碼。

### 快速入門 {#quickstart}

沒有第三步：若要安裝並執行，只要下載並連按兩下Quickstart JAR檔案即可。 沒有步驟三。 任何其他選用功能只需要從Package Share安裝適當的套件。

小型快速入門：將快速入門JAR檔案的大小維持在最小。 使用程式庫時採取明智且最佳化的方式，將選用功能移至「封裝共用」。

更短的啟動時間：進行可能影響啟動時間的變更時，請確定這會縮短啟動時間，而非更長。

### 精簡與平均 {#lean-and-mean}

我們偏好輕巧、小巧、快速又優雅的程式碼和專案。 「夠好」還不夠好。

程式碼重複使用：我們以OSGi為基礎的產品架構和「一切都是內容」的理念意味著，我們擁有重複使用程式碼和成品的絕佳機會。 我們儘可能利用這一事實，讓功能簡單明瞭。

鬆散耦合：我們偏好鬆散耦合的互動，而非緊密相依性和「不想要的親密關係」。 鬆散的耦合也允許更多的程式碼重複使用。

### 不要破壞示範 {#don-t-break-the-demo}

熟悉示範指令碼和示範中最常顯示的產品功能。 瞭解您所做的任何操作都不會中斷「示範指令碼」功能。 核心產品應一律可供展示使用，即使在開發期間亦然。

### 可靠性設計 {#design-for-reliability}

我們致力於以失效軟方式設計和程式碼功能，讓（例如）單一DOM元素的問題不會導致整個頁面無法呈現。 換言之，就是製造出致命的東西。 讓其他一切都能倖存。 讓產品「原諒」。

### 異常是新常態 {#abnormal-is-the-new-normal}

不要依賴關機掛接，確保在啟動時進行清理。 異常終止是正常終止。

`shutdown == kill -9 == power outage`

### 準備彈性叢集 {#be-ready-for-elastic-clustering}

隨時準備進行彈性叢集；隨時假設有叢集。 一般來說，遵守內容存放庫中的所有內容表示內建叢集支援。

### 向下相容性設計 {#design-for-backward-compatibility}

您所做的任何操作都不應破壞客戶的舊程式碼。 僅考慮 `/libs` 以包含在升級期間可更新的產品代碼。 此 `/apps` 存放庫的區段是專案程式碼，而 `/etc` 區段包含必須保留的自訂設定。 一般而言，請勿覆寫中的任何專案 `/apps`， `/content`、和 `/home`. 升級後，舊的專案程式碼、設定和內容應會如升級前般繼續運作。

針對回溯相容性進行設計也可確保升級體驗與初始安裝的簡單性相符。 只需停止AEM、取代Quickstart JAR檔案並再次啟動AEM就足夠了。 隨著安裝基礎的急速成長，升級效率成為日益顯著的優勢。

雖然現有的API在更新且更完善的功能時會標示為已過時，但之前5.x版中公開的所有API都需要保持功能，因為它們可能會在自訂應用程式程式碼中使用。 不應移除此類API。

關於內容結構和使用者體驗的一般一致性，也應該記得回溯相容性。

## 核心概念 {#core-concepts}

**作者執行個體**  — 一般而言，基於安全、控管和其他原因，生產網站會將AEM例項劃分為製作例項和發佈例項。 如需部署架構（包括作者/發佈執行個體）的詳細資訊，請參閱AEM執行個體相關檔案。

**快取、炒制和烘烤**  — 傳統上，烘焙和油炸的概念是不同網頁內容管理系統之間的重要區別。 在CMS行話中，「烘烤」是指在發佈時間將資料提交到靜態檔案的概念，而「油炸」是指在請求時間處理資料以供最終簡報（即及時）的概念。

**群集和負載平衡**  — 為了提高可用性並改善生產環境的效能，通常會合併多個製作和/或發佈執行個體（至叢集中），方法是讓不同的使用者群組可以使用它們，或在Dispatcher設定之後平衡其負載。

您也可以合併內容存放庫的多個例項，以建立 *高可用性* JCR解決方案，然後可與AEM解決方案整合，以針對硬體與軟體故障提供最大保護。 另請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) 以取得進一步資訊。

**元件**  — 在AEM中，元件是一種物件型別，通常可以從Sidekick拖放來建立例項。 舉例來說，AEM隨附的現成可用元件包括文字、標題、Tag Cloud、轉盤、影像和List元件，這些元件都可在執行階段從Sidekick取得。

**內容尋找器**  — 在製作模式中，「內容尋找器」是位於頁面左側的特殊面板（框架），視您在上方選取的標籤而定，會顯示影像、檔案、Flash資產、頁面、段落或存放庫資源清單，您可將其從「內容尋找器」拖放至您正在處理的頁面（在右方）。

**數位資產**  — 在AEM中，數位資產通常（是）影像和多媒體檔案。 如需詳細資訊，請參閱在DAM中使用數位資產。

**Dispatcher** - Dispatcher既是快取又是負載平衡工具，並提供特定的安全性防護措施。

**ExtJS Widget** - AEM中大部分的使用者介面元素都使用ExtJS，這是使用JavaScript撰寫的協力廠商Widget程式庫。 ExtJS提供高效能、可自訂的UI Widget，以及設計良好且可擴充的元件模型。

**JCR、Java™內容存放庫** - Java™內容儲存庫規格(JSR-283)提供抽象資料模型和應用程式設計介面，用於實現結合了檔案系統和物件資料庫功能的大規模可擴充NoSQL資料儲存庫。 雖然您不需要詳盡瞭解JSR-283，但應花時間熟悉JCR的基本功能及其背後的資料模型，因為JCR才可能實現AEM的「內容至上」理念。

實質上，JCR是節點和屬性的系統，節點可以繼承自其他節點，所有內容都儲存為屬性 *值*. 請注意，除了一般繼承以外，JCR還允許使用「mixin」節點的概念，這可啟用多重繼承的模型化。

JCR有多種預先定義的節點型別和屬性型別，但一般而言，輸入系統相當靈活，（事實上） JCR的其中一項優勢就是允許以同樣簡便的方式儲存/管理結構化和非結構化內容。 也就是說，JCR可以容納高度結構化的資料，但它也可以容納任意的動態資料結構，而不受結構描述限制。

JCR的Java™ API適用的JavaDoc為 [此處](https://jackrabbit.apache.org/jcr/jcr-api.html).

在嘗試讀取JavaDoc或JCR規格本身之前，您可能需要先檢視 [此高階說明](/help/sites-developing/the-basics.md#java-content-repository) Adobe Experience Services實作的JCR數量。

**多站點管理員(MSM)** - AEM的MSM功能可協助客戶處理多語言和跨國內容，讓客戶在集中品牌推廣與本地化內容之間取得平衡。

**osgi** - OSGi是一種以服務為基礎的執行階段技術，可為AEM中的模組化Java™開發提供基礎。 此架構不僅為程式碼資源（稱為套裝）提供高度動態（且安全）的類別載入和執行環境，而且可完全控制套裝所公開的各種服務的可見度和生命週期。 服務登入提供結合生命週期動態（和版本需求）的組合合作模型。 OSGi解決了許多應用程式伺服器原本要解決的問題，但以輕量、高度動態的方式解決，例如可讓熱部署服務（無需重新啟動伺服器即可立即使用新程式碼）。

**Parsys，段落系統**  — 段落系統(parsys)是複合元件，可讓作者將不同型別的元件新增至頁面，並包含其他段落元件。 每個段落型別都會表示為元件。 段落系統本身也是元件，包含其他段落元件。

**微核心**  — 存放庫中的每個工作區都可以個別設定，以透過特定微核心（管理資料讀取和寫入的類別）儲存其資料。 同樣地，也可以獨立設定儲存庫範圍的版本存放區，以使用特定微核心。 有數種不同的微核心可供使用，能夠以各種檔案格式或關聯式資料庫儲存資料。 (例如，有MongoDB、DB2®或Oracle的持續性管理員) AEM的預設微核心為TarMK （請參閱下面的進一步說明）。

**發佈執行個體**  — 基於安全性、治理和其他原因，生產網站通常會將AEM執行個體劃分為作者和發佈執行個體。 如需部署架構（包括作者/發佈執行個體）的詳細資訊，請參閱AEM執行個體相關檔案。

**快速入門**  — 與許多其他程式不同，您是使用單一「快速入門」自動解壓縮JAR檔案來安裝AEM。 第一次連按兩下JAR檔案時，就會自動安裝所需的一切。 快速入門JAR包含CRX存放庫（包括管理設施）、虛擬存放庫服務、索引和搜尋服務、工作流程服務、安全性和網頁伺服器所需的所有檔案，以及CQ Servlet Engine (CQSE)和所有AEM服務。 沒有其他檔案可安裝：快速入門是獨立的。

第一次啟動Quickstart時，會在背景建立整個JCR相容存放庫，這可能需要幾分鐘的時間。 初次啟動後，後續啟動的速度會快很多，因為存放庫基礎架構已經奠定。

您可以適當地重新命名Quickstart檔案，以控制許多啟動選項(例如作用中連線埠號碼以及相關AEM執行個體是否應為Publish執行個體或Author執行個體等等)。 若要檢視這方面的選項清單，請在命令列上使用「 — help」執行JAR：

```shell
java -jar <quickstartfilename>.jar -help
```

**復寫代理**  — 復寫代理程式是AEM的核心，其機制用於從製作環境發佈（啟用）內容至發佈環境；從Dispatcher快取排清內容；將使用者產生的內容（例如表單輸入）從發佈環境傳回至製作環境。

**支架**  — 使用支架，您可以建立包含欄位的表單（支架），這些欄位會反映您想要用於頁面的結構，然後使用此表單以根據此結構輕鬆建立頁面。

**細分**  — 網站訪客造訪網站時，有不同的興趣和目標。 瞭解訪客的目標並達到他們的期望，是線上行銷的重要成功先決條件。 分段可透過分析和描述訪客的詳細資料來協助實現此目標。

**Sidekick**  — 此Sidekick是類似浮動視窗的浮動視窗，會顯示在可編輯的頁面上，您可從其中拖曳新元件，以及執行套用至頁面的動作。

**Site Catalyst** -SiteCatalyst為行銷人員提供一個可以測量、分析和最佳化多個行銷管道中所有線上方案的整合資料的位置。 您可以使用Adobe SiteCatalyst來分析來自AEM網站的資料。

**Tar儲存(TarMK)** - TarMK是AEM中的預設持續性系統。 雖然AEM可設定為使用不同的持續性系統（例如MongoDB），但TarMK具有某些優勢，因為它是針對典型JCR使用案例進行效能最佳化（因此速度很快）、使用業界標準的資料格式，而且可以快速輕鬆地備份。

**範本**  — 在AEM中，範本會指定特定型別的頁面。 它定義頁面的結構（同時通常會指定縮圖影像和各種屬性）。 例如，您可以為產品頁面、Sitemap和聯絡資訊使用不同的範本。

**工作流程** - AEM Workflow系統可讓您建立涉及頁面或資產的自動化程式。
