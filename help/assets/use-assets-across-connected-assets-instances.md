---
title: 在 Adobe Experience Manager Sites 編寫工作流程中使用「連線資產」共用 DAM 資產
description: 在其他 Experience Manager 網站的部署工作中建立網頁時，使用遠端 Adobe Experience Manager Assets 部署的可用資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: ccdafa89793e97f69294958d814cccf3554b496d

---


# 使用「連線資產」在 AEM Sites 中共用 DAM 資產 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。或許出於幾種原因，導致現有部署的地理位置分散，但礙於工作所需而得搭配使用，或是併購後才發現基礎架構的組成複雜分歧，母公司希望能加以整合。

AEM Sites 提供建立網頁的功能，而 AEM Assets 是可為網站提供必要資產的數位資產管理 (DAM) 系統。AEM 現在整合了 AEM Sites 和 AEM Assets，能支援上述使用案例。

## 連線資產概觀 {#overview-of-connected-assets}

在「頁面編輯器」中編輯頁面時，作者可從不同 AEM Assets 部署順暢地搜尋、瀏覽及內嵌資產。若要管理 AEM，請對 AEM Sites 本機部署與 AEM Assets 不同 (遠端) 部署執行一次性整合。

Sites 作者可以唯讀本機資產的形式取得遠端資產。此功能可支援順暢的搜尋作業，並允許一次使用數個遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮大量移轉資產。請參閱[資產移轉指南](/help/assets/assets-migration-guide.md)。

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 每個部署中，使用者都是適當使用者群組的成員。
* 若為 Adobe Experience Manager 部署類型，需符合其中一項支援條件。AEM 6.5 Assets可與AEM搭配使用，做為雲端服務。 如需詳細資訊，請 [參閱AEM中的「Connected Assets」（連線資產）功能(Cloud Service)](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | AEM Sites 雲端服務 | AMS 上的 AEM 6.5 Sites | 內部部署的 AEM 6.5 Sites |
   |---|---|---|---|
   | **AEM Assets 雲端服務** | 支援 | 支援 | 支援 |
   | **AMS 上的 AEM 6.5 Assets** | 支援 | 支援 | 支援 |
   | **內部部署的 AEM 6.5 Assets** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者可在「內容尋找器」中搜尋影像和下列類型的文件，並在「頁面編輯器」中使用找到的資產。文件可新增至 `Download` 元件，且影像可新增至 `Image` 元件。作者也可以在任何可延伸預設 `Download` 或 `Image` 元件的自訂 AEM 元件中新增遠端資產。支援的格式清單包括：

* **影像格式**:Image元件支援的影像格 [式](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/components/image.translate.html) ，由Connected Assets支援。 不支援動態媒體影像。
* **文件格式**：請參閱[連線資產支援的文件格式](assets-formats.md#supported-document-formats)。

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定及使用功能以及其相對應的使用者群組時，相關的各種角色。本機範圍適用於由作者建立網頁的使用案例。遠端範圍適用於託管所需資產的 DAM 部署。Sites 作者會擷取這些遠端資產。

| 角色 | 範圍 | 使用者群組 | 逐步說明中的使用者名稱 | 需求 |
|---|---|---|---|---|
| AEM Sites 管理員 | 本機 | AEM 管理員 | `admin` | 設定 AEM，設定與遠端資產部署的整合。 |
| DAM 使用者 | 本機 | 作者 | `ksaner` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| AEM Sites 作者 | 本機 | 作者 (在遠端 DAM 上擁有讀取存取權限，並在本機 Sites 上擁有作者存取權限) | `ksaner` | 一般使用者是指使用這項整合提升其內容速度的 Sites 作者。作者可使用「內容尋找器」在遠端 DAM 中搜尋及瀏覽資產，並在本機網頁中使用所需的影像。已採用 `ksaner` DAM 使用者的認證。 |
| AEM Assets 管理員 | 遠端 | AEM 管理員 | 遠端 AEM 上的 `admin` | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | 作者 | 遠端 AEM 上的 `ksaner` | 遠端 AEM 部署上的作者角色。使用「內容尋找器」，在「連線資產」中搜尋和瀏覽資產。 |
| DAM 經銷商 (技術使用者) | 遠端 | 套件建立者和網站作者 | 遠端 AEM 上的 `ksaner` | AEM 本機伺服器 (非 Site 作者角色) 會代表 Sites 作者，以遠端部署上這名使用者的名義來擷取遠端資產。此角色與上述的兩個 `ksaner` 角色不一樣，而且屬於不同的使用者群組。 |

## 設定 Sites 和 Assets 部署之間的連線 {#configure-a-connection-between-sites-and-assets-deployments}

AEM 管理員可建立這項整合。一旦建立之後，系統會透過您在 Sites 部署和 DAM 部署中定義的使用者群組，建立使用該整合所需的權限。

若要設定「連線資產」和本機 Sites 連線，請遵循這些步驟操作。

1. 存取現有的 AEM Sites 部署，或使用下列命令建立部署：

   1. 在 JAR 檔案的資料夾中，在終端機上執行下列命令以建立各個 AEM 伺服器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 幾分鐘後，AEM 伺服器就會成功啟動。將此 AEM Sites 部署視為網頁編寫的本機電腦，例如 `https://[local_sites]:4502`。

1. 確定 AEM Sites 部署和 AMS 上的 AEM Assets 部署，都存在具有本機範圍的使用者和角色。建立 Assets 部署的技術使用者，並新增至[相關使用者和群組](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)所提及的使用者群組。

1. 在 `https://[local_sites]:4502` 存取本機 AEM Sites 部署。按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. AEM Assets 位置為 `https://[assets_servername_ams]:[port]`。
   1. DAM 經銷商 (技術使用者) 的認證。
   1. 在&#x200B;**[!UICONTROL 「掛接點」]**&#x200B;欄位中，輸入 AEM 擷取資產的本機 AEM 路徑。例如，`remoteassets` 資料夾。
   1. 根據您的網路調整&#x200B;**[!UICONTROL 原始二進位傳輸最佳化臨界值]**。大於此臨界值的資產轉譯項目會以非同步方式傳送。
   1. 如果您是使用資料存放區來儲存資產，且「資料存放區」是兩個 AEM 部署之間的共用儲存空間，請選取&#x200B;**[!UICONTROL 「與連線資產共用的資料存放區」]**。這種情況下，臨界值限制並不重要，因為實際的資產二進位檔位於資料存放區，而且不會轉移。
      ![連線資產的典型設定](assets/connected-assets-typical-config.png)
   *圖：連線資產的典型設定*

1. 資產處理完畢且轉譯完成擷取後，請停用工作流程啟動器。調整本機 (AEM Sites) 部署上的啟動器設定，以排除 `connectedassets` 資料夾 (遠端資產擷取作業的執行位置)。

   1. 在 AEM Sites 部署中，按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 啟動器」]**。

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. 在「屬性」設定精靈中，將&#x200B;**[!UICONTROL 「路徑」]**&#x200B;欄位變更為下列對應內容，更新其規則運算式以排除掛接點 **[!UICONTROL connectedassets]**。
   | 變更前 | 變更後 |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)renditions/original | /content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*/)renditions/original | /content/dam(/((?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >作者擷取資產時，會擷取遠端 AEM 部署上可用的所有轉譯項目。若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。「DAM 更新資產」工作流程會隨即觸發，並建立更多轉譯項目。這些轉譯項目僅限在本機 Sites 部署中使用，不可在遠端 DAM 部署中使用。

1. 在遠端 AEM Assets 的 CORS 設定中，將 AEM Sites 例項新增為其中一個&#x200B;**[!UICONTROL 「允許的原始項」]**。

   1. 使用管理員認證登入。搜尋「跨原始」。存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web 主控台」]**。

   1. 若要建立 AEM Sites 例項的 CORS 設定，請按一下&#x200B;**[!UICONTROL 「Adobe Granite 跨原始資源共用原則」]**&#x200B;旁的 ![aem_assets_add_icon](assets/aem_assets_add_icon.png) 圖示。

   1. 在&#x200B;**[!UICONTROL 「允許的原始項」]**&#x200B;欄位中，輸入本機 Sites 的 URL，也就是 `https://[local_sites]:[port]`。儲存設定。

## 使用遠端資產 {#use-remote-assets}

網站作者使用「內容尋找器」連線至 DAM 例項。作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要向遠端 DAM 驗證，請備妥管理員提供的 DAM 使用者認證。

作者可以在單一網頁中使用本機 DAM 和遠端 DAM 例項所提供的可用資產。使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

系統只會鎖定那些標籤與本機 Sites 例項完全對應的遠端資產 (分類層次結構相同)，擷取其標籤。其他所有標籤會一概捨棄。由於 AEM 提供全文字搜尋功能，作者可使用遠端 AEM 部署上的所有標籤來搜尋遠端資產。

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. 從 AEM 工作區存取&#x200B;**[!UICONTROL 「Assets]** > **[!UICONTROL 檔案」]**，導覽至遠端部署的 Assets UI。或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。
1. 在 Sites 例項右上角的設定檔啟動器中，按一下&#x200B;**[!UICONTROL 「模擬為」]**。輸入 `ksaner` 作為使用者名稱，選取畫面上提供的選項，然後按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 在&#x200B;**[!UICONTROL 「Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL tw]** > **[!UICONTROL zh」]**&#x200B;開啟「We.Retail」網頁。編輯頁面。或者，您也可以在瀏覽器中存取 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`，進而編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. 開啟「Assets」標籤，然後按一下&#x200B;**[!UICONTROL 「登入連線資產」]**。
1. 提供憑證 `ksaner` 作為使用者名稱，且以 `password` 作為密碼。這位使用者對這兩種 AEM 部署都具有編寫權限。
1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   本機 AEM Sites 部署上，擷取的資產為唯讀狀態。您仍可使用 AEM Sites 元件提供的選項，編輯所擷取的資產。由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項*

1. 如果資產是以非同步方式擷取，一有擷取任務執行失敗，網站作者就會收到通知。編寫過程中或甚至在完成編寫之後，作者都能在[非同步工作](/help/assets/asynchronous-jobs.md)使用者介面中查看擷取任務和錯誤的詳細資訊。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：關於在背景發生之資產的非同步擷取通知*

1. 發佈頁面時，AEM 會顯示頁面所使用資產的完整清單。請確認發佈時，系統已成功擷取遠端資產。若要檢查所擷取資產的個別狀態，請參閱[非同步工作](/help/assets/asynchronous-jobs.md)使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未成功擷取，頁面還是會照常發佈。使用遠端資產的元件會以空白形式發佈。AEM 通知區域會依照非同步工作頁面所出現的錯誤來顯示通知。

>[!CAUTION]
>
>擷取的遠端資產一旦用於網頁中，只要任何人有權存取所擷取資產儲存位置的本機資料夾，都能搜尋和使用 (即上述逐步說明中的`connectedassets`)。這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

## 限制 {#limitations}

**權限與資產管理**

* 本機資產不會與遠端部署上的原始資產同步。對 DAM 部署所做的任何編輯、刪除或撤銷權限操作都不會傳播到下游。
* 本機資產為唯讀副本。AEM 元件會對資產執行非破壞性的編輯作業。不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和列出的文件格式。不支援動態媒體資產、內容片段和體驗片段。
* 不會擷取中繼資料結構。
* 所有 Sites 作者都具備所擷取副本的讀取權限，即使他們沒有遠端 DAM 部署的存取權限，還是可以讀取。
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。請參閱[資產移轉指南](assets-migration-guide.md)。
* 無法將遠端資產當做頁面屬性使用者介面上的頁 [!UICONTROL 面縮圖] 。 您可以按一下「選取影像」，在「縮圖」的「頁 [!UICONTROL 面屬性] 」使用者介面中設定網頁的縮圖 。

**設定和授權**

* 支援在 AMS 上部署 AEM Assets。
* AEM Sites 一次可連線至單一 AEM Assets 存放庫。
* AEM Assets 授權可作為遠端存放庫使用。
* AEM Sites 的一或多個授權可作為本機編寫部署。

**使用狀況**

* 目前僅支援搜尋遠端資產及拖曳本機頁面上的遠端資產，以便編寫內容。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。作者可從[!UICONTROL 「內容尋找器」]將遠端資產拖曳至[!UICONTROL 「頁面編輯器」]，以利重新嘗試。
* 您可以對擷取的資產執行非破壞性的簡單編輯作業，也能執行透過 AEM `Image` 元件支援的編輯工作。資產僅供唯讀。

## 疑難排解問題 {#troubleshoot}

請依照下列步驟，疑難排解常見的錯誤情形：

* 如果您無法從「內容尋找器」搜尋遠端資產，請再次檢查，確定您具備所需的角色和權限。
* 從遠端 DAM 擷取的資產可能會無法發佈至網頁，原因包括：該資產不存在於遠端；缺乏適當的擷取權限；網路發生問題。確認資產未從遠端 DAM 移除，或權限未受到變更；確認您符合適當的先決條件；重新嘗試將資產新增至頁面並重新發佈。檢查[非同步工作清單](/help/assets/asynchronous-jobs.md)，找出資產擷取作業的錯誤。
