---
title: AEM Mobile SetUp
seo-title: AEM Mobile SetUp
description: 請依照本頁面來設定AEM Mobile，讓使用者在AEM中建立和管理內容。 本頁提供有關將AEM例項與雲端AEM Mobile隨選服務帳戶和專案整合的資訊。
seo-description: 請依照本頁面來設定AEM Mobile，讓使用者在AEM中建立和管理內容。 本頁提供有關將AEM例項與雲端AEM Mobile隨選服務帳戶和專案整合的資訊。
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>從AEM 6.2或6.3移轉至AEM 6.5的現有AEM mobile應用程式客戶，可從PackageShare下載套件，繼續使 [用AEM Mobile應用程式](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package)。 不過，AEM 6.5的新安裝將不支援AEM Mobile Apps功能。

若要使用AEM為AEM mobile應用程式製作內容，您必須將AEM例項與雲端AEM Mobile隨選服務帳戶和專案整合。

請依照下列步驟來設定AEM Mobile，讓使用者在AEM中建立和管理內容。

## AEM Mobile布建 {#aem-mobile-provisioning}

若要開始設定AEM Mobile，您必須：

* **請求API金鑰**:若要存取On-Demand Services API，您需要申請API金鑰。 若要申請API金鑰，請填妥 [PDF表格](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html)。 將填妥的表格傳送至Adobe開發人員支援： [wwds@adobe.com](mailto:wwds@adobe.com)

* **產生裝置ID和裝置Token**:收到API金鑰後，您就可以產生裝置ID和裝置Token。 請前往 [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) ，並執行下列動作：

   * 提供API金鑰
   * 使用您已新增至AEM mobile專案的Adobe ID登入，並具備下列權限（請參閱建立專案的下列步驟）

      * 管理>管理專案和使用者
      * 「內容>新增及編輯內容、刪除內容、檢視內容、發佈內容」

如果符合所有條件，將會產生裝置ID和裝置Token。

>[!NOTE]
>
>您應授與AEM mobile專案的存取權，此為所需的Adobe ID。 請參 [閱線上說明中的「AEM mobile帳戶管理](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) 」。

## 建立AEM mobile專案 {#creating-projects-for-aem-mobile}

當您建立專案時，您會為任何您要定位的平台指定設定：iOS、Android、Windows和案頭網頁檢視器。 您指定的許多專案設定都會影響應用程式的行為。

建立專案時，必須使用具有主管理員角色的Adobe ID登入On-Demand Services入口網站。 編輯專案需要主管理員角色或具有「管理專案」和「使用者」權限 **的使用者角色** 。

>[!NOTE]
>
>若要進一步瞭解「在AEM mobile中建立專案」，請按一 [下這裡](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html)。

## 設定AEM Mobile連接器 {#configuring-an-aem-mobile-connector}

AEM設定涉及連接器設定的下列步驟。 在AEM mobile連接器設定完成後，使用者就可以設定使用者群組和權限。

AEM Mobile On-Demand連接器可用來將AEM mobile管理的內容與Adobe Experience Manager mobile的隨選服務系結。 這可讓內容作者使用AEM的工具建立和管理行動應用程式的內容，同時使用AEM mobile的隨選服務，以輕鬆發佈行動內容。

>[!NOTE]
>
>這是設定AEM例項的一次性步驟。

### 設定AEM Mobile On-Demand services用戶端 {#configuring-aem-mobile-on-demand-services-client}

您必須完成設定步驟，AEM mobile整合才能正常運作。

1. 轉至OSGI服務配置

   1. AEM >工具>作業> Web Console
   1. 捲動或搜尋 ***Experience Manager Mobile On-demand Services Client（原為Adobe Digital Publishing Solution Client）***

1. 編輯 ***Experience Manager Mobile On-demand Services Client***

   1. **（必填）輸入必填欄位** :

      1. 用戶端識別碼.
      1. 用戶端密碼.
   1. **（可選）** 「編輯現有值」。


1. 儲存變更。
1. 以下是一個配置示例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 設定AEM Mobile On-Demand Services cloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 前往雲端服務

   1. AEM >工具>部署> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)。 捲動或搜 ***尋Adobe Experience Manager Mobile隨選服務***

1. 選擇 ***立即配置*** 或 ***顯示配置*** ，然後選擇添加新配置表徵圖

1. 建立新設定

   1. 輸入標題和名稱
   1. 輸入設備ID
   1. 輸入裝置Token
   1. 選擇 ***測試設備配置*** ，以驗證輸入的值
   1. 選擇確定

## 新增AEM mobile使用者角色和指派權限 {#adding-aem-mobile-user-roles-and-assigning-permissions}

建立專案後，您應建立角色並授與使用者存取權。 只有主管理員可以建立和編輯角色。 當您建立角色時，您會為指派這些權限的使用者啟用權能（或權限）。 例如，您可以建立一個角色，其中包含建立應用程式的權限，而另一個角色則包含建立和發佈內容的權限。

在AEM mobile應用程式開發中，有三個不同的角色：

* 管理員
* 開發人員
* 作者

如需建立具有不同權限（例如建立應用程式或建立和發佈內容）的角色的詳細資訊，請按一下「AEM Mobile說明」中的「建立使用者角色及授與存取權 [](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) 」。

>[!NOTE]
>
>管理應用程式內容需要開發人員、內容製作者和管理員共同努力。 作者會根據應用程式開發人員產生的範本和元件來控制頁面。 最後，管理員策略性地發佈更新的應用程式內容。 設定AEM群組和權限會定義其在應用程式儀表板或控制中心中的角色。
>
>如需AEM Mobile儀表板的詳細資訊，請按一 [下這裡](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

在您建立具有不同權限的角色後，例如建立應用程式或建立和發佈內容，請參閱「設定使用者和使用者群組」 [****](/help/mobile/aem-mobile-configure-users.md)，以設定您的使用者和群組，以支援製作和管理行動應用程式。

### 其他資源 {#additional-resources}

若要進一步瞭解建立AEM Mobile隨選服務應用程式的其他兩個角色和責任，請參閱下列資源：

* [針對AEM Mobile隨選服務開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [製作適用於AEM Mobile隨選服務應用程式的AEM內容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>若要預覽應用程式內容，包括瀏覽頁和文章，請參閱「使用預 [檢預覽」](/help/mobile/aem-mobile-manage-ondemand-services.md)。
