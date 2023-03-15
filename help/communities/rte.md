---
title: RTF編輯器要點
seo-title: Rich Text Editor Essentials
description: RTF編輯器功能概觀
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

# RTF編輯器要點 {#rich-text-editor-essentials}

## 概觀 {#overview}

RTF編輯器(RTE)提供使用標籤輸入文本的功能。

對於Communities元件，與 [製作環境中的RTF編輯器](../../help/sites-authoring/rich-text-editor.md)，則會影響在發佈環境中輸入的文字。

![RTF編輯器](assets/rich-text-editor.png)

## 啟用RTF編輯器 {#enabling-rich-text-editor}

允許使用者產生內容(UGC)的社群元件可啟用以允許RTE。 視元件已新增至頁面或包含在 [函式](functions.md),RTE預設為啟用或不啟用。

如果未啟用，只需輸入 [作者編輯模式](sites-console.md#authoring-site-content)，選取要編輯的元件，然後選取 `Rich Text Editor` 核取方塊。

RTE適用於下列Communities元件：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [評論](comments.md)
* [菲萊布里](file-library.md)
* [論壇](forum.md)
* [傳送訊息](configure-messaging.md)
* [QnA](working-with-qna.md)
* [評論](reviews.md)

## 自訂 {#customization}

RTF編輯器可自訂，因為實作是根據 [CKEditor](https://www.ckeditor.com/).

Communities元件的目前設定位於 `cq.social.  scf   clientlib`，位於

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建議修改cq.social.scf clientlib，因為日後的升級可能會覆寫任何編輯。

### 自訂範例：內嵌連結 {#example-customization-inline-links}

基於安全性考慮，預設情況下，向成員呈現的富文本表徵圖集中不包含超連結選項。 在UGC中允許href時，其雜訊能力較強。

要將超連結選項添加到工具欄，請執行以下操作：

* 添加名為「 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 選擇 **[!UICONTROL 全部儲存]**

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
