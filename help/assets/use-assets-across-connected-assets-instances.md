---
title: 在Adobe Experience Manager Sites製作工作流程中，使用連結的資產來共用DAM資產
description: 在其他Experience Manager網站部署中建立網頁時，請使用遠端Adobe Experience Manager Assets部署中的可用資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8a014887f395c5ade0affcb3c199e090af263bdc

---


# 使用「連線的資產」在AEM Sites中共用DAM資產 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企業中，建立網站所需的基礎架構可能會分散。 建立這些網站的網站建立功能和數位資產有時可能會駐留在不同的部署中。 一些原因可能是部署分散各地，需要協同工作；收購導致母公司希望整合的異質基礎設施；這種規模的增長導致資產管理需要專門執行。

AEM Sites提供建立網頁的功能，而AEM Assets是數位資產管理(DAM)系統，可為網站提供必要的資產。 AEM現在整合AEM Sites和AEM Assets，以支援上述使用案例。

## 連線資產概觀 {#overview-of-connected-assets}

在「頁面編輯器」中編輯頁面時，作者可以從不同的AEM Assets部署順暢地搜尋、瀏覽和內嵌資產。 若要讓AEM管理員執行AEM Sites的本機部署與AEM Assets的不同（遠端）部署的一次性整合。

對於網站作者，遠端資產可做為唯讀本機資產。 此功能可支援順暢搜尋並一次使用數個遠端資產。 若要讓許多遠端資產在單次部署時可供使用，請考慮大量移轉資產。 請參閱 [資產移轉指南](/help/assets/assets-migration-guide.md)。

### 先決條件和支援的部署 {#prerequisites}

在您使用或設定此功能之前，請確定：

* 使用者是每個部署中適當使用者群組的一部分。
* 對於Adobe Experience manager部署類型，符合其中一項支援的標準。 AEM 6.5 Assets可與AEM搭配使用，做為雲端服務。 如需詳細資訊，請 [參閱AEM中的「Connected Assets」（連線資產）功能(Cloud Service)](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | AEM Sites 雲端服務 | AMS上的AEM 6.5網站 | AEM 6.5內部部署網站 |
   |---|---|---|---|
   | **AEM Assets 雲端服務** | 支援 | 支援 | 支援 |
   | **AEM 6.5 Assets on AMS** | 不支援 | 支援 | 支援 |
   | **AEM 6.5內部部署資產** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者可在Content Finder中搜尋影像和下列類型的檔案，並在「頁面編輯器」中使用搜尋的資產。 可將檔案新增至元 `Download` 件，並將影像新增至元 `Image` 件。 作者也可以在任何可延伸預設或元件的自訂AEM元件中新增遠 `Download` 端資 `Image` 產。 如需支援格式的清單，請參閱「連 [接的資產」支援格式](assets-formats.md#supported-document-formats)。

### Users and groups involved {#users-and-groups-involved}

以下說明配置和使用功能及其相應用戶組時涉及的各種角色。 本機範圍用於作者建立網頁的使用案例。 遠端範圍用於托管所需資產的DAM部署。 「站點」作者會讀取這些遠程資產。

| 角色 | 範圍 | 使用者群組 | 逐步執行中的使用者名稱 | 需求 |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM Sites Administrator | 本機 | AEM管理員 | `admin` | 設定AEM，設定與遠端資產部署的整合。 |
| DAM使用者 | 本機 | 作者 | `ksaner` | 用於在中查看和複製提取的資產 `/content/DAM/connectedassets/`。 |
| AEM Sites作者 | 本機 | 作者（可在遠端DAM上存取讀取權，並可在本機網站上存取作者） | `ksaner` | 一般使用者是網站作者，他們使用此項整合來提升內容速度。 作者使用Content Finder和本機網頁中的必要影像，在遠端DAM中搜尋及瀏覽資產。 使用 `ksaner` DAM使用者的認證。 |
| AEM Assets管理員 | 遠端 | AEM管理員 | `admin` 在遠端AEM上 | 設定跨原始資源共用(CORS)。 |
| DAM使用者 | 遠端 | 作者 | `ksaner` 在遠端AEM上 | 在遠端AEM部署上編寫角色。 使用內容搜尋器，在「已連線資產」中搜尋及瀏覽資產。 |
| DAM配銷商（技術使用者） | 遠端 | 封裝建立工具和網站作者 | `ksaner` 在遠端AEM上 | AEM本端伺服器（而非網站作者角色）會使用此位於遠端部署的使用者來擷取遠端資產，代表網站作者。 此角色與上述兩個角色不同， `ksaner` 且屬於不同的使用者群組。 |

## 設定網站與資產部署之間的連線 {#configure-a-connection-between-sites-and-assets-deployments}

AEM管理員可以建立此整合。 在建立後，使用它所需的權限會透過在網站部署和DAM部署上定義的使用者群組來建立。

要配置「已連接資產」和「本地站點」連接，請遵循以下步驟。

1. 存取現有的AEM Sites部署，或使用下列命令建立部署：

   1. 在JAR檔案的檔案夾中，在終端上執行下列命令以建立每個AEM伺服器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 幾分鐘後，AEM伺服器就會成功啟動。 請將此AEM Sites部署視為網頁製作的本機電腦，例如 `https://[local_sites]:4502`。

1. 請確定AEM Sites部署和AMS上的AEM Assets部署上都有具有本機範圍的使用者和角色。 建立資產部署的技術使用者，並新增至相關使用者和群組中 [提及的使用者群組](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)。

1. 請在存取本機AEM Sites部署 `https://[local_sites]:4502`。 按一 **[!UICONTROL 下「工具]** >資 **[!UICONTROL 產]** >連線 **[!UICONTROL 的資產設定]** 」，並提供下列值：

   1. AEM Assets位置為 `https://[assets_servername_ams]:[port]`。
   1. DAM配銷商的認證（技術使用者）。
   1. 在「 **[!UICONTROL 裝載點]** 」欄位中，輸入AEM擷取資產的本機AEM路徑。 例如， `remoteassets` folder。

   1. 根據您的網路調 **[!UICONTROL 整原始二進位傳輸優化閾值]** 。 大小大於此臨界值的資產轉譯會非同步傳送。
   1. 如果 ****&#x200B;您使用資料存放區來儲存資產，而「資料存放區」是兩個AEM部署之間的共用儲存區，請選取「與已連接資產共用的資料存放區」。 在這種情況下，閾值限制並不重要，因為實際資產二進位檔案駐留在資料儲存上，並且不會傳輸。
   ![連接資產的典型配置](assets/connected-assets-typical-config.png)

   *圖：連接資產的典型配置*

1. 當資產已處理且已擷取轉譯時，請停用工作流程啟動器。 調整本機(AEM Sites)部署上的啟動程式設定，排除 `connectedassets` 擷取遠端資產的檔案夾。

   1. 在AEM Sites部署中，按一下「工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流程]****[!UICONTROL >]** Rachilers」。

   1. 使用工作流程搜尋啟動程 **[!UICONTROL 式：DAM更新資產]****[!UICONTROL 和DAM中繼資料回寫]**。

   1. 選擇工作流啟動程式，然後按一下 **[!UICONTROL 操作欄上]** 「屬性」(Properties)。

   1. 在「屬性」嚮導中，將 **[!UICONTROL Path]** 欄位更改為以下映射，以更新其規則運算式以排除連接的 **[!UICONTROL 資產]**。
   | 之前 | 之後 |
   |---|---|
   | /content/dam(/(?!/subassets)。*/)轉譯／原始 | /content/dam(/(?!/subassets)(?!connectedassets)。*/)轉譯／原始 |
   | /content/dam(/.*/)轉譯／原始 | /content/dam(/(?!connectedassets)。*/)轉譯／原始 |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/(?!connectedassets)。*/)jcr:content/metadata |

   >[!NOTE]
   >
   >當作者擷取資產時，會擷取遠端AEM部署上可用的所有轉譯。 如果您想要建立已擷取資產的更多轉譯，請略過此設定步驟。 「DAM更新資產」工作流程會被觸發並建立更多轉譯。 這些轉譯僅在本機網站部署中可用，在遠端DAM部署中則不可用。

1. 將AEM Sites例項新增為遠端AEM Assets **[!UICONTROL CORS組態上的]** 「允許來源」。

   1. 使用管理員憑據登錄。 搜尋跨原點。 存取 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web主控台]**。

   1. 若要建立AEM Sites例項的CORS設定，請按一下 ![Adobe Granite Cross-Origin Resource Sharing Policy](assets/aem_assets_add_icon.png) 旁的aem_assets_add_icon **[!UICONTROL 圖示]**。

   1. 在「允 **[!UICONTROL 許來源]**」欄位中，輸入本機網站的URL，即 `https://[local_sites]:[port]`。 保存配置。

## 使用遠端資產 {#use-remote-assets}

網站作者使用Content Finder連線至DAM例項。 作者可以瀏覽、搜尋和拖曳元件中的遠端資產。 若要向遠端DAM驗證，請讓管理員提供的DAM使用者認證保持便利。

作者可以在單一網頁中使用本機DAM和遠端DAM例項兩者上的可用資產。 使用內容搜尋器可在搜尋本機DAM或搜尋遠端DAM之間切換。

只有那些具有與本地Sites實例相同分類層次結構的完全對應標籤的遠程資產的標籤才會被讀取。 會捨棄任何其他標籤。 作者可以使用遠端AEM部署上所有顯示的標籤來搜尋遠端資產，因為AEM提供全文搜尋。

### 使用的逐步介紹 {#walk-through-of-usage}

使用上述設定來嘗試編寫體驗，以瞭解功能的運作方式。 在遠端DAM部署中使用您選擇的檔案或影像。

1. 從AEM工作區存取「資產 **[!UICONTROL >檔案」，導覽至遠端部]** 署的「資 **[!UICONTROL 產]** 」UI。 或者，在瀏 `https://[assets_servername_ams]:[port]/assets.html/content/dam` 覽器中存取。 上傳您選擇的資產。
1. 在Sites實例的右上角的Profile Activator中，按一下Impersonate **[!UICONTROL as]**。 提供 `ksaner` 為用戶名，選擇提供的選項，然後按一下「 **[!UICONTROL 確定」]**。
1. 在「網站 **[!UICONTROL >]** We.Retail **[!UICONTROL >]** us **[!UICONTROL >]** en.Sites」開啟「We.Retail」網站頁 ****&#x200B;面。 編輯頁面。 或者，在瀏 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 覽器中存取以編輯頁面。

   按一 **[!UICONTROL 下頁面左上角]** 「切換側面板」。

1. 開啟「資產」標籤，然後按一 **[!UICONTROL 下「登入已連線的資產」]**。
1. 提供憑證- `ksaner` 以使用者名稱 `password` 和密碼。 此使用者對這兩種AEM部署都具有編寫權限。
1. 搜尋您新增至DAM的資產。 遠端資產會顯示在左側面板中。 篩選影像或檔案，並進一步篩選支援的檔案類型。 拖曳元件上的影 `Image` 像和元件上的文 `Download` 件。

   擷取的資產在本機AEM Sites部署上為唯讀。 您仍可以使用AEM Sites元件提供的選項來編輯擷取的資產。 依元件編輯是無損的。

   ![在遠端DAM上搜尋資產時，篩選檔案類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端DAM上搜尋資產時，篩選檔案類型和影像的選項*

1. 如果資產以非同步方式擷取且任何擷取工作失敗，網站作者會收到通知。 在編寫時，甚至在編寫之後，作者可以在非同步作業用戶介面中查看有關讀取任務和錯 [誤的詳細信](/help/assets/asynchronous-jobs.md) 息。

   ![關於在背景發生之資產的非同步擷取通知。](assets/assets_async_transfer_fails.png)

   *圖：關於在背景發生之資產的非同步擷取通知。*

1. 發佈頁面時，AEM會顯示頁面中使用的資產完整清單。 請確定發佈時已成功擷取遠端資產。 要檢查每個已獲取資產的狀態，請參閱非 [同步作業](/help/assets/asynchronous-jobs.md) 用戶介面。

   >[!NOTE]
   >
   >即使未擷取一或多個遠端資產，也會發佈頁面。 使用遠端資產的元件會發佈為空白。 AEM通知區域會針對非同步作業頁面中顯示的錯誤顯示通知。

>[!CAUTION]
>
>一旦在網頁中使用，擷取的遠端資產就可供任何有權存取儲存擷取資產之本機資料夾的人搜尋及使用(在上述`connectedassets` 逐步存取中)。 這些資產也可供搜尋，並可透過 [!UICONTROL Content Finder在本機儲存庫中顯示]。

擷取的資產可當成任何其他本機資產使用，但相關聯的中繼資料無法編輯除外。

## 限制 {#limitations}

**權限與管理資產**

* 本機資產不會與遠端部署上的原始資產同步。 對DAM部署的任何編輯、刪除或撤銷權限都不會傳播到下游。
* 本機資產為唯讀副本。 AEM元件會對資產進行非破壞性編輯。 不允許進行其他編輯。
* 本機擷取的資產僅適用於製作用途。 無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和所列的檔案格式。 不支援動態媒體資產、內容片段和體驗片段。
* 中繼資料結構未擷取。
* 所有「網站作者」都對擷取的副本具有讀取權限，即使他們沒有遠端DAM部署的存取權。
* 無API支援可自訂整合。
* 此功能支援順暢搜尋和使用遠端資產。 若要讓許多遠端資產在單次部署時可供使用，請考慮移轉資產。 請參閱 [資產移轉指南](assets-migration-guide.md)。
* 無法將遠端資產當做頁面屬性使用者介面上的頁 [!UICONTROL 面縮圖] 。 您可以按一下「選取影像」，在「縮圖」的「頁 [!UICONTROL 面屬性] 」使用者介面中設定網頁的縮圖 。

**設定和授權**

* 支援在AMS上部署AEM Assets。
* AEM Sites一次可以連線至單一AEM Assets存放庫。
* AEM Assets的授權，可當成遠端儲存庫使用。
* AEM Sites的一或多份授權可做為本機製作部署。

**使用狀況**

* 只支援搜尋遠端資產並拖曳本機頁面上的遠端資產來製作內容的功能。
* 5秒後擷取作業逾時。 作者在擷取資產時可能遇到問題，例如是否有網路問題。 作者可從 [!UICONTROL Content Finder拖曳遠端資產至頁面編輯器] ，以 [!UICONTROL 重新嘗試]。
* 您可以對擷取的資產進行非破壞性的簡單編輯，以及透過AEM `Image` 元件支援的編輯。 資產為唯讀。

## 疑難排解問題 {#troubleshoot}

請依照下列步驟，疑難排解常見錯誤案例：

* 如果您無法從Content Finder搜尋遠端資產，請重新檢查並確定所需的角色和權限已就緒。
* 從遠端Dam擷取的資產可能因下列原因無法發佈至網頁：它不存在於遠端；缺乏適當的權限來擷取；網路故障。 確保資產未從遠端DAM移除，或權限未變更；確保符合適當的先決條件；重新嘗試將資產新增至頁面並重新發佈。 檢查非 [同步作業清單](/help/assets/asynchronous-jobs.md) ，以找出資產擷取錯誤。
