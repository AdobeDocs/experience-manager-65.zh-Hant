---
title: 建立元件
description: 瞭解如何使用由「註釋」和「註釋」元件組成的註釋系統來擴充元件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 建立元件  {#create-the-components}

延伸元件的範例使用由兩個元件組成的註解系統。

* 註解 — 放在頁面上的元件所構成的註解系統。
* 評論 — 擷取已張貼評論之例項的元件。

兩個元件都必須放置到位，尤其是如果自訂張貼的註解的外觀。

>[!NOTE]
>
>每個網站頁面只允許一個註解系統。
>
>許多Communities功能已經包含註解系統，其resourceType可以修改為參考擴充的註解系統。

## 建立註解元件 {#create-the-comments-component}

這些指示會指定`.hidden`以外的&#x200B;**群組**&#x200B;值，以便元件可以從元件瀏覽器(sidekick)使用。

刪除自動建立的JSP檔案是因為會改用預設的HBS檔案。

1. 瀏覽至&#x200B;**CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. 建立自訂應用程式的位置：

   * 選取`/apps`節點

      * **建立名為**[!UICONTROL &#x200B;自訂&#x200B;]**的資料夾**

   * 選取`/apps/custom`節點

      * **建立名為**[!UICONTROL &#x200B;元件&#x200B;]**的資料夾**

1. 選取`/apps/custom/components`節點

   * **[!UICONTROL 建立>元件……]**

      * **標籤**： *註解*
      * **標題**： *替代註解*
      * **描述**： *替代註解樣式*
      * **超級型別**： *social/commons/components/hbs/comments*
      * **群組**： *自訂*

   * 選取&#x200B;**[!UICONTROL 下一步]**
   * 選取&#x200B;**[!UICONTROL 下一步]**
   * 選取&#x200B;**[!UICONTROL 下一步]**
   * 選取&#x200B;**[!UICONTROL 確定]**

1. 展開已建立的節點： `/apps/custom/components/comments`
1. 選取&#x200B;**[!UICONTROL 全部儲存]**
1. 用滑鼠右鍵按一下`comments.jsp`
1. 選取&#x200B;**[!UICONTROL 刪除]**
1. 選取&#x200B;**[!UICONTROL 全部儲存]**

![create-component](assets/create-component.png)

### 建立子註解元件 {#create-the-child-comment-component}

這些方向將&#x200B;**群組**&#x200B;設定為`.hidden`，因為只有父元件應包含在頁面中。

刪除自動建立的JSP檔案是因為會改用預設的HBS檔案。

1. 導覽至`/apps/custom/components/comments`節點
1. 以滑鼠右鍵按一下節點

   * 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 元件……]**

      * **標籤**： *註解*
      * **標題**： *替代註解*
      * **描述**： *替代註解樣式*
      * **超級型別**： *social/commons/components/hbs/comments/comment*
      * **群組**： `*.hidden*`

   * 選取&#x200B;**[!UICONTROL 下一步]**
   * 選取&#x200B;**[!UICONTROL 下一步]**
   * 選取&#x200B;**[!UICONTROL 下一步]**
   * 選取&#x200B;**[!UICONTROL 確定]**

1. 展開已建立的節點： `/apps/custom/components/comments/comment`
1. 選取&#x200B;**[!UICONTROL 全部儲存]**
1. 用滑鼠右鍵按一下`comment.jsp`
1. 選取&#x200B;**[!UICONTROL 刪除]**
1. 選取&#x200B;**[!UICONTROL 全部儲存]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### 複製及修改預設HBS指令碼 {#copy-and-modify-the-default-hbs-scripts}

使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 複製`comments.hbs`

   * 來自[/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 至[/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編輯`comments.hbs`至：

   * 變更`data-scf-component`屬性的值（~第20行）：

      * 來自`social/commons/components/hbs/comments`
      * 至`/apps/custom/components/comments`

   * 修改以包含自訂註解元件（第75行）：

      * 取代`{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * 與`{{include this resourceType='/apps/custom/components/comments/comment'}}`

* 複製`comment.hbs`

   * 從[/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 至[/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編輯`comment.hbs`至：

   * 變更data-scf-component屬性的值（~第19行）

      * 來自`social/commons/components/hbs/comments/comment`
      * 至`/apps/custom/components/comments/comment`

* 選取`/apps/custom`節點
* 選取&#x200B;**[!UICONTROL 全部儲存]**

## 建立使用者端資源庫資料夾 {#create-a-client-library-folder}

若要避免包含此使用者端程式庫，可以使用預設註解系統clientlib的類別值( `cq.social.author.hbs.comments`)。 不過，此clientlib隨後也必須包含在預設元件的所有執行個體中。

使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 選取`/apps/custom/components/comments`節點
* 選取&#x200B;**[!UICONTROL 建立節點]**

   * **名稱**：`clientlibs`
   * **類型**：`cq:ClientLibraryFolder`
   * 新增至&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤：

      * **名稱** `categories` **型別** `String` **值** `cq.social.author.hbs.comments` `Multi`
      * **名稱** `dependencies` **型別** `String` **值** `cq.social.scf` `Multi`

* 選取&#x200B;**[!UICONTROL 全部儲存]**
* 選取`/apps/custom/components/comments/clientlib`節點後，建立三個檔案：

   * **名稱**：`css.txt`
   * **名稱**：`js.txt`
   * **名稱**： customcommentsystem.js

* 輸入&#39;customcommentsystem.js&#39;作為`js.txt`的內容
* 選取&#x200B;**[!UICONTROL 全部儲存]**

![comments-clientlibs](assets/comments-clientlibs.png)

## 註冊SCF模型與檢視 {#register-the-scf-model-view}

延伸（覆寫） SCF元件時，resourceType不同（覆寫使用相對搜尋機制，在`/libs`前搜尋`/apps`，使resourceType保持相同）。 這就是為什麼需要編寫JavaScript （在使用者端程式庫中）來註冊SCF JS模型和檢視自訂resourceType的原因。

輸入下列文字作為`customcommentsystem.js`的內容：

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

* 選取&#x200B;**[!UICONTROL 全部儲存]**

## 應用程式Publish {#publish-the-app}

若要在發佈環境中體驗擴充元件，必須複製自訂元件。

其中一個方法是：

* 從全域導覽，

   * 選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
   * 選取&#x200B;**[!UICONTROL 啟動樹狀結構]**
   * 將`Start Path`設為`/apps/custom`
   * 取消核取&#x200B;**[!UICONTROL Only Modified]**
   * 選取&#x200B;**[!UICONTROL 啟動]**&#x200B;按鈕
