---
title: 雲端設定
description: 將隨選應用程式關聯至雲端設定，可讓Adobe Experience Manager (AEM)建立雙向連結，直接與Mobile On-Demand代管專案通訊。 請依照此頁面瞭解更多資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 5%

---

# 雲端設定{#cloud-configuration}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

將隨選應用程式關聯至雲端設定，可讓Adobe Experience Manager (AEM)建立雙向連結，直接與Mobile On-Demand代管專案通訊。 將應用程式連結至Mobile On-Demand專案後，您就能在AEM內建立內容（例如文章、橫幅和集合），並將內容提供至Mobile On-Demand。

從那裡，發佈、預覽和管理內容變得可行。 您也可以將現有的Mobile On-Demand內容匯入AEM並執行內容編輯。

## 設定雲端設定 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>開始為On-Demand應用程式設定雲端設定之前，您必須熟悉AEM Mobile布建和設定AEM Mobile On-demand Services使用者端。
>
>如需詳細資訊，請參閱管理一節中的[設定AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md)。

若要設定Mobile On-DemandCloud Service，請從您的應用程式儀表板按一下&#x200B;**管理連線**&#x200B;圖磚右上角的齒輪。

您應熟悉應用程式控制面板和可用的圖磚。 如需詳細資訊，請參閱[AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

### 設定雲端設定的連結 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>確保您有現有的隨選使用者端和雲端設定。
>
>如需詳細資訊，請參閱管理一節中的[設定AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md)。

下列步驟說明如何設定雲端設定的連結：

1. 從&#x200B;**Mobile**，選擇&#x200B;**應用程式**，然後從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下&#x200B;**管理連線**&#x200B;圖磚上的齒輪圖示。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 輸入現有的設定，或輸入&#x200B;**設定標題**、**裝置識別碼**&#x200B;和&#x200B;**裝置權杖**&#x200B;來建立設定。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 驗證您的&#x200B;**裝置識別碼**&#x200B;和&#x200B;**裝置代號**&#x200B;後，請從清單中選擇您的隨選專案。

   按一下「**提交**」。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   **管理連線**&#x200B;圖磚會顯示您的雲端設定。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >如果您嘗試變更此應用程式與哪個專案相關聯，在控制面板中切換專案時，您將會收到內容完整性問題的警告，如下圖所示：

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 後續步驟 {#the-next-steps}

為您的應用程式設定雲端設定後，請參閱以下管理內容的資源：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
