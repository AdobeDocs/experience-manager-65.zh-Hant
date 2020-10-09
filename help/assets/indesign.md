---
title: 整 [!DNL Assets] 合 [!DNL InDesign Server]
description: 瞭解如何 [!DNL Adobe Experience Manager Assets] 整合 [!DNL Adobe InDesign Server]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 3%

---


# 與 [!DNL Adobe Experience Manager Assets] [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 用途：

* 一個代理，用於分配特定處理任務的負載。 代理是與代理工 [!DNL Experience Manager] 作者通信以完成特定任務的實例，而其他實例 [!DNL Experience Manager] 則用於傳遞結果。
* 用於定義和管理特定任務的代理工作器。
這些工作可以涵蓋各種任務；例如，使用 [!DNL InDesign Server] 處理檔案。

若要完全上傳您 [!DNL Experience Manager Assets] 使用Proxy建立 [!DNL Adobe InDesign] 的檔案。 這會使用代理工作器與通信， [!DNL Adobe InDesign Server]在此處 [運行指令碼](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) ，以提取元資料並生成各種格式副本 [!DNL Experience Manager Assets]。 代理工作器可啟用雲配置中實例與實 [!DNL InDesign Server] 例之 [!DNL Experience Manager] 間的雙向通信。

>[!NOTE]
>
>[!DNL Adobe InDesign] 提供兩種不同的方案。 [Adobe InDesign案頭應用程式](https://www.adobe.com/products/indesign.html) ，用於設計用於印刷和數位散發的頁面版面。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 可讓您根據所建立的檔案，以程式設計方式建立自動化檔案 [!DNL InDesign]。 它以服務的形式運行，為其 [ExtendScript](https://www.adobe.com/devnet/scripting.html) 引擎提供介面。指令碼的編寫 [!DNL ExtendScript]方式與類似 [!DNL JavaScript]。 有關指令碼的 [!DNL InDesign] 資訊，請 [參見https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 擷取的運作方式 {#how-the-extraction-works}

可 [!DNL Adobe InDesign Server] 以與之整合， [!DNL Experience Manager Assets] 以便上傳以下方式建立的INDD檔案、產生 [!DNL InDesign] 轉譯、提取所有媒體（例如視訊）並儲存為資產：

>[!NOTE]
>
>舊版可 [!DNL Experience Manager] 以擷取XMP和縮圖，現在所有媒體都可擷取。

1. 將INDD檔案上傳至 [!DNL Experience Manager Assets]。
1. 框架通過SOAP(簡單對象訪問協 [!DNL InDesign Server] 議)將命令指令碼發送到。
此命令指令碼將：

   * 檢索INDD檔案。
   * 執行 [!DNL InDesign Server] 命令：

      * 會擷取結構、文字和任何媒體檔案。
      * 產生PDF和JPG轉譯。
      * 產生HTML和IDML轉譯。
   * 將產生的檔案張貼回 [!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是以XML為基礎的格式，可轉譯檔案的所有 [!DNL InDesign] 內容。 它會使用 [ZIP壓縮儲存為壓縮的](https://www.techterms.com/definition/zip) 套件。 如需詳細資訊，請 [參閱InDesign Interchange Formats INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果 [!DNL InDesign Server] 未安裝或未配置，則仍可將INDD檔案上載到 [!DNL Experience Manager]。 但產生的轉譯將限制為PNG和JPEG。 您將無法產生HTML、.idml或頁面轉譯。

1. 擷取和轉譯產生後：

   * 此結構會複製到( `cq:Page` 類型的轉譯)。
   * 提取的文本和檔案儲存在中 [!DNL Experience Manager Assets]。
   * 所有轉譯都儲存在 [!DNL Experience Manager Assets]資產本身中。

## 與Experience [!DNL InDesign Server] Manager整合 {#integrating-the-indesign-server-with-aem}

若要整合 [!DNL InDesign Server] 以便與 [!DNL Experience Manager Assets] 設定Proxy搭配使用，您必須：

1. [安裝InDesign Server](#installing-the-indesign-server)。
1. 如有需要， [請設定Experience Manager資產工作流程](#configuring-the-aem-assets-workflow)。
只有當預設值不適用於您的例項時，才需要這麼做。
1. 為InDesign [Server設定代理工作器](#configuring-the-proxy-worker-for-indesign-server)。

### 安裝 [!DNL InDesign Server] {#installing-the-indesign-server}

要安裝並啟動， [!DNL InDesign Server] 以便與 [!DNL Experience Manager]:

1. 下載並安裝 [!DNL InDesign Server]。

1. 如有需要，您可以自訂例項的 [!DNL InDesign Server] 設定。

1. 從命令行啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這會在連接埠8080上以SOAP外掛程式監聽來啟動伺服器。 所有日誌消息和輸出都直接寫入命令窗口。

   >[!NOTE]
   >
   >如果要將輸出消息保存到檔案，則使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 設定工作 [!DNL Experience Manager Assets] 流程 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有預先設定的工作流程 **[!UICONTROL DAM更新資產]**，其中具有幾個流程步驟，專門用於 [!DNL InDesign]:

* [媒體提取](#media-extraction)
* [頁面提取](#page-extraction)

此工作流程會設定預設值，這些預設值可適用於您在各種作者例項上的設定(此為標準工作流程，因此在「編輯工作流程」( [Editing a Workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))下會提供更多資訊。 如果您使用預設值（包括SOAP埠），則不需要任何設定。

設定後，上傳檔 [!DNL InDesign] 案至( [!DNL Experience Manager Assets] 透過任何常用方法)會觸發工作流程來處理資產並準備各種轉譯。 將INDD檔案上傳至以測試您的設定， [!DNL Experience Manager Assets] 以確認您看到IDS在 `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

此步驟控制從INDD檔案抽取介質。

若要自訂，您可以編 **[!UICONTROL 輯]** 「媒體擷 **[!UICONTROL 取」步驟的「引]** 數」標籤。

![媒體擷取引數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體擷取引數和指令碼路徑

* **ExtendScript程式庫**:這是其他指令碼所需的簡單http get/post方法程式庫。

* **擴充指令碼**:您可以在此處指定不同的指令碼組合。 如果希望在上執行自己的指令碼， [!DNL InDesign Server]請將指令碼保存在 `/apps/settings/dam/indesign/scripts`。

如需指令碼的相 [!DNL Adobe InDesign] 關資訊，請參 [閱InDesign開發人員檔案](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>請 勿變更ExtendScript程式庫。此程式庫提供與Sling通訊所需的HTTP功能。 此設定指定要發送到的庫以 [!DNL InDesign Server] 便在其中使用。

「媒 `ThumbnailExport.jsx` 體擷取」工作流程步驟執行的指令碼會產生JPG格式的縮圖轉譯。 「處理縮圖」工作流程步驟會使用此格式副本，以產生所需的靜態格式副本 [!DNL Experience Manager]。

您可以設定「處理縮圖」工作流程步驟，以產生不同大小的靜態轉譯。 請確定您未移除預設值，因為介面需要這些預設 [!DNL Experience Manager Assets] 值。 最後，「刪除影像預覽轉譯」工作流程步驟會移除JPG縮圖轉譯，因為不再需要它。

#### Page extraction {#page-extraction}

這會從擷 [!DNL Experience Manager] 取的元素建立頁面。 擷取處理常式可用來從轉譯（目前為HTML或IDML）擷取資料。 然後，此資料會用於使用PageBuilder建立頁面。

若要自訂，您可以編輯「頁 **[!UICONTROL 面擷取]** 」步驟 **[!UICONTROL 的「引]** 數」標籤。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面擷取處理常式**:從彈出式清單中，選取您要使用的處理常式。 擷取處理常式會針對由相關人員選擇的特定轉譯 `RenditionPicker` 進行操作(請參 `ExtractionHandler` 閱API)。
In a standard [!DNL Experience Manager] installation the following is available:
   * IDML Export Extraction句柄：對在「媒體擷 `IDML` 取」步驟中產生的轉譯進行操作。

* **頁面名稱**:指定您要指派給產生頁面的名稱。 若保留空白，則名稱為「page」（若「page」已存在，則為衍生值）。

* **頁面標題**:指定您要指派給產生頁面的標題。

* **頁面根路徑**:結果頁面的根位置路徑。 如果保留空白，則會使用保留資產轉譯的節點。

* **頁面範本**:產生產生頁面時要使用的範本。

* **頁面設計**:產生產生頁面時要使用的頁面設計。

### 為配置代理工作器 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>該工作器駐留在代理實例上。

1. 在「工具」控制台中，展 **[!UICONTROL 開左窗格中的「雲端服務]** 」設定。 然後展開「 **[!UICONTROL 雲端代理設定」]**。

1. 連按兩下 **[!UICONTROL IDS工作器]** ，以開啟以進行設定。

1. 按一下 **[!UICONTROL 編輯]** ，開啟配置對話框並定義所需設定：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS池**&#x200B;用於與通信的SOAP端點 [!DNL InDesign Server]。 您可以新增、移除和訂購項目。

1. 按一下「確定」以儲存。

### 設定Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果 [!DNL InDesign Server] 和 [!DNL Experience Manager] 運行在不同的主機上，或者這兩個應用程式都未在預設埠上運行，請配置 [!UICONTROL Day CQ Link Externalizer] ，以設定主機名、埠和內容路徑 [!DNL InDesign Server]。

1. 在訪問Web控制台 `https://[aem_server]:[port]/system/console/configMgr`。
1. Locate the configuration **[!UICONTROL Day CQ Link Externalizer]**, and click **[!UICONTROL Edit]** to open it.
1. 指定主機名和上下文路徑，然 [!DNL Adobe InDesign Server] 後按一下 **保存**。

   ![chlimage_1-97](assets/chlimage_1-290.png)

### 啟用並行作業處理 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server-s}

您現在可以啟用IDS的並行作業處理。 確定可處理的並行作業的最`x`大數 [!DNL InDesign Server] 量():

* 在單個多處理器機器上，可處理的並行作業(`x`)的最 [!DNL InDesign Server] 大數目比運行IDS的處理器數少一個。
* 在多台電腦上運行IDS時，您需要計算可用處理器總數（即所有電腦上），然後減去電腦總數。

要配置並行IDS作業數：

1. 開啟 **[!UICONTROL Felix]** Console的「設定」標籤；例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 在下選擇IDS處理隊列 `Apache Sling Job Queue Configuration`。

1. 設定:

   * **類型** - `Parallel`
   * **最大並行作業** - `<*x*>` （如上所計算）

1. 儲存這些變更。
1. 若要啟用Adobe CS6和更新版本的多階段作業支援，請勾選設定 `enable.multisession.name` 下的核取 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 方塊。
1. 通過將SOAP [端點添加 `x` 到IDS工作器配置中，建立IDS工作器池](#configuring-the-proxy-worker-for-indesign-server)。

   如果有多台電腦在 [!DNL InDesign Server]運行，請為每個電腦添加SOAP端點（每台電腦的處理器數-1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作池時，可以啟用IDS工作池的阻止清單。
>
>若要這麼做，請啟用 **[!UICONTROL IDS作業尋回的設定下]**`com.day.cq.dam.ids.impl.IDSJobProcessor.name` 的enable.retry.name核取方塊。
>
>此外，在配 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 置下，設定參數的正值，該參數在將IDS從作業處理程式清單中 `max.errors.to.blacklist` 禁止之前確定作業檢索的數量。
>
>預設情況下，在IDS工作`retry.interval.to.whitelist.name`器經過幾分鐘的可配置()時間後重新驗證。 如果線上找到該工作器，則會將其從被阻止的清單中刪除。

## 啟用10.0或 [!DNL InDesign Server] 更新版本的支援 {#enabling-support-for-indesign-server-or-later}

對 [!DNL InDesign Server] 於10.0或更高版本，請執行下列步驟以啟用多階段作業支援。

1. 從實例中開啟配置 [!DNL Experience Manager Assets] 管理器 `https://[aem_server]:[port]/system/console/configMgr`。
1. 編輯配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. 選取「ids.cc.en **[!UICONTROL ()]** 」選項，然後按一 **[!UICONTROL 下「儲存]**」。

>[!NOTE]
>
>為 [!DNL InDesign Server] 與整 [!DNL Experience Manager Assets]合，請使用多核處理器，因為單核系統不支援整合所需的階段作業支援功能。

## 配置認 [!DNL Experience Manager] 證 {#configure-aem-credentials}

您可以變更從部署存取的預設管理員認證(使用者名 [!DNL InDesign Server] 稱和密 [!DNL Experience Manager] 碼)，而不中斷與的整合 [!DNL InDesign Server]。

1. 前往 `/etc/cloudservices/proxy.html`.
1. 在對話方塊中，指定新的使用者名稱和密碼。
1. 儲存認證。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

