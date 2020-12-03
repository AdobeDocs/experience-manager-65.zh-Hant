---
title: 擴充事件追蹤
seo-title: 擴充事件追蹤
description: AEM Analytics可讓您追蹤網站上的使用者互動
seo-description: AEM Analytics可讓您追蹤網站上的使用者互動
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# 擴充事件追蹤{#extending-event-tracking}

AEM Analytics可讓您追蹤網站上的使用者互動。 身為開發人員，您可能需要：

* 追蹤訪客與您的元件互動的方式。 這可以對[自訂事件執行。](#custom-events)
* [存取ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [添加記錄回呼](#adding-record-callbacks)。

>[!NOTE]
>
>這項資訊基本上是一般的，但是使用[Adobe Analytics](/help/sites-administering/adobeanalytics.md)做為特定範例。
>
>有關開發元件和對話框的一般資訊，請參見[開發元件](/help/sites-developing/components.md)。

## 自訂事件{#custom-events}

自訂事件會追蹤任何與頁面上特定元件可用性相關的項目。 這也包含範本特定的事件，因為page-component會被視為另一個元件。

### 追蹤頁面載入的自訂事件{#tracking-custom-events-on-page-load}

這可以使用偽屬性`data-tracking`（舊記錄屬性仍受支援，以提供回溯相容性）來完成。 您可以將它新增至任何HTML標籤。

`data-tracking`的語法為

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

您可以將任意數量的鍵值對作為第二個參數傳遞，即稱為有效負載。

例如：

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

在頁面載入時，所有`data-tracking`屬性都會收集並新增至ContextHub的事件儲存區，這些屬性可在其中對應至Adobe Analytics事件。 Adobe Analytics將不會追蹤未映射的事件。 如需對應事件的詳細資訊，請參閱[連線至Adobe Analytics](/help/sites-administering/adobeanalytics.md)。

### 頁面載入後追蹤自訂事件{#tracking-custom-events-after-page-load}

若要追蹤載入頁面後發生的事件（例如使用者互動），請使用`CQ_Analytics.record` JavaScript函式：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

位置

* `events` 是字串或字串陣列（針對多個事件）。

* `values` 包含所有要追蹤的值
* `collect` 為可選項，並將返回包含事件和資料對象的陣列。
* `options` 為選用項目，並包含HTML元素和等連結追蹤 `obj` 選項 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`。

* `componentPath` 是必要的屬性，建議將其設為  `<%=resource.getResourceType()%>`

例如，使用下列定義時，按一下&#x200B;**跳至top**&#x200B;連結的使用者會引發兩個事件： `jumptop`和`headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 訪問ContextHub {#accessing-values-in-the-contexthub}中的值

ContextHub JavaScript API具有`getStore(name)`函式，可傳回指定的商店（如果有的話）。 儲存具有`getItem(key)`函式，該函式返回指定密鑰的值（如果可用）。 使用`getKeys()`函式，可檢索特定儲存的已定義鍵陣列。

使用`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`函式綁定函式，可通知您儲存上的值更改。

要獲得ContextHub初始可用性通知的最佳方式是使用`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`函式。

**ContextHub的其他事件：**

所有商店都準備就緒：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

特定商店：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另請參閱完整的[ContextHub API參考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 添加記錄回呼{#adding-record-callbacks}

使用函式`CQ_Analytics.registerBeforeCallback(callback,rank)`和`CQ_Analytics.registerAfterCallback(callback,rank)`註冊回呼前後。

這兩個函式都將函式作為第一個引數，將排名作為第二個引數，這決定了回呼的執行順序。

如果您的回呼傳回false，將不會執行執行鏈中後續的回呼。
