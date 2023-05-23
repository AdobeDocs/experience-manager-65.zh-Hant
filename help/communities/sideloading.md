---
title: 元件旁載入
seo-title: Component Sideloading
description: 當將網頁設計為簡單、單頁的應用時，社區元件旁載入非常有用，該應用根據站點訪問者選擇的內容動態更改顯示的內容
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

# 元件旁載入 {#component-sideloading}

## 概觀 {#overview}

當將網頁設計為簡單的單頁應用時，社區元件旁載入非常有用，該應用會根據站點訪問者選擇的內容動態更改顯示的內容。

如果頁面模板中不存在社區元件，而是在站點訪問者選擇後動態添加社區元件，則會完成此操作。

由於社交元件框架(SCF)具有輕量級的存在，因此只註冊在初始頁載入時存在的SCF元件。 要在頁面載入後註冊動態添加的SCF元件，必須調用SCF以「側載」該元件。

當設計頁面以旁載入社區元件時，可以快取整個頁面。

動態添加SCF元件的步驟如下：

1. [將元件添加到DOM](#dynamically-add-component-to-dom)

1. [側載元件](#sideload-by-invoking-scf) 使用兩種方法之一：

* [動態包含](#dynamic-inclusion)
   * 啟動所有動態添加的元件
* [動態載入](#dynamic-loading)
   * 按需添加一個特定元件

>[!NOTE]
>
>側裝 [非現有資源](scf.md#add-or-include-a-communities-component) 不支援。

## 將元件動態添加到DOM {#dynamically-add-component-to-dom}

無論元件是動態包含的還是動態載入的，都必須先將其添加到DOM中。

添加SCF元件時，最常使用的標籤是DIV標籤，但也可以使用其他標籤。 由於SCF僅在頁面初始載入時檢查DOM，因此在顯式調用SCF之前，對DOM的添加不會被注意。

無論使用什麼標籤，元素至少必須通過包含以下兩個屬性來符合正常的SCF根元素模式：

* **資料元件ID**

   添加的元件的有效路徑。

* **資料scf分量**

   元件的resourceType。

下面是添加的注釋元件的一個示例：

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## 通過調用SCF進行側載 {#sideload-by-invoking-scf}

### 動態包含 {#dynamic-inclusion}

動態包含使用引導請求，導致SCF檢查DOM並引導頁面上找到的所有SCF元件。

要在頁面載入後隨時初始化SCF元件，只需觸發JQuery事件，如下所示：

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動態載入 {#dynamic-loading}

動態載入提供了對載入SCF元件的控制。

不要引導在DOM中找到的所有SCF元件，而是可以指定特定的SCF元件來使用此JavaScript方法載入：

`SCF.addComponent(document.getElementById(*someId*));`

位置 `someId` 是 `data-component-id` 屬性。
