---
title: SPA模型路由
seo-title: SPA模型路由
description: 對於AEM中的單頁應用程式，應用程式負責路由。 本文檔介紹路由選擇機制、合同和可用選項。
seo-description: 對於AEM中的單頁應用程式，應用程式負責路由。 本文檔介紹路由選擇機制、合同和可用選項。
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# SPA型號路由{#spa-model-routing}

對於AEM中的單頁應用程式，應用程式負責路由。 本文檔介紹路由選擇機制、合同和可用選項。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 項目路由{#project-routing}

應用程式擁有路由，然後由專案前端開發人員實作。 本檔案說明AEM伺服器傳回之模型專屬的路由。 頁面模型資料結構會公開基礎資源的URL。 前端項目可以使用任何提供路由功能的自定義或第三方庫。 一旦路由需要模型的片段，就可以調用`PageModelManager.getData()`函式。 當模型路由變更時，必須觸發事件以警告監聽程式庫，例如頁面編輯器。

## 架構 {#architecture}

有關詳細說明，請參閱SPA Blueprint文檔的[PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)部分。

## ModelRouter {#modelrouter}

`ModelRouter` —— 啟用時——封裝HTML5歷史API函式`pushState`和`replaceState`，以保證預取和存取給定的模型片段。 然後，它通知已註冊的前端元件模型已修改。

## 手動與自動模型路由{#manual-vs-automatic-model-routing}

`ModelRouter`會自動擷取模型片段。 但是，如同任何自動化工具一樣，它都有其局限性。 如果需要，可禁用`ModelRouter`或將&lt;a0/>配置為使用元屬性忽略路徑（請參閱[SPA頁元件](/help/sites-developing/spa-page-component.md)文檔的元屬性部分）。 然後，前端開發人員可以通過請求`PageModelManager`使用`getData()`函式載入任何給定的模型片段來實現自己的模型路由層。

>[!NOTE]
>
>目前，We.Retail Journal Sample React項目說明了自動化方法，而Angular項目說明了手動方法。 半自動化方法也是有效的使用案例。

>[!CAUTION]
>
>目前版本的`ModelRouter`僅支援使用指向Sling Model入口點實際資源路徑的URL。 它不支援使用虛名URL或別名。

## 傳送合同{#routing-contract}

目前的實作是以SPA專案使用HTML5歷史API來路由至不同應用程式頁面的假設為基礎。

### 設定 {#configuration}

`ModelRouter`支援模型路由的概念，因為它監聽`pushState`和`replaceState`對預回遷模型片段的調用。 在內部，它會觸發`PageModelManager`以載入對應於指定URL的模型，並觸發其他模組可監聽的`cq-pagemodel-route-changed`事件。

依預設，此行為會自動啟用。 若要停用它，SPA應呈現下列中繼屬性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

請注意，SPA的每條路由都應對應AEM中的可存取資源（例如&quot; `/content/mysite/mypage"`），因為`PageModelManager`會在選取路由後自動嘗試載入對應的頁面模型。 不過，如果需要，SPA也可以定義`PageModelManager`應忽略的路由的「塊清單」:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
