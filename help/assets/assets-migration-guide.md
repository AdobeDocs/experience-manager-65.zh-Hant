---
title: 將資產大量移轉至Adobe Experience Manager Assets
description: 說明如何將資產匯入AEM、套用中繼資料、產生轉譯，以及啟用資產以發佈例項。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 如何大量移轉資產 {#assets-migration-guide}

將資產移轉至AEM時，需考慮數個步驟。 從目前的首頁擷取資產和中繼資料並不在本檔案的範圍內，因為這些資產在實施之間差異很大，但本檔案說明如何將這些資產匯入AEM、套用其中繼資料、產生轉譯，以及啟用它們以發佈例項。

## 必備條件 {#prerequisites}

在實際執行此方法中的任何步驟之前，請先檢閱並實作 [Assets效能調整提示中的指引](performance-tuning-guidelines.md)。 許多步驟（例如設定最大併發作業）都可大幅提升伺服器在負載下的穩定性與效能。 在系統載入資產後，其他步驟（如配置檔案資料儲存）的執行難度要大得多。

>[!NOTE]
>
>下列資產移轉工具不屬於AEM,Adobe不支援：
>
>* ACS AEM Tools Tag Maker
>* ACS AEM工具CSV資產匯入工具
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* 合成工作流程
>
>
本軟體為開放原始碼， [Apache v2授權涵蓋此軟體](https://adobe-consulting-services.github.io/pages/license.html)。 若要提出問題或報告問題，請造訪ACS AEM工具和 [ACS AEM公域的GitHub](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)[問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 移轉至AEM {#migrating-to-aem}

將資產移轉至AEM需要幾個步驟，且應視為分階段程式。 遷移的階段如下：

1. 停用工作流程。
1. 載入標籤。
1. 收錄資產。
1. 處理轉譯。
1. 啟動資產。
1. 啟用工作流程。

![chlimage_1-223](assets/chlimage_1-223.png)

### 停用工作流程 {#disabling-workflows}

開始移轉之前，請停用DAM更新資產工作流程的啟動器。 最好將所有資產收錄至系統，然後以批次執行工作流程。 如果您在移轉進行時已上線，您可以排程這些活動在下班時間執行。

### 載入標籤 {#loading-tags}

您可能已經有了要套用至影像的標籤分類法。 雖然CSV Asset Importer和AEM對中繼資料描述檔的支援可自動將標籤套用至資產的程式，但是標籤必須載入系統中。 ACS [AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) （ACS AEM工具標籤製作器）功能可讓您使用載入系統的Microsoft excel試算表填入標籤。

### 收錄資產 {#ingesting-assets}

在將資產放入系統時，效能與穩定性是重要的考量。 由於您要將大量資料載入系統，因此您需要確保系統能盡可能地執行，以盡量減少所需的時間，並避免系統超載，這可能會導致系統崩潰，尤其是在已在生產中的系統中。

將資產載入系統有兩種方法：使用HTTP的推播方式或使用JCR API的推播方式。

#### 透過HTTP傳送 {#pushing-through-http}

Adobe的「受管理服務」團隊使用名為Glutton的工具，將資料載入客戶環境。 Glutton是小型Java應用程式，可從一個目錄將所有資產載入AEM例項上的另一個目錄。 您也可以使用諸如Perl指令碼之類的工具將資產發佈到儲存庫中，而不是Glutton。

使用推送https的方法有兩個主要的缺點：

1. 資產需要透過HTTP傳輸至伺服器。 這需要相當多的開銷，而且非常耗時，因而延長了執行遷移所需的時間。
1. 如果您有必須套用至資產的標籤和自訂中繼資料，此方法需要執行第二個自訂程式，以便在匯入資產後，將此中繼資料套用至資產。

接收資產的另一種方法是從本地檔案系統提取資產。 不過，如果您無法將外部磁碟機或網路共用載入伺服器，以執行以拉式為基礎的方式，則最好透過HTTP張貼資產。

#### 從本地檔案系統中讀取 {#pulling-from-the-local-filesystem}

[ACS AEM Tools CSV Asset Importer](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) ，會從CSV檔案中為資產匯入提取檔案系統的資產和資產中繼資料。 AEM Asset Manager API可用來將資產匯入系統並套用已設定的中繼資料屬性。 理想情況下，資產會透過網路檔案載入或透過外部磁碟機載入伺服器。

由於資產不需要透過網路傳輸，因此整體效能大幅提升，而且通常認為此方法是將資產載入儲存庫的最有效方式。 此外，由於此工具支援中繼資料擷取，因此您可以在單一步驟中匯入所有資產和中繼資料，而不是建立第二個步驟，以透過個別工具套用中繼資料。

### 處理轉譯 {#processing-renditions}

將資產載入系統後，您需要透過DAM更新資產工作流程來處理這些資產，以擷取中繼資料並產生轉譯。 在執行此步驟之前，您需要複製並修改DAM更新資產工作流程，以符合您的需求。 現成可用的工作流程包含許多您不需要的步驟，例如產生Scene7 PTIFF或整合InDesign伺服器。

根據您的需求設定工作流程後，您有兩個執行工作流程的選項：

1. 最簡單的方法是 [ACS Commons的Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)。 此工具允許您執行查詢，並通過工作流處理查詢結果。 還有設定批次大小的選項。
1. 您可搭配「合成工 [作流程」使用ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)[](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。 雖然此方法的參與度更高，但可讓您移除AEM工作流程引擎的額外負荷，同時最佳化伺服器資源的使用。 此外，Fast Action Manager還通過動態監控伺服器資源並調節系統上的負載，進一步提高了效能。 ACS Commons功能頁上提供了示例指令碼。

### 啟動資產 {#activating-assets}

對於具有發佈層的部署，您需要將資產啟動至發佈群。 雖然Adobe建議執行多個單一發佈例項，但將所有資產複製至單一發佈例項，然後複製該例項最有效率。 在啟動大量資產時，在觸發樹狀結構啟動後，您可能需要進行干預。 原因如下：當觸發啟動時，項目會新增至Sling工作／事件佇列。 當此佇列的大小開始超過約40,000個項目後，處理速度大幅降低。 當此隊列的大小超過100,000個項目後，系統穩定性就會開始受到影響。

要解決此問題，您可以使用 [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 來管理資產複製。 這樣不需使用Sling佇列，降低開銷，同時可調節工作負載，以防止伺服器過載。 使用FAM管理複製的範例顯示在功能的檔案頁面上。

將資產傳送至發佈農場的其他選項包括使 [用vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html)[或oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，這些工具是Jackrabbit的一部份。 另一個選擇是針對您的AEM基礎架構使用開放來源工具，稱為 [Grabbit](https://github.com/TWCable/grabbit)，該工具聲稱其效能比vlt快。

對於上述任何方法，但須注意的是，作者實例上的資產並未顯示為已啟動。 若要處理以正確啟動狀態來標籤這些資產，您還需要執行指令碼，將資產標示為已啟動。

>[!NOTE]
>
>Adobe不維護或支援Grabbit。

### 仿製發佈 {#cloning-publish}

在啟動資產後，您可以複製您的發佈例項，以建立部署所需的份數。 克隆伺服器相當簡單，但需要記住一些重要步驟。 若要複製發佈：

1. 備份源實例和資料儲存。
1. 將實例和資料儲存的備份還原到目標位置。 以下步驟均參考此新實例。
1. 在中執行檔案系統 `crx-quickstart/launchpad/felix` 搜索 `sling.id`。 刪除此檔案。
1. 在資料儲存的根路徑下，找到並刪除任何 `repository-XXX` 檔案。
1. 編 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 輯 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 並指向新環境中資料儲存的位置。
1. 啟動環境。
1. 更新作者上任何複製代理的配置，以指向新實例上正確的發佈實例或調度器刷新代理，以指向新環境的正確調度程式。

### 啟用工作流程 {#enabling-workflows}

完成移轉後，應重新啟用DAM更新資產工作流程的啟動器，以支援轉譯產生和中繼資料擷取，以持續使用日常系統。

## 跨AEM部署移轉 {#migrating-between-aem-instances}

雖然不是這麼常見，但有時您需要將大量資料從一個AEM例項移轉至另一個例項；例如，當您執行AEM升級、升級硬體或移轉至新的資料中心時，例如AMS移轉。

在這種情況下，您的資產已填入中繼資料，且已產生轉譯。 您只需專注於將資產從一個實例移至另一個實例。 在AEM例項之間移轉時，請執行下列步驟：

1. 停用工作流程：由於您要移轉轉譯以及我們的資產，所以您想要停用DAM更新資產的工作流程啟動器。

1. 移轉標籤：由於您已在來源AEM例項中載入標籤，因此您可以在內容套件中建立標籤，並在目標例項上安裝套件。

1. 移轉資產：建議使用兩種工具，將資產從一個AEM例項移至另一個：

   * **Vault Remote Copy** 或vlt rcp，允許您跨網路使用vlt。 您可以指定源目錄和目標目錄，並從一個實例下載所有儲存庫資料並將其載入到另一個實例。 Vlt rcp在 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** 是Time Warner Cable為其AEM實作而開發的開放原始碼內容同步工具。 由於它使用連續的資料流，與vlt rcp相比，它的延遲更低，並聲稱速度比vlt rcp快2到10倍。 Grabbit也僅支援Delta內容的同步，這可讓Grabbit在初始移轉通過完成後同步變更。

1. 啟動資產：請依照說明來啟 [動針對初始](#activating-assets) AEM移轉所記錄的資產。

1. 仿製發佈：和新移轉一樣，載入單一發佈執行個體並進行仿製比在兩個節點上啟動內容更有效率。 請參閱 [仿製發佈。](#cloning-publish)

1. 啟用工作流程：完成移轉後，請重新啟用DAM更新資產工作流程的啟動器，以支援產生轉譯和中繼資料擷取，以持續使用日常系統。
