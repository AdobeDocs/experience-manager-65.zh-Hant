---
title: AEM Mobile設定
seo-title: AEM Mobile SetUp
description: 按照此頁設定AEM Mobile，從而允許用戶建立和管理內AEM容。 本頁提供有關將實AEM例與基於雲的AEM Mobile On-demand Services帳戶和項目整合的資訊。
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 1%

---

# AEM Mobile設定{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>現有的AEM Mobile應用從AEM6.2或6.3遷移到AEM6.5的客戶可以通過從PackageShare下載包繼續使用AEM Mobile應用。 但是，新安裝的6AEM.5版不支援AEM Mobile應用程式功能。

為了用AEM於為AEM Mobile應用生成內容，您必AEM須將實例與基於雲的AEM Mobile On-demand Services帳戶和項目整合。

按照這些步驟設定AEM Mobile，從而允許用戶建立和管理內AEM容。

## AEM Mobile資源調配 {#aem-mobile-provisioning}

要開始設定AEM Mobile，您需要：

* **請求API密鑰**:要訪問On-Demand Services API，需要請求API密鑰。 要請求API密鑰，請完成 [PDF窗體](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html)。 將填寫好的表單發送至Adobe Developer支援： [wwds@adobe.com](mailto:wwds@adobe.com)

* **生成設備ID和設備令牌**:收到API密鑰後，可以生成設備ID和設備令牌。 轉到 `https://aex.aemmobile.adobe.com` 並執行以下操作：

   * 提供API密鑰
   * 使用您已添加到AEM Mobile項目的具有以下權限的Adobe ID登錄（請參閱以下建立項目的步驟）

      * 管理>管理項目和用戶
      * 內容>添加和編輯內容、刪除內容、查看內容、發佈內容

如果滿足所有條件，將生成設備ID和設備令牌。

>[!NOTE]
>
>Adobe ID應獲准參與AEM Mobile項目。 請參閱 [AEM Mobile帳戶管理](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) 中。

## 為AEM Mobile建立項目 {#creating-projects-for-aem-mobile}

建立項目時，您會為所瞄準的任何平台指定設定：iOS、Android、Windows和案頭Web查看器。 您指定的許多項目設定都會影響應用的行為。

建立項目需要使用具有主管理員角色的Adobe ID登錄到按需服務門戶。 編輯項目需要主管理員角色或用戶角色 **管理項目和用戶** 權限。

>[!NOTE]
>
>要瞭解有關在AEM Mobile建立項目的詳細資訊，請按一下 [這裡](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html)。

## 配置AEM Mobile連接器 {#configuring-an-aem-mobile-connector}

設定AEM涉及以下連接器配置步驟。 完成AEM Mobile連接器配置後，用戶可以設定用戶組和權限。

AEM Mobile按需連接器用於將AEM Mobile管理的內容與Adobe Experience Manager Mobile的按需服務綁定。 這使內容作者能夠使用工具為移動應用建立和管AEM理材料，同時使用AEM Mobile的按需服務輕鬆分發移動內容。

>[!NOTE]
>
>這是設定實例的一個步AEM驟。

### 配置AEM Mobile On-demand Services客戶端 {#configuring-aem-mobile-on-demand-services-client}

必須完成配置步驟，才能使AEM Mobile整合正常運行。

1. 轉到OSGI服務配置

   1. AEM>工具>操作> Web控制台
   1. 滾動或搜索 ***Experience Manager移動按需服務客戶端(以前是Adobe數字發佈解決方案客戶端)***

1. 編輯 ***Experience Manager移動按需服務客戶端***

   1. **（強制）** 輸入必填欄位：

      1. 用戶端識別碼.
      1. 用戶端密碼.
   1. **（可選）** 編輯現有值。


1. 儲存變更。
1. 下面是一個配置示例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 配置AEM Mobile On-demand Services雲服務 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 轉到Cloud Services

   1. >AEM工具>部署> [雲服務](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)。 滾動或搜索 ***Adobe Experience Manager Mobile按需服務***

1. 選擇 ***立即配置*** 或 ***顯示配置*** ，然後選擇「添加新配置」表徵圖

1. 建立新配置

   1. 輸入標題和名稱
   1. 輸入設備ID
   1. 輸入設備令牌
   1. 選擇 ***Test設備配置*** 驗證輸入的值
   1. 選擇確定

## 添加AEM Mobile用戶角色和分配權限 {#adding-aem-mobile-user-roles-and-assigning-permissions}

建立項目後，應建立角色並授予用戶訪問權限。 只有主管理員才能建立和編輯角色。 建立角色時，可以為任何分配了這些權限的用戶啟用權能（或權限）。 例如，您可以建立一個包含應用程式構建權限的角色和另一個包含建立和發佈內容權限的角色。

在AEM Mobile應用開發中，存在三個不同的角色：

* 管理員
* 開發人員
* 作者

有關建立具有不同權限的角色的詳細資訊，請按一下 [建立用戶角色和授予訪問權限](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) 在AEM Mobile。

>[!NOTE]
>
>管理應用內容需要開發人員、內容作者和管理員共同努力。 作者操作頁面，這些頁面又基於應用程式開發人員生成的模板和元件。 最後，管理員戰略性地發佈更新的應用程式內容。 設定組AEM和權限在應用程式儀表板或控制中心中定義其角色。
>
>有關AEM Mobile儀表板的詳細資訊，請按一下 [這裡](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

建立具有不同權限的角色後，請參閱 [**配置用戶和用戶組**](/help/mobile/aem-mobile-configure-users.md) 配置用戶和組以支援您的移動應用的創作和管理。

### 其他資源 {#additional-resources}

要詳細瞭解建立AEM Mobile On-demand Services應用程式的其他兩個角色和職責，請參閱以下資源：

* [開發AEMAEM Mobile On-demand Services內容](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand ServicesAEM應用的創作內容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>要預覽應用內容，包括瀏覽頁面和文章，請參閱 [使用印前檢查預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)。
