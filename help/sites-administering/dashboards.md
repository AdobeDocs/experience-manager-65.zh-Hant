---
title: 控制面板
description: 瞭解如何建立、設定和開發新的AEM儀表板。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 4%

---

# 控制面板{#dashboards}

使用AEM時，您可以管理許多不同型別的內容（例如頁面、資產）。 AEM儀表板提供簡單易用且可自訂的方式，來定義顯示整合資料的頁面。

>[!NOTE]
>
>AEM控制面板是按使用者建立，因此使用者只能存取自己的控制面板。
>
>但是，[儀表板範本](#creating-a-dashboard-template)可用於共用一般設定和儀表板配置。

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理儀表板 {#administering-dashboards}

### 建立控制面板 {#creating-a-dashboard}

1. 在&#x200B;**工具**&#x200B;區段中，按一下&#x200B;**設定主控台**。
1. 在樹狀結構中，按兩下&#x200B;**儀表板**。
1. 按一下&#x200B;**新儀表板**。
1. 輸入&#x200B;**Title** （例如，我的儀表板）和&#x200B;**Name**。
1. 按一下&#x200B;**建立**。

### 複製控制面板 {#cloning-a-dashboard}

您可能想要有多個控制面板，以從不同檢視快速檢視有關您內容的資訊。 為協助您建立新儀表板，AEM提供複製功能，可用來複製現有儀表板。 若要複製控制面板，請依照下列步驟進行：

1. 在&#x200B;**工具**&#x200B;區段中，按一下&#x200B;**設定主控台**。

1. 在樹狀結構中，按一下&#x200B;**儀表板**。
1. 按一下您要複製的控制面板。

1. 按一下&#x200B;**複製**。

1. 輸入新儀表板的&#x200B;**名稱**。

### 移除控制面板 {#removing-a-dashboard}

1. 在&#x200B;**工具**&#x200B;區段中，按一下&#x200B;**設定主控台**。

1. 在樹狀結構中，按一下&#x200B;**儀表板**。
1. 按一下您要刪除的控制面板。

1. 按一下&#x200B;**移除**。

1. 按一下「**是**」確認。

## 控制面板元件 {#dashboard-components}

### 概觀 {#overview}

儀表板元件不過是一般[AEM元件](/help/sites-developing/developing-components-samples.md)。 本節說明AEM隨附的報告元件。

### 網站分析報表元件 {#web-analytics-reporting-components}

AEM隨附一組元件，可轉譯[SiteCatalyst](/help/sites-administering/adobeanalytics.md)資料的多個量度。 這些元件列在&#x200B;**儀表板**&#x200B;區段下的Sidekick中。

每個報表元件至少提供三個標籤：

* **基本**：包含主要組態。

* **報告：**&#x200B;包含每個報告的特定組態。
* **樣式**：包含樣式設定，例如圖表大小和邊界。

報表元件會以預設設定進行初始化，協助您快速設定儀表板。

#### 基本設定 {#basic-configuration}

**基本**&#x200B;索引標籤提供下列組態專案的存取權：

**標題**&#x200B;顯示在儀表板上的標題。

**要求型別**&#x200B;要求資料的方式。

**SiteCatalyst設定（選擇性）**&#x200B;您要用來連線至SiteCatalyst的設定。 若未提供，則會假設設定是在「控制面板」頁面（透過頁面屬性）上進行。

**報表套裝ID （選用）**&#x200B;您要用來產生圖形的SiteCatalyst報表套裝。

#### 報告設定 {#report-configuration}

若要顯示網頁統計資料，您必須定義要收集的資料日期範圍。 **報表**&#x200B;索引標籤提供兩個欄位來定義該範圍。

>[!NOTE]
>
>設定較大的日期範圍可能會降低儀表板的回應能力。

**起始日期**&#x200B;擷取資料的絕對或相對日期。

**至**&#x200B;日期擷取資料的絕對或相對日期。

每個元件也會定義特定的設定。

#### 超時報表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期粒度** X軸的時間單位（例如日、小時）。

**量度**&#x200B;您要顯示的事件清單。

**元素**&#x200B;劃分圖形中量度資料的元素清單。

#### 排名清單報表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素**&#x200B;劃分圖形中量度資料的元素。

**量度**&#x200B;您要顯示的事件。

**否 排名最前的專案**&#x200B;報告所顯示的專案數。

#### 排名報表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**量度**&#x200B;您要顯示的事件。

**元素**&#x200B;劃分圖形中量度資料的元素。

#### 主要網站區域報表 {#top-site-section-report}

此元件會根據下列設定，顯示一個圖形，其中顯示網站中造訪次數最多的區域。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否 排名最前的專案**&#x200B;在報告中顯示的區段數。

#### 趨勢報表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期粒度** X軸的時間單位（例如日、小時）。

**量度**&#x200B;您要顯示的事件。

**元素**&#x200B;劃分圖形中量度資料的元素。

## 擴充控制面板 {#extending-dashboard}

### 概觀 {#overview-1}

儀表板是一般頁面( `cq:Page`)，因此任何元件都可以用來組裝儀表板。

有一個預設元件群組`Dashboard`，其中包含預設為啟用範本的分析報告元件。

### 建立控制面板範本 {#creating-a-dashboard-template}

範本會定義新控制面板的預設內容。 您可以使用數個範本來建立不同型別的儀表板。

控制面板範本的建立方式與其他頁面範本相同，只是它們儲存在`/libs/cq/dashboards/templates/`下。 請參閱[建立Contentpage範本](/help/sites-developing/website.md#creating-the-contentpage-template)區段。

>[!NOTE]
>
>控制面板範本會在使用者之間共用。

### 開發儀表板元件 {#developing-a-dashboard-component}

開發儀表板元件包含建立一般AEM元件。 本節說明顯示前10名貢獻者的元件範例。

![chlimage_1-31](assets/chlimage_1-31a.png)

最常使用的作者元件儲存在`/apps/geometrixx-outdoors/components/reporting`的存放庫中，並由：

1. 讀取jcr資料並定義`html`預留位置的`jsp`檔案。

1. 包含一個`js`檔案的使用者端資料庫，可擷取及排序資料，然後填入`html`預留位置。

![chlimage_1-32](assets/chlimage_1-32a.png)

下列JavaScript檔案在`geout.reporting.topauthors` [使用者端資料庫](/help/sites-developing/clientlibs.md)中定義為元件本身的子系。

[QueryBuilder](/help/sites-developing/querybuilder-api.md)用於查詢存放庫以讀取`cq:AuditEvent`節點。 查詢結果是JSON物件，系統會從中擷取作者貢獻。

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

`JSP`包含`global.jsp`和`clientlib`。

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
