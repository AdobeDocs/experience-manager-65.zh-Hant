---
title: 大量移轉資產
description: 說明如何將資產帶入 [!DNL Adobe Experience Manager]、套用中繼資料、產生轉譯，並將它們啟動至發佈例項。
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 8%

---

# 如何大量移轉資產 {#assets-migration-guide}

將資產移轉至 [!DNL Adobe Experience Manager]，需考慮幾個步驟。 從目前主目錄中擷取資產和中繼資料並不在本檔案的範圍，因為不同實施之間差異極大，但本檔案將說明如何將這些資產帶入 [!DNL Experience Manager]、套用其中繼資料、產生轉譯，並將它們啟動至發佈例項。

## 先決條件 {#prerequisites}

在實際執行此方法中的任何步驟之前，請先檢閱並實作中的指引 [資產效能調校秘訣](performance-tuning-guidelines.md). 許多步驟（例如設定並行作業的最大值）可大幅提升伺服器在負載下的穩定性和效能。 在系統載入資產後，其他步驟（例如設定檔案資料存放區）則要困難得多。

>[!NOTE]
>
>下列資產移轉工具不屬於 [!DNL Experience Manager] Adobe不支援和：
>
>* ACS AEM Tools Tag Maker
>* ACS AEM工具CSV資產匯入工具
>* ACS Commons大量工作流程管理員
>* ACS Commons快速動作管理員
>* 綜合工作流程
>
>本軟體為開放原始碼， [Apache v2授權涵蓋此軟體](https://adobe-consulting-services.github.io/pages/license.html)。若要提出問題或報告問題，請造訪ACS AEM工具和 [ACS AEM公域的GitHub](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)[問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)。

## 移轉至 [!DNL Experience Manager] {#migrating-to-aem}

將資產移轉至 [!DNL Experience Manager] 需要數個步驟，應視為分階段程式。 移轉的階段如下：

1. 停用工作流程。
1. 載入標籤。
1. 擷取資產。
1. 處理轉譯。
1. 啟用資產。
1. 啟用工作流程。

![chlimage_1-223](assets/chlimage_1-223.png)

### 停用工作流程 {#disabling-workflows}

在開始移轉之前，請針對以下專案停用您的啟動器： [!UICONTROL DAM更新資產] 工作流程。 最好將所有資產擷取到系統中，然後批次執行工作流程。 如果您已在移轉過程中上線，您可以將這些活動排程為在非工作時間執行。

### 載入標籤 {#loading-tags}

您可能已有要套用至影像的標籤分類法。 同時使用CSV Asset Importer和 [!DNL Experience Manager] 對中繼資料設定檔的支援可自動執行將標籤套用至資產的程式，標籤必須載入系統中。 此 [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 功能可讓您使用載入至系統的Microsoft Excel試算表填入標籤。

### 擷取資產 {#ingesting-assets}

將資產擷取至系統時，效能和穩定性是重要考量。 由於您要將大量資料載入系統，因此您想要確保系統執行良好，將所需的時間減至最少，並避免系統超載，這可能會導致系統當機，尤其是在已經投入生產的系統中。

將資產載入系統有兩種方法：使用HTTP的推播式方法，或使用JCR API的拉取式方法。

#### 透過HTTP傳送 {#pushing-through-http}

Adobe的Managed Services團隊會使用名為Glutton的工具，將資料載入客戶環境。 Glutton是一種小型Java應用程式，可將一個目錄中的所有資產載入到上的另一個目錄中。 [!DNL Experience Manager] 部署。 您也可以使用Perl指令碼等工具，將資產發佈至存放庫，而不使用Glutton。

使用推送https的方法有兩個主要缺點：

1. 資產必須透過HTTP傳輸至伺服器。 這需要不少的額外負荷，而且相當耗時，因此會延長執行移轉所需的時間。
1. 如果您必須將標籤和自訂中繼資料套用至資產，此方法需要執行第二個自訂程式，才能在資產匯入後將此中繼資料套用至資產。

擷取資產的另一種方法是從本機檔案系統提取資產。 不過，如果您無法將外部磁碟機或網路共用掛接至伺服器，無法執行提取式方法，則最好透過HTTP張貼資產。

#### 從本機檔案系統擷取 {#pulling-from-the-local-filesystem}

此 [ACS AEM工具CSV資產匯入工具](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) 從檔案系統提取資產，並從CSV檔案提取資產中繼資料，以匯入資產。 Experience Manager Asset Manager API可將資產匯入系統，並套用已設定的中繼資料屬性。 理想情況下，資產會透過網路檔案掛載或外部磁碟機掛載在伺服器上。

由於資產不需要透過網路傳輸，因此整體效能會大幅提升，而且此方法通常被認為是將資產載入存放庫的最有效率方式。 此外，由於工具支援中繼資料擷取，因此您可以在單一步驟中匯入所有資產和中繼資料，而非同時建立第二個步驟，透過個別工具套用中繼資料。

### 處理轉譯 {#processing-renditions}

將資產載入系統後，您需要透過以下方式處理資產： [!UICONTROL DAM更新資產] 工作流程來擷取中繼資料並產生轉譯。 在執行此步驟之前，您需要複製並修改 [!UICONTROL DAM更新資產] 工作流程以符合您的需求。 現成的工作流程包含許多您可能不需要的步驟，例如Dynamic Media PTIFF產生或 [!DNL InDesign Server] 整合。

根據您的需求設定工作流程後，您有兩個選項可執行它：

1. 最簡單的方法是 [ACS Commons的大量工作流程管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). 此工具可讓您執行查詢，並透過工作流程處理查詢的結果。 也有設定批次大小的選項。
1. 您可搭配「合成工 [作流程」使用ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)[](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。雖然此方法的參與度更高，但可讓您移除 [!DNL Experience Manager] 工作流程引擎，同時最佳化伺服器資源的使用。 此外，Fast Action Manager還通過動態監控伺服器資源並調節系統上的負載，進一步提高了效能。ACS Commons功能頁上提供了示例指令碼。

### 啟用資產 {#activating-assets}

若為具有發佈階層的部署，您需要將資產啟動至發佈伺服器陣列。 雖然Adobe建議執行多個發佈執行個體，但最有效率的方式是將所有資產復寫至單一發佈執行個體，然後複製該執行個體。 啟用大量資產時，觸發樹狀結構啟用後，您可能需要介入。 原因如下：觸發啟用時，專案會新增至Sling工作/事件佇列。 此佇列的大小開始超過約40,000個專案後，處理速度就會大幅放緩。 當此佇列的大小超過100,000個專案後，系統穩定性就會開始受到影響。

若要解決此問題，您可以使用 [快速動作管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 以管理資產復寫。 這可在不使用Sling佇列的情況下運作，可降低額外負荷，同時限制工作負荷以防止伺服器超載。 使用FAM管理復寫的範例會顯示在該功能的檔案頁面上。

將資產傳送至發佈農場的其他選項包括使 [用vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html)[或oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，這些工具是Jackrabbit的一部份。另一個選項是針對使用開放原始碼工具 [!DNL Experience Manager] 已呼叫基礎結構 [Grabbit](https://github.com/TWCable/grabbit)，聲稱其效能比vlt快。

對於這些方法中的任一方法，請注意製作例項上的資產未顯示為已啟動。 若要以正確的啟用狀態處理標幟這些資產的問題，您也需要執行指令碼以將資產標示為已啟用。

>[!NOTE]
>
>Adobe不維護或不支援Grabbit。

### 原地複製發佈 {#cloning-publish}

資產啟動後，您可以複製發佈執行個體，以建立部署所需數量的復本。 複製伺服器相當簡單明瞭，但有一些重要的步驟需要記住。 若要複製發佈：

1. 備份來源執行個體和資料存放區。
1. 將執行個體和資料存放區的備份還原至目標位置。 下列步驟均參照此新執行個體。
1. 在下執行檔案系統搜尋 `crx-quickstart/launchpad/felix` 的 `sling.id`. 刪除此檔案。
1. 在資料存放區的根路徑下，找到並刪除任何 `repository-XXX` 檔案。
1. 編輯 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 和 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 指向新環境中資料存放區的位置。
1. 啟動環境。
1. 更新作者上任何復寫代理程式的設定，以指向新執行個體上的正確發佈執行個體或Dispatcher Flush代理程式，以指向新環境的正確Dispatcher。

### 啟用工作流程 {#enabling-workflows}

完成移轉後， [!UICONTROL DAM更新資產] 應重新啟用工作流程，以支援轉譯產生和中繼資料擷取，以供日常系統使用。

## 移轉位置 [!DNL Experience Manager] 部署 {#migrating-between-aem-instances}

雖然這幾乎不常見，但有時您需要從移轉大量資料 [!DNL Experience Manager] 部署至其他位置；例如，當您執行 [!DNL Experience Manager] 升級、升級您的硬體，或移轉至新的資料中心，例如AMS移轉。

在此情況下，您的資產已填入中繼資料，且已產生轉譯。 您只需專注於將資產從一個例項移至另一個例項即可。 當移轉介於 [!DNL Experience Manager] 部署，請執行以下步驟：

1. 停用工作流程：由於您要將轉譯與我們的資產一起移轉，因此您想要為停用工作流程啟動器 [!UICONTROL DAM更新資產] 工作流程。

1. 移轉標籤：因為來源中已載入標籤 [!DNL Experience Manager] 部署，您可以在內容套件中建置這些套件，並將套件安裝在target執行個體上。

1. 移轉資產：建議使用兩種工具將資產從一種移出 [!DNL Experience Manager] 部署到另一個：

   * **儲存庫遠端複製** 或vlt rcp，可讓您在網路上使用vlt。 您可以指定來源和目的地目錄，vlt會從某個執行個體下載所有存放庫資料，並將其載入另一個執行個體。 Vlt rcp記錄於 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** 是由Time Warner Cable所開發的開放原始碼內容同步化工具， [!DNL Experience Manager] 實作。 由於它使用連續資料流，因此與vlt rcp相比，它的延遲較低，而且速度比vlt rcp快2到10倍。 Grabbit也僅支援差異內容的同步處理，可在初始移轉階段完成後同步處理變更。

1. 啟動資產：遵循的指示 [啟用資產](#activating-assets) 已記錄初始移轉至 [!DNL Experience Manager].

1. 複製發佈：就像執行新的移轉作業一樣，載入單一發佈執行個體並加以複製會比在兩個節點上啟動內容更有效率。 另請參閱 [正在複製發佈。](#cloning-publish)

1. 啟用工作流程：完成移轉後，請重新啟用以下專案的啟動器： [!UICONTROL DAM更新資產] 此工作流程可支援產生轉譯及擷取中繼資料，以供日常系統使用。
