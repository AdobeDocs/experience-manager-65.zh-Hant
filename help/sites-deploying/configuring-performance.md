---
title: 效能優化
description: 瞭解如何配置某些方面AEM以優化效能。
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
feature: Configuring
exl-id: 5b0c9a8c-0f5f-46ee-a455-adb9b9d27270
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6503'
ht-degree: 12%

---

# 效能優化 {#performance-optimization}

>[!NOTE]
>
>有關效能的一般准則，請閱讀 [效能指南](/help/sites-deploying/performance-guidelines.md) 的子菜單。
>
>有關故障排除和修復效能問題的詳細資訊，另請參閱 [效能樹](/help/sites-deploying/performance-tree.md)。
>
>此外，您還可以查看 [效能調整提示](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hant)。

一個關鍵問題是您的網站響應訪問者請求所花費的時間。 儘管此值因每個請求而異，但可以定義平均目標值。 一旦這個價值被證明是可實現和可維護的，就可以用來監測網站的效能並指出潛在問題的發展。

您所希望的響應時間在作者和發佈環境上是不同的，反映了目標受眾的不同特徵：

## 作者環境 {#author-environment}

此環境由輸入和更新內容的作者使用。 它必須滿足在更新內容頁面和這些頁面上的單個元素時，每個用戶都生成大量效能密集型請求的少數用戶。

## 發佈環境 {#publish-environment}

此環境包含可供用戶使用的內容。 在這裡，請求數量更多，速度也同樣重要。 但是，由於這些請求的性質不那麼動態，因此可以採用額外的效能增強機制；例如快取內容或負載平衡。

>[!NOTE]
>
>* 配置效能優化後，請按照中的步驟操作 [艱難的一天](/help/sites-developing/tough-day.md) test環境。
>* 另請參閱 [效能調整提示。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hant)


## 效能優化方法 {#performance-optimization-methodology}

「項目」的效能優AEM化方法可以用五條簡單的規則進行總結，這些規則可以遵循，從一開始就避免效能問題：

1. [優化計畫](#planning-for-optimization)
1. [模擬現實](#simulate-reality)
1. [確立堅實的目標](#establish-solid-goals)
1. [保持相關性](#stay-relevant)
1. [敏捷迭代循環](#agile-iteration-cycles)

這些規則一般適用於Web項目，與項目經理和系統管理員相關，以確保其項目在啟動時不會面臨效能挑戰。

### 優化計畫 {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

在效能優化階段計畫大約10%的項目工作。 實際效能優化要求取決於項目的複雜性水準和開發團隊的經驗。 儘管您的項目可能（最終）不需要分配時間，但最好始終在建議的區域中規劃效能優化。

在可能的情況下，首先應將項目軟啟動給有限的受眾，以收集真實體驗並進行進一步的優化，而不必在發佈完整產品後承受額外壓力。

在您「即時」後，效能優化尚未結束。 此時，您將體驗系統上的「真實」負載。 在發射後，必須計畫進行進一步調整。

由於系統負載更改，並且系統的效能配置檔案會隨時間而變化，因此應將效能「調整」或「運行狀況檢查」安排在6至12個月的間隔內。

### 模擬現實 {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

如果您與一個網站一起直播，那麼在發佈後發現您遇到效能問題，可能是因為您的負載和效能test並不能夠充分模擬現實。

模擬現實是困難的，而你想要投入多少精力來實現「真實」取決於你項目的性質。 &quot;Real&quot;不僅指&quot;真實代碼&quot;和&quot;真實通信&quot;，還指&quot;真實內容&quot;，特別是關於內容大小和結構的內容。 根據儲存庫的大小和結構，模板的行為可能會有所不同。

### 確立堅實的目標 {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

正確制定業績目標的重要性不容低估。 通常，在人們專注於特定的績效目標後，即使這些目標是基於假設，也很難在事後改變。

確立良好、穩健的業績目標確實是最棘手的領域之一。 通常最好從可比網站（例如新網站的前身）收集真實生活日誌和基準。

### 保持相關性 {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

一次優化一個瓶頸是十分重要的。 如果您嘗試並行執行操作而未驗證一次優化的影響，則可能會丟失對哪個優化度量有幫助的跟蹤。

### 敏捷迭代循環 {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

效能調整是一個迭代過程，涉及、測量、分析、優化和驗證，直到達到目標。 為瞭解決這一問題，在優化階段實施敏捷的驗證過程，而不是在每次迭代後執行更重的測試過程。

這一重點意味著實施優化的開發人員應快速判斷優化是否已達到目標。 這些資訊很有價值，因為當達到目標時，優化就結束了。

## 基本效能指南 {#basic-performance-guidelines}

通常，將未快取的html請求保持在100毫秒以內。 具體而言，以下可作為准則：

* 70%的頁面請求應在不到100毫秒內得到響應。
* 25%的頁面請求應在100毫秒 — 300毫秒內得到響應。
* 4%的頁面請求應在300毫秒 — 500毫秒內得到響應。
* 1%的頁面請求應在500毫秒內得到響應，即1000毫秒。
* 任何頁面的響應速度都不應低於1秒。

上述數字假設以下條件：

* 在發佈時衡量（沒有與創作環境相關的間接費用）
* 在伺服器上測量（無網路開銷）
* 未快取(無AEM輸出快取，無Dispatcher快取)
* 僅適用於具有多個依賴關係的複雜項目(HTML、JS、PDF...)
* 系統上沒有其他負載

有些問題經常導致效能問題，包括：

* Dispatcher快取低效
* 在普通顯示模板中使用查詢。

JVM和OS級別調整通常不會導致效能的顯著飛躍，因此應在優化週期的最後階段執行。

內容儲存庫的結構方式也會影響效能。 為獲得最佳效能，連接到內容儲存庫中各個節點的子節點數不應超過1,000（作為規則）。

在通常的效能優化練習中，您的好友是：

*  `request.log`
* 基於元件的定時
* Java™探查器。

### 載入和編輯數字資產時的效能 {#performance-when-loading-and-editing-digital-assets}

由於載入和編輯數字資產時涉及大量資料，因此效能可能成為一個問題。

這裡有兩個因素影響效能：

* CPU — 多核在轉碼時使工作更加順暢
* 硬碟 — 並行RAID磁碟實現相同

要提高效能，請考慮以下因素：

* 每天要上載多少個資產？ 可以基於以下各項作出良好估計：

![chlimage_1-77](assets/chlimage_1-77.png)

* 編輯的時間框架（通常為工作日的長度，對於國際業務更多）。
* 上載的影像的平均大小（以及每個影像生成的格式副本的大小）(MB)。
* 確定平均資料速率：

![chlimage_1-78](assets/chlimage_1-78.png)

* 80%的編輯是在20%的時間內完成的，因此在高峰時間，您的資料速率是平均資料速率的四倍。 這樣的表現是你的目標。

## 效能監控 {#performance-monitoring}

效能（或缺乏效能）是用戶首先注意到的問題之一，因此，與任何具有用戶介面的應用程式一樣，效能至關重要。 要優化安裝效能，AEM請監視實例的各種屬性及其行為。

有關如何執行效能監視的資訊，請參見 [監視效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)。

導致效能問題的問題往往難以跟蹤，即使它們的影響很容易看到。

一個基本的出發點是在系統正常運行時對系統有良好的瞭解。 除非您知道環境在正常運行時「外觀」和「行為」如何，否則很難在效能惡化時找到問題所在。 在系統正常運行時花費時間進行調查，並確保收集效能資訊是一項持續的任務。 這樣，您就可以在業績受到影響時進行比較。

下圖說明了內容請求可以採AEM取的路徑，因此說明了影響效能的不同元素的數量。

![chlimage_1-79](assets/chlimage_1-79.png)

效能也是卷和容量之間的平衡：

* **卷**  — 系統處理和交付的輸出量。
* **容量**  — 系統交付卷的能力。

在整個網路鏈的各個位置都可以顯示效能。

![chlimage_1-80](assets/chlimage_1-80.png)

有幾個功能區域通常會影響效能：

* 快取
* 應用程式（您的項目）代碼
* 搜索功能

### 效能基本規則 {#basic-rules-regarding-performance}

在優化效能時，應牢記以下某些規則：

* 效能調整 *必須* 是每個項目的一部分。
* 不要在開發週期的早期進行優化。
* 效能僅與最薄弱的環節一樣好。
* 始終考慮容量與容量。
* 首先優化重要事物。
* 不優化 *現實* 目標。

>[!NOTE]
>
>請記住，您用於衡量績效的機制通常會影響您正嘗試衡量的內容。 設法解釋這些差異，盡可能消除其影響；尤其是，應盡可能取消激活瀏覽器插件。

## 配置效能 {#configuring-for-performance}

可以配置AEM（和/或基礎儲存庫）的某些方面以優化效能。 以下是可能性和建議，您必須確定是否或如何在進行更改之前使用相關功能。

>[!NOTE]
>
>請參閱 [效能優化](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hant)。

### 搜索索引 {#search-indexing}

從6AEM.0開始，Adobe Experience Manager使用基於Oak的儲存庫體系結構。

您可以在以下位置找到更新的索引資訊：

* [查詢和索引的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [查詢和索引](/help/sites-deploying/queries-and-indexing.md)

### 併發工作流處理 {#concurrent-workflow-processing}

要提高效能，請限制併發運行的工作流進程數。 預設情況下，工作流引擎並行處理的工作流數與Java™ VM可用的處理器數一樣多。 當工作流步驟需要大量處理資源（RAM或CPU）時，並行運行其中的幾個工作流會對可用伺服器資源提出很高要求。

例如，當上載映像（或通常的DAM資產）時，工作流會自動將映像導入DAM。 影像通常具有高解析度，並且很容易耗用數百MB的堆來處理。 並行處理這些影像給儲存子系統和垃圾收集器帶來高負載。

工作流引擎使用Apache Sling作業隊列來處理和調度工作項處理。 預設情況下，已從Apache Sling作業隊列配置服務工廠建立以下作業隊列服務以處理工作流作業：

* 花崗岩工作流隊列：大多數工作流步驟（如處理DAM資產的步驟）都使用「花崗岩工作流隊列」服務。
* 花崗岩工作流外部進程作業隊列：此服務用於特殊的外部工作流步驟，這些步驟通常用於聯繫外部系統並輪詢結果。 例如，InDesign介質提取過程步驟被實現為外部過程。 工作流引擎使用外部隊列來處理輪詢。 (請參閱 [com.day.cq.workflow.exec.WorkflowExternalProcess](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html)。)

配置這些服務以限制併發運行的工作流進程的最大數量。

>[!NOTE]
>
>配置這些作業隊列會影響所有工作流，除非您為特定工作流模型建立了作業隊列(請參閱 [配置特定工作流模型的隊列](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) )。

#### 儲存庫中的配置 {#configuration-in-the-repo}

如果要配置服務 [使用sling:OsgiConfig節點](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)，必須找到現有服務的PID，例如：org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705。 可以使用Web控制台來發現PID。

配置名為 `queue.maxparallel`。

#### Web控制台中的配置 {#configuration-in-the-web-console}

配置這些服務 [使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，在Apache Sling Job Queue Configuration服務工廠下找到現有配置項。

配置名為「最大並行作業」的屬性。

### 配置特定工作流的隊列 {#configure-the-queue-for-a-specific-workflow}

為特定工作流模型建立作業隊列，以便您可以配置該工作流模型的作業處理。 這樣，您的配置會影響特定工作流的處理，而預設的「花崗岩工作流隊列」的配置會控制其他工作流的處理。

當工作流模型執行時，它們會為特定主題建立Sling作業。 預設情況下，該主題與為常規花崗岩工作流隊列或花崗岩工作流外部進程作業隊列配置的主題匹配：

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

工作流模型生成的實際作業主題包括特定於模型的尾碼。 例如， **DAM更新資產** 工作流模型生成具有以下主題的作業：

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

因此，您可以為與工作流模型的作業主題匹配的主題建立作業隊列。 配置隊列的效能相關屬性只影響生成與隊列主題匹配的作業的工作流模型。

以下過程使用 **DAM更新資產** 以工作流為例。

1. 執行要為其建立作業隊列的工作流模型，以便生成主題統計資訊。 例如，向Assets添加映像以執行 **DAM更新資產** 工作流。
1. 開啟Sling作業控制台(`https://<host>:<port>/system/console/slingevent`)。
1. 在控制台中發現與工作流相關的主題。 對於DAM更新資產，可找到以下主題：

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. 為每個主題建立一個作業隊列。 要建立作業隊列，請為Apache Sling作業隊列工廠服務建立工廠配置。

   工廠配置與中所述的花崗岩工作流隊列類似 [併發工作流處理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)，但「主題」屬性與工作流作業的主題匹配除外。

### DAMAEM資產同步服務 {#cq-dam-asset-synchronization-service}

的 `AssetSynchronizationService` 用於同步來自已裝載儲存庫（包括LiveLink、Documentum®等）的資產。 預設情況下，此同步每300秒（5分鐘）進行一次定期檢查，因此如果不使用已裝載的資料庫，則可以禁用此服務。

禁用服務由 [配置OSGi服務](/help/sites-deploying/configuring-osgi.md) **CQ DAM資產同步服務** 設定 **同步期間** ( `scheduler.period`)到（最少為）一年（以秒為單位定義）。

### 多個DAM實例 {#multiple-dam-instances}

部署多個DAM實例有助於在以下情況下實現效能：

* 由於為作者環境定期上載許多資產，您的負載很高；這裡，可以專門為作者提供服務。
* 您在全球各地（例如美國、歐洲、亞洲）擁有多個團隊。

其他注意事項包括：

* 將作者&quot;在製品&quot;與出版&quot;最終&quot;分開
* 將作者內部用戶與發佈時的外部訪問者/用戶分開（例如，代理、新聞代表、客戶和學生）。

## 質量保證的最佳做法 {#best-practices-for-quality-assurance}

效能對您的發佈環境至關重要。 因此，在實施項目時，必須仔細規劃和分析您對發佈環境的績效test。

本節旨在對定義test概念時涉及的問題進行標準化概述，該概念專門用於在您的 *發佈* 環境。 此資訊主要對QA工程師、項目經理和系統管理員感興趣。

下面介紹了對上的應用程式執行效能testAEM的標準化方法 *發佈* 環境。 此效能test涉及以下五個階段：

* [知識驗證](#verification-of-knowledge)
* [範圍定義](#scope-definition)
* [Test方法](#test-methodologies)
* [績效目標的定義](#defining-the-performance-goals)
* [優化](#optimization)

控制是一個額外的、全面的過程 — 必需的，但不限於測試。

### 知識驗證 {#verification-of-knowledge}

第一步是記錄您在開始測試之前必須知道的基礎資訊：

* 您的test環境的體系結構
* 詳細描述需要測試的內部元素（隔離和組合）的應用程式圖

#### Test體系結構 {#test-architecture}

記錄用於效能測試的test環境的體系結構。

您需要複製計畫的生產發佈環境，以及Dispatcher和Load Balancer。

#### 應用程式映射 {#application-map}

獲取一個清晰的概述，您可以從中建立整個應用程式的映射(您可能已經通過「作者」環境上的test獲得了此映射)。

圖表表示了應用程式的內部元素，可以給出測試要求的概述；通過顏色編碼，它還可以作為報告的基礎。

### 範圍定義 {#scope-definition}

應用程式通常具有一系列使用案例。 有些使用案例很重要，有些則不那麼重要。

要將效能測試範圍集中在發佈上，Adobe建議您定義以下內容：

* 最重要的業務使用案例
* 最關鍵的技術使用案例

使用案例的數量由您決定，但應限於易於管理的數量（例如，介於5到10之間）。

一旦選擇了關鍵使用案例，就可以為每個案例定義關鍵績效指標(KPI)和用於衡量它們的工具。 常見KPI示例包括：

* 端到端響應時間
* Servlet響應時間
* 單個元件的響應時間
* 服務的響應時間
* 線程池中空閒線程數
* 可用連接數
* 系統資源（如CPU和I/O訪問）

### Test方法 {#test-methodologies}

此概念有四個用於定義和測試效能目標的方案：

* 單元件test
* 組合元件test
* *上線* 場景
* 錯誤方案

根據以下原則。

#### 元件斷點 {#component-breakpoints}

* 每個元件在與效能相關時具有特定的斷開點。 即，一個元件可以顯示良好的效能直到達到某個特定的點，然後效能會迅速降低。
* 要獲得應用程式的完整概述，必須首先驗證元件以確定何時到達每個元件的斷點。
* 要查找可以執行載入test的斷點，在該斷點中，在一段時間內，您將增加用戶數以建立不斷增加的載入。 通過監視此負載和元件的響應，在達到元件的斷開點時，會遇到特定的效能行為。 該點可以按每秒併發事務處理數以及併發用戶數（如果元件對此KPI很敏感）來限定。
* 然後，此資訊可以作為改進的基準，指示所使用測量的效率，並幫助定義test方案。

#### 交易記錄 {#transactions}

* 術語事務用於表示完整網頁的請求，包括頁面本身和所有後續調用。 即，頁面請求、任何調AJAX用、影像和其他對象 **請求向下鑽取**。
* 要全面分析每個請求，您可以表示調用堆棧的每個元素，然後合計每個元素的平均處理時間。

### 定義績效目標 {#defining-the-performance-goals}

在定義範圍和相關KPI後，將設定特定績效目標。 這一過程包括設計test情景和目標值。

Test效能在平均和峰值條件下都表現良好。 此外，您需要Going Live方案test，以確保您能夠在網站首次發佈時滿足對網站的更多興趣。

您從現有網站收集的任何經驗或統計資訊在確定未來目標時也非常有用。 例如，來自您現場網站的頂級流量。

#### 單元件Test {#single-component-tests}

必須在平均和峰值條件下測試關鍵元件。

在這兩種情況下，當預定義數量的用戶使用系統時，您都可以定義每秒的預期事務數。

| Component | Test類型 | 否. 用戶 | Tx/秒（預期） | Tx/秒（已測試） | 說明 |
|---|---|---|---|---|---|
| 首頁單用戶 | 平均 | 1 | 1 |  |  |
|  | 峰 | 1 | 3 |  |  |
| 首頁100個用戶 | 平均 | 100 | 3 |  |  |
|  | 峰 | 100 | 3 |  |

#### 組合元件Test {#combined-component-tests}

組合測試元件可以更仔細地反映應用行為。 必須再次測試平均和峰值條件。

| 方案 | Component | 否. 用戶 | Tx/秒（預期） | Tx/秒（已測試） | 說明 |
|---|---|---|---|---|---|
| 混合平均 | 首頁 | 10 | 1 |  |  |
|  | 搜尋 | 10 | 1 |  |  |
|  | 新聞 | 10 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 激活 | 10 | 3 |  | 模擬作者行為。 |
| 混合峰 | 首頁 | 100 | 5 |  |  |
|  | 搜尋 | 50 | 5 |  |  |
|  | 新聞 | 100 | 10 |  |  |
|  | 事件 | 100 | 10 |  |  |
|  | 激活 | 20 | 20 |  | 模擬作者行為。 |

#### 正在進行即時Test {#going-live-tests}

在網站上市後的頭幾天，您可以預期興趣會增加。 此方案甚至比您正在測試的峰值還要大。 Adobe建議您test「即時」方案，以確保系統能夠滿足此情況。

| 方案 | Test類型 | 否. 用戶 | Tx/秒（預期） | Tx/秒（已測試） | 說明 |
|---|---|---|---|---|---|
| 上即時峰 | 首頁 | 200 | 20 |  |  |
|  | 搜尋 | 100 | 10 |  |  |
|  | 新聞 | 200 | 20 |  |  |
|  | 事件 | 200 | 20 |  |  |
|  | 激活 | 20 | 20 |  | 模擬作者行為。 |

#### 錯誤方案Test {#error-scenario-tests}

Test錯誤情形，以確保系統正確、適當地反應。 不僅在於錯誤本身的處理方式，還在於它對效能的影響。 例如：

* 當用戶嘗試在搜索框中輸入無效的搜索項時會發生什麼
* 當搜索項如此一般，以致返回過多的結果時會發生什麼

在設計這些test時，應該記住並非所有情景都會定期發生。 但是，它們對整個系統的影響是重要的。

| 錯誤方案 | 錯誤類型 | 否. 用戶 | Tx/秒（預期） | Tx/秒（已測試） | 說明 |
|---|---|---|---|---|---|
| 搜索元件重載 | 搜索全局通配符（星號） | 10 | 1 |  | 僅&amp;ast;&amp;ast;&amp;ast;的子菜單。 |
|  | 停止字 | 20 | 2 |  | 搜索停止字。 |
|  | 空字串 | 10 | 1 |  | 正在搜索空字串。 |
|  | 特殊字元 | 10 | 1 |  | 正在搜索特殊字元。 |

#### 耐力Test {#endurance-tests}

只有在系統連續運行一段時間後，才會遇到某些問題。 使用耐力test來test在所需時間週期內的恆定平均載荷。 然後可以分析任何效能降級。

| 方案 | Test類型 | 否. 用戶 | Tx/秒（預期） | Tx/秒（已測試） | 說明 |
|---|---|---|---|---|---|
| 耐力test（72小時） | 首頁 | 10 | 1 |  |  |
|  | 搜尋 | 10 | 1 |  |  |
|  | 新聞 | 20 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 激活 | 1 | 3 |  | 模擬作者行為。 |

### 優化 {#optimization}

在後期實施階段，優化應用程式以實現並最大化效能目標。

必須測試所做的任何優化，以確保它們具有：

* 不影響功能
* 在釋放之前已通過載入test驗證

您可以選擇一些工具來幫助您進行負載生成、效能監控和結果分析。 其中一些工具包括：

* [JMeter](https://jmeter.apache.org/)
* [載入運行器](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)
* [紅外線](https://www.infraredsoftware.com/)
* [Java™互動式配置檔案](https://jiprof.sourceforge.net/)

優化後，再次test以確認影響。

### 報告 {#reporting}

持續報告可讓所有人瞭解狀態。 如前所述，使用顏色編碼時，可以使用體系結構圖來處理此狀態。

完成所有test後，報告以下內容：

* 遇到任何嚴重錯誤
* 仍需進行更多調查的非關鍵問題
* 在測試期間作出的任何假設
* 測試中需要提出的任何建議

## 使用Dispatcher時優化效能 {#optimizing-performance-when-using-the-dispatcher}

的 [調度程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 是Adobe的快取和/或負載平衡工具。 使用Dispatcher時，請考慮優化您的網站以獲得快取效能。

>[!NOTE]
>
>Dispatcher版本與AEM無關，但Dispatcher文檔嵌入到文檔AEM中。 請始終使用文檔中嵌入的Dispatcher文檔獲取最新版本AEM。
>
>如果您依循連結至 Dispatcher 文件，且該連結內嵌於舊版 AEM 的文件中，您可能會被重新導向至本頁。

Dispatcher提供了幾種內置機制，如果您的網站利用這些機制，您可以使用這些機制來優化效能。 本節將說明如何設計網站，好讓快取的優點最大化。

>[!NOTE]
>
>記住 Dispatcher 會將快取儲存在標準網頁伺服器上可能會有所幫助。 瞭解此資訊意味著您可以使用URL將所有可以儲存為頁面和請求的內容都快取。 而且，您不能儲存其他內容，如cookie、會話資料和表單資料。
>
>通常，許多快取策略都涉及選擇好的URL，而不依賴於此附加資料。
>
>使用Dispatcher 4.1.11版，您還可以快取響應標頭，請參見 [快取HTTP響應標頭](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)。

### 計算Dispatcher快取比率 {#calculating-the-dispatcher-cache-ratio}

快取比率公式估計快取處理的請求在進入系統的請求總數中所佔的百分比。 要計算快取比率，需要執行以下操作：

* 請求總數。 此資訊可在Apache中找到 `access.log`。 有關詳細資訊，請參閱 [正式Apache文檔](https://httpd.apache.org/docs/2.4/logs.html#accesslog)。

* 發佈實例所服務的請求數。 此資訊可在 `request.log` 例子。 有關詳細資訊，請參閱 [解釋request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) 和 [查找日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files)。

計算快取比率的公式為：

* (請求總數 **減** 發佈上的請求數) **劃分** 按請求總數計算。

例如，如果請求總數為129491，而Publish實例所服務的請求數為58959，則快取比率為： **(129491 - 58959)/129491= 54.5%**。

如果您沒有一對一的發佈程式/調度程式配對，請將來自所有調度程式和發佈程式的請求添加到一起，以獲得準確的度量。 另請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md)。

>[!NOTE]
>
>為獲得最佳效能，Adobe建議將快取比率90%到95%。

#### 使用一致的頁面編碼 {#using-consistent-page-encoding}

使用Dispatcher 4.1.11版，可以快取響應標頭。 如果未在Dispatcher上快取響應標頭，則如果將頁編碼資訊儲存在標頭中，則可能會出現問題。 在此情況下，當 Dispatcher 從快取中提供頁面時，將會對此頁面使用網頁伺服器的預設編碼。 有兩種方式可避免此問題：

* 如果您只使用一種編碼，請確定在網頁伺服器上使用的編碼與 AEM 網站的預設編碼相同。
* 要設定編碼，請使用 `<META>` HTML `head` 部分，如下例所示：

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### 避免 URL 參數 {#avoid-url-parameters}

可能的話，請避免針對您想要快取的頁面使用 URL 參數。 例如，如果您有圖片庫，則絕對不會快取以下 URL (除非 Dispatcher [已適當地設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache))：

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

不過，您可以將這些參數放到頁面 URL 中，如下所示：

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>此URL調用與 `gallery.html`。 在範本定義中，您可以指定哪一個指令碼會轉譯頁面，或者針對所有頁面使用相同指令碼。

#### 使用 URL 自訂 {#customize-by-url}

如果您允許使用者變更字體大小 (或是其他任何版面自訂內容)，請確定不同自訂內容會反映在 URL 中。

例如，不會快取 Cookie，所以如果您將字體大小儲存在 Cookie (或類似機制) 中，將不會為快取頁面保留字體大小。 因此，Dispatcher 會隨機傳回任何字體大小的文件。

在 URL 中包含字體大小當作選擇器可避免這個問題：

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>對於大多數佈局方面，也可以使用樣式表或客戶端指令碼，或兩者。 這些儀器與快取功能配合良好。
>
>此策略對於打印版本也很有用，在該版本中，您可以使用URL，例如：
>
>`www.myCompany.com/news/main.print.html`
>
>使用範本定義的指令碼萬用字元時，您可以指定轉譯列印頁面的個別指令碼。

#### 讓用作標題的影像檔案失效 {#invalidating-image-files-used-as-titles}

如果您將頁面標題或其他文字轉譯為圖片，建議您儲存檔案，以便在頁面內容更新時將其刪除：

1. 將影像檔案放在與頁面相同的資料夾中。
1. 針對影像檔案使用以下命名格式：

   `<page file name>.<image file name>`

例如，可以儲存頁面標題 `myPage.html` 的 `file myPage.title.gif`。 頁面更新時會自動刪除此檔案，所以對頁面標題所做的任何變更都會自動反映到快取中。

>[!NOTE]
>
>影像檔案不一定實際存在於 AEM 執行個體上。 您可以使用可動態建立影像檔案的指令碼。 然後 Dispatcher 會將檔案儲存在網頁伺服器上。

#### 讓用於導覽的影像檔案失效 {#invalidating-image-files-used-for-navigation}

如果將圖片用於導航條目，則方法與標題基本相同，但稍複雜一些。 將所有導覽影像與目標頁面一起儲存。 如果您將兩張圖片用於一般和活躍情境，可以使用以下指令碼：

* 正常顯示頁面的指令碼。
* 處理「.normal」請求並傳回正常圖片的指令碼。
* 處理「.active」請求並傳回已啟用的圖片的指令碼。

使用與頁面相同的命名句柄建立這些圖片非常重要，以確保內容更新會刪除這些圖片和頁面。

對於未修改的頁面，儘管頁面本身自動失效，但圖片仍保留在快取中。

#### 個人化 {#personalization}

建議將個性化限制到必要的位置。 以下說明原因：

* 如果您使用可自由地自訂的起始頁，則每次使用者請求該頁面時都必須編寫它。
* 相反，如果您提供十個不同的起始頁，則可以快取其中的每個頁，從而提高效能。

>[!TIP]
>有關配置Dispatcher快取的詳細資訊，請參見 [DispatcherAEM快取教程](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html) 及其章節 [快取受保護的內容。](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html#dispatcher-tips-and-tricks)

如果通過將用戶名稱放入標題欄來個性化每個頁面（例如），則會對效能產生影響。

>[!TIP]
>有關快取安全內容，請參見 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hant) 中。

關於將受限內容和公共內容混合到一個頁面上，請考慮使用伺服器端在Dispatcher中包括的策略，或客戶端在瀏覽器中通過Ajax包括的策略。

>[!TIP]
>
>有關處理混合的公共內容和受限內容，請參見 [設定Sling Dynamic Include。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html)

#### 黏性連線 {#sticky-connections}

[黏性連線](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en#the-benefits-of-load-balancing)可確保同一個使用者的文件都會在相同伺服器上編寫。 如果使用者離開此資料夾並於稍後返回，連線仍然保持不變。 要保存需要網站粘滯連接的所有文檔，請定義一個資料夾。 試著不要將其他文件放在該資料夾中。 如果使用個性化頁面和會話資料，則此方案會影響負載平衡。

#### MIME 類型 {#mime-types}

瀏覽器可使用兩種方式來判斷檔案的類型：

1. 按其擴展(例如， `.html`。 `.gif`, `.jpg`)。
1. 透過伺服器隨著檔案一起傳送的 MIME 類型。

對於大多數檔案，MIME 類型會隱含在副檔名中。 就是，

1. 按其擴展(例如， `.html`。 `.gif`, `.jpg`)。
1. 透過伺服器隨著檔案一起傳送的 MIME 類型。

如果檔案名稱沒有副檔名，則會顯示為純文字。

使用Dispatcher 4.1.11版，可以快取響應標頭。 如果未快取Dispatcher上的響應標頭，則MIME類型是HTTP標頭的一部分。 因此，如果應用AEM程式返回的檔案沒有識別的檔案結尾，而是依賴MIME類型，則這些檔案可能會錯誤顯示。

若要確保檔案可以正確地快取，請遵循以下準則：

* 確定檔案總是有適當的副檔名。
* 避免使用URL(如 `download.jsp?file=2214`。 要使用包含檔案規範的URL，請重寫指令碼。 對於上例，此重寫是 `download.2214.pdf`。

## 備份效能 {#backup-performance}

本節介紹一系列基準，用於評估備份效能AEM和備份活動對應用程式效能的影響。 備AEM份在系統運行時給系統帶來很大負載，Adobe會測量這種影響，以及嘗試調制這些影響的備份延遲設定的影響。 其目標是提供一些參考資料，說明在實際配置和生產資料數量中備份的預期效能，並就如何估計計畫系統的備份時間提供指導。

### 參考環境 {#reference-environment}

#### 物理系統 {#physical-system}

本文檔中報告的結果是從參考環境中運行的基準中獲得的，具有以下配置。 此配置類似於資料中心中的典型生產環境：

* HP ProLiant DL380 G6,8個CPU x 2.533 GHz
* 串列連接SCSI 300 GB,10,000-RPM驅動器
* 硬體RAID控制器；RAID0+5陣列中的八個驅動器
* VMware映像CPU x 2英特爾至強® E5540,2.53 GHz
* Red Hat® Linux® 2.6.18-194.el5;Java™ 1.6.0_29
* 單作者實例

此伺服器上的磁碟子系統是快速的，可代表生產伺服器中可能使用的高效能RAID配置。 備份效能對磁碟效能非常敏感，此環境的結果反映了快速RAID配置的效能。 VMWare映像配置為在RAID陣列上具有物理駐留在本地磁碟儲存中的單個大磁碟卷。

配AEM置將儲存庫和資料儲存放在作業系統和軟體的同一邏輯AEM卷上。 備份的目標目錄也位於此邏輯檔案系統上。

#### 資料卷 {#data-volumes}

下表說明了備份基準中使用的資料卷的大小。 首先安裝初始基線內容，然後添加額外的已知資料量以增加備份內容的大小。 以特定的增量建立備份，以表示內容和一天內可能產生的內容大幅增加。 內容（頁面、影像、標籤）的分佈大致基於真實的生產資產組合。 頁面、影像和標籤最多限制為800個子頁面。 每個頁面都包括標題、Flash、文本/影像、視頻、幻燈片、表單、表格、雲和旋轉木馬元件。 映像從400個唯一檔案大小從37 KB到594 KB的池上傳。

| 內容 | 節點 | 頁面 | 影像 | 標記 |
|---|---|---|---|---|
| 基本安裝 | 69 610 | 562 | 256 | 237 |
| 用於增量備份的小內容 |  | +100 | +2 | +2 |
| 用於完整備份的大型內容 |  | +10 000 | +100 | +100 |

在每次重複時添加的附加內容集中重複備份基準。

#### 基準方案 {#benchmark-scenarios}

備份基準包括兩種主要情形：在系統應用程式負載較重時進行備份，在系統空閒時進行備份。 儘管一般建議在盡可能空閒時AEM執行備份，但在某些情況下，必須在系統負載不足時運行備份。

* **空閒狀態**  — 執行備份時沒有其他活AEM動。
* **負載**  — 備份是在系統從聯機進程負載不足80%時執行的。 備份延遲會隨負載變化而變化。

從伺服器日誌中獲取備份時間和結果備份AEM的大小。 通常建議將備份安排在空閒時AEM的非工作時間，例如在午夜。 這一設想方案代表了所建議的方法。

載入由建立的頁面、刪除的頁面、遍歷和查詢組成，其中最大載入來自頁面遍歷和查詢。 添加和刪除過多頁會不斷增大工作區大小並阻止備份完成。 指令碼使用的載入分佈為75%頁遍歷、24%查詢和1%頁建立（沒有嵌套子頁的單級）。 空閒系統上的每秒峰值平均事務數是使用四個並行線程實現的，該並行線程用於在負載下測試備份。

負載對備份效能的影響可以通過具有此應用程式負載和沒有此應用程式負載時的效能差異來估計。 通過比較每小時在進行和不進行並行備份時的事務處理場景吞吐量，以及在不同「備份延遲」設定下運行備份，可以發現備份對應用程式吞吐量的影響。

* **延遲設定**  — 對於其中幾種情形，備份延遲設定也會變化，使用10毫秒（預設）、1毫秒和0毫秒的值來探索此設定如何影響備份效能。
* **備份類型**  — 所有備份都是將儲存庫外部備份到備份目錄而不建立zip ，但在比較中，除了直接使用tar命令。 由於無法將增量備份建立到zip檔案，或者當以前的完全備份是zip檔案時，備份目錄方法是生產情況中最常用的方法。

### 結果摘要 {#summary-of-results}

#### 備份時間和吞吐量 {#backup-time-and-throughput}

這些基準測試的主要結果是顯示備份時間隨備份類型和資料總量的變化而變化。 下圖顯示了使用預設備份配置獲得的備份時間，這是總頁數的函式。

![chlimage_1-81](assets/chlimage_1-81.png)

空閒實例上的備份時間相當一致，平均每秒0.608 MB，而不考慮完整備份或增量備份（請參見下圖）。 備份時間只是備份資料量的函式。 完成完整備份的時間會隨著頁面總數的增加而明顯增加。 完成增量備份的時間也隨著頁總數的增加而增加，但速度要低得多。 由於備份的資料量相對較少，完成增量備份所花的時間要短得多。

備份的大小是完成備份所花時間的主要決定因素。 下圖顯示了作為最終備份大小的函式所花費的時間。

![chlimage_1-82](assets/chlimage_1-82.png)

此圖表說明增量備份和完整備份都遵循一個簡單的大小與時間模式，Adobe可以將此模式作為吞吐量來度量。 空閒實例上的備份時間相當一致，平均每秒0.61 MB，而不考慮基準環境上的完整或增量備份。

#### 備份延遲 {#backup-delay}

提供備份延遲參數以限制備份可能干擾生產工作負載的程度。 該參數指定一個等待時間（以毫秒為單位），該時間以逐個檔案的方式分散到備份操作中。 總體效果部分取決於受影響檔案的大小。 以MB/秒為單位測量備份效能為比較延遲對備份的影響提供了一種合理的方法。

* 與常規應用程式負載同時運行備份會對常規負載的吞吐量產生負面影響。
* 影響可能很小（只有5%）或很大，導致吞吐量下降75%。 這可能最取決於應用。
* 備份在CPU上不是負載很重，因此與I/O密集型工作負載相比，CPU密集型生產工作負載受備份影響較小。

![chlimage_1-83](assets/chlimage_1-83.png)

為了進行比較，使用檔案系統備份(「tar」)備份同一儲存庫檔案而獲得的吞吐量。 tar的效能相當，但稍高於延遲設定為零的備份。 即使設定一個小的延遲也會大大降低備份吞吐量，而預設延遲10毫秒將導致吞吐量大幅降低。 如果備份可能在應用程式總體使用率較低或應用程式可能空閒時進行，請將延遲降低到預設值以下，以允許備份更快地進行。

持續備份的應用程式吞吐量的實際影響確實取決於應用程式和基礎架構的詳細資訊。 延遲值的選擇應通過應用程式的經驗分析進行，但應盡可能小地選擇，以便備份能夠盡快完成。 由於選擇延遲值與對應用程式吞吐量的影響之間只存在微弱的關聯，因此選擇延遲應有利於縮短總體備份時間，以將備份的總體影響降至最低。 一個備份需要8個小時才能完成，但吞吐量影響為–20% ，其總體影響可能比一個備份要花費2個小時才能完成但吞吐量影響為–30%的備份大。

### 引用 {#references}

* [管理 — 備份和還原](/help/sites-administering/backup-and-restore.md)
* [管理 — 容量和卷](/help/managing/best-practices-further-reference.md#capacity-and-volume)
