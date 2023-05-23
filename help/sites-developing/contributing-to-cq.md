---
title: 貢獻AEM
seo-title: Contributing to AEM
description: 按大AEM型開源項目中通常採用的行之有效的方法開發
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 0%

---

# 貢獻AEM{#contributing-to-aem}

## 開發方法 {#development-methodology}

是按照大AEM型開源項目中通常採用的行之有效的方法開發的。 事實上，技術AEM堆棧中的許多核心元素都作為活動的開源項目進行維護，如Sling和Jackrabbit，這些項目是為Apache Software Foundation提供的。 本精神的一個主要方面是AEM鼓勵您利用可用的郵件清單和線上論壇與開發團隊直接互動。

如果您要提供AEM到的元件，則應像您在提供開源項目時AEM那樣熟悉，並像您打算為此類項目提供幫助時那樣與現有核心團隊進行溝通。

## 所需體驗 {#required-experience}

超文本傳輸協定(HTTP)是我們所做一切的中心。 因此，在做AEM出貢獻之前，您應深入瞭解HTTP，最好是能夠編寫具有線程池的多線程HTTP伺服器的Java實現。 您還應瞭解HTTP/1.1 keep-alive行為，並應深入瞭解與JavaScript的伺服器/客戶端交互，特別是由表示的非同步交互樣式AJAX。

因為頁面動態性和交互內容是WM體驗的關鍵，所以您必須對文檔對象模型及其在響應事件時進行寫程式操作的可能性有相當深入的瞭解。 您應該瞭解一些知識，例如，對多個瀏覽器文檔（例如，使用iframe）進行即時DOM操作和拖放行為。

那麼，在最高層，您應該對以下方面有深入的瞭解：

* 這樣 [HTTP/1.1協定](https://www.ietf.org/rfc/rfc2616.txt)
* HTML [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* 級聯樣式表
* 可擴展標籤語言(XML)
* 非同步JavaScript和XML(AJAX)設計模式
* JavaScript對象符號(JSON)
* 文檔對象模型
* 有狀態與無狀態交互
* [統一資源標識符](https://www.ietf.org/rfc/rfc2396.txt)
* 瀏覽器Cookie
* 和其他現代網路開發概念

Adobe Experience Manager的技術堆棧基於 [阿帕奇費利克斯](https://felix.apache.org/) 具有OSGI容器 [阿帕奇斯林](https://sling.apache.org/site/index.html) Web框架並嵌入Java內容儲存庫([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html))基於 [阿帕奇·傑克拉比特](https://jackrabbit.apache.org/jcr-api.html)。 您應熟悉這些單獨的項目以及您要貢獻的區域中使用的任何其他開源元件（如Apache Lucene）。

## 部落知識 {#tribal-knowledge}

某些概念和指導原則在前日文化中根深蒂固。 本節列出了您應注意的「深入DNA」問題。

### 一切都是內容 {#everything-is-content}

內容不僅包括Web應用程式持續存在的所有資料。 程式碼、庫、指令碼、模板、HTML、CSS、影像和各種、任何東西的對象都保留在內容儲存庫中，並通過包管理器和包共用以包的形式導入/導出。

### 大衛模型 {#david-s-model}

在Java內容儲存庫中建模內容的方式需要一種完全不同於在關係世界中建立資料建模的軟體行業中常見做法的思維方式。 JCR方式對任何新內容管理人員而言都是必不可少的 [戴維模型：內容建模指南](https://wiki.apache.org/jackrabbit/DavidsModel)。

### 休息 {#restfulness}

REST方法深深地植根於我們的工作。 這意味著，除其他外，避免有狀態的交互，並牢記URI是內容和服務的確定地址。

REST(REpresentational State Transfer)是指萬維網所基於的軟體體系結構樣式。 闡述了使Web工作的關鍵要素，為如何設計基於Web的軟體提供了一套原則。 當設計要在Web上使用的API時，遵守這些「最佳實踐」是明智的。

因為REST提供了我們做的許多事情背後的指導理念，所以您應該認為，熟悉REST風格設計的原理是必不可少的。 一個好的起點是 [羅伊·菲爾丁的論文](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)。

### Sling請求解決方案 {#sling-request-resolution}

要瞭解的一個關鍵方面AEM是，傳入請求如何與內容和應用程式行為相關，內容如何在內容儲存庫中構造，以及在何處查找應用程式邏輯以處理AEM請求。 瞭解Apache [Sling URL分解](https://sling.apache.org/site/url-decomposition.html) 以及它實施REST體系結構樣式及其無狀態、可快取和分層系統約束的方式。

要瞭解Apache Sling請求解析的關鍵方面是：請求如何主要映射到內容儲存庫中的特定資源，請求的附加屬性以及這些內容對象的屬性如何確定將調用哪些應用程式碼來呈現內容，以及/apps中的代碼如何覆蓋/libs中的代碼。

### 快速入門 {#quickstart}

沒有第三步：要安裝和運行，只需下載並按兩下Quickstart JAR檔案即可。 沒有第三步。 任何其他可選功能只需從包共用中安裝相應的包即可。

小Quickstart大小：將Quickstart JAR檔案的大小保持在最小。 智慧、優化地使用庫，將可選功能移到包共用。

更快的啟動時間：當您做出可能影響啟動時間的更改時，請確保它會縮短，而不是延長。

### 瘦和平 {#lean-and-mean}

我們喜歡輕巧、小巧、快速、優雅的代碼和項目。 &quot;夠好&quot;還不夠好。

代碼重用：我們基於OSGi的產品體系結構和「一切都是內容」的理念意味著我們擁有異常好的機會來重新使用代碼和產品。 我們盡量利用這個事實來保持特徵簡潔和平均。

松耦合：我們更喜歡鬆散耦合的互動，而不是緊密依賴和「不需要的親密」。 松耦合還使代碼重用更多。

### 不要中斷演示 {#don-t-break-the-demo}

熟悉演示中最常見的演示指令碼和產品功能。 至少要瞭解，您不應該破壞「演示指令碼」功能。 核心產品應始終準備好演示，即使在開發期間也是如此。

### 可靠性設計 {#design-for-reliability}

我們努力設計並編碼失效軟體功能，以便（例如）單個DOM元素的問題不會導致整個頁面不呈現。 換句話說：製造致命的東西。 讓其他一切都活下去。 讓產品&quot;原諒&quot;

### 異常是新常態 {#abnormal-is-the-new-normal}

不要依賴關閉掛接，確保啟動時進行清理。 異常終止是正常終止。

`shutdown == kill -9 == power outage`

### 準備好進行彈性聚類 {#be-ready-for-elastic-clustering}

始終準備進行彈性聚類，始終假設存在聚類。 通常，遵守內容儲存庫中的所有內容意味著內置群集支援。

### 向後相容設計 {#design-for-backward-compatibility}

您所做的任何操作都不應破壞客戶的舊代碼。 僅考慮 `/libs` 包含可在升級過程中更新的產品代碼。 的 `/apps` 儲存庫的部分是項目代碼， `/etc` 節包含需要保留的自定義配置。 通常，不要覆蓋 `/apps`。 `/content` 和 `/home`。 升級後，舊項目代碼、配置和內容應繼續像升級前一樣運行。

設計向後相容性還可確保升級體驗與初始安裝的簡單性相匹配。 只需停AEM止、替換Quickstart JAR檔案並重新啟動AEM，就足夠了。 隨著安裝基礎的快速增長，升級效率將成為一項日益顯著的優勢。

雖然現有API在較新時可以且應被標籤為不建議使用，但更好的功能會替換它們，但在以前的5.x版本中公開的所有API都需要保持功能，因為它們可能正在自定義應用程式碼中使用。 不應刪除此類API。

在內容結構和用戶體驗的總體一致性方面，還應考慮向後相容性。

## 核心概念 {#core-concepts}

**作者實例**  — 通常，出於安全、治理和其他原因，生產站點會將實例分AEM為「作者」和「發佈」實例。 有關部署體系結構（包括「作者/發佈」實例）的詳細資訊，請參閱有關「實例」AEM的文檔。

**快取、煎炸和烘烤**  — 傳統上，烘焙和煎炸的概念是不同Web內容管理系統之間的重要區別。 在CMS術語中，「烘烤」是指在發佈時將資料提交到靜態檔案的概念，而「煎熬」是指在請求時（即在適當時間）處理資料以進行最終演示的概念。

**群集和負載平衡**  — 為了提高生產環境的可用性和提高效能，通常將多個作者和/或發佈實例（發佈到群集中）組合起來，方法是將它們提供給不同的用戶組，或在Dispatcher配置後對它們進行負載平衡。

還可以將內容儲存庫的多個實例組合起來，以建立 *高可用性* JCR解決方案，然後可與您的解決方案集AEM成，以最大程度地防止硬體和軟體故障。 請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) 的上界。

**元件**  — 在AEM中，「元件」是一種對象類型，通常可以通過從Sidekick中拖放它們來建立其實例。 例如，隨附的現成元件包括文AEM本、標題、標籤雲、旋轉軸、影像和清單元件，這些元件在運行時都可從Sidekick獲得。

**內容查找器**  — 在創作模式中， Content Finder是頁面左側的一個特殊面板（框架），根據您在頂部選擇的頁籤，它顯示影像、文檔、Flash資產、頁面、段落或儲存庫資源清單，您可以將這些資源從Content Finder拖放到您正在處理的頁面（右側）中。

**數字資產**  — 在中AEM，數字資產是（通常）影像和富媒體檔案。 有關詳細資訊，請參閱在DAM中使用數字資產。

**調度程式** - Dispatcher既是快取工具，又是負載平衡工具，也提供了某些安全保護。

**ExtJS小部件**  — 大多數用戶介面元AEM素都使用ExtJS,ExtJS是以JavaScript編寫的第三方小部件庫。 ExtJS具有高效能、可定製的UI小部件和設計良好且可擴展的元件模型。

**JCR,Java內容儲存庫** - Java內容儲存庫規範(JSR-283)提供了抽象資料模型和應用程式寫程式介面，用於實現將檔案系統和對象資料庫的功能結合在一起的大規模可擴展的NoSQL資料儲存庫。 雖然您不需要詳盡地瞭解JSR-283，但您應該花些時間熟悉JCR的基本功能以及其基礎資料模型，因為JCR是使「一切都是內容」的哲學成為可能的AEM。

JCR本質上是一個節點和屬性的系統，節點可以從其他節點繼承，所有內容都作為屬性儲存 *值*。 請注意，除了普通繼承外，JCR還允許使用「mixin」節點的概念，這允許對多個繼承進行建模。

JCR具有許多預定義的節點類型和屬性類型，但通常打字系統相當靈活，而且（實際上）JCR的一個優勢是它允許以同樣輕鬆的方式儲存/管理結構化和非結構化內容。 即JCR可以容納高度結構化的資料，但也可以容納沒有模式約束的任意動態資料結構。

用於JCR的Java API的JavaDoc為 [這裡](https://jackrabbit.apache.org/jcr/jcr-api.html)。

在嘗試讀取JavaDoc或JCR規範本身之前，您可能需要查看 [這個高層解釋](/help/sites-developing/the-basics.md#java-content-repository) 由Adobe Experience Services實施的JCR。

**多站點管理器(MSM)** - MSM功能可幫助客AEM戶處理多語言和跨國內容，使他們能夠平衡集中品牌與本地化內容。

**OSGi** - OSGi是基於服務的運行時技術，為中的模組化Java開發提供AEM基礎。 它是一個框架，它不僅為代碼資源（稱為捆綁包）提供了高度動態（安全）的分類載入和執行環境，而且對捆綁包所暴露的各種服務的可見性和生命週期提供了完全控制。 服務註冊表為捆綁包提供了合作模型，該模型考慮了生命週期動態（和版本要求）。 OSGi解決了應用程式伺服器本想解決的許多問題，但是以輕量、高度動態的方式解決了這些問題，使熱部署服務（使新代碼立即可用而不重新啟動伺服器）成為可能。

**Parsys，段落系統**  — 段落系統(parsys)是一個複合元件，它允許作者將不同類型的元件添加到頁面中，並包含其他段落元件。 每個段落類型都表示為元件。 該段系統本身也是一個組成部分，其中包含其他段落組成部分。

**微核**  — 儲存庫中的每個工作區都可以單獨配置，以通過特定的微內核（管理資料讀寫的類）儲存其資料。 同樣，儲存庫範圍的版本儲存也可以獨立配置為使用特定的微內核。 有許多不同的微內核可用，能夠以各種檔案格式或關係資料庫儲存資料。 (例如，MongoDB、DB2或Oracle有持久性管理器)的預設微內AEM核為TarMK（請參閱下面的進一步內容）。

**發佈實例**  — 出於安全性、治理和其他原因，生產站點通常會將實例分AEM為「作者」和「發佈」實例。 有關部署體系結構（包括「作者/發佈」實例）的詳細資訊，請參閱有關「實例」AEM的文檔。

**快速啟動**  — 與許多其他程式不同，AEM您使用單個「快速啟動」自解壓JAR檔案進行安裝。 首次按兩下JAR檔案時，您需要的所有內容都將自動安裝。 快速啟動JAR包括CRX儲存庫（包括管理設施）、虛擬儲存庫服務、索引和搜索服務、工作流服務、安全性和Web伺服器以及CQ Servlet引擎(CQSE)和所有服務所需的所AEM有檔案。 沒有其他檔案可安裝：快速啟動是自帶的。

第一次啟動Quickstart時，它會在後台建立一個與JCR相容的整個儲存庫，這可能需要幾分鐘的時間。 在初始啟動後，隨後啟動的速度會快得多，因為儲存庫基礎架構已經佈置完畢。

許多啟動選項(如活動埠號以及所AEM涉實例是發佈實例還是作者實例；)可通過適當更名Quickstart檔案來控制。 要查看這方面的選項清單，請在命令行上使用「 — help」運行JAR:

```shell
java -jar <quickstartfilename>.jar -help
```

**複製代理**  — 複製代理是用於將AEM內容從作者發佈（激活）到發佈環境的機制的核心；刷新Dispatcher快取中的內容；將用戶生成的內容（例如，表單輸入）從「發佈」環境返回到「作者」環境。

**腳手架**  — 使用腳手架，您可以建立一個表單（腳手架），其中的欄位反映您需要的頁面結構，然後使用此表單根據此結構輕鬆建立頁面。

**分段**  — 站點訪問者在訪問站點時有不同的興趣和目標。 瞭解訪問者的目標並滿足他們的期望是線上營銷的重要成功先決條件。 通過分析和表徵訪問者的細節，分割有助於實現這一點。

**側腳** - Sidekick是顯示在可編輯頁面上的類似調色板的浮動窗口，可從該窗口拖動新元件，並執行應用於該頁面的操作。

**站點催化劑** -SiteCatalyst為營銷人員提供了一個測量、分析和優化跨多個營銷渠道的所有線上計畫的整合資料的場所。 你可以用Adobe SiteCatalyst來分析網AEM站的資料。

**Tar儲存(TarMK)** - TarMK是中的預設持久性系AEM統。 儘管AEM可以配置為使用不同的持久性系統（如MongoDB），但TarMK具有某些優勢，即它針對典型JCR使用情形進行效能優化（因此速度非常快），使用行業標準資料格式，並且可以快速、輕鬆地備份。

**模板**  — 在AEM中，模板指定特定類型的頁面。 它定義頁面的結構（同時通常還指定縮略圖和各種屬性）。 例如，您可能有單獨的產品頁面、模板和聯繫資訊模板。

**工作流**  — 工作AEM流系統允許建立涉及頁面或資產的自動化流程。
