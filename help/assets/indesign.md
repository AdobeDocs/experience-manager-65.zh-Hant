---
title: 將 [!DNL Assets] 與 [!DNL InDesign Server]整合
description: 了解如何將 [!DNL Adobe Experience Manager Assets] 與 [!DNL Adobe InDesign Server]整合。
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 3%

---

# 將[!DNL Adobe Experience Manager Assets]與[!DNL Adobe InDesign Server]整合 {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用：

* 分配特定處理任務的負載的代理。 Proxy是與Proxy工作者通訊以完成特定任務的[!DNL Experience Manager]例項，以及傳送結果的其他[!DNL Experience Manager]例項。
* 定義和管理特定任務的代理工作。
這可以涵蓋各種任務；例如，使用[!DNL InDesign Server]處理檔案。

若要將檔案完全上傳至您使用[!DNL Adobe InDesign]代理建立的[!DNL Experience Manager Assets]。 這會使用代理工作器與[!DNL Adobe InDesign Server]通訊，其中[scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)會執行以擷取中繼資料並產生[!DNL Experience Manager Assets]的各種轉譯。 在雲配置中，代理工作器啟用[!DNL InDesign Server]和[!DNL Experience Manager]實例之間的雙向通信。

>[!NOTE]
>
>[!DNL Adobe InDesign] 提供為兩種不同的產品。[Adobe](https://www.adobe.com/products/indesign.html) InDesign案頭應用程式，用於設計用於打印和數字分發的頁面佈局。[Adobe InDesign ](https://www.adobe.com/products/indesignserver.html) Server讓您能夠根據您使用建立的內容，以程式設計方式建立自動化 [!DNL InDesign]檔案。它作為提供其[ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)引擎介面的服務運行。指令碼寫入[!DNL ExtendScript]，與[!DNL JavaScript]類似。 有關[!DNL InDesign]指令碼的資訊，請參見[https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。

## 提取的運作方式 {#how-the-extraction-works}

[!DNL Adobe InDesign Server]可與[!DNL Experience Manager Assets]整合，以便上傳、產生轉譯、擷取所有媒體（例如視訊）並儲存為資產：[!DNL InDesign]

>[!NOTE]
>
>舊版[!DNL Experience Manager]可擷取XMP和縮圖，現在可擷取所有媒體。

1. 將INDD檔案上傳至[!DNL Experience Manager Assets]。
1. 框架通過SOAP（簡單對象訪問協定）將命令指令碼發送到[!DNL InDesign Server]。
此命令指令碼將：

   * 檢索INDD檔案。
   * 執行[!DNL InDesign Server]命令：

      * 會擷取結構、文字和任何媒體檔案。
      * 會產生PDF和JPG轉譯。
      * 會產生HTML和IDML轉譯。
   * 將產生的檔案發回[!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是基於XML的格式，可呈現[!DNL InDesign]檔案的所有內容。 會使用[ZIP](https://www.techterms.com/definition/zip)壓縮，以壓縮套件形式儲存。 有關詳細資訊，請參閱[InDesign交換格式INX和IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >如果未安裝或未配置[!DNL InDesign Server]，則仍可將INDD檔案上載到[!DNL Experience Manager]中。 不過，產生的轉譯將限制為PNG和JPEG。 您將無法產生HTML、.idml或頁面轉譯。

1. 擷取和轉譯產生後：

   * 此結構會複製到`cq:Page`（轉譯類型）。
   * 提取的文本和檔案儲存在[!DNL Experience Manager Assets]中。
   * 所有轉譯都會儲存在[!DNL Experience Manager Assets]中，位於資產本身。

## 將[!DNL InDesign Server]與Experience Manager整合 {#integrating-the-indesign-server-with-aem}

若要整合[!DNL InDesign Server]以與[!DNL Experience Manager Assets]搭配使用，並在設定代理後，您需要：

1. [安裝InDesign Server](#installing-the-indesign-server)。
1. 如有需要，請[設定Experience Manager資產工作流程](#configuring-the-aem-assets-workflow)。
只有在預設值不適合您的例項時，才需要這個選項。
1. 為InDesign Server](#configuring-the-proxy-worker-for-indesign-server)配置[代理工作器。

### 安裝[!DNL InDesign Server] {#installing-the-indesign-server}

要安裝並啟動[!DNL InDesign Server]以用於[!DNL Experience Manager]，請執行以下操作：

1. 下載並安裝[!DNL InDesign Server]。

1. 如果需要，可以自定義[!DNL InDesign Server]實例的配置。

1. 從命令行啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這會在連接埠8080上以SOAP外掛程式監聽來啟動伺服器。 所有日誌消息和輸出都直接寫入命令窗口。

   >[!NOTE]
   >
   >如果要將輸出消息保存到檔案，則使用重定向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置[!DNL Experience Manager Assets]工作流 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 有預先設定的工 **[!UICONTROL 作流程DAM更新資產]**，其中包含數個處理步驟，專門用 [!DNL InDesign]於：

* [媒體提取](#media-extraction)
* [頁面提取](#page-extraction)

此工作流程是以預設值設定的，這些預設值可針對您在各種製作執行個體上的設定進行調整（這是標準工作流程，因此可在[編輯工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)下取得詳細資訊）。 如果您使用預設值（包括SOAP埠），則無需配置。

設定後，將[!DNL InDesign]檔案上傳至[!DNL Experience Manager Assets]（透過任何常用方法）會觸發工作流程以處理資產並準備各種轉譯。 將INDD檔案上傳至[!DNL Experience Manager Assets]以確認您看見ID在`<*your_asset*>.indd/Renditions`下建立的不同轉譯

#### 媒體擷取 {#media-extraction}

此步驟控制從INDD檔案中提取介質。

若要自訂，您可以編 **[!UICONTROL 輯]** 「媒體擷 **[!UICONTROL 取」步驟的「引]** 數」標籤。

![媒體擷取引數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體擷取引數和指令碼路徑

* **ExtendScript資料庫**:這是其他指令碼所需的簡單http get/post方法程式庫。

* **擴充指令碼**:您可以在此處指定不同的指令碼組合。如果希望在[!DNL InDesign Server]上執行自己的指令碼，請在`/apps/settings/dam/indesign/scripts`保存指令碼。

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>請 勿變更ExtendScript程式庫。此程式庫提供與Sling通訊所需的HTTP功能。 此設定指定要發送到[!DNL InDesign Server]以供其使用的庫。

由「媒體擷取」工作流程步驟執行的`ThumbnailExport.jsx`指令碼會產生JPG格式的縮圖轉譯。 「處理縮圖」工作流步驟將使用此格式副本生成[!DNL Experience Manager]所需的靜態格式副本。

您可以設定「處理縮圖」工作流程步驟，以產生不同大小的靜態轉譯。 請確定您不要移除預設值，因為這些預設值是[!DNL Experience Manager Assets]介面的必要項目。 最後，「刪除影像預覽轉譯」工作流程步驟會移除JPG縮圖轉譯，因為這已不再需要。

#### 頁面擷取 {#page-extraction}

這會從擷取的元素建立[!DNL Experience Manager]頁面。 擷取處理常式可用來從轉譯（目前為HTML或IDML）中擷取資料。 然後，系統會使用此資料建立使用PageBuilder的頁面。

若要自訂，您可以編輯「頁 **[!UICONTROL 面擷取]** 」步驟 **[!UICONTROL 的「引]** 數」標籤。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面擷取處理常式**:從彈出式清單中，選取您要使用的處理常式。擷取處理常式會針對由相關人員選擇的特定轉譯 `RenditionPicker` 進行操作(請參 `ExtractionHandler` 閱API)。
在標準[!DNL Experience Manager]安裝中，可以使用以下內容：
   * IDML匯出擷取控制代碼：對在MediaExtract步驟中產生的`IDML`轉譯進行操作。

* **頁面名稱**:指定要指派給產生頁面的名稱。若保留為空白，則名稱為「page」（若「page」已存在，則為衍生項目）。

* **頁面標題**:指定您要指派給產生頁面的標題。

* **頁面根路徑**:產生頁面的根位置路徑。如果保留為空白，則會使用保留資產轉譯的節點。

* **頁面範本**:產生產生的頁面時要使用的範本。

* **頁面設計**:產生產生的頁面時要使用的頁面設計。

### 為[!DNL InDesign Server]配置代理工作器 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>工作程式駐留在代理實例上。

1. 在「工具」控制台中，展開左窗格中的&#x200B;**[!UICONTROL Cloud Services配置]**。 然後展開&#x200B;**[!UICONTROL 雲代理配置]**。

1. 連按兩下 **[!UICONTROL IDS工作器]** ，以開啟以進行設定。

1. 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟配置對話框並定義所需設定：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
Pool要用於與通信的SOAP端 [!DNL InDesign Server]點。您可以新增、移除和訂購項目為必要項目。

1. 按一下「確定」以儲存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果[!DNL InDesign Server]和[!DNL Experience Manager]位於不同的主機上，或者這兩個應用程式中的一個或兩個都未在預設埠上工作，則配置[!UICONTROL  Day CQ Link Externalizer]以設定[!DNL InDesign Server]的主機名、埠和內容路徑。

1. 在`https://[aem_server]:[port]/system/console/configMgr`訪問Web控制台。
1. 找到配置&#x200B;**[!UICONTROL Day CQ Link Externalizer]**。 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟。
1. 連結外部化程式設定有助於為[!DNL Experience Manager]部署和[!DNL InDesign Server]建立絕對URL。 使用&#x200B;**[!UICONTROL Domains]**&#x200B;欄位指定[!DNL Adobe InDesign Server]的主機名。 按一下「**儲存**」。

   在絕對URL中，使用`localhost`作為本機（作者）例項的主機名稱，以及發佈例項的主機名稱或IP位址，如下圖所示。

   ![連結外部化程式設定](assets/link-externalizer-config.png)

### 為[!DNL InDesign Server]啟用並行作業處理 {#enabling-parallel-job-processing-for-indesign-server}

您現在可以為ID啟用平行作業處理。 確定[!DNL InDesign Server]可處理的並行作業的最大數量(`x`):

* 在單台多處理器電腦上，[!DNL InDesign Server]可處理的並行作業(`x`)的最大數量比運行IDS的處理器數少1。
* 在多台電腦上運行ID時，您需要計算可用處理器總數（即所有電腦上的），然後減去電腦總數。

要配置並行IDS作業的數量：

1. 開啟Felix Console的&#x200B;**[!UICONTROL Configurations]**&#x200B;標籤；例如：`https://[aem_server]:[port]/system/console/configMgr`。

1. 在`Apache Sling Job Queue Configuration`下選取IDS處理佇列。

1. 設定:

   * **類型**  -  `Parallel`
   * **最大並行作業**  -  `<*x*>` （如上所計算）

1. 儲存這些變更。
1. 若要啟用AdobeCS6及更新版本的多工作階段支援，請核取`com.day.cq.dam.ids.impl.IDSJobProcessor.name`設定下的`enable.multisession.name`核取方塊。
1. 通過向IDS工作器配置](#configuring-the-proxy-worker-for-indesign-server)中添加SOAP端點，建立[池`x` ID工作器。

   如果有多台電腦運行[!DNL InDesign Server]，請為每台電腦添加SOAP端點（每台電腦的處理器數–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用工作池時，您可以啟用IDS工作池的封鎖清單。
>
>要執行此操作，請在`com.day.cq.dam.ids.impl.IDSJobProcessor.name`配置下啟用&#x200B;**[!UICONTROL enable.retry.name]**&#x200B;複選框，該複選框可啟用IDS作業檢索。
>
>此外，在`com.day.cq.dam.ids.impl.IDSPoolImpl.name`配置下，為`max.errors.to.blacklist`參數設定一個正值，該值確定了在從作業處理程式清單中禁止ID之前的作業檢索數。
>
>預設情況下，在可設定(`retry.interval.to.whitelist.name`)的時間（以分鐘為單位）之後，IDS工作器會重新驗證。 如果聯機找到該工作，則會從阻止清單中刪除該工作。

## 啟用[!DNL InDesign Server] 10.0或更新版本支援 {#enabling-support-for-indesign-server-or-later}

對於[!DNL InDesign Server] 10.0或更高版本，請執行以下步驟以啟用多會話支援。

1. 從您的[!DNL Experience Manager Assets]實例`https://[aem_server]:[port]/system/console/configMgr`中開啟Configuration Manager。
1. 編輯配置`com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. 選擇&#x200B;**[!UICONTROL ids.cc.enable]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>對於與[!DNL Experience Manager Assets]的[!DNL InDesign Server]整合，請使用多核處理器，因為單核系統不支援整合所需的會話支援功能。

## 配置[!DNL Experience Manager]憑據 {#configure-aem-credentials}

您可以更改預設管理員憑據（用戶名和密碼），以便從[!DNL Experience Manager]部署訪問[!DNL InDesign Server]，而不中斷與[!DNL InDesign Server]的整合。

1. 前往 `/etc/cloudservices/proxy.html`.
1. 在對話方塊中，指定新的使用者名稱和密碼。
1. 儲存憑證。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

