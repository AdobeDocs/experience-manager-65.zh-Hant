---
title: SPA模型路由
seo-title: SPA模型路由
description: 對於AEM中的單頁應用程式，應用程式負責路由。 本文檔介紹了路由機制、合同和可用選項。
seo-description: 對於AEM中的單頁應用程式，應用程式負責路由。 本文檔介紹了路由機制、合同和可用選項。
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# SPA模型路由{#spa-model-routing}

對於AEM中的單頁應用程式，應用程式負責路由。 本文檔介紹了路由機制、合同和可用選項。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 項目路由{#project-routing}

應用程式擁有路由，然後由項目前端開發人員實施。 本檔案說明AEM伺服器傳回之模型的特定路由。 頁面模型資料結構會公開基礎資源的URL。 前端專案可使用任何提供路由功能的自訂或協力廠商程式庫。 一旦路由需要模型的片段，就可以調用`PageModelManager.getData()`函式。 當模型路由變更時，必須觸發事件，以警告監聽程式庫，例如頁面編輯器。

## 架構 {#architecture}

如需詳細說明，請參閱SPA Blueprint檔案的[PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)區段。

## ModelRouter {#modelrouter}

`ModelRouter` — 當啟用時 — 封裝HTML5歷史API函式`pushState`和`replaceState`，以確保預先擷取並存取指定的模型片段。 然後，它通知已註冊的前端元件，模型已被修改。

## 手動與自動模型路由{#manual-vs-automatic-model-routing}

`ModelRouter`會自動擷取模型片段。 但是，如同任何自動化工具一樣，它有其局限性。 需要時，可禁用`ModelRouter`或將配置為使用元屬性忽略路徑(請參閱[SPA頁面元件](/help/sites-developing/spa-page-component.md)文檔的元屬性部分)。 然後，前端開發人員可通過請求`PageModelManager`使用`getData()`函式載入任何給定的模型片段來實現自己的模型路由層。

>[!NOTE]
>
>目前，We.Retail Journal範例React專案說明自動化方法，而Angular專案則說明手動方法。 半自動方法也是有效的使用案例。

>[!CAUTION]
>
>`ModelRouter`的目前版本僅支援使用URL，指向Sling Model登入點的實際資源路徑。 不支援使用虛名URL或別名。

## 傳送合同{#routing-contract}

目前的實作以SPA專案使用HTML5歷史記錄API來路由至不同應用程式頁面的假設為基礎。

### 設定 {#configuration}

`ModelRouter`支援模型路由的概念，因為它監聽`pushState`和`replaceState`呼叫以預先擷取模型片段。 在內部，它會觸發`PageModelManager`以載入與指定URL對應的模型，並引發其他模組可監聽的`cq-pagemodel-route-changed`事件。

依預設，會自動啟用此行為。 若要停用，SPA應呈現下列中繼屬性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

請注意，SPA的每條路由都應對應至AEM中的可存取資源（例如&quot; `/content/mysite/mypage"`），因為一旦選取路由，`PageModelManager`會自動嘗試載入對應的頁面模型。 不過，如有需要，SPA也可以定義應由`PageModelManager`忽略的路由的「塊清單」：

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
