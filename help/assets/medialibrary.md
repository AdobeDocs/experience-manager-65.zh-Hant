---
title: 使用Media Library進行基本數字資產管理
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

[!DNL Adobe Experience Manager] 平台提供了不同的資產管理功能。 Media Library允許用戶將少量資產上載到儲存庫、搜索和使用網頁中的資產，並完成有關資產的簡單資產管理任務。

Media Library是輕量級數字資產管理(DAM)解決方案， [!DNL Adobe Experience Manager Sites] 許可證。 [!DNL Sites] 是Web內容管理(WCM)產品。 Media Library與所有的Experience Manager合作。

[!DNL Adobe Experience Manager Assets] 許可證可單獨購買。 [!DNL Experience Manager Assets] 允許通過企業使用案例、元資料、架構、搜索和用戶介面的自定義以及Media Library提供的其他許多功能對資產進行穩健處理。

## 許可要求 {#avail-media-library-license}

擁有 [!DNL Sites] 牌照有權使用Media Library。 它適用於 [!DNL Experience Manager]。

Media Library作為站點的一部分安裝。 除站點許可證和安裝外，不需要其他許可證或軟體包。

## [!DNL Assets] 決戰Media Library {#assets-and-media-library}

Experience Manager Assets提供企業級DAM功能。 資產功能隨 [!DNL Experience Manager] 一個包裝。 但是，未購買資產許可證的用戶無權使用高級DAM功能。 沒有資產許可證，僅 [Media Library特徵](#use-media-library) 的雙曲餘切值。

如果要防止意外使用 [!DNL Assets] 您尚未授權的功能，然後刪除 [!DNL Assets] — 特定的工作流、元件、分類、選項和 [!DNL Assets] 管理員 [!DNL Experience Manager]。 這樣可以防止用戶意外使用 [!DNL Assets] 你沒有許可證的。

## 使用Media Library {#use-media-library}

Media Library為以下使用情形提供了基本的DAM功能：

* 使用 [!DNL Adobe Experience Manager Sites]。
* 使用 [!DNL Adobe Experience Manager Forms]。
* 使用 [!DNL Adobe Experience Manager Screens]。
* [!DNL Assets] 用於無頭操作的HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

要使用Media Library功能，可以使用 [!DNL Experience Manager] 用戶介面。 Media Library是 [!DNL Experience Manager Sites] 安裝，不需要單獨的介面或載入項。 使用現有介面，Media Library用戶有權完成以下任務：

* 建立資料夾以組織資產。
* 上傳資產.
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜索（包括相似性搜索）資產。
* 將值添加到元資料欄位（智慧標籤欄位除外）中的值並編輯這些值，這些值在 [!UICONTROL 基本] 頁籤 [!UICONTROL 屬性] 的子菜單。
* 添加和刪除靜態格式副本。
* 下載資料夾、資產和資產格式副本。
* 建立資產版本。
* 建立並執行資產審查任務。
* 注釋資產。
* 將資產添加到 [!DNL Sites] Content Finder中的頁面。
* 使用 [!DNL Content Fragments].
* 使用HTTP REST和GraphQL API [!DNL Content Fragments] 和引用的媒體資產，在「站點」許可證下。
* Marketing Cloud整合。
* 自定義和擴展資產管理用戶介面。
* 訪問查詢生成器(API)以擴展搜索功能。
* 建立靜態標籤。
* 編寫項目和任務。
* 活動流（時間軸）。
* 注釋和注釋。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>許多高級DAM使用案例由 [!DNL Experience Manager Assets]。 Media Library許可證只允許您使用Media Library履行所列的使用案例。 如果未列出使用案例，請勿將其與Media Library許可證一起使用。 如果您有任何疑問，請與Adobe客戶支援聯繫。

請注意，您不能使用智慧標籤， [!DNL Asset] 連結， [!DNL Asset] 選擇器、批量標籤、修改資產工作流或標準 [!DNL Adobe Experience Manager] 用戶介面訪問Media Library [!DNL Assets] 許可證。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5內部產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

