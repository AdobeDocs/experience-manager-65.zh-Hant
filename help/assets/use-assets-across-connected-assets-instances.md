---
title: 使用「連線資產」在 中共用 DAM 資產 [!DNL Sites]
description: 使用遠端 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 部署上可用的資產。
contentOwner: AG
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: 37073594b45995ade7f0e73c519feb21adf48482
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 29%

---

# 使用「連線資產」在 中共用 DAM 資產 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。原因之一，是現有部署分散，需要搭配使用。 另一個原因可能是收購導致基礎架構的差異，包括母公司希望一起使用的不同[!DNL Experience Manager]版本。

「連線資產」功能整合[!DNL Experience Manager Sites]和[!DNL Experience Manager Assets]，可支援上述使用案例。 使用者可以在[!DNL Sites]中建立網頁，使用個別[!DNL Assets]部署中的數位資產。

## 連線資產概觀 {#overview-of-connected-assets}

在[!UICONTROL 頁面編輯器]中編輯頁面時，作者可以順暢地搜尋、瀏覽及內嵌來自作為資產來源之不同[!DNL Assets]部署的資產。 管理員將具有[!DNL Sites]功能的[!DNL Experience Manager]部署與具有[!DNL Assets]功能的[!DNL Experience Manager]其他部署建立一次性整合。

對於[!DNL Sites]作者，遠端資產以唯讀本機資產的形式提供。 此功能可支援順暢的搜尋作業，並允許一次使用數個遠端資產。若要一次在[!DNL Sites]部署中提供許多遠端資產，請考慮大量移轉資產。 請參閱[Experience Manager資產移轉指南](/help/assets/assets-migration-guide.md)。

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 使用者是每個部署中適當使用者群組的成員。
* 對於[!DNL Adobe Experience Manager]部署類型，滿足支援的條件之一。 [!DNL Experience Manager] 6.5可 [!DNL Assets] 搭配 [!DNL Experience Manager] Cloud Service使用。如需此功能在[!DNL Experience Manager]中以[!DNL Cloud Service]形式運作的詳細資訊，請參閱 [!DNL Experience Manager] 中以 [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)形式運作的[連線資產。

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] AMS上的 [!DNL Sites] 6.5 | [!DNL Experience Manager] 6.5內 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支援 | 支援 | 支援 |
   | **[!DNL Experience Manager]AMS上的 [!DNL Assets] 6.5** | 支援 | 支援 | 支援 |
   | **[!DNL Experience Manager]6.5內 [!DNL Assets] 部部署** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者在「內容尋找器」中搜尋影像和下列類型的檔案，並在「頁面編輯器」中使用搜尋的資產。 文檔將添加到`Download`元件，並將影像添加到`Image`元件。 作者也會在延伸預設`Download`或`Image`元件的任何自訂[!DNL Experience Manager]元件中新增遠端資產。 支援的格式為：

* **影像格式**:影像元件支 [援的](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html) 格式。
* **文檔格式**:請參閱支 [援的檔案格式](assets-formats.md#supported-document-formats)。

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定及使用功能以及其相對應的使用者群組時，相關的各種角色。本機範圍適用於作者建立網頁的使用案例。 遠端範圍適用於託管所需資產的 DAM 部署。[!DNL Sites]作者會擷取這些遠端資產。

| 角色 | 範圍 | 使用者群組 | 逐步說明中的使用者名稱 | 需求 |
|---|---|---|---|---|
| [!DNL Sites] 管理員 | 本機 | [!DNL Experience Manager] `administrators` | `admin` | 設定[!DNL Experience Manager]並配置與遠程[!DNL Assets]部署的整合。 |
| DAM 使用者 | 本機 | `Authors` | `ksaner` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| [!DNL Sites] 作者 | 本機 | <ul><li>`Authors` (在遠端DAM上具有讀取存取權，並在本機上具有作者存取權 [!DNL Sites]) </li> <li>`dam-users` 本地  [!DNL Sites]</li></ul> | `ksaner` | 一般使用者為[!DNL Sites]作者，他們使用此整合來改善其內容速度。 作者可使用[!UICONTROL 內容尋找器]，並在本機網頁中使用所需影像，在遠端DAM中搜尋及瀏覽資產。 已採用 `ksaner` DAM 使用者的認證。 |
| [!DNL Assets] 管理員 | 遠端 | [!DNL Experience Manager] `administrators` | `admin` 遠端  [!DNL Experience Manager] | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | `Authors` | `ksaner` 遠端  [!DNL Experience Manager] | 在遠程[!DNL Experience Manager]部署上編寫角色。 使用[!UICONTROL 內容尋找器]在「連線資產」中搜尋和瀏覽資產。 |
| DAM 經銷商 (技術使用者) | 遠端 | [!DNL Sites] `Authors` | `ksaner` 遠端  [!DNL Experience Manager] | [!DNL Experience Manager]本機伺服器（非[!DNL Sites]作者角色）會代表[!DNL Sites]作者，使用遠端部署上的此使用者來擷取遠端資產。 此角色與上述的兩個 `ksaner` 角色不一樣，而且屬於不同的使用者群組。 |

## 配置[!DNL Sites]和[!DNL Assets]部署之間的連接 {#configure-a-connection-between-sites-and-assets-deployments}

[!DNL Experience Manager]管理員可以建立此整合。 建立後，需要的使用權限會透過使用者群組建立。 在[!DNL Sites]部署和DAM部署中定義使用者群組。

要配置「已連接資產」和本地[!DNL Sites]連接，請執行以下步驟：

1. 使用以下命令訪問現有[!DNL Sites]部署或建立部署：

   1. 在JAR檔案的資料夾中，在終端上執行以下命令以建立每個[!DNL Experience Manager]伺服器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 幾分鐘後，[!DNL Experience Manager]伺服器將成功啟動。 將此[!DNL Sites]部署視為網頁編寫的本地電腦，如`https://[local_sites]:4502`。

1. 確保[!DNL Sites]部署和AMS上的[!DNL Assets]部署上存在具有適當範圍的用戶和角色。 在[!DNL Assets]部署上建立技術用戶，並將其添加到[涉及的用戶和組](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)中提及的用戶組。

1. 在`https://[local_sites]:4502`訪問本地[!DNL Sites]部署。 按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. 配置的&#x200B;**[!UICONTROL Title]**。
   1. **[!UICONTROL 遠端]** DAM URL是格式 [!DNL Assets] 中位置的URL  `https://[assets_servername]:[port]`。
   1. DAM 經銷商 (技術使用者) 的認證。
   1. 在&#x200B;**[!UICONTROL 掛接點]**&#x200B;欄位中，輸入[!DNL Experience Manager]擷取資產的本機[!DNL Experience Manager]路徑。 例如，`remoteassets` 資料夾。從DAM擷取的資產會儲存在[!DNL Sites]部署的此資料夾中。
   1. **[!UICONTROL 本機網]** 站URL是部署的 [!DNL Sites] 位置。[!DNL Assets] 部署會使用此值來維護此部署所擷取之數位資產的 [!DNL Sites] 參考。
   1. [!DNL Sites]技術用戶的憑據。
   1. **[!UICONTROL 原始二進位傳輸最佳化臨界值]**&#x200B;欄位值會指定原始資產（包括轉譯）是否同步傳輸。 檔案大小較小的資產可以輕鬆擷取，而檔案大小相對較大的資產最好以非同步方式同步。 值取決於您的網路功能。
   1. 如果您是使用資料存放區來儲存資產，且「資料存放區」是兩個 部署之間的共用儲存空間，請選取&#x200B;**[!UICONTROL 「與連線資產共用的資料存放區」]**。在此情況下，臨界值限制並不重要，因為資料存放區上有實際的資產二進位檔，且不會傳輸。

   ![連線資產功能的典型設定](assets/connected-assets-typical-config.png)

   *圖：「連線資產」功能的一般設定。*

1. 部署[!DNL Assets]上的現有數位資產已處理且會產生轉譯。 這些轉譯會使用此功能擷取，因此不需要重新產生轉譯。 停用工作流程啟動器以防止重新產生轉譯。 調整([!DNL Sites])部署上的啟動器配置，以排除`connectedassets`資料夾（資產會擷取在此資料夾中）。

   1. 在[!DNL Sites]部署中，按一下「**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 啟動器]**」。

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. 在[!UICONTROL 屬性]精靈中，將&#x200B;**[!UICONTROL 路徑]**&#x200B;欄位變更為下列對應，以更新其規則運算式以排除掛接點&#x200B;**[!UICONTROL connectedassets]**。

   | 變更前 | 變更後 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作者擷取資產時，會擷取遠端 部署上可用的所有轉譯項目。若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。「[!UICONTROL  DAM更新資產]」工作流程會隨即觸發，並建立更多轉譯項目。 這些轉譯僅可在本機[!DNL Sites]部署中使用，不可在遠端DAM部署中使用。

1. 在[!DNL Assets]部署的CORS設定中，將[!DNL Sites]部署新增為允許的來源。 如需詳細資訊，請參閱[了解CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)。

1. 配置[相同網站Cookie支援](/help/sites-administering/same-site-cookie-support.md)。

您可以檢查已配置[!DNL Sites]部署和[!DNL Assets]部署之間的連接。

![已連接資產的連接測 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*試圖：已設定連線資產的連線測試 [!DNL Sites]。*

## 使用遠端資產 {#use-remote-assets}

網站作者使用「內容尋找器」連線至DAM部署。 作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要向遠端 DAM 驗證，請備妥管理員提供的 DAM 使用者認證。

作者可在單一網頁中使用本機DAM和遠端DAM部署上可用的資產。 使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

系統只會擷取具有完全對應標籤的遠端資產標籤，以及本機[!DNL Sites]部署中可用的相同分類階層。 其他所有標籤會一概捨棄。作者可以使用遠端[!DNL Experience Manager]部署上的所有標籤來搜尋遠端資產，因為這提供全文搜尋功能。

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. 從[!DNL Experience Manager]工作區存取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**，導覽至遠端部署的[!DNL Assets]介面。 或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。
1. 在[!DNL Sites]部署中，在右上角的配置式激活器中，按一下「模擬為&#x200B;]**」。**[!UICONTROL &#x200B;輸入 `ksaner` 作為使用者名稱，選取畫面上提供的選項，然後按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 在&#x200B;**[!UICONTROL 「Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL tw]** > **[!UICONTROL zh」]**&#x200B;開啟「We.Retail」網頁。編輯頁面。或者，您也可以在瀏覽器中存取 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`，進而編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. 開啟[!UICONTROL Assets]標籤，然後按一下&#x200B;**[!UICONTROL 登入連線資產]**。
1. 提供憑證 `ksaner` 作為使用者名稱，且以 `password` 作為密碼。此使用者對這兩種[!DNL Experience Manager]部署都有編寫權限。
1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   本機[!DNL Sites]部署上，擷取的資產為唯讀狀態。 您仍可以使用[!DNL Sites]元件提供的選項來編輯擷取的資產。 由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項.*

1. 如果資產是以非同步方式擷取，一有擷取任務執行失敗，網站作者就會收到通知。在編寫時或甚至在編寫後，作者都可以在[非同步作業](/help/sites-administering/asynchronous-jobs.md)使用者介面中查看擷取任務和錯誤的詳細資訊。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：背景中非同步擷取資產作業的相關通知。*

1. 發佈頁面時，[!DNL Experience Manager]會顯示頁面上使用的完整資產清單。 請確認發佈時，系統已成功擷取遠端資產。若要檢查所擷取資產的每個狀態，請參閱[非同步作業](/help/sites-administering/asynchronous-jobs.md)使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未成功擷取，頁面還是會照常發佈。使用遠端資產的元件會以空白形式發佈。[!DNL Experience Manager]通知區域會針對非同步作業頁面中顯示的錯誤顯示通知。

>[!CAUTION]
>
>擷取的遠端資產一旦用於網頁中，只要任何人有權存取本機資料夾，都可搜尋和使用。 擷取的資產會儲存在本機資料夾中（上述逐步說明中的`connectedassets`）。 這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

### 檢查跨網頁的資產使用情形 {#asset-usage-references}

[!DNL Experience Manager] 可讓DAM使用者檢查資產的所有參考。它有助於了解及管理遠端[!DNL Sites]和複合資產中資產的使用情形。 部署[!DNL Experience Manager Sites]的許多網頁作者可以在不同網頁的遠端[!DNL Assets]上使用資產。 為了簡化資產管理，避免導致參考損毀，DAM使用者必須檢查本機和遠端網頁上資產的使用情形。 資產的[!UICONTROL 屬性]頁面中的[!UICONTROL 參考]標籤會列出資產的本機和遠端參考。

要查看和管理[!DNL Assets]部署上的引用，請執行以下步驟：

1. 在「[!DNL Assets]控制台」中選擇資產，然後從工具欄按一下「**[!UICONTROL 屬性]**」。
1. 按一下「**[!UICONTROL 參考]**」標籤。 請參閱&#x200B;**[!UICONTROL 本機參考]** ，以了解在[!DNL Assets]部署上使用資產的資訊。 請參閱**[!UICONTROL 遠端參考]以取得[!DNL Sites]部署上資產的使用，該部署是使用連線資產功能擷取資產。

   ![資產屬性頁面中的遠端參考](assets/connected-assets-remote-reference.png)

1. [!DNL Sites]頁面的參考會顯示每個本機[!DNL Sites]的參考總數。 查找所有參照並顯示參照總數可能需要一些時間。
1. 參考清單是互動式的，DAM使用者可以按一下參考以開啟參考頁面。 如果由於某些原因無法擷取遠端參考，則會顯示通知，通知使用者失敗。
1. 使用者可以移動或刪除資產。 移動或刪除資產時，所有選取資產/資料夾的參考總數會顯示在警告對話方塊中。 刪除尚未顯示參考的資產時，會顯示警告對話方塊。

   ![強制刪除警告](assets/delete-referenced-asset.png)

## 限制和最佳實務 {#tip-and-limitations}

* 若要取得資產使用情形的相關分析，請在[!DNL Sites]例項上設定[ Assets Insight](/help/assets/asset-insights.md)功能。

### 權限與資產管理 {#permissions-and-managing-assets}

* 本機資產不會與遠端部署上的原始資產同步。對 DAM 部署所做的任何編輯、刪除或撤銷權限操作都不會傳播到下游。
* 本機資產為唯讀副本。[!DNL Experience Manager] 元件會對資產執行非破壞性的編輯作業。不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和列出的文件格式。[!DNL Content Fragments] 不 [!DNL Experience Fragments] 支援和。
* [!DNL Experience Manager] 不會擷取中繼資料結構。這表示所有擷取的中繼資料都可能無法顯示。 如果在[!DNL Sites]部署上單獨更新架構，則會顯示所有元資料屬性。
* 所有[!DNL Sites]作者都對擷取的復本擁有讀取權限，即使作者無法存取遠端DAM部署亦然。
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。請參閱[資產移轉指南](assets-migration-guide.md)。
* 您無法在[!UICONTROL 頁面屬性]使用者介面上將遠端資產設為頁面縮圖。 您可以按一下「[!UICONTROL 選擇影像]」，從[!UICONTROL 縮圖]的用戶介面設定[!UICONTROL 頁面屬性]中的網頁縮圖。

### 設定和授權 {#setup-licensing}

* [!DNL Assets] 支援在 [!DNL Adobe Managed Services] 上部署。
* [!DNL Sites] 一次可連線至 [!DNL Assets] 單一存放庫。
* 需要[!DNL Assets]的許可證才能作為遠程儲存庫使用。
* 需要[!DNL Sites]的一個或多個許可證作為本地編寫部署。

### 使用狀況 {#usage}

* 使用者可在編寫時搜尋遠端資產，並拖曳到本機頁面上。 不支援其他功能。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。作者可從[!UICONTROL Content Finder]拖曳遠端資產至[!UICONTROL Page Editor]，以重新嘗試。
* 您可以對擷取的資產執行非破壞性的簡單編輯作業，也能執行透過 `Image` 元件支援的編輯工作。資產僅供唯讀。
* 重新擷取資產的唯一方法是將其拖曳至頁面上。 沒有API支援或其他方法可重新擷取資產以進行更新。
* 如果從DAM終止服務資產，這些資產會繼續在[!DNL Sites]頁面上使用。
* 資產的遠端參考項目會以非同步方式擷取。 參考和總計數不是即時的，如果DAM使用者檢視參考時，Sites作者使用資產，可能會有一些差異。 DAM使用者可以重新整理頁面，並在幾分鐘內重試以取得總計數。

## 疑難排解問題 {#troubleshoot}

若要疑難排解常見錯誤，請遵循下列步驟：

* 如果您無法從[!UICONTROL 內容尋找器]搜尋遠端資產，請確定已具備必要的角色和權限。

* 從遠端DAM擷取的資產可能因一或多個原因無法發佈在網頁上。 遠程伺服器上不存在它，缺少獲取它的適當權限，或者網路故障可能是原因。 確認資產未從遠端DAM中移除。 請確定已具備適當權限，並符合必要條件。 重試將資產新增至頁面並重新發佈。 檢查[非同步工作清單](/help/sites-administering/asynchronous-jobs.md)，找出資產擷取作業的錯誤。

* 如果您無法從本機[!DNL Sites]部署存取遠端DAM部署，請確定允許跨網站Cookie，並設定[相同網站Cookie支援](/help/sites-administering/same-site-cookie-support.md)。 如果跨網站Cookie遭到封鎖，[!DNL Experience Manager]的部署可能無法驗證。 例如，在無痕模式中， [!DNL Google Chrome]可能會封鎖第三方Cookie。 若要允許[!DNL Chrome]瀏覽器中的Cookie，請按一下位址列中的「眼睛」圖示，導覽至&#x200B;**網站無法運作** > **已封鎖**，選取遠端DAM URL，並允許登入代號Cookie。 或者，請參閱[如何啟用第三方Cookie](https://support.google.com/chrome/answer/95647)。

   ![Chrome瀏覽器中無痕模式出現Cookie錯誤](assets/chrome-cookies-incognito-dialog.png)

* 如果未檢索遠程引用並導致錯誤消息，請檢查[!DNL Sites]部署是否可用，並檢查網路連接問題。 稍後重試以檢查。 [!DNL Assets] 部署嘗試兩次建立與部署 [!DNL Sites] 的連接，然後報告失敗。

   ![無法擷取資產遠端參考](assets/reference-report-failure.png)
