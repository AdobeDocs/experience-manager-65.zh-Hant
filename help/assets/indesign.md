---
title: 整合 [!DNL Assets] with [!DNL InDesign Server]
description: 了解如何整合 [!DNL Adobe Experience Manager Assets] with [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 3%

---

# 整合 [!DNL Adobe Experience Manager Assets] with [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用：

* 分配特定處理任務的負載的代理。 代理是 [!DNL Experience Manager] 與代理工作人員通信以完成特定任務的實例，以及 [!DNL Experience Manager] 執行個體來傳送結果。
* 定義和管理特定任務的代理工作。
這可以涵蓋各種任務；例如，使用 [!DNL InDesign Server] 來處理檔案。

若要將檔案完全上傳至 [!DNL Experience Manager Assets] 您建立的 [!DNL Adobe InDesign] 已使用代理。 這會使用代理工作程式來與 [!DNL Adobe InDesign Server]，其中 [指令碼](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 執行以擷取中繼資料，並為 [!DNL Experience Manager Assets]. 代理工作器可啟用 [!DNL InDesign Server] 和 [!DNL Experience Manager] 雲端設定中的例項。

>[!NOTE]
>
>[!DNL Adobe InDesign] 提供為兩種不同的產品。 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 用於設計用於打印和數字分發的頁面佈局的案頭應用。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 使您能夠基於已使用建立的內容，以寫程式方式建立自動化文檔 [!DNL InDesign]. 它作為一種服務，為它提供介面 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.指令碼寫入 [!DNL ExtendScript]，其類似於 [!DNL JavaScript]. 如需有關 [!DNL InDesign] 指令碼請參閱 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## 提取的運作方式 {#how-the-extraction-works}

此 [!DNL Adobe InDesign Server] 可與 [!DNL Experience Manager Assets] 使INDD檔案以 [!DNL InDesign] 可以上傳、產生轉譯、擷取所有媒體（例如視訊），並儲存為資產：

>[!NOTE]
>
>舊版 [!DNL Experience Manager] 能擷取XMP和縮圖，現在可擷取所有媒體。

1. 將INDD檔案上傳至 [!DNL Experience Manager Assets].
1. 框架將命令指令碼發送到 [!DNL InDesign Server] 通過SOAP（簡單對象訪問協定）。
此命令指令碼將：

   * 檢索INDD檔案。
   * 執行 [!DNL InDesign Server] 命令：

      * 會擷取結構、文字和任何媒體檔案。
      * PDF和JPG轉譯會產生。
      * HTML和IDML轉譯會產生。
   * 將產生的檔案發佈回 [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML是以XML為基礎的格式，可轉譯 [!DNL InDesign] 檔案。 會以壓縮套件的形式儲存，使用 [ZIP](https://www.techterms.com/definition/zip) 壓縮。 如需詳細資訊，請參閱 [InDesign交換格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >若 [!DNL InDesign Server] 未安裝或未配置，則您仍可將INDD檔案上載到 [!DNL Experience Manager]. 不過，產生的轉譯將僅限於PNG和JPEG。 您將無法產生HTML、 .idml或頁面轉譯。

1. 擷取和轉譯產生後：

   * 該結構被複製到 `cq:Page` （轉譯類型）。
   * 擷取的文字和檔案會儲存在 [!DNL Experience Manager Assets].
   * 所有轉譯都儲存在 [!DNL Experience Manager Assets]，即資產本身。

## 整合 [!DNL InDesign Server] 與Experience Manager {#integrating-the-indesign-server-with-aem}

若要整合 [!DNL InDesign Server] 搭配使用 [!DNL Experience Manager Assets] 設定代理後，您需要：

1. [安裝InDesign Server](#installing-the-indesign-server).
1. 如果需要， [設定Experience Manager Assets工作流程](#configuring-the-aem-assets-workflow).
只有在預設值不適合您的例項時，才需要這個選項。
1. 設定 [代理工作InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### 安裝 [!DNL InDesign Server] {#installing-the-indesign-server}

安裝並啟動 [!DNL InDesign Server] 搭配使用 [!DNL Experience Manager]:

1. 下載並安裝 [!DNL InDesign Server].

1. 如有需要，您可以自訂 [!DNL InDesign Server] 例項。

1. 從命令行啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這會在連接埠8080上以SOAP外掛程式監聽來啟動伺服器。 所有日誌消息和輸出都直接寫入命令窗口。

   >[!NOTE]
   >
   >如果要將輸出消息保存到檔案，則使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 設定 [!DNL Experience Manager Assets] 工作流程 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有預先設定的工作流程 **[!UICONTROL DAM更新資產]**，有幾個處理步驟，具體針對 [!DNL InDesign]:

* [媒體提取](#media-extraction)
* [頁面提取](#page-extraction)

此工作流程會設定預設值，這些值可針對您在各種製作例項上的設定進行調整(這是標準工作流程，因此可在下方取得詳細資訊 [編輯工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果您使用預設值（包括SOAP埠），則無需配置。

設定後，請上傳 [!DNL InDesign] 檔案 [!DNL Experience Manager Assets] （透過任何常用方法）觸發工作流程以處理資產並準備各種轉譯。 將INDD檔案上傳至 [!DNL Experience Manager Assets] 以確認您在 `<*your_asset*>.indd/Renditions`

#### 媒體擷取 {#media-extraction}

此步驟控制從INDD檔案中提取介質。

若要自訂，您可以編 **[!UICONTROL 輯]** 「媒體擷 **[!UICONTROL 取」步驟的「引]** 數」標籤。

![媒體擷取引數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體擷取引數和指令碼路徑

* **ExtendScript資料庫**:這是其他指令碼所需的簡單http get/post方法程式庫。

* **擴充指令碼**:您可以在此處指定不同的指令碼組合。 如果您想要在 [!DNL InDesign Server]，將指令碼儲存在 `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>請 勿變更ExtendScript程式庫。此程式庫提供與Sling通訊所需的HTTP功能。 此設定會指定要傳送至的程式庫 [!DNL InDesign Server] 供使用。

此 `ThumbnailExport.jsx` 由「媒體擷取」工作流程步驟執行的指令碼會產生JPG格式的縮圖轉譯。 「處理縮圖」工作流程步驟會使用此轉譯，以產生所需的靜態轉譯 [!DNL Experience Manager].

您可以設定「處理縮圖」工作流程步驟，以產生不同大小的靜態轉譯。 請確定您不會移除預設值，因為 [!DNL Experience Manager Assets] 介面。 最後，「刪除影像預覽轉譯」工作流程步驟會移除JPG縮圖轉譯，因為這已不再需要。

#### 頁面擷取 {#page-extraction}

這會建立 [!DNL Experience Manager] 頁面。 擷取處理常式可用來從轉譯(目前為HTML或IDML)中擷取資料。 然後，系統會使用此資料建立使用PageBuilder的頁面。

若要自訂，您可以編輯「頁 **[!UICONTROL 面擷取]** 」步驟 **[!UICONTROL 的「引]** 數」標籤。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面擷取處理常式**:從彈出式清單中，選取您要使用的處理常式。 擷取處理常式會針對由相關人員選擇的特定轉譯 `RenditionPicker` 進行操作(請參 `ExtractionHandler` 閱API)。
在標準中 [!DNL Experience Manager] 安裝下列項目：
   * IDML匯出擷取控制代碼：在 `IDML` 在MediaExtract步驟中產生的轉譯。

* **頁面名稱**:指定要指派給產生頁面的名稱。 若保留為空白，則名稱為「page」（若「page」已存在，則為衍生項目）。

* **頁面標題**:指定您要指派給產生頁面的標題。

* **頁面根路徑**:產生頁面的根位置路徑。 如果保留為空白，則會使用保留資產轉譯的節點。

* **頁面範本**:產生產生的頁面時要使用的範本。

* **頁面設計**:產生產生的頁面時要使用的頁面設計。

### 為配置代理工作器 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>工作程式駐留在代理實例上。

1. 在工具主控台中，展開 **[!UICONTROL Cloud Services配置]** 中。 然後展開 **[!UICONTROL 雲端代理設定]**.

1. 連按兩下 **[!UICONTROL IDS工作器]** ，以開啟以進行設定。

1. 按一下 **[!UICONTROL 編輯]** 要開啟「配置」對話框並定義所需的設定：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS池**
要用於與通信的SOAP端點 [!DNL InDesign Server]. 您可以新增、移除和訂購項目為必要項目。

1. 按一下「確定」以儲存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

若 [!DNL InDesign Server] 和 [!DNL Experience Manager] 位於不同的主機上，或其中一個或兩個應用程式在預設埠上不工作，然後配置 [!UICONTROL Day CQ Link Externalizer] 為 [!DNL InDesign Server].

1. 在 `https://[aem_server]:[port]/system/console/configMgr`.
1. 找出設定 **[!UICONTROL Day CQ Link Externalizer]**. 按一下 **[!UICONTROL 編輯]** 來開啟。
1. 連結外部化程式設定可協助為 [!DNL Experience Manager] 部署和 [!DNL InDesign Server]. 使用 **[!UICONTROL 網域]** 欄位，指定 [!DNL Adobe InDesign Server]. 按一下「**儲存**」。

   在絕對URL中，使用 `localhost` 做為本機（作者）例項的主機名稱，以及發佈例項的主機名稱或IP位址，如下圖所示。

   ![連結外部化程式設定](assets/link-externalizer-config.png)

### 為 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

您現在可以為ID啟用平行作業處理。 確定最大並行作業數(`x`) [!DNL InDesign Server] 可以處理：

* 在單台多處理器電腦上，並行作業的最大數量(`x`) [!DNL InDesign Server] 可處理的數量比運行ID的處理器數量少1。
* 在多台電腦上運行ID時，您需要計算可用處理器總數（即所有電腦上的），然後減去電腦總數。

要配置並行IDS作業的數量：

1. 開啟 **[!UICONTROL 配置]** Felix Console的標籤；例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 在下方選取IDS處理佇列 `Apache Sling Job Queue Configuration`.

1. 設定:

   * **類型** - `Parallel`
   * **最大並行作業數** - `<*x*>` （如上文計算）

1. 儲存這些變更。
1. 要啟用對AdobeCS6和更高版本的多會話支援，請檢查 `enable.multisession.name` 核取方塊，在下 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定。
1. 建立 [池 `x` 將SOAP端點新增至IDS工作器設定，以啟用IDS工作器](#configuring-the-proxy-worker-for-indesign-server).

   如果有多台電腦在運行 [!DNL InDesign Server]，為每台電腦添加SOAP端點（每台電腦的處理器數–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作池時，您可以啟用IDS工作池的封鎖清單。
>
>若要這麼做，請啟用 **[!UICONTROL enable.retry.name]** 核取方塊，位於 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定，可啟用IDS作業擷取。
>
>此外，在 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 設定，請為 `max.errors.to.blacklist` 參數，它確定在從作業處理程式清單中禁止ID之前的作業檢索數。
>
>依預設，在可設定(`retry.interval.to.whitelist.name`)重新驗證IDS背景工作的分鐘數。 如果聯機找到該工作，則會從阻止清單中刪除該工作。

## 啟用 [!DNL InDesign Server] 10.0或更新版本 {#enabling-support-for-indesign-server-or-later}

針對 [!DNL InDesign Server] 10.0或更高版本，請執行以下步驟以啟用多會話支援。

1. 從 [!DNL Experience Manager Assets] 執行個體 `https://[aem_server]:[port]/system/console/configMgr`.
1. 編輯設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. 選取 **[!UICONTROL ids.cc.enable]** ，然後按一下 **[!UICONTROL 儲存]**.

>[!NOTE]
>
>針對 [!DNL InDesign Server] 整合 [!DNL Experience Manager Assets]，請使用多核處理器，因為單核系統不支援整合所需的會話支援功能。

## 設定 [!DNL Experience Manager] 憑據 {#configure-aem-credentials}

您可以更改用於訪問 [!DNL InDesign Server] 從 [!DNL Experience Manager] 部署，而不會中斷與 [!DNL InDesign Server].

1. 前往 `/etc/cloudservices/proxy.html`.
1. 在對話方塊中，指定新的使用者名稱和密碼。
1. 儲存憑證。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

