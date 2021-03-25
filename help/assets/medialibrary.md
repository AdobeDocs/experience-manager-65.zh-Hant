---
title: 使用媒體庫進行基本數位資產管理
description: '[!DNL Experience Manager Assets] 和媒體庫，以進行資產管理。'
contentOwner: AG
role: 建築師、領導者
translation-type: tm+mt
source-git-commit: 15c525746a613eb33cd09b7ff476f43aa18b146b
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 使用媒體庫進行基本資產管理{#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] 平台提供不同的功能來管理資產。「媒體庫」允許用戶將少量資產上傳到儲存庫、搜索和使用網頁中的資產，並完成資產上的簡單資產管理任務。

媒體庫是輕量型數位資產管理(DAM)解決方案，隨附[!DNL Adobe Experience Manager Sites]授權。 [!DNL Sites] 是網頁內容管理(WCM)方案。媒體庫可與所有Experience Manager功能搭配使用。

[!DNL Adobe Experience Manager Assets] 授權需另外購買。[!DNL Experience Manager Assets] 允許透過企業使用案例、中繼資料、結構描述、搜尋和使用者介面的自訂，以及媒體程式庫提供的其他功能，對資產進行強穩處理。

## 授權需求{#avail-media-library-license}

擁有[!DNL Sites]授權的客戶有權使用媒體庫。 它適用於[!DNL Experience Manager]的所有元件。

媒體程式庫會安裝為網站的一部分。 除Sites授權和安裝外，不需要額外的授權或套件。

## [!DNL Assets] 與媒體庫  {#assets-and-media-library}

Experience Manager資產提供企業級DAM功能。 資產功能是透過[!DNL Experience Manager]在單一套件中提供。 但是，未購買資產授權的使用者無權使用進階DAM功能。 沒有「資產」許可證，則僅[介質庫功能](#use-media-library)可用。

如果您想要防止未授權之[!DNL Assets]功能的意外使用，請從[!DNL Experience Manager]移除所有[!DNL Assets]特定工作流程、元件、分類、選項和[!DNL Assets]管理員。 如此可避免使用者意外使用您未授權的[!DNL Assets]功能。

## 使用媒體庫{#use-media-library}

媒體庫廣泛涵蓋下列使用案例：

* 為使用[!DNL Adobe Experience Manager Sites]建立的網頁提供基本DAM功能。
* 使用[!DNL Adobe Experience Manager Forms]建立的最適化表單和通訊。
* 使用[!DNL Adobe Experience Manager Screens]建立數位螢幕體驗。
* [!DNL Assets] HTTP REST API，以進行無頭操作。

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

要使用介質庫功能，可以使用預設的[!DNL Experience Manager]用戶介面。 介質庫是[!DNL Experience Manager Sites]安裝的一部分，不需要單獨的介面或附加模組。 使用現有介面，媒體庫用戶有權完成下列任務：

* 建立資料夾以組織資產。
* 上傳資產。
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜尋（包括相似性搜尋）資產。
* 在中繼資料欄位中新增值並編輯值，但智慧型標籤欄位除外，這些值預設會顯示在資產的[!UICONTROL 屬性]頁面的[!UICONTROL 基本]標籤中。
* 新增和刪除靜態轉譯。
* 下載檔案夾、資產和資產轉譯。
* 建立資產版本。
* 建立並執行資產的審核工作。
* 註解資產。
* 透過Content Finder將資產新增至[!DNL Sites]頁面。
* 使用[!DNL Content Fragments]。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>許多進階DAM使用案例都由[!DNL Experience Manager Assets]完成。 「媒體庫」授權僅允許您使用「媒體庫」完成所列的使用案例。 如果未列出使用案例，請勿將它與「媒體庫」授權搭配使用。 如果您有任何疑問，請聯絡Adobe客戶服務。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5內部部署產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

