---
title: 上傳共用資源
seo-title: Uploading Shared Resources
description: 「內容管理」動作是協助建立及管理應用程式內內容的基礎要素。 請詳閱本頁面，了解如何上傳共用資源。
seo-description: Content Management actions are the building blocks that help to create and manage content within an application. Follow this page to learn about uploading shared resources.
uuid: f3595299-1279-4b94-9a49-9d1893250549
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 958461b0-4cbb-452b-88ea-9b98ada14750
exl-id: 4b3acc7c-f1f7-4837-ae3a-9435d6ce1349
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 上傳共用資源 {#uploading-shared-resources}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

「內容管理」動作是協助建立及管理應用程式內內容的基礎要素。 會對應用程式內的內容執行下列動作。

>[!NOTE]
>
>若要進一步了解AEM Mobile應用程式的設計考量事項，請參閱 [AEM Mobile應用程式的設計考量事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html) 中。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

## 上傳共用資源 {#uploading-shared-resources-1}

通常，所有作者甚至應用程式的內容（例如文章）都必須有相同的外觀和感覺。 因此，讓所有人都能使用指令碼、css和字型至關重要。 此操作會將此類共用資源發送到Mobile On-Demand，然後，Mobile On-Demand會根據需要使用。

設定應用程式並將其與雲端設定建立關聯後，即可上傳您的共用資源。 如需將應用程式與雲端設定關聯的詳細步驟，請按一下 [此處](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md).

>[!NOTE]
>
>共用資源使用ContentSync來收集所有不同的資源。 請參閱 [具有ContentSync的行動](/help/mobile/mobile-ondemand-contentsync.md) 以取得更多詳細資訊。

請依照下列步驟上傳文章的共用資源：

1. 從中選取文章 **管理文章** 方塊。
1. 按一下 **上傳共用資源** 上傳共用HTML資源。

   ![chlimage_1-133](assets/chlimage_1-133.png)

### 下一步 {#the-next-step}

在您學習建立和發佈內容後，請參閱

* [為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)

或仍需了解製作主題，請參閱

[為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)
