---
title: 使用「連線資產」在中共用DAM資產 [!DNL Sites]
description: 使用遠端上可用的資產 [!DNL Adobe Experience Manager Assets] 在另一個網頁上建立您的網頁時部署 [!DNL Adobe Experience Manager Sites] 部署。
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3909'
ht-degree: 15%

---

# 使用「連線資產」在中共用DAM資產 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=en) |
| AEM 6.5 | 本文章 |


大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。其中一個原因可能是地理上分散且需要協同工作的現有部署。 另一個原因可能是併購導致基礎架構迥異，包括不同 [!DNL Experience Manager] 版本，母公司想要一起使用的版本。

「連線資產」功能可整合以下用途，支援上述使用案例 [!DNL Experience Manager Sites] 和 [!DNL Experience Manager Assets]. 使用者可以在以下位置建立網頁： [!DNL Sites] 使用來自不同資產的數位資產 [!DNL Assets] 部署。

>[!NOTE]
>
>只有在您需要使用遠端DAM部署中可用的資產（位於單獨的Sites部署中）來製作網頁時，才需設定「連線資產」 。

## 連線資產概觀 {#overview-of-connected-assets}

在中編輯頁面時 [!UICONTROL 頁面編輯器] 作為目標目的地，作者可順暢地搜尋、瀏覽及內嵌其他來源的資產 [!DNL Assets] 作為資產來源的部署。 管理員會為的部署建立一次性整合 [!DNL Experience Manager] 替換為 [!DNL Sites] 另一個部署的功能 [!DNL Experience Manager] 替換為 [!DNL Assets] 功能。 網站作者也可以透過Connected Assets在其網站的網頁中使用Dynamic Media影像，並使用Dynamic Media功能，例如智慧型裁切和影像預設集。

對於 [!DNL Sites] 作者，遠端資產會以唯讀本機資產的形式提供。 此功能可支援順暢的搜尋作業，並可存取網站編輯器上的遠端資產。 若有任何其他使用案例，需要完整的資產語料庫才能在Sites上使用，請考慮大量移轉資產，而非使用「連線資產」。 另請參閱 [Experience Manager Assets移轉指南](/help/assets/assets-migration-guide.md).

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 使用者是每個部署中適當使用者群組的一部分。
* 的 [!DNL Adobe Experience Manager] 部署型別，即符合其中一個支援的條件。 [!DNL Experience Manager] 6.5 [!DNL Assets] 搭配使用 [!DNL Experience Manager] as a Cloud Service。 如需此功能在中如何運作的詳細資訊 [!DNL Experience Manager] as a [!DNL Cloud Service]，請參閱 [Experience Manageras a Cloud Service中的連線資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] 在AMS上 | [!DNL Experience Manager] 6.5 [!DNL Sites] 內部部署 |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支援 | 支援 | 支援 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 在AMS上** | 支援 | 支援 | 支援 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 內部部署** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者在「內容尋找器」中搜尋影像和下列型別的檔案，並在「頁面編輯器」中拖曳搜尋的資產。 檔案將新增至 `Download` 元件和影像至 `Image` 元件。 作者也可以在任何自訂內容中新增遠端資產 [!DNL Experience Manager] 延伸預設值的元件 `Download` 或 `Image` 元件。 支援的格式為：

* **影像格式**：此變數的 [影像元件](assets-formats.md#supported-raster-image-formats) 支援。
* **檔案格式**：請參閱 [支援的檔案格式](assets-formats.md#supported-document-formats).

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定及使用功能以及其相對應的使用者群組時，相關的各種角色。本機範圍適用於作者建立網頁的使用案例。 遠端範圍適用於託管所需資產的 DAM 部署。此 [!DNL Sites] 作者會擷取這些遠端資產。

| 角色 | 範圍 | 使用者群組 | 逐步說明中的使用者名稱 | 說明 |
|---|---|---|---|---|
| [!DNL Sites] 管理員 | 本機 | [!DNL Experience Manager] `administrators` | `admin` | 設定 [!DNL Experience Manager] 並設定與遠端裝置的整合 [!DNL Assets] 部署。 |
| DAM 使用者 | 本機 | `Authors` | `ksaner` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| [!DNL Sites] 作者 | 本機 | <ul><li>`Authors` （在遠端DAM上擁有讀取存取權，並在本機上擁有作者存取權） [!DNL Sites]) </li> <li>`dam-users` 在本機 [!DNL Sites]</li></ul> | `ksaner` | 一般使用者為 [!DNL Sites] 使用此整合來提高內容速度的作者。 作者搜尋及瀏覽遠端DAM中的資產，使用 [!UICONTROL 內容尋找器] 並在本機網頁中使用所需的影像。 已採用 `ksaner` DAM 使用者的認證。 |
| [!DNL Assets] 管理員 | 遠端 | [!DNL Experience Manager] `administrators` | `admin` 在遠端 [!DNL Experience Manager] | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | `Authors` | `ksaner` 在遠端 [!DNL Experience Manager] | 遠端上的作者角色 [!DNL Experience Manager] 部署。 在「連線資產」中使用搜尋和瀏覽資產 [!UICONTROL 內容尋找器]. |
| DAM 經銷商 (技術使用者) | 遠端 | [!DNL Sites] `Authors` | `ksaner` 在遠端 [!DNL Experience Manager] | 遠端部署上的這個使用者是由 [!DNL Experience Manager] 本機伺服器(非 [!DNL Sites] 作者角色)，以代表取得遠端資產 [!DNL Sites] 作者。 此角色與上述的兩個 `ksaner` 角色不一樣，而且屬於不同的使用者群組。 |

### 連線資產架構 {#connected-assets-architecture}

Experience Manager可讓您將遠端DAM部署作為來源連線到多個Experience Manager [!DNL Sites] 部署。 不過，您可以連線 [!DNL Sites] 只有一個遠端DAM部署的部署。

評估要連線至遠端DAM部署的最佳站台執行個體數量。 Adobe建議將Sites例項逐步連線至部署，並測試遠端DAM的效能是否不受影響，因為每個已連線的Sites例項都會對遠端DAM上的資料流量產生影響。

下列圖表說明支援的情境：

![連線資產架構](assets/connected-assets-architecture.png)

下圖說明不支援的情況：

![連線資產架構](assets/connected-assets-architecture-unsupported.png)

## 設定兩者之間的連線 [!DNL Sites] 和 [!DNL Assets] 部署 {#configure-a-connection-between-sites-and-assets-deployments}

一個 [!DNL Experience Manager] 管理員可建立此整合。 建立後，系統會透過使用者群組建立使用該整合所需的許可權。 使用者群組定義於 [!DNL Sites] 部署和DAM部署。

若要設定「連線資產」和本機 [!DNL Sites] 連線能力，請遵循下列步驟：

1. 存取現有的 [!DNL Sites] 部署，或使用下列命令建立部署：

   1. 在JAR檔案的資料夾中，在終端機上執行以下命令以建立每個 [!DNL Experience Manager] 伺服器。
      `java -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 幾分鐘後， [!DNL Experience Manager] 伺服器啟動成功。 考慮以下事項 [!DNL Sites] 將部署為網頁編寫的本機電腦，例如 `https://[local_sites]:4502`.

1. 確定具有適當範圍的使用者和角色存在於 [!DNL Sites] 部署和 [!DNL Assets] 在AMS部署。 建立技術使用者： [!DNL Assets] 部署並新增至中提及的使用者群組 [相關使用者和群組](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. 存取本機 [!DNL Sites] 部署位置 `https://[local_sites]:4502`. 按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. A **[!UICONTROL 標題]** 設定的。
   1. **[!UICONTROL 遠端DAM URL]** 為的URL [!DNL Assets] 格式中的位置 `https://[assets_servername]:[port]`.
   1. DAM 經銷商 (技術使用者) 的認證。
   1. 在 **[!UICONTROL 掛接點]** 欄位，輸入本機 [!DNL Experience Manager] 路徑，其中 [!DNL Experience Manager] 擷取資產。 例如， `remoteassets` 資料夾。 從DAM擷取的資產會儲存在上的此資料夾中， [!DNL Sites] 部署。
   1. **[!UICONTROL 本機站台URL]** 是的位置 [!DNL Sites] 部署。 [!DNL Assets] 部署使用此值來維護由此擷取的數位資產的參考 [!DNL Sites] 部署。
   1. 的認證 [!DNL Sites] 技術使用者。
   1. 的值 **[!UICONTROL 原始二進位傳輸最佳化臨界值]** 欄位會指定是否同步傳輸原始資產（包括轉譯）。 檔案大小較小的資產可隨時擷取，而檔案大小相對較大的資產則最適合非同步處理。 該值取決於您的網路功能。
   1. 選取 **[!UICONTROL 與連線資產共用的資料存放區]**，如果您使用資料存放區來儲存資產，且資料存放區在兩個部署之間共用。 在此情況下，臨界值限制並不重要，因為實際的資產二進位檔可在資料存放區上取得且不會傳輸。

   ![連線資產功能的典型設定](assets/connected-assets-typical-config.png)

   *圖：連線資產功能的典型設定。*

1. 上的現有數位資產 [!DNL Assets] 已經處理部署並產生轉譯。 系統會使用此功能來擷取這些轉譯，因此不需要重新產生轉譯。 停用工作流程啟動器，以防止重新產生轉譯。 調整上的啟動器設定([!DNL Sites])部署以排除 `connectedassets` 資料夾（資產會在此資料夾中擷取）。

   1. 開啟 [!DNL Sites] 部署，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 啟動器]**.

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. 在 [!UICONTROL 屬性] 精靈，變更 **[!UICONTROL 路徑]** 欄位做為下列對應，以更新其規則運算式來排除掛接點 **[!UICONTROL connectedassets]**.

   | 變更前 | 變更後 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作者擷取資產時，會擷取遠端部署上可用的所有轉譯。 若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。此 [!UICONTROL DAM更新資產] 工作流程會觸發，並建立更多轉譯。 這些轉譯專案僅在本機提供 [!DNL Sites] 而不是在遠端DAM部署上。

1. 新增 [!DNL Sites] 部署為CORS設定中允許的原始項，在 [!DNL Assets] 部署。 如需詳細資訊，請參閱 [瞭解CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. 設定 [相同網站Cookie支援](/help/sites-administering/same-site-cookie-support.md).

您可以檢查已設定組態之間的連線， [!DNL Sites] 部署和 [!DNL Assets] 部署。

![已設定連線資產的連線測試 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*圖：已設定連線資產的連線測試 [!DNL Sites].*

## 使用Dynamic Media資產 {#dynamic-media-assets}


使用「連線資產」，您可以使用透過以下方式處理的影像資產： [!DNL Dynamic Media] 從Sites頁面上的遠端DAM部署，並使用Dynamic Media功能，例如智慧型裁切和影像預設集。

使用 [!DNL Dynamic Media] 透過連線資產：

1. 設定 [!DNL Dynamic Media] 在已啟用同步模式的遠端DAM部署上。
1. 設定 [連線資產](#configure-a-connection-between-sites-and-assets-deployments).
1. 設定 [!DNL Dynamic Media] ，其公司名稱與遠端DAM上設定的公司名稱相同。 Sites部署必須擁有Dynamic Media帳戶的唯讀存取權，才能使用連線的資產。 因此，請務必在Sites例項的Dynamic Media設定中停用同步模式。

>[!CAUTION]
>
>透過連線資產和 [!DNL Dynamic Media] 設定，您無法使用 [!DNL Dynamic Media] 以處理上可用的本機資產 [!DNL Sites] 部署。

## 設定 [!DNL Dynamic Media] {#configure-dynamic-media}

進行設定 [!DNL Dynamic Media] 於 [!DNL Assets] 和 [!DNL Sites] 部署：

1. 啟用和設定 [!DNL Dynamic Media] 作為遠端上的全域設定 [!DNL Assets] 作者部署。 若要設定Dynamic Media，請參閱 [設定Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).
在遠端 [!DNL Assets] 部署，在 [!UICONTROL Dynamic Media同步模式]，選取 **[!UICONTROL 預設為啟用]**.

1. 建立「連線資產」設定，如所述 [設定網站與資產部署之間的連線](#configure-a-connection-between-sites-and-assets-deployments). 另外，選取 **[!UICONTROL 擷取Dynamic Media連線資產的原始轉譯]** 選項。

1. 設定 [!DNL Dynamic Media] 在本機 [!DNL Sites] 和遠端 [!DNL Assets] 部署。 依照指示進行 [設定 [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * 在所有設定中使用相同的公司名稱。
   * 在本機 [!DNL Sites]，在 [!UICONTROL Dynamic Media同步模式]，選取 **[!UICONTROL 預設為停用]**. 此 [!DNL Sites] 部署必須擁有對的唯讀存取權 [!DNL Dynamic Media] 帳戶。
   * 在本機 [!DNL Sites]，在 **[!UICONTROL 發佈資產]** 選項，選取 **[!UICONTROL 選擇性發佈]**. 不要選取 **[!UICONTROL 同步處理所有內容]**.

1. 啟用 [[!DNL Dynamic Media] 影像核心元件中的支援](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). 此功能會啟用預設值 [影像元件](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) 以顯示 [!DNL Dynamic Media] 影像時間 [!DNL Dynamic Media] 作者在本機網頁中使用影像 [!DNL Sites] 部署。

## 使用遠端資產 {#use-remote-assets}

網站作者使用「內容尋找器」連線至DAM部署。 作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要向遠端DAM驗證，請備妥管理員提供的認證（如有）。

作者可以在單一網頁中使用本機DAM和遠端DAM部署上可用的資產。 使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

系統只會擷取具有完全對應標籤以及本機可用的相同分類階層的遠端資產標籤 [!DNL Sites] 部署。 其他所有標籤會一概捨棄。作者可使用遠端裝置上的所有標籤來搜尋遠端資產 [!DNL Experience Manager] 部署，因為它提供全文檢索搜尋。

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. 導覽至 [!DNL Assets] 存取遠端部署上的介面 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** 從 [!DNL Experience Manager] 工作區。 或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。
1. 在 [!DNL Sites] 部署，在右上角的設定檔啟動器中，按一下 **[!UICONTROL 模擬為]**. 輸入 `ksaner` 作為使用者名稱，選取畫面上提供的選項，然後按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 在&#x200B;**[!UICONTROL 「Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL tw]** > **[!UICONTROL zh」]**&#x200B;開啟「We.Retail」網頁。編輯頁面。或者，您也可以在瀏覽器中存取 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html`，進而編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. 開啟 [!UICONTROL 資產] 索引標籤（遠端內容尋找器）並按一下 **[!UICONTROL 登入連線資產]**.
1. 提供憑證 `ksaner` 作為使用者名稱，且以 `password` 作為密碼。此使用者對以下兩個專案均具有編寫許可權： [!DNL Experience Manager] 部署。
1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   擷取的資產在本機上是唯讀的 [!DNL Sites] 部署。 您仍然可以使用您提供的選項 [!DNL Sites] 元件，以編輯所擷取的資產。 由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端DAM上搜尋資產時，篩選檔案型別和影像的選項。*

1. 如果資產的原始檔案是以非同步方式擷取，且擷取任務失敗，網站作者會收到通知。 編寫過程中或甚至在完成編寫之後，作者都能在「 」中檢視擷取任務和錯誤的詳細資訊 [非同步作業](/help/sites-administering/asynchronous-jobs.md) 使用者介面。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：背景中非同步擷取資產作業的相關通知。*

1. 發佈頁面時， [!DNL Experience Manager] 顯示頁面上使用之資產的完整清單。 請確認發佈時，系統已成功擷取遠端資產。若要檢查每個所擷取資產的狀態，請參閱 [非同步作業](/help/sites-administering/asynchronous-jobs.md) 使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未完全擷取，頁面還是會發佈。 此 [!DNL Experience Manager] 通知區域會顯示通知，指出非同步作業頁面中顯示的錯誤。

>[!CAUTION]
>
>擷取的遠端資產一旦用於網頁中，只要任何人有權存取本機資料夾，都可以搜尋和使用。 擷取的資產會儲存在本機資料夾中(`connectedassets` 在上述逐步說明中)。 這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

### 檢查跨網頁資產的使用情況 {#asset-usage-references}

[!DNL Experience Manager] 可讓DAM使用者檢查資產的所有參考。 它有助於瞭解和管理遠端資產的使用 [!DNL Sites] 和在複合資產中。 許多網頁作者於 [!DNL Experience Manager Sites] 部署可以使用遠端上的資產 [!DNL Assets] 在不同的網頁中。 若要簡化資產管理，避免導致參照損毀，DAM使用者務必要檢查本機與遠端網頁上資產的使用情形。 此 [!UICONTROL 引用] 索引標籤在資產的 [!UICONTROL 屬性] 頁面會列出資產的本機與遠端參考。

若要檢視及管理以下專案上的參照： [!DNL Assets] 部署，請遵循下列步驟：

1. 選取中的資產 [!DNL Assets] 主控台並按一下 **[!UICONTROL 屬性]** 工具列中的。
1. 按一下 **[!UICONTROL 引用]** 標籤。 另請參閱 **[!UICONTROL 本機參考]** 以在上使用資產 [!DNL Assets] 部署。 請參閱**[!UICONTROL 遠端參考] 用於上的資產 [!DNL Sites] 使用「連線資產」功能擷取資產的部署。

   ![資產「屬性」頁面中的遠端參考](assets/connected-assets-remote-reference.png)

1. 的參照 [!DNL Sites] 頁面會顯示每個本機的參照總數 [!DNL Sites]. 尋找所有參照並顯示參照總數可能需要一些時間。
1. 引用清單是互動式的，DAM使用者可以按一下引用以開啟引用頁面。 如果由於某種原因無法擷取遠端參考，則會顯示通知，通知使用者發生失敗。
1. 使用者可以移動或刪除資產。 移動或刪除資產時，所有選定資產/資料夾的參照總數會顯示在警告對話方塊中。 刪除尚未擷取參考的資產時，會顯示警告對話方塊。

   ![強制刪除警告](assets/delete-referenced-asset.png)

### 管理遠端DAM中資產的更新 {#manage-updates-in-remote-dam}

晚於 [設定連線](#configure-a-connection-between-sites-and-assets-deployments) 在遠端DAM和之間 [!DNL Sites] 部署，遠端DAM上的資產可在 [!DNL Sites] 部署。 然後，您可以在遠端DAM資產或資料夾上執行更新、刪除、重新命名和移動操作。 更新會在 [!DNL Sites] 部署。 此外，若在本機使用遠端DAM上的資產 [!DNL Experience Manager Sites] 頁面上，對遠端DAM上資產的更新會顯示在 [!DNL Sites] 頁面。

將資產從一個位置移動至另一個位置時，請確定 [調整引用](/help/assets/manage-assets.md) 好讓資產顯示在 [!DNL Sites] 頁面。 如果您將資產移至無法從本機存取的位置 [!DNL Sites] 部署，資產無法在Sites部署上顯示。

您也可以更新遠端DAM上資產的中繼資料屬性，而變更可在本機使用 [!DNL Sites] 部署。

[!DNL Sites] 作者可預覽以下頁面上的可用更新： [!DNL Sites] 部署，然後重新發佈變更，以便在 [!DNL Experience Manager] 發佈執行個體。

[!DNL Experience Manager] 在中顯示資產的已過期狀態視覺指示器 `Remote Assets Content Finder` 以阻止網站作者在網站上使用資產 [!DNL Sites] 頁面。 如果您使用的資產在 [!DNL Sites] 頁面上，資產無法顯示於 [!DNL Experience Manager] 發佈執行個體。

## 常見問題 {#frequently-asked-questions}

+++**若您需要使用上可用的資產，您應設定「連線資產」。 [!DNL Sites] 部署？**

在這種情況下，不需要設定連線資產。 您可以使用上的可用資產 [!DNL Sites] 部署。

+++

+++**您何時需要設定「連線資產」功能？**

只有在您需要使用上遠端DAM部署中的可用資產時，才設定「連線資產」功能 [!DNL Sites] 部署。

+++

+++**您可以連線多個 [!DNL Sites] 在設定「連線的資產」之後部署到遠端DAM部署？**

是，您可以連線多個 [!DNL Sites] 在設定「連線的資產」之後部署到遠端DAM部署。 如需詳細資訊，請參閱 [連線資產架構](#connected-assets-architecture).

+++

+++**您可以連線到多少個遠端DAM部署 [!DNL Sites] 在設定「連線資產」後進行部署？**

您可以將一個遠端DAM部署連線至 [!DNL Sites] 在設定「連線資產」之後進行部署。 如需詳細資訊，請參閱 [連線資產架構](#connected-assets-architecture).

+++

+++**您是否能使用您網站上的Dynamic Media資產？ [!DNL Sites] 在設定「連線資產」後進行部署？**

設定「連線資產」後， [!DNL Dynamic Media] 資產位於 [!DNL Sites] 以唯讀模式部署。 因此，您無法使用 [!DNL Dynamic Media] 若要處理上的資產，請 [!DNL Sites] 部署。 如需詳細資訊，請參閱 [設定Sites與Dynamic Media部署之間的連線](#dynamic-media-assets).

+++

+++**您是否能使用上遠端DAM部署的影像和檔案格式型別資產？ [!DNL Sites] 在設定「連線資產」後進行部署？**

可以，您可以在「 」上使用遠端DAM部署的影像和檔案格式型別資產 [!DNL Sites] 在設定「連線資產」之後進行部署。

+++

+++**您是否能使用上遠端DAM部署的內容片段和視訊資產？ [!DNL Sites] 在設定「連線資產」後進行部署？**

否，您無法使用位於上的遠端DAM部署的內容片段和視訊資產 [!DNL Sites] 在設定「連線資產」之後進行部署。

+++

+++**您能否在上使用遠端DAM部署的Dynamic Media資產 [!DNL Sites] 在設定「連線資產」後進行部署？**

是，您可以從上的遠端DAM部署設定及使用Dynamic Media影像資產 [!DNL Sites] 在設定「連線資產」之後進行部署。 如需詳細資訊，請參閱 [設定Sites與Dynamic Media部署之間的連線](#dynamic-media-assets).

+++

+++**設定「連線資產」後，您能否對遠端DAM資產或資料夾執行更新、刪除、重新命名和移動操作？**

是，在設定「連線資產」後，您可以在遠端DAM資產或資料夾上執行更新、刪除、重新命名和移動操作。 這些更新會在Sites部署中自動提供，但會有一些延遲。 如需詳細資訊，請參閱 [管理遠端DAM中資產的更新](#handling-updates-to-remote-assets).

+++

+++**設定「連線資產」後，您能否在 [!DNL Sites] 部署，並使其可用於遠端DAM部署？**

您可以將資產新增至 [!DNL Sites] 但是，部署這些資產無法用於遠端DAM部署。

+++

## 限制和最佳實務 {#tip-and-limitations}

* 若要取得資產使用方式的深入分析，請設定 [Assets Insight](/help/assets/asset-insights.md) 上的功能 [!DNL Sites] 執行個體。

* 您無法將遠端資產拖曳至 [影像元件設定對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=en#configure-dialog). 不過，您可以直接將遠端資產拖曳至Sites頁面上的影像元件，而不需按一下 **[!UICONTROL 設定]**.

### 許可權與資產管理 {#permissions-and-managing-assets}

* 本機資產為唯讀副本。[!DNL Experience Manager] 元件會對資產執行非破壞性編輯。 不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 僅支援影像和列出的文件格式。[!DNL Content Fragments] 和 [!DNL Experience Fragments] 不受支援。
* [!DNL Experience Manager] 不會擷取中繼資料結構。 這表示可能不會顯示所有擷取的中繼資料。 如果結構描述單獨更新，在 [!DNL Sites] 部署，則會顯示所有中繼資料屬性。
* 全部 [!DNL Sites] 即使作者無法存取遠端DAM部署，作者仍擁有擷取副本的讀取許可權。
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。請參閱[資產移轉指南](assets-migration-guide.md)。
* 無法使用遠端資產作為上的頁面縮圖 [!UICONTROL 頁面屬性] 使用者介面。 您可以在下列位置設定網頁縮圖： [!UICONTROL 頁面屬性] 來自的使用者介面 [!UICONTROL 縮圖] 按一下 [!UICONTROL 選取影像].

### 設定和授權 {#setup-licensing}

* [!DNL Assets] 部署於 [!DNL Adobe Managed Services] 支援。
* [!DNL Sites] 可以連線至單一 [!DNL Assets] 一次部署。
* 的授權 [!DNL Assets] 必須使用遠端存放庫。
* 的一或多個授權 [!DNL Sites] 需要以本機編寫部署方式運作。

### 使用情況 {#usage}

* 使用者可在編寫時搜尋遠端資產，並將這些資產拖曳至本機頁面。 不支援其他功能。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。作者可從拖曳遠端資產重新嘗試 [!UICONTROL 內容尋找器] 至 [!UICONTROL 頁面編輯器].
* 非破壞性的簡單編輯作業，以及透過支援的編輯工作 `Image` 元件時，才能對擷取的資產執行此操作。 資產僅供唯讀。
* 重新擷取資產的唯一方法是將其拖曳至頁面上。 沒有API支援或其他方法可重新擷取資產以進行更新。
* 如果資產從DAM解除委任，這些資產將繼續用於 [!DNL Sites] 頁面。
* 系統會非同步擷取資產的遠端參考專案。 參考資料與總計數並非即時，如果Sites作者在DAM使用者檢視參考資料時使用資產，則可能會有一些差異。 DAM使用者可以重新整理頁面，並在幾分鐘後重試以取得總計數。

## 疑難排解問題 {#troubleshoot}

若要疑難排解常見錯誤，請遵循下列步驟：

* 如果您無法從搜尋遠端資產， [!UICONTROL 內容尋找器]，然後確定已具備所需的角色和許可權。

* 由於一個或多個原因，從遠端DAM擷取的資產可能不會發佈在網頁上。 遠端伺服器上沒有擷取檔案，缺少擷取檔案的適當許可權，或是網路故障可能是原因。 確保資產沒有從遠端DAM移除。 確保有適當的許可權且符合先決條件。 再次嘗試將資產新增至頁面並重新發佈。 檢查[非同步工作清單](/help/sites-administering/asynchronous-jobs.md)，找出資產擷取作業的錯誤。

* 如果您無法從本機存取遠端DAM部署 [!DNL Sites] 部署，確定允許跨網站Cookie，並且 [相同網站Cookie支援](/help/sites-administering/same-site-cookie-support.md) 已設定。 如果跨網站Cookie遭到封鎖，則部署 [!DNL Experience Manager] 可能無法驗證。 例如， [!DNL Google Chrome] 可能會封鎖第三方Cookie。 允許Cookie進入 [!DNL Chrome] 瀏覽器，按一下位址列中的「眼睛」圖示，導覽至 **網站無法運作** > **已封鎖**，選取遠端DAM URL，並允許登入權杖Cookie。 或者，請參閱 [如何啟用第三方Cookie](https://support.google.com/chrome/answer/95647).

  ![無痕模式中Chrome瀏覽器的Cookie錯誤](assets/chrome-cookies-incognito-dialog.png)

* 如果您無法從Managed Servicesas a Cloud ServiceSites部署存取AdobeExperience Manager Sites遠端DAM部署，請更新 `aem_author.vhost` 檔案，位於 `"/etc/httpd/conf.d/available_vhosts`，讓遠端DAM在Dispatcher設定中包含以下標頭：

  ```xml
  Header Set Access-Control-Allow-Origin <Local Sites instance host>
  Header Set Access-Control-Allow-Credentials true
  ```

* 如果未擷取遠端參考並導致錯誤訊息，請檢查 [!DNL Sites] 部署可用，並檢查網路連線問題。 請稍後重試以檢查。 [!DNL Assets] 部署嘗試與建立連線兩次 [!DNL Sites] 部署，然後報告失敗。

  ![無法擷取資產遠端參考](assets/reference-report-failure.png)

* 如果Cookie不是從Sites伺服器傳送到Google Chrome中的Assets伺服器，這是因為Assets連線不是透過HTTPS。 如果您沒有在Assets執行個體上使用HTTPS，則 `SameSite=None` 使用Assets伺服器驗證後，無法將標頭新增至回應。

