---
title: 編輯啟動
seo-title: 編輯啟動
description: 為頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動復本中的內容。
seo-description: 為頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動復本中的內容。
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 3%

---

# 編輯啟動{#editing-launches}

## 編輯啟動頁面{#editing-launch-pages}

為頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動復本中的內容。

1. 開啟頁面進行編輯。
1. 在Sidekick中，選擇&#x200B;**Versioning**&#x200B;標籤，然後展開&#x200B;**Launches**&#x200B;組。 目前正在編輯的啟動標題會使用粗體字型。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 選擇要處理的啟動，然後按一下&#x200B;**Switch**。
1. 開始編輯。

   >[!NOTE]
   >
   >您可以使用Sidekick的&#x200B;**Page**&#x200B;標籤來執行動作，例如&#x200B;**建立子頁面**&#x200B;等。

## 編輯啟動配置{#editing-a-launch-configuration}

建立啟動後，您可以變更啟動名稱和啟動日期。 您也可以指定要與啟動相關聯的影像。

1. 開啟啟動管理頁面([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))。

1. 選擇所需的啟動，然後按一下&#x200B;**Edit**&#x200B;以開啟對話框：

   * 在&#x200B;**一般**&#x200B;標籤中，您可以編輯：

      * **標題**
      * **上線日期**:這等同於啟動日期
      * **生產就緒**

      如需這些欄位的用途和互動的相關資訊，請參閱[啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events)。

   * 在&#x200B;**Image**&#x200B;標籤中，可以上傳影像檔案。


1. 按一下「**儲存**」。

## 探索頁面{#discovering-the-launch-status-of-a-page}的啟動狀態

編輯頁面的啟動時，有關啟動的資訊會顯示在Sidekick的&#x200B;**Versioning**&#x200B;標籤底部：

* 啟動的名稱。
* 上次變更後的時間。
* 執行上次變更的使用者。
* **Production Ready**&#x200B;標幟的狀態(orange=not set;green=set)。

![chlimage_1-186](assets/chlimage_1-186.png)
