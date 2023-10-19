---
title: 建立元件
description: 瞭解如何使用由「註釋」和「註釋」元件組成的註釋系統來擴充元件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

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

這些方向會指定 **群組** 以外的值 `.hidden` 因此，元件可從元件瀏覽器(sidekick)取得。

刪除自動建立的JSP檔案是因為會改用預設的HBS檔案。

1. 瀏覽至 **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. 建立自訂應用程式的位置：

   * 選取 `/apps` 節點

      * **建立資料夾** 已命名 **[!UICONTROL 自訂]**

   * 選取 `/apps/custom` 節點

      * **建立資料夾** 已命名 **[!UICONTROL 元件]**

1. 選取 `/apps/custom/components` 節點

   * **[!UICONTROL 建立>元件……]**

      * **標籤**： *評論*
      * **標題**： *替代註解*
      * **說明**： *替代註解樣式*
      * **超級型別**： *social/commons/components/hbs/comments*
      * **群組**： *自訂*

   * 選取 **[!UICONTROL 下一個]**
   * 選取 **[!UICONTROL 下一個]**
   * 選取 **[!UICONTROL 下一個]**
   * 選取 **[!UICONTROL 確定]**

1. 展開已建立的節點： `/apps/custom/components/comments`
1. 選取 **[!UICONTROL 全部儲存]**
1. 按一下右鍵 `comments.jsp`
1. 選取 **[!UICONTROL 刪除]**
1. 選取 **[!UICONTROL 全部儲存]**

![create-component](assets/create-component.png)

### 建立子註解元件 {#create-the-child-comment-component}

這些方向已設定 **群組** 至 `.hidden` 因為頁面中僅應包含父元件。

刪除自動建立的JSP檔案是因為會改用預設的HBS檔案。

1. 導覽至 `/apps/custom/components/comments` 節點
1. 以滑鼠右鍵按一下節點

   * 選取 **[!UICONTROL 建立]** > **[!UICONTROL 元件……]**

      * **標籤**： *評論*
      * **標題**： *替代註解*
      * **說明**： *替代註解樣式*
      * **超級型別**： *social/commons/components/hbs/comments/comment*
      * **群組**： `*.hidden*`

   * 選取 **[!UICONTROL 下一個]**
   * 選取 **[!UICONTROL 下一個]**
   * 選取 **[!UICONTROL 下一個]**
   * 選取 **[!UICONTROL 確定]**

1. 展開已建立的節點： `/apps/custom/components/comments/comment`
1. 選取 **[!UICONTROL 全部儲存]**
1. 按一下右鍵 `comment.jsp`
1. 選取 **[!UICONTROL 刪除]**
1. 選取 **[!UICONTROL 全部儲存]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### 複製及修改預設HBS指令碼 {#copy-and-modify-the-default-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 複製 `comments.hbs`

   * 從 [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 至 [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編輯 `comments.hbs` 至：

   * 變更 `data-scf-component` 屬性（~第20行）：

      * 從 `social/commons/components/hbs/comments`
      * 至 `/apps/custom/components/comments`

   * 修改以包含自訂註解元件（第75行）：

      * 取代 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * 替換為 `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* 複製 `comment.hbs`

   * 從 [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 至 [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編輯 `comment.hbs` 至：

   * 變更data-scf-component屬性的值（~第19行）

      * 從 `social/commons/components/hbs/comments/comment`
      * 至 `/apps/custom/components/comments/comment`

* 選取 `/apps/custom` 節點
* 選取 **[!UICONTROL 全部儲存]**

## 建立使用者端資源庫資料夾 {#create-a-client-library-folder}

若要避免包含此使用者端程式庫，可以使用預設註解系統clientlib的類別值( `cq.social.author.hbs.comments`)。 不過，此clientlib隨後也必須包含在預設元件的所有執行個體中。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 選取 `/apps/custom/components/comments` 節點
* 選取 **[!UICONTROL 建立節點]**

   * **名稱**：`clientlibs`
   * **類型**：`cq:ClientLibraryFolder`
   * 新增至 **[!UICONTROL 屬性]** 標籤：

      * **名稱** `categories` **型別** `String` **值** `cq.social.author.hbs.comments` `Multi`
      * **名稱** `dependencies` **型別** `String` **值** `cq.social.scf` `Multi`

* 選取 **[!UICONTROL 全部儲存]**
* 替換為 `/apps/custom/components/comments/clientlib`s節點已選取，請建立三個檔案：

   * **名稱**：`css.txt`
   * **名稱**：`js.txt`
   * **名稱**： customcommentsystem.js

* 輸入&#39;customcommentsystem.js&#39;作為的內容 `js.txt`
* 選取 **[!UICONTROL 全部儲存]**

![comments-clientlibs](assets/comments-clientlibs.png)

## 註冊SCF模型與檢視 {#register-the-scf-model-view}

延伸（覆寫） SCF元件時，resourceType會不同（覆寫使用搜尋範圍的相關搜尋機制） `/apps` 早於 `/libs` 以使resourceType保持相同)。 這就是為什麼需要編寫JavaScript （在使用者端程式庫中）來註冊SCF JS模型和檢視自訂resourceType的原因。

輸入下列文字作為 `customcommentsystem.js`：

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

* 選取 **[!UICONTROL 全部儲存]**

## 發佈應用程式 {#publish-the-app}

若要在發佈環境中體驗擴充元件，必須複製自訂元件。

其中一個方法是：

* 從全域導覽，

   * 選取 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**
   * 選取 **[!UICONTROL 啟動樹狀結構]**
   * 設定 `Start Path` 至 `/apps/custom`
   * 取消核取 **[!UICONTROL 僅限已修改的專案]**
   * 選取 **[!UICONTROL 啟動]** 按鈕
