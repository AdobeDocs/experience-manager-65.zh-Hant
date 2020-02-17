---
title: 建立節點
seo-title: 建立節點
description: 覆蓋注釋系統
seo-description: 覆蓋注釋系統
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 建立節點 {#create-nodes}

將注釋系統與自訂版本重疊，方法是將所需的最少檔案從/libs複製至/apps並在/apps中修改。

>[!CAUTION]
>
>不會編輯/libs資料夾的內容，因為任何重新安裝或升級都可能會刪除或取代/libs資料夾，而/apps資料夾的內容則未受影響。

在作 [者例項上使用CRXDE](../../help/sites-developing/developing-with-crxde-lite.md) Lite，首先在/apps檔案夾中建立路徑，該路徑與/libs檔案夾中重疊元件的路徑相同。

要複製的路徑為

* `/libs/social/commons/components/hbs/comments/comment`

路徑中的某些節點是資料夾，有些是元件。

1. 瀏覽至 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 建 `/apps/social` 立（如果尚不存在）
   * 選擇節 `/apps` 點
   * **[!UICONTROL 「建立>資料夾……」]**
      * 輸入名稱: `social`
1. 選擇節 `social` 點
   * **[!UICONTROL 建立>資料夾……]**
      * 輸入名稱: `commons`
1. 選擇節 `commons` 點
   * **[!UICONTROL 建立>資料夾……]**
      * 輸入名稱: `components`
1. 選擇節 `components` 點
   * **[!UICONTROL 「建立>資料夾。.]**.」
      * 輸入名稱: `hbs`
1. 選擇節 `hbs` 點
   * **[!UICONTROL 「建立>建立元件……」]**
      * 輸入標籤： `comments`
      * Enter Title: `Comments`
      * Enter Description: `List of comments without showing avatars`
      * 超級類型: `social/commons/components/comments`
      * 輸入組： `Communities`
      * 按一下「 **[!UICONTROL Next]** （下一步）」直到 **[!UICONTROL 「OK（確定）」]**
1. 選擇節 `comments` 點

   * **[!UICONTROL 「建立>建立元件……」]**

      * 輸入標籤： `comment`
      * Enter Title: `Comment`
      * Enter Description: `A comment instance without avatars`
      * 超級類型: `social/commons/components/comments/comment`
      * 輸入組： `.hidden`
      * 按一下「 **[!UICONTROL Next]** （下一步）」直到 **[!UICONTROL 「OK（確定）」]**
   * 選擇「 **[!UICONTROL 全部保存」]**
1. 刪除預設值 `comments.jsp`
   * 選擇節點 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選擇刪 **[!UICONTROL 除]**
1. 刪除預設注釋。jsp
   * 選擇節點 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選擇刪 **[!UICONTROL 除]**
   * 選擇「 **[!UICONTROL 全部保存」]**

>[!NOTE]
>
>為了保留繼承鏈，覆蓋元件的 `Super Type` (屬性 `sling:resourceSuperType`)設定為與要覆蓋的元件 `Super Type` 的相同值，在這種情況下
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`
>



覆蓋本身(屬 `Type`性 `sling:resourceType`)必須是相對的自我參考，如此在/apps中找不到的任何內容就會在/libs中尋找。
* 名稱: `sling:resourceType`
* 類型: `String`
* 值: `social/commons/components/hbs/comments`

1. 選擇綠色 `[+] Add`
   * 名稱: `sling:resourceType`
   * 類型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 選擇綠色 `[+] Add`
   * 選擇「 **[!UICONTROL 全部保存」]**

![chlimage_1-4](assets/chlimage_1-4.png)

