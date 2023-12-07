---
title: SPA模型路由
description: 若為AEM中的單頁應用程式，則由應用程式負責路由。 本檔案說明路由機制、合約及可用的選項。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# SPA模型路由{#spa-model-routing}

若為AEM中的單頁應用程式，則由應用程式負責路由。 本檔案說明路由機制、合約及可用的選項。

>[!NOTE]
>
>對於需要以SPA框架為基礎的使用者端轉譯(例如React或Angular)專案，建議使用SPA編輯器解決方案。

## 專案路由 {#project-routing}

應用程式擁有路由，並由專案前端開發人員實作。 本檔案說明AEM伺服器傳回之模型的特定路由。 頁面模型資料結構會公開基礎資源的URL。 前端專案可以使用任何提供路由功能的自訂或第三方資料庫。 一旦路由預期到模型的片段，就會呼叫 `PageModelManager.getData()` 功能可以建立。 當模型路由已變更時，必須觸發事件，以警告聆聽程式庫，例如「頁面編輯器」。

## 架構 {#architecture}

如需詳細說明，請參閱 [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) SPA Blueprint檔案的部分。

## 模型路由器 {#modelrouter}

此 `ModelRouter`  — 啟用時 — 封裝HTML5 History API函式 `pushState` 和 `replaceState` 以確保可預先擷取及存取模型的指定片段。 然後通知註冊的前端元件模型已被修改。

## 手動與自動模型製程 {#manual-vs-automatic-model-routing}

此 `ModelRouter` 自動擷取模型的片段。 但就像任何自動化工具一樣，它也伴隨著限制。 需要時 `ModelRouter` 可停用或設定為使用中繼屬性略過路徑(請參閱 [SPA頁面元件](/help/sites-developing/spa-page-component.md) 檔案)。 前端開發人員可透過請求 `PageModelManager` 若要使用載入模型的任何給定片段 `getData()` 函式。

>[!NOTE]
>
>此 [We.Retail日誌](https://github.com/adobe/aem-sample-we-retail-journal) 範例React專案說明了自動化方法，而Angular專案說明了手動方法。 半自動化方法也是有效的使用案例。

>[!CAUTION]
>
>目前版本的 `ModelRouter` 僅支援使用指向Sling模型進入點的實際資源路徑的URL。 不支援使用虛名URL或別名。

## 路由合約 {#routing-contract}

目前實施是根據SPA專案使用HTML5 History API路由傳送到不同應用程式頁面的假設。

### 設定 {#configuration}

此 `ModelRouter` 支援模型路由的概念，因為它會偵聽 `pushState` 和 `replaceState` 對預先擷取模型片段的呼叫。 在內部，它會觸發 `PageModelManager` 載入與指定URL對應的模型，並觸發 `cq-pagemodel-route-changed` 其他模組可以監聽的事件。

依預設，此行為會自動啟用。 若要停用，SPA應呈現以下中繼屬性：

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

請注意，SPA的每個路由都應對應至AEM中可存取的資源(例如，&quot; `/content/mysite/mypage"`)，因為 `PageModelManager` 選取路由後，將自動嘗試載入對應的頁面模型。 不過，如有需要，SPA也可定義路由的「封鎖清單」，應由 `PageModelManager`：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
