---
title: 擴充ContextHub
seo-title: Extending ContextHub
description: 當提供的儲存和模組不符合您的解決方案需求時，定義新類型的ContextHub儲存和模組
seo-description: Define new types of ContextHub stores and modules when the ones provided do not meet your solution requirements
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# 擴充ContextHub{#extending-contexthub}

當提供的儲存和模組不符合您的解決方案需求時，定義新類型的ContextHub儲存和模組。

## 建立自訂商店候選項 {#creating-custom-store-candidates}

ContextHub存放區是根據註冊存放區候選項目建立。 若要建立自訂商店，您需要建立並註冊商店候選商店。

包含建立和註冊儲存候選項的程式碼的javascript檔案必須包含在 [用戶庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders). 資料夾的類別必須符合下列模式：

```xml
contexthub.store.[storeType]
```

此 `[storeType]` 類別的一部分是 `storeType` 已註冊商店候選的商店。 (請參閱 [註冊ContextHub儲存候選項](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate))。 例如，對於 `contexthub.mystore`，用戶端程式庫資料夾的類別必須 `contexthub.store.contexthub.mystore`.

### 建立ContextHub存放區候選項 {#creating-a-contexthub-store-candidate}

若要建立商店候選項目，請使用 [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 函式，以擴展基儲存庫之一：

* [&#39;ContextHub.Store.PerisentStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PerisentJSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

請注意，每個基本存放區會將 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) 儲存。

下列範例會建立 `ContextHub.Store.PersistedStore` 儲存候選項：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂存放區候選項目將定義其他函式或覆寫存放區的初始設定。 數個 [樣本庫候選項](/help/sites-developing/ch-samplestores.md) 安裝在下方的存放庫中 `/libs/granite/contexthub/components/stores`. 若要從這些範例中學習，請使用CRXDE Lite來開啟javascript檔案。

### 註冊ContextHub儲存候選項 {#registering-a-contexthub-store-candidate}

註冊候選儲存庫以將其與ContextHub框架整合，並允許從中建立儲存庫。 要註冊商店候選商，請使用 [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 函式 `ContextHub.Utils.storeCandidates` 類別。

註冊商店候選項時，您會提供商店類型的名稱。 從候選項建立商店時，您可以使用商店類型來識別其所依據的候選項。

註冊商店候選商時，您會指出其優先順序。 當使用與已註冊的儲存候選相同的儲存類型來註冊儲存候選時，使用優先順序較高的候選。 因此，您可以使用新實施來覆寫現有的商店候選項目。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多數情況下，只需要一個候選者，而優先順序可設為 `0`，但如果您有興趣，可以了解 [更多高級註冊，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 允許根據javascript條件選擇少數的存放區實施(`applies`)和候選優先順序。

## 建立ContextHub UI模組類型 {#creating-contexthub-ui-module-types}

在 [隨ContextHub安裝](/help/sites-developing/ch-samplemodules.md) 不符合您的要求。 若要建立UI模組類型，請透過擴充 `ContextHub.UI.BaseModuleRenderer` 類別，然後註冊 `ContextHub.UI`.

若要建立UI模組轉譯器，請建立 `Class` 包含轉譯UI模組邏輯的物件。 至少，您的類必須執行以下操作：

* 擴充 `ContextHub.UI.BaseModuleRenderer` 類別。 此類別是所有UI模組轉譯器的基本實作。 此 `Class` 對象定義名為 `extend` 用於將此類命名為正在擴展的類。

* 提供預設設定。 建立 `defaultConfig` 屬性。 此屬性是物件，包含針對 [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模組，以及您需要的任何其他屬性。

的來源 `ContextHub.UI.BaseModuleRenderer` 位於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  若要註冊轉譯器，請使用 [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 方法 `ContextHub.UI` 類別。 您必須提供模組類型的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自行執行的匿名函式中建立並註冊渲染器類。 以下範例是以contexthub.browserinfo UI模組的原始碼為基礎。 此UI模組是 `ContextHub.UI.BaseModuleRenderer` 類別。

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

包含建立和註冊轉譯器的程式碼的javascript檔案必須包含在 [用戶庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders). 資料夾的類別必須符合下列模式：

```xml
contexthub.module.[moduleType]
```

此 `[moduleType]` 類別的一部分是 `moduleType` 已註冊模組轉譯器。 例如，對於 `moduleType` of `contexthub.browserinfo`，用戶端程式庫資料夾的類別必須 `contexthub.module.contexthub.browserinfo`.
