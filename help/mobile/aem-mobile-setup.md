---
title: AEM Mobile設定
seo-title: AEM Mobile SetUp
description: 請依照本頁面操作來設定AEM Mobile，以便使用者在AEM中建立和管理內容。 本頁提供將AEM例項與雲端AEM Mobile On-demand Services帳戶及專案整合的相關資訊。
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# AEM Mobile設定{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>從AEM 6.2或6.3移轉至AEM 6.5的現有AEM Mobile應用程式客戶，可以借由下載 [來自PackageShare的包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). 不過，全新安裝的AEM 6.5將不支援AEM Mobile應用程式功能。

若要使用AEM為AEM Mobile應用程式產生內容，您必須將AEM例項與雲端型AEM Mobile On-demand Services帳戶和專案整合。

請依照下列步驟來設定AEM Mobile，以便使用者在AEM中建立和管理內容。

## AEM Mobile布建 {#aem-mobile-provisioning}

若要開始設定AEM Mobile，您必須：

* **要求API金鑰**:若要存取On-Demand Services API，您需要要求API金鑰。 若要要求API金鑰，請完成 [PDF表單](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). 將填妥的表單傳送至Adobe Developer支援： [wwds@adobe.com](mailto:wwds@adobe.com)

* **產生裝置ID和裝置代號**:收到API金鑰後，即可產生裝置ID和裝置Token。 前往 [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) 並執行下列動作：

   * 提供API金鑰
   * 使用您已新增至AEM Mobile專案的Adobe ID登入，並具備下列權限（請參閱以下建立專案的步驟）

      * 管理>管理專案和使用者
      * 「內容」 > 「新增及編輯內容」 、 「刪除內容」 、 「檢視內容」 、 「發佈內容」

如果符合所有條件，便會產生裝置ID和裝置代號。

>[!NOTE]
>
>需要的Adobe ID應獲得AEM Mobile專案的存取權。 請參閱 [帳戶管理AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) 中。

## 建立AEM Mobile專案 {#creating-projects-for-aem-mobile}

建立專案時，需指定所要鎖定之任何平台的設定：iOS、Android、Windows和案頭網頁檢視器。 您指定的許多專案設定會影響應用程式的行為。

若要建立專案，必須使用具有主管理員角色的Adobe ID登入On-Demand Services入口網站。 編輯專案需要主管理員角色或使用者角色，具有 **管理專案和使用者** 權限。

>[!NOTE]
>
>若要進一步了解在AEM Mobile中建立專案，請按一下 [此處](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## 設定AEM Mobile連接器 {#configuring-an-aem-mobile-connector}

AEM設定涉及連接器配置的下列步驟。 完成AEM Mobile連接器設定後，使用者就可以設定使用者群組和權限。

AEM Mobile On-Demand連接器可用來將AEM Mobile管理內容與Adobe Experience Manager Mobile的On-Demand服務系結。 這可讓內容作者使用AEM工具為行動應用程式建立和管理材料，同時使用AEM Mobile的隨需服務來輕鬆發佈行動內容。

>[!NOTE]
>
>這是設定AEM例項的一次性步驟。

### 設定AEM Mobile On-demand Services用戶端 {#configuring-aem-mobile-on-demand-services-client}

您必須完成設定步驟，AEM Mobile整合才能正常運作。

1. 前往OSGI服務設定

   1. AEM >工具>操作> Web Console
   1. 捲動或搜尋 ***Experience ManagerMobile On-demand Services用戶端(原AdobeDigital Publishing Solution Client)***

1. 編輯 ***Experience ManagerMobile On-demand Services用戶端***

   1. **（強制）** 輸入必填欄位：

      1. 用戶端識別碼.
      1. 用戶端密碼.
   1. **（可選）** 編輯現有值。


1. 儲存變更。
1. 以下是設定範例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 設定AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 前往Cloud Services

   1. AEM >工具>部署> [雲端服務](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). 捲動或搜尋 ***Adobe Experience Manager Mobile On-demand Services***

1. 選擇 ***立即配置*** 或 ***顯示配置*** 並選取「新增設定」圖示

1. 建立新配置

   1. 輸入標題和名稱
   1. 輸入設備ID
   1. 輸入裝置代號
   1. 選擇 ***測試設備配置*** 驗證輸入值
   1. 選擇確定

## 新增AEM Mobile使用者角色和指派權限 {#adding-aem-mobile-user-roles-and-assigning-permissions}

建立專案後，您應建立角色並授與使用者的存取權。 只有主管理員可以建立和編輯角色。 建立角色時，您會為獲指派這些權限的使用者啟用功能（或權限）。 例如，您可以建立一個角色，其中包含建立應用程式的權限，以及建立和發佈內容的權限。

在AEM Mobile應用程式開發中，有三個不同的角色：

* 管理員
* 開發人員
* 作者

如需以不同權限建立角色的詳細資訊，例如建立應用程式或建立及發佈內容，請按一下 [建立用戶角色和授予訪問權限](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) 在AEM Mobile幫助中。

>[!NOTE]
>
>管理應用程式內容需要開發人員、內容作者和管理員共同努力。 作者會根據應用程式開發人員產生的範本和元件來操控頁面。 最後，管理員會策略性地發佈更新的應用程式內容。 設定AEM群組和權限會在應用程式控制面板或控制中心中定義其角色。
>
>如需AEM Mobile控制面板的詳細資訊，請按一下 [此處](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

使用不同權限建立角色後（例如建立應用程式或建立及發佈內容），請參閱 [**設定您的使用者和使用者群組**](/help/mobile/aem-mobile-configure-users.md) 設定您的使用者和群組，以支援行動應用程式的製作和管理。

### 其他資源 {#additional-resources}

若要深入了解建立AEM Mobile On-demand Services應用程式的其他兩個角色和責任，請參閱下列資源：

* [為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>若要預覽應用程式內容，包括瀏覽頁面和文章，請參閱 [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md).
