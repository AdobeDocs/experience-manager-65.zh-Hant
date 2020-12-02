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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 6%

---


# 建立節點{#create-nodes}

將從`/libs`至`/apps`所需的最少檔案數複製至`/apps`並修改至&lt;a2/>，以自訂版本覆蓋註解系統。

>[!CAUTION]
>
>不會編輯/libs資料夾的內容，因為任何重新安裝或升級都可能會刪除或取代/libs資料夾，而/apps資料夾的內容則未受影響。

在作者實例上使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)，首先在/apps資料夾中建立路徑，該路徑與/libs資料夾中覆蓋元件的路徑相同。

要複製的路徑為：

* `/libs/social/commons/components/hbs/comments/comment`

路徑中的某些節點是資料夾，有些是元件。

1. 瀏覽至[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 建立`/apps/social`（如果尚未存在）
   * 選擇`/apps`節點
   * **[!UICONTROL 「建立>資料夾……」]**
      * 輸入名稱: `social`
1. 選擇`social`節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 資料夾……]**
      * 輸入名稱: `commons`
1. 選擇`commons`節點
   * **[!UICONTROL 建立>資料夾……]**
      * 輸入名稱: `components`
1. 選擇`components`節點
   * **[!UICONTROL 建立>資料夾。.]**.
      * 輸入名稱: `hbs`
1. 選擇`hbs`節點
   * **[!UICONTROL 建立]** >創 **[!UICONTROL 建元件……]**
      * 輸入標籤：`comments`
      * 輸入標題：`Comments`
      * 輸入說明：`List of comments without showing avatars`
      * 超級類型: `social/commons/components/comments`
      * 輸入組：`Communities`
      * 按一下&#x200B;**[!UICONTROL Next]**&#x200B;直到&#x200B;**[!UICONTROL OK]**
1. 選擇`comments`節點

   * **[!UICONTROL 建立]** >創 **[!UICONTROL 建元件……]**

      * 輸入標籤：`comment`
      * 輸入標題：`Comment`
      * 輸入說明：`A comment instance without avatars`
      * 超級類型: `social/commons/components/comments/comment`
      * 輸入組：`.hidden`
      * 按一下&#x200B;**[!UICONTROL Next]**&#x200B;直到&#x200B;**[!UICONTROL OK]**
   * 選擇&#x200B;**[!UICONTROL 全部保存]**
1. 刪除預設`comments.jsp`
   * 選擇節點`/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選擇&#x200B;**[!UICONTROL Delete]**
1. 刪除預設注釋。jsp
   * 選擇節點`/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選擇&#x200B;**[!UICONTROL Delete]**
   * 選擇&#x200B;**[!UICONTROL 全部保存]**

>[!NOTE]
>
>為保留繼承鏈，覆蓋元件的`Super Type`（屬性`sling:resourceSuperType`）設為與要覆蓋元件的`Super Type`相同的值，在這種情況下：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


覆蓋本身的`Type`（屬性`sling:resourceType`）必須是相對的自我參考，如此在/apps中找不到的任何內容就會在/libs中尋找。
* 名稱: `sling:resourceType`
* 類型: `String`
* 值: `social/commons/components/hbs/comments`

1. 選擇綠色`[+] Add`
   * 名稱: `sling:resourceType`
   * 類型: `String`
   * 值: `social/commons/components/hbs/comments/comment`
1. 選擇綠色`[+] Add`
   * 選擇&#x200B;**[!UICONTROL 全部保存]**

![create-nodes](assets/create-nodes.png)

