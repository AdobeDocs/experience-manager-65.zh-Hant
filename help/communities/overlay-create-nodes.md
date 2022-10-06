---
title: 建立節點
seo-title: Create Nodes
description: 覆蓋評論系統
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 7%

---

# 建立節點 {#create-nodes}

複製注釋系統所需的最少檔案數，使用自訂版本覆蓋注釋系統 `/libs` into `/apps` 在 `/apps`.

>[!CAUTION]
>
>不會編輯/libs資料夾的內容，因為任何重新安裝或升級都可以刪除或替換/libs資料夾，而/apps資料夾的內容不會更改。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 在製作例項上，首先在/apps資料夾中建立路徑，該路徑與/libs資料夾中重疊元件的路徑相同。

重複的路徑為：

* `/libs/social/commons/components/hbs/comments/comment`

路徑中的某些節點是資料夾，有些是元件。

1. 瀏覽至 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 建立 `/apps/social` （如果尚未存在）
   * 選擇 `/apps` 節點
   * **[!UICONTROL 建立>資料夾……]**
      * 輸入名稱: `social`
1. 選擇 `social` 節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 資料夾……]**
      * 輸入名稱: `commons`
1. 選擇 `commons` 節點
   * **[!UICONTROL 建立>資料夾……]**
      * 輸入名稱: `components`
1. 選擇 `components` 節點
   * **[!UICONTROL 建立>資料夾……]**.
      * 輸入名稱: `hbs`
1. 選擇 `hbs` 節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 建立元件……]**
      * 輸入標籤： `comments`
      * 輸入標題： `Comments`
      * 輸入說明: `List of comments without showing avatars`
      * 超級類型: `social/commons/components/comments`
      * 輸入組： `Communities`
      * 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 確定]**
1. 選擇 `comments` 節點

   * **[!UICONTROL 建立]** > **[!UICONTROL 建立元件……]**

      * 輸入標籤： `comment`
      * 輸入標題： `Comment`
      * 輸入說明: `A comment instance without avatars`
      * 超級類型: `social/commons/components/comments/comment`
      * 輸入組： `.hidden`
      * 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 確定]**
   * 選擇 **[!UICONTROL 全部儲存]**
1. 刪除預設值 `comments.jsp`
   * 選擇節點 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選擇 **[!UICONTROL 刪除]**
1. 刪除預設注釋.jsp
   * 選擇節點 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選擇 **[!UICONTROL 刪除]**
   * 選擇 **[!UICONTROL 全部儲存]**

>[!NOTE]
>
>為了保留繼承鏈， `Super Type` （屬性） `sling:resourceSuperType`)，則覆蓋元件的值會設為與 `Super Type` 重疊的元件，在此例中：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


覆蓋圖本身 `Type`（屬性） `sling:resourceType`)必須是相對的自我參考，這樣在/apps中找不到的任何內容，就會在/libs中尋找。
* 名稱: `sling:resourceType`
* 類型: `String`
* 值: `social/commons/components/hbs/comments`

1. 選取綠色 `[+] Add`
   * 名稱: `sling:resourceType`
   * 類型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 選取綠色 `[+] Add`
   * 選擇 **[!UICONTROL 全部儲存]**

![建立節點](assets/create-nodes.png)
