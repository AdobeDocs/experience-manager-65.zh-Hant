---
title: SPA頁面元件
seo-title: SPA頁面元件
description: 在SPA中，頁面元件不提供其子元件的HTML元素，而是將其委派到SPA架構。 本檔案說明如何讓SPA的頁面元件變得獨特。
seo-description: 在SPA中，頁面元件不提供其子元件的HTML元素，而是將其委派到SPA架構。 本檔案說明如何讓SPA的頁面元件變得獨特。
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA頁面元件{#spa-page-component}

在SPA中，頁面元件不提供其子元件的HTML元素，而是將其委派到SPA架構。 本檔案說明如何讓SPA的頁面元件變得獨特。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 簡介 {#introduction}

SPA的頁面元件不會透過JSP或HTL檔案與資源物件提供其子元件的HTML元素。 此操作委託給SPA框架。 子元件的表示方式會擷取為JSON資料結構（即模型）。 然後，SPA元件會根據提供的JSON模型新增至頁面。 因此，頁面元件初始內文構圖與預先轉譯的HTML對應內容不同。

## 頁面模型管理 {#page-model-management}

將頁面模型的解析度和管理委託給提供的模 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 塊。 SPA在初始化時必須與模 `PageModelManager` 塊進行交互，以提取初始頁面模型並註冊模型更新——大部分是在作者通過頁面編輯器編輯頁面時生成的。 SPA `PageModelManager` 項目可作為npm包訪問。 身為AEM和SPA之間的解譯員， `PageModelManager` 本來是SPA的伴侶。

若要允許編寫頁面，必須新增名為的用戶 `cq.authoring.pagemodel.messaging` 端程式庫，以提供SPA與頁面編輯器之間的通訊管道。 如果SPA頁元件繼承自頁wcm/core元件，則有以下選項可使客戶端庫 `cq.authoring.pagemodel.messaging` 類別可用：

* 如果範本是可編輯的，請將用戶端程式庫類別新增至頁面原則。
* 使用頁面元件新增用戶 `customfooterlibs.html` 端程式庫類別。

別忘了將類別包含限制 `cq.authoring.pagemodel.messaging` 在頁面編輯器的上下文中。

## 通信資料類型 {#communication-data-type}

通訊資料類型是使用屬性在AEM page元件內設定HTML元 `data-cq-datatype` 素。 當通訊資料類型設為JSON時，GET請求會點擊元件的Sling Model端點。 在頁面編輯器中發生更新後，更新元件的JSON表示法會傳送至頁面模型程式庫。 然後頁面模型庫會警告SPA更新。

**SPA頁面元件-`body.html`**

```
<div id="page"></div>
```

除了不延遲DOM生成的良好做法外，SPA框架還要求在主體末尾添加指令碼。

**SPA頁面元件-`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA內容的元資源屬性：

**SPA頁面元件-`customheaderlibs.html`**

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
>在請求元件的Sling Model表示時，預設模型選取器會靜態設定。

## 中繼屬性 {#meta-properties}

* `cq:wcmmode`:編輯器的WCM模式（例如頁面、範本）
* `cq:pagemodel_root_url`:應用程式的根模型URL。 直接存取子頁面時很重要，因為子頁面模型是應用程式根模型的片段。 然後 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 系統地將應用程式初始模型從其根入口點重新合成為進入應用程式。

* `cq:pagemodel_router`:啟用或停用程 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 式庫 `PageModelManager` 的

* `cq:pagemodel_route_filters`:以逗號分隔的清單或規則表達式，以提供必須忽 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 略的路由。

## 頁面編輯器覆蓋同步 {#page-editor-overlay-synchronization}

覆蓋的同步性由類別提供的完全相同的變異觀測器 `cq.authoring.page` 保證。

## Sling Model JSON匯出結構設定 {#sling-model-json-exported-structure-configuration}

啟用路由功能時，假設SPA的JSON匯出包含應用程式的不同路由，這要歸功於AEM導覽元件的JSON匯出。 AEM導覽元件的JSON輸出可透過下列兩個屬性，在SPA的根頁面內容原則中設定：

* `structureDepth`:與導出的樹的深度對應的編號
* `structurePatterns`:與要導出的頁對應的regex的陣列的regex

這可以在中的SPA示例內容中顯示 `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`。
