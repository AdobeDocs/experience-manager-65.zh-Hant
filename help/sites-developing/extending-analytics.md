---
title: 擴展事件跟蹤
seo-title: Extending Event Tracking
description: 分AEM析允許您跟蹤網站上的用戶交互
seo-description: AEM Analytics allows you to track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 擴展事件跟蹤{#extending-event-tracking}

分AEM析允許您跟蹤網站上的用戶交互。 作為開發人員，您可能需要：

* 跟蹤訪問者與元件交互的方式。 這可以通過 [自定義事件。](#custom-events)
* [ContextHub中的訪問值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [添加記錄回調](#adding-record-callbacks)。

>[!NOTE]
>
>這些資訊基本上是通用的，但是它使用 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 的上界。
>
>有關開發元件和對話框的一般資訊，請參見 [開發元件](/help/sites-developing/components.md)。

## 自定義事件 {#custom-events}

自定義事件跟蹤任何依賴於頁面上特定元件可用性的內容。 這還包括特定於模板的事件，因為頁面元件被視為另一個元件。

### 跟蹤頁面載入上的自定義事件 {#tracking-custom-events-on-page-load}

可以使用偽屬性 `data-tracking` （為了向後相容，仍支援較舊的記錄屬性）。 您可以將此項添加到任何HTML標籤。

的語法 `data-tracking` 是

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

可以傳遞任意數量的鍵值對作為第二個參數（稱為負載）。

示例可能如下所示：

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

在頁面載入時，全部 `data-tracking` 屬性將被收集並添加到ContextHub的事件儲存中，在該儲存中，屬性可以映射到Adobe Analytics事件。 未映射的事件不會被Adobe Analytics跟蹤。 請參閱 [連接到Adobe Analytics](/help/sites-administering/adobeanalytics.md) 的子菜單。

### 載入頁後跟蹤自定義事件 {#tracking-custom-events-after-page-load}

要跟蹤載入頁面後發生的事件（如用戶交互），請使用 `CQ_Analytics.record` JavaScript函式：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

位置

* `events` 是字串或字串陣列（對於多個事件）。

* `values` 包含要跟蹤的所有值
* `collect` 是可選的，並將返回包含事件和資料對象的陣列。
* `options` 是可選的，包含連結跟蹤選項，如HTML元素 `obj` 和 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`。

* `componentPath` 是必需的屬性，建議將其設定為 `<%=resource.getResourceType()%>`

例如，使用以下定義，用戶按一下 **跳到頂** 連結將導致兩個事件， `jumptop` 和 `headlineclick`，將被激發：

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 訪問ContextHub中的值 {#accessing-values-in-the-contexthub}

ContextHub JavaScript API具有 `getStore(name)` 函式（如果可用）。 商店有 `getItem(key)` 函式（如果可用）。 使用 `getKeys()` 函式可檢索特定儲存的已定義鍵的陣列。

通過使用 `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 的子菜單。

通知ContextHub初始可用性的最佳方法是使用 `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 的子菜單。

**ContextHub的其他事件：**

所有商店都已就緒：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

儲存特定：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另請參閱 [ContextHub API參考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 添加記錄回調 {#adding-record-callbacks}

使用函式註冊回調前後 `CQ_Analytics.registerBeforeCallback(callback,rank)` 和 `CQ_Analytics.registerAfterCallback(callback,rank)`。

這兩個函式都將函式作為第一個參數，將秩作為第二個參數，這表示回調的執行順序。

如果回調返回false，則不執行執行鏈中後續的回調。
