---
title: SPA的動態模型與元件對應
seo-title: Dynamic Model to Component Mapping for SPAs
description: 本文說明Javascript SPA SDK for AEM中如何進行動態模型與元件的對應。
seo-description: This article describes how the dynamic model to component mapping occurs in the Javascript SPA SDK for AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# SPA的動態模型與元件對應{#dynamic-model-to-component-mapping-for-spas}

本檔案說明Javascript SPA SDK for AEM中如何進行動態模型與元件的對應。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 元件映射模組 {#componentmapping-module}

此 `ComponentMapping` 模組作為NPM包提供到前端項目。 它儲存前端元件，並為單頁應用程式將前端元件映射到AEM資源類型提供了一種方式。 這可在剖析應用程式的JSON模型時，啟用元件的動態解析。

模型中呈現的每個項目都包含 `:type` 公開AEM資源類型的欄位。 裝載時，前端元件可使用從基礎庫接收的模型片段來呈現自身。

請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 有關模型解析和對模型的前端元件訪問的詳細資訊的文檔。

另請參閱npm套件： [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型導向的單頁應用程式 {#model-driven-single-page-application}

運用Javascript SPA SDK for AEM的單頁應用程式是模型導向：

1. 前端元件自行註冊到 [元件映射儲存](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. 然後 [容器](/help/sites-developing/spa-blueprint.md#container)，一經由 [模型提供程式](/help/sites-developing/spa-blueprint.md#the-model-provider)，會反覆顯示其模型內容( `:items`)。

1. 若是頁面，其子項( `:children`)，會先從 [元件對應](/help/sites-developing/spa-blueprint.md#componentmapping) 然後將其實例化。

## 應用程式初始化 {#app-initialization}

每個元件都會透過 [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). 因此，初始化採用以下一般形式：

1. 每個模型提供程式都自行初始化，並監聽對與其內部元件對應的模型片段所做的更改。
1. 此 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 必須初始化為，如 [初始化流程](/help/sites-developing/spa-blueprint.md).

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型將傳遞到前端根 [容器](/help/sites-developing/spa-blueprint.md#container) 應用程式的元件。
1. 模型的片段最終傳播到每個單獨的子元件。

![app_model_initialization](assets/app_model_initialization.png)
