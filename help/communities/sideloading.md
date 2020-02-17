---
title: 元件側載
seo-title: 元件側載
description: 當網頁設計為簡單的單一頁面應用程式時，社群元件側載會很有用，它會根據網站訪客選取的項目動態變更顯示的項目
seo-description: 當網頁設計為簡單的單一頁面應用程式時，社群元件側載會很有用，它會根據網站訪客選取的項目動態變更顯示的項目
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 元件側載 {#component-sideloading}

## 概覽 {#overview}

當網頁設計為簡單的單一頁面應用程式時，社群元件側載會很有用，它會根據網站訪客選取的項目動態變更顯示的項目。

當頁面範本中不存在社群元件，但會在網站訪客選取後動態新增時，就會完成此動作。

由於社交元件框架(SCF)具有輕量級存在，因此僅註冊初始頁面載入時存在的SCF元件。 對於動態添加的SCF元件，在頁面載入後要註冊，必須調用SCF以「側載」該元件。

當頁面設計為側載Communities元件時，可快取整個頁面。

動態添加SCF元件的步驟包括：

1. [將元件新增至DOM](#dynamically-add-component-to-dom)

1. [使用下列兩種方法](#sideload-by-invoking-scf) 之一側載元件：

* [動態包含](#dynamic-inclusion)
   * 引導所有動態添加的元件
* [動態載入](#dynamic-loading)
   * 隨選新增一個特定元件

>[!NOTE]
>
>不支援 [側載非現有資](scf.md#add-or-include-a-communities-component) 源。

## 動態新增元件至DOM {#dynamically-add-component-to-dom}

不論元件是動態包含或動態載入，都必須先將其新增至DOM。

添加SCF元件時，最常用的標籤是DIV標籤，但也可以使用其他標籤。 由於SCF僅在頁面初始載入時檢查DOM，因此在明確呼叫SCF之前，DOM的新增功能將不會引起注意。

無論使用什麼標籤，元素至少必須包含以下兩個屬性，以符合正常的SCF根元素模式：

* **data-component-id**&#x200B;新增元件的有效路徑

* **data-scf-component**&#x200B;元件的resourceType

以下是新增注釋元件的範例：

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

要在頁面載入後隨時初始化SCF元件，只需觸發JQuery事件，如下所示：

$(document)。trigger(SCF.events.BOOTSTRAP_REQUEST);

### 動態載入 {#dynamic-loading}

動態載入提供對載入SCF元件的控制。

與其引導DOM中找到的所有SCF元件，您可以使用以下JavaScript方法指定要載入的特定SCF元件：

SCF.addComponent(document.getElementById(*someId*));

其 *中* someId是 **data-component-id屬性的值** 。
