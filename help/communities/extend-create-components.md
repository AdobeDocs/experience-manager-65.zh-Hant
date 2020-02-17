---
title: 建立元件
seo-title: 建立元件
description: 建立注釋元件
seo-description: 建立注釋元件
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 建立元件 {#create-the-components}

擴展元件的示例使用注釋系統，該系統實際上由兩個元件組成

* 注釋——包含的注釋系統，是放置在頁面上的元件
* Comment —— 擷取已張貼留言之例項的元件

這兩個元件都必須到位，尤其是自訂已張貼留言的外觀時。

>[!NOTE]
>
>每個網站頁面僅允許一個注釋系統。
>
>許多Communities功能已包含注釋系統，其resourceType可修改以參考擴充的注釋系統。

## 建立注釋元件 {#create-the-comments-component}

這些方向會指 **定Group** （群組）值， `.hidden` 以便從元件瀏覽器(sidekick)使用元件。

刪除自動建立的JSP檔案是因為將改用預設的HBS檔案。

1. 瀏覽至 **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. 建立自訂應用程式的位置：

   * 選擇節 `/apps` 點

      * **建立名為** custom的資 **[!UICONTROL 料夾]**
   * 選擇節 `/apps/custom` 點

      * **建立名為元件的資料夾** (Create Folder **[!UICONTROL )]**


1. 選擇節 `/apps/custom/components` 點

   * **[!UICONTROL 「建立>元件……」]**

      * **標籤**:注 *釋*
      * **標題**:替 *代注釋*
      * **說明**:替 *代注釋樣式*
      * **超類型**: *social/commons/components/hbs/comments*
      * **群組**:自 *訂*
   * 選擇下 **[!UICONTROL 一步]**
   * 選擇下 **[!UICONTROL 一步]**
   * 選擇下 **[!UICONTROL 一步]**
   * 選擇「確 **[!UICONTROL 定」]**


1. 展開剛建立的節點： `/apps/custom/components/comments`
1. 選擇「 **[!UICONTROL 全部保存」]**
1. 按一下滑鼠右鍵 `comments.jsp`
1. 選擇刪 **[!UICONTROL 除]**
1. 選擇「 **[!UICONTROL 全部保存」]**

![chlimage_1-70](assets/chlimage_1-70.png)

### 建立子注釋元件 {#create-the-child-comment-component}

這些指示將 **Group** (組 `.hidden` )設定為，因為頁面中應僅包含父元件。

刪除自動建立的JSP檔案是因為將改用預設的HBS檔案。

1. 導航到節 `/apps/custom/components/comments` 點
1. 按一下右鍵節點

   * 選擇「 **[!UICONTROL 建立」>「元件……」。]**

      * **標籤**:評 *論*
      * **標題**:替 *代注釋*
      * **說明**:替代 *注釋樣式*
      * **超類型**: *social/commons/components/hbs/comments/comments*
      * **群組**: `*.hidden*`
   * 選擇下 **[!UICONTROL 一步]**
   * 選擇下 **[!UICONTROL 一步]**
   * 選擇下 **[!UICONTROL 一步]**
   * 選擇「確 **[!UICONTROL 定」]**


1. 展開剛建立的節點： `/apps/custom/components/comments/comment`
1. 選擇「 **[!UICONTROL 全部保存」]**
1. 按一下滑鼠右鍵 `comment.jsp`
1. 選擇刪 **[!UICONTROL 除]**
1. 選擇「 **[!UICONTROL 全部保存」]**

![chlimage_1-71](assets/chlimage_1-71.png) ![chlimage_1-72](assets/chlimage_1-72.png)

### 複製和修改預設HBS指令碼 {#copy-and-modify-the-default-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 複製 `comments.hbs`

   * 來 [自/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 至 [/應用程式／自訂／元件／留言](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編輯 `comments.hbs` 至：

   * 變更屬性的 `data-scf-component` 值(~line 20):

      * 從 `social/commons/components/hbs/comments`
      * 至 `/apps/custom/components/comments`
   * 修改以包含自訂注釋元件(~line 75):

      * 取代 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * 使用 `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* 複製 `comment.hbs`

   * 來 [自/libs/social/commons/components/hbs/comments/comments/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 至 [/apps/custom/components/comments/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編輯 `comment.hbs` 至：

   * 更改data-scf-component屬性的值(~ line 19)

      * 從 `social/commons/components/hbs/comments/comment`
      * 至 `/apps/custom/components/comments/comment`

* 選擇節 `/apps/custom` 點
* 選擇「 **[!UICONTROL 全部保存」]**

## 建立客戶端庫資料夾 {#create-a-client-library-folder}

為避免明確包含此客戶端庫，可以使用( `cq.social.author.hbs.comments`)預設注釋系統的clientlib的類別值，但預設元件的所有實例也將包含此clientlib。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 選擇節 `/apps/custom/components/comments` 點
* 選擇 **[!UICONTROL 建立節點]**

   * **名稱**: `clientlibs`
   * **類型**: `cq:ClientLibraryFolder`
   * 「添加到屬 **[!UICONTROL 性]** 」頁籤：

      * **名稱** Type `categories` **Value** Zhing `String`****`cq.social.author.hbs.comments``Multi`
      * **名稱** Type `dependencies` **Value** Zhing `String`****`cq.social.scf``Multi`

* 選擇「 **[!UICONTROL 全部保存」]**
* 在選 `/apps/custom/components/comments/clientlib`取s節點後，建立3個檔案：

   * **名稱**: `css.txt`
   * **名稱**: `js.txt`
   * **名稱**:customcommentsystem.js

* 輸入&#39;customcommentsystem.js&#39;作為 `js.txt`
* 選擇「 **[!UICONTROL 全部保存」]**

![chlimage_1-73](assets/chlimage_1-73.png)

## 註冊SCF模型和視圖 {#register-the-scf-model-view}

在擴展（覆蓋）SCF元件時，resourceType不同(覆蓋使用以前搜索的相對搜索機制，以 `/apps` 使 `/libs` resourceType保持不變)。 這就是為什麼必須編寫JavaScript（在用戶端程式庫中）來註冊SCF JS模型並檢視自訂resourceType。

輸入以下文本作為內容 `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* 選擇「 **[!UICONTROL 全部保存」]**

## 發佈應用程式 {#publish-the-app}

為了在發佈環境中體驗擴展元件，需要複製自定義元件。

一種方法是

* 從全域導覽

   * 選擇 **[!UICONTROL 工具>部署>複製]**
   * 選取 `Activate Tree`
   * 設定 `Start Path`:to `/apps/custom`
   * 取消選中 `Only Modified`
   * 「選擇」 `Activate`按鈕

