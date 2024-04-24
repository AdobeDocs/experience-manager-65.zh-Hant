---
title: 建立節點
description: 瞭解如何從/libs複製所需的最少檔案數並在/apps中編輯，以自訂版本覆蓋評論系統。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# 建立節點 {#create-nodes}

複製最少需要的檔案數，以自訂版本覆蓋註解系統 `/libs` 到 `/apps` 並在中進行修改 `/apps`.

>[!CAUTION]
>
>/libs資料夾的內容永遠不會被編輯，因為任何重新安裝或升級都可能會刪除或取代/libs資料夾，而/apps資料夾的內容則保持不變。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 在author執行個體上，從/apps資料夾中建立路徑開始，這個路徑與/libs資料夾中覆蓋元件的路徑相同。

要複製的路徑為：

* `/libs/social/commons/components/hbs/comments/comment`

路徑中的某些節點是資料夾，某些則是元件。

1. 瀏覽至 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 建立 `/apps/social` （如果尚未存在）
   * 選取 `/apps` 節點
   * **[!UICONTROL 建立>資料夾]**
      * 輸入名稱： `social`
1. 選取 `social` 節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**
      * 輸入名稱： `commons`
1. 選取 `commons` 節點
   * **[!UICONTROL 建立>資料夾]**
      * 輸入名稱： `components`
1. 選取 `components` 節點
   * **[!UICONTROL 建立>資料夾]**.
      * 輸入名稱： `hbs`
1. 選取 `hbs` 節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 建立元件]**
      * 輸入標籤： `comments`
      * 輸入標題： `Comments`
      * 輸入說明： `List of comments without showing avatars`
      * 超級型別： `social/commons/components/comments`
      * 輸入群組： `Communities`
      * 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 確定]**
1. 選取 `comments` 節點

   * **[!UICONTROL 建立]** > **[!UICONTROL 建立元件]**

      * 輸入標籤： `comment`
      * 輸入標題： `Comment`
      * 輸入說明： `A comment instance without avatars`
      * 超級型別： `social/commons/components/comments/comment`
      * 輸入群組： `.hidden`
      * 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 確定]**
   * 選取 **[!UICONTROL 全部儲存]**
1. 刪除預設值 `comments.jsp`
   * 選取節點 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選取 **[!UICONTROL 刪除]**
1. 刪除預設的comment.jsp
   * 選取節點 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選取 **[!UICONTROL 刪除]**
   * 選取 **[!UICONTROL 全部儲存]**

>[!NOTE]
>
>若要保留繼承鏈， `Super Type` (屬性 `sling:resourceSuperType`)，其值會設定為與 `Super Type` 覆蓋的元件數目，在此案例中為：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

覆蓋圖自己的 `Type`(屬性 `sling:resourceType`)必須是相對自我參照，如此一來，在/apps中找不到的任何內容都會在/libs中尋找。
* 名稱：`sling:resourceType`
* 類型：`String`
* 值： `social/commons/components/hbs/comments`

1. 選取綠色 `[+] Add`
   * 名稱：`sling:resourceType`
   * 類型：`String`
   * 值： `social/commons/components/hbs/comments/comment`
1. 選取綠色 `[+] Add`
   * 選取 **[!UICONTROL 全部儲存]**

![create-nodes](assets/create-nodes.png)
