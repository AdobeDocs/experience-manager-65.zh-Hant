---
title: SalesforceCommerce Cloud
seo-title: SalesforceCommerce Cloud/ Demandware
description: 了解如何使用SalesforceCommerce Cloud/ Demandware部署電子商務。
seo-description: 了解如何使用SalesforceCommerce Cloud/ Demandware部署電子商務。
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---


# SalesforceCommerce Cloud{#salesforce-commerce-cloud}

部署必要的電子商務套件將提供電子商務架構的完整功能，以及SalesforceCommerce Cloud/Demandware實作（包括示範目錄）所提供的電子商務功能的參考實作。

## 具有SalesforceCommerce Cloud{#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}的電子商務所需的包

若要安裝電子商務功能，您需要：

* AEM eCommerce架構：

   * 這是標準AEM安裝的一部分

* AEM Demandware商務內容套件

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>此整合支援SalesforceCommerce Cloud/ Demandware執行個體，設定為使用OCAPI 17.6版或更新版本。

### 使用SalesforceCommerce Cloud{#installation-of-ecommerce-with-salesforce-commerce-cloud}安裝電子商務

若要使用Demandware Commerce整合設定安裝AEM(使用示範目錄、Geometrixx Outdoors)，基本步驟為：

1. [安裝AEM](/help/sites-deploying/deploy.md)。
1. 使用[套件管理器](/help/sites-administering/package-manager.md)安裝內容套件：
1. [](/help/sites-authoring/page-authoring.md) 編寫您在AEM中需要的補充頁面。

>[!NOTE]
>
>若要下載套件，請導覽至[套件共用](/help/sites-administering/package-manager.md#package-share)。

AEM和Demandware沙箱之間的伺服器連線必須設定。 大部分的設定已預先設定為使用提供的SiteGenis示範內容套件，使用預設路徑、程式庫等。 如果連接器與其他網站和程式庫搭配使用，您需要更新此設定。

1. 導覽至[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 按一下「**Demandware客戶端**」。
1. 視需要輸入&#x200B;**執行個體端點ip或hostname**。

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 按一下「**儲存**」。
1. 按一下WebDAV **的「Demandware TransportHandler插件」。**
1. 設定&#x200B;**WebDAV用戶**&#x200B;和&#x200B;**WebDAV用戶密碼**。

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 按一下「**儲存**」。

#### 複寫 {#replication}

應在安裝程式包後啟用複製，您可以在此處驗證：[https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>預設情況下，複製代理配置為資訊日誌級別。 如果您想要取得詳細資訊，可以將記錄層級切換為除錯。

#### OAuth {#oauth}

OAuth用戶端已設定為可搭配Demandware沙箱例項使用。 為了測試目的，不需要進行任何變更。

對於測試和生產系統，OAuth用戶端必須設定適當的用戶端ID和密碼。

1. 導覽至[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 按一下&#x200B;**Demandware存取權杖提供者**。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 視需要修改值，然後按一下&#x200B;**Save**。

### SalesforceCommerce Cloud沙箱{#salesforce-commerce-cloud-sandbox}

必須設定Demandware沙箱，才能執行新的Velocity範本引擎。

>[!NOTE]
>
>下列精靈不屬於AEM Demandware連接器。 示範內容套件中提供此功能，有助於快速設定SiteGenesis示範頁面。

1. 導覽至[https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html)。
1. 按一下「**編輯」。**
1. 驗證值，然後按一下&#x200B;**OK**。
1. 按一下&#x200B;**初始化**。
1. 轉到WebDAV資料夾並檢查已發佈的模板檔案，例如`adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`下。

   >[!NOTE]
   >
   >擴充功能將為`.vs`。

1. 也檢查匯出的JS和CSS檔案，例如`adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`底下。

