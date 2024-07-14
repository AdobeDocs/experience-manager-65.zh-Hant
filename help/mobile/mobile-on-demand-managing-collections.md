---
title: 管理集合
description: 系列代表定義良好的貯體，其中填充了適合封面主題的文章或橫幅等內容。 請依照此頁面瞭解更多資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 管理集合{#managing-collections}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

內容管理動作是建置區塊，可協助您建立和管理應用程式中的內容。 以下是對應用程式內的內容執行的動作。

## 集合概述 {#collections-overview}

集合代表定義明確的&#x200B;*貯體*，其中包含適合封面主題的文章或橫幅等內容。

>[!NOTE]
>
>請參閱線上說明中的下列資源，以瞭解AEM Mobile應用程式中的下列主題：
>
>* [設計考量](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理集合](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>

## 建立集合 {#creating-a-collection}

建立集合的一般工作流程如下：

1. 從側邊欄選取&#x200B;**行動裝置**。
1. 在Mobile中，從目錄選擇您的Mobile On-Demand應用程式。
1. 按一下&#x200B;**管理系列**&#x200B;圖磚右上角的向下箭頭。
1. 完成精靈的每個步驟，以繼續建立您的新文章。
1. 準備就緒後，按一下&#x200B;**建立**。
1. 您的新文章會顯示在&#x200B;**管理集合**&#x200B;圖磚中。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 匯入新的集合 {#importing-a-new-collection}

現有的Mobile On-Demand內容可以從Mobile On-Demand下載（匯入）到AEM。 如此可讓您編輯與檢視本機內容。

>[!NOTE]
>
>匯入不包含影像。

匯入新集合的工作流程

1. 在Mobile中，從目錄選擇您的Mobile On-Demand應用程式。
1. 按一下&#x200B;**管理集合**&#x200B;圖磚右上角的向下箭頭，然後選取「匯入集合」。
1. 在對話方塊上按一下&#x200B;**匯入集合**，然後關閉。
1. 您的Mobile On-Demand集合現在會顯示在&#x200B;**管理集合**&#x200B;圖磚中。

>[!CAUTION]
>
>先關聯Mobile On-Demand連線。

## 編輯集合 {#editing-a-collection}

使用內建的AEM拖放編輯器來新增或變更文章。 可以新增/移除文字和影像等元件。 可以插入來自DAM Assets的影像。

編輯集合的工作流程：

1. 在Mobile中，從目錄選擇您的Mobile On-Demand應用程式。
1. 從&#x200B;**管理集合**&#x200B;圖磚選取AEM來源文章。
1. 從清單檢視中按一下醒目提示的集合，以在內容編輯器中開啟它。
1. 使用內容編輯器拖曳集合內容（手稿、影像、文字等）。

### 檢視和編輯收藏集中的中繼資料 {#viewing-and-editing-the-metadata-within-a-collection}

系列具有許多屬性，例如標題、說明、影像。 此動作用於檢視及修改這類屬性。 這些變更可選擇在儲存時上傳至Mobile On-Demand。

檢視/編輯集合的一般工作流程：

1. 在Mobile中，從目錄選擇您的Mobile On-Demand應用程式。
1. 從&#x200B;**管理集合**&#x200B;圖磚中選擇集合。

1. 從動作列中選取&#x200B;**屬性**。
1. 檢視該文章的所有可用中繼資料。
1. 如有需要，請編輯中繼資料，完成時請按一下&#x200B;**儲存**。
1. 或者，您可以立即將變更上傳至Mobile On-Demand。

## 上傳集合 {#uploading-a-collection}

上傳動作會複製所選內容並將其新增至Mobile On-Demand專案。 現有行動隨選內容已由新版本取代。

上傳集合的一般工作流程：

1. 從&#x200B;**Mobile**，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在&#x200B;**管理集合**&#x200B;圖磚中，選取要上傳至Mobile On-Demand的文章。
1. 如有需要，可從清單檢視新增更多集合。
1. 從動作列選取&#x200B;**上傳**，然後按一下對話方塊中的[上傳]。
1. 您的集合現在已上傳至Mobile On-Demand。

## 刪除集合 {#deleting-a-collection}

此作業會從Mobile On-Demand刪除選取的集合，並選擇性地從本機AEM執行個體刪除。

刪除集合的一般工作流程：

1. 在Mobile中，從目錄選擇您的Mobile On-Demand應用程式。
1. 在&#x200B;**管理集合**&#x200B;方塊中選取要刪除的文章。
1. 確定已在清單中選取它；視需要選取要刪除的其他專案。
1. 按一下動作列中的&#x200B;**刪除**。
1. 檢查您是否要從AEM和Mobile On-Demand中刪除。
1. 按一下&#x200B;**刪除**。
1. 您的集合現在已從清單中移除。

## 新增內容至集合 {#adding-content-to-collections}

集合本質上是一類相關內容。 這類功能會將文章、橫幅等內容收集在一起，放入可定義應用程式導覽結構的套件中。 集合可採用巢狀結構。

>[!NOTE]
>
>內容必須先上傳至Mobile On-Demand，才能新增至集合。

集合基本上是相關內容的類別：它們將文章、橫幅等內容收集在一起，成為定義應用程式導覽結構的套件。 集合可採用巢狀結構。

1. 在Mobile中，從目錄選擇您的Mobile On-Demand應用程式。
1. 選取先前上傳的文章（或橫幅/集合）
1. 從動作列選擇「新增至」。
1. 從對話方塊中選取先前上傳的集合。
1. 按一下&#x200B;**更新**&#x200B;以新增內容至集合。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 後續步驟 {#the-next-steps}

如需有關管理集合的資訊，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
