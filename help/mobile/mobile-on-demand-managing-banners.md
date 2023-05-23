---
title: 管理橫幅
seo-title: Managing Banners
description: 橫幅通常表示圖形促銷連結。 請按照此頁瞭解詳細資訊。
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
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

內容管理操作是幫助建立和管理應用程式內內容的構造塊。 對應用程式內的內容執行以下操作。

## 橫幅概述 {#banners-overview}

橫幅通常表示圖形促銷連結。

>[!NOTE]
>
>請參閱聯機幫助中的以下資源，以瞭解AEM Mobile應用中的以下主題：
>
>* [設計注意事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [建立橫幅](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>


## 建立橫幅 {#creating-a-banner}

建立項目的一般工作流如下：

1. 選擇 **移動** 從側軌上。
1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 按一下右上角的向下箭頭 **管理橫幅** 平鋪。
1. 通過嚮導的每個步驟繼續建立新橫幅。
1. 準備好後，按一下 **建立**。
1. 您的新橫幅將出現在 **管理橫幅** 平鋪。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 導入新橫幅 {#importing-a-new-banner}

現有移動按需內容可從移動按需下載（導入）到AEM。 這允許編輯和查看本地內容。

>[!NOTE]
>
>導入不包括映像。

導入新文章的工作流

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 按一下右上角的向下箭頭 **管理橫幅** 平鋪，然後選擇「導入橫幅」。
1. 按一下 **導入橫幅** ，然後選擇「關閉」。
1. 您的Mobile On-Demand文章現在出現在 **管理橫幅** 平鋪。

>[!CAUTION]
>
>必須先關聯移動按需連接。

## 編輯橫幅 {#editing-a-banner}

使用內置的AEM拖放編輯器添加或更改項目。 可以添加/刪除文本和影像等元件。 可以插入DAM Assets中的影像。

>[!CAUTION]
>
>編輯器中只AEM能開啟在中建立的橫幅。

編輯項目的工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 從**管AEM理橫幅**磁貼中選擇來源橫幅。
1. 按一下清單視圖中突出顯示的標題，在內容編輯器中將其開啟。
1. 使用內容編輯器拖動標題內容（稿件、影像、文本等）。

### 查看和編輯標題中的元資料 {#viewing-and-editing-the-metadata-within-a-banner}

條幅具有許多屬性，如標題、說明、影像。 此操作用於查看和修改此類屬性。 （可選）這些更改可在保存後上載到Mobile On-Demand。

檢視/編輯項目的常規工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 從 **管理橫幅** 平鋪。

1. 選擇 **屬性** 按鈕。
1. 查看該文章的所有可用元資料。
1. 編輯元資料（如果需要），然後按一下 **保存** 完成。
1. （可選）立即將更改上載到Mobile On-Demand。

## 上載橫幅 {#uploading-a-banner}

上載操作將複製所選內容並將其添加到移動按需項目。 現有的Mobile On-Demand內容已被新版本取代。

上載橫幅廣告的常規工作流：

1. 從 **移動**，從目錄中選擇您的Mobile On-Demand應用。
1. 在 **管理橫幅** 平鋪，選擇要上載到Mobile On-Demand的標題。
1. 如果需要，請從清單視圖添加更多條幅。
1. 選擇 **上載** 在操作欄中，然後按一下對話框中的上載。
1. 您的橫幅現已上載到Mobile On-Demand。

![chlimage_1-7](assets/chlimage_1-7.gif)

## 刪除標題 {#deleting-a-banner}

此操作會從Mobile On-Demand中刪除選定的標題，或從本地實例中刪AEM除。

要刪除橫幅廣告的常規工作流：

1. 從Mobile中，從目錄中選擇您的Mobile On-Demand應用。
1. 選擇要在 **管理橫幅** 平鋪。
1. 確保在清單中選擇了它（根據需要選擇要刪除的其他）。
1. 按一下 **刪除** 按鈕。
1. 檢查是否要從Mobile On-DemandAEM和Mobile On-Demand中刪除。
1. 按一下&#x200B;**刪除**。
1. 您的橫幅現在已從清單中刪除。

### 後續步驟 {#the-next-steps}

您瞭解管理橫幅的內容，請參閱

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [正在上載共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用印前檢查預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
