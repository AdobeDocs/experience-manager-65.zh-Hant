---
title: 比較Adobe Experience Manager Assets和Media Library產品。
description: 比較Experience Manager Assets和Media Library產品，並瞭解其差異。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 2%

---


# Experience Manager Assets與Experience Manager Media Library的比較 {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager Assets是Experience Manager平台不可或缺的一部分。 此順暢整合被視為Experience Manager的主要優點，可確保內容管理的一致性，並提高內容作者的生產力。

## 常見問題 {#frequently-asked-questions}

### 什麼是資產？ {#what-is-aem-assets}

資產是Experience Manager的一項功能，可讓使用者在網路儲存庫中管理其數位資產（影像、視訊、檔案和音訊剪輯）。 資產包括中繼資料支援、轉譯、搜尋器和管理介面。

### 什麼是Experience Manager Media Library? {#what-is-the-aem-media-library}

Experience Manager Media Library是Experience Manager WCM內容存放庫的指定部分，影像和其他共用資源會儲存在此存放庫。 媒體庫為WCM提供基本的數位資產管理功能。

### 我可從不屬於WCM的Assets獲得什麼？ {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

資產客戶僅能使用的獨特功能包括：

* 擷取和編輯除標題、標籤和說明以外之中繼資料的能力。
* 「資產管理員」，可從歡迎畫面取得。
* 所有與數位資產管理相關的工作流程步驟，例如擷取、資產刪除、子資產處理、中繼資料擷取。
* 程式庫，包 `dam` 括在封裝空間中。

使用這些功能需要有效的資產授權。

### 資產是否可以單獨套件使用？ {#is-aem-assets-available-as-a-separate-package}

否. 為方便安裝和部署，所有Experience Manager應用程式和附加元件都以單一套件形式提供，並包含所有功能。 這並不表示您擁有使用套件中所有功能的權限。

### 我想編輯數位資產的中繼資料。 我需要資產嗎？ {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

如果您打算編輯除標題、說明和標籤以外的中繼資料，則必須取得資產授權。

### 我想在我的網站上使用類別謂詞。 我需要資產嗎？ {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

是的，類別謂詞是Assets的一部分，需要Assets授權。

### 我想在匯入時自動調整影像大小。 我需要資產嗎？ {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

否. 調整靜態影像的大小和自動工作流程導向轉換，以及管理轉譯的能力，都是Experience Manager Media Library的一部分。 這些功能不需要「資產」授權。

### 我想使用自訂的影像元件來調整影像大小。 我需要資產嗎？ {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

影像元件是WCM的一部分。 影像元件（但也由資產使用）所使用的圖形庫是Experience Manager平台的一部分，不需要資產授權。

### 如果我未授權資產，如何防止使用者使用資產？ {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

您可以從Experience Manager移除所有資產特定的工作流程、元件、分類、選項和資產管理員。 如此可避免使用者意外使用您未授權的資產功能。

### 我想要將影像新增至頁面，並想要裁切這些影像並調整其大小。 我需要資產嗎？ {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

在此使用案例中，不需要購買資產，即使使用媒體庫也不需要在網站上使用影像，因為智慧型影像元件可讓您直接上傳影像至頁面。

### 資產與媒體庫中可用功能的詳細清單 {#listoffeatures}

**Experience Manager Assets**

* 系列和燈箱
* 進階的中繼資料屬性與管理
* Adobe Asset Link（連線至適用於企業的Creative Cloud）
* Experience manager 桌面應用程式
* 處理設定檔
* [!DNL Adobe InDesign Server] 整合
* 資產範本和型錄製作者架構
* [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]和整 [!DNL Adobe InDesign] 合
* 多語言資產管理
* PIM整合
* 權限管理
* Camera RAW支援
* 搜尋Facet管理與設定
* 預先建立的DAM工作流程（例如像片拍攝）
* 資產報告與分析，稱為「前瞻分析」
* 3D資產管理
* 連線資產
* 品牌入口網站
* 自助服務存取
* 瀏覽、搜尋和下載
* 系列和資料夾共用
* 管理工具和介面
* 智慧標籤
* 視覺搜尋

**媒體庫**

* 基本中繼資料屬性
* 標籤管理
* 版本控制
* 靜態轉譯
* 專案、工作、工作流程編寫
* 活動串流（時間軸）
* 查詢產生器(API)
* Marketing Cloud整合
* UI自訂與擴充功能
* 注釋和注釋
