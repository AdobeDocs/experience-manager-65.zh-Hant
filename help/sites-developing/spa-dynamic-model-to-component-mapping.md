---
title: SPA的動態模型到元件映射
seo-title: SPA的動態模型到元件映射
description: 本文說明Javascript SPA SDK for AEM中如何產生動態模型至元件的對應。
seo-description: 本文說明Javascript SPA SDK for AEM中如何產生動態模型至元件的對應。
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA的動態模型到元件映射{#dynamic-model-to-component-mapping-for-spas}

本檔案說明Javascript SPA SDK for AEM中如何進行動態模型與元件對應。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 元件映射模組 {#componentmapping-module}

該 `ComponentMapping` 模組作為NPM包提供給前端項目。 它可儲存前端元件，並為「單頁應用程式」提供將前端元件對應至AEM資源類型的方式。 如此可在剖析應用程式的JSON模型時，啟用元件的動態解析度。

模型中的每個項目都包含一個 `:type` 欄位，可顯示AEM資源類型。 當裝載時，前端元件可以使用它從基礎庫接收到的模型片段進行自身渲染。

請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) （SPA藍圖）檔案，以取得模型剖析和前端元件存取模型的詳細資訊。

另請參閱npm套件： [https://www.npmjs.com/package/@adobe/cq-spa-component-mapping](https://www.npmjs.com/package/@adobe/cq-spa-component-mapping)

## 模型導向的單頁應用程式 {#model-driven-single-page-application}

「單頁應用程式」運用Javascript SPA SDK for AEM是模型導向：

1. 前端元件可自行註冊至元 [件對應商店](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)。
1. 然後， [Container](/help/sites-developing/spa-blueprint.md#container)( [Model Provider)在提供模型後](/help/sites-developing/spa-blueprint.md#the-model-provider)，會重複其模型內容( `:items`)。

1. 如果是頁面，其子項( `:children`)會先從「元件對應」取得元件類 [別](/help/sites-developing/spa-blueprint.md#componentmapping) ，然後執行個體化它。

## 應用程式初始化 {#app-initialization}

每個元件都會與的功能一起擴展 [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)。 因此，初始化採用以下一般形式：

1. 每個模型提供器都自行初始化，並偵聽對與其內部元件相對應的模型段所做的更改。
1. 必 [ 須以 `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 初始化流表示 [初始化](/help/sites-developing/spa-blueprint.md)。

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型會傳遞至應用程式的前 [端根](/help/sites-developing/spa-blueprint.md#container) Container元件。
1. 模型的段最終會傳播到每個單獨的子元件。

![app_model_initialization](assets/app_model_initialization.png)

