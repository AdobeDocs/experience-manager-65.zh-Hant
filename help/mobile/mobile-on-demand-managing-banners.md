---
title: 管理橫幅
seo-title: Managing Banners
description: 橫幅通常代表圖形促銷連結。 請詳閱本頁以了解更多。
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# 管理橫幅{#managing-banners}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

「內容管理」動作是協助建立及管理應用程式內內容的基礎要素。 會對應用程式內的內容執行下列動作。

## 橫幅概述 {#banners-overview}

橫幅通常代表圖形促銷連結。

>[!NOTE]
>
>請參閱線上說明中的下列資源，了解AEM Mobile應用程式中的下列主題：
>
>* [設計考量事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [建立橫幅](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>


## 建立橫幅 {#creating-a-banner}

建立文章的一般工作流程如下：

1. 選擇 **行動** 從側邊欄。
1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 按一下 **管理橫幅** 方塊。
1. 執行精靈的每個步驟，繼續建立新橫幅。
1. 準備就緒後，按一下 **建立**.
1. 您的新橫幅會顯示在 **管理橫幅** 方塊。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 匯入新橫幅 {#importing-a-new-banner}

現有的行動隨選內容可從Mobile On-Demand下載（匯入）至AEM。 這可允許編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包含影像。

匯入新文章的工作流程

1. 從「行動」中，從目錄中選擇您的行動隨選應用程式。
1. 按一下 **管理橫幅** 並選取「匯入橫幅」。
1. 按一下 **匯入橫幅** ，然後按一下「關閉」。
1. 您的行動隨選文章現在會顯示在 **管理橫幅** 方塊。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

## 編輯橫幅 {#editing-a-banner}

使用內建的AEM拖放編輯器來新增或變更文章。 可新增/移除文字和影像等元件。 可插入DAM Assets的影像。

>[!CAUTION]
>
>編輯器中只能開啟在AEM中建立的橫幅。

編輯文章的工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 從**管理橫幅**方塊中選取AEM來源的橫幅。
1. 從清單檢視中按一下醒目提示的橫幅，以在內容編輯器中開啟它。
1. 使用內容編輯器來拖曳橫幅內容（手稿、影像、文字等）。

### 在橫幅中檢視和編輯中繼資料 {#viewing-and-editing-the-metadata-within-a-banner}

橫幅有許多屬性，例如標題、說明、影像。 此動作用於檢視和修改此類屬性。 （可選）這些變更可在儲存時上傳至Mobile On-Demand。

檢視/編輯文章的一般工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 從 **管理橫幅** 方塊。

1. 選擇 **屬性** 從動作列。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，然後按一下 **儲存** 時才能使用。
1. （可選）立即將變更上傳至Mobile On-Demand。

## 上傳橫幅 {#uploading-a-banner}

上傳動作會複製選取的內容，並將其新增至行動隨選專案。 已有的行動隨選內容會由新版本取代。

上傳橫幅的一般工作流程：

1. 從 **行動**，請從目錄中選擇您的Mobile On-Demand應用程式。
1. 在 **管理橫幅** 圖磚上，選取要上傳至「行動隨選」的橫幅。
1. 視需要從清單檢視新增更多橫幅。
1. 選擇 **上傳** 在動作列中，按一下對話方塊中的「上傳」 。
1. 您的橫幅現在已上傳至Mobile On-Demand。

![chlimage_1-7](assets/chlimage_1-7.gif)

## 刪除橫幅 {#deleting-a-banner}

此操作會從Mobile On-Demand中刪除所選橫幅，並（可選）從本地AEM實例刪除。

刪除橫幅的一般工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 在 **管理橫幅** 方塊。
1. 確認已在清單中選取（視需要選取其他項目以刪除）。
1. 按一下 **刪除** 從動作列。
1. 檢查您是否要從AEM以及Mobile On-Demand中刪除。
1. 按一下&#x200B;**刪除**。
1. 您的橫幅現在會從清單中移除。

### 後續步驟 {#the-next-steps}

若要了解如何管理橫幅廣告，請參閱

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
