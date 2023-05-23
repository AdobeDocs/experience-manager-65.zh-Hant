---
title: 延伸 ContextHub
seo-title: Extending ContextHub
description: 當提供的儲存和模組不符合您的解決方案要求時，定義新類型的ContextHub儲存和模組
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

# 延伸 ContextHub{#extending-contexthub}

當提供的儲存和模組不符合您的解決方案要求時，定義新類型的ContextHub儲存和模組。

## 建立自定義儲存候選 {#creating-custom-store-candidates}

ContextHub儲存是從註冊的儲存候選建立的。 要建立自定義儲存，您需要建立和註冊儲存候選。

包含建立和註冊儲存候選的代碼的javascript檔案必須包含在 [客戶端庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders)。 資料夾的類別必須與以下模式匹配：

```xml
contexthub.store.[storeType]
```

的 `[storeType]` 類別的一部分是 `storeType` 註冊商店候選者。 (請參閱 [註冊ContextHub儲存候選](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate))。 例如，對於 `contexthub.mystore`，客戶端庫資料夾的類別必須是 `contexthub.store.contexthub.mystore`。

### 建立ContextHub儲存候選 {#creating-a-contexthub-store-candidate}

要建立商店候選，請使用 [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 函式以擴展一個基儲存：

* [「ContextHub.Store.PeristedStore」](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [「ContextHub.Store.SessionStore」](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PeristedJSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

請注意，每個基本儲存 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) 商店。

下面的示例建立 `ContextHub.Store.PersistedStore` 儲存候選：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的定製商店候選者將定義附加功能或覆蓋商店的初始配置。 幾個 [樣品庫候選](/help/sites-developing/ch-samplestores.md) 安裝在下面的儲存庫中 `/libs/granite/contexthub/components/stores`。 要從這些示例中學習，請使用CRXDE Lite開啟javascript檔案。

### 註冊ContextHub儲存候選 {#registering-a-contexthub-store-candidate}

註冊儲存候選，將其與ContextHub框架整合，並允許從該框架建立儲存。 要註冊商店候選，請使用 [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 函式 `ContextHub.Utils.storeCandidates` 類。

註冊商店候選時，將提供商店類型的名稱。 從候選建立儲存庫時，使用儲存庫類型標識其所基於的候選。

註冊商店候選時，請指明其優先順序。 當使用與已註冊的儲存候選者相同的儲存類型註冊儲存候選者時，使用具有較高優先順序的候選者。 因此，您可以用新實現覆蓋現有儲存候選。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多數情況下，只需要一個候選人，並且可以將優先順序設定為 `0`，但如果你有興趣，你可以瞭解 [更高級的註冊，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 允許根據javascript條件選擇少數儲存實現之一(`applies`)和候選優先順序。

## 建立ContextHub UI模組類型 {#creating-contexthub-ui-module-types}

當以下模組類型為 [隨ContextHub一起安裝](/help/sites-developing/ch-samplemodules.md) 不符合你的要求。 要建立UI模組類型，請通過擴展 `ContextHub.UI.BaseModuleRenderer` 類，然後註冊到 `ContextHub.UI`。

要建立UI模組呈現器，請建立 `Class` 包含呈現UI模組的邏輯的對象。 至少，您的類必須執行以下操作：

* 擴展 `ContextHub.UI.BaseModuleRenderer` 類。 此類是所有UI模組呈現器的基本實現。 的 `Class` 對象定義名為 `extend` 將此類命名為正在擴展的類。

* 提供預設配置。 建立 `defaultConfig` 屬性。 此屬性是一個對象，包含為 [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模組和您需要的任何其他屬性。

源 `ContextHub.UI.BaseModuleRenderer` 位於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  要註冊呈現器，請使用 [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 方法 `ContextHub.UI` 類。 需要提供模組類型的名稱。 管理員基於此呈現器建立UI模組時，會指定此名稱。

在自執行匿名函式中建立並註冊呈現器類。 以下示例基於contexthub.browserinfo UI模組的原始碼。 此UI模組是 `ContextHub.UI.BaseModuleRenderer` 類。

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

包含建立和註冊呈現器的代碼的javascript檔案必須包含在 [客戶端庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders)。 資料夾的類別必須與以下模式匹配：

```xml
contexthub.module.[moduleType]
```

的 `[moduleType]` 類別的一部分是 `moduleType` 已註冊模組呈現器。 例如， `moduleType` 共 `contexthub.browserinfo`，客戶端庫資料夾的類別必須是 `contexthub.module.contexthub.browserinfo`。
