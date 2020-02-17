---
title: Rich Text Editor Essentials
seo-title: Rich Text Editor Essentials
description: Rich Text Editor功能概觀
seo-description: Rich Text Editor功能概觀
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rich Text Editor Essentials {#rich-text-editor-essentials}

## 概覽 {#overview}

富格文本編輯器(RTE)提供了輸入帶有標注的文本的功能。

對於「社群」元件，雖然與作者環 [境中的Rich Text編輯器類似](../../help/sites-authoring/rich-text-editor.md)，但會影響在發佈環境中輸入的文字。

![chlimage_1-410](assets/chlimage_1-410.png)

## 啟用富格文字編輯器 {#enabling-rich-text-editor}

允許用戶生成內容(UGC)的社群元件可以啟用允許RTE。 RTE預設情況下可能啟用或不啟用 [](functions.md)，具體取決於元件是添加到頁面還是包含在函式中。

如果未啟用，只需進入作 [者編輯模式](sites-console.md#authoring-site-content)，選擇要編輯的元件，然後選中複選框 `Rich Text Editor` 即可。

RTE可用於以下Communities元件：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [評論](comments.md)
* [Filebrary](file-library.md)
* [論壇](forum.md)
* [傳送訊息](configure-messaging.md)
* [QnA](working-with-qna.md)
* [評論](reviews.md)

## 自訂 {#customization}

Rich Text Editor的實現基於 [CKEditor，因此可進行自定義](https://www.ckeditor.com/)。

Communities元件的當前配置位於中 `cq.social.  scf   clientlib`，位於

`/libs/clientlibs/social/commons/scf/ckrte.js`

不建議修改cq.social.scf clientlib，因為未來的升級可能會覆寫任何編輯。

### 自訂範例：內嵌連結 {#example-customization-inline-links}

由於安全性的考慮，在預設情況下，超連結選項不會包含在提供給成員的豐富文字圖示集中。 在UGC中允許href時，其惡意攻擊能力較強。

要將超連結選項添加到工具欄：

* 新增名為「 `links`」的工具列
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 選擇「 **[!UICONTROL 全部保存」]**

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

