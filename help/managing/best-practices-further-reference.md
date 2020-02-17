---
title: 檢查清單——進一步參考
seo-title: 檢查清單——進一步參考
description: 進一步瞭解詳細說明及／或增強管理專案——最佳實務檢查清單所涵蓋的檔案和原則。
seo-description: 進一步瞭解詳細說明及／或增強管理專案——最佳實務檢查清單所涵蓋的檔案和原則。
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
translation-type: tm+mt
source-git-commit: 37ec3d8ce779ba392e6a92c828efb5fad749abec

---


# 檢查清單——進一步參考{#the-checklist-further-reference}

本頁提供了詳細資訊，以詳細說明和／或補充「管理項目——最佳做法核對表」 [所涵蓋的文檔和原則](/help/managing/best-practices.md)。

## AEM —— 您將使用什麼？ {#aem-what-will-you-be-using}

>[!CAUTION]
>
>本小節中的清單並非完整，而是作為介紹。

### AEM中的功能 {#features-within-aem}

實作AEM（尤其是首次）時，您需要檢閱AEM [的功能和工作流程](https://www.adobe.com/marketing/experience-manager.html) ，以確定您需要／需要哪些區域。

考慮您將要使用的AEM功能，以及對您設計的影響；例如：

* [商務](/help/sites-administering/ecommerce.md)
* [畫面](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [資產](/help/assets/assets.md)
* [標記](/help/sites-administering/tags.md)
* [多網站管理與翻譯](/help/sites-administering/msm-and-translation.md)
* [表單](/help/forms/home.md)
* [社群](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

此外，請檢 [查AEM的各種版本的「發行說明」](/help/release-notes/release-notes.md)，以查看新增任何新功能的時間。

### 整合 {#integrations}

AEM可與其他Adobe產品及／或協力廠商服務整合。 這些功能可增加您的可用功能。

如需完 [整資訊](/help/sites-administering/integration.md) ，請參閱解決方案整合。

## 移轉或升級？ {#migrate-or-upgrade}

主要考量是您是否要：

* 升級現有安裝。
* 將內容從目前系統移轉至全新安裝。

從舊版移至目前版本時，有兩個選項：

* 使用 [Package Manager](/help/sites-administering/package-manager.md) ，將所有內容和應用程式碼從舊系統匯出至新系統。
* [就地升級](/help/sites-deploying/upgrade.md) ，讓舊系統升級。 在大多數情況下，這是建議的選擇。

## 基本基本准則 {#basic-ground-rules}

與任何項目一樣，盡快建立基本規則至關重要。 其中包括：

>[!NOTE]
>
>這些點子是一般的，「最 [佳實務檢查清單](/help/managing/best-practices.md) 」會說明與AEM相關的細節。

* **角色**

   這些都應該有明確的界定，並向參與項目的每個人公開。 此外，建議強調：

   * 決策者
   * 聯絡點

* **職責**

   * 針對每個角色，明確定義與專案相關的責任，有助於避免混淆。

* **參與**

   只要盡快讓相關方參與，您就可以鼓勵他們成為專案的 *利害關係人* ，進而增加他們對成功的承諾。

   * 在客戶方面，這包括作者——他們必須每天與系統合作。
   * 在您自己的專案團隊中，這也包括負責品質保證的人員。 他們瞭解客戶的需求越多，就越能規劃測試。

* **溝通途徑**

   * 雖然這些規定不應過於正規化，但具體定義應確保關鍵人員隨時獲得通知，因此保持最新。 應特別注意與外部方的溝通。

* **程序**

   要定義的流程將取決於您的個別項目。 請再次嘗試保持這些簡單，同時考慮：

   * 定義與任何第三方互動的程式（和通訊途徑）;例如設計機構和第三方軟體供應商等。
   * 客戶通常有自己的「項目管理和報告」流程和工具。

* **追蹤工具**

   有許多工具可用來追蹤專案錯誤、工作和其他方面的資訊——如需詳細資訊，請參 [閱潛在工具概觀](#overview-of-potential-tools) 。

   * 這裡要注意的要點是，僅保留一份資訊並分享資訊（因此也可存取使用的工具）。 這樣可簡化維護作業，並有助於防止不一致。

* **範圍**

   明確各級項目應涵蓋的內容：

   * 個別發行（如果使用了反覆發行程式，而且不論是交付給客戶還是內部測試團隊）。
   * AEM專案。
   * 整個項目；包括任何協力廠商軟體、其對測試的影響、組織問題等。
   * 對於某些方面來說，說明項目範圍內 *的內容* ，也很有用。 這有助於避免混淆和錯誤假設，儘管它應限於基本問題。

* **報告**

   明確定義您將以何種形式、多久向誰報告的資訊。

* **術語**

   * 定義要使用的任何縮寫和／或客戶特定術語。

* **假設**

   * 定義所做的任何假設。

這些資訊可在項目手冊中定義；使用Wiki還有助於確保有效地處理正在進行的更改。 無論這些定義如何，關鍵因素是：

* 定義並維護資訊
* 向所有相關人員清楚傳達資訊。 雖然標準的項目管理實踐，但明確的角色定義和良好的溝通是無法讓項目成為或中斷的。
* 所追蹤的任何資訊只保留一個版本；例如，錯誤追蹤、期刊追蹤等。

## 關鍵績效指標和目標量度 {#key-performance-indicators-and-target-metrics}

組織使用關鍵績效指標(KPI)來評估其在達到目標時的成功。 這些指標是可衡量的價值，可用來證明具體目標的實現效率。

這些指標可以是：

* 商務:

   * 用於衡量關鍵業務目標。
   * 請務必選擇適合您業務／藍本的KPI，並清楚定義KPI的內容、如何衡量、如何使用及由誰使用。

* 效能：

   * 定義如何測量系統效能。
   * 例如頁面載入時間、伺服器回應時間和資料庫查詢效能。

有些指標（但並非全部）可以根據您識別和定義的目標量度。

### 目標量度 {#target-metrics}

量度用於定義網站品質的量化度量——基本上是您要達到的效能目標的定義，可用來定義 [KPI（關鍵績效指標）](#key-performance-indicators-and-target-metrics)。

您可定義許多量度，但您定義的量度通常涵蓋效能和並行性目標。 尤其是那些難以量化、往往容易進行情緒評估的 *因素* :

* 「我們的網站 *今天太慢* 」-何時 *太慢* ?

* 「當我 *的同事登入時* ，一切都停了下來」—系統可以支援多少並行用戶？
* &quot;當我搜索時，系 *統停止* &quot; —— 哪種搜索請求正影響系統？
* 「下 *載檔案* 」 —— 可接受的下載時間（在正常網路條件下）為何？

目標量度是在專案開始時定義，以便：

* 指出您將提供之網站的預期維度
* 指出您要達到的最低品質
* 定義這些因素的實際測量方式
* 用作關鍵績效指標 [的基礎](#key-performance-indicators-and-target-metrics)

定義目標量度時，請務必小心：

* 如果設定得太高，可能完全無法實現
* 如果設定為過低波動，則不能突出顯示
* 確保它們能夠反複和一致地衡量
* 以平衡所測量的不同因素
* 某些量度會與測試環境有關，但有些量度應反映實際案例，因為它們必須可測量且可重制於生產網站上
* 根據量度對網站的重要性排定其優先順序
* 將量度限制為可實際監控的量度集

在專案開發期間，可視需要更新和調整這些專案。 在成功實施項目後，這些項目可幫助您控制安裝並監控／維護持續操作所需的服務級別。

當使用正確時，這些量度可提供有用的工具；如果用起來不負責任，那就會浪費時間分散注意力。 和以往一樣，您需要瞭解您所測量的內容、您如何測量它，以及測量原因。

>[!NOTE]
>
>本節將討論將審議的基本原則和問題。 每個安裝都不同，所以要測量的實際值會不同。

### 一切都取決於您的專案設計 {#everything-rests-on-your-project-design}

所有要測量的量度，在某種程度上都會受專案設計的影響。 相反地，許多問題最好由設計變更來解決。

因此，您應先定義目標量度， *再決定* 您的設計。 這可讓您根據這些因素來最佳化您的設計。 一旦您的專案開發完成，就很難對基本設計原則做任何變更。

當您建立網站的結構時，請遵循AEM網站的建議結構。 請確定您瞭解下列問題和／或原則：

* 如何建構網站內容。
* 範本和元件的運作方式。
* 快取的運作方式。
* 個人化內容的影響。
* 搜尋功能的運作方式。
* 如何使用CSS和相關技術來建立精簡、非冗餘的HTML程式碼。

如果您覺得您的設計不符合准則，或者您不確定其中的某些含意，請在開始程式設計階段或填寫內容之前先釐清這些問題。

### 基礎架構 {#infrastructure}

要定義或評估基礎架構，它將幫助定義目標值，例如：

* 訪客／日；均值和峰值
* 點擊／日；均值和峰值
* 提供的網頁數
* 網頁內容量

這將幫助您評估和選擇您的基礎架構，具體取決於您的情況和網站的戰略重要性：

* 伺服器數
* AEM例項數（作者和發佈）

### 效能 {#performance}

可評估的效能因素有：

* 個別頁面的回應時間，已考慮：

   * 作者環境的回應時間
   * 發佈環境上的回應時間

* 搜尋請求的回應時間

本節內容可與「效能最佳化 [」一起閱讀](/help/sites-deploying/configuring-performance.md) ，以擴充實際測量效能的技術細節。

#### 個別頁面的回應時間 {#response-times-for-individual-pages}

關鍵問題是您的網站回應訪客要求所花的時間。

雖然此值會因每個請求而異，但可以定義平均目標值。 一旦這個值被證明是可實現和可維護的，它就可以用來監控網站的效能並指出潛在問題的發展

作者和發佈環境的不同目標

您要針對的回應時間在作者和發佈環境中會有所不同，反映目標讀者：

* **作者環境**

   此環境由作者輸入和更新內容使用，因此它必須：

   * 適合在更新內容頁面和這些頁面上個別元素時產生大量請求的少數使用者
   * 盡可能快地提高生產力，讓您的內容可上網

* **發佈環境**

   此環境包含您提供給使用者的內容：

   * 速度仍然很重要，但通常比作者環境慢
   * 通常採用額外的效能增強機制：

      * 內容會快取
      * 應用負載平衡

#### 設定目標回應時間 {#setting-target-response-times}

那麼，您如何決定可實現的（平均）回應時間？ 這通常是經驗問題：

* 您網站上的過去經驗
* 體驗AEM
* 識別具有高於平均回應時間的複雜頁面（如果可能，應個別最佳化）

但是，（在受控情況下）可適用下列准則：

* 70%的頁面要求應在100毫秒內回覆。
* 25%的頁面要求應在100毫秒至300毫秒內回應。
* 4%的頁面要求應在300毫秒-500毫秒內回應。
* 1%的頁面要求應在500ms-1000ms內回應。
* 任何頁面的回應速度都不應慢於1秒。

上述數字假設下列條件：

* 在發佈時測量（無編寫環境和／或CFC開銷）
* 在伺服器上測量（無網路開銷）
* 未快取（無AEM輸出快取，無Dispatcher快取）
* 僅適用於具有許多相依性的複雜項目(HTML、JS、PDF、...)
* 系統上沒有其他負載

您可使用數種機制來監控回應時間：

* **使用AEM request.log監控回應時間**

   效能分析的好起點是請求記錄。 除了其他資訊外，您還可使用此資訊來查看個別要求的回應時間。 如需詳 [細資訊，請參閱](/help/sites-deploying/configuring-performance.md) 「效能最佳化」。

* **使用HTML注釋監控回應時間**

   HTML注釋可用於在每個頁面的來源中包含響應時間資訊：

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### 搜尋請求 {#search-requests}

搜尋請求對您的網站有重大影響，包括：

* 實際搜尋的回應時間

   * 快速搜尋功能是您網站的品質目標

* 對一般效能的影響

   * 由於搜尋功能必須掃描（可能較大）內容的區段，或是特別擷取的索引，因此若未最佳化，可能會影響整個系統的效能

為搜尋請求設定目標，同樣是體驗問題，具體取決於：

* AEM的體驗
* 評估與其他目標相比使用搜索的頻率
* 您的永續性管理員
* 搜索索引
* 搜索功能的複雜性；一個僅允許輸入1個搜索詞的基本搜索函式比允許用戶使用AND/OR/NOT建立複雜搜索語句的高級搜索更快。

從您的專案開始，就應規劃並整合這些項目。 可監控的機制包括：

* **使用AEM request.log監控搜尋回應時間**

   同樣，request.log可以用來監控搜索請求的響應時間；如需詳 [細資訊，請參閱](/help/sites-deploying/configuring-performance.md) 「效能最佳化」。

* **用於測量搜索響應時間的寫程式機構**

   若要自訂您收集的搜尋請求相關資訊及其效能，建議將資訊收集納入您的專案原始碼中；如需詳 [細資訊，請參閱](/help/sites-deploying/configuring-performance.md) 「效能最佳化」。

### 並行 {#concurrency}

您的網站將可供許多使用者／訪客在作者和發佈環境中使用。 測試時，數字通常比您所用的要多，但也會波動，難以預測。 您的網站需要針對平均同時使用者／訪客數量進行設計，而不需注意到負面效能影響。 同樣， `request.log` 可用於併發測試；如需詳 [細資訊，請參閱](/help/sites-deploying/configuring-performance.md) 「效能最佳化」。

併發用戶數的目標取決於環境類型：

* **作者環境**

   * 通常可以準確估計併發用戶的數量。 您將知道您總共有多少位作者，不過（可能）並非所有作者都會同時使用。

* **發佈環境**

   * 這較難預測，因此您必須選取目標值。 同樣地，這應以您目前網站的體驗，以及對新網站的實際期望為基礎。
   * 特殊事件（例如，當您發佈新的、非常受歡迎的內容時）可能超出預期，甚至超出功能（如某些事件的票證可供銷售時，有時會在媒體上報告）。

### 容量和卷 {#capacity-and-volume}

在討論相關度量之前，請先快速定義術語：

* **卷**

   * 系統處理和傳送的輸出量。

* **容量**

   * 系統提供大量內容的能力。
   * 在每個步驟中，容量和容量的測量都不同，如下表所示。 為獲得最佳效能，請確保每個步驟的容量與卷匹配，並確保所有步驟都共用容量和卷。 例如，您可以在用戶端電腦上計算導覽，或將導覽放入快取中，而不需針對每個要求在伺服器上計算。

* **容量和卷**

   | 什麼／位置 | 容量 | 卷 |
   |---|---|---|
   | 用戶端 | 使用者電腦的計算能力。 | 頁面版面的複雜性。 |
   | 網路 | 網路頻寬。 | 頁面大小（程式碼、影像等）。 |
   | Dispatchercache | Web伺服器的伺服器記憶體（主記憶體和硬碟）。 | Web伺服器（主記憶體和硬碟）。 快取頁面的數目和大小。 |
   | 輸出快取 | AEM伺服器的伺服器記憶體（主記憶體和硬碟）。 | 輸出快取中的頁數和大小、每頁的依賴項數。 調度器快取會降低此卷。 |
   | Web伺服器 | Web伺服器的計算能力。 | 請求數。 快取會降低此卷。 |
   | 範本 | Web伺服器的計算能力。 | 範本的複雜性。 |
   | 存放庫 | 儲存庫的效能。 | 從儲存庫載入的頁數。 |

### 其他量度 {#other-metrics}

上節詳細說明要定義的主要量度。

視您的特定需求而定，單獨定義或將上述分類納入考量的其他量度可能會很有用。

不過，最好有一組精確、可輕鬆可靠運作的核心量度，而不是嘗試測量和定義網站的每個方面。 您的網站完全由其性質決定，一旦交給您的使用者，就會立即開始改變和發展。

## 安全性 {#security}

安全至關重要，而且是一個日益嚴峻的挑戰。 必須 ***從您*** 專案的最早階段開始考慮並規劃它。

The [Security Checklist](/help/sites-administering/security-checklist.md) details steps you should that that you should to berfuce the an your AEM installation is secure when deployed. 其他安全方面則涵蓋在「安 [全性（開發時）」](/help/sites-developing/security.md) 、「使 [用者管理與安全性」中](/help/sites-administering/security.md)。

## 並行和迭代任務 {#parallel-and-iterative-tasks}

>[!NOTE]
>
>以下：
>
>* 提供與AEM專案第 *一次實作* 相關的概觀。
>* 以抽象概述為目的；請參閱 [專案檢查清單](/help/managing/best-practices.md) ，瞭解特定階段／里程碑／任務。
>* 任何時間尺度都是理論上的。
>



對於標準AEM專案的新實作，您需要考慮下列工作：

* 從銷售流程移交。
* 客戶應用程式的實&#x200B;**作**（開發）。
* 在客戶站點（基礎結構）上安裝和配置基礎結構(和相關&#x200B;**流程**)。
* 建立（或移轉）內容(**內容**)。
* 移交給操作(**維護／支援**)。
* 後續發行。

![chlimage_1-2](assets/chlimage_1-2.png)

建議在所有方面使用迭代方法：

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>將專案啟動分割為 **Soft Launch(s)** （可用性降低，多次重複）和 **Hard Launch** （完全可用性——即時），以便在實際的生產環境中進行調整、最佳化和使用者培訓。

>[!NOTE]
>
>如需您 [](/help/managing/best-practices.md) 在專案生命週期中應執行（或評估）的工作範例，請參閱專案檢查清單。

每個類別的注意事項有：

* **開發**

   * 首先定義基本架構。
   * 使用數個迭代(Sprint)進行開發：

      * 首次衝刺相當於第一個全面開發週期。
      * 第一次衝刺會產生第一次部署至您的測試環境。
      * 每次衝刺都有可跑的結果。
      * 每次衝刺都會獲得客戶簽名（結構化測試的最低要求，並提供意見回應）。
   * 針對專案期間可能更新的可用AEM版本進行規劃。
   * 在Sprint期間規劃測試和最佳化。
   * 規劃穩定化和最佳化階段。
   * 建立要計畫用於進一步發行的項目記錄。
   * 規劃合作夥伴的參與與和移交。


* **基礎架構**

   * 首先定義基本體系結構：

      * 定義效能需求。
      * 定義績效目標（即明確定義預期）。
      * 定義硬體和基礎架構架構；包括調整大小。
      * 定義部署。
   * 使用數個迭代；對於第一次衝刺和初始配置準備：

      * 開發環境。
      * 開發流程。
      * 測試環境。
      * 部署程式（包括配置管理）。
   * 規劃數個負載測試。
   * 在Sprint期間規劃測試和最佳化。
   * 規劃穩定化和最佳化階段。
   * 盡早部署至生產環境（讓營運團隊設定系統以取得經驗）。
   * 盡早使用指名用戶和定義的角色。
   * 計畫培訓（例如，管理員培訓）。
   * 規劃移交至營運。



* **內容**

   * 基本架構：
      * 推動內容階層。
      * 有助於定義內容概念。
      * 定義MSM的使用與配置。
      * 定義角色、群組、工作流程和權限。
   * 請考慮離線頁面建立是否有用。
   * 規劃早期建立首頁和內容（用於測試和意見回應）。
   * 規劃現有內容的移轉。
   * 在重構後規劃「in-sprint-migration」。
   * 規劃「內容燒毀」（上線內容的網站地圖）。

## 估計時間和精力 {#estimating-time-and-effort}

然後，您可以根據產生的任務清單對（高級別）任務定義的時間和精力進行初始估計。 這些應包括指出誰（客戶或合作夥伴）將在何時執行什麼工作。

以下清單顯示了標準近似值和所涉及的工作量之間的相互關係，因此包括成本：

>[!CAUTION]
>
>這些數字只能用於初步估計。 經驗豐富的AEM開發人員必須進行詳細分析。

| 相位 | 努力 |
|---|---|
| 開發 | 每個元件節點的粗略估計為2 - 4小時，將涵蓋所有開發需求。 |
| 開發人員測試 | 15%的開發 |
| 後續行動 | 10%的開發 |
| 文件 | 15%的開發 |
| JavaDoc檔案 | 10%的開發 |
| 修正錯誤 | 15%的開發 |
| 專案管理 | 20%的項目成本用於進行中的項目管理和治理 |

然後，詳細規劃可以將可用或所需的資源與期限和成本關聯起來。

## 參考架構 {#reference-architecture}

給出了AEM體系結構的參考體系結構，為AEM體系結構提供了模板解決方案。 該參考體系結構解決了企業系統常遇到的問題，包括擴展、可靠性和安全性。

應定義下列網站度量：

| 分類 | 定義 |
|---|---|
| 網際網路網站數量 |  |
| 內部網站數量 |  |
| 程式碼庫數（例如，如果網際網路和內部網路不同） |  |
| 個別頁數 |  |
| 網站瀏覽次數／日 |  |
| 頁面檢視次數／日 |  |
| 資料傳輸量（以GB為單位）/天 |  |
| 併發用戶數（已關閉的用戶組） |  |
| 並行訪客數（發佈） |  |
| 並行作者數 |  |
| 註冊作者人數 |  |
| 頁面啟動次數／工作日 |  |
| 部署期間啟動頁面的次數 |  |

## 潛在工具概觀 {#overview-of-potential-tools}

提供下列清單，以通知您可使用的工具。 本軟體是作為簡介，而非廣泛的建議清單，而且絕不妨礙您使用您偏好的其他工具。

<table>
 <tbody>
  <tr>
   <td><strong>產品</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>AEM本身提供多種機制，可協助您監控、測試、調查和除錯應用程式；包括：</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">開發人員模式</a></li>
     <li>測試 <a href="/help/sites-developing/hobbes.md">主控台</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">操作儀表板</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">內容分析</a></li>
     <li>內 <a href="/help/sites-authoring/author-environment-tools.md#content-tree">容樹</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>硒</td>
   <td><a href="https://docs.seleniumhq.org/">Selenium</a> 是Open Source測試工具。 測試會直接在瀏覽器中執行——模擬您的使用者工作方式。</td>
  </tr>
  <tr>
   <td>Microsoft Project</td>
   <td>常用的專案管理工具。</td>
  </tr>
  <tr>
   <td>吉拉</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> 是Open Source（開放原始碼）工具，可追蹤和管理軟體錯誤的詳細資料。 工作流程可視需要強加至錯誤詳細資訊。</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> 是修訂控制軟體。</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse是Open Source IDE，由各種專案組成。 這些解決方案的重點是建立由可擴充的架構、工具和執行階段所組成的開放式開發平台，以便在整個生命週期中建立、部署和管理軟體。</p> <p>如需詳 <a href="/help/sites-developing/howto-projects-eclipse.md">細資訊，請參閱如何使用Eclipse開發AEM專案</a> 。</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>專業（因此需要承擔許可成本）的IDE，提供全方位的功能。 </p> <p>如需 <a href="/help/sites-developing/ht-intellij.md">詳細資訊，請參閱如何使用IntelliJ IDEA開發AEM專案</a> 。</p> </td>
  </tr>
  <tr>
   <td>馬文</td>
   <td><a href="https://maven.apache.org/">Maven</a> 是軟體專案管理與理解工具，可管理專案的建立程式（軟體和檔案）。</td>
  </tr>
 </tbody>
</table>

## 進一步閱讀 {#further-reading}

此外，以下各節特別感興趣：

* [快速入門](/help/sites-deploying/deploy.md#getting-started)
* [技術需求](/help/sites-deploying/technical-requirements.md)
* [監控和維護實例](/help/sites-deploying/monitoring-and-maintaining.md)

### Best Practices {#best-practices}

Adobe針對所有階段和受眾提供進一步的最佳實務：

* [部署](/help/sites-deploying/best-practices.md)
* [製作](/help/sites-authoring/best-practices.md)
* [管理](/help/sites-administering/administer-best-practices.md)
* [開發](/help/sites-developing/best-practices.md)
* [專案管理](/help/managing/best-practices.md)