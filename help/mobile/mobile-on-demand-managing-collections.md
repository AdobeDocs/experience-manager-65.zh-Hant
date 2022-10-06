---
title: 管理集合
seo-title: Managing Collections
description: 集合代表定義完善的貯體，裡面裝滿了符合封面主題的文章或橫幅等內容。 請詳閱本頁以了解更多。
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# 管理集合{#managing-collections}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

「內容管理」動作是協助建立及管理應用程式內內容的基礎要素。 會對應用程式內的內容執行下列動作。

## 集合概述 {#collections-overview}

集合代表定義良好的 *貯體* 滿是符合封面主題的文章或橫幅等內容。

>[!NOTE]
>
>請參閱線上說明中的下列資源，了解AEM Mobile應用程式中的下列主題：
>
>* [設計考量事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理集合](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>


## 建立集合 {#creating-a-collection}

建立集合的一般工作流程如下：

1. 選擇 **行動** 從側邊欄。
1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 按一下 **管理集合** 方塊。
1. 執行精靈的每個步驟，繼續建立新文章。
1. 準備就緒後，按一下 **建立**.
1. 新文章會顯示在 **管理集合** 方塊。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 匯入新集合 {#importing-a-new-collection}

現有的行動隨選內容可從Mobile On-Demand下載（匯入）至AEM。 這可允許編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包含影像。

匯入新集合的工作流程

1. 從「行動」中，從目錄中選擇您的行動隨選應用程式。
1. 按一下 **管理集合** 並選取「匯入集合」 。
1. 按一下 **匯入集合** ，然後按一下「關閉」。
1. 您的行動隨選集合現在會顯示在 **管理集合** 方塊。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

## 編輯集合 {#editing-a-collection}

使用內建的AEM拖放編輯器來新增或變更文章。 可新增/移除文字和影像等元件。 可插入DAM Assets的影像。

編輯集合的工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 從中選取AEM來源的文章 **管理集合** 方塊。
1. 從清單檢視中按一下醒目提示的集合，以在內容編輯器中開啟。
1. 使用內容編輯器拖曳收藏內容（手稿、影像、文字等）。

### 檢視和編輯集合中的中繼資料 {#viewing-and-editing-the-metadata-within-a-collection}

集合有許多屬性，例如標題、說明、影像。 此動作用於檢視和修改此類屬性。 （可選）這些變更可在儲存時上傳至Mobile On-Demand。

檢視/編輯集合的一般工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 從 **管理集合** 方塊。

1. 選擇 **屬性** 從動作列。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，然後按一下 **儲存** 時才能使用。
1. （可選）立即將變更上傳至Mobile On-Demand。

## 上傳集合 {#uploading-a-collection}

上傳動作會複製選取的內容，並將其新增至行動隨選專案。 已有的行動隨選內容會由新版本取代。

上傳集合的一般工作流程：

1. 從 **行動**，請從目錄中選擇您的Mobile On-Demand應用程式。
1. 在 **管理集合** 圖磚上，選取要上傳至「行動隨選」的文章。
1. 視需要從清單檢視新增更多集合。
1. 選擇 **上傳** 在動作列中，按一下對話方塊中的「上傳」 。
1. 您的集合現在已上傳至Mobile On-Demand。

## 刪除集合 {#deleting-a-collection}

此操作會從Mobile On-Demand中刪除所選集合，並（可選）從本地AEM實例刪除。

刪除集合的一般工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 在 **管理集合** 方塊。
1. 確認已在清單中選取（視需要選取其他項目以刪除）。
1. 按一下 **刪除** 從動作列。
1. 檢查您是否要從AEM以及Mobile On-Demand中刪除。
1. 按一下&#x200B;**刪除**。
1. 您的集合現在會從清單中移除。

## 新增內容至集合 {#adding-content-to-collections}

集合實質上是相關內容的類別。 它們會將文章、橫幅等內容收集到可定義應用程式導覽結構的套件中。 集合可以巢狀化。

>[!NOTE]
>
>內容必須先上傳至Mobile On-Demand，才能新增至集合。

集合本質上是相關內容的類別：它們會將文章、橫幅等內容收集到可定義應用程式導覽結構的套件中。 集合可以巢狀化。

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 選取先前上傳的文章（或橫幅/系列）
1. 從操作欄中選擇「添加到」。
1. 從對話方塊選取先前上傳的集合。
1. 按一下 **更新** 將內容新增至集合。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 後續步驟 {#the-next-steps}

若要了解如何管理系列，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
