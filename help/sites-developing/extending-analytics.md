---
title: 擴充事件追蹤
description: AEM Analytics可讓您追蹤使用者在您網站上的互動
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 擴充事件追蹤{#extending-event-tracking}

AEM Analytics可讓您追蹤使用者在您網站上的互動。 作為開發人員，您可能需要：

* 追蹤訪客與您元件的互動情形。 這可以透過[自訂事件完成。](#custom-events)
* [存取ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [新增記錄回呼](#adding-record-callbacks)。

>[!NOTE]
>
>此資訊基本上是通用的，但特定範例會使用[Adobe Analytics](/help/sites-administering/adobeanalytics.md)。
>
>如需開發元件和對話方塊的一般資訊，請參閱[開發元件](/help/sites-developing/components.md)。

## 自訂事件 {#custom-events}

自訂事件會追蹤任何與頁面上特定元件可用性相關的專案。 這也包括範本專屬的事件，因為頁面元件會被視為另一個元件。

### 追蹤頁面載入上的自訂事件 {#tracking-custom-events-on-page-load}

您可以使用虛擬屬性`data-tracking`來完成（舊記錄屬性仍支援回溯相容性）。 您可以將它新增至任何HTML標籤。

`data-tracking`的語法為

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

您可以傳遞任何數量的機碼值組作為第二個引數，稱為裝載。

範例看起來可能像這樣：

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

在頁面載入時，將會收集所有`data-tracking`屬性並新增至ContextHub的事件存放區，以便將其對應至Adobe Analytics事件。 Adobe Analytics不會追蹤未對應的事件。 如需對應事件的詳細資訊，請參閱[連線到Adobe Analytics](/help/sites-administering/adobeanalytics.md)。

### 頁面載入後追蹤自訂事件 {#tracking-custom-events-after-page-load}

若要追蹤載入頁面後發生的事件（例如使用者互動），請使用`CQ_Analytics.record` JavaScript函式：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

位置

* `events`為字串或字串陣列（適用於多個事件）。

* `values`包含所有要追蹤的值
* `collect`是選擇性的，將傳回包含事件和資料物件的陣列。
* `options`是選用專案，並包含連結追蹤選項，例如HTML專案`obj`和` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`。

* `componentPath`是必要的屬性，建議將其設為`<%=resource.getResourceType()%>`

例如，使用下列定義，使用者按一下&#x200B;**跳至頂端**&#x200B;連結將會導致兩個事件`jumptop`和`headlineclick`被引發：

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 存取ContextHub中的值 {#accessing-values-in-the-contexthub}

ContextHub JavaScript API有一個`getStore(name)`函式可傳回指定的存放區（如果有的話）。 存放區具有`getItem(key)`函式，會傳回指定機碼的值（如果有的話）。 使用`getKeys()`函式可以擷取特定存放區已定義金鑰的陣列。

您可以使用`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`函式繫結函式，通知您儲存區上的值變更。

要收到有關ContextHub初始可用性的通知，最佳方式是使用`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`函式。

ContextHub的&#x200B;**其他事件：**

所有商店都準備就緒：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

特定商店：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另請參閱完整的[ContextHub API參考](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 新增記錄回呼 {#adding-record-callbacks}

使用函式`CQ_Analytics.registerBeforeCallback(callback,rank)`和`CQ_Analytics.registerAfterCallback(callback,rank)`登入回呼之前和之後。

這兩個函式都會將函式當作第一個引數，並將排名當作第二個引數，這會指定執行回呼的順序。

如果您的回呼傳回false，則執行鏈結中後續的回呼將不會執行。
