---
title: 應用程式建立和配置操作
seo-title: Application Create and Configuration Actions
description: 建立應用通常是建立和管理AEM Mobile按需內容的第一步。 請按照此頁瞭解詳細資訊。
seo-description: Creating an app is often the first step towards creating and managing AEM Mobile On-Demand content. Follow this page to learn more.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# 應用程式建立和配置操作{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

## 建立按需應用程式 {#creating-an-on-demand-application}

建立應用通常是建立和管理AEM Mobile按需內容的第一步，通常在管理員級別AEM執行。 它表示內容外殼，可在移動設備上查看，可隨時顯示作者建立的內容，如文章、影像、收藏等。

可以在儀表板或AEM Mobile控制中心中查看應用的詳細資訊。

>[!NOTE]
>
>儀表板是一系列有用的磁貼，可概述應用的內容、元資料和AEM Mobile按需連接狀態。
>
>請參閱 [AEM Mobile應用程式儀表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 的雙曲餘切值。

**要建立按需應用，請執行以下操作：**

1. 選擇 **移動** 從側軌上。
1. 選擇 **應用** 的子菜單。
1. 按一下 **建立** 選擇 **應用** 下拉。
1. 選擇移動應用模板，然後按一下 **下一個**。
1. 輸入應用屬性，如 **標題**。 **名稱**。 **說明**。
1. 按一下&#x200B;**下一步**。
1. 如果已知，請輸入雲配置詳細資訊，否則按一下 **建立**。
1. 按一下 **完成** 查看目錄中的新AEM Mobile應用。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>此過程允許您在中建立應用實例AEM。

## 使用應用模板 {#using-app-templates}

應用程式模板提供了一種利用開發人員建立的現有設計的簡便方法，這些設計用於在中建立新應AEM用。

什麼是應用模板？ 將其視為表示應用的基線或基礎的頁面模板和元件的集合。
在基於另一個應用的模板建立新應用時，您將得到一個應用，該應用的起始點代表從中建立該應用的應用。

您必須擁有現有的移動應用模板（或安裝了應用模板的應用）才能使用此功能。

### 下一步 {#the-next-step}

從應用程式儀表板建立按需應用程式後，下一步是將您的應用程式與雲配置相關聯。

請參閱 [將應用與雲配置關聯](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) 的子菜單。

### 前進 {#getting-ahead}

一旦您熟悉建立按需應用程式並因此將該應用程式與雲配置相關聯，請參閱 [內容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

**內容管理操作** 涉及以下內容的建立和管理：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [正在上載共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

要瞭解管理員和開發人員的角色和職責，請參閱以下資源：

* [開發AEMAEM Mobile On-demand Services內容](/help/mobile/aem-mobile-on-demand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
