---
title: SPA頁面元件
seo-title: SPA Page Component
description: 在SPA中，頁面元件不提供其子元件的HTML元素，而是將此元素委派至SPA架構。 本檔案說明如何讓SPA的頁面元件獨一無二。
seo-description: In an SPA the page component doesn't provide the HTML elements of its child components, but instead delegates this to the SPA framework. This document explains how this makes the page component of an SPA unique.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 17c198c744111753ffffcc0758f98859524c964e
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# SPA頁面元件{#spa-page-component}

在SPA中，頁面元件不提供其子元件的HTML元素，而是將此元素委派至SPA架構。 本檔案說明如何讓SPA的頁面元件獨一無二。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 簡介 {#introduction}

SPA的頁面元件不會透過JSP或HTL檔案和資源物件提供其子元件的HTML元素。 此操作已委派給SPA架構。 子元件的表示方式會以JSON資料結構（即模型）擷取。 接著會根據提供的JSON模型，將SPA元件新增至頁面。 因此，頁面元件初始主體組成與其預先呈現的HTML對應不同。

## 頁面模型管理 {#page-model-management}

頁面模型的解析度及管理已委派給提供 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 模組。 SPA必須與 `PageModelManager` 模組，當它初始化以擷取初始頁面模型並註冊模型更新時，大多會在作者透過頁面編輯器編輯頁面時產生。 此 `PageModelManager` 可由SPA專案以npm套件形式存取。 作為AEM和SPA的翻譯， `PageModelManager` 是伴隨SPA。

若要允許製作頁面，用戶端程式庫名為 `cq.authoring.pagemodel.messaging` 必須新增，才能提供SPA和頁面編輯器之間的通訊通道。 如果SPA頁面元件繼承自頁面wcm/核心元件，則有下列選項可讓 `cq.authoring.pagemodel.messaging` 客戶端庫類別可用：

* 如果模板是可編輯的，請將客戶端庫類別添加到頁面策略中。
* 使用 `customfooterlibs.html` 頁面元件。

別忘了限制 `cq.authoring.pagemodel.messaging` 類別來識別頁面編輯器的內容。

## 通信資料類型 {#communication-data-type}

通訊資料類型是使用在AEM Page元件內設定HTML元素， `data-cq-datatype` 屬性。 當通訊資料類型設為JSON時，GET要求會點擊元件的Sling模型端點。 在頁面編輯器中發生更新後，更新元件的JSON表示會傳送至頁面模型程式庫。 然後頁面模型程式庫會警告SPA有更新。

**SPA頁面元件 —`body.html`**

```
<div id="page"></div>
```

除了非是避免延遲DOM產生的良好作法，SPA架構還需要在內文結尾新增指令碼。

**SPA頁面元件 —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA內容的元資源屬性：

**SPA頁面元件 —`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>請求元件的「Sling模型」表示時，會靜態設定預設模型選取器。

## 中繼屬性 {#meta-properties}

* `cq:wcmmode`:編輯器的WCM模式（例如頁面、範本）
* `cq:pagemodel_root_url`:應用程式的根模型URL。 直接存取子頁面時非常重要，因為子頁面模型是應用程式根模型的片段。 此 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 然後系統地將應用程式初始模型重新組合為從其根入口點進入應用程式。

* `cq:pagemodel_router`:啟用或停用 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 的 `PageModelManager` 資料庫

* `cq:pagemodel_route_filters`:以逗號分隔的清單或規則運算式，以提供路由 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 必須忽略。

>[!CAUTION]
>
>本檔案僅將We.Retail Journal應用程式用於示範用途。 它不應用於任何項目工作。
>
>任何AEM專案皆應運用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，可支援使用React或Angular的SPA專案，並運用SPA SDK。AEM上的所有SPA專案都應以SPA Starter Kit的Maven原型為基礎。

## 頁面編輯器覆蓋同步 {#page-editor-overlay-synchronization}

覆蓋的同步由 `cq.authoring.page` 類別。

## Sling模型JSON匯出結構設定 {#sling-model-json-exported-structure-configuration}

啟用路由功能後，假設SPA的JSON匯出包含應用程式的不同路由，這要歸功於AEM導覽元件的JSON匯出。 AEM導覽元件的JSON輸出可透過下列兩個屬性，在SPA根頁面內容原則中設定：

* `structureDepth`:與導出的樹的深度相對應的數字
* `structurePatterns`:與要匯出的頁面對應之規則陣列的規則運算式

這可顯示在以下的SPA範例內容中： `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
