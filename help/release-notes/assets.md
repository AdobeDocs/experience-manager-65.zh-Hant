---
title: ' [!DNL Adobe Experience Manager Assets] 6.5的發行說明。'
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]的新功能和增強。'
exl-id: 6d9c9f09-ea42-43fb-98f7-12ce82d308bf
source-git-commit: 62544559020b0c0afd7bb31fb832b82ba3d47919
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets] 發行說明 {#aem-assets-release-notes}

以下是[!DNL Adobe Experience Manager] 6.5 [!DNL Assets]版本的主要功能和重點。

## 與[!DNL Adobe Creative Cloud]和創意工作流程整合 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 提供多種方式來與整合 [!DNL Adobe Creative Cloud] 和共用資產，以便用於創意與行銷或業務團隊密切合作的工作流程。[!DNL Experience Manager] 6.5繼續改進整合工作，並進一步精簡整合工作，以揭示更多機會和精簡現有方法。

請閱讀下文，了解[!DNL Experience Manager] 6.5的特定功能和整合，以便您最能支援內容速度使用案例。

### Adobe資產連結 {#aal}

[!DNL Adobe Asset Link] 加強創意人員與行銷人員在內容建立程式中的協作。創作者可以存取儲存在[!DNL Experience Manager Assets]中的內容，而不需離開他們最熟悉的應用程式。 創意人員可使用[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]應用程式中的應用程式內面板，順暢地瀏覽、搜尋、簽出和簽入資產。

[!DNL Adobe Asset Link] 是企業產品 [Creative Cloud的](https://www.adobe.com/creativecloud/business/enterprise.html) 一部分。有關詳細資訊，包括[!DNL Experience Manager]部署的必要配置，請參閱[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

![在Adobe Photoshop中搜尋資產](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] 整合 {#stock}

貴組織可在[!DNL Experience Manager Assets]內使用其[!DNL Adobe Stock]企業計畫，確保授權資產可廣泛用於您的創意和行銷專案。 您可以使用[!DNL Experience Manager]的強大DAM功能，快速尋找、預覽和授權儲存在Experience Manager中的[!DNL Adobe Stock]資產。

[!DNL Adobe Stock] 該服務為設計人員和企業提供數百萬張高質量、精心策劃、免版稅的照片、向量圖、插圖、視頻、模板和3D資產，供其所有創意項目使用。

如需詳細資訊，請參閱在Experience Manager Assets中使用Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md) 。[

![從Experience Manager Assets預覽Adobe Stock影像和授權](assets/stock_image_preview_license_options.png)

*圖：從中 [!DNL Adobe Stock] 預覽影像和許可 [!DNL Experience Manager Assets]證。*

![在Experience Manager中搜尋及篩選授權的Adobe Stock影像](assets/aem-search-filters2.jpg)

*圖：在中搜尋及篩選授權 [!DNL Adobe Stock] 的影 [!DNL Experience Manager]像。*

### [!DNL Adobe InDesign]中的動態引用 {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 用於檔 [!DNL Adobe InDesign] 案的是動態的。如果參考的資產在存放庫中移動，則參考會自動更新。 如需詳細資訊，請參閱[如何管理複合資產](/help/assets/managing-linked-subassets.md)。

## Brand Portal功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 可協助您輕鬆取得、有效控制並安全地將經核准的資產分散給外部廠商/代理，以及跨裝置將內部業務使用者。它有助於提高資產共用的效率，加快資產上市時間，並消除不合規使用和未經授權的訪問的風險。

如需詳細資訊，請參閱[Brand Portal的新功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hant)。

## 連線資產 {#connectedassets}

在大型企業中，建立網站所需的基礎架構可以分散。 有時，網站建立功能和所需的數位資產會分散在不同的孤立環境中。

[!DNL Experience Manager Sites] 提供建立網頁的功能，而 是可為網站提供必要資產的數位資產管理 (DAM) 系統。[!DNL Experience Manager Assets][!DNL Experience Manager] 現在透過整合和支援上述使 [!DNL Sites] 用案 [!DNL Assets]例。請參閱[如何設定及使用連線資產功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![從不同部署 [!DNL Experience Manager] 頁面上 [!DNL Sites] 的部署拖 [!DNL Experience Manager] 曳資產](assets/connected-assets-drag-and-drop-only.gif)

*圖：從不同部署 [!DNL Experience Manager] 頁面上 [!DNL Sites] 的部署拖 [!DNL Experience Manager] 曳資產。*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 提供增強的多媒體製作和內 [!DNL Experience Manager Assets] 容傳遞，提供身臨其境且個人化的尖端體驗。透過上傳單一高品質主要資產並使用Adobe的進階雲端轉譯和檢視器，您可以即時提供任何轉譯組合，以支援貴組織的媒體策略。

如需新[!DNL Dynamic Media]功能的詳細資訊，請參閱[Dynamic Media發行說明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)。

### 360視訊支援 {#video-support}

使用尖端檢視器直接在[!DNL Experience Manager]中管理360個視訊檔案，將VR體驗提供至案頭、行動裝置和VR頭戴式電腦。 如需詳細資訊，請參閱[使用360視訊](/help/assets/360-video.md)。

### 自訂影片縮圖 {#custom-video-thumbnails}

您現在可以使用視訊本身或DAM中儲存的其他內容影格，自訂視訊資產的縮圖。 如需其他指示，請參閱[關於視訊縮圖](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

### 協助工具增強功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 檢視器現在支援增強的協助工具功能，例如Aria支援、螢幕閱讀器和Alt-text。如需其他詳細資訊，請參閱[檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html)。

## 搜尋體驗增強功能 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5之後，行銷人員可以從搜尋結果頁面更快找到所需資產。甚至在套用搜尋篩選器之前，搜尋刻面也會以資產數量更新。 透過篩選器查看預期的計數，可協助使用者有效率地導覽搜尋結果。 如需詳細資訊，請參閱[在Experience Manager中搜尋資產](../assets/search-assets.md)。

![查看未篩選搜尋Facet中搜尋結果的資產數量](/help/assets/assets/asset_search_results_in_facets_filters.png)

*圖：在搜尋Facet中查看未篩選搜尋結果的資產數量。*

## 可用性增強 {#usability-enhancement}

您現在可以選取資料夾內或搜尋結果中所有已載入的資產。 可協助您快速管理多個資產。 核取方塊會選取符合案例的所有資產（例如搜尋結果），而不只是選取[!DNL Experience Manager]介面中可見的資產。

![使用「全部選取」選項，只要按一下即可選取所有載入的資產。](assets/select-all-in-aem-assets.gif)

*圖：使用「全部選取」選項，只要按一下即可選取所有載入的資產。*

## 中繼資料增強功能 {#metadata-enhancements}

[!DNL Assets] 可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的配置和中繼資料。現在，您可以在建立資料夾時，將資料夾中繼資料結構指派給現有資料夾。 如需詳細資訊，請參閱[資料夾中繼資料結構](/help/assets/metadata-config.md#folder-metadata-schema)。

指定階層式中繼資料時，可在執行階段從JSON檔案載入選項，例如，不必在表單中手動輸入。 如需詳細資訊，請參閱[階層式中繼資料](/help/assets/metadata-schemas.md#cascading-metadata)。

## 報表增強功能 {#reporting-enhancements}

內容片段和連結分享現在會包含在下載的報表中。 如需詳細資訊，請參閱[資產報表](/help/assets/asset-reports.md)。
