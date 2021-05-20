---
title: 應用程式建立和配置操作
seo-title: 應用程式建立和配置操作
description: 建立應用程式通常是建立和管理AEM Mobile On-Demand內容的第一步。 請詳閱本頁以了解更多。
seo-description: 建立應用程式通常是建立和管理AEM Mobile On-Demand內容的第一步。 請詳閱本頁以了解更多。
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 應用程式建立和配置操作{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

## 建立按需應用程式{#creating-an-on-demand-application}

建立應用程式通常是建立和管理AEM Mobile隨選內容的第一步，通常是在AEM管理員層級執行。 它代表內容殼層，可在行動裝置上檢視，可顯示作者建立的內容，例如文章、影像、集合等。

您可以在控制面板或AEM Mobile控制中心中檢視應用程式的詳細資訊。

>[!NOTE]
>
>「控制面板」是一系列實用圖磚，可提供應用程式內容、中繼資料和AEM Mobile隨選連線狀態的概觀。
>
>如需詳細資訊，請參閱[AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 。

**若要建立隨選應用程式：**

1. 從側邊欄選取&#x200B;**Mobile**。
1. 從導航中選擇&#x200B;**Apps**。
1. 按一下「**建立**」並從下拉式清單中選取「**應用程式**」。
1. 選擇「行動應用程式」範本，然後按一下&#x200B;**Next**。
1. 輸入應用程式屬性，例如&#x200B;**Title**、**Name**、**Description**。
1. 按一下&#x200B;**下一步**。
1. 如果已知，請輸入雲配置詳細資訊，否則按一下&#x200B;**Create**。
1. 按一下&#x200B;**Done**&#x200B;以在目錄中檢視您的新AEM Mobile應用程式。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>此程式可讓您在AEM中建立應用程式例項。

## 使用應用程式範本{#using-app-templates}

應用程式範本可讓您輕鬆運用開發人員建立的現有設計，以在AEM內建立新應用程式。

什麼是應用程式範本？ 將其想像為頁面範本和元件的集合，這些範本和元件代表應用程式的基準或基礎。
根據其他應用程式的範本建立新應用程式時，您會看到某個應用程式的起始點代表，該應用程式即為建立該應用程式的來源。

您必須有現有的行動應用程式範本（或已安裝應用程式範本的應用程式）才能使用此功能。

### 下一步{#the-next-step}

從應用程式控制面板建立隨選應用程式後，下一步就是將您的應用程式與雲端設定建立關聯。

如需詳細資訊，請參閱[將應用程式與雲端設定關聯](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) 。

### 搶先一步{#getting-ahead}

在您熟悉如何建立隨需應用程式，從而將該應用程式與雲配置關聯後，請參閱[內容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

**內容管** 理操作涉及以下內容的建立和管理：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
