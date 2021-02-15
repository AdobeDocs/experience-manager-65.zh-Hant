---
title: 使用「連線資產」在 中共用 DAM 資產 [!DNL Sites]
description: 使用遠程 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 部署上可用的資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d05dc3af0a885e51758194783e773695086d7956
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 40%

---


# 使用「連線資產」在 中共用 DAM 資產 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。一個原因可能是現有部署在地理位置分散，需要協同工作。 另一個原因可能是收購導致母公司希望共同使用的異質基礎設施。

使用者可在[!DNL Experience Manager Sites]中建立網頁。 [!DNL Experience Manager Assets] 是數位資產管理(DAM)系統，可為網站提供所需資產。[!DNL Experience Manager] 現在可透過整合和來支援上述使 [!DNL Sites] 用案例 [!DNL Assets]。

## 連線資產概觀 {#overview-of-connected-assets}

當在[!UICONTROL 頁面編輯器]中編輯頁面作為目標目的地時，作者可以順暢地搜尋、瀏覽及內嵌來自不同[!DNL Assets]部署（作為資產來源）的資產。 管理員建立具有[!DNL Sites]功能的[!DNL Experience Manager]部署與具有[!DNL Assets]功能的[!DNL Experience Manager]部署的一次性整合。

對於[!DNL Sites]作者，遠端資產可做為唯讀本機資產。 此功能可支援順暢的搜尋作業，並允許一次使用數個遠端資產。若要在一次執行的[!DNL Sites]部署中提供許多遠端資產，請考慮大量移轉資產。 請參閱[Experience Manager資產遷移指南](/help/assets/assets-migration-guide.md)。

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 使用者是每個部署中適當使用者群組的一部分。
* 對於[!DNL Adobe Experience Manager]部署類型，符合其中一個支援的標準。 [!DNL Experience Manager] 6.5可 [!DNL Assets] 搭配雲 [!DNL Experience Manager] 端服務使用。如需此功能在[!DNL Experience Manager as a Cloud Service]中運作的詳細資訊，請參閱Experience Manager中的[ Connected Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | [!DNL Sites] 雲端服務 | [!DNL Experience Manager] 6.5  [!DNL Sites] on AMS. | [!DNL Experience Manager] 6.5內 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支援 | 支援 | 支援 |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] on AMS.** | 支援 | 支援 | 支援 |
   | **[!DNL Experience Manager]6.5內 [!DNL Assets] 部部署** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者在Content Finder中搜尋影像和下列類型的檔案，並在「頁面編輯器」中使用搜尋的資產。 文檔將添加到`Download`元件中，影像將添加到`Image`元件中。 作者也會將遠端資產新增至任何可擴充預設`Download`或`Image`元件的自訂[!DNL Experience Manager]元件。 支援的格式包括：

* **影像格式**:Image元件支援 [的](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 格式。[!DNL Dynamic Media] 不支援影像。
* **檔案格式**:請參閱支 [援的檔案格式](assets-formats.md#supported-document-formats)。

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定及使用功能以及其相對應的使用者群組時，相關的各種角色。本機範圍用於作者建立網頁的使用案例。 遠端範圍適用於託管所需資產的 DAM 部署。[!DNL Sites]作者會讀取這些遠程資產。

| 角色 | 範圍 | 使用者群組 | 逐步說明中的使用者名稱 | 需求 |
|---|---|---|---|---|
| [!DNL Sites] 管理員 | 本機 | [!DNL Experience Manager] `administrators` | `admin` | 設定[!DNL Experience Manager]並配置與遠程[!DNL Assets]部署的整合。 |
| DAM 使用者 | 本機 | `Authors` | `ksaner` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| [!DNL Sites] 作者 | 本機 | <ul><li>`Authors` (在遠端DAM上具有讀取存取權，在本機上具有作者存取權 [!DNL Sites]) </li> <li>`dam-users` 本地  [!DNL Sites]</li></ul> | `ksaner` | 使用者為[!DNL Sites]作者，他們使用此整合來改善其內容速度。 作者使用[!UICONTROL Content Finder]在遠端DAM中搜尋及瀏覽資產，並使用本機網頁中的必要影像。 已採用 `ksaner` DAM 使用者的認證。 |
| [!DNL Assets] 管理員 | 遠端 | [!DNL Experience Manager] `administrators` | `admin` 遠程  [!DNL Experience Manager] | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | `Authors` | `ksaner` 遠程  [!DNL Experience Manager] | 在遠程[!DNL Experience Manager]部署上的作者角色。 使用[!UICONTROL 內容搜尋器]搜尋及瀏覽已連線資產中的資產。 |
| DAM 經銷商 (技術使用者) | 遠端 | [!DNL Sites] `Authors` | `ksaner` 遠程  [!DNL Experience Manager] | [!DNL Experience Manager]本機伺服器（非[!DNL Sites]作者角色）會代表[!DNL Sites]作者使用此位於遠端部署的使用者來擷取遠端資產。 此角色與上述的兩個 `ksaner` 角色不一樣，而且屬於不同的使用者群組。 |

## 配置[!DNL Sites]和[!DNL Assets]部署{#configure-a-connection-between-sites-and-assets-deployments}之間的連接

[!DNL Experience Manager]管理員可以建立此整合。 建立後，使用權限所需的權限會透過使用者群組建立。 用戶組在[!DNL Sites]部署和DAM部署上定義。

要配置「已連接資產」和「本地[!DNL Sites]連接」，請執行以下步驟：

1. 使用以下命令訪問現有的[!DNL Sites]部署或建立部署：

   1. 在JAR檔案的資料夾中，在終端上執行以下命令以建立每個[!DNL Experience Manager]伺服器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 幾分鐘後，[!DNL Experience Manager]伺服器成功啟動。 將此[!DNL Sites]部署視為網頁製作的本機電腦，例如`https://[local_sites]:4502`。

1. 確保[!DNL Sites]部署和[!DNL Assets]部署AMS上存在具有本地範圍的用戶和組。 在[!DNL Assets]部署上建立技術用戶，並添加到[涉及的用戶和組中提及的用戶組](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)。

1. 訪問`https://[local_sites]:4502`的本地[!DNL Sites]部署。 按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. [!DNL Assets] 位置為 `https://[assets_servername_ams]:[port]`。
   1. DAM 經銷商 (技術使用者) 的認證。
   1. 在&#x200B;**[!UICONTROL 裝載點]**&#x200B;欄位中，輸入[!DNL Experience Manager]讀取資產的本地[!DNL Experience Manager]路徑。 例如，`remoteassets` 資料夾。
   1. 根據您的網路調整&#x200B;**[!UICONTROL 原始二進位傳輸最佳化臨界值]**。大於此臨界值的資產轉譯項目會以非同步方式傳送。
   1. 如果您是使用資料存放區來儲存資產，且「資料存放區」是兩個 部署之間的共用儲存空間，請選取&#x200B;**[!UICONTROL 「與連線資產共用的資料存放區」]**。這種情況下，臨界值限制並不重要，因為實際的資產二進位檔位於資料存放區，而且不會轉移。

   ![連線資產的典型設定](assets/connected-assets-typical-config.png)

   *圖：連線資產的典型設定.*

1. 資產處理完畢且轉譯完成擷取後，請停用工作流程啟動器。調整本地([!DNL Sites])部署上的啟動程式配置，以排除擷取遠端資產的`connectedassets`資料夾。

   1. 在[!DNL Sites]部署中，按一下&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 啟動器]**。

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. 在[!UICONTROL 屬性]精靈中，將&#x200B;**[!UICONTROL 路徑]**&#x200B;欄位變更為下列對應，以更新其規則運算式，排除已連線資產&#x200B;]**的裝載點。**[!UICONTROL 

   | 變更前 | 變更後 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作者擷取資產時，會擷取遠端 部署上可用的所有轉譯項目。若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。[!UICONTROL DAM Update Asset]工作流程會觸發並建立更多轉譯。 這些轉譯僅在本機[!DNL Sites]部署中可用，在遠端DAM部署中則不可用。

1. 將[!DNL Sites]部署新增為遠端[!DNL Assets'] CORS組態上的&#x200B;**[!UICONTROL 允許來源]**。

   1. 使用管理員憑證登入。 搜尋 `Cross-Origin`. 存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web 主控台」]**。

   1. 若要建立[!DNL Sites]部署的CORS設定，請按一下&#x200B;**[!UICONTROL Adobe Granite跨原始資源共用政策]**&#x200B;旁邊的新增選項![資產新增圖示](assets/do-not-localize/assets_add_icon.png)。

   1. 在&#x200B;**[!UICONTROL 允許的來源]**&#x200B;欄位中，輸入本機[!DNL Sites]的URL，即`https://[local_sites]:[port]`。 儲存設定。

## 使用遠端資產 {#use-remote-assets}

網站作者使用Content Finder連線至DAM部署。 作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要向遠端 DAM 驗證，請備妥管理員提供的 DAM 使用者認證。

作者可在單一網頁中使用本機DAM和遠端DAM部署上的可用資產。 使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

只有那些具有與本地[!DNL Sites]部署中相同的分類層次具有完全對應標籤的遠程資產的標籤被讀取。 其他所有標籤會一概捨棄。作者可以使用遠端[!DNL Experience Manager]部署上的所有標籤來搜尋遠端資產，因為它提供全文搜尋功能。

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. 從[!DNL Experience Manager]工作區訪問&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**，導航到遠程部署上的[!DNL Assets]介面。 或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。
1. 在[!DNL Sites]部署中，在右上角的描述檔激活器中，按一下&#x200B;**[!UICONTROL Impersonate as]**。 輸入 `ksaner` 作為使用者名稱，選取畫面上提供的選項，然後按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 在&#x200B;**[!UICONTROL 「Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL tw]** > **[!UICONTROL zh」]**&#x200B;開啟「We.Retail」網頁。編輯頁面。或者，您也可以在瀏覽器中存取 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`，進而編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. 開啟[!UICONTROL Assets]標籤，然後按一下&#x200B;**[!UICONTROL 登入已連線的資產]**。
1. 提供憑證 `ksaner` 作為使用者名稱，且以 `password` 作為密碼。此用戶對[!DNL Experience Manager]部署都具有編寫權限。
1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   在本地[!DNL Sites]部署中，讀取的資產是只讀的。 您仍然可以使用[!DNL Sites]元件提供的選項來編輯擷取的資產。 由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項.*

1. 如果資產是以非同步方式擷取，一有擷取任務執行失敗，網站作者就會收到通知。編寫過程中或甚至在完成編寫之後，作者都能在[非同步工作](/help/sites-administering/asynchronous-jobs.md)使用者介面中查看擷取任務和錯誤的詳細資訊。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：背景中非同步擷取資產作業的相關通知。*

1. 發佈頁面時，[!DNL Experience Manager]會顯示頁面上使用之資產的完整清單。 請確認發佈時，系統已成功擷取遠端資產。若要檢查所擷取資產的個別狀態，請參閱[非同步工作](/help/sites-administering/asynchronous-jobs.md)使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未成功擷取，頁面還是會照常發佈。使用遠端資產的元件會以空白形式發佈。[!DNL Experience Manager]通知區域會針對非同步作業頁面中顯示的錯誤顯示通知。

>[!CAUTION]
>
>一旦在網頁中使用，擷取的遠端資產就可供任何有權存取本機資料夾的人搜尋及使用。 擷取的資產會儲存在本機資料夾中（位於上述逐步連結中的`connectedassets`）。 這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

## 限制和最佳做法{#tips-and-limitations}

* 若要取得資產使用情況的深入資訊，請在[!DNL Sites]例項上設定[Asset Insight](/help/assets/asset-insights.md)功能。

### 權限與資產管理{#permissions-and-managing-assets}

* 本機資產不會與遠端部署上的原始資產同步。對 DAM 部署所做的任何編輯、刪除或撤銷權限操作都不會傳播到下游。
* 本機資產為唯讀副本。[!DNL Experience Manager] 元件會對資產執行非破壞性的編輯作業。不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和列出的文件格式。[!DNL Dynamic Media] 不支援資產、內容片段和體驗片段。
* [!DNL Experience Manager] 不會擷取中繼資料結構。這表示可能無法顯示所有擷取的中繼資料。 如果模式單獨更新，則顯示所有屬性。
* 所有[!DNL Sites]作者都對讀取的副本具有讀取權限，即使作者無法訪問遠程DAM部署。
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。請參閱[資產移轉指南](assets-migration-guide.md)。
* 在[!UICONTROL 頁面屬性]使用者介面上，無法將遠端資產當做頁面縮圖使用。 您可以按一下「選擇影像」，從「[!UICONTROL 縮圖]」使用者介面的「頁面屬性」中設定網頁的縮圖。

### 設定和授權 {#setup-licensing}

* [!DNL Assets] 支援在 [!DNL Adobe Managed Services] 上部署。
* [!DNL Sites] 一次可以連接到 [!DNL Assets] 單個儲存庫。
* [!DNL Assets]的許可證，用作遠程資料庫。
* [!DNL Sites]的一或多份授權可做為本機製作部署。

### 使用狀況 {#usage}

* 使用者可在製作時搜尋遠端資產，並拖曳這些資產至本機頁面。 不支援其他功能。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。作者可以重新嘗試，將遠端資產從[!UICONTROL Content Finder]拖曳至[!UICONTROL 頁面編輯器]。
* 您可以對擷取的資產執行非破壞性的簡單編輯作業，也能執行透過 `Image` 元件支援的編輯工作。資產僅供唯讀。
* 唯一可重新擷取資產的方法，就是將資產拖曳至頁面上。 沒有API支援或其他方法可重新擷取資產以進行更新。
* 如果資產從DAM中終止運作，則這些資產會繼續在[!DNL Sites]頁面上使用。

## 疑難排解問題 {#troubleshoot}

要排除常見錯誤情形的故障，請執行以下步驟：

* 如果您無法從[!UICONTROL Content Finder]搜尋遠端資產，請確定已有必要的角色和權限。
* 從遠端Dam擷取的資產可能因一個或多個原因無法發佈在網頁上。 它不存在於遠程伺服器上，缺少獲取它的適當權限，或者網路故障可能是原因。 確保資產未從遠端DAM移除。 請確定已有適當的權限，並符合先決條件。 重新嘗試將資產新增至頁面並重新發佈。 檢查[非同步工作清單](/help/sites-administering/asynchronous-jobs.md)，找出資產擷取作業的錯誤。
* 如果您無法從本機[!DNL Sites]部署存取遠端DAM部署，請確定允許跨網站Cookie。 如果跨網站Cookie遭到封鎖，[!DNL Experience Manager]的兩個部署可能無法驗證。 例如，Incognito模式下的[!DNL Google Chrome]可能會阻止第三方Cookie。 若要允許[!DNL Chrome]瀏覽器中的Cookie，請按一下位址列中的「eye」圖示，導覽至「網站無法運作>已封鎖」，選取「遠端DAM URL」，並允許登入Token Cookie。 或者，請參閱[如何啟用協力廠商Cookie的說明。](https://support.google.com/chrome/answer/95647)

   ![Chrome在Incognito模式中發生Cookie錯誤](assets/chrome-cookies-incognito-dialog.png)
