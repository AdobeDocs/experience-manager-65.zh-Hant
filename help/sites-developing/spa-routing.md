---
title: 模SPA型路由
seo-title: SPA Model Routing
description: 對於中的單頁應AEM用程式，應用程式負責路由。 本文檔介紹了可用的傳送機制、合同和選項。
seo-description: For single page applications in AEM, the app is responsible for the routing. This document describes the routing mechanism, the contract, and options available.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: 509ea0945e6c80e50f6f5bffd4c68282d586504a
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 模SPA型路由{#spa-model-routing}

對於中的單頁應AEM用程式，應用程式負責路由。 本文檔介紹了可用的傳送機制、合同和選項。

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## 項目路由 {#project-routing}

App擁有路由，然後由項目前端開發人員實施。 本文檔介紹特定於伺服器返回的模型的路AEM由。 頁面模型資料結構公開了基礎資源的URL。 前端項目可以使用任何提供路由功能的定製或第三方庫。 一旦路由需要模型的片段，則調用 `PageModelManager.getData()` 函式。 當模型路由已更改時，必須觸發事件以警告偵聽庫，如「頁面編輯器」。

## 架構 {#architecture}

有關詳細說明，請參閱 [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 的上界SPA。

## 模型路由器 {#modelrouter}

的 `ModelRouter`  — 啟用時 — 封裝HTML5歷史記錄API函式 `pushState` 和 `replaceState` 以保證模型的給定片段被預取並可訪問。 然後，它通知註冊的前端元件模型已被修改。

## 手動與自動模型路由 {#manual-vs-automatic-model-routing}

的 `ModelRouter` 自動提取模型的片段。 但是，像任何自動化工具一樣，它都有局限性。 當需要時 `ModelRouter` 可以禁用或配置為使用元屬性忽略路徑(請參閱 [頁SPA面元件](/help/sites-developing/spa-page-component.md) )。 然後，前端開發人員可以通過請求 `PageModelManager` 使用 `getData()` 的子菜單。

>[!NOTE]
>
>的 [We.零售日誌](https://github.com/adobe/aem-sample-we-retail-journal) 示例React項目演示了自動化方法，而Angular項目演示了手動方法。 半自動化方法也是有效的使用案例。

>[!CAUTION]
>
>當前版本的 `ModelRouter` 僅支援使用指向Sling Model入口點的實際資源路徑的URL。 它不支援使用虛榮URL或別名。

## 傳送合同 {#routing-contract}

當前實現基於以下假設：項SPA目使用HTML5歷史記錄API路由到不同的應用程式頁。

### 設定 {#configuration}

的 `ModelRouter` 支援模型路由的概念 `pushState` 和 `replaceState` 調用預取模型片段。 在內部，它觸發 `PageModelManager` 載入與給定URL對應的模型並觸發 `cq-pagemodel-route-changed` 其他模組可以監聽的事件。

預設情況下，此行為將自動啟用。 要禁用它，SPA應呈現以下元屬性：

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

請注意，每條路SPA由都應與中的可訪問資AEM源對應(例如， `/content/mysite/mypage"`) `PageModelManager` 將在選擇路由後自動嘗試載入相應的頁面模型。 但是，如果需要，SPA還可以定義路由的「阻止清單」，這些路由應被 `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
