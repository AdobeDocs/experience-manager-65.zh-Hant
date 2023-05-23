---
title: 控制面板
seo-title: Dashboards
description: 瞭解如何建立、配置和開發新儀AEM表板。
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 4%

---

# 控制面板{#dashboards}

使用AEM時，您能夠管理許多不同類型的內容（如頁面、資產）。 儀AEM表板提供了一種易於使用和可自定義的方法來定義顯示統一資料的頁面。

>[!NOTE]
>
>儀AEM表板是按每個用戶建立的，因此用戶只能訪問其自己的儀表板。
>
>但是， [儀表板模板](#creating-a-dashboard-template) 可用於共用公共配置和儀表板佈局。

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理儀表板 {#administering-dashboards}

### 建立儀表板 {#creating-a-dashboard}

要建立新儀表板，請按如下步驟操作：

1. 在 **工具** ，按一下 **配置控制台**。
1. 在樹中，按兩下 **儀表板**。
1. 按一下 **新建儀表板**。
1. 鍵入 **標題** （例如我的儀表板）和 **名稱**。
1. 按一下&#x200B;**建立**。

### 克隆儀表板 {#cloning-a-dashboard}

您可能希望具有多個儀表板，以便從不同的視圖快速查看有關您的內容的資訊。 為幫助您建立新儀表板，AEM提供了可用於複製現有儀表板的克隆功能。 要克隆儀表板，請按如下步驟操作：

1. 在 **工具** ，按一下 **配置控制台**。

1. 在樹中，按一下 **儀表板**。
1. 按一下要克隆的儀表板。

1. 按一下 **克隆**。

1. 鍵入 **名稱** 新儀表板。

### 刪除儀表板 {#removing-a-dashboard}

1. 在 **工具** ，按一下 **配置控制台**。

1. 在樹中，按一下 **儀表板**。
1. 按一下要刪除的儀表板。

1. 按一下&#x200B;**移除**。

1. 按一下「**是**」確認。

## 儀表板元件 {#dashboard-components}

### 概觀 {#overview}

儀表板元件只是常規元件 [AEM元件](/help/sites-developing/developing-components-samples.md)。 本節介紹隨附的報告組AEM件。

### Web Analytics報告元件 {#web-analytics-reporting-components}

隨AEM一組元件一起提供 [SiteCatalyst](/help/sites-administering/adobeanalytics.md) 資料。 這些元件列在Sidekick下 **儀表板** 的子菜單。

每個報告元件至少提供三個頁籤：

* **基本**:包含主配置。

* **報告：** 包含每個報告的特定配置。
* **樣式**:包含樣式配置，如圖表大小和邊距。

報告元件是使用預設配置初始化的，該配置可幫助您快速設定儀表板。

#### 基本配置 {#basic-configuration}

的 **基本** 頁籤提供對以下配置項的訪問：

**標題** 儀表板上顯示的標題。

**請求類型** 請求資料的方式。

**SiteCatalyst配置（可選）** 要用於連接到SiteCatalyst的配置。 如果未提供，則假定配置是在儀表板頁（通過頁面屬性）上配置。

**報表套件ID（可選）** 要用於生成圖形的SiteCatalyst報告套件。

#### 報表配置 {#report-configuration}

為了顯示Web統計資訊，您需要定義要發送的資料的日期範圍。 的 **報告** 頁籤提供兩個欄位來定義該範圍。

>[!NOTE]
>
>設定較大的日期範圍可以降低儀表板的響應速度。

**日期自** 從中提取資料的絕對或相對日期。

**日期至** 讀取資料的絕對或相對日期。

每個元件還定義特定設定。

#### 超時報表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期粒度** X軸的時間單位（如日、小時）。

**度量** 要顯示的事件清單。

**元素** 分解圖形中度量資料的元素清單。

#### 排名清單報表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素** 分解圖形中度量資料的元素。

**度量** 要顯示的事件。

**否. 頂項** 報表顯示的項數。

#### 排名報表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**度量** 要顯示的事件。

**元素** 分解圖形中度量資料的元素。

#### 主要網站區域報表 {#top-site-section-report}

此元件顯示一個圖表，顯示網站的訪問次數較多的部分，具體取決於以下配置。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否. 頂項** 報表中顯示的節數。

#### 趨勢報表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期粒度** X軸的時間單位（如日、小時）。

**度量** 要顯示的事件。

**元素** 分解圖形中度量資料的元素。

## 擴展儀表板 {#extending-dashboard}

### 概觀 {#overview-1}

儀表板是普通頁( `cq:Page`)，因此任何元件都可用於裝配儀表板。

存在預設元件組 `Dashboard` 包含預設情況下在模板上啟用的分析報告元件。

### 建立儀表板模板 {#creating-a-dashboard-template}

模板定義新儀表板的預設內容。 您可以使用多個模板來建立不同類型的儀表板。

儀表板模板與其他頁面模板一樣建立，但它們儲存在 `/libs/cq/dashboards/templates/`。 查看 [建立內容頁模板](/help/sites-developing/website.md#creating-the-contentpage-template) 的子菜單。

>[!NOTE]
>
>儀表板模板在用戶之間共用。

### 開發儀表板元件 {#developing-a-dashboard-component}

開發操控板元件包括建立常規元AEM件。 本節介紹顯示前10個參與者的元件示例。

![chlimage_1-31](assets/chlimage_1-31a.png)

頂級作者元件儲存在儲存庫中，位於 `/apps/geometrixx-outdoors/components/reporting` 由：

1. a `jsp` 讀取jcr資料並定義 `html` 佔位符。

1. 包含一個 `js` 讀取並排序資料的檔案，然後填充 `html` 佔位符。

![chlimage_1-32](assets/chlimage_1-32a.png)

以下Javascript檔案在 `geout.reporting.topauthors` [客戶端庫](/help/sites-developing/clientlibs.md) 作為元件本身的子項。

的 [查詢生成器](/help/sites-developing/querybuilder-api.md) 用於查詢要讀取的儲存庫 `cq:AuditEvent` 節點。 查詢結果是JSON對象，從中提取作者貢獻。

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

的 `JSP` 包括 `global.jsp` 和 `clientlib`。

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
