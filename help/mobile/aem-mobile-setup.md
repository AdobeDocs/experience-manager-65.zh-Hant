---
title: AEM Mobile設定
description: 請依照本頁面的說明設定AEM Mobile，讓使用者能在Adobe Experience Manager (AEM)中建立和管理內容。 本頁提供整合AEM執行個體與雲端型AEM Mobile On-demand Services帳戶和專案的相關資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# AEM Mobile設定{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>從AEM 6.2或6.3移轉至AEM 6.5的現有Adobe Experience Manager (AEM)行動應用程式客戶，可以從「封裝共用」下載套件，繼續使用AEM Mobile應用程式。 不過，新安裝的AEM 6.5不支援AEM Mobile應用程式功能。

若要使用AEM產生AEM Mobile應用程式的內容，您必須將AEM執行個體與雲端型AEM Mobile On-demand Services帳戶和專案整合。

請依照下列步驟設定AEM Mobile，讓使用者能夠在AEM中建立和管理內容。

## AEM Mobile布建 {#aem-mobile-provisioning}

若要開始設定AEM Mobile，您必須：

* **要求API金鑰**：若要存取On-Demand Services API，您必須要求API金鑰。 若要要求API金鑰，請完成[PDF表單](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html)。 將完成的表單傳送至Adobe Developer支援： [wwds@adobe.com](mailto:wwds@adobe.com)

* **產生裝置ID和裝置Token**：收到API金鑰後，即可產生裝置ID和裝置Token。 移至`https://aex.aemmobile.adobe.com`並執行下列動作：

   * 提供API金鑰
   * 使用您新增至AEM Mobile專案的Adobe ID登入，並具備下列許可權（請參閱下列步驟以建立專案）

      * 管理>管理專案和使用者
      * 內容>新增與編輯內容、刪除內容、檢視內容、Publish內容

如果滿足所有條件，則會產生裝置ID和裝置代號。

>[!NOTE]
>
>應授予所需的Adobe ID對AEM Mobile專案的存取權。 請參閱線上說明中的[AEM Mobile帳戶管理](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html)。

## 建立AEM Mobile專案 {#creating-projects-for-aem-mobile}

建立專案時，您可以針對要定位的任何平台指定設定： iOS、Android™、Windows和Desktop Web Viewer。 您指定的許多專案設定都會影響應用程式的行為。

建立專案需要使用具有主要管理員角色的Adobe ID登入On-Demand Services入口網站。 編輯專案需要主要管理員角色或具有&#x200B;**管理專案和使用者**&#x200B;許可權的使用者角色。

>[!NOTE]
>
>若要進一步瞭解如何在AEM Mobile中建立專案，請按一下[這裡](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html)。

## 設定AEM Mobile聯結器 {#configuring-an-aem-mobile-connector}

AEM設定涉及聯結器設定的以下步驟。 AEM Mobile聯結器設定完成後，使用者即可設定使用者群組和許可權。

AEM Mobile On-Demand聯結器可用來將AEM Mobile管理的內容與Adobe Experience Manager Mobile的On-Demand服務繫結。 這可讓內容作者使用AEM工具建立及管理行動應用程式的素材，同時使用AEM Mobile的On-Demand Services輕鬆發佈行動內容。

>[!NOTE]
>
>此為設定AEM例項的一次性步驟。

### 設定AEM Mobile On-demand Services使用者端 {#configuring-aem-mobile-on-demand-services-client}

完成設定步驟，讓AEM Mobile整合正確運作。

1. 前往OSGI服務設定

   1. AEM >工具>作業> Web主控台
   1. 捲動或搜尋&#x200B;***Experience ManagerMobile On-demand Services使用者端(AdobeDigital Publishing Solution使用者端)***

1. 編輯&#x200B;***Experience ManagerMobile On-demand Services使用者端***

   1. **（必要）**&#x200B;輸入必要欄位：

      1. 使用者端ID。
      1. 使用者端密碼。

   1. **（選擇性）**&#x200B;編輯現有值。

1. 儲存變更。
1. 以下是設定範例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 設定AEM Mobile On-demand Services雲端服務 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 前往「Cloud Service」。

   1. AEM >工具>部署> [雲端服務](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)。 捲動或搜尋&#x200B;***Adobe Experience Manager Mobile隨選服務***

1. 選取&#x200B;***立即設定***&#x200B;或&#x200B;***顯示設定***，然後選取新增設定圖示。

1. 建立設定

   1. 輸入標題和名稱
   1. 輸入裝置ID
   1. 輸入裝置Token
   1. 選取&#x200B;***測試裝置組態***，以便您驗證輸入的值
   1. 選取確定

## 新增AEM Mobile使用者角色與指派許可權 {#adding-aem-mobile-user-roles-and-assigning-permissions}

建立專案後，您應建立角色並授予使用者存取許可權。 只有主要管理員可以建立和編輯角色。 當您建立角色時，您可為獲指派這些許可權的使用者啟用權能（或許可權）。 例如，您可以建立一個包含應用程式建置許可權的角色，以及另一個包含建立和發佈內容許可權的角色。

在AEM Mobile應用程式開發中，有三個不同的角色：

* 管理員
* 開發人員
* 作者

如需以不同許可權建立角色（例如建立應用程式或建立和發佈內容）的詳細資訊，請按一下AEM Mobile說明中的[建立使用者角色並授與存取權](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html)。

>[!NOTE]
>
>管理應用程式內容需要開發人員、內容作者和管理員共同作出努力。 作者操控頁面，這些頁面又以應用程式開發人員產生的範本和元件為基礎。 最後，管理員策略性地發佈更新的應用程式內容。 設定AEM群組和許可權會定義它們在應用程式控制面板或控制中心中的角色。
>
>請參閱[AEM Mobile儀表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

當您完成建立具有不同許可權的角色（例如建立應用程式或建立與發佈內容）時，請參閱&#x200B;[**設定您的使用者和使用者群組**](/help/mobile/aem-mobile-configure-users.md)。 這麼做可協助您設定使用者和群組，以支援行動應用程式的製作和管理。

### 其他資源 {#additional-resources}

若要進一步瞭解建立AEM Mobile On-demand Services應用程式的其他兩個角色和責任，請參閱下列資源：

* [為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>若要預覽應用程式內容（包括瀏覽頁面和文章），請參閱[使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)。
