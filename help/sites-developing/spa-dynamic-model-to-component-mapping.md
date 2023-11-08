---
title: SPA的動態模型至元件對應
description: 瞭解在Adobe Experience Manager適用的JavaScript SPA SDK中元件對映的動態模型如何發生。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# SPA的動態模型至元件對應{#dynamic-model-to-component-mapping-for-spas}

本檔案說明適用於Adobe Experience Manager (AEM)的JavaScript SPA SDK中元件對映的動態模型如何發生。

>[!NOTE]
>
>對於需要以SPA框架為基礎的使用者端轉譯(例如React或Angular)專案，建議使用SPA編輯器解決方案。

## 元件對應模組 {#componentmapping-module}

此 `ComponentMapping` 模組會以NPM封裝的形式提供給前端專案。 它儲存前端元件，並提供單頁應用程式將前端元件對應到AEM資源型別的方法。 如此一來，在剖析應用程式的JSON模型時，就能啟用元件的動態解析。

模型中每個專案都包含 `:type` 公開AEM資源型別的欄位。 掛載時，前端元件可使用從基礎程式庫收到的模型片段來轉譯自身。

另請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 有關模型剖析和模型的前端元件存取的更多資訊。

另請參閱npm套件： [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驅動單頁應用程式 {#model-driven-single-page-application}

使用AEM適用的JavaScript SPA SDK的單頁應用程式是模型導向的：

1. 前端元件向 [元件對應存放區](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. 然後 [容器](/help/sites-developing/spa-blueprint.md#container)，一旦由提供模型 [模型提供者](/help/sites-developing/spa-blueprint.md#the-model-provider)，反複執行其模型內容( `:items`)。

1. 如果有頁面，其子項( `:children`)首先從取得元件類別 [元件對應](/help/sites-developing/spa-blueprint.md#componentmapping) 然後將其例項化。

## 應用程式初始化 {#app-initialization}

每個元件都可藉由以下功能擴展： [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). 因此，初始化會採用下列一般形式：

1. 每個模型提供者會自我初始化，並監聽對應到其內部元件的模型片段所做的變更。
1. 此 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 必須初始化，如以下所示 [初始化流程](/help/sites-developing/spa-blueprint.md).

1. 儲存後，頁面模型管理員會傳回應用程式的完整模型。
1. 然後，此模型傳遞至前端根 [容器](/help/sites-developing/spa-blueprint.md#container) 應用程式的元件。
1. 模型片段最後會傳播至每個個別的子元件。

![app_model_initialization](assets/app_model_initialization.png)
