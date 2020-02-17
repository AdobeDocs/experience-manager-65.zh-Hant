---
title: 在表單清單項上添加自定義操作
seo-title: 在表單清單項上添加自定義操作
description: 表單開發人員可在表單入口網頁的表單清單中新增更多動作。 依預設，表單清單可讓您存取表單、填寫表單並送出。
seo-description: 表單開發人員可在表單入口網頁的表單清單中新增更多動作。 依預設，表單清單可讓您存取表單、填寫表單並送出。
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 在表單清單項上添加自定義操作{#adding-custom-action-on-form-lister-items}

在AEM Forms中，您可以建立列出可用表單的入口網頁。 依預設，您可以搜尋並列出入口網站頁面上的表單。 您可以開啟表單以填寫和提交資訊。 入口網站頁面上列出的表單，現在只提供轉譯動作。 若要進一步瞭解入口網站頁面上的可用動作，請參 [閱建立表單入口網站頁面](../../forms/using/creating-form-portal-page.md)。

您可以新增其他選項至入口網站頁面。 您可以自訂表單入口網站的範本，自訂這些選項或動作。

本文將展示如何建立按鈕，以直接從表單入口網頁傳送表單連結。 此自訂作業需要更新Search &amp; Lister元件的範本。

下面提供將動作新增至範本所需的程式碼。 程式 `onclick` 碼片段中的屬性具有指令碼，可透過電子郵件傳送表單連結。

```mxml
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

您可以在自訂範本中新增類似動作。 若要定義JavaScript函式，請在頁面層級指令碼上新增該函式，並將其連結至必要的HTML元素。 在上述範例中，運算式 `onclick` 是連結的函式。

對範本進行編輯後，範例入口網頁會包含一個按鈕，可透過電子郵件傳送表單的連結，如下所示。

![email](assets/email.png)

