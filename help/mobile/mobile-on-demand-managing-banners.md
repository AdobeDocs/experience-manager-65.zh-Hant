---
title: 管理橫幅
seo-title: 管理橫幅
description: 橫幅通常代表圖形促銷連結。 請依照本頁進一步瞭解。
seo-description: 橫幅通常代表圖形促銷連結。 請依照本頁進一步瞭解。
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理橫幅{#managing-banners}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

內容管理動作是協助建立和管理應用程式內容的建立區塊。 對應用程式內的內容執行下列動作。

## 橫幅概觀 {#banners-overview}

橫幅通常代表圖形促銷連結。

>[!NOTE]
>
>請參閱「線上說明」中的下列資源，以瞭解AEM mobile應用程式中的下列主題：
>
>* [設計考量](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [建立橫幅](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>



## 建立橫幅 {#creating-a-banner}

建立文章的一般工作流程如下：

1. 從側 **欄選取** 「行動」。
1. 從Mobile，從目錄中選擇您的Mobile On-Demand應用程式。
1. 按一下「管理橫幅」方塊右上角的 **向下箭頭** 。
1. 在精靈的每個步驟中都可繼續建立新橫幅。
1. 準備就緒後，按一下「 **建立**」。
1. 您的新橫幅會出現在「管 **理橫幅** 」方塊中。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 匯入新橫幅 {#importing-a-new-banner}

現有的Mobile On-Demand內容可從Mobile On-Demand下載（匯入）至AEM。 這可讓您編輯和檢視本機內容。

>[!NOTE]
>
>匯入不包含影像。

匯入新文章的工作流程

1. 從Mobile，從目錄中選擇您的行動隨選應用程式。
1. 按一下「管理橫幅」方塊右上角的向下箭 **頭** ，並選取「匯入橫幅」。
1. 按一 **下對話方塊上的** 「匯入橫幅」，然後按一下「關閉」。
1. 您的行動隨選文章現在會顯示在「管理橫 **幅」方塊** 。

>[!CAUTION]
>
>您必須先建立行動隨選連線的關聯。

## 編輯橫幅 {#editing-a-banner}

使用內建的AEM拖放編輯器來新增或變更文章。 可新增／移除文字和影像等元件。 可插入DAM資產的影像。

>[!CAUTION]
>
>只有在AEM中建立的橫幅才能在編輯器中開啟。

編輯文章的工作流程：

1. 從Mobile，從目錄中選擇您的Mobile On-Demand應用程式。
1. 從**「管理橫幅**」方塊選取AEM來源的橫幅。
1. 按一下清單檢視中反白顯示的橫幅，在內容編輯器中將其開啟。
1. 使用內容編輯器拖曳橫幅內容（手稿、影像、文字等）。

### 在橫幅中檢視和編輯中繼資料 {#viewing-and-editing-the-metadata-within-a-banner}

橫幅包含許多屬性，例如標題、說明、影像。 此操作用於查看和修改這些屬性。 （可選）這些變更可在儲存時上傳至Mobile On-Demand。

檢視／編輯文章的一般工作流程：

1. 從Mobile，從目錄中選擇您的Mobile On-Demand應用程式。
1. 從「管理橫幅」方塊 **中選擇橫幅** 。

1. 從操 **作欄中** ，選擇屬性。
1. 檢視該文章的所有可用中繼資料。
1. 視需要編輯中繼資料，然後在完成時 **按一下** 「儲存」。
1. （可選）立即將變更上傳至Mobile On-Demand。

## 上傳橫幅 {#uploading-a-banner}

上傳動作會複製選取的內容，並將其新增至Mobile On-Demand專案。 現有的行動隨選內容會由新版本取代。

上傳橫幅的一般工作流程：

1. 從 **Mobile**，從型錄中選擇您的Mobile On-Demand應用程式。
1. 在「管 **理橫幅** 」方塊中，選取要上傳至Mobile On-Demand的橫幅。
1. 視需要從清單檢視新增更多橫幅。
1. 從動 **作列選取** 「上傳」，然後在對話方塊中按一下「上傳」。
1. 您的橫幅現在會上傳到Mobile On-Demand。

![chlimage_1-7](assets/chlimage_1-7.gif)

## 刪除橫幅 {#deleting-a-banner}

此作業會從Mobile On-Demand中刪除選取的橫幅，並選擇性地從本機AEM例項中刪除。

刪除橫幅的一般工作流程：

1. 從Mobile，從目錄中選擇您的Mobile On-Demand應用程式。
1. 在「管理橫幅」方塊中選取要刪 **除的橫幅** 。
1. 請確定清單中已選取（視需要選取其他要刪除的項目）。
1. 按一 **下動作列** 中的「刪除」。
1. 檢查您是否要從AEM和Mobile On-Demand中刪除。
1. 按一 **下刪除**。
1. 您的橫幅現在會從清單中移除。

### 後續步驟 {#the-next-steps}

在您瞭解如何管理橫幅廣告後，請參閱

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理系列](/help/mobile/mobile-on-demand-managing-collections.md)
* [上傳共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈／取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
