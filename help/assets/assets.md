---
title: ' [!DNL Adobe Experience Manager Assets] 簡介'
description: 了解什麼是數位資產管理、其使用案例，以及 [!DNL Adobe Experience Manager Asset] 產品。
contentOwner: AG
feature: 資產管理
role: Leader, Architect, Business Practitioner
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 12%

---

# 關於[!DNL Adobe Experience Manager Assets]作為DAM解決方案{#administering-assets}

[!DNL Assets] 是數位資產管理(DAM)工具，是平台的必要部分，可 [!DNL Experience Manager] 讓您的企業管理和發佈數位資產。整個組織的使用者可以管理、儲存及存取許多類型的數位資產，例如影像、影片、檔案、音訊剪輯、3D檔案和多媒體，以用於網路、印刷品和數位散發。

## 什麼是數位資產管理？{#what-is-digital-asset-management}

[!DNL Assets] 提供組織關鍵數位資產的全企業共用和分發。整個組織的用戶可以通過Web介面（或CIFS或WebDAV資料夾）儲存、管理和訪問數字資產，如影像、圖形、音頻、視頻和文檔。

[!DNL Assets] 的功 [!DNL Experience Manager] 能可讓您執行下列動作：

* 新增及共用各種檔案格式的影像、文件、音訊檔案與視訊檔案。
* 依標籤、燈箱或星號（您的最愛）將資產分組，以管理資產。 為資產加上註解。
* 搜尋檔案名稱、文件全文，以及搜尋日期、文件類型和標記，來尋找資產。
* 新增或編輯資產的中繼資料資訊。中繼資料會自動與對應的資產版本結合。 您可以匯入或匯出資產中繼資料。
* 執行影像編輯功能，例如縮放和新增影像濾鏡。 使用WebDAV或CIFS資料夾同時導入和導出多個數字資產。
* 使用工作流程和通知，以允許聯合處理和下載任何資產集，並管理資產的存取權限。

### [!DNL Experience Manager Assets] 與整合  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 與完整整合， [!DNL Sites] 並可順暢地用於所有使用案例。例如，在製作網頁時，[!DNL Sites]作者可以透過「內容尋找器」來尋找和使用數位資產。 [!DNL Assets]的用戶介面與[!DNL Sites]的用戶介面相同。 如需完整詳細資訊，請參閱[Sites](/help/sites-authoring/page-authoring.md)概觀。

基本用戶介面與[!DNL Sites]的介面相同。 如需完整詳細資訊，請參閱[網站概觀](/help/sites-authoring/page-authoring.md)。

### 數位資產管理與影像元件{#digital-asset-management-versus-image-component}

判斷要將影像放入DAM存放庫或使用影像元件時，請考量影像生命週期：

* 如果影像的生命週期與頁面相同，請使用影像元件。
* 例如，如果影像具有單獨的生命週期，則使用影像兩次或在WCM外使用，則使用[!DNL Assets]。

## 什麼是數位資產？{#what-are-digital-assets}

資產是數位檔案、影像、視訊或音訊（或其中一部分），可以多次轉譯也可以有子資產（例如photoshop檔案中的圖層、PowerPoint檔案中的投影片、PDF中的頁面、ZIP中的檔案）。

資產基本上是二進位加中繼資料加轉譯加子資產。如需詳細資訊，請參閱[DAM效能指南](/help/sites-deploying/assets-performance-sizing.md) 。

>[!CAUTION]
>
>上傳和/或編輯大量資產（尤其是影像）可能會影響[!DNL Experience Manager]部署的效能。

### [!DNL Experience Manager Assets] 術語  {#aem-assets-terminology}

在[!DNL Experience Manager]中使用數位資產時，您需要了解下列術語：

* **集合**:資產的集合，根據實體位置（資料夾）、通用屬性（儲存的搜尋資料夾）或使用者選取項目（燈箱資料夾）。

* **** [!DNL Assets] 中繼資料包中繼資料；例如作者、到期日、DRM資訊(Digital Rights Management)等。中繼資料受存取控制。 [!DNL Assets] 支援下列各種現成的通用中繼資料結構：

   * 都柏林核心：包括作者、說明、日期、主旨等。
   * IPTC:包括事件、模型、位置等。
   * WCM:包括頁面屬性、[!UICONTROL 開啟時間]和[!UICONTROL 關閉時間]等。

* **標籤**: [!DNL Assets] 可加以標籤和分類。請參閱[組織資產](/help/assets/organize-assets.md)。

* **轉譯**:轉譯是資產的二進位表示法。[!DNL Assets] 一律有主要表示法 — 上傳之檔案的主要表示法。它們可以有不限數量的其他表示法，例如，可能是由自訂的工作流程步驟或在上傳資產時所建立。轉譯可能有不同大小、不同解析度、加上浮水印，或其他某個已變更的特性。

* **版本**:版本設定會在特定時間點建立數位資產的快照。您可以將資產還原為舊版。 請參閱 [!DNL Assets]](manage-assets.md#asset-versioning)中的[版本設定。

* **子資產**:子資產是組成資產的資產，例如檔案中的圖層 [!DNL Adobe Photoshop] 或PDF檔案中的頁面。在[!DNL Assets]中，您可以像管理資產一樣管理子資產。

### 如何使用數位資產{#how-to-work-with-assets}

您對資產或集合執行動作。 動作可以建立或修改資產、集合和轉譯。 您對資產執行的許多基本動作（上傳、刪除、更新、儲存子資產）會觸發預先設定的工作流程。 這些在[!DNL Assets]中會自動開啟，並在[!DNL Assets]媒體處理常式中詳細說明。

您可以使用這些預先設定的工作流程來執行的工作：

* 將資產儲存在存放庫中，或從中刪除資產。
* 擷取及儲存資產的中繼資料；個別中繼資料項目會儲存為XMP。
* 產生資產的轉譯和縮圖；包括視需要自動調整大小和裁切。
* 視需要轉換資產代碼。 例如，行動裝置和網頁使用的視訊會以每秒24個畫面進行轉碼，下載以每秒30個畫面的視訊。 使用行動裝置和網頁的音訊會以128 Kbps轉碼，下載則以192 Kbps轉碼。

當然，您也可以手動套用工作流程。 如需預設工作流程的清單，請參閱[Assets媒體處理常式](media-handlers.md)。

## [!DNL Experience Manager Assets] 和  [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

如需差異的相關資訊，請參閱[資產和Media Library](medialibrary.md)。

>[!MORELIKETHIS]
>
>* [影片簡介 — 將資產Experience Manager為現代DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [了解中繼資料概念](/help/assets/metadata-concepts.md)

