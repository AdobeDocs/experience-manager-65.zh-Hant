---
title: 擴充事件追蹤
seo-title: 擴充事件追蹤
description: AEM Analytics可讓您追蹤使用者在您網站上的互動
seo-description: AEM Analytics可讓您追蹤使用者在您網站上的互動
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 擴展事件跟蹤{#extending-event-tracking}

AEM Analytics可讓您追蹤使用者在您網站上的互動。 身為開發人員，您可能需要：

* 追蹤訪客與元件的互動方式。 這可以用[自訂事件來完成。](#custom-events)
* [存取ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [新增記錄回呼](#adding-record-callbacks)。

>[!NOTE]
>
>此資訊基本上是一般的，但針對特定範例使用[Adobe Analytics](/help/sites-administering/adobeanalytics.md)。
>
>有關開發元件和對話框的一般資訊，請參閱[開發元件](/help/sites-developing/components.md)。

## 自訂事件{#custom-events}

自訂事件會追蹤任何與頁面上特定元件的可用性相關的項目。 這也包括範本專屬的事件，因為頁面元件會視為另一個元件。

### 在頁面載入時追蹤自訂事件{#tracking-custom-events-on-page-load}

您可以使用偽屬性`data-tracking`來完成此操作（仍支援舊記錄屬性以實現回溯相容性）。 您可以將其新增至任何HTML標籤。

`data-tracking`的語法為

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

您可以將任何數量的機碼值組作為第二個參數（稱為有效負載）傳遞。

範例看起來可能如下：

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

頁面載入時，會收集所有`data-tracking`屬性，並新增至ContextHub的事件存放區，以便對應至Adobe Analytics事件。 未對應的事件將不會由Adobe Analytics追蹤。 如需關於對應事件的詳細資訊，請參閱[連線至Adobe Analytics](/help/sites-administering/adobeanalytics.md) 。

### 在頁面載入{#tracking-custom-events-after-page-load}後追蹤自訂事件

若要追蹤頁面載入後發生的事件（例如使用者互動），請使用`CQ_Analytics.record` JavaScript函式：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

其中

* `events` 是字串或字串陣列（適用於多個事件）。

* `values` 包含所有要追蹤的值
* `collect` 為選用項目，將傳回包含事件和資料物件的陣列。
* `options` 為選用項目，且包含HTML元素和等連結追 `obj` 蹤選 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`項。

* `componentPath` 是必要的屬性，建議將其設為  `<%=resource.getResourceType()%>`

例如，使用下列定義時，按一下&#x200B;**跳至top**&#x200B;連結的使用者會導致觸發`jumptop`和`headlineclick`這兩個事件：

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 存取ContextHub {#accessing-values-in-the-contexthub}中的值

ContextHub JavaScript API具有`getStore(name)`函式，可傳回指定的存放區（若有）。 儲存具有`getItem(key)`函式，該函式返回指定密鑰的值（如果可用）。 使用`getKeys()`函式可檢索特定儲存的已定義鍵陣列。

您可以使用`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`函式綁定函式，以通知儲存區上的值更改。

要通知ContextHub的初始可用性，最好使用`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`函式。

**ContextHub的其他事件：**

所有商店都準備就緒：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

特定儲存：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另請參閱完整的[ContextHub API參考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 添加記錄回調{#adding-record-callbacks}

使用函式`CQ_Analytics.registerBeforeCallback(callback,rank)`和`CQ_Analytics.registerAfterCallback(callback,rank)`註冊回呼之前和之後。

這兩個函式都將函式當作第一個引數，並將排名當作第二個引數，而此引數會指定回呼的執行順序。

如果回呼傳回false，則執行鏈中後續的回呼將不會執行。
