---
title: 擴充ContextHub
seo-title: 擴充ContextHub
description: 定義新類型的ContextHub儲存和模組（當提供的儲存和模組不符合您的解決方案要求時）
seo-description: 定義新類型的ContextHub儲存和模組（當提供的儲存和模組不符合您的解決方案要求時）
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 擴充ContextHub{#extending-contexthub}

定義新類型的ContextHub儲存空間和模組，但提供的儲存空間和模組不符合您的解決方案需求。

## 建立自訂商店候選者 {#creating-custom-store-candidates}

ContextHub儲存區是從註冊的儲存區候選來建立。 若要建立自訂商店，您必須建立並註冊商店申請人。

包含建立和註冊商店候選項之程式碼的javascript檔案必須包含在用戶端程 [式庫資料夾中](/help/sites-developing/clientlibs.md#creating-client-library-folders)。 資料夾的類別必須符合下列模式：

```xml
contexthub.store.[storeType]
```

類別 `[storeType]` 的一部分是storeType，商店候選者會用其註冊。 (請參 [閱註冊ContextHub商店候選項](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate))。 例如，對於storeType的 `contexthub.mystore`，客戶程式庫資料夾的類別必須 `contexthub.store.contexthub.mystore`。

### 建立ContextHub商店候選項 {#creating-a-contexthub-store-candidate}

要建立儲存候選項，請使用 [ 函式來擴 `ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 展一個基本儲存：

* ` [ContextHub.Store.PersistedStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)`
* ` [ContextHub.Store.SessionStore](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)`
* ` [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)`
* ` [ContextHub.Store.PersistedJSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)`

請注意，每個基本儲存都擴展了 ` [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core)` 儲存。

下面的示例建立儲存候選項的最簡 `ContextHub.Store.PersistedStore` 擴展：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂商店申請人將會定義其他函式或覆寫商店的初始設定。 在/ [libs/granite/contexthub/components/stores下的儲存庫中](/help/sites-developing/ch-samplestores.md) ，會安裝幾個樣例儲存候選。 若要從這些範例中學習，請使用CRXDE Lite來開啟javascript檔案。

### 註冊ContextHub商店候選項 {#registering-a-contexthub-store-candidate}

註冊商店候選者，將其與ContextHub架構整合，並讓商店從中建立。 要註冊儲存候選項，請使 [ 用類 `registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 的函 `ContextHub.Utils.storeCandidates` 數。

在註冊商店候選人時，您會提供商店類型的名稱。 從候選商建立商店時，您會使用商店類型來識別其所依據的候選商。

當您註冊商店候選人時，請指出其優先順序。 當使用與已註冊的儲存候選者相同的儲存類型註冊儲存候選者時，使用優先順序較高的候選者。 因此，您可以使用新實作來覆寫現有的商店申請人。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

## 建立ContextHub UI模組類型 {#creating-contexthub-ui-module-types}

當隨ContextHub安裝的UI模組類型不 [符合您的要求時](/help/sites-developing/ch-samplemodules.md) ，請建立自訂UI模組類型。 若要建立UI模組類型，請擴充類別，然後將其註冊，以建立 `ContextHub.UI.BaseModuleRenderer` 新的UI模組轉譯器 `ContextHub.UI`。

若要建立UI模組轉換器，請建立 `Class` 包含轉換UI模組邏輯的物件。 至少，您的類別必須執行下列動作：

* 擴充課 `ContextHub.UI.BaseModuleRenderer` 程。 此類別是所有UI模組轉譯器的基本實作。 對 `Class` 像定義一個名為的屬 `extend` 性，用於將此類命名為正在擴展的類。

* 提供預設設定。 建立屬 `defaultConfig` 性。 此屬性是一個對象，包括為 [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模組定義的屬性，以及您需要的任何其他屬性。

來源位 `ContextHub.UI.BaseModuleRenderer` 於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  要註冊渲染器，請使 ` [registerRenderer](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)` 用類的方 `ContextHub.UI` 法。 您需要提供模組類型的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自行執行的匿名函式中建立並註冊渲染器類。 以下示例基於contexthub.browserinfo UI模組的原始碼。 此UI模組是類別的簡單擴充 `ContextHub.UI.BaseModuleRenderer` 功能。

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

包含建立和註冊轉譯器的程式碼的javascript檔案必須包含在用戶端程 [式庫資料夾中](/help/sites-developing/clientlibs.md#creating-client-library-folders)。 資料夾的類別必須符合下列模式：

```xml
contexthub.module.[moduleType]
```

類 `[moduleType]` 別的一部分是模組 `moduleType` 渲染器註冊時使用的。 例如，對於 `moduleType` 的 `contexthub.browserinfo`，客戶端庫資料夾的類別必須為 `contexthub.module.contexthub.browserinfo`。
