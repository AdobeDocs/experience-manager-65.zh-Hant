---
title: 元件側載
description: 當網頁設計成簡單的單頁應用程式時，Communities元件旁載會很有用，該應用程式會根據網站訪客的選取內容來動態地變更顯示內容
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 元件側載 {#component-sideloading}

## 概觀 {#overview}

當網頁設計成簡單的單頁應用程式時，Communities元件旁載會很有用，該應用程式會根據網站訪客的選取內容來動態地變更顯示內容。

當Communities元件不存在於頁面範本中，而是根據網站訪客的選擇以動態方式新增時，即可完成這項作業。

由於社交元件架構(SCF)具有輕量型存在，因此只會註冊初始頁面載入時存在的SCF元件。 若要在頁面載入後註冊動態新增的SCF元件，必須叫用SCF來「側載」元件。

當頁面設計為側載Communities元件時，可以快取整個頁面。

動態新增SCF元件的步驟如下：

1. [將元件新增至DOM](#dynamically-add-component-to-dom)

1. [使用下列兩種方法之一側載元件](#sideload-by-invoking-scf)：

* [動態包含](#dynamic-inclusion)
   * 啟動所有動態新增的元件
* [動態載入](#dynamic-loading)
   * 隨選新增一個特定元件

>[!NOTE]
>
>不支援[非現有資源](scf.md#add-or-include-a-communities-component)的旁載作業。

## 動態新增元件至DOM {#dynamically-add-component-to-dom}

無論元件是以動態方式包含或動態載入，必須先將其新增至DOM。

新增SCF元件時，最常使用的標籤是DIV標籤，但也可能使用其他標籤。 因為SCF只會在頁面初次載入時檢查DOM，所以在明確叫用SCF之前，不會注意到DOM的這項新增。

無論使用何種標籤，元素至少都必須包含這兩個屬性，以符合一般的SCF根元素模式：

* **資料元件識別碼**

  新增元件的有效路徑。

* **data-scf-component**

  元件的resourceType。

以下是新增的註釋元件範例：

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## 透過叫用SCF進行側載 {#sideload-by-invoking-scf}

### 動態包含 {#dynamic-inclusion}

動態包含使用啟動載入要求，導致SCF檢查DOM並啟動頁面上的所有SCF元件。

若要在頁面載入後隨時初始化SCF元件，只需引發JQuery事件，如下所示：

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動態載入 {#dynamic-loading}

動態載入可讓您控制載入SCF元件。

您可以使用此JavaScript方法指定要載入的特定SCF元件，而不需啟動載入在DOM中找到的所有SCF元件：

`SCF.addComponent(document.getElementById(*someId*));`

其中`someId`是`data-component-id`屬性的值。
