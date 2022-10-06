---
title: 檢查清單 — 進一步參考
seo-title: The Checklist - Further Reference
description: 了解詳細資訊，詳細說明和/或增強「管理項目 — 最佳實務檢查清單」涵蓋的檔案和原則。
seo-description: Learn about further details that elaborate on and/or augment the documents and principles covered by the Managing Projects - Best Practices Checklist.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
exl-id: 36620e3e-ecdf-4062-bbef-65513362d691
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '3757'
ht-degree: 1%

---

# 檢查清單 — 進一步參考{#the-checklist-further-reference}

本頁提供進一步詳細資訊，以詳細闡述及/或增強 [管理專案 — 最佳實務檢查清單](/help/managing/best-practices.md).

## AEM — 您將使用什麼？ {#aem-what-will-you-be-using}

>[!CAUTION]
>
>本小節中的清單並非詳盡無遺，而是作為簡介。

### AEM內的功能 {#features-within-aem}

實作AEM時（尤其是首次），您需要檢閱 [AEM的功能與工作流程](https://www.adobe.com/tw/marketing/experience-manager.html) 確定您想要/需要的領域。

請考量您將使用的AEM功能，以及對您設計的影響；例如：

* [商務](/help/commerce/cif-classic/administering/ecommerce.md)
* [畫面](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [Assets](/help/assets/assets.md)
* [標記](/help/sites-administering/tags.md)
* [多網站管理與翻譯](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/home.md)
* [社群](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

此外，請檢查 [發行說明](/help/release-notes/release-notes.md)，以查看何時新增任何新功能。

### Integrations {#integrations}

AEM可與其他Adobe產品及/或協力廠商服務整合。 這些功能可增加您可支配的功能。

請參閱 [解決方案整合](/help/sites-administering/integration.md) 以取得完整資訊。

## 遷移還是升級？ {#migrate-or-upgrade}

主要考量是您是否想：

* 升級現有安裝。
* 將內容從當前系統遷移到全新安裝。

從舊版移至目前版本時，有兩個選項：

* 使用 [封裝管理員](/help/sites-administering/package-manager.md) 將所有內容和應用程式代碼從舊系統導出到新系統。
* [升級](/help/sites-deploying/upgrade.md) 舊系統就位。 在大多數情況下，這是建議的選擇。

## 基本基本准則 {#basic-ground-rules}

與任何項目一樣，盡快建立基本規則至關重要。 這些包括：

>[!NOTE]
>
>這些點是通用的， [最佳實務檢查清單](/help/managing/best-practices.md) 處理AEM的相關細節。

* **角色**

   應明確界定，並向參與項目的所有人公佈。 此外，建議強調：

   * 決策者
   * 接觸點

* **責任**

   * 對於每個角色，請明確定義與專案相關的責任，有助於避免混淆。

* **參與**

   通過盡快讓感興趣的方參與進來，您可以鼓勵他們成為 *利害關係人* 因此，他們對項目成功的承諾越來越大。

   * 在客戶端，這包括作者 — 他們必須每天與系統合作。
   * 在您自己的專案團隊中，這也包括負責品質保證的人員。 他們越了解客戶的要求，就越能規劃測試。

* **溝通途徑**

   * 雖然這些規定不應過分正規化，但具體定義應確保隨時向關鍵人員通報情況，從而保持最新。 應特別注意與外部方的溝通。

* **程序**

   要定義的程式取決於您的個別專案。 再次嘗試保持這些簡單，並考慮：

   * 定義與任何第三方互動的流程（和溝通途徑）;例如設計機構和第三方軟體供應商等。
   * 客戶通常擁有自己的項目管理和報告過程和工具。

* **追蹤工具**

   有許多工具可用來追蹤有關錯誤、任務和專案其他方面的資訊 — 請參閱 [潛在工具概觀](#overview-of-potential-tools) 以取得更多詳細資訊。

   * 此處需要注意的要點是僅保留資訊的一個副本並共用資訊（因此可以訪問所使用的工具）。 這樣就能輕鬆維護，並有助於防止差異。

* **範圍**

   明確各級項目應涵蓋的內容：

   * 個別發行（若使用迭代發行程式，且無論是提供給客戶還是您的內部測試團隊）。
   * AEM專案。
   * 整個項目；包括任何協力廠商軟體、其對測試的影響、組織問題和其他許多問題。
   * 對於某些方面，說明內容也會很有用 *not* 在項目範圍內。 這有助於防止混淆和錯誤的假設，但應限於基本問題。

* **報告**

   明確定義您要報告的資訊、形式、報告頻率和向誰報告。

* **術語**

   * 定義要使用的任何縮寫和/或客戶專屬術語。

* **假設**

   * 定義所做的任何假設。

這些資訊可在《項目手冊》中定義；使用Wiki也有助於確保有效處理持續的更改。 無論這些定義如何，關鍵因素是：

* 資訊已定義並維護
* 向所有有關人員明確傳達資訊。 雖然標準的項目管理實踐，但是不能經常重複，以使清晰的角色定義和良好的溝通能夠建立或破壞一個項目。
* 只保留任何被追蹤資訊的一個版本；例如錯誤追蹤、問題追蹤等。

## 關鍵績效指標和目標量度 {#key-performance-indicators-and-target-metrics}

組織使用關鍵績效指標(KPI)來評估其達到目標時的成功。 這些指標是可衡量的價值，可用來證明如何有效地實現具體目標。

這些指標可以是：

* 商務:

   * 用於測量關鍵業務目標。
   * 請務必以清楚的定義選擇適合您的業務/情境的KPI，以判斷KPI是什麼、如何衡量、如何使用以及由誰使用。

* 效能：

   * 定義如何測量系統的效能。
   * 例如頁面載入時間、伺服器回應時間和資料庫查詢效能。

某些指標（但並非全部）可以根據您所識別和定義的目標量度。

### 目標量度 {#target-metrics}

量度可用來定義網站品質的量化測量 — 基本上，這些量度是您要達成之效能目標的定義，可用來定義您的 [KPI（關鍵績效指標）](#key-performance-indicators-and-target-metrics).

有許多量度可定義，但您定義的量度通常涵蓋效能和並行性目標。 尤其是難以量化，而且往往容易被 *情感* 評估：

* 「我們的網站 *太慢了* 今天，什麼時候 *慢慢* 合格？

* 「一切」 *停了下來* 當我的同事登入時」 — 系統可支援多少同時使用者？
* 「當我搜索時，系統 *停了下來* 「 — 哪種搜索請求正在影響系統？
* 「它需要 *年齡* 要下載檔案，「 — 可接受的下載時間（在正常網路條件下）是多少？

目標量度是在專案開始時定義，以：

* 指出您要提供的網站的預期維度
* 指定要達到的最低質量
* 定義這些因素的實際測量方式
* 作為 [關鍵績效指標](#key-performance-indicators-and-target-metrics)

定義目標量度時，請務必小心：

* 如果太高，可能完全無法實現
* 如果設定為過低波動，則不能突出顯示
* 以確保可重複及一致地測量
* 以平衡所測量的不同因素
* 某些量度會與測試環境相關，但有些量度應反映實際情況，因為它們必須可測量且可重複，在您的生產網站上
* 根據量度對網站的重要性排列量度的優先順序
* 將量度限制為可實際監控的集合

在開發專案期間，可視需要更新及調整。 項目成功實施後，它們可用於幫助您控制安裝，並監視/維護持續操作所需的服務級別。

若正確使用，這些量度可提供實用工具；如果不負責任地使用，它們可能會浪費時間分散注意力。 和往常一樣，你需要了解自己在衡量什麼，如何衡量它，以及為什麼。

>[!NOTE]
>
>本節將討論要審議的基本原則和問題。 每個安裝都不同，因此要測量的實際值會不同。

### 一切取決於您的專案設計 {#everything-rests-on-your-project-design}

所有要測量的量度，在某種程度上會受到專案設計的影響。 反之，許多問題最好通過設計變更來解決。

因此，您應定義目標量度 *befor* 決定你的設計。 這可讓您根據這些因素來最佳化設計。 專案一經開發，就很難對基本設計原則進行任何變更。

建立網站結構時，請遵循AEM網站的建議結構。 請務必了解下列問題和/或原則：

* 如何建構網站內容。
* 範本和元件的運作方式。
* 快取的運作方式。
* 個人化內容的影響。
* 搜尋功能的運作方式。
* 如何使用CSS和相關技術來建立緊湊、非重複的HTML程式碼。

如果您覺得您的設計不符合准則，或如果您不確定其中的某些含意，請在開始程式設計階段或填寫內容之前先釐清這些問題。

### 基礎設施 {#infrastructure}

要定義或評估基礎架構，將有助於定義目標值，例如：

* 訪客/日；平均和峰值
* 點擊/日；平均和峰值
* 可供使用的網頁數
* 網頁內容量

這將幫助您評估和選擇您的基礎架構，具體取決於您的情況和網站的戰略意義：

* 伺服器數
* AEM例項數（製作和發佈）

### 效能 {#performance}

可評估的效能因素有數個：

* 個別頁面的回應時間，已考慮：

   * 製作環境的回應時間
   * 發佈環境的回應時間

* 搜尋請求的回應時間

本節可與 [效能最佳化](/help/sites-deploying/configuring-performance.md) 擴展了實際測量效能的技術細節。

#### 個別頁面的回應時間 {#response-times-for-individual-pages}

一個主要問題是您的網站回應訪客請求所花的時間。

雖然此值會因每個請求而異，但可定義平均目標值。 一旦此值經證實可達且可維護，即可用來監控網站的效能並指出潛在問題的發展

製作和發佈環境上的不同目標

您要針對的回應時間在製作和發佈環境中會有所不同，反映目標對象：

* **製作環境**

   此環境供輸入及更新內容的作者使用，因此必須：

   * 適用於更新內容頁面和這些頁面上的個別元素時，產生大量請求的少數使用者
   * 盡可能快地提高他們將您的內容發佈到您網站的生產力

* **發佈環境**

   此環境包含您可供使用者使用的內容：

   * 速度仍然重要，但通常比製作環境慢
   * 經常採用其他效能增強機制：

      * 快取內容
      * 已應用負載平衡

#### 設定目標回應時間 {#setting-target-response-times}

那麼，如何決定可達（平均）的回應時間？ 這通常是經驗問題：

* 網站的過去體驗
* AEM體驗
* 識別回應時間超過平均的複雜頁面（如有可能，應個別最佳化）

但是，（在受控情況下）可採用以下准則：

* 70%的頁面要求應在100毫秒內回應。
* 25%的頁面要求應在100毫秒至300毫秒內回應。
* 4%的頁面要求應在300毫秒至500毫秒內回應。
* 1%的頁面要求應在500ms-1000ms內回應。
* 任何頁面的回應速度都不應低於1秒。

上述數字假設下列條件：

* 在發佈時測量（無製作環境和/或CFC開銷）
* 在伺服器上測量（無網路開銷）
* 未快取(無AEM輸出快取、無Dispatcher快取)
* 僅適用於具有許多相依性的複雜項目(HTML、JS、PDF、..)
* 系統上沒有其他負載

您可使用數種機制來監控回應時間：

* **使用AEM request.log監控回應時間**

   效能分析的一個好起點是請求記錄。 在其他資訊中，您可以使用此項目來查看個別請求的回應時間。 請參閱 [效能最佳化](/help/sites-deploying/configuring-performance.md) 以取得更多詳細資訊。

* **監控含有HTML備注的回應時間**

   HTML備注可用來在每個頁面的來源中包含回應時間資訊：

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### 搜尋請求 {#search-requests}

搜尋請求對您的網站可能有重大影響，包括：

* 實際搜索的響應時間

   * 快速搜尋功能是您網站的品質目標

* 對一般效能的影響

   * 由於搜索功能必須掃描（可能很大）內容的部分，或是特別提取的索引，因此，如果不優化，這可能會影響整個系統的效能

設定搜尋請求的目標，同樣取決於體驗：

* AEM體驗
* 與其他目標相比，評估搜索的使用頻率
* 您的持續性管理器
* 搜索索引
* 搜索函式的複雜性；僅允許輸入1個搜索詞的基本搜索功能比允許用戶使用AND/OR/NOT建立複雜搜索語句的高級搜索更快。

從您的專案開始，就應規劃並整合這些功能。 可用於監測的機制包括：

* **使用AEM request.log監控搜尋回應時間**

   可再次使用request.log來監控搜尋要求的回應時間；請參閱 [效能最佳化](/help/sites-deploying/configuring-performance.md) 以取得更多詳細資訊。

* **用於測量搜索響應時間的寫程式機制**

   若要自訂您收集的搜尋請求相關資訊及其效能，建議您在專案原始碼中加入資訊收集；請參閱 [效能最佳化](/help/sites-deploying/configuring-performance.md) 以取得更多詳細資訊。

### 並行 {#concurrency}

您的網站將可在製作和發佈環境中供許多使用者/訪客使用。 測試時，數字通常比您所用的要多，但也會波動，難以預測。 您的網站需要針對平均同時使用者/訪客人數而設計，而不需注意到負面效能影響。 再次 `request.log` 可進行併發測試；請參閱 [效能最佳化](/help/sites-deploying/configuring-performance.md) 以取得更多詳細資訊。

同時使用者人數的目標取決於環境類型：

* **製作環境**

   * 通常可準確估計同時使用的使用者人數。 您會知道總共有多少位作者，但（可能）並非所有作者都會同時作用。

* **發佈環境**

   * 這較難預測，因此您必須選取目標值。 這應該以您目前網站的體驗，以及您新網站的實際期望為基礎。
   * 特殊事件（例如，當您發佈新的、非常受歡迎的內容時）可能超出預期，甚至超出功能（如某些事件的票證可供銷售時，媒體有時會報導）。

### 容量和容量 {#capacity-and-volume}

討論相關量度前，請先快速定義下列詞語：

* **卷**

   * 系統處理和傳送的輸出量。

* **容量**

   * 系統傳送卷的能力。
   * 在每個步驟中，容量和容量的測量方式都不同，如下表所示。 為獲得最佳效能，請確保每個步驟的容量與卷匹配，並且所有步驟都共用容量和卷。 例如，您可以在客戶端電腦上計算導航，或將其放入快取中，而不必針對每個請求在伺服器上計算導航。

* **容量和容量**

   | 什麼/位置 | 容量 | 卷 |
   |---|---|---|
   | 用戶端 | 用戶電腦的計算能力。 | 頁面配置的複雜性。 |
   | 網路 | 網路頻寬。 | 頁面大小（程式碼、影像等）。 |
   | Dispatcher快取 | Web伺服器的伺服器記憶體（主記憶體和硬碟）。 | Web伺服器（主記憶體和硬碟）。 快取頁數和大小。 |
   | 輸出快取 | AEM伺服器的伺服器記憶體（主記憶體和硬碟）。 | 輸出快取中的頁數和大小、每頁的相依性數。 Dispatcher快取會降低此卷。 |
   | 網頁伺服器 | Web伺服器的計算能力。 | 請求數量。 快取會降低此卷。 |
   | 範本 | Web伺服器的計算能力。 | 範本的複雜度。 |
   | 存放庫 | 儲存庫的效能。 | 從儲存庫載入的頁數。 |

### 其他量度 {#other-metrics}

前幾節詳細說明要定義的主要量度。

視您的特定需求而定，單獨定義其他量度或將上述分類納入考量，可能會很實用。

不過，建議您提供一組精確且可靠運作的核心量度，而不要嘗試測量和定義網站的每個層面。 您的網站純粹是由於其性質，一旦交給您的使用者，就會開始變更和發展。

## 安全性 {#security}

安全至關重要，而且是一個日益嚴峻的挑戰。 It ***必須*** 從專案的最初階段開始加以考量和規劃。

此 [安全性檢查清單](/help/sites-administering/security-checklist.md) 詳細說明您應採取的步驟，以確保部署時的AEM安裝安全無虞。 其他安全方面在 [安全性（開發時）](/help/sites-developing/security.md) 和 [使用者管理與安全性](/help/sites-administering/security.md).

## 並行和迭代任務 {#parallel-and-iterative-tasks}

>[!NOTE]
>
>以下項目：
>
>* 提供與 *first* 實作AEM專案。
>* 用途為摘要概述；請參閱 [專案檢查清單](/help/managing/best-practices.md) 特定階段/里程碑/任務。
>* 任何時間尺度都是理論上的。
>


對於標準AEM專案的新實作，您需要考慮下列工作：

* 從銷售流程切換。
* 客戶應用程式的實作(**開發**)。
* 在客戶站點(**基礎設施**)。
* 建立（或移轉）內容(**內容**)。
* 切換至操作(**維護/支援**)。
* 後續發行。

![chlimage_1-2](assets/chlimage_1-2.png)

建議在所有方面使用迭代方法：

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>將專案啟動分割為 **軟啟動** (降低可用性、多次迭代和 **硬啟動** （完全可用性 — 正式啟用），允許在生產環境的實際條件下進行調校、優化和用戶培訓。

>[!NOTE]
>
>請參閱 [專案檢查清單](/help/managing/best-practices.md) 以了解在項目的生命週期中應執行（或評估）的任務的示例。

每個類別的注意事項有：

* **開發**

   * 首先定義基礎架構。
   * 使用數個迭代(sprint)進行開發：

      * 首次衝刺相當於第一個完整開發週期。
      * 首次衝刺將生成對測試環境的首次部署。
      * 每次衝刺都有跑步結果。
      * 每次衝刺都會獲得客戶簽核（具有反饋的結構化測試的最小值）。
   * 針對專案期間可用AEM版本的最終更新進行規劃。
   * 在短跑期間規劃測試和最佳化。
   * 穩定化和最佳化階段計畫。
   * 建立要計畫供進一步發行的項目記錄。
   * 合作夥伴參與和移交計畫。


* **基礎設施**

   * 首先定義基本架構：

      * 定義效能需求。
      * 定義績效目標（即明確定義期望）。
      * 定義硬體和基礎架構體系結構；包括大小調整。
      * 定義部署。
   * 使用數個迭代；對於第一個sprint和初始配置準備：

      * 開發環境。
      * 開發程式。
      * 測試環境。
      * 部署過程（包括配置管理）。
   * 計畫多個負載測試。
   * 在短跑期間規劃測試和最佳化。
   * 穩定化和最佳化階段的計畫。
   * 盡早部署至生產環境（讓營運團隊設定系統以獲得經驗）。
   * 盡早使用指名的使用者和定義的角色。
   * 計畫培訓（例如，管理員培訓）。
   * 計畫移交給行動。



* **內容**

   * 基本架構：
      * 推動內容階層。
      * 有助於定義內容概念。
      * 定義MSM使用和配置。
      * 定義角色、群組、工作流程和權限。
   * 請考慮離線頁面建立是否有用。
   * 規劃搶先建立第一個頁面和內容（以用於測試和意見回饋）。
   * 規劃現有內容的移轉。
   * 重構後規劃「in-sprint-migration」。
   * 計畫「內容燃起」（上線內容的Sitemap）。

## 預估時間和工作量 {#estimating-time-and-effort}

然後，您可以根據生成的任務清單對（高級）任務定義的時間和工作量進行初始估計。 這些應包括指出將由誰（客戶或合作夥伴）做什麼以及何時做什麼。

下清單顯示了標準近似值和所涉工作的相互關係，因此也包括成本：

>[!CAUTION]
>
>這些數字只能用於初步估計。 經驗豐富的AEM開發人員必須進行詳細分析。

| 階段 | 工作 |
|---|---|
| 開發 | 每個元件節點粗估2至4小時，可涵蓋所有開發需求。 |
| 開發人員測試 | 15%的發展 |
| 後續 | 10%的發展 |
| 文件 | 15%的發展 |
| JavaDoc檔案 | 10%的發展 |
| 錯誤修正 | 15%的發展 |
| 專案管理 | 20%的項目成本用於進行中的項目管理和治理 |

然後，詳細規劃可將可用或所需資源與截止日期和成本相關。

## 參考架構 {#reference-architecture}

參考架構旨在為AEM架構提供範本解決方案。 該參考體系結構解決了企業系統經常遇到的問題，包括擴展、可靠性和安全性。

應定義下列網站量度：

| 分類 | 定義 |
|---|---|
| 網際網路站點數 |  |
| 內聯網站點數 |  |
| 代碼基數（例如，如果Internet和Intranet不同） |  |
| 個別頁面數 |  |
| 網站造訪次數/日 |  |
| 頁面檢視次數/日 |  |
| 資料傳輸的卷（以GB為單位）/天 |  |
| 同時使用者人數（封閉使用者群組） |  |
| 同時訪客數（發佈） |  |
| 同時作者人數 |  |
| 註冊作者人數 |  |
| 頁面激活次數/工作日 |  |
| 部署期間的頁面啟動數 |  |

## 潛在工具概觀 {#overview-of-potential-tools}

提供下列清單，通知您可使用的工具。 這是作為簡介，而非廣泛的建議清單，當然不應阻礙您使用您偏好的任何其他工具。

<table>
 <tbody>
  <tr>
   <td><strong>產品</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>AEM本身提供多種機制，可協助您監控、測試、調查及除錯應用程式；包括：</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">開發人員模式</a></li>
     <li>此 <a href="/help/sites-developing/hobbes.md">測試主控台</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">操作儀表板</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">內容分析</a></li>
     <li>此 <a href="/help/sites-authoring/author-environment-tools.md#content-tree">內容樹</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>硒</td>
   <td><a href="https://docs.seleniumhq.org/">硒</a> 是開放原始碼測試工具。 測試會直接在瀏覽器中執行，以模擬使用者的運作方式。</td>
  </tr>
  <tr>
   <td>Microsoft專案</td>
   <td>常用的專案管理工具。</td>
  </tr>
  <tr>
   <td>吉拉</td>
   <td><a href="https://www.atlassian.com/software/jira">吉拉</a> 是開放原始碼工具，用於追蹤及管理軟體錯誤的詳細資訊。 工作流程可視需要強加至錯誤詳細資訊。</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> 是修訂控制軟體。</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse是開放原始碼IDE，由各種項目組成。 這些重點是構建一個由可擴展的框架、工具和運行時組成的開放式開發平台，以便在整個生命週期中構建、部署和管理軟體。</p> <p>請參閱 <a href="/help/sites-developing/howto-projects-eclipse.md">如何使用Eclipse開發AEM專案</a> 以取得更多資訊。</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>專業（因此可能需要支付許可費）IDE提供一系列全面的功能。 </p> <p>請參閱 <a href="/help/sites-developing/ht-intellij.md">如何使用IntelliJ IDEA開發AEM專案</a> 以取得更多資訊。</p> </td>
  </tr>
  <tr>
   <td>馬文</td>
   <td><a href="https://maven.apache.org/">馬文</a> 是一種軟體項目管理和理解工具，可管理項目的構建過程（軟體和文檔）。</td>
  </tr>
 </tbody>
</table>

## 進一步閱讀 {#further-reading}

此外，以下幾節特別感興趣：

* [快速入門](/help/sites-deploying/deploy.md#getting-started)
* [技術需求](/help/sites-deploying/technical-requirements.md)
* [監視和維護您的執行個體](/help/sites-deploying/monitoring-and-maintaining.md)

### 最佳作法 {#best-practices}

Adobe針對所有階段和對象提供進一步的最佳實務：

* [部署](/help/sites-deploying/best-practices.md)
* [製作](/help/sites-authoring/best-practices.md)
* [管理](/help/sites-administering/administer-best-practices.md)
* [開發](/help/sites-developing/best-practices.md)
* [專案管理](/help/managing/best-practices.md)
