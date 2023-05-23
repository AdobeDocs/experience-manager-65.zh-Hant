---
title: 添加窗體線程表項的自定義操作
seo-title: Adding custom action on form lister items
description: 表單開發人員可以在表單門戶頁面上的表單清單中添加更多操作。 預設情況下，表單清單允許您訪問表單、填寫表單並提交它。
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing allows you to access the form, fill it, and submit it.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 添加窗體線程表項的自定義操作{#adding-custom-action-on-form-lister-items}

在AEM Forms，您可以建立一個門戶頁面，列出可用表單。 預設情況下，可以搜索和列出門戶頁面上的表單。 您可以開啟表單以填寫和提交資訊。 在門戶頁面上列出的表單的框外僅提供呈現操作。 要瞭解有關門戶頁面上可用操作的詳細資訊，請參閱 [建立表單門戶頁](../../forms/using/creating-form-portal-page.md)。

您可以向門戶頁面添加其他選項。 可通過自定義表單門戶模板來自定義這些選項或操作。

本文介紹如何建立按鈕以直接從表單門戶頁面發送表單連結。 此自定義要求更新Search &amp; Lister元件的模板。

下面提供了將操作添加到模板所需的代碼。 的 `onclick` 代碼段中的屬性包含通過電子郵件發送表單連結的指令碼。

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

可以在自定義模板中添加類似操作。 要定義JavaScript函式，請在頁面級指令碼上添加該函式，並將其與必需的HTML元素連結。 在上例中， `onclick` 表達式是連結函式。

在對模板進行編輯後，示例門戶頁面包含一個按鈕，用於通過電子郵件發送表單連結，如下所示。

![email](assets/email.png)
