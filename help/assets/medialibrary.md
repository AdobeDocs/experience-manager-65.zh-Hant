---
title: 使用Media Library進行基本數位資產管理
description: '"[!DNL Experience Manager Assets] 和Media Library的資產管理業務。」'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 4%

---


# 使用Media Library進行基本資產管理 {#manage-assets-using-media-library}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/medialibrary.html?lang=zh-Hant) |

[!DNL Adobe Experience Manager] platform提供不同的資產管理功能。 Media Library可讓使用者將少量資產上傳至存放庫、搜尋及使用網頁中的資產，並完成資產的簡單資產管理工作。

Media Library是輕量型數位資產管理(DAM)解決方案，隨附 [!DNL Adobe Experience Manager Sites] 授權。 [!DNL Sites] 是網頁內容管理(WCM)產品。 Media Library可搭配所有Experience Manager功能使用。

[!DNL Adobe Experience Manager Assets] 許可證可單獨購買。 [!DNL Experience Manager Assets] 可透過企業使用案例、中繼資料的自訂、結構、搜尋和使用者介面，以及Media Library提供的其他功能，來強大處理資產。

## 授權需求 {#avail-media-library-license}

具有 [!DNL Sites] 授權可使用Media Library。 適用於 [!DNL Experience Manager].

Media Library會隨Sites一併安裝。 除了Sites授權和安裝外，不需要其他授權或套件。

## [!DNL Assets] 與Media Library {#assets-and-media-library}

Experience Manager Assets提供企業級DAM功能。 資產功能透過 [!DNL Experience Manager] 單一套件中。 不過，尚未購買Assets授權的使用者無權使用進階DAM功能。 沒有Assets授權，僅 [Media Library功能](#use-media-library) 的URL區段。

如果您想要防止非預期的使用 [!DNL Assets] 您未獲得許可的功能，請刪除 [!DNL Assets] — 特定的工作流、元件、分類、選項和 [!DNL Assets] 管理員 [!DNL Experience Manager]. 這麼做可避免使用者意外使用 [!DNL Assets] 您未授權的功能。

## 使用Media Library {#use-media-library}

Media Library提供下列使用案例的基本DAM功能：

* 使用 [!DNL Adobe Experience Manager Sites].
* 使用建立的最適化表單和通訊 [!DNL Adobe Experience Manager Forms].
* 使用建立的數位螢幕體驗 [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] 無頭操作的HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

若要使用Media Library功能，您可以使用預設 [!DNL Experience Manager] 使用者介面。 Media Library是 [!DNL Experience Manager Sites] 安裝，不需要單獨的介面或載入項。 使用現有介面，Media Library使用者有權完成下列工作：

* 建立資料夾以組織資產。
* 上傳資產.
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜尋（包括相似性搜尋）資產。
* 新增值至，並編輯中繼資料欄位中的值（智慧標籤欄位除外），這些欄位可在 [!UICONTROL 基本] 資產的標籤 [!UICONTROL 屬性] 頁面。
* 新增和刪除靜態轉譯。
* 下載資料夾、資產和資產轉譯。
* 建立資產版本。
* 建立並執行資產的審核工作。
* 為資產加上注釋。
* 將資產新增至 [!DNL Sites] 頁面。
* 使用 [!DNL Content Fragments].
* 請使用HTTP REST和GraphQL API，以 [!DNL Content Fragments] 和參考的媒體資產，依照Sites授權。
* Marketing Cloud整合。
* 自訂及擴充資產管理使用者介面。
* 存取查詢產生器(API)以擴充搜尋功能。
* 建立靜態標籤。
* 編寫專案和工作。
* 活動資料流（時間軸）。
* 註解和註解。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>許多進階DAM使用案例都由 [!DNL Experience Manager Assets]. Media Library授權可讓您僅使用Media Library履行列出的使用案例。 如果未列出使用案例，請勿將其用於Media Library授權。 若您有任何疑問，請聯絡Adobe客戶支援。

請注意，您無法使用智慧標籤， [!DNL Asset] 連結， [!DNL Asset] 選取器、大量標籤、修改資產工作流程或標準 [!DNL Adobe Experience Manager] 使用者介面，不使用 [!DNL Assets] 授權。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5內部部署產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

