---
title: 管理文章
seo-title: 管理文章
description: 請詳閱本頁，了解如何建立及管理文章。
seo-description: 請詳閱本頁，了解如何建立及管理文章。
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 管理文章{#managing-articles}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

「內容管理」動作是協助您在應用程式中建立及管理文章的基礎要素。 應用程式內的文章會執行下列動作。

## 文章概述{#articles-overview}

文章表示基於文本的文本，並附有用於傳達資訊的藝術。

>[!NOTE]
>
>請參閱線上說明中的下列資源，了解AEM Mobile應用程式中的下列主題：
>
>* [設計考量事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [管理文章](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)

>



## 建立文章{#creating-an-article}

建立文章的一般工作流程如下：

1. 從側邊欄選取&#x200B;**Mobile**。
1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 按一下「管理文章&#x200B;**」方塊右上角的向下箭頭。**
1. 選擇文章模板，然後按一下&#x200B;**Next**。
1. 執行精靈的每個步驟，繼續建立新文章。
1. 準備就緒後，按一下&#x200B;**Create**。
1. 您的新文章會顯示在「管理文章&#x200B;**」方塊中。**

## 匯入新文章{#importing-a-new-article}

現有的行動隨選內容可從Mobile On-Demand下載（匯入）至AEM。 這可允許編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包含影像。

匯入新文章的工作流程

1. 從「行動」中，從目錄中選擇您的行動隨選應用程式。
1. 按一下&#x200B;**管理文章**&#x200B;方塊右上角的向下箭頭，然後選取「匯入文章」。
1. 按一下對話方塊上的「**匯入文章**」，然後按一下「關閉」。
1. 您的行動隨選文章現在會顯示在&#x200B;**管理文章**&#x200B;方塊中。

>[!CAUTION]
>
>您必須先關聯Mobile On-Demand連線。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 編輯文章{#editing-an-article}

使用內建的AEM拖放編輯器來新增或變更文章。 可新增/移除文字和影像等元件。 可插入DAM Assets的影像。

>[!CAUTION]
>
>編輯器中只能開啟在AEM中建立的文章。

編輯文章的工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 從&#x200B;**管理文章**&#x200B;方塊選取AEM來源的文章。
1. 從清單檢視中按一下醒目提示的文章，以在內容編輯器中開啟它。
1. 使用內容編輯器來拖曳文章內容（手稿、影像、文字等）。

### 檢視和編輯文章{#viewing-and-editing-the-metadata-within-an-article}中的中繼資料

文章、橫幅等內容擁有許多屬性，例如標題、說明、影像。 此動作用於檢視和修改此類屬性。 （可選）這些變更可在儲存時上傳至Mobile On-Demand。

檢視/編輯文章的一般工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 從&#x200B;**管理文章**&#x200B;方塊中選擇文章。

1. 從操作欄中選擇&#x200B;**查看屬性**。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，並在完成時按一下&#x200B;**儲存**。
1. （可選）立即將變更上傳至Mobile On-Demand。

## 上傳文章{#uploading-an-article}

上傳動作會複製選取的內容，並將其新增至行動隨選專案。 已有的行動隨選內容會由新版本取代。

上傳文章的一般工作流程：

1. 從&#x200B;**Mobile**，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在&#x200B;**管理文章**&#x200B;方塊中，選取要上傳至Mobile On-Demand的文章。
1. 視需要從清單檢視新增更多文章。
1. 從操作欄中選擇&#x200B;**Upload**，然後按一下對話框中的Upload。
1. 您的文章現在已上傳至Mobile On-Demand。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 刪除文章{#deleting-an-article}

此操作會從Mobile On-Demand刪除所選內容，並選擇性地從本機AEM例項刪除。

刪除文章的一般工作流程：

1. 從「行動」中，從目錄中選擇您的「行動隨選」應用程式。
1. 在&#x200B;**管理文章**&#x200B;方塊中選取要刪除的文章。
1. 確認已在清單中選取（視需要選取其他項目以刪除）。
1. 按一下動作列中的&#x200B;**Delete**。
1. 檢查您是否要從AEM以及Mobile On-Demand中刪除。
1. 按一下&#x200B;**Delete**。
1. 您的文章現在會從清單中移除。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 後續步驟{#the-next-steps}

若要了解如何管理文章，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
