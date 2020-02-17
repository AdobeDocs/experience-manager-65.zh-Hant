---
title: 比較AEM Assets和AEM Media Library產品
description: 比較AEM Assets和AEM Media Library產品，並瞭解其差異。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 569c552686e6312ecae0d500147a8b65354c303d

---


# AEM Assets與AEM Media Library {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager(AEM)Assets是AEM平台不可或缺的一部分。 此順暢整合被視為AEM的主要優點，可確保內容管理的一致性，並提高內容作者的生產力。

## Frequently asked questions {#frequently-asked-questions}

### 什麼是AEM Assets? {#what-is-aem-assets}

AEM Assets是AEM Platform上的應用程式，可讓我們的客戶在網路儲存庫中管理其數位資產（影像、視訊、檔案和音訊片段）。 AEM Assets包含中繼資料支援、轉譯、Digital Asset Management Finder和AEM Assets Administration UI。

### 什麼是AEM Media Library? {#what-is-the-aem-media-library}

AEM Media Library是AEM WCM內容存放庫的指定部分，影像和其他共用資源都會儲存在此處。 「媒體庫」使用AEM WCM的「數位資產管理」功能。

### 我可從不屬於AEM WCM的AEM Assets獲得哪些資訊？ {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

AEM Assets客戶僅能使用的獨特功能包括：

* 擷取和編輯除標題、標籤和說明以外之中繼資料的能力。
* 「AEM資產管理員」，可從歡迎畫面中選取網站管理員旁的第二個按鈕。
* 所有與「數位資產管理」相關的工作流程步驟，即AEM Assets Ingestion、AEM Assets Deletion、AEM Assets Sub-Asset-Handling、AEM Assets中繼資料擷取。
* 程式庫，包括「dam」im封裝空間。

使用這些功能需要有效的AEM Assets授權。

### AEM Assets是否可以個別套件使用？ {#is-aem-assets-available-as-a-separate-package}

否. 為方便安裝和部署，所有AEM應用程式和附加元件都以單一套件形式提供，並包含所有功能。 這並不表示您擁有使用套件中所有功能的權限。

### 我想編輯數位資產的中繼資料。 我需要AEM資產嗎？ {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

如果您打算編輯除標題、說明和標籤以外的中繼資料，則必須取得AEM Assets的授權。

### 我想在我的網站上使用類別謂詞。 我需要AEM資產嗎？ {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

是的，類別謂詞是AEM Assets的一部分，需要AEM Assets授權。

### 我想在匯入時自動調整影像大小。 我需要AEM資產嗎？ {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

否. AEM媒體庫包含調整靜態影像大小和自動工作流程導向轉換功能以及管理轉譯的功能。 這些功能不需要AEM Assets授權。

### 我想使用自訂的影像元件來調整影像大小。 我需要AEM資產嗎？ {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

影像元件是AEM WCM的一部分。 影像元件（但也由AEM Assets）使用的圖形庫是AEM平台的一部分，不需要AEM Assets授權。

### 如果我未授權AEM Assets，該如何防止使用者使用AEM Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

您可以從AEM移除所有AEM Assets專屬的工作流程、元件、分類、選項和AEM Assets管理員。 如此可避免使用者意外使用您未授權的AEM Assets功能。

### 我想要將影像新增至頁面，並想要裁切這些影像並調整其大小。 我需要AEM資產嗎？ {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

在此使用案例中，您不需要購買AEM Assets，即使使用媒體程式庫也不需要在網站上使用影像，因為智慧型影像元件可讓您直接上傳影像至頁面。

### AEM Assets與媒體程式庫中可用功能的詳細清單 {#listoffeatures}

**AEM Assets**

* 系列和燈箱
* 進階的中繼資料屬性與管理
* Adobe Asset Link（連線至適用於企業的Creative Cloud）
* AEM案頭應用程式
* 處理設定檔
* InDesign server整合
* 資產範本和型錄製作者架構
* Adobe Photoshop、Illustrator和InDesign連結資產
* 多語言資產管理
* PIM整合
* Rights Management
* Camera RAW支援
* 搜尋Facet管理與設定
* 預先建立的DAM工作流程（例如像片拍攝）
* 資產報告與分析：資產見解
* 3D資產管理
* 連線資產
* 品牌入口網站
* 自助服務存取
* 瀏覽、搜尋和下載
* 系列和資料夾共用
* 管理工具
* 智慧標記
* 視覺搜尋
* 資產管理UI

**媒體庫**

* 基本中繼資料屬性
* 標記管理
* 版本控制
* 靜態轉譯
* 專案、工作、工作流程編寫
* 活動串流（時間軸）
* 查詢產生器(API)
* Marketing cloud整合
* UI自訂與擴充功能
* 注釋與注釋
