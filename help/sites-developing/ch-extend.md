---
title: 延伸 ContextHub
description: 當提供的ContextHub存放區和模組不符合您的解決方案需求時，定義這些新的型別
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# 延伸 ContextHub{#extending-contexthub}

當提供的ContextHub存放區和模組不符合您的解決方案需求時，請定義這些新型別。

## 建立自訂商店候選者 {#creating-custom-store-candidates}

ContextHub存放區是從已登入的存放區候選專案建立的。 若要建立自訂商店，請建立並註冊商店候選商店。

包含建立及登入存放區候選程式碼的JavaScript檔案必須包含在[使用者端程式庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 資料夾的類別必須符合以下模式：

```xml
contexthub.store.[storeType]
```

類別的`[storeType]`部分為登入商店候選者的`storeType`。 （請參閱[註冊ContextHub存放區候選專案](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)）。 例如，對於`contexthub.mystore`的storeType，使用者端程式庫資料夾的類別必須是`contexthub.store.contexthub.mystore`。

### 建立ContextHub存放區候選專案 {#creating-a-contexthub-store-candidate}

若要建立候選商店，請使用[`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent)函式來擴充其中一個基本商店：

* [&#39;ContextHub.Store.PersistedStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersistedJSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

每個基底存放區都會擴充[`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core)存放區。

下列範例會建立`ContextHub.Store.PersistedStore`存放區候選的最簡單延伸模組：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂商店候選者會定義其他功能或覆寫商店的初始設定。 有數個[範例商店候選者](/help/sites-developing/ch-samplestores.md)安裝在`/libs/granite/contexthub/components/stores`下的存放庫中。 若要瞭解這些範例的內容，請使用CRXDE Lite開啟JavaScript檔案。

### 註冊ContextHub存放區候選專案 {#registering-a-contexthub-store-candidate}

註冊存放區候選項，以將其與ContextHub架構整合，並啟用從中建立存放區的功能。 若要登入存放區候選專案，請使用`ContextHub.Utils.storeCandidates`類別的[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)函式。

註冊候選商店時，需提供該商店型別的名稱。 從候選者建立存放區時，您可以使用存放區型別來識別它所依據的候選者。

當您註冊候選商店時，請指出其優先順序。 當使用與已登入的候選商店相同的候選商店型別登入候選商店時，會使用具有較高優先順序的候選商店。 因此，您可以使用新的實作來覆寫現有的商店候選者。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

通常只需要一個候選者，而且優先順序可以設定為`0`。 但如果您有興趣，您可以瞭解更多[進階註冊，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)，這允許根據JavaScript條件(`applies`)和候選優先順序選擇少數商店實作之一。

## 建立ContextHub UI模組型別 {#creating-contexthub-ui-module-types}

當與ContextHub](/help/sites-developing/ch-samplemodules.md)一起安裝的[模組不符合您的需求時，請建立自訂UI模組型別。 若要建立UI模組型別，請擴充`ContextHub.UI.BaseModuleRenderer`類別，然後向`ContextHub.UI`註冊，以建立UI模組轉譯器。

若要建立UI模組轉譯器，請建立包含轉譯UI模組的邏輯的`Class`物件。 您的類別至少必須執行下列動作：

* 擴充`ContextHub.UI.BaseModuleRenderer`類別。 此類別是所有UI模組轉譯器的基本實施。 `Class`物件定義名為`extend`的屬性，您可用來將此類別命名為要擴充的類別。

* 提供預設設定。 建立`defaultConfig`屬性。 此屬性是物件，其中包含為[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模組定義的屬性，以及您需要的任何其他屬性。

`ContextHub.UI.BaseModuleRenderer`的來源位於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。 若要註冊轉譯器，請使用`ContextHub.UI`類別的[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)方法。 提供模組型別的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自動執行的匿名函式中建立並註冊轉譯器類別。 以下範例是根據contexthub.browserinfo UI模組的原始程式碼。 此UI模組是`ContextHub.UI.BaseModuleRenderer`類別的簡單擴充。

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

包含建立及註冊轉譯器之程式碼的JavaScript檔案必須包含在[使用者端程式庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 資料夾的類別必須符合以下模式：

```xml
contexthub.module.[moduleType]
```

類別的`[moduleType]`部分是模組轉譯器登入的`moduleType`。 例如，對於`contexthub.browserinfo`的`moduleType`，使用者端資料庫資料夾的類別必須是`contexthub.module.contexthub.browserinfo`。
