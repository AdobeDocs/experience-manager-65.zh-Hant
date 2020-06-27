---
title: Use Connected Assets to share DAM assets in [!DNL Adobe Experience Manager Sites] authoring workflow.
description: 使用遠程部署中可用 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 的資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 51%

---


# 使用「連線資產」在 中共用 DAM 資產 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。一個原因可能是現有部署在地理位置分散，需要協同工作。 另一個原因可能是收購導致母公司希望共同使用的異質基礎設施。

使用者可在中建立網頁 [!DNL Experience Manager Sites]。 [!DNL Experience Manager Assets] 是數位資產管理(DAM)系統，可為網站提供所需資產。 [!DNL Experience Manager] 現在整合和支援上述使用 [!DNL Sites] 案例 [!DNL Assets]。

## 連線資產概觀 {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. 管理員會建立部署的一次性整合， [!DNL Sites] 並使用不同的（遠端）部署 [!DNL Assets]。

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. 此功能可支援順暢的搜尋作業，並允許一次使用數個遠端資產。To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk. 請參 [閱Experience Manager資產遷移指南](/help/assets/assets-migration-guide.md)。

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 每個部署中，使用者都是適當使用者群組的成員。
* 對於Adobe Experience Manager部署類型，符合其中一個支援的標準。 [!DNL Experience Manager] 6.5可 [!DNL Assets] 搭配雲 [!DNL Experience Manager] 端服務使用。 如需詳細資訊，請 [參閱Experience Manager中的「Connected Assets」（連接資產）功能，即雲端服務](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | [!DNL Sites] 雲端服務 | [!DNL Experience Manager] 6.5 [!DNL Sites] on AMS. | [!DNL Experience Manager] 6.5內 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]雲端服務&#x200B;** | 支援 | 支援 | 支援 |
   | **[!DNL Experience Manager]6.5[!DNL Assets]on AMS.** | 支援 | 支援 | 支援 |
   | **[!DNL Experience Manager]6.5內[!DNL Assets]部部署&#x200B;** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者可在「內容尋找器」中搜尋影像和下列類型的文件，並在「頁面編輯器」中使用找到的資產。文件可新增至 `Download` 元件，且影像可新增至 `Image` 元件。Authors can also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. 支援的格式包括：

* **影像格式**: Image元件支 [持的格式](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/components/image.translate.html) 。 [!DNL Dynamic Media] 不支援影像。
* **檔案格式**: 請參 [閱「連線資產」支援的檔案格式](assets-formats.md#supported-document-formats)。

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定及使用功能以及其相對應的使用者群組時，相關的各種角色。本機範圍用於作者建立網頁的使用案例。 遠端範圍適用於託管所需資產的 DAM 部署。The [!DNL Sites] author fetches these remote assets.

| 角色 | 範圍 | 使用者群組 | 逐步說明中的使用者名稱 | 需求 |
|---|---|---|---|---|
| [!DNL Sites] 管理員 | 本機 | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| DAM 使用者 | 本機 | `Authors` | `ksaner` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| [!DNL Sites] 作者 | 本機 | `Authors` (在遠端DAM上具有讀取存取權，在本機上具有作者存取權 [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. 已採用 `ksaner` DAM 使用者的認證。 |
| [!DNL Assets] 管理員 | 遠端 | [!DNL Experience Manager] `administrators` | `admin` 遠程 [!DNL Experience Manager] | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | `Authors` | `ksaner` 遠程 [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| DAM 經銷商 (技術使用者) | 遠端 | [!DNL Sites] `Authors` | `ksaner` 遠程 [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. 此角色與上述的兩個 `ksaner` 角色不一樣，而且屬於不同的使用者群組。 |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. 按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. [!DNL Assets] 位置為 `https://[assets_servername_ams]:[port]`。
   1. DAM 經銷商 (技術使用者) 的認證。
   1. 在&#x200B;**[!UICONTROL 「掛接點」]**&#x200B;欄位中，輸入 擷取資產的本機 路徑。[!DNL Experience Manager][!DNL Experience Manager]例如，`remoteassets` 資料夾。
   1. 根據您的網路調整&#x200B;**[!UICONTROL 原始二進位傳輸最佳化臨界值]**。大於此臨界值的資產轉譯項目會以非同步方式傳送。
   1. 如果您是使用資料存放區來儲存資產，且「資料存放區」是兩個 部署之間的共用儲存空間，請選取&#x200B;**[!UICONTROL 「與連線資產共用的資料存放區」]**。這種情況下，臨界值限制並不重要，因為實際的資產二進位檔位於資料存放區，而且不會轉移。
   ![連線資產的典型設定](assets/connected-assets-typical-config.png)

   *圖：連線資產的典型設定.*

1. 資產處理完畢且轉譯完成擷取後，請停用工作流程啟動器。Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | 變更前 | 變更後 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作者擷取資產時，會擷取遠端 部署上可用的所有轉譯項目。若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. 使用管理員憑證登入。 搜尋 `Cross-Origin`. 存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web 主控台」]**。

   1. To create a CORS configuration for [!DNL Sites] instance, click add option ![aem_assets_add_icon](assets/do-not-localize/aem_assets_add_icon.png) next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. 儲存設定。

## 使用遠端資產 {#use-remote-assets}

網站作者使用「內容尋找器」連線至 DAM 例項。作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要向遠端 DAM 驗證，請備妥管理員提供的 DAM 使用者認證。

作者可在單一網頁中使用本機DAM和遠端DAM例項上的可用資產。 使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. 其他所有標籤會一概捨棄。Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. 或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. 輸入 `ksaner` 作為使用者名稱，選取畫面上提供的選項，然後按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 在&#x200B;**[!UICONTROL 「Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL tw]** > **[!UICONTROL zh」]**&#x200B;開啟「We.Retail」網頁。編輯頁面。或者，您也可以在瀏覽器中存取 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`，進而編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. 提供憑證 `ksaner` 作為使用者名稱，且以 `password` 作為密碼。This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. 由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項.*

1. 如果資產是以非同步方式擷取，一有擷取任務執行失敗，網站作者就會收到通知。編寫過程中或甚至在完成編寫之後，作者都能在[非同步工作](/help/assets/asynchronous-jobs.md)使用者介面中查看擷取任務和錯誤的詳細資訊。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：背景中非同步擷取資產作業的相關通知。*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. 請確認發佈時，系統已成功擷取遠端資產。若要檢查所擷取資產的個別狀態，請參閱[非同步工作](/help/assets/asynchronous-jobs.md)使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未成功擷取，頁面還是會照常發佈。使用遠端資產的元件會以空白形式發佈。The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>擷取的遠端資產一旦用於網頁中，只要任何人有權存取所擷取資產儲存位置的本機資料夾，都能搜尋和使用 (即上述逐步說明中的`connectedassets`)。這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

## 限制 {#limitations}

### 權限與資產管理 {#permissions-and-managing-assets}

* 本機資產不會與遠端部署上的原始資產同步。對 DAM 部署所做的任何編輯、刪除或撤銷權限操作都不會傳播到下游。
* 本機資產為唯讀副本。[!DNL Experience Manager] 元件會對資產執行非破壞性的編輯作業。不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和列出的文件格式。[!DNL Dynamic Media] 不支援資產、內容片段和體驗片段。
* 不會擷取中繼資料結構。
* All [!DNL Sites] authors have read permissions on the fetched copies, even if authors do not have access to the remote DAM deployment.
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。請參閱[資產移轉指南](assets-migration-guide.md)。
* 無法將遠端資產當做頁面屬性使用者介面上的頁 [!UICONTROL 面縮圖] 。 您可以按一下「選取影像」，在「縮圖」的「頁 [!UICONTROL 面屬性] 」使用者介面中設定網頁的縮圖 。

### 設定和授權 {#setup-licensing}

* [!DNL Assets] 支援在上 [!DNL Adobe Managed Services] 部署。
* [!DNL Sites] 一次可以連接到 [!DNL Assets] 單個儲存庫。
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### 使用狀況 {#usage}

* 目前僅支援搜尋遠端資產及拖曳本機頁面上的遠端資產，以便編寫內容。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* 您可以對擷取的資產執行非破壞性的簡單編輯作業，也能執行透過 `Image` 元件支援的編輯工作。資產僅供唯讀。

## 疑難排解問題 {#troubleshoot}

請依照下列步驟，疑難排解常見的錯誤情形：

* If you cannot search for remote assets from the [!UICONTROL Content Finder] then ensure that the required roles and permissions are in place.
* 從遠端Dam擷取的資產可能因一個或多個原因無法發佈在網頁上。 它不存在於遠程伺服器上，缺少獲取它的適當權限，或者網路故障可能是原因。 確保資產未從遠端DAM移除。 請確定已有適當的權限，並符合必要條件。 重新嘗試將資產新增至頁面並重新發佈。 檢查[非同步工作清單](/help/assets/asynchronous-jobs.md)，找出資產擷取作業的錯誤。
