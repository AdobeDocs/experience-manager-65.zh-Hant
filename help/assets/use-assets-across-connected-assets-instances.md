---
title: 使用「連線資產」在[!DNL Adobe Experience Manager Sites]製作工作流程中共用DAM資產。
description: 在其他Experience Manager網站部署中建立網頁時，請使用遠端[!DNL Adobe Experience Manager Assets]部署中的可用資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 使用「連線資產」在 中共用 DAM 資產 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。或許出於幾種原因，導致現有部署的地理位置分散，但礙於工作所需而得搭配使用，或是併購後才發現基礎架構的組成複雜分歧，母公司希望能加以整合。

[!DNL Adobe Experience Manager Sites] 提供建立網頁的功能，而 是可為網站提供必要資產的數位資產管理 (DAM) 系統。[!DNL Adobe Experience Manager Assets][!DNL Experience Manager] 現在整合和支援上述使用 [!DNL Experience Manager Sites] 案例 [!DNL Experience Manager Assets]。

## 連線資產概觀 {#overview-of-connected-assets}

When editing pages in Page Editor, the authors can seamlessly search, browse, and embed assets from a different [!DNL Experience Manager Assets] deployment. To do an [!DNL Experience Manager] administrator do a one-time integration of a local deployment of [!DNL Experience Manager Sites] with a different (remote) deployment of [!DNL Experience Manager Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. 此功能可支援順暢的搜尋作業，並允許一次使用數個遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮大量移轉資產。請參 [閱Experience Manager資產遷移指南](/help/assets/assets-migration-guide.md)。

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 每個部署中，使用者都是適當使用者群組的成員。
* 若為 Adobe Experience Manager 部署類型，需符合其中一項支援條件。[!DNL Experience Manager] 6.5可 [!DNL Assets] 搭配雲 [!DNL Experience Manager] 端服務使用。 如需詳細資訊，請 [參閱Experience Manager中的「Connected Assets」（連接資產）功能，即雲端服務](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | [!DNL Experience Manager Sites] 雲端服務 | AMS上的Experience Manager 6.5 [!DNL Sites] 版 | Experience Manager 6.5現 [!DNL Sites] 場部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]雲端服務&#x200B;** | 支援 | 支援 | 支援 |
   | **AMS上的Experience Manager 6.5[!DNL Assets]版** | 支援 | 支援 | 支援 |
   | **Experience Manager 6.5現[!DNL Assets]場部署** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者可在「內容尋找器」中搜尋影像和下列類型的文件，並在「頁面編輯器」中使用找到的資產。文件可新增至 `Download` 元件，且影像可新增至 `Image` 元件。Authors can also add the remote assets in any custom Experience Manager component that extends the default `Download` or `Image` components. 支援的格式清單包括：

* **影像格式**:Image元件支援的影像格 [式](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/components/image.translate.html) ，由Connected Assets支援。 [!DNL Dynamic Media] 不支援影像。
* **文件格式**：請參閱[連線資產支援的文件格式](assets-formats.md#supported-document-formats)。

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定及使用功能以及其相對應的使用者群組時，相關的各種角色。本機範圍適用於由作者建立網頁的使用案例。遠端範圍適用於託管所需資產的 DAM 部署。The [!DNL Sites] author fetches these remote assets.

| 角色 | 範圍 | 使用者群組 | 逐步說明中的使用者名稱 | 需求 |
|---|---|---|---|---|
| [!DNL Sites] 管理員 | 本機 | Experience Manager管理員 | `admin` | 設定Experience Manager，設定與遠端部署的 [!DNL Assets] 整合。 |
| DAM 使用者 | 本機 | 作者 | `ksaner` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| [!DNL Sites] 作者 | 本機 | Author (with read access on the remote DAM and author access on local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. 作者可使用「內容尋找器」在遠端 DAM 中搜尋及瀏覽資產，並在本機網頁中使用所需的影像。已採用 `ksaner` DAM 使用者的認證。 |
| [!DNL Assets] 管理員 | 遠端 | Experience Manager管理員 | `admin` 在遠程Experience Manager上 | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | 作者 | `ksaner` 在遠程Experience Manager上 | 在遠端Experience Manager部署上擔任作者角色。 使用「內容尋找器」，在「連線資產」中搜尋和瀏覽資產。 |
| DAM 經銷商 (技術使用者) | 遠端 | 套件建立者和網站作者 | `ksaner` 在遠程Experience Manager上 | This user present on the remote deployment is used by Experience Manager local server (not the Site author role) to fetch the remote assets, on behalf of [!DNL Sites] author. 此角色與上述的兩個 `ksaner` 角色不一樣，而且屬於不同的使用者群組。 |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

Experience Manager管理員可以建立此整合。 Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Experience Manager Sites] deployment or create a deployment using the following command:

   1. 在JAR檔案的資料夾中，在終端上執行以下命令以建立每個Experience Manager伺服器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 幾分鐘後，Experience Manager伺服器會成功啟動。 Consider this [!DNL Experience Manager Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the Experience Manager Sites deployment and on the [!DNL Experience Manager Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Experience Manager Sites] deployment at `https://[local_sites]:4502`. 按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. [!DNL Experience Manager Assets] 位置為 `https://[assets_servername_ams]:[port]`。
   1. DAM 經銷商 (技術使用者) 的認證。
   1. In **[!UICONTROL Mount Point]** field, enter the local Experience Manager path where Experience Manager fetches the assets. 例如，`remoteassets` 資料夾。
   1. 根據您的網路調整&#x200B;**[!UICONTROL 原始二進位傳輸最佳化臨界值]**。大於此臨界值的資產轉譯項目會以非同步方式傳送。
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both Experience Manager deployments. 這種情況下，臨界值限制並不重要，因為實際的資產二進位檔位於資料存放區，而且不會轉移。
      ![連線資產的典型設定](assets/connected-assets-typical-config.png)
   *圖：連線資產的典型設定.*

1. 資產處理完畢且轉譯完成擷取後，請停用工作流程啟動器。Adjust the launcher configurations on the local ([!DNL Experience Manager Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Experience Manager Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. 在「屬性」設定精靈中，將&#x200B;**[!UICONTROL 「路徑」]**&#x200B;欄位變更為下列對應內容，更新其規則運算式以排除掛接點 **[!UICONTROL connectedassets]**。
   | 變更前 | 變更後 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >當作者擷取資產時，會擷取遠端Experience Manager部署上可用的所有轉譯。 若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Experience Manager Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Experience Manager Assets] CORS configuration.

   1. 使用管理員認證登入。搜尋 `Cross-Origin`. 存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web 主控台」]**。

   1. To create a CORS configuration for [!DNL Experience Manager Sites] instance, click ![aem_assets_add_icon](assets/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. 儲存設定。

## 使用遠端資產 {#use-remote-assets}

網站作者使用「內容尋找器」連線至 DAM 例項。作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要向遠端 DAM 驗證，請備妥管理員提供的 DAM 使用者認證。

作者可以在單一網頁中使用本機 DAM 和遠端 DAM 例項所提供的可用資產。使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. 其他所有標籤會一概捨棄。作者可以使用遠端Experience Manager部署中顯示的所有標籤來搜尋遠端資產，因為Experience Manager提供全文搜尋。

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. Navigate to the [!DNL Assets] user interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. 或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. 輸入 `ksaner` 作為使用者名稱，選取畫面上提供的選項，然後按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 在&#x200B;**[!UICONTROL 「Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL tw]** > **[!UICONTROL zh」]**&#x200B;開啟「We.Retail」網頁。編輯頁面。或者，您也可以在瀏覽器中存取 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`，進而編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. 提供憑證 `ksaner` 作為使用者名稱，且以 `password` 作為密碼。This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   The fetched assets are read-only on the local [!DNL Experience Manager Sites] deployment. You can still use the options provided by your [!DNL Experience Manager Sites] components to edit the fetched asset. 由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項.*

1. 如果資產是以非同步方式擷取，一有擷取任務執行失敗，網站作者就會收到通知。編寫過程中或甚至在完成編寫之後，作者都能在[非同步工作](/help/assets/asynchronous-jobs.md)使用者介面中查看擷取任務和錯誤的詳細資訊。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：背景中非同步擷取資產作業的相關通知。*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. 請確認發佈時，系統已成功擷取遠端資產。若要檢查所擷取資產的個別狀態，請參閱[非同步工作](/help/assets/asynchronous-jobs.md)使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未成功擷取，頁面還是會照常發佈。使用遠端資產的元件會以空白形式發佈。The [!DNL Experience Manager] notification area displays notification for errors that show in async jobs page.

>[!CAUTION]
>
>擷取的遠端資產一旦用於網頁中，只要任何人有權存取所擷取資產儲存位置的本機資料夾，都能搜尋和使用 (即上述逐步說明中的`connectedassets`)。這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

## 限制 {#limitations}

**權限與資產管理**

* 本機資產不會與遠端部署上的原始資產同步。對 DAM 部署所做的任何編輯、刪除或撤銷權限操作都不會傳播到下游。
* 本機資產為唯讀副本。Experience Manager元件對資產進行非破壞性編輯。 不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和列出的文件格式。[!DNL Dynamic Media] 不支援資產、內容片段和體驗片段。
* 不會擷取中繼資料結構。
* All [!DNL Sites] authors have read permissions on the fetched copies, even if they do not have access to the remote DAM deployment.
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。請參閱[資產移轉指南](assets-migration-guide.md)。
* 無法將遠端資產當做頁面屬性使用者介面上的頁 [!UICONTROL 面縮圖] 。 您可以按一下「選取影像」，在「縮圖」的「頁 [!UICONTROL 面屬性] 」使用者介面中設定網頁的縮圖 。

**設定和授權**

* [!DNL Experience Manager Assets] 支援在AMS上部署。
* [!DNL Experience Manager Sites] 一次可以連接到 [!DNL Experience Manager Assets] 單個儲存庫。
* A license of [!DNL Experience Manager Assets] working as remote repository.
* One or more licenses of [!DNL Experience Manager Sites] working as local authoring deployment.

**使用狀況**

* 目前僅支援搜尋遠端資產及拖曳本機頁面上的遠端資產，以便編寫內容。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。作者可從[!UICONTROL 「內容尋找器」]將遠端資產拖曳至[!UICONTROL 「頁面編輯器」]，以利重新嘗試。
* 您可以對擷取的資產執行非破壞性的簡單編輯作業，也能執行透過 [!DNL Experience Manager] 元件支援的編輯工作。`Image`資產僅供唯讀。

## 疑難排解問題 {#troubleshoot}

請依照下列步驟，疑難排解常見的錯誤情形：

* 如果您無法從「內容尋找器」搜尋遠端資產，請再次檢查，確定您具備所需的角色和權限。
* 從遠端 DAM 擷取的資產可能會無法發佈至網頁，原因包括：該資產不存在於遠端；缺乏適當的擷取權限；網路發生問題。確認資產未從遠端 DAM 移除，或權限未受到變更；確認您符合適當的先決條件；重新嘗試將資產新增至頁面並重新發佈。檢查[非同步工作清單](/help/assets/asynchronous-jobs.md)，找出資產擷取作業的錯誤。
