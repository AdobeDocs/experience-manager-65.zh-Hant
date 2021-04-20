---
title: 將 [!DNL Assets] 與 [!DNL InDesign Server]整合
description: 瞭解如何將 [!DNL Adobe Experience Manager Assets] 與 [!DNL Adobe InDesign Server]整合。
contentOwner: AG
role: Administrator
feature: Publishing
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 4%

---


# 將[!DNL Adobe Experience Manager Assets]與[!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}整合

[!DNL Adobe Experience Manager Assets] 用途：

* 一個代理，用於分配特定處理任務的負載。 Proxy是與Proxy工作者通訊以完成特定工作的[!DNL Experience Manager]例項，以及傳送結果的其他[!DNL Experience Manager]例項。
* 用於定義和管理特定任務的代理工作器。
這些工作可以涵蓋各種任務；例如，使用[!DNL InDesign Server]處理檔案。

要將檔案完全上載到使用[!DNL Adobe InDesign]代理建立的[!DNL Experience Manager Assets]。 這會使用代理工作器與[!DNL Adobe InDesign Server]通訊，其中[scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)會執行以擷取中繼資料並產生[!DNL Experience Manager Assets]的各種轉譯。 代理工作器啟用雲配置中[!DNL InDesign Server]和[!DNL Experience Manager]實例之間的雙向通信。

>[!NOTE]
>
>[!DNL Adobe InDesign] 提供兩種不同的方案。[Adobe](https://www.adobe.com/products/indesign.html) InDesign案頭應用程式，用於設計平面印刷和數位散發的頁面版面。[Adobe InDesign](https://www.adobe.com/products/indesignserver.html) Serverenals you to programmable create automated documents on they you created with  [!DNL InDesign].它以服務形式運行，為其[ExtendScript](https://www.adobe.com/devnet/scripting.html)引擎提供介面。指令碼編寫在[!DNL ExtendScript]中，與[!DNL JavaScript]類似。 有關[!DNL InDesign]指令碼的資訊，請參見[https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 抽取的工作方式{#how-the-extraction-works}

[!DNL Adobe InDesign Server]可與[!DNL Experience Manager Assets]整合，以便上傳以[!DNL InDesign]建立的INDD檔案、產生轉譯、提取所有媒體（例如視訊）並儲存為資產：

>[!NOTE]
>
>舊版[!DNL Experience Manager]可以擷取縮XMP圖，現在可以擷取所有媒體。

1. 將INDD檔案上傳至[!DNL Experience Manager Assets]。
1. 框架通過SOAP（簡單對象訪問協定）將命令指令碼發送到[!DNL InDesign Server]。
此命令指令碼將：

   * 檢索INDD檔案。
   * 執行[!DNL InDesign Server]命令：

      * 會擷取結構、文字和任何媒體檔案。
      * 產生PDF和JPG轉譯。
      * 產生HTML和IDML轉譯。
   * 將產生的檔案張貼回[!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是以XML為基礎的格式，可轉譯[!DNL InDesign]檔案的所有內容。 它使用[ZIP](https://www.techterms.com/definition/zip)壓縮儲存為壓縮包。 如需詳細資訊，請參閱[InDesign交換格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果未安裝或未配置[!DNL InDesign Server]，則仍可將INDD檔案上載到[!DNL Experience Manager]。 但產生的轉譯將限制為PNG和JPEG。 您將無法產生HTML、.idml或頁面轉譯。

1. 擷取和轉譯產生後：

   * 此結構會複製到`cq:Page`（轉譯類型）。
   * 提取的文本和檔案儲存在[!DNL Experience Manager Assets]中。
   * 所有轉譯都儲存在[!DNL Experience Manager Assets]資產本身。

## 將[!DNL InDesign Server]與Experience Manager{#integrating-the-indesign-server-with-aem}整合

若要整合[!DNL InDesign Server]以搭配[!DNL Experience Manager Assets]使用，並在設定Proxy後，您必須：

1. [安裝InDesign Server](#installing-the-indesign-server)。
1. 如果需要，[配置Experience Manager資產工作流](#configuring-the-aem-assets-workflow)。
只有當預設值不適用於您的例項時，才需要這麼做。
1. 為InDesign Server配置[代理工作器。](#configuring-the-proxy-worker-for-indesign-server)

### 安裝[!DNL InDesign Server] {#installing-the-indesign-server}

要安裝並啟動[!DNL InDesign Server]以便與[!DNL Experience Manager]一起使用：

1. 下載並安裝[!DNL InDesign Server]。

1. 如果需要，您可以自定義[!DNL InDesign Server]實例的配置。

1. 從命令行啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這會在連接埠8080上以SOAP外掛程式監聽來啟動伺服器。 所有日誌消息和輸出都直接寫入命令窗口。

   >[!NOTE]
   >
   >如果要將輸出消息保存到檔案，則使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置[!DNL Experience Manager Assets]工作流{#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 具有預先設定的工作流程 **[!UICONTROL DAM更新資產]**，其中具有幾個流程步驟，專門用於 [!DNL InDesign]:

* [媒體提取](#media-extraction)
* [頁面提取](#page-extraction)

此工作流程會以預設值設定，這些預設值可適用於您在各種作者例項上的設定（這是標準工作流程，因此在[編輯工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)下可取得更多資訊）。 如果您使用預設值（包括SOAP埠），則不需要任何設定。

在設定後，將[!DNL InDesign]檔案上傳至[!DNL Experience Manager Assets]（透過任何常用方法）會觸發工作流程來處理資產並準備各種轉譯。 將INDD檔案上傳至[!DNL Experience Manager Assets]以測試您的設定，確認您看到IDS在`<*your_asset*>.indd/Renditions`下建立的不同轉譯

#### 介質提取{#media-extraction}

此步驟控制從INDD檔案抽取介質。

若要自訂，您可以編 **[!UICONTROL 輯]** 「媒體擷 **[!UICONTROL 取」步驟的「引]** 數」標籤。

![媒體擷取引數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體擷取引數和指令碼路徑

* **ExtendScript圖書館**:這是其他指令碼所需的簡單http get/post方法程式庫。

* **擴充指令碼**:您可以在此處指定不同的指令碼組合。如果希望在[!DNL InDesign Server]上執行自己的指令碼，請在`/apps/settings/dam/indesign/scripts`上保存指令碼。

如需[!DNL Adobe InDesign]指令碼的詳細資訊，請參閱[InDesign開發人員檔案](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>請 勿變更ExtendScript程式庫。此程式庫提供與Sling通訊所需的HTTP功能。 此設定指定要發送到[!DNL InDesign Server]的庫，以便在此處使用。

由「媒體擷取」工作流程步驟執行的`ThumbnailExport.jsx`指令碼會產生JPG格式的縮圖轉譯。 「處理縮圖」工作流步驟使用此格式副本來生成[!DNL Experience Manager]所需的靜態格式副本。

您可以設定「處理縮圖」工作流程步驟，以產生不同大小的靜態轉譯。 請確保不刪除預設值，因為[!DNL Experience Manager Assets]介面需要這些預設值。 最後，「刪除影像預覽轉譯」工作流程步驟會移除JPG縮圖轉譯，因為不再需要它。

#### 頁面擷取{#page-extraction}

這會從擷取的元素建立[!DNL Experience Manager]頁面。 擷取處理常式可用來從轉譯（目前為HTML或IDML）擷取資料。 然後，此資料會用於使用PageBuilder建立頁面。

若要自訂，您可以編輯「頁 **[!UICONTROL 面擷取]** 」步驟 **[!UICONTROL 的「引]** 數」標籤。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面擷取處理常式**:從彈出式清單中，選取您要使用的處理常式。擷取處理常式會針對由相關人員選擇的特定轉譯 `RenditionPicker` 進行操作(請參 `ExtractionHandler` 閱API)。
在標準[!DNL Experience Manager]安裝中，可使用以下功能：
   * IDML Export Extraction句柄：對在MediaExtract步驟中生成的`IDML`轉譯進行操作。

* **頁面名稱**:指定您要指派給產生頁面的名稱。若保留空白，則名稱為「page」（若「page」已存在，則為衍生值）。

* **頁面標題**:指定您要指派給產生頁面的標題。

* **頁面根路徑**:結果頁面的根位置路徑。如果保留空白，則會使用保留資產轉譯的節點。

* **頁面範本**:產生產生頁面時要使用的範本。

* **頁面設計**:產生產生頁面時要使用的頁面設計。

### 為[!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}配置代理工作器

>[!NOTE]
>
>該工作器駐留在代理實例上。

1. 在「工具」控制台中，展開左窗格中的「Cloud Services配置」。 ****&#x200B;然後展開&#x200B;**[!UICONTROL 雲端代理設定]**。

1. 連按兩下 **[!UICONTROL IDS工作器]** ，以開啟以進行設定。

1. 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;開啟配置對話框並定義所需設定：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
池用於與通信的SOAP端點 [!DNL InDesign Server]。您可以新增、移除和訂購項目。

1. 按一下「確定」以儲存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果[!DNL InDesign Server]和[!DNL Experience Manager]位於不同的主機上，或者其中一個或兩個應用程式都未在預設埠上工作，則配置[!UICONTROL Day CQ Link Externalizer]以設定[!DNL InDesign Server]的主機名、埠和內容路徑。

1. 訪問`https://[aem_server]:[port]/system/console/configMgr`的Web控制台。
1. 找到配置&#x200B;**[!UICONTROL Day CQ Link Externalizer]**。 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟。
1. 連結外部化設定可協助建立[!DNL Experience Manager]部署和[!DNL InDesign Server]的絕對URL。 使用&#x200B;**[!UICONTROL 域]**&#x200B;欄位指定[!DNL Adobe InDesign Server]的主機名和上下文路徑。 按一下「**儲存**」。

   ![連結外部化設定](assets/link-externalizer-config.png)

### 啟用[!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}的並行作業處理

您現在可以啟用IDS的並行作業處理。 確定[!DNL InDesign Server]可處理的並行作業的最大數目(`x`):

* 在單個多處理器機器上，[!DNL InDesign Server]可處理的並行作業(`x`)的最大數量比運行IDS的處理器數少1。
* 在多台電腦上運行IDS時，您需要計算可用處理器總數（即所有電腦上），然後減去電腦總數。

要配置並行IDS作業數：

1. 開啟Felix控制台的&#x200B;**[!UICONTROL Configurations]**&#x200B;頁籤；例如：`https://[aem_server]:[port]/system/console/configMgr`。

1. 在`Apache Sling Job Queue Configuration`下選擇IDS處理隊列。

1. 設定:

   * **類型** -  `Parallel`
   * **最大並行作業** -  `<*x*>` （如上所計算）

1. 儲存這些變更。
1. 若要啟用AdobeCS6和更新版本的多階段作業支援，請勾選`com.day.cq.dam.ids.impl.IDSJobProcessor.name`組態下的`enable.multisession.name`核取方塊。
1. 通過將SOAP端點添加到IDS Worker配置](#configuring-the-proxy-worker-for-indesign-server)中，建立`x` IDS工作器的[池。

   如果有多台電腦運行[!DNL InDesign Server]，請為每個電腦添加SOAP端點（每台電腦的處理器數-1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作池時，可以啟用IDS工作池的阻止清單。
>
>要執行此操作，請啟用`com.day.cq.dam.ids.impl.IDSJobProcessor.name`配置下的&#x200B;**[!UICONTROL enable.retry.name]**&#x200B;複選框，該複選框將啟用IDS作業檢索。
>
>此外，在`com.day.cq.dam.ids.impl.IDSPoolImpl.name`配置下，為`max.errors.to.blacklist`參數設定正值，該值在禁止IDS進入作業處理程式清單之前確定作業檢索的數量。
>
>預設情況下，在以分鐘為單位的可配置(`retry.interval.to.whitelist.name`)時間後，IDS工作器將重新驗證。 如果線上找到該工作器，則會將其從被阻止的清單中刪除。

## 啟用[!DNL InDesign Server] 10.0或更新版本{#enabling-support-for-indesign-server-or-later}的支援

對於[!DNL InDesign Server] 10.0或更高版本，請執行以下步驟以啟用多會話支援。

1. 從[!DNL Experience Manager Assets]實例`https://[aem_server]:[port]/system/console/configMgr`開啟配置管理器。
1. 編輯配置`com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. 選擇&#x200B;**[!UICONTROL ids.cc.enable]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>對於與[!DNL Experience Manager Assets]整合的[!DNL InDesign Server]，請使用多核處理器，因為單核系統不支援整合所需的會話支援功能。

## 配置[!DNL Experience Manager]憑據{#configure-aem-credentials}

您可以更改從[!DNL Experience Manager]部署訪問[!DNL InDesign Server]的預設管理員憑據（用戶名和密碼），而不中斷與[!DNL InDesign Server]的整合。

1. 前往 `/etc/cloudservices/proxy.html`.
1. 在對話方塊中，指定新的使用者名稱和密碼。
1. 儲存認證。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

