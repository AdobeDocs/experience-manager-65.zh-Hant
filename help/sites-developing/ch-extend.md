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
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 擴充ContextHub{#extending-contexthub}

定義新類型的ContextHub儲存空間和模組，但提供的儲存空間和模組不符合您的解決方案需求。

## 建立自訂商店候選項{#creating-custom-store-candidates}

ContextHub儲存區是從註冊的儲存區候選來建立。 若要建立自訂商店，您必須建立並註冊商店申請人。

包含建立和註冊儲存候選項的代碼的javascript檔案必須包含在[客戶端庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 資料夾的類別必須符合下列模式：

```xml
contexthub.store.[storeType]
```

類別的`[storeType]`部分是註冊商店候選的`storeType`。 （請參閱[註冊ContextHub Store Candidate](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)）。 例如，對於`contexthub.mystore`的storeType，用戶端程式庫資料夾的類別必須為`contexthub.store.contexthub.mystore`。

### 建立ContextHub儲存候選項{#creating-a-contexthub-store-candidate}

要建立儲存候選項，請使用[`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent)函式擴展一個基本儲存：

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

請注意，每個基本儲存都擴展了[`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core)儲存。

下面的示例建立`ContextHub.Store.PersistedStore`儲存候選項的最簡單擴展：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂商店申請人將會定義其他函式或覆寫商店的初始設定。 在`/libs/granite/contexthub/components/stores`下的儲存庫中安裝了幾個[樣例儲存候選項](/help/sites-developing/ch-samplestores.md)。 若要從這些範例中學習，請使用CRXDE Lite來開啟javascript檔案。

### 註冊ContextHub儲存候選項{#registering-a-contexthub-store-candidate}

註冊商店候選者，將其與ContextHub架構整合，並讓商店從中建立。 要註冊儲存候選項，請使用`ContextHub.Utils.storeCandidates`類的[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)函式。

當您註冊商店候選者時，會提供商店類型的名稱。 從候選商建立商店時，您會使用商店類型來識別其所依據的候選商。

當您註冊商店候選人時，請指出其優先順序。 當使用與已註冊的儲存候選者相同的儲存類型註冊儲存候選者時，使用優先順序較高的候選者。 因此，您可以使用新實作來覆寫現有的商店申請人。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多數情況下，只需要一個候選項，且優先順序可設為`0`，但如果您有興趣，則可瞭解更多進階註冊，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)可讓您根據javascript條件(`applies`)和候選項優先順序來選擇少數商店實作之一。[

## 建立ContextHub UI模組類型{#creating-contexthub-ui-module-types}

當與ContextHub](/help/sites-developing/ch-samplemodules.md)一起安裝的[模組不符合您的需求時，建立自訂UI模組類型。 要建立UI模組類型，請通過擴展`ContextHub.UI.BaseModuleRenderer`類並向`ContextHub.UI`註冊來建立新的UI模組渲染器。

若要建立UI模組轉譯器，請建立包含轉譯UI模組邏輯的`Class`物件。 至少，您的類別必須執行下列動作：

* 擴充`ContextHub.UI.BaseModuleRenderer`類別。 此類別是所有UI模組轉譯器的基本實作。 `Class`對象定義名為`extend`的屬性，用於將此類命名為正在擴展的類。

* 提供預設設定。 建立`defaultConfig`屬性。 此屬性是一個對象，包含為[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模組定義的屬性以及您需要的任何其他屬性。

`ContextHub.UI.BaseModuleRenderer`的來源位於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  要註冊渲染器，請使用`ContextHub.UI`類的[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)方法。 您需要提供模組類型的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自行執行的匿名函式中建立並註冊渲染器類。 以下示例基於contexthub.browserinfo UI模組的原始碼。 此UI模組是`ContextHub.UI.BaseModuleRenderer`類的簡單擴展。

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

包含建立和註冊轉譯器的程式碼的javascript檔案必須包含在[用戶端程式庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 資料夾的類別必須符合下列模式：

```xml
contexthub.module.[moduleType]
```

類別的`[moduleType]`部分是用於註冊模組渲染器的`moduleType`。 例如，對於`contexthub.browserinfo`的`moduleType`，客戶機庫資料夾的類別必須是`contexthub.module.contexthub.browserinfo`。
