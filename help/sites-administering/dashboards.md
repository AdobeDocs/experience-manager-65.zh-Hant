---
title: 控制面板
seo-title: 控制面板
description: 瞭解如何建立、設定和開發新的AEM儀表板。
seo-description: 瞭解如何建立、設定和開發新的AEM儀表板。
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
translation-type: tm+mt
source-git-commit: 69dfd6b41b32cb9131fd90fd7039a0c224889db5

---


# 控制面板{#dashboards}

使用AEM時，您可以管理許多不同類型的內容（例如頁面、資產）。 AEM儀表板提供簡單易用且可自訂的方式，來定義顯示整合資料的頁面。

>[!NOTE]
>
>AEM控制面板是依每位使用者而建立，因此使用者只能存取其專屬的控制面板。
>
>不過，「控 [制面板](#creating-a-dashboard-template) 」範本可用於共用常用的設定和「控制面板」配置。

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理控制面板 {#administering-dashboards}

### 建立控制面板 {#creating-a-dashboard}

要建立新控制面板，請按如下步驟進行：

1. 在「工 **具** 」區段中，按一 **下「設定控制台」**。
1. 在樹狀結構中，按兩下「儀 **表板**」。
1. 按一 **下「新控制面板**」。
1. 鍵入 **Title** （例如My Dashboard）和 **Name**。
1. 按一下&#x200B;**「建立」**。

### 複製控制面板 {#cloning-a-dashboard}

您可能想要擁有多個控制面板，以便從不同檢視中快速查看您的內容相關資訊。 為協助您建立新的控制面板，AEM提供可用來複製現有控制面板的仿製功能。 若要複製控制面板，請依下列步驟進行：

1. 在「工 **具** 」區段中，按一 **下「設定控制台」**。

1. 在樹狀結構中，按一下「控 **制面板**」。
1. 按一下您要複製的控制面板。

1. 按一 **下仿製**。

1. 輸入新 **控制面板** 的名稱。

### 移除控制面板 {#removing-a-dashboard}

1. 在「工 **具** 」區段中，按一 **下「設定控制台」**。

1. 在樹狀結構中，按一下「控 **制面板**」。
1. 按一下您要刪除的控制面板。

1. 按一下 **移除**。

1. 按一 **下「是** 」以確認。

## 控制面板元件 {#dashboard-components}

### 概覽 {#overview}

控制面板元件只是一般 [AEM元件](/help/sites-developing/developing-components-samples.md)。 本節說明AEM隨附的報表元件。

### 網頁分析報表元件 {#web-analytics-reporting-components}

AEM隨附一組元件，可呈現您 [SiteCatalyst資料的多個度量](/help/sites-administering/adobeanalytics.md) 。 這些元件會列在「儀表板」區段下 **的Sidekick** 。

每個報表元件至少提供三個標籤：

* **基本**:包含主配置。

* **** 報表：包含每個報表的特定設定。
* **樣式**:包含樣式設定，例如圖表大小和邊界。

報表元件會以預設設定初始化，以協助您快速設定控制面板。

#### 基本配置 {#basic-configuration}

「基 **本** 」頁籤提供對以下配置項的訪問：

**標題** ：控制面板上顯示的標題。

**請求類型** ：請求資料的方式。

**SiteCatalyst設定（選用）** ：您要用來連線至SiteCatalyst的設定。 如果未提供，則假定在「儀表板」頁面（通過頁面屬性）上配置配置。

**報表套裝ID（選用）** ：您要用來產生圖形的SiteCatalyst報表套裝。

#### 報表設定 {#report-configuration}

若要顯示Web統計資料，您必須定義您要擷取之資料的日期範圍。 「報 **表** 」標籤提供兩個欄位來定義該範圍。

>[!NOTE]
>
>設定較大的日期範圍可降低控制面板的回應速度。

**日期自** 「絕對」或從中擷取資料的相對日期。

**日期至** 「絕對」或擷取資料的相對日期。

每個元件也定義特定的設定。

#### 超時報表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期詳細程度** X軸的時間單位（例如日、小時）。

**量度** ：您要顯示的事件清單。

**元素** ：劃分圖表中量度資料的元素清單。

#### 排名清單報表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素** ：在圖形中劃分量度資料的元素。

**量度** ：您要顯示的事件。

**否. 排名最前的項目** ：報表顯示的項目數。

#### 排名報表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**量度** ：您要顯示的事件。

**元素** ：在圖形中劃分量度資料的元素。

#### 主要網站區域報表 {#top-site-section-report}

此元件會根據下列設定顯示一個圖形，顯示網站較常瀏覽的區段。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否. 排名最前的項目** ：報表中顯示的區段數。

#### 趨勢報表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期詳細程度** X軸的時間單位（例如日、小時）。

**量度** ：您要顯示的事件。

**元素** ：在圖形中劃分量度資料的元素。

## 擴充控制面板 {#extending-dashboard}

### 概覽 {#overview-1}

控制面板是一般頁面( `cq:Page`)，因此，任何元件都可用來組合控制面板。

預設的元件群組包含 `Dashboard` 分析報表元件，預設會在範本上啟用。

### Creating A Dashboard Template {#creating-a-dashboard-template}

範本會定義新控制面板的預設內容。 您可以使用數個範本來建立不同類型的控制面板。

控制面板範本的建立方式與其他頁面範本類似，但是這些範本會儲存在下 `/libs/cq/dashboards/templates/`方。 請參閱「 [建立內容頁面範本](/help/sites-developing/website.md#creating-the-contentpage-template) 」一節。

>[!NOTE]
>
>控制面板範本會在使用者之間共用。

### 開發儀表板元件 {#developing-a-dashboard-component}

開發控制面板元件包括建立一般AEM元件。 本節說明顯示前10名貢獻者的元件範例。

![chlimage_1-31](assets/chlimage_1-31a.png)

頂層作者元件儲存在儲存庫中， `/apps/geometrixx-outdoors/components/reporting` 由以下組成：

1. 讀取 `jsp` jcr資料並定義預留位置的 `html` 檔案。

1. 用戶端程式庫包含一個檔 `js` 案，可擷取並排序資料，然後填入預留 `html` 位置。

![chlimage_1-32](assets/chlimage_1-32a.png)

以下Javascript檔案在用戶端 `geout.reporting.topauthors` 庫中 [](/help/sites-developing/clientlibs.md) 定義為元件本身的子項。

QueryBuilder [用於查詢儲存庫](/help/sites-developing/querybuilder-api.md) ，以讀取節 `cq:AuditEvent` 點。 查詢結果是擷取作者貢獻的JSON物件。

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

其中 `JSP` 包括 `global.jsp` 和 `clientlib`。

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

