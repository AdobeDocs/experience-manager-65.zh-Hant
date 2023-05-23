---
title: 動態模型到元件的映SPA射
seo-title: Dynamic Model to Component Mapping for SPAs
description: 本文介紹在的Javascript SDK中如何進行動態模型到組SPA件的映AEM射。
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

# 動態模型到元件的映SPA射{#dynamic-model-to-component-mapping-for-spas}

本文檔介紹在的Javascript SDK中如何進行動態模型到組SPA件的映AEM射。

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## 元件映射模組 {#componentmapping-module}

的 `ComponentMapping` 模組作為NPM包提供到前端項目。 它儲存前端元件，並為單頁應用程式將前端元件映射到資源類型提供AEM了方法。 這樣，在分析應用程式的JSON模型時，就可以動態解析元件。

模型中存在的每個項都包含 `:type` 顯示資源類AEM型的欄位。 裝載後，前端元件可以使用它從基礎庫接收到的模型片段來呈現自己。

請參閱 [藍SPA圖](/help/sites-developing/spa-blueprint.md) 的子菜單。

另請參見npm包： [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動的單頁應用程式 {#model-driven-single-page-application}

使用Javascript SDKSPA的單頁應AEM用程式由模型驅動：

1. 前端元件自行註冊到 [元件映射儲存](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)。
1. 然後 [容器](/help/sites-developing/spa-blueprint.md#container)，一旦由 [模型提供程式](/help/sites-developing/spa-blueprint.md#the-model-provider)，對模型內容進行迭代( `:items`)。

1. 對於頁面，其子代( `:children`)首先從 [元件映射](/help/sites-developing/spa-blueprint.md#componentmapping) 然後實例化它。

## 應用程式初始化 {#app-initialization}

每個元件都使用 [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)。 因此，初始化採用以下一般形式：

1. 每個模型提供器都初始化自身並偵聽對與其內部元件對應的模型段所做的更改。
1. 的 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 必須初始化為由表示 [初始化流](/help/sites-developing/spa-blueprint.md)。

1. 一旦儲存，頁面模型管理器將返回應用的完整模型。
1. 然後，此模型將傳遞給前端根 [容器](/help/sites-developing/spa-blueprint.md#container) 元件。
1. 模型的各部分最終傳播到每個單獨的子元件。

![app_model_initialization](assets/app_model_initialization.png)
