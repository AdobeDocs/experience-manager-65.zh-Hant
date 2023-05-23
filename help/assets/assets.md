---
title: ' [!DNL Adobe Experience Manager Assets] 簡介'
description: 瞭解什麼是數字資產管理、其使用案例，以及 [!DNL Adobe Experience Manager Asset] 提供。
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# 關於 [!DNL Adobe Experience Manager Assets] 作為DAM解決方案 {#administering-assets}

[!DNL Assets] 是數字資產管理(DAM)工具，是 [!DNL Experience Manager] 平台，使您的企業能夠管理和分發數字資產。 組織中的用戶可以管理、儲存和訪問多種類型的數字資產，如影像、視頻、文檔、音頻剪輯、3D檔案和富媒體，供在Web上使用、打印和數字分發。

## 什麼是數字資產管理？ {#what-is-digital-asset-management}

[!DNL Assets] 提供企業範圍內對組織關鍵數字資產的共用和分發。 跨組織的用戶可以通過Web介面（或CIFS或WebDAV資料夾）儲存、管理和訪問數字資產（如影像、圖形、音頻、視頻和文檔）。

[!DNL Assets] 能力 [!DNL Experience Manager] 允許您執行以下操作：

* 以各種檔案格式添加和共用影像、文檔、音頻檔案和視頻檔案。
* 通過按標籤、燈箱或星號（您的收藏夾）對資產進行分組來管理資產。 向資產添加註釋。
* 通過搜索檔案名、文檔全文以及搜索日期、文檔類型和標籤來查找資產。
* 添加或編輯資產的元資料資訊。 元資料與相應資產一起自動版本化。 您可以導入或導出資產元資料。
* 執行影像編輯功能，如縮放和添加影像濾鏡。 使用WebDAV或CIFS資料夾同時導入和導出多個數字資產。
* 使用工作流和通知允許聯合處理和下載任何資產集，並管理對資產的訪問權限。

### [!DNL Experience Manager Assets] 與 [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 完全整合 [!DNL Sites] 並能夠無縫地適用於所有使用情形。 例如，在創作網頁時， [!DNL Sites] 作者可以通過Content Finder查找和使用數字資產。 的用戶介面 [!DNL Assets] 與 [!DNL Sites]。 請參閱 [站點概述](/help/sites-authoring/page-authoring.md) 的雙曲餘切值。

基本用戶介面與 [!DNL Sites]。 請參閱 [站點概述](/help/sites-authoring/page-authoring.md) 的雙曲餘切值。

### 數字資產管理與映像元件 {#digital-asset-management-versus-image-component}

在確定是將映像放入DAM儲存庫還是使用映像元件時，請考慮映像的生命週期：

* 如果影像與頁面具有相同的生命週期，請使用「影像」元件。
* 如果影像具有單獨的生命週期，例如，如果兩次或在WCM外使用影像，則使用 [!DNL Assets]。

## 什麼是數字資產？ {#what-are-digital-assets}

資產是數字文檔、影像、視頻或音頻（或其一部分），可以具有多個格式副本，並且可以具有子資產（例如，photoshop檔案中的圖層、PowerPoint檔案中的幻燈片、pdf中的頁面、ZIP中的檔案）。

資產實質上是二進位加元資料加上格式副本加子資產。 查看 [DAM效能指南](/help/sites-deploying/assets-performance-sizing.md) 的上界。

>[!CAUTION]
>
>上傳和/或編輯大量資產（尤其是影像）會影響您的效能 [!DNL Experience Manager] 部署。

### [!DNL Experience Manager Assets] 術語 {#aem-assets-terminology}

使用中的數字資產時 [!DNL Experience Manager]，您需要瞭解以下術語：

* **集合**:資產的集合，基於物理位置（資料夾）、公共屬性（保存的搜索資料夾）或用戶選擇（光箱資料夾）。

* **元資料** [!DNL Assets] 有元資料；例如，作者、到期日期、DRM資訊(Digital Rights Management)等。 元資料受訪問控制。 [!DNL Assets] 支援以下各種通用元資料方案：

   * 都柏林核心：包括作者、描述、日期、主題等。
   * IPTC:包括事件、模型、位置等。
   * WCM:包括頁面屬性， [!UICONTROL 準時] 和 [!UICONTROL 關機時間]等等。

* **標籤**: [!DNL Assets] 可以被標籤和分類。 請參閱 [組織資產](/help/assets/organize-assets.md)。

* **格式副本**:格式副本是資產的二進位表示形式。 [!DNL Assets] 始終具有主要表示形式 — 上載檔案的主要表示形式。 它們可以具有建立的任意數量的附加表示法，例如通過自定義工作流步驟或上載資產時建立的表示法。 格式副本的大小可能不同，解析度可能不同，添加了水印，或者某些其他更改了的特徵。

* **版本**:版本控制在特定時間點建立數字資產的快照。 您可以將資產還原到以前的版本。 請參閱 [版本控制 [!DNL Assets]](manage-assets.md#asset-versioning)。

* **子資產**:子資產是構成資產的資產，例如， [!DNL Adobe Photoshop] 檔案或PDF檔案中的頁面。 在 [!DNL Assets]，您可以像管理資產一樣管理子資產。

### 如何使用數字資產 {#how-to-work-with-assets}

您可以對資產或收集執行操作。 操作可以建立或修改資產、收集和格式副本。 您對資產執行的許多基本操作 — 上載、刪除、更新、保存子資產 — 觸發預配置的工作流。 這些功能將自動開啟 [!DNL Assets] 詳細描述 [!DNL Assets] 媒體處理程式。

您可以使用這些預配置的工作流執行的任務：

* 將資產保存到儲存庫，或從中刪除資產。
* 提取並保存資產的元資料；單個元資料項將另存為XMP。
* 為資產生成格式副本和縮略圖；包括自動調整大小和在必要時裁剪。
* 在必要時對資產進行轉碼。 例如，移動和Web使用的視頻以每秒24幀的方式轉碼，下載每秒30幀的視頻。 用於移動和Web的音頻以128 Kbps進行轉碼，用於下載的音頻以192 Kbps進行轉碼。

當然，您也可以手動應用工作流。 請參閱 [資產媒體處理程式](media-handlers.md)的子菜單。

## [!DNL Experience Manager Assets] 和 [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

請參閱 [資產和Media Library](medialibrary.md) 瞭解差異。

>[!MORELIKETHIS]
>
>* [視頻簡介 — Experience Manager Assets作為現代DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [瞭解元資料概念](/help/assets/metadata-concepts.md)

