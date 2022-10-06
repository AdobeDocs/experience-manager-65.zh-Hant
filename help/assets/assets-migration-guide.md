---
title: 大量移轉資產
description: 說明如何將資產帶入 [!DNL Adobe Experience Manager]、套用中繼資料、產生轉譯，以及啟用它們以發佈例項。
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 8%

---

# 如何大量移轉資產 {#assets-migration-guide}

將資產移轉至 [!DNL Adobe Experience Manager]，請考慮幾個步驟。 從其當前主目錄中提取資產和元資料不屬於本文檔的範圍，因為它在實施之間差異很大，但本文檔介紹如何將這些資產帶入 [!DNL Experience Manager]、套用其中繼資料、產生轉譯，以及啟用它們以發佈執行個體。

## 必備條件 {#prerequisites}

在實際執行此方法中的任何步驟之前，請先檢閱並實作 [資產效能調整秘訣](performance-tuning-guidelines.md). 許多步驟（如配置最大併發作業）都極大地提高了伺服器在負載下的穩定性和效能。 在系統載入資產後，其他步驟（例如設定檔案資料存放區）則難度更大。

>[!NOTE]
>
>下列資產移轉工具不屬於 [!DNL Experience Manager] 和不受Adobe支援：
>
>* ACS AEM Tools Tag Maker
>* ACS AEM工具CSV資產匯入工具
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* 合成工作流程
>
>本軟體為開放原始碼， [Apache v2授權涵蓋此軟體](https://adobe-consulting-services.github.io/pages/license.html)。若要提出問題或報告問題，請造訪ACS AEM工具和 [ACS AEM公域的GitHub](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)[問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 移轉至 [!DNL Experience Manager] {#migrating-to-aem}

將資產移轉至 [!DNL Experience Manager] 需要數個步驟，並應視為分階段程式。 移轉階段如下：

1. 停用工作流程。
1. 載入標籤。
1. 擷取資產。
1. 處理轉譯。
1. 啟動資產。
1. 啟用工作流程。

![chlimage_1-223](assets/chlimage_1-223.png)

### 停用工作流程 {#disabling-workflows}

開始移轉前，請停用 [!UICONTROL DAM更新資產] 工作流程。 最好將所有資產內嵌至系統，然後以批次執行工作流程。 如果您在移轉進行時已上線，您可以排程這些活動在非工作時間執行。

### 載入標籤 {#loading-tags}

您可能已準備好將標籤分類套用至影像。 而CSV資產匯入工具和 [!DNL Experience Manager] 支援中繼資料設定檔可自動將標籤套用至資產的程式，這些標籤需要載入到系統中。 此 [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 功能可讓您使用載入至系統的Microsoft Excel試算表填入標籤。

### 內嵌資產 {#ingesting-assets}

將資產擷取至系統中時，效能和穩定性是重要考量。 由於您要將大量資料載入到系統中，因此，您希望確保系統能盡其所能地運行，以最大限度地減少所需時間，並避免系統超載，這可能導致系統崩潰，特別是在已在生產的系統中。

將資產載入系統有兩種方法：使用HTTP的推送式方法，或使用JCR API的提取式方法。

#### 透過HTTP傳送 {#pushing-through-http}

Adobe的Managed Services團隊使用名為Glutton的工具，將資料載入客戶環境中。 Glutton是小型Java應用程式，會將所有資產從一個目錄載入至 [!DNL Experience Manager] 部署。 您也可以使用工具（例如Perl指令碼）將資產張貼至存放庫，而不是使用Glutton。

使用透過https推送的方式有兩個主要缺點：

1. 資產需透過HTTP傳輸至伺服器。 這需要相當多的開銷，而且非常耗時，因而延長了執行遷移所花費的時間。
1. 如果您有必須套用至資產的標籤和自訂中繼資料，此方法需要執行第二個自訂程式，才能在匯入資產後將此中繼資料套用至資產。

擷取資產的另一種方法是從本機檔案系統提取資產。 不過，如果您無法將外部硬碟或網路共用裝載至伺服器以執行提取式方法，則透過HTTP張貼資產是最佳選項。

#### 從本地檔案系統獲取 {#pulling-from-the-local-filesystem}

此 [ACS AEM工具CSV資產匯入工具](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) 從檔案系統提取資產，並從CSV檔案提取資產中繼資料以匯入資產。 Experience Manager資產管理器API可用來將資產匯入系統，並套用已設定的中繼資料屬性。 理想情況下，資產會透過網路檔案裝載或外部驅動器裝載在伺服器上。

由於資產不需要透過網路傳輸，因此整體效能大幅改善，且通常認為此方法是將資產載入存放庫的最有效方式。 此外，由於工具支援中繼資料擷取，因此您可以在單一步驟中匯入所有資產和中繼資料，而非也可以建立第二個步驟，透過個別工具套用中繼資料。

### 處理轉譯 {#processing-renditions}

將資產載入系統後，您需透過 [!UICONTROL DAM更新資產] 擷取中繼資料和產生轉譯的工作流程。 執行此步驟之前，您需要複製並修改 [!UICONTROL DAM更新資產] 符合您需求的工作流程。 現成可用的工作流程包含許多您可能不需要的步驟，例如產生Dynamic Media PTIFF或 [!DNL InDesign Server] 整合。

根據您的需求設定工作流程後，您有兩個選項可執行工作流程：

1. 最簡單的方法是 [ACS Commons的Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). 此工具允許您執行查詢，並通過工作流處理查詢結果。 還有設定批大小的選項。
1. 您可搭配「合成工 [作流程」使用ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)[](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。雖然此方法的參與度更高，但可讓您移除 [!DNL Experience Manager] 工作流程引擎，同時最佳化伺服器資源的使用。 此外，Fast Action Manager還通過動態監控伺服器資源並調節系統上的負載，進一步提高了效能。ACS Commons功能頁上提供了示例指令碼。

### 啟動資產 {#activating-assets}

若是具有發佈層級的部署，您需要將資產啟動至發佈伺服器陣列。 雖然Adobe建議執行多個單一發佈例項，但將所有資產複製到單一發佈例項，然後複製該例項最為有效。 在啟動大量資產時，觸發樹狀結構啟動後，您可能需要進行干預。 原因如下：觸發啟動時，項目會新增至Sling作業/事件佇列。 此佇列的大小開始超過約40,000個項目後，處理速度大幅放緩。 當此隊列的大小超過100,000個項後，系統穩定性就會開始受到影響。

若要解決此問題，您可以使用 [快速操作管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 管理資產復寫。 這樣就不需要使用Sling佇列，降低開銷，同時限制工作負載以防止伺服器過載。 功能的檔案頁面上顯示了使用FAM管理復寫的範例。

將資產傳送至發佈農場的其他選項包括使 [用vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html)[或oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，這些工具是Jackrabbit的一部份。另一個選項是使用開放來源工具 [!DNL Experience Manager] 基礎設施 [格拉比特](https://github.com/TWCable/grabbit)，其效能比vlt快。

對於其中任何方法，請注意製作例項上的資產未顯示為已啟動。 若要處理以正確啟動狀態標籤這些資產，您也需執行指令碼，將資產標示為已啟動。

>[!NOTE]
>
>Adobe不維護或支援Grabbit。

### 原地複製發佈 {#cloning-publish}

啟動資產後，您可以複製發佈執行個體，以建立部署所需的所有復本。 克隆伺服器相當簡單，但有一些重要步驟需要記住。 若要原地複製發佈：

1. 備份源實例和資料儲存。
1. 將實例和資料儲存的備份還原到目標位置。 下列步驟皆參考此新例項。
1. 在下執行檔案系統搜索 `crx-quickstart/launchpad/felix` for `sling.id`. 刪除此檔案。
1. 在資料存放區的根路徑下，找到並刪除任何 `repository-XXX` 檔案。
1. 編輯 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 和 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 指向新環境中資料儲存庫的位置。
1. 啟動環境。
1. 更新作者上任何復寫代理的設定，以指向新執行個體上正確的發佈執行個體或調度程式排清代理，以指向新環境的正確調度程式。

### 啟用工作流程 {#enabling-workflows}

完成遷移後， [!UICONTROL DAM更新資產] 應重新啟用工作流程，以支援產生轉譯和擷取中繼資料，以持續使用日常系統。

## 跨 [!DNL Experience Manager] 部署 {#migrating-between-aem-instances}

雖然並不常見，但有時您需要從一個 [!DNL Experience Manager] 部署到另一個；例如，當您執行 [!DNL Experience Manager] 升級、升級硬體或遷移到新的資料中心，例如通過AMS遷移。

在此情況下，資產已填入中繼資料，且已產生轉譯。 您只需專注於將資產從一個執行個體移至另一個執行個體。 在 [!DNL Experience Manager] 部署時，請執行以下步驟：

1. 停用工作流程：由於您要移轉轉譯以及我們的資產，因此您想要停用 [!UICONTROL DAM更新資產] 工作流程。

1. 移轉標籤：因為您已在來源中載入標籤 [!DNL Experience Manager] 部署時，您可以在內容套件中建置這些元件，並在target執行個體上安裝套件。

1. 移轉資產：建議您使用兩種工具，將資產從一個 [!DNL Experience Manager] 部署到另一個：

   * **保管庫遠程副本** 或vlt rcp，可讓您跨網路使用vlt。 您可以指定源目錄和目標目錄，然後vlt從一個實例下載所有儲存庫資料並將其載入到另一個實例。 Vlt rcp記錄於 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **格拉比特** 是時代華納有線為其開發的開放原始碼內容同步工具 [!DNL Experience Manager] 實作。 因為它使用連續的資料流，與vlt rcp相比，它的延遲更低，並聲稱速度比vlt rcp快2到10倍。 Grabbit也僅支援增量內容的同步，這可讓其在完成初始遷移過程後同步更改。

1. 啟動資產：遵循 [啟用資產](#activating-assets) 已記錄，可初次移轉至 [!DNL Experience Manager].

1. 原地複製發佈：和新移轉一樣，載入單一發佈執行個體並複製執行個體比在兩個節點上啟動內容更有效率。 請參閱 [複製發佈。](#cloning-publish)

1. 啟用工作流：完成遷移後，重新啟用 [!UICONTROL DAM更新資產] 支援產生轉譯和擷取中繼資料的工作流程，以持續使用日常系統。
