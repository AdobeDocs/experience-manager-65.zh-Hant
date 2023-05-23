---
title: 管理集合
seo-title: Managing Collections
description: 收藏品代表一個定義清晰的儲存桶，裡面裝滿了適合封面主題的文章或橫幅等內容。 請按照此頁瞭解詳細資訊。
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
ht-degree: 1%

---

# 管理集合{#managing-collections}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

內容管理操作是幫助建立和管理應用程式內內容的構造塊。 對應用程式內的內容執行以下操作。

## 收集概述 {#collections-overview}

集合表示定義良好 *桶* 滿是符合封面主題的文章或橫幅等內容。

>[!NOTE]
>
>請參閱聯機幫助中的以下資源，以瞭解AEM Mobile應用中的以下主題：
>
>* [設計注意事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理集合](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>


## 建立集合 {#creating-a-collection}

建立集合的一般工作流如下：

1. 選擇 **移動** 從側軌上。
1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 按一下右上角的向下箭頭 **管理集合** 平鋪。
1. 通過嚮導的每個步驟繼續建立新項目。
1. 準備好後，按一下 **建立**。
1. 您的新文章將出現在 **管理集合** 平鋪。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 導入新集合 {#importing-a-new-collection}

現有移動按需內容可從移動按需下載（導入）到AEM。 這允許編輯和查看本地內容。

>[!NOTE]
>
>導入不包括映像。

導入新集合的工作流

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 按一下右上角的向下箭頭 **管理集合** 平鋪，然後選擇「導入集合」。
1. 按一下 **導入集合** ，然後選擇「關閉」。
1. 您的移動按需收集現在顯示在 **管理集合** 平鋪。

>[!CAUTION]
>
>必須先關聯移動按需連接。

## 編輯集合 {#editing-a-collection}

使用內置的AEM拖放編輯器添加或更改項目。 可以添加/刪除文本和影像等元件。 可以插入DAM Assets中的影像。

要編輯集合的工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 從中選AEM擇源項目 **管理集合** 平鋪。
1. 從清單視圖中按一下突出顯示的集合，在內容編輯器中將其開啟。
1. 使用內容編輯器拖動收集內容（手稿、影像、文本等）。

### 查看和編輯集合中的元資料 {#viewing-and-editing-the-metadata-within-a-collection}

集合具有許多屬性，如標題、說明、影像。 此操作用於查看和修改此類屬性。 （可選）這些更改可在保存後上載到Mobile On-Demand。

檢視/編輯集合的常規工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 從 **管理集合** 平鋪。

1. 選擇 **屬性** 按鈕。
1. 查看該文章的所有可用元資料。
1. 編輯元資料（如果需要），然後按一下 **保存** 完成。
1. （可選）立即將更改上載到Mobile On-Demand。

## 上載集合 {#uploading-a-collection}

上載操作將複製所選內容並將其添加到移動按需項目。 現有的Mobile On-Demand內容已被新版本取代。

要上載集合的常規工作流：

1. 從 **移動**，從目錄中選擇您的Mobile On-Demand應用。
1. 在 **管理集合** 平鋪，選擇要上載到Mobile On-Demand的項目。
1. 如果需要，從清單視圖添加更多集合。
1. 選擇 **上載** 在操作欄中，然後按一下對話框中的上載。
1. 您的集合現在已上載到Mobile On-Demand。

## 刪除集合 {#deleting-a-collection}

此操作將從Mobile On-Demand中刪除選定的集合，或從本地實例中刪AEM除。

要刪除集合的常規工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 選擇要刪除的文章 **管理集合** 平鋪。
1. 確保在清單中選中了它（根據需要選擇要刪除的其他選項）。
1. 按一下 **刪除** 按鈕。
1. 檢查是否要從Mobile On-DemandAEM和Mobile On-Demand中刪除。
1. 按一下&#x200B;**刪除**。
1. 您的收藏現在已從清單中刪除。

## 將內容添加到集合 {#adding-content-to-collections}

集合本質上是相關內容的類別。 它們將文章、橫幅等內容收集到定義應用程式導航結構的包中。 集合可以嵌套。

>[!NOTE]
>
>必須先將內容上載到Mobile On-Demand，然後才能將其添加到集合。

集合本質上是一類相關內容：它們將文章、橫幅等內容收集到定義應用程式導航結構的包中。 集合可以嵌套。

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 選擇以前上載的文章（或橫幅/收藏）
1. 從操作欄中選擇「添加到」。
1. 從對話框中選擇以前上載的集合。
1. 按一下 **更新** 來添加內容。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 後續步驟 {#the-next-steps}

瞭解管理收藏的資訊，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [正在上載共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用印前檢查預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
