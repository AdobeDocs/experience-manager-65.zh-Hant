---
title: 富格文本編輯器軟體包
seo-title: Rich Text Editor Essentials
description: 富格文本編輯器功能概述
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# 富格文本編輯器軟體包 {#rich-text-editor-essentials}

## 概觀 {#overview}

富格文本編輯器(RTE)提供了輸入帶有標注的文本的功能。

對於社區元件，與 [作者環境中的富文本編輯器](../../help/sites-authoring/rich-text-editor.md)，它影響在發佈環境中輸入的文本。

![富文本編輯器](assets/rich-text-editor.png)

## 啟用RTF編輯器 {#enabling-rich-text-editor}

允許用戶生成內容(UGC)的社區元件可以啟用RTE。 根據元件是添加到頁面還是包含在 [函式](functions.md)，預設情況下，RTE可能啟用或不啟用。

如果未啟用，只需輸入 [作者編輯模式](sites-console.md#authoring-site-content)，選擇要編輯的元件，然後選擇 `Rich Text Editor` 複選框。

RTE可用於以下社區元件：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [評論](comments.md)
* [菲利布里](file-library.md)
* [論壇](forum.md)
* [傳送訊息](configure-messaging.md)
* [QnA](working-with-qna.md)
* [評論](reviews.md)

## 自定義 {#customization}

由於實現基於以下內容，因此可定製富文本編輯器 [CKEditor](https://www.ckeditor.com/)。

社區元件的當前配置位於 `cq.social.  scf   clientlib`，位於

`/libs/clientlibs/social/commons/scf/ckrte.js`

建議不要修改cq.social.scf客戶端庫，因為以後的升級可能會覆蓋任何編輯。

### 自定義示例：內聯連結 {#example-customization-inline-links}

出於安全考慮，預設情況下，超連結選項不包括在呈現給成員的富文本表徵圖集中。 在UGC中，當允許參照時，故障的發生能力很大。

要將超連結選項添加到工具欄：

* 添加名為「」的工具欄 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 選擇 **[!UICONTROL 全部保存]**

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
