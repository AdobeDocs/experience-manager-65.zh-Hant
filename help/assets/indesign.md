---
title: 整合 [!DNL Assets] 與 [!DNL InDesign Server]
description: 瞭解如何整合 [!DNL Adobe Experience Manager Assets] 與 [!DNL Adobe InDesign Server]。
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 4%

---

# 整合 [!DNL Adobe Experience Manager Assets] 與 [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用：

* 用於分配某些處理任務的負載的代理。 代理是 [!DNL Experience Manager] 與代理工作程式通信以完成特定任務的實例，以及 [!DNL Experience Manager] 實例以傳遞結果。
* 定義和管理特定任務的代理工作程式。
這些任務可以涵蓋各種任務；例如，使用 [!DNL InDesign Server] 處理檔案。

要將檔案完全上載到 [!DNL Experience Manager Assets] 你用 [!DNL Adobe InDesign] 使用代理。 這使用代理工作程式與 [!DNL Adobe InDesign Server]，也請參見Wiki頁。 [指令碼](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 運行以提取元資料並生成各種格式副本 [!DNL Experience Manager Assets]。 代理工作程式啟用 [!DNL InDesign Server] 和 [!DNL Experience Manager] 雲配置中的實例。

>[!NOTE]
>
>[!DNL Adobe InDesign] 作為兩個單獨的產品提供。 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 用於設計打印和數字分發頁面佈局的案頭應用。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 使您能夠根據已建立的文檔以寫程式方式建立自動文檔 [!DNL InDesign]。 它以服務的形式運行，為它提供介面 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.指令碼寫入 [!DNL ExtendScript]，與 [!DNL JavaScript]。 有關 [!DNL InDesign] 指令碼參見 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 提取工作原理 {#how-the-extraction-works}

的 [!DNL Adobe InDesign Server] 可與 [!DNL Experience Manager Assets] 使INDD檔案 [!DNL InDesign] 可以上傳、生成格式副本、提取所有媒體（例如視頻）並儲存為資產：

>[!NOTE]
>
>以前版本 [!DNL Experience Manager] 能夠提取XMP和縮略圖，現在可以提取所有媒體。

1. 將INDD檔案上載到 [!DNL Experience Manager Assets]。
1. 框架將命令指令碼發送到 [!DNL InDesign Server] 通過SOAP（簡單對象訪問協定）。
此命令指令碼將：

   * 檢索INDD檔案。
   * 執行 [!DNL InDesign Server] 命令：

      * 將提取結構、文本和任何媒體檔案。
      * PDF和JPG格式副本將生成。
      * HTML和IDML格式副本將生成。
   * 將結果檔案發回 [!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是基於XML的格式，用於呈現 [!DNL InDesign] 的子菜單。 它以壓縮包的形式儲存， [ZIP](https://www.techterms.com/definition/zip) 壓縮。 有關詳細資訊，請參見 [InDesign交換格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果 [!DNL InDesign Server] 未安裝或未配置，則仍可將INDD檔案上載到 [!DNL Experience Manager]。 但生成的格式副本將限於PNG和JPEG。 您將無法生成HTML、.idml或頁面格式副本。

1. 提取和格式副本生成後：

   * 結構被複製到 `cq:Page` （格式副本類型）。
   * 提取的文本和檔案儲存在 [!DNL Experience Manager Assets]。
   * 所有格式副本都儲存在 [!DNL Experience Manager Assets]，在資產本身中。

## 整合 [!DNL InDesign Server] Experience Manager {#integrating-the-indesign-server-with-aem}

整合 [!DNL InDesign Server] 用於 [!DNL Experience Manager Assets] 配置代理後，您需要：

1. [安裝InDesign Server](#installing-the-indesign-server)。
1. 如果需要， [配置Experience Manager Assets工作流](#configuring-the-aem-assets-workflow)。
只有在預設值不適合您的實例時，才需要這樣做。
1. 配置 [InDesign Server的代理工作程式](#configuring-the-proxy-worker-for-indesign-server)。

### 安裝 [!DNL InDesign Server] {#installing-the-indesign-server}

安裝並啟動 [!DNL InDesign Server] 用於 [!DNL Experience Manager]:

1. 下載並安裝 [!DNL InDesign Server]。

1. 如果需要，可以自定義 [!DNL InDesign Server] 實例。

1. 從命令行啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這將在埠8080上使用SOAP插件啟動伺服器。 所有日誌消息和輸出都直接寫入命令窗口。

   >[!NOTE]
   >
   >如果要將輸出消息保存到檔案，則使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置 [!DNL Experience Manager Assets] 工作流 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有預配置的工作流 **[!UICONTROL DAM更新資產]**，具有特定於 [!DNL InDesign]:

* [媒體提取](#media-extraction)
* [頁面提取](#page-extraction)

此工作流是使用預設值設定的，這些預設值可適用於您在各種作者實例上的設定(這是標準工作流，因此在下面提供了詳細資訊 [編輯工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-step))。 如果使用預設值（包括SOAP埠），則不需要配置。

安裝後，正在上載 [!DNL InDesign] 檔案 [!DNL Experience Manager Assets] （通過任何常用方法）觸發工作流以處理資產並準備各種格式副本。 通過將INDD檔案上載到 [!DNL Experience Manager Assets] 確認您看到IDS建立的不同格式副本 `<*your_asset*>.indd/Renditions`

#### 介質提取 {#media-extraction}

此步驟控制從INDD檔案中提取介質。

若要自訂，您可以編 **[!UICONTROL 輯]** 「媒體擷 **[!UICONTROL 取」步驟的「引]** 數」標籤。

![媒體抽取參數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體抽取參數和指令碼路徑

* **ExtendScript圖書館**:這是其他指令碼所需的簡單http get/post方法庫。

* **擴展指令碼**:可以在此處指定不同的指令碼組合。 如果希望在 [!DNL InDesign Server]，將指令碼保存在 `/apps/settings/dam/indesign/scripts`。

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>請 勿變更ExtendScript程式庫。此庫提供與Sling通信所需的HTTP功能。 此設定指定要發送到的庫 [!DNL InDesign Server] 供使用。

的 `ThumbnailExport.jsx` 「媒體提取」工作流步驟運行的指令碼將生成JPG格式的縮略圖格式副本。 此格式副本由「進程縮略圖」工作流步驟使用，以生成所需的靜態格式副本 [!DNL Experience Manager]。

您可以配置「流程縮略圖」工作流步驟，以生成不同大小的靜態格式副本。 確保不刪除預設值，因為 [!DNL Experience Manager Assets] 。 最後，「刪除影像預覽格式副本」工作流步驟將刪除JPG縮略圖格式副本，因為不再需要它。

#### 頁面提取 {#page-extraction}

這將建立 [!DNL Experience Manager] 的子菜單。 提取處理程式用於從格式副本(當前HTML或IDML)中提取資料。 此資料然後用於使用PageBuilder建立頁面。

若要自訂，您可以編輯「頁 **[!UICONTROL 面擷取]** 」步驟 **[!UICONTROL 的「引]** 數」標籤。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面提取處理程式**:從彈出式清單中，選擇要使用的處理程式。 擷取處理常式會針對由相關人員選擇的特定轉譯 `RenditionPicker` 進行操作(請參 `ExtractionHandler` 閱API)。
在標準中 [!DNL Experience Manager] 安裝可用：
   * IDML導出提取句柄：在 `IDML` 在MediaExtract步驟中生成的格式副本。

* **頁名**:指定要分配給結果頁面的名稱。 如果留空，則名稱為「page」（如果「page」已存在，則為派生）。

* **頁面標題**:指定要分配給結果頁面的標題。

* **頁根路徑**:生成頁面的根位置的路徑。 如果保留為空，則將使用保存資產格式副本的節點。

* **頁面模板**:生成結果頁時要使用的模板。

* **頁面設計**:生成結果頁面時要使用的頁面設計。

### 為配置代理工作程式 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>工作程式駐留在代理實例上。

1. 在工具控制台中，展開 **[!UICONTROL Cloud Services配置]** 的子菜單。 然後展開 **[!UICONTROL 雲代理配置]**。

1. 連按兩下 **[!UICONTROL IDS工作器]** ，以開啟以進行設定。

1. 按一下 **[!UICONTROL 編輯]** 要開啟配置對話框並定義所需設定：

   ![代理伺服器配置](assets/proxy_idsworkerconfig.png)

   * **IDS池**
用於與 [!DNL InDesign Server]。 您可以添加、刪除和需要訂購項目。

1. 按一下「確定」保存。

### 配置日CQ連結外部化程式 {#configuring-day-cq-link-externalizer}

如果 [!DNL InDesign Server] 和 [!DNL Experience Manager] 位於不同的主機上，或者其中一個或兩個應用程式都未在預設埠上工作，然後配置 [!UICONTROL 第CQ天連結外部化程式] 為 [!DNL InDesign Server]。

1. 訪問Web控制台 `https://[aem_server]:[port]/system/console/configMgr`。
1. 找到配置 **[!UICONTROL 第CQ天連結外部化程式]**。 按一下 **[!UICONTROL 編輯]** 開啟。
1. 連結外部化程式設定幫助為 [!DNL Experience Manager] 部署和 [!DNL InDesign Server]。 使用 **[!UICONTROL 域]** 欄位，以指定 [!DNL Adobe InDesign Server]。 按一下「**儲存**」。

   在絕對URL中，使用 `localhost` 作為本地（作者）實例的主機名，以及發佈實例的主機名或IP地址，如下圖所示。

   ![連結外部化器設定](assets/link-externalizer-config.png)

### 啟用並行作業處理 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

現在，您可以啟用IDS的並行作業處理。 確定最大並行作業數(`x`) [!DNL InDesign Server] 可以處理：

* 在單個多處理器電腦上，並行作業的最大數(`x`) [!DNL InDesign Server] 可以處理的處理器數量比運行IDS的處理器數量少一倍。
* 在多台電腦上運行IDS時，需要計算可用處理器總數（即所有電腦上），然後減去電腦總數。

要配置並行IDS作業數：

1. 開啟 **[!UICONTROL 配置]** Felix控制台。例如： `https://[aem_server]:[port]/system/console/configMgr`。

1. 選擇下的IDS處理隊列 `Apache Sling Job Queue Configuration`。

1. 設定:

   * **類型** - `Parallel`
   * **最大並行作業數** - `<*x*>` （如上文計算）

1. 保存這些更改。
1. 要啟用對AdobeCS6及更高版本的多會話支援，請選中 `enable.multisession.name` 複選框，在 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置。
1. 建立 [池 `x` 通過將SOAP終結點添加到IDS Worker配置來IDS工作程式](#configuring-the-proxy-worker-for-indesign-server)。

   如果有多台電腦在運行 [!DNL InDesign Server]，為每台電腦添加SOAP端點（每台電腦的處理器數–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作程式池時，可以啟用IDS工作程式的阻止清單。
>
>為此，請啟用 **[!UICONTROL enable.retry.name]** 複選框，在 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置，它啟用IDS作業檢索器。
>
>另外，在 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 配置，為 `max.errors.to.blacklist` 參數，它確定在將IDS從作業處理程式清單中禁止之前的作業檢索次數。
>
>預設情況下，在可配置(`retry.interval.to.whitelist.name`)重新驗證IDS工作進程的時間（分鐘）。 如果聯機找到該工作人員，則會將其從阻止清單中刪除。

## 為 [!DNL InDesign Server] 10.0或更高版本 {#enabling-support-for-indesign-server-or-later}

對於 [!DNL InDesign Server] 10.0或更高版本，請執行以下步驟以啟用多會話支援。

1. 從您的 [!DNL Experience Manager Assets] 實例 `https://[aem_server]:[port]/system/console/configMgr`。
1. 編輯配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. 選擇 **[!UICONTROL ids.cc.en]** ，然後按一下 **[!UICONTROL 保存]**。

>[!NOTE]
>
>對於 [!DNL InDesign Server] 整合 [!DNL Experience Manager Assets]，使用多核處理器，因為單核系統不支援整合所需的會話支援功能。

## 配置 [!DNL Experience Manager] 憑據 {#configure-aem-credentials}

您可以更改預設管理員憑據（用戶名和密碼）以訪問 [!DNL InDesign Server] 從 [!DNL Experience Manager] 部署，而不中斷與 [!DNL InDesign Server]。

1. 前往 `/etc/cloudservices/proxy.html`.
1. 在對話框中，指定新用戶名和密碼。
1. 保存憑據。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

