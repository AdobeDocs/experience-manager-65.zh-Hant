---
title: 元件側載
seo-title: Component Sideloading
description: 將網頁設計為簡單的單頁應用程式時，會根據網站訪客所選取的項目動態變更顯示內容，Communities元件會側載相當實用
seo-description: Communities component sideloading is useful when a web page is designed as a simple, single page app that dynamically alters what is displayed depending on what is selected by the site visitor
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 元件側載 {#component-sideloading}

## 總覽 {#overview}

將網頁設計為簡單的單頁應用程式時，會根據網站訪客所選取的項目動態變更顯示內容，Communities元件側載相當實用。

當頁面範本中不存在Communities元件，而是依網站訪客的選擇以動態方式新增時，就會完成此作業。

由於社交元件框架(SCF)具有輕量級存在，因此只註冊初始頁面載入時存在的SCF元件。 要在頁面載入後註冊動態添加的SCF元件，必須調用SCF以「側載」該元件。

設計用來側載Communities元件的頁面時，可以快取整個頁面。

動態添加SCF元件的步驟如下：

1. [將元件新增至DOM](#dynamically-add-component-to-dom)

1. [側載元件](#sideload-by-invoking-scf) 使用下列兩種方法之一：

* [動態包含](#dynamic-inclusion)
   * 引導所有動態添加的元件
* [動態載入](#dynamic-loading)
   * 按需添加一個特定元件

>[!NOTE]
>
>的側載 [非現有資源](scf.md#add-or-include-a-communities-component) 不支援。

## 動態新增元件至DOM {#dynamically-add-component-to-dom}

無論元件是動態包含或動態載入，必須先將其新增至DOM。

新增SCF元件時，最常使用的標籤是DIV標籤，但也可以使用其他標籤。 由於SCF只會在頁面最初載入時檢查DOM，因此在明確叫用SCF之前，DOM的這項新增內容不會被察覺。

無論使用什麼標籤，元素至少必須包含以下兩個屬性，以符合正常的SCF根元素模式：

* **data-component-id**

   新增元件的有效路徑。

* **data-scf-component**

   元件的resourceType。

以下是新增備注元件的範例：

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## 調用SCF進行側載 {#sideload-by-invoking-scf}

### 動態包含 {#dynamic-inclusion}

動態包含使用引導請求，導致SCF檢查DOM並引導頁面上找到的所有SCF元件。

若要在頁面載入後隨時初始化SCF元件，只需引發JQuery事件，如下所示：

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動態載入 {#dynamic-loading}

動態載入可以控制載入SCF元件。

可以指定特定的SCF元件來使用此JavaScript方法載入，而不是引導在DOM中找到的所有SCF元件：

`SCF.addComponent(document.getElementById(*someId*));`

其中 `someId` 是 `data-component-id` 屬性。
