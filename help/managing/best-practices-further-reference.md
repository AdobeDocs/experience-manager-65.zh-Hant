---
title: 核對表 — 進一步參考
seo-title: The Checklist - Further Reference
description: 瞭解詳細介紹和/或補充管理項目 — 最佳做法核對表所涵蓋的文檔和原則的詳細資訊。
seo-description: Learn about further details that elaborate on and/or augment the documents and principles covered by the Managing Projects - Best Practices Checklist.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
exl-id: 36620e3e-ecdf-4062-bbef-65513362d691
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---

# 核對表 — 進一步參考{#the-checklist-further-reference}

本頁提供了詳細資訊，以詳細闡述和/或補充《公約》所涵蓋的檔案和原則 [管理項目 — 最佳做法核對表](/help/managing/best-practices.md)。

## AEM — 你要用什麼？ {#aem-what-will-you-be-using}

>[!CAUTION]
>
>本分節所列的清單並非詳盡無遺，而是作為介紹。

### 內部功AEM能 {#features-within-aem}

在實施AEM時（尤其是首次）, [功能和工作流AEM](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html) 確定你想要或需要哪些區域。

考慮您所使AEM用的功能以及對設計的影響；例如：

* [商務](/help/commerce/cif-classic/administering/ecommerce.md)
* [Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [Assets](/help/assets/assets.md)
* [標記](/help/sites-administering/tags.md)
* [多站點管理和翻譯](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/home.md)
* [社群](/help/communities/deploy-communities.md)

另外，檢查 [發行說明](/help/release-notes/release-notes.md)中，查看添加AEM任何新功能的時間。

### 整合 {#integrations}

可以AEM與其他Adobe產品或第三方服務整合，或兩者兼備。 這些工作流可增加您所能使用的功能和能力。

請參閱 [解決方案整合](/help/sites-administering/integration.md) 的雙曲餘切值。

## 遷移還是升級？ {#migrate-or-upgrade}

一個主要的考慮是，您是否願意：

* 升級現有安裝。
* 將內容從當前系統遷移到全新安裝。

從以前的版本移到當前版本時，有兩個選項：

* 使用 [包管理器](/help/sites-administering/package-manager.md) 將所有內容和應用程式碼從舊系統導出到新系統。
* [升級](/help/sites-deploying/upgrade.md) 舊系統就位。 此方法通常是推薦的選擇。

## 基本基本規則 {#basic-ground-rules}

與任何項目一樣，必須盡快制定基本規則。 這些規則包括：

>[!NOTE]
>
>這些點是泛型的， [最佳做法核對表](/help/managing/best-practices.md) 具體談AEM論

* **角色**

   應明確定義角色，並向參與項目的所有人公佈角色。 此外，最好強調：

   * 決策者
   * 聯繫點

* **職責**

   * 對於每個角色，明確定義與項目相關的責任有助於防止混淆。

* **參與**

   通過盡快讓感興趣的方參與進來，你可以鼓勵他們 *利益相關者* 的下界。 這樣做會增加他們對成功的承諾。

   * 在客戶方面，此角色包括日常與系統協作的作者
   * 在您自己的項目團隊中，此參與還包括負責質量保證的人員。 他們越瞭解客戶的要求，就越能規劃test。

* **通信路徑**

   * 雖然溝通途徑不應過於正規化，但具體定義應確保關鍵人員始終得到通知，因而保持最新。 應特別注意與外部各方的溝通。

* **程序**

   定義的流程取決於您的單個項目。 同樣，嘗試使這些過程保持簡單，並考慮：

   * 確定與任何第三方互動的流程（和溝通途徑）;例如設計機構和第三方軟體供應商等。
   * 客戶通常擁有自己的項目管理和報告流程和工具。

* **跟蹤工具**

   有許多工具可用於跟蹤有關項目錯誤、任務和其他方面的資訊 — 請參閱 [潛在工具概述](#overview-of-potential-tools) 的子菜單。

   * 此處需要注意的關鍵點是只保留資訊的一個副本，並共用資訊（因此可以訪問所使用的工具）。 此工作流簡化了維護並幫助防止了差異。

* **範圍**

   明確各級項目應涵蓋的內容：

   * 單個版本(如果使用迭代版本流程，且不管這些版本是交付給客戶還是您的內部test團隊)。
   * 項AEM目。
   * 整個項目；包括任何第三方軟體，它們對測試的影響，組織問題等。
   * 對於某些方面，它還可以說明 *不* 在項目範圍內。 這一想法有助於防止混淆和錯誤假設，儘管它應限於基本問題。

* **報告**

   明確定義要報告的資訊、報告形式、報告頻率和報告對象。

* **術語**

   * 定義要使用的任何縮寫和/或客戶特定術語。

* **假設**

   * 定義所做假設。

這些資訊可在項目手冊中定義；使用Wiki還有助於確保有效處理正在進行的更改。 無論這些假設是什麼，關鍵因素是：

* 定義並維護資訊
* 資訊被明確傳達給所有相關人員。 雖然標準的項目管理實踐，但是它的重複頻率不能足夠高，以至於清晰的角色定義和良好的溝通能夠使項目成為或中斷項目。
* 只保留一個版本的任何被跟蹤的資訊；例如，錯誤跟蹤和問題跟蹤。

## 主要績效指標和目標指標 {#key-performance-indicators-and-target-metrics}

組織使用關鍵績效指標(KPI)來評估其在達到目標方面的成功。 這些指標是可衡量的價值，可用來表明具體目標如何得到有效實現。

這些指標可以是：

* 商務:

   * 用於衡量關鍵業務目標。
   * 選擇適合您的業務/方案的KPI非常重要，它們的定義明確，包括它們是什麼、如何衡量、如何使用和由誰使用。

* 效能：

   * 定義如何度量系統的效能。
   * 一些示例包括頁面載入時間、伺服器響應時間和資料庫查詢效能。

某些指標可以基於您識別和定義的目標指標。

### 目標度量 {#target-metrics}

度量用於定義網站質量的量化度量。 它們基本上是您想要實現的效能目標的定義，可用於定義您的 [KPI（主要績效指標）](#key-performance-indicators-and-target-metrics)。

可以定義許多度量，但通常您定義的度量涵蓋效能和併發性目標。 特別是難以量化的因素，往往容易 *情感* 評估：

* 「網站是 *太慢了* 今天&quot; — 何時 *慢慢* 合格？

* 「一切」 *咧著嘴停了下來* 當我的同事登錄時」 — 系統可支援多少並行用戶？
* 「當我搜索時，系統 *咧著嘴停了下來* &quot; — 哪些搜索請求會影響系統？
* &quot; *年齡* 下載檔案」 — 可接受的下載時間（在正常網路條件下）是多少？

目標度量在項目開始時定義為：

* 指明可提供的網站的預期維度
* 指明要達到的最小質量
* 定義衡量這些因素的方式
* 用作 [主要績效指標](#key-performance-indicators-and-target-metrics)

定義目標度量時必須始終注意：

* 如果設定得太高，則可能無法實現
* 如果設定得過低，則不能突出顯示
* 確保他們能夠反複、一致地
* 在所測量的不同因素之間提供平衡
* 某些指標與test環境有關，但有些指標應反映真實情況，因為它們必須可以在製作網站上測量和重現
* 根據指標對網站的重要性排定其優先順序
* 將度量限制為可監視的集

在項目開發過程中，可酌情更新和調整。 在項目成功實施後，它們可用於幫助您控制安裝並監控/維護持續操作所需的服務級別。

如果使用得當，這些指標可提供有用的工具；如果不負責任地使用，可能會浪費時間分散注意力。 一如既往，瞭解你在衡量什麼，你如何衡量它，以及為什麼。

>[!NOTE]
>
>本節討論供審議的基本原則和問題。 每個安裝都不同，因此要測量的實際值往往不同。

### 一切都取決於您的項目設計 {#everything-rests-on-your-project-design}

所有測量的指標都受項目設計的影響。 相反，許多問題最好通過設計更改來解決。

因此，定義目標度量 *先* 決定你的設計。 這樣，您就可以根據這些因素優化設計。 在您的項目開發完成後，對基本設計原則的挑戰性就來了。

建立網站結構時，請遵循建議的網站結AEM構。 確保您瞭解以下問題和/或原則：

* 如何構建網站內容。
* 模板和元件的工作方式。
* 快取如何工作？
* 個性化內容的影響。
* 搜索功能的工作原理。
* 如何使用CSS和相關技術建立緊湊、非冗餘的HTML代碼。

如果您認為您的設計不遵循指導原則，或者您不確定其中的某些含義，請澄清這些問題。 在開始寫程式階段或填寫內容之前，請執行此操作。

### 基礎設施 {#infrastructure}

要定義或評估基礎架構，定義目標值會有所幫助，例如：

* 訪客/日；均值和峰值
* 點擊/天；均值和峰值
* 可用的網頁數
* Web內容量

根據您的情況和網站的戰略意義，定義基礎架構可以幫助您評估和選擇您的基礎架構：

* 伺服器數
* 實例數(AEM作者和發佈)

### 效能 {#performance}

可以評估以下幾個效能因素：

* 單個頁面的響應時間，計算：

   * 對作者環境的響應時間
   * 發佈環境上的響應時間

* 搜索請求的響應時間

可以使用 [效能優化](/help/sites-deploying/configuring-performance.md) 擴展了實際測量效能的技術細節。

#### 單個頁面的響應時間 {#response-times-for-individual-pages}

一個關鍵問題是您的網站響應訪問者請求所花費的時間。

儘管此值因每個請求而異，但可以定義平均目標值。 一旦這一價值被證明是可實現和可維護的，就可以用來監控網站的效能並指出潛在問題的發展

作者和發佈環境的不同目標

您所希望的響應時間在作者和發佈環境上不同，反映了目標受眾：

* **作者環境**

   此環境由作者輸入和更新內容使用，因此它必須：

   * 滿足在更新內容頁面和這些頁面上的單個元素時生成大量請求的少數用戶
   * 盡可能快地最大限度地提高他們的工作效率，以便將內容放到您的網站上

* **發佈環境**

   此環境包含您為用戶提供的內容：

   * 速度仍然至關重要，但通常比作者環境慢
   * 通常採用額外的效能增強機制：

      * 內容已快取
      * 應用了負載平衡

#### 設定目標響應時間 {#setting-target-response-times}

您如何確定可實現的（平均）響應時間？ 問題和答案通常是經驗問題：

* 在您的網站上的體驗
* 體驗AEM
* 識別響應時間高於平均值的複雜頁面(這些頁面應單獨優化（如果可能）

但是，在受控情況下，可以採用以下准則：

* 70%的頁面請求應在100毫秒內作出答復。
* 25%的頁面請求應在100毫秒至300毫秒內作出響應。
* 4%的頁面請求應在300ms-500ms內響應。
* 1%的頁面請求應在500ms-1000ms內響應。
* 任何頁面的響應速度都不應低於1秒。

上述數字假設以下條件：

* 在發佈時測量（無創作環境和/或CFC開銷）
* 在伺服器上測量（無網路開銷）
* 未快取(無AEM輸出快取，無Dispatcher快取)
* 僅用於具有多個依賴關係的複雜項目(HTML、JS、PDF、..)
* 系統上沒有其他負載

可以使用多種機制來監視響應時間：

* **使用request.log監AEM視響應時間**

   效能分析的一個好起點是請求日誌。 除其他資訊外，您還可以看到單個請求的響應時間。 請參閱 [效能優化](/help/sites-deploying/configuring-performance.md) 的子菜單。

* **使用HTML注釋監視響應時間**

   HTML注釋可用於在每個頁的源中包括響應時間資訊：

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### 搜索請求 {#search-requests}

搜索請求對您的網站有重大影響，具體包括：

* 實際搜索的響應時間

   * 快速搜索功能是您網站的質量目標

* 對一般效能的影響

   * 由於搜索功能必須掃描（可能較大）內容的部分或特別提取的索引，因此此功能可能會影響整個系統的效能，如果未進行優化

為搜索請求設定目標同樣取決於以下方面：

* 體AEM驗
* 評估與其他目標相比使用搜索的頻率
* 您的持久性管理器
* 搜索索引
* 搜索功能的複雜性；一個允許輸入一個搜索項的基本搜索功能比一個允許用戶使用AND/OR/NOT構建複雜搜索語句的高級搜索要快。

這些搜索請求應從項目開始就開始計畫和整合。 可用於監測的機制包括：

* **使用request.log監視搜索AEM響應時間**

   請求.log再次可用於監視搜索請求的響應時間；見 [效能優化](/help/sites-deploying/configuring-performance.md) 的子菜單。

* **用於測量搜索響應時間的寫程式機構**

   要定制您收集的有關搜索請求及其效能的資訊，建議您在項目原始碼中包含資訊收集；見 [效能優化](/help/sites-deploying/configuring-performance.md) 的子菜單。

### 併發 {#concurrency}

在作者和發佈環境中，讓某些用戶和訪問者都可訪問您的網站。 資料通常比測試時所用的要多，但也會波動，難以預測。 為平均數量的併發用戶和訪問者設計網站，而不會注意到對效能的負面影響。 同樣，使用 `request.log` 進行併發test。 請參閱 [效能優化](/help/sites-deploying/configuring-performance.md) 的子菜單。

併發用戶數的目標取決於環境類型：

* **作者環境**

   * 通常可以準確估計併發用戶數。 你可以知道你總共有多少作者，但（可能）並非所有作者同時都處於活動狀態。

* **發佈環境**

   * 發佈環境更難預測，因此必須選擇目標值。 同樣，它應該基於您當前網站的經驗以及您對新網站的現實期望。
   * 特殊事件（例如，當您發佈新的熱門內容時）可能超出預期，甚至超出能力（如某些事件的門票可供銷售時，媒體有時會報導）。

### 容量和卷 {#capacity-and-volume}

在討論相關指標之前，請快速定義以下術語：

* **卷**

   * 系統處理和傳送的輸出量。

* **容量**

   * 系統交付卷的能力。
   * 在每個步驟中，容量和體積的測量都不同，如下表所示。 為獲得最佳效能，請確保每個步驟的容量與卷相匹配，並確保所有步驟都共用容量和卷。 例如，您可以在客戶端電腦上計算導航，或將其放入快取中，而不是在伺服器上計算每個請求的導航。

* **容量和卷**

   | 何處 | 容量 | 卷 |
   |---|---|---|
   | 用戶端 | 用戶電腦的計算能力。 | 頁面佈局的複雜性。 |
   | 網路 | 網路頻寬。 | 頁面大小（代碼、影像等）。 |
   | 調度程式快取 | Web伺服器的伺服器記憶體（主記憶體和硬碟）。 | Web伺服器（主記憶體和硬碟）。 快取頁的數量和大小。 |
   | 輸出快取 | 伺服器的服AEM務器記憶體（主記憶體和硬碟）。 | 輸出快取中的頁數和大小，每頁的依賴關係數。 Dispatcher快取會降低此卷。 |
   | 網頁伺服器 | Web伺服器的計算能力。 | 請求數。 快取會降低此卷。 |
   | 範本 | Web伺服器的計算能力。 | 模板的複雜性。 |
   | 存放庫 | 儲存庫的效能。 | 從儲存庫載入的頁數。 |

### 其他指標 {#other-metrics}

前面各節詳細介紹了要定義的主要度量。

根據您的特定要求，您可能有必要單獨定義附加度量，或對上述分類進行覈算。

但是，最好有一組簡單可靠的準確核心指標，而不是嘗試測量和定義網站的每個方面。 從本質上講，您的網站在交給您的用戶後開始發生變化和發展。

## 安全性 {#security}

安全至關重要，而且是一個日益嚴峻的挑戰。 它 ***必須*** 從項目的最初階段開始考慮和計畫。

的 [安全核對表](/help/sites-administering/security-checklist.md) 詳細說明您應採取的步驟，以確保在部AEM署時安全安裝。 其他安全方面在下文 [安全性（開發時）](/help/sites-developing/security.md) 和 [用戶管理和安全](/help/sites-administering/security.md)。

## 並行和迭代任務 {#parallel-and-iterative-tasks}

>[!NOTE]
>
>以下內容：
>
>* 提供與 *第一* 項目的AEM執行。
>* 是抽象概述；查看 [項目核對表](/help/managing/best-practices.md) 特定階段/里程碑/任務。
>* 任何時間尺度都是理論上的。
>


對於標準項目的新實AEM施，請考慮以下任務：

* 從銷售流程移交。
* 實施客戶應用程式(**開發**)。
* 在客戶站點(**基礎設施**)。
* 建立（或遷移）內容(**內容**)。
* 切換到操作(**維護/支援**)。
* 後續版本。

![chlimage_1-2](assets/chlimage_1-2.png)

對於所有方面，建議使用迭代方法：

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>要允許在生產環境的實際條件下進行調整、優化和用戶培訓，請將項目啟動分解為 **軟啟動** (減少可用性、多次迭代和 **硬啟動** （完全可用 — 即時）。

>[!NOTE]
>
>查看 [項目核對表](/help/managing/best-practices.md) 例如，在項目的生命週期中應執行（或評估）的任務。

每個類別需要注意的一點是：

* **開發**

   * 首先定義基本體系結構。
   * 使用多個迭代（約束）進行開發：

      * 第一個衝刺相當於第一個完整的開發週期。
      * 第一個sprint將產生第一個部署到您的test環境。
      * 每次衝刺都有可跑的結果。
      * 每個sprint都會獲得客戶簽名(最少有帶反饋的結構化test)。
   * 計畫在項目期間是否會更新AEM可用版本。
   * 在短跑期間計畫test和優化。
   * 計畫穩定和優化階段。
   * 建立要計畫以供進一步發行的物料日誌。
   * 合作夥伴參與和移交計畫。


* **基礎設施**

   * 首先定義基本體系結構：

      * 定義效能要求。
      * 定義績效目標（即明確定義預期）。
      * 定義硬體和基礎架構架構；包括規模。
      * 定義部署。
   * 使用多個迭代；為首次sprint和初始配置準備：

      * 發展環境。
      * 開發過程。
      * Test環境。
      * 部署過程（包括配置管理）。
   * 計畫多個負載test。
   * 在短跑期間計畫test和優化。
   * 計畫穩定和優化階段。
   * 盡早部署到生產環境（讓運營團隊設定系統以獲得經驗）。
   * 盡早使用命名用戶和定義的角色。
   * 計畫培訓（例如，管理員培訓）。
   * 向行動移交計畫。



* **內容**

   * 基本體系結構：
      * 驅動內容層次結構。
      * 幫助定義內容概念。
      * 定義MSM使用和佈局。
      * 定義角色、組、工作流和權限。
   * 請考慮離線頁面建立是否有用。
   * 計畫早期建立首頁和內容(用於test和反饋)。
   * 規劃現有內容的遷移。
   * 重構後的「in-sprint-migration」計畫。
   * 計畫「內容燃盡」（即時內容的站點地圖）。

## 估計時間和工作量 {#estimating-time-and-effort}

根據生成的任務清單，您可以對（高級別）任務定義的時間和工作量進行初步估計。 這些估計應包括指明由誰（客戶或合作夥伴）做什麼和何時做什麼。

以下清單顯示了標準近似值和所涉及工作的相互關係，因此也顯示了成本：

>[!CAUTION]
>
>這些數字只能用於初步估計。 經驗豐AEM富的開發人員必須進行詳細分析。

| 階段 | 努力 |
|---|---|
| 開發 | 大致估計每個元件節點2-4小時，涵蓋所有開發需求。 |
| 開發人員測試 | 15%的發展 |
| 後續行動 | 10%的發展 |
| 文件 | 15%的發展 |
| JavaDoc文檔 | 10%的發展 |
| 修蟲 | 15%的發展 |
| 專案管理 | 20%的項目成本用於持續的項目管理和治理 |

然後，詳細規劃可以將可用或所需資源與截止日期和成本相關聯。

## 參考體系結構 {#reference-architecture}

給出了參考體系結構，為該體系結構提供了模AEM板解決方案。 該參考體系結構解決了企業系統通常遇到的問題，包括擴展性、可靠性和安全性。

應定義以下站點度量：

| 分類 | 定義 |
|---|---|
| 網站數 |  |
| 內聯網站數 |  |
| 代碼庫數（例如，如果Internet和Intranet不同） |  |
| 單頁數 |  |
| 站點訪問數/天 |  |
| 頁面視圖數/天 |  |
| 資料傳輸的卷（以GB為單位）/天 |  |
| 併發用戶數（關閉的用戶組） |  |
| 併發訪問者數（發佈） |  |
| 併發作者數 |  |
| 註冊作者數 |  |
| 頁面激活數/工作日 |  |
| 部署期間的頁激活數 |  |

## 潛在工具概述 {#overview-of-potential-tools}

提供以下清單以通知您可以使用的工具。 它旨在作為介紹，而不是廣泛的建議清單，不應阻止您使用任何其他工具。

<table>
 <tbody>
  <tr>
   <td><strong>產品</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>它AEM本身提供了一系列機制來幫助您監視、test、調查和調試應用程式；包括：</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">開發人員模式</a></li>
     <li>的 <a href="/help/sites-developing/hobbes.md">測試控制台</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">操作儀表板</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">內容分析</a></li>
     <li>的 <a href="/help/sites-authoring/author-environment-tools.md#content-tree">內容樹</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>硒</td>
   <td><a href="https://www.selenium.dev/">硒</a> 是開源test工具。 test直接在瀏覽器中運行，模擬用戶的工作方式。</td>
  </tr>
  <tr>
   <td>Microsoft®項目</td>
   <td>常用的項目管理工具。</td>
  </tr>
  <tr>
   <td>吉拉</td>
   <td><a href="https://www.atlassian.com/software/jira">吉拉</a> 是用於跟蹤和管理軟體錯誤詳細資訊的開源工具。 工作流可以根據需要強加到Bug詳細資訊上。</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">蠢貨</a> 是修訂版控制軟體。</td>
  </tr>
  <tr>
   <td>日蝕</td>
   <td><p>Eclipse是一個開源IDE，由各種項目組成。 它側重於構建一個由可擴展的框架、工具和運行時間組成的開放式開發平台，用於在整個生命週期中構建、部署和管理軟體。</p> <p>請參閱 <a href="/help/sites-developing/howto-projects-eclipse.md">如何利用EclipseAEM開發項目</a> 的子菜單。</p> </td>
  </tr>
  <tr>
   <td>智慧J</td>
   <td><p>專業IDE（因此可能需要許可成本）提供全面的功能。 </p> <p>請參閱 <a href="/help/sites-developing/ht-intellij.md">如何利用IntelliJ IDEAAEM開發項目</a> 的子菜單。</p> </td>
  </tr>
  <tr>
   <td>馬文</td>
   <td><a href="https://maven.apache.org/">馬文</a> 是一種軟體項目管理和理解工具，可以管理項目的生成過程（軟體和文檔）。</td>
  </tr>
 </tbody>
</table>

## 延伸閱讀 {#further-reading}

此外，以下各節特別感興趣：

* [快速入門](/help/sites-deploying/deploy.md#getting-started)
* [技術要求](/help/sites-deploying/technical-requirements.md)
* [監視和維護實例](/help/sites-deploying/monitoring-and-maintaining.md)

### 最佳做法 {#best-practices}

Adobe為所有階段和受眾提供了進一步的最佳做法：

* [部署](/help/sites-deploying/best-practices.md)
* [編寫](/help/sites-authoring/best-practices.md)
* [管理](/help/sites-administering/administer-best-practices.md)
* [開發](/help/sites-developing/best-practices.md)
* [專案管理](/help/managing/best-practices.md)
