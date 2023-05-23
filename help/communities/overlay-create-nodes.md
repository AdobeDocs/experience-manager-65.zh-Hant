---
title: 建立節點
seo-title: Create Nodes
description: 覆蓋注釋系統
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

將注釋系統與自定義版本重疊，方法是複製注釋系統中所需的最少檔案數 `/libs` 入 `/apps` 修改 `/apps`。

>[!CAUTION]
>
>/libs資料夾的內容從不編輯，因為任何重新安裝或升級都可能刪除或替換/libs資料夾，而/apps資料夾的內容保持不變。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 在作者實例上，首先在/apps資料夾中建立路徑，該路徑與/libs資料夾中重疊元件的路徑相同。

要複製的路徑是：

* `/libs/social/commons/components/hbs/comments/comment`

路徑中的某些節點是資料夾，有些是元件。

1. 瀏覽到 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 建立 `/apps/social` （如果尚不存在）
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
   * **[!UICONTROL 建立>資料夾……]**。
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
   * 選擇 **[!UICONTROL 全部保存]**
1. 刪除預設 `comments.jsp`
   * 選擇節點 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選擇 **[!UICONTROL 刪除]**
1. 刪除預設的comment.jsp
   * 選擇節點 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選擇 **[!UICONTROL 刪除]**
   * 選擇 **[!UICONTROL 全部保存]**

>[!NOTE]
>
>為保留繼承鏈， `Super Type` （屬性） `sling:resourceSuperType`)的值與 `Super Type` 在本例中：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


覆蓋本身 `Type`（屬性） `sling:resourceType`)必須是相對的自引用，以便在/apps中找不到的任何內容，然後在/libs中查找。
* 名稱: `sling:resourceType`
* 類型: `String`
* 值: `social/commons/components/hbs/comments`

1. 選擇綠色 `[+] Add`
   * 名稱: `sling:resourceType`
   * 類型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 選擇綠色 `[+] Add`
   * 選擇 **[!UICONTROL 全部保存]**

![建立節點](assets/create-nodes.png)
