---
title: 整合 [!DNL Assets] 與 [!DNL InDesign Server]
description: 瞭解如何整合 [!DNL Adobe Experience Manager Assets] 與 [!DNL Adobe InDesign Server]。
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 75c15b0f0e4de2ea7fff339ae46b88ce8f6af83f
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 2%

---

# 將[!DNL Adobe Experience Manager Assets]與[!DNL Adobe InDesign Server]整合 {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets]使用：

* 用於分配特定處理任務負載的Proxy。 Proxy是與Proxy工作者通訊以完成特定任務的[!DNL Experience Manager]執行個體，以及傳送結果的其他[!DNL Experience Manager]執行個體。
* Proxy Worker用來定義和管理特定工作。
這些可以涵蓋各種工作；例如，使用[!DNL InDesign Server]處理檔案。

若要將檔案完全上傳至您已使用[!DNL Adobe InDesign]建立的[!DNL Experience Manager Assets]，請使用Proxy。 這會使用Proxy Worker與[!DNL Adobe InDesign Server]通訊，其中執行指令碼以擷取中繼資料並產生[!DNL Experience Manager Assets]的各種轉譯。 Proxy背景工作可啟用雲端組態中[!DNL InDesign Server]與[!DNL Experience Manager]執行個體之間的雙向通訊。

>[!NOTE]
>
>[!DNL Adobe InDesign]以兩種不同的方案提供。 [Adobe InDesign](https://www.adobe.com/products/indesign.html)案頭應用程式，用來設計列印和數位分送的版面配置。 [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html)可讓您根據使用[!DNL InDesign]建立的內容，以程式設計方式建立自動化檔案。 它是以提供ExtendScript引擎介面的服務方式運作。 指令碼是以[!DNL ExtendScript]撰寫，類似[!DNL JavaScript]。

## 擷取的運作方式 {#how-the-extraction-works}

[!DNL Adobe InDesign Server]可以與[!DNL Experience Manager Assets]整合，以便上傳以[!DNL InDesign]建立的INDD檔案、產生轉譯、擷取所有媒體（例如視訊）並儲存為資產：

>[!NOTE]
>
>舊版[!DNL Experience Manager]能夠擷取XMP和縮圖，現在可以擷取所有媒體。

1. 將您的INDD檔案上傳到[!DNL Experience Manager Assets]。
1. 框架會透過SOAP (Simple Object Access Protocol)將命令指令碼傳送至[!DNL InDesign Server]。
這個命令指令碼會：

   * 擷取INDD檔案。
   * 執行[!DNL InDesign Server]命令：

      * 會擷取結構、文字及任何媒體檔案。
      * PDF和JPG轉譯會產生。
      * HTML和IDML轉譯會產生。

   * 將產生的檔案發佈回[!DNL Experience Manager Assets]。

   >[!NOTE]
   >
   >IDML是以XML為基礎的格式，可轉譯[!DNL InDesign]檔案的所有內容。 它使用[ZIP](https://techterms.com/definition/zip)壓縮儲存為壓縮封裝。 如需詳細資訊，請參閱[InDesign Interchange Formats INX與IDML](https://www.peachpit.com/promotions/adobe-creative-cloud-2024-release-books-ebooks-and-142536)。

   >[!CAUTION]
   >
   >如果未安裝或未設定[!DNL InDesign Server]，則您仍可上傳INDD檔案至[!DNL Experience Manager]。 不過，產生的轉譯僅限於PNG和JPEG。 您將無法產生HTML、`.idml`或頁面轉譯。

1. 在擷取和轉譯產生後：

   * 結構已復寫至`cq:Page` （轉譯型別）。
   * 擷取的文字和檔案儲存在[!DNL Experience Manager Assets]中。
   * 所有轉譯都儲存在資產本身的[!DNL Experience Manager Assets]中。

## 將[!DNL InDesign Server]與Experience Manager整合 {#integrating-the-indesign-server-with-aem}

若要整合[!DNL InDesign Server]以與[!DNL Experience Manager Assets]搭配使用，且在設定您的Proxy之後，您需要：

1. [安裝InDesign Server](#installing-the-indesign-server)。
1. 必要時，[設定Experience Manager Assets工作流程](#configuring-the-aem-assets-workflow)。
只有在預設值不適合您的執行個體時，才需要執行此操作。
1. 設定InDesign Server](#configuring-the-proxy-worker-for-indesign-server)的[Proxy背景工作。

### 安裝[!DNL InDesign Server] {#installing-the-indesign-server}

若要安裝並啟動[!DNL InDesign Server]以搭配[!DNL Experience Manager]使用：

1. 下載並安裝[!DNL InDesign Server]。

1. 如有必要，您可以自訂[!DNL InDesign Server]執行個體的設定。

1. 從命令列啟動伺服器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   這會啟動伺服器，並在連線埠8080上接聽SOAP外掛程式。 所有日誌訊息和輸出都直接寫入命令視窗中。

   >[!NOTE]
   >
   >如果要將輸出訊息儲存到檔案中，請使用重新導向；例如，在Windows下：
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 設定[!DNL Experience Manager Assets]工作流程 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets]已預先設定工作流程&#x200B;**[!UICONTROL DAM更新資產]**，其中包含數個[!DNL InDesign]專屬的處理步驟：

* [媒體提取](#media-extraction)
* [頁面提取](#page-extraction)

此工作流程設定了預設值，這些預設值可適用於您在各種作者執行個體上的設定（這是標準工作流程，因此[編輯工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)下提供了更多資訊）。 如果您使用預設值(包括SOAP連線埠)，則不需要進行設定。

安裝之後，將[!DNL InDesign]檔案上傳到[!DNL Experience Manager Assets] （透過任何常用方法）會觸發工作流程來處理資產並準備各種轉譯。 將INDD檔案上傳到[!DNL Experience Manager Assets]以測試您的設定，確認您看到由ID在`<*your_asset*>.indd/Renditions`下建立的不同轉譯

#### 媒體擷取 {#media-extraction}

此步驟控制從INDD檔案擷取媒體。

若要自訂，您可以編輯&#x200B;**[!UICONTROL 媒體擷取]**&#x200B;步驟的&#x200B;**[!UICONTROL 引數]**&#x200B;標籤。

![媒體擷取引數和指令碼路徑](assets/media_extraction_arguments_scripts.png)

媒體擷取引數和指令碼路徑

* **ExtendScript程式庫**：這是簡單的http get/post方法程式庫，其他指令碼需要它。

* **延伸指令碼**：您可以在此指定不同的指令碼組合。 如果您想要在[!DNL InDesign Server]上執行自己的指令碼，請將指令碼儲存在`/apps/settings/dam/indesign/scripts`。

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>請勿變更ExtendScript程式庫。 此程式庫提供與Sling通訊所需的HTTP功能。 此設定指定要傳送至[!DNL InDesign Server]在那裡使用的資料庫。

媒體擷取工作流程步驟執行的`ThumbnailExport.jsx`指令碼會產生JPG格式的縮圖轉譯。 此轉譯是由「處理縮圖」工作流程步驟用來產生[!DNL Experience Manager]所需的靜態轉譯。

您可以設定「處理縮圖」工作流程步驟，以產生不同大小的靜態轉譯。 請確定您未移除預設值，因為[!DNL Experience Manager Assets]介面需要這些預設值。 最後，「刪除影像預覽轉譯」工作流程步驟會移除JPG縮圖轉譯，因為已不再需要。

#### 頁面擷取 {#page-extraction}

這會從擷取的元素建立[!DNL Experience Manager]頁面。 擷取處理常式用於從轉譯(目前為HTML或IDML)中擷取資料。 然後，這些資料會用於使用「頁面產生器」建立頁面。

若要自訂，您可以編輯「頁 **[!UICONTROL 面擷取]** 」步驟 **[!UICONTROL 的「引]** 數」標籤。

![chlimage_1-96](assets/chlimage_1-289.png)

* **頁面擷取處理常式**：從快顯清單中選取您要使用的處理常式。 擷取處理常式會針對相關`RenditionPicker`選擇的特定轉譯進行操作（請參閱`ExtractionHandler` API）。 在標準[!DNL Experience Manager]安裝中，可以使用下列專案：
   * IDML匯出擷取控制代碼：在MediaExtract步驟中產生的`IDML`轉譯上操作。

* **頁面名稱**：指定您要指派給結果頁面的名稱。 如果保留為空白，則名稱為「page」（如果「page」已存在，則為衍生專案）。

* **頁面標題**：指定您要指派給結果頁面的標題。

* **頁面根路徑**：結果頁面的根位置路徑。 如果保留為空白，則會使用儲存資產轉譯的節點。

* **頁面範本**：產生結果頁面時要使用的範本。

* **頁面設計**：產生結果頁面時要使用的頁面設計。

### 設定[!DNL InDesign Server]的Proxy背景工作 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>Worker位於Proxy執行個體上。

1. 在[工具]主控台中，展開左側窗格中的&#x200B;**[!UICONTROL 雲端服務組態]**。 然後展開&#x200B;**[!UICONTROL 雲端Proxy設定]**。

1. 連按兩下 **[!UICONTROL IDS工作器]** ，以開啟以進行設定。

1. 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟設定對話方塊並定義必要的設定：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS集區**
用來與[!DNL InDesign Server]通訊的SOAP端點。 您可以新增、移除及訂購必要專案。

1. 按一下「確定」以儲存。

### 設定Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果[!DNL InDesign Server]和[!DNL Experience Manager]位於不同的主機上，或這些應用程式之一或兩者皆未在預設連線埠上運作，請設定[!UICONTROL Day CQ Link Externalizer]以設定[!DNL InDesign Server]的主機名稱、連線埠和內容路徑。

1. 在`https://[aem_server]:[port]/system/console/configMgr`存取Web主控台。
1. 找出組態&#x200B;**[!UICONTROL Day CQ Link Externalizer]**。 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟。
1. 連結外部化程式設定可協助建立[!DNL Experience Manager]部署和[!DNL InDesign Server]的絕對URL。 使用&#x200B;**[!UICONTROL 網域]**&#x200B;欄位來指定[!DNL Adobe InDesign Server]的主機名稱。 按一下「**儲存**」。

   在絕對URL中，使用`localhost`作為本機（作者）執行個體的主機名稱，以及發佈執行個體的主機名稱或IP位址，如下圖所示。

   ![連結外部器設定](assets/link-externalizer-config.png)

### 為[!DNL InDesign Server]啟用平行工作處理 {#enabling-parallel-job-processing-for-indesign-server}

您現在可以啟用ID的平行作業處理。 決定[!DNL InDesign Server]可以處理的平行工作數目上限(`x`)：

* 在單一多處理器電腦上，[!DNL InDesign Server]可以處理的平行工作數目上限(`x`)比執行ID的處理器數目少一個。
* 當您在多部機器上執行ID時，您必須計算可用的處理器總數（即所有機器上的處理器），然後減去機器總數。

若要設定平行ID作業的數目：

1. 開啟Felix主控台的&#x200B;**[!UICONTROL 組態]**&#x200B;標籤；例如： `https://[aem_server]:[port]/system/console/configMgr`。

1. 選取`Apache Sling Job Queue Configuration`下的IDS處理佇列。

1. 設定：

   * **型別** - `Parallel`
   * **最大平行工作** - `<*x*>` （如上計算）

1. 儲存這些變更。
1. 若要啟用Adobe CS6和更新版本的多工作階段支援，請核取`com.day.cq.dam.ids.impl.IDSJobProcessor.name`設定下的`enable.multisession.name`核取方塊。
1. 將SOAP端點新增至IDS Worker設定](#configuring-the-proxy-worker-for-indesign-server)，以建立`x` IDS Worker的[集區。

   如果有多部電腦執行[!DNL InDesign Server]，請為每部電腦新增SOAP端點（每部電腦的處理器數目–1）。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>使用背景工作集區時，您可以啟用IDS背景工作區的封鎖清單。
>
>若要這麼做，請在`com.day.cq.dam.ids.impl.IDSJobProcessor.name`設定下啟用&#x200B;**[!UICONTROL enable.retry.name]**&#x200B;核取方塊，以啟用IDS工作重試。
>
>此外，在`com.day.cq.dam.ids.impl.IDSPoolImpl.name`設定下，為`max.errors.to.blacklist`引數設定正值，該值決定在從工作處理常式清單中禁止ID之前的工作重試次數。
>
>根據預設，在可設定的(`retry.interval.to.whitelist.name`)時間（以分鐘為單位）之後，會重新驗證IDS背景工作。 如果線上上找到背景工作，就會從封鎖清單中移除背景工作。

## 啟用[!DNL InDesign Server] 10.0或更新版本的支援 {#enabling-support-for-indesign-server-or-later}

若為[!DNL InDesign Server] 10.0或更新版本，請執行下列步驟以啟用多工作階段支援。

1. 從您的[!DNL Experience Manager Assets]執行個體`https://[aem_server]:[port]/system/console/configMgr`開啟Configuration Manager。
1. 編輯組態`com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. 選取&#x200B;**[!UICONTROL ids.cc.enable]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL 儲存]**。

>[!NOTE]
>
>若要與[!DNL Experience Manager Assets]整合[!DNL InDesign Server]，請使用多核心處理器，因為單核心系統不支援整合所需的工作階段支援功能。

## 設定[!DNL Experience Manager]認證 {#configure-aem-credentials}

您可以變更從[!DNL Experience Manager]部署存取[!DNL InDesign Server]的預設系統管理員認證（使用者名稱和密碼），而不中斷與[!DNL InDesign Server]的整合。

1. 前往 `/etc/cloudservices/proxy.html`。
1. 在對話方塊中，指定新的使用者名稱和密碼。
1. 儲存認證。

>[!MORELIKETHIS]
>
>* [關於Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
