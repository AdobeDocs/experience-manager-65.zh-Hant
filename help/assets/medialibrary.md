---
title: 使用Media Library進行基本的數位資產管理
description: '"[!DNL Experience Manager Assets] 以及適用於資產管理的Media Library。」'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# 使用Media Library進行基本資產管理 {#manage-assets-using-media-library}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager] platform提供管理資產的不同功能。 Media Library可讓使用者將少量資產上傳至存放庫、搜尋並使用網頁中的資產，以及完成資產的簡單資產管理任務。

Media Library是輕量版的數位資產管理(DAM)解決方案，隨附免費的 [!DNL Adobe Experience Manager Sites] 授權。 [!DNL Sites] 是Web內容管理(WCM)產品。 Media Library可與Experience Manager的所有功能搭配使用。

[!DNL Adobe Experience Manager Assets] 授權可單獨購買。 [!DNL Experience Manager Assets] 可透過企業使用案例、中繼資料、結構描述、搜尋和使用者介面的自訂，以及Media Library提供的功能以外的許多其他功能，輕鬆處理資產。

## 授權需求 {#avail-media-library-license}

客戶擁有 [!DNL Sites] 授權有權使用Media Library。 它可搭配的所有元件使用 [!DNL Experience Manager].

Media Library會安裝為Sites的一部分。 除了Sites授權和安裝以外，不需要額外的授權或套件。

## [!DNL Assets] 與Media Library {#assets-and-media-library}

Experience Manager Assets提供企業級DAM功能。 Assets功能提供自 [!DNL Experience Manager] 在單一套件中。 但是，尚未購買Assets授權的使用者無權使用進階DAM功能。 僅限沒有Assets授權 [Media Library功能](#use-media-library) 可用。

如果您想避免不小心使用 [!DNL Assets] 您尚未授權的功能，然後移除所有 [!DNL Assets] — 特定工作流程、元件、分類、選項及 [!DNL Assets] 管理員來源 [!DNL Experience Manager]. 這麼做可防止您的使用者意外使用 [!DNL Assets] 您未授權的功能。

## 使用Media Library {#use-media-library}

Media Library為下列使用案例提供基本DAM功能：

* 網頁建立方式： [!DNL Adobe Experience Manager Sites].
* 使用建立的調適型表單和通訊 [!DNL Adobe Experience Manager Forms].
* 數位熒幕體驗建立方式： [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] 適用於Headless作業的HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

若要使用Media Library功能，您可以使用預設值 [!DNL Experience Manager] 使用者介面。 Media Library是 [!DNL Experience Manager Sites] 安裝且不需要個別介面或附加元件。 使用現有介面，Media Library使用者可完成下列工作：

* 建立資料夾以組織資產。
* 上傳資產。
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜尋（包括相似度搜尋）資產。
* 在中繼資料欄位中新增值並編輯值，但「智慧標籤」欄位除外，這些欄位可在 [!UICONTROL 基本] 資產的「 」標籤 [!UICONTROL 屬性] 頁面。
* 新增和刪除靜態轉譯。
* 下載資料夾、資產和資產轉譯。
* 建立資產版本。
* 對資產建立並執行稽核任務。
* 為資產加上註釋。
* 將資產新增至 [!DNL Sites] 頁面瀏覽內容尋找器。
* 使用 [!DNL Content Fragments].
* 將HTTP REST和GraphQL API用於 [!DNL Content Fragments] 和參照的媒體資產，在Sites授權下。
* Marketing Cloud整合。
* 自訂及擴充資產管理使用者介面。
* 存取查詢產生器(API)以擴充搜尋功能。
* 建立靜態標籤。
* 編寫專案和任務。
* 活動資料流（時間軸）。
* 註釋和註解。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>許多進階DAM使用案例由完成 [!DNL Experience Manager Assets]. Media Library授權可讓您使用Media Library僅履行列出的使用案例。 如果未列出使用案例，請勿將其與Media Library授權搭配使用。 如果您有任何疑問，請聯絡Adobe客戶支援。

請注意，您無法使用智慧標籤， [!DNL Asset] 連結， [!DNL Asset] 選擇器、大量標籤、修改資產工作流程或標準 [!DNL Adobe Experience Manager] 存取Media Library的使用者介面，不需 [!DNL Assets] 授權。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5內部部署產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)
