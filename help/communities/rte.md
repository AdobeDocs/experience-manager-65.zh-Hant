---
title: RTF編輯器基本知識
description: 瞭解RTF編輯器的基礎和功能，此編輯器可讓您輸入含有標示的文字。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# RTF編輯器基本知識 {#rich-text-editor-essentials}

## 概觀 {#overview}

RTF編輯器(RTE)可讓您輸入含有標示的文字。

針對Communities元件，而與 [作者環境中的RTF編輯器](../../help/sites-authoring/rich-text-editor.md)，它會影響在發佈環境中輸入的文字。

![RTF編輯器](assets/rich-text-editor.png)

## 啟用RTF編輯器 {#enabling-rich-text-editor}

允許使用者產生內容(UGC)的Communities元件可啟用以允許RTE。 將元件新增至頁面或包含在 [函式](functions.md)，預設情況下可能會啟用，也可能不會啟用RTE。

如果未啟用，只要輸入 [作者編輯模式](sites-console.md#authoring-site-content)，選取要編輯的元件，然後選取 `Rich Text Editor` 核取方塊。

RTE適用於下列Communities元件：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [評論](comments.md)
* [檔案庫](file-library.md)
* [論壇](forum.md)
* [傳送訊息](configure-messaging.md)
* [QnA](working-with-qna.md)
* [評論](reviews.md)

## 自訂 {#customization}

RTF編輯器可以自訂，因為實作是根據 [複製器](https://ckeditor.com/).

Communities元件的目前設定在 `cq.social.  scf   clientlib`，在存放庫中的

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建議修改cq.social.scf clientlib，因為日後的升級可能會覆寫任何編輯。

### 自訂範例：內嵌連結 {#example-customization-inline-links}

基於安全性考量，預設情況下顯示給成員的RTF圖示集中不包含超連結選項。 在UGC中允許href時，惡意轉換的能力很強。

若要將超連結選項新增至工具列：

* 新增名為「」的工具列 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 選取 **[!UICONTROL 全部儲存]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
