---
title: 發行說明 [!DNL Adobe Experience Manager Assets] 6.5。
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]的新功能和增強功能。'
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager Assets] 發行說明  {#aem-assets-release-notes}

以下是[!DNL Adobe Experience Manager] 6.5 [!DNL Assets]版本的主要功能和亮點。

## 與[!DNL Adobe Creative Cloud]和創意工作流程{#integration-with-adobe-creative-cloud-and-creative-workflows}整合

[!DNL Adobe Experience Manager] 提供多種方式來整合與 [!DNL Adobe Creative Cloud] 共用資產，以便在創意與行銷或商業團隊緊密協作的工作流程中使用。[!DNL Experience Manager] 6.5繼續改進整合，並進一步簡化整合，以發掘更多機會並簡化現有方法。

閱讀以瞭解[!DNL Experience Manager] 6.5的特定功能和整合，以最佳化支援內容速度使用案例。

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] 加強創意人員與行銷人員在內容建立流程中的協作。創意人員可存取儲存在[!DNL Experience Manager Assets]中的內容，而不需離開他們最熟悉的應用程式。 創作人員可使用[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]應用程式中的應用程式內面板，順暢地瀏覽、搜尋、結帳和登入資產。

[!DNL Adobe Asset Link] 是適用於企 [業的Creative Cloud產](https://www.adobe.com/creativecloud/business/enterprise.html) 品的一部分。如需詳細資訊，包括部署[!DNL Experience Manager]的必要設定，請參閱[Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

![在Adobe Photoshop中搜尋資產](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] 整合  {#stock}

貴組織可在[!DNL Experience Manager Assets]內使用其[!DNL Adobe Stock]企業計畫，以確保授權資產廣泛適用於您的創意和行銷專案。 您可以使用[!DNL Experience Manager]的強大DAM功能，快速尋找、預覽並授權儲存在Experience Manager中的[!DNL Adobe Stock]資產。

[!DNL Adobe Stock] 服務可讓設計人員和企業針對其所有創意專案，取用數百萬個高品質、優質且免版稅的像片、向量、插圖、視訊、範本和3D資產。

如需詳細資訊，請參閱「在Experience Manager資產中使用Adobe Stock資產」[。](/help/assets/aem-assets-adobe-stock.md)

![從Experience Manager Assets預覽Adobe Stock影像和授權](assets/stock_image_preview_license_options.png)

*圖：從內 [!DNL Adobe Stock] 部預覽影像和授權 [!DNL Experience Manager Assets]。*

![在Experience Manager中搜尋及篩選已授權的Adobe Stock影像](assets/aem-search-filters2.jpg)

*圖：在中搜尋及篩選 [!DNL Adobe Stock] 授權影像 [!DNL Experience Manager]。*

### [!DNL Adobe InDesign] {#dynamic-references-in-indesign}中的動態引用

[!DNL Experience Manager Assets] 用於檔案 [!DNL Adobe InDesign] 中是動態的。如果引用的資產在儲存庫中移動，則引用會自動更新。 如需詳細資訊，請參閱[如何管理複合資產](/help/assets/managing-linked-subassets.md)。

## 品牌入口網站功能{#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 協助您透過各種裝置輕鬆取得、有效控制並安全地將已核准的資產發佈給外部廠商／代理商和內部商業使用者。它有助於提高資產分享的效率，加速資產上市時間，並消除不合規使用和未經授權存取的風險。

如需詳細資訊，請參閱[品牌入口網站的新增功能](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html)。

## 連線資產 {#connectedassets}

在大型企業中，建立網站所需的基礎架構可以分散。 有時，網站建立功能和所需的數位資產會處在不同的孤島中。

[!DNL Experience Manager Sites] 提供建立網頁的功能，而 是可為網站提供必要資產的數位資產管理 (DAM) 系統。[!DNL Experience Manager Assets][!DNL Experience Manager] 現在可透過整合和來支援上述使 [!DNL Sites] 用案例 [!DNL Assets]。請參閱[如何設定和使用「已連接的資產」功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![將資產從部署拖 [!DNL Experience Manager] 曳至不 [!DNL Sites] 同部署的頁 [!DNL Experience Manager] 面](assets/connected-assets-drag-and-drop-only.gif)

*圖：將資產從不同部 [!DNL Experience Manager] 署的頁 [!DNL Sites] 面上的部署拖 [!DNL Experience Manager] 曳。*

## 動態媒體 {#dynamic-media}

[!DNL Dynamic Media] 提供增強的豐富式媒體製作與發佈， [!DNL Experience Manager Assets] 以提供如臨現場且個人化的尖端體驗。透過上傳單一高品質的主資產，並使用我們的進階雲端演算和檢視器，您可以即時提供任何轉譯組合，以支援組織的媒體策略。

有關新[!DNL Dynamic Media]功能的詳細資訊，請參閱[動態媒體發行說明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)。

### 360視訊支援{#video-support}

使用尖端檢視器直接在[!DNL Experience Manager]中管理360視訊檔案，將VR體驗發佈至桌上型電腦、行動裝置和VR頭戴式裝置。 如需詳細資訊，請參閱[使用360視訊](/help/assets/360-video.md)。

### 自訂視訊縮圖{#custom-video-thumbnails}

您現在可以使用視訊本身的影格或儲存在DAM中的其他內容，自訂視訊資產的縮圖。 如需其他指示，請參閱[關於視訊縮圖](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

### 協助工具增強功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 檢視器現在支援增強的協助工具功能，例如Aria支援、螢幕閱讀程式和Alt-text。如需詳細資訊，請參閱[動態媒體檢視器發行說明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html)。

## 搜尋體驗增強功能{#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5之後，行銷人員可以更快速地從搜尋結果頁面發現所需資產。即使在套用搜尋篩選器之前，搜尋Facet也會以資產數目進行更新。 查看篩選的預期計數有助於使用者有效率地瀏覽搜尋結果。 如需詳細資訊，請參閱「在Experience Manager中搜尋資產」[。](../assets/search-assets.md)

![在搜尋刻面中查看資產數量，而不篩選搜尋結果](/help/assets/assets/asset_search_results_in_facets_filters.png)

*圖：在搜尋刻面中查看資產數目，而不篩選搜尋結果。*

## 可用性增強{#usability-enhancement}

您現在可以選擇資料夾內或搜尋結果中的所有載入資產。 它可協助您快速管理多個資產。 此核取方塊會選取符合藍本的所有資產，例如搜尋結果，而不只是[!DNL Experience Manager]介面中可見的資產。

![使用「全選」選項，只要按一下，即可選取所有載入的資產。](assets/select-all-in-aem-assets.gif)

*圖：使用「全選」選項，只要按一下，即可選取所有載入的資產。*

## 中繼資料增強功能{#metadata-enhancements}

[!DNL Assets] 可讓您為資產資料夾建立中繼資料結構，以定義資料夾屬性頁面中顯示的配置和中繼資料。您現在可以將資料夾元資料架構分配給現有資料夾或建立新資料夾。 如需詳細資訊，請參閱[資料夾中繼資料結構](/help/assets/metadata-config.md#folder-metadata-schema)。

指定階層式中繼資料時，可在執行時期從JSON檔案載入選項，例如，而不需在表單中手動輸入。 如需詳細資訊，請參閱[階層式中繼資料](/help/assets/metadata-schemas.md#cascading-metadata)。

## 報告增強功能{#reporting-enhancements}

「內容片段」和連結分享現在會包含在下載的報表中。 如需詳細資訊，請參閱[資產報表](/help/assets/asset-reports.md)。
