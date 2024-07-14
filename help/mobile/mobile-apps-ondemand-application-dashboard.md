---
title: AEM Mobile應用程式控制面板
description: 您可以從AEM Mobile Application Dashboard或Control Center管理應用程式和行動應用程式內容。 請依照此頁面瞭解更多資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: daafc8b8-3c01-4c97-a14b-f1b706600249
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 4%

---

# AEM Mobile應用程式控制面板 {#aem-mobile-application-dashboard}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

您可以從AEM Mobile Application Dashboard或Control Center管理應用程式和行動應用程式內容。

您可以按一下右下角的「……」，鑽研控制中心的每個圖磚，以檢視或編輯詳細資訊。

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>您可以按一下圖磚的勾選圖示（左上9個點），重新排列圖磚。 訂單變更因使用者而異 — 因個別使用者而異。

管理應用程式內容需要開發人員、內容作者和管理員共同作出努力。 作者操控頁面，這些頁面又以應用程式開發人員產生的範本和元件為基礎。

最後，管理員策略性地發佈更新的應用程式內容。

## 「管理應用程式」動態磚 {#the-manage-app-tile}

**管理應用程式**&#x200B;圖磚會顯示可用的應用程式資訊：

* 標題
* 說明
* 圖示
* 上次修改時間
* 上次修改者

![chlimage_1-55](assets/chlimage_1-55.png)

## 「管理連線」圖磚 {#the-manage-connection-tile}

**管理連線**&#x200B;圖磚會顯示AEM Mobile On-demand Services連線資訊：

* 雲端設定名稱
* 專案名稱和ID
* 連線狀態

>[!NOTE]
>
>按一下右上方的齒輪，設定Mobile On-Demand雲端設定。
>
>如需詳細資訊，請參閱[設定Mobile On-Demand Services](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)。

![chlimage_1-56](assets/chlimage_1-56.png)

## 管理實體 {#managing-entities}

這3個圖磚可提供應用程式內容狀態的概觀：

* **橫幅**
* **篇文章**
* **集合**

按一下右下角的省略符號(...)，可展開每個圖磚以提供更詳細的清單檢視。 這些清單檢視提供存取常見Mobile On Demand動作（如刪除、上傳和編輯屬性）的替代方式。

### 「管理橫幅」圖磚 {#the-manage-banners-tile}

**管理橫幅**&#x200B;圖磚可讓您管理橫幅的內容。 橫幅會顯示下列資訊：

* 影像
* **標題**：橫幅的名稱
* **已修改**：上次在AEM中修改
* **已上傳**：上次從AEM上傳
* **已發佈**：上次發佈的要求表單AEM
* **SOURCE**：來源(AEM本機或來自Mobile On Demand的遠端)

下圖顯示AEM Mobile應用程式儀表板中的&#x200B;**管理橫幅**&#x200B;圖磚：

![chlimage_1-57](assets/chlimage_1-57.png)

>[!NOTE]
>
>請參閱&#x200B;**[管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)**&#x200B;以建立、刪除或更新橫幅。

### 「管理文章」圖磚 {#the-manage-articles-tile}

**管理文章**&#x200B;圖磚可讓您管理文章的內容。 會顯示文章的下列資訊：

* 影像
* **TITLE**：文章的名稱
* **已修改**：上次在AEM中修改
* **已上傳**：上次從AEM上傳
* **已發佈**：上次發佈的要求表單AEM
* **SOURCE**：來源(AEM本機或來自Mobile On-Demand的遠端)

下圖顯示AEM Mobile應用程式儀表板中的&#x200B;**管理文章**&#x200B;動態磚：

![chlimage_1-58](assets/chlimage_1-58.png)

>[!NOTE]
>
>請參閱&#x200B;[**管理文章**](/help/mobile/mobile-on-demand-managing-articles.md)&#x200B;以建立、刪除或更新文章。

### 管理集合圖磚 {#the-manage-collections-tile}

**管理集合**&#x200B;圖磚可讓您管理集合的內容。 系統會顯示集合的下列資訊：

* 影像
* **TITLE**：集合的名稱
* **已修改**：上次在AEM中修改
* **已上傳**：上次從AEM上傳
* **已發佈**：上次發佈的要求表單AEM
* **SOURCE**：來源(AEM本機或來自Mobile On-Demand的遠端)

下圖顯示AEM Mobile應用程式儀表板中的&#x200B;**管理集合**&#x200B;圖磚：

![chlimage_1-59](assets/chlimage_1-59.png)

>[!NOTE]
>
>請參閱&#x200B;**[管理集合](/help/mobile/mobile-on-demand-managing-collections.md)**&#x200B;以建立、刪除或更新集合。

### 後續步驟 {#the-next-steps}

在您熟悉應用程式控制面板後，請參閱下列資源以建立行動應用程式：

* [應用程式建立和設定動作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [將隨選應用程式關聯至雲端設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [內容管理動作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)

### 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
