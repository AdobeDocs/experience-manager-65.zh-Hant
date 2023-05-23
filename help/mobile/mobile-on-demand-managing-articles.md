---
title: 管理文章
seo-title: Managing Articles
description: 請按照本頁瞭解有關建立和管理文章的資訊。
seo-description: Follow this page to learn about creating and managing Articles.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 管理文章{#managing-articles}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

內容管理操作是幫助在應用程式中建立和管理文章的構造塊。 對應用程式中的項目執行以下操作。

## 文章概述 {#articles-overview}

文章表示基於文本和藝術以傳遞資訊。

>[!NOTE]
>
>請參閱聯機幫助中的以下資源，以瞭解AEM Mobile應用中的以下主題：
>
>* [設計注意事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [管理文章](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>


## 建立文章 {#creating-an-article}

建立項目的一般工作流如下：

1. 選擇 **移動** 從側軌上。
1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 按一下右上角的向下箭頭 **管理文章** 平鋪。
1. 選擇文章模板並按一下 **下一個**。
1. 通過嚮導的每個步驟繼續建立新項目。
1. 準備好後，按一下 **建立**。
1. 您的新文章將出現在 **管理文章** 平鋪。

## 導入新文章 {#importing-a-new-article}

現有移動按需內容可從移動按需下載（導入）到AEM。 這允許編輯和查看本地內容。

>[!NOTE]
>
>導入不包括映像。

導入新文章的工作流

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 按一下右上角的向下箭頭 **管理文章** 平鋪並選擇「導入文章」。
1. 按一下 **導入文章** ，然後選擇「關閉」。
1. 您的Mobile On-Demand文章現在出現在 **管理文章** 平鋪。

>[!CAUTION]
>
>必須先關聯移動按需連接。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 編輯文章 {#editing-an-article}

使用內置的AEM拖放編輯器添加或更改項目。 可以添加/刪除文本和影像等元件。 可以插入DAM Assets中的影像。

>[!CAUTION]
>
>編輯器中只AEM能開啟在中建立的項目。

編輯項目的工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 從中選AEM擇源項目 **管理文章** 平鋪。
1. 從清單視圖中按一下突出顯示的項目，在內容編輯器中將其開啟。
1. 使用內容編輯器拖動文章內容（稿件、影像、文本等）。

### 查看和編輯項目中的元資料 {#viewing-and-editing-the-metadata-within-an-article}

諸如文章、橫幅等內容具有許多屬性，如標題、說明、影像。 此操作用於查看和修改此類屬性。 （可選）這些更改可在保存後上載到Mobile On-Demand。

檢視/編輯項目的常規工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 從 **管理文章** 平鋪。

1. 選擇 **查看屬性** 按鈕。
1. 查看該文章的所有可用元資料。
1. 編輯元資料（如果需要），然後按一下 **保存** 完成。
1. （可選）立即將更改上載到Mobile On-Demand。

## 上載文章 {#uploading-an-article}

上載操作將複製所選內容並將其添加到移動按需項目。 現有的Mobile On-Demand內容已被新版本取代。

上載項目的常規工作流：

1. 從 **移動**，從目錄中選擇您的Mobile On-Demand應用。
1. 在 **管理文章** 平鋪，選擇要上載到Mobile On-Demand的項目。
1. 如果需要，從清單視圖中添加更多項目。
1. 選擇 **上載** 在操作欄中，然後按一下對話框中的上載。
1. 您的文章現在已上載到Mobile On-Demand。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 刪除文章 {#deleting-an-article}

此操作從Mobile On-Demand中刪除所選內容，也可從本地實例中AEM刪除。

刪除項目的一般工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 選擇要刪除的文章 **管理文章** 平鋪。
1. 確保在清單中選中了它（根據需要選擇要刪除的其他選項）。
1. 按一下 **刪除** 按鈕。
1. 檢查是否要從Mobile On-DemandAEM和Mobile On-Demand中刪除。
1. 按一下&#x200B;**刪除**。
1. 您的文章現在已從清單中刪除。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 後續步驟 {#the-next-steps}

您瞭解管理文章的一個資訊，請參閱

* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [正在上載共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用印前檢查預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
