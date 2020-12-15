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
source-git-commit: 418e7fad2d990f1a7cb3b69ab4c290ca1b7075ba
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---


# 建立元件{#create-the-components}

擴展元件的示例使用注釋系統，該系統實際上由兩個元件組成

* 注釋——包含的注釋系統，該系統是放置在頁面上的元件。
* Comment —— 擷取已張貼留言之例項的元件。

這兩個元件都必須到位，尤其是自訂已張貼留言的外觀時。

>[!NOTE]
>
>每個網站頁面僅允許一個注釋系統。
>
>許多Communities功能已包含注釋系統，其resourceType可修改以參考擴充的注釋系統。

## 建立注釋元件{#create-the-comments-component}

這些方向指定除`.hidden`外的&#x200B;**Group**&#x200B;值，以便從元件瀏覽器(sidekick)使元件可用。

刪除自動建立的JSP檔案是因為將改用預設的HBS檔案。

1. 瀏覽至&#x200B;**CRXDE|Lite**([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. 建立自訂應用程式的位置：

   * 選擇`/apps`節點

      * **建立** Foldernamed自 **[!UICONTROL 訂]**
   * 選擇`/apps/custom`節點

      * **建立** Foldernamed元 **[!UICONTROL 件]**


1. 選擇`/apps/custom/components`節點

   * **[!UICONTROL 「建立>元件……」]**

      * **標籤**: *留言*
      * **標題**: *替代注釋*
      * **說明**: *替代注釋樣式*
      * **超類型**: *social/commons/components/hbs/comments*
      * **群組**: *自訂*
   * 選擇&#x200B;**[!UICONTROL Next]**
   * 選擇&#x200B;**[!UICONTROL Next]**
   * 選擇&#x200B;**[!UICONTROL Next]**
   * 選擇&#x200B;**[!UICONTROL 確定]**


1. 展開剛建立的節點：`/apps/custom/components/comments`
1. 選擇&#x200B;**[!UICONTROL 全部保存]**
1. 按一下右鍵`comments.jsp`
1. 選擇&#x200B;**[!UICONTROL Delete]**
1. 選擇&#x200B;**[!UICONTROL 全部保存]**

![create-component](assets/create-component.png)

### 建立子注釋元件{#create-the-child-comment-component}

這些方向將&#x200B;**Group**&#x200B;設為`.hidden`，因為頁面中應僅包含父元件。

刪除自動建立的JSP檔案是因為將改用預設的HBS檔案。

1. 導航至`/apps/custom/components/comments`節點
1. 按一下右鍵節點

   * 選擇&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 元件……]**

      * **標籤**: *評論*
      * **標題**: *替代注釋*
      * **說明**: *替代注釋樣式*
      * **超類型**: *social/commons/components/hbs/comments/comments*
      * **群組**:  `*.hidden*`
   * 選擇&#x200B;**[!UICONTROL Next]**
   * 選擇&#x200B;**[!UICONTROL Next]**
   * 選擇&#x200B;**[!UICONTROL Next]**
   * 選擇&#x200B;**[!UICONTROL 確定]**


1. 展開剛建立的節點：`/apps/custom/components/comments/comment`
1. 選擇&#x200B;**[!UICONTROL 全部保存]**
1. 按一下右鍵`comment.jsp`
1. 選擇&#x200B;**[!UICONTROL Delete]**
1. 選擇&#x200B;**[!UICONTROL 全部保存]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### 複製和修改預設HBS指令碼{#copy-and-modify-the-default-hbs-scripts}

使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 複製 `comments.hbs`

   * 從[/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 至[/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 將`comments.hbs`編輯為：

   * 更改`data-scf-component`屬性的值(~line 20):

      * 從 `social/commons/components/hbs/comments`
      * 至 `/apps/custom/components/comments`
   * 修改以包含自訂注釋元件(~line 75):

      * 取代 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * 使用 `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* 複製 `comment.hbs`

   * 從[/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 至[/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 將`comment.hbs`編輯為：

   * 更改data-scf-component屬性的值(~ line 19)

      * 從 `social/commons/components/hbs/comments/comment`
      * 至 `/apps/custom/components/comments/comment`

* 選擇`/apps/custom`節點
* 選擇&#x200B;**[!UICONTROL 全部保存]**

## 建立客戶端庫資料夾{#create-a-client-library-folder}

為避免明確包含此客戶端庫，可使用預設注釋系統的clientlib的類別值(`cq.social.author.hbs.comments`)，但是，預設元件的所有實例也將包含此clientlib。

使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 選擇`/apps/custom/components/comments`節點
* 選擇&#x200B;**[!UICONTROL 建立節點]**

   * **名稱**:  `clientlibs`
   * **類型**:  `cq:ClientLibraryFolder`
   * 添加到&#x200B;**[!UICONTROL 屬性]**&#x200B;頁籤：

      * **NameTypeValue** `categories` **** `String` **** `cq.social.author.hbs.comments` `Multi`
      * **NameTypeValue** `dependencies` **** `String` **** `cq.social.scf` `Multi`

* 選擇&#x200B;**[!UICONTROL 全部保存]**
* 選擇`/apps/custom/components/comments/clientlib`s節點後，建立3個檔案：

   * **名稱**:  `css.txt`
   * **名稱**:  `js.txt`
   * **名稱**:customcommentsystem.js

* 輸入&#39;customcommentsystem.js&#39;作為`js.txt`的內容
* 選擇&#x200B;**[!UICONTROL 全部保存]**

![comments-clientlibs](assets/comments-clientlibs.png)

## 註冊SCF型號並查看{#register-the-scf-model-view}

在擴展（覆蓋）SCF元件時，resourceType不同（覆蓋使用在`/libs`之前通過`/apps`搜索的相對搜索機制，以使resourceType保持不變）。 這就是為什麼必須編寫JavaScript（在用戶端程式庫中）來註冊SCF JS模型並檢視自訂resourceType。

輸入以下文本作為`customcommentsystem.js`的內容：

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

* 選擇&#x200B;**[!UICONTROL 全部保存]**

## 發佈應用程式{#publish-the-app}

為了在發佈環境中體驗擴展元件，需要複製自定義元件。

一種方法是：

* 從全域導覽，

   * 選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]**
   * 選擇&#x200B;**[!UICONTROL 激活樹]**
   * 將`Start Path`設為`/apps/custom`
   * 取消選中&#x200B;**[!UICONTROL 僅已修改]**
   * 選擇&#x200B;**[!UICONTROL 激活]**&#x200B;按鈕

