---
title: ' [!DNL Adobe Experience Manager Assets]簡介。'
description: 瞭解什麼是數位資產管理、其使用案例，以及 [!DNL Adobe Experience Manager Asset] 產品。
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 12%

---


# 關於[!DNL Adobe Experience Manager Assets]作為DAM解決方案{#administering-assets}

[!DNL Assets] 是數位資產管理(DAM)工具，是平台的一個組成部分，可 [!DNL Experience Manager] 讓您的企業管理和分發數位資產。組織內的使用者可以管理、儲存和存取多種類型的數位資產，例如影像、視訊、檔案、音訊剪輯、3D檔案和多媒體，以便用於網路、平面印刷和數位散發。

## 什麼是數位資產管理？{#what-is-digital-asset-management}

[!DNL Assets] 提供企業內部共用和分發組織的重要數位資產。組織內的使用者可以透過Web介面（或CIFS或WebDAV資料夾）儲存、管理和存取數位資產，例如影像、圖形、音訊、視訊和檔案。

[!DNL Assets] 功能 [!DNL Experience Manager] 可讓您執行下列動作：

* 新增及共用各種檔案格式的影像、文件、音訊檔案與視訊檔案。
* 依標籤、燈箱或星號（您的最愛）將資產分組，以管理資產。 為資產加上註解。
* 搜尋檔案名稱、文件全文，以及搜尋日期、文件類型和標記，來尋找資產。
* 新增或編輯資產的中繼資料資訊。中繼資料會自動與對應的資產一起更新版本。 您可以匯入或匯出資產中繼資料。
* 執行影像編輯功能，例如縮放和新增影像濾鏡。 使用WebDAV或CIFS資料夾同時匯入和匯出多個數位資產。
* 使用工作流程和通知，允許共同處理和下載任何資產集，並管理資產的存取權。

### [!DNL Experience Manager Assets] 與  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 完全整合併 [!DNL Sites] 順暢地運作於所有使用案例。例如，在製作網頁時，[!DNL Sites]作者可以透過Content Finder尋找和使用數位資產。 [!DNL Assets]的用戶介面與[!DNL Sites]的用戶介面相同。 如需詳細資訊，請參閱[網站概觀](/help/sites-authoring/page-authoring.md)。

基本用戶介面與[!DNL Sites]的基本用戶介面相同。 如需詳細資訊，請參閱[網站概觀](/help/sites-authoring/page-authoring.md)。

### 數位資產管理與影像元件{#digital-asset-management-versus-image-component}

在確定要將映像放入DAM儲存庫或使用映像元件時，請考慮映像生命週期：

* 如果影像的生命週期與頁面相同，請使用影像元件。
* 例如，如果影像具有單獨的生命週期，如果使用兩次或在WCM外使用影像，則使用[!DNL Assets]。

## 什麼是數位資產？{#what-are-digital-assets}

資產是數位檔案、影像、視訊或音訊（或其一部分），可以有多個轉譯，也可以有子資產（例如，photoshop檔案中的圖層、PowerPoint檔案中的投影片、PDF中的頁面、ZIP中的檔案）。

資產基本上是二進位加中繼資料加轉譯加子資產。如需詳細資訊，請參閱[DAM效能指南](/help/sites-deploying/assets-performance-sizing.md)。

>[!CAUTION]
>
>上傳和／或編輯大量資產（尤其是影像）可能會影響[!DNL Experience Manager]部署的效能。

### [!DNL Experience Manager Assets] 術語  {#aem-assets-terminology}

在[!DNL Experience Manager]中使用數位資產時，您需要瞭解下列術語：

* **系列**:資產的集合，根據實體位置（資料夾）、常用屬性（儲存的搜尋資料夾）或使用者選擇（燈箱資料夾）。

* **元數** [!DNL Assets] 據包元資料；例如，作者、過期日期、DRM資訊（數位版權管理）等。中繼資料受到存取控制。 [!DNL Assets] 支援以下各種現成的常用元資料模式：

   * Dublin Core:包括作者、說明、日期、主旨等。
   * IPTC:包括事件、模型、位置等。
   * WCM:包括頁面屬性、[!UICONTROL On Time]和[!UICONTROL Off Time]等。

* **標籤**: [!DNL Assets] 可以標籤和分類。請參閱[組織資產](/help/assets/organize-assets.md)。

* **轉譯**:轉譯是資產的二進位表示法。[!DNL Assets] 一律有主要表示法——上傳檔案的主要表示法。它們可以有不限數量的其他表示法，例如，可能是由自訂的工作流程步驟或在上傳資產時所建立。轉譯可能有不同大小、不同解析度、加上浮水印，或其他某個已變更的特性。

* **版本**:版本修訂會在特定時間點建立數位資產的快照。您可以將資產還原為舊版。 請參閱Assets](manage-assets.md#asset-versioning)中的[版本控制。

* **子資產**:子資產是組成資產的資產，例如，檔案中的圖層或PDF [!DNL Adobe Photoshop] 檔案中的頁面。在[!DNL Assets]中，您可以像管理資產一樣管理子資產。

### 如何使用資產{#how-to-work-with-assets}

您可以對資產或系列執行動作。 動作可以建立或修改資產、系列和轉譯。 您對資產執行的許多基本動作——上傳、刪除、更新、儲存子資產——會觸發預先設定的工作流程。 這些功能在[!DNL Assets]中自動開啟，並在[!DNL Assets]媒體處理常式中詳細說明。

您可以使用這些預先設定的工作流程執行的工作：

* 將資產儲存在儲存庫中，或從中刪除資產。
* 擷取及儲存資產的中繼資料；個別的中繼資料項目會儲存為XMP。
* 產生資產的轉譯和縮圖；包括視需要自動調整大小和裁切。
* 視需要轉碼資產。 例如，行動與網路使用的視訊會轉碼為每秒24個畫格，下載每秒30個畫格的視訊。 行動與網路使用的音訊會以128 Kbps轉碼，以192 Kbps的音訊下載。

當然，您也可以手動套用工作流程。 如需預設工作流程的清單，請參閱[資產媒體處理常式](/help/assets/media-handlers.md)。

## [!DNL Experience Manager Assets] 和  [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

有關差異的資訊，請參閱[資產和MediaLibrary](/help/assets/medialibrary.md)。
