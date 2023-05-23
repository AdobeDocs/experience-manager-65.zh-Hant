---
title: 為分析實現伺服器端頁面命名
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics使用s.pageName屬性唯一標識頁面並關聯為頁面收集的資料
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# 為分析實現伺服器端頁面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用 `s.pageName` 屬性，以唯一標識頁並關聯為頁收集的資料。 通常，在中執行以下任AEM務，以將值分配給發送到分AEM析的此屬性：

* 使用Analytics雲服務框架將CQ變數映射到Analytics `s.pageName` 屬性。 (請參閱 [使用Adobe Analytics屬性映射元件資料](/help/sites-administering/adobeanalytics-mapping.md)。)

* 設計頁面元件，使其包括映射到的CQ變數 `s.pageName` 屬性。 (請參閱 [實施Adobe Analytics定制元件跟蹤](/help/sites-developing/extending-analytics-components.md)。)

要在站點控制台和Content Insight中公開分析報告資料，AEM需要 `s.pageName` 屬性。 Analytics AEM Java API定義 `AnalyticsPageNameProvider` 您實施的介面，以向Sites控制台和Content Insights提供 `s.pageName` 屬性。 您 `AnaltyicsPageNameProvider` 服務解析伺服器上的pageName屬性以用於報告目的，因為可以在客戶端上使用Javascript動態設定該屬性以用於跟蹤目的。

## 「預設分析」頁名稱提供程式服務 {#the-default-analytics-page-name-provider-service}

的 `DefaultPageNameProvider` 服務是確定 `s.pageName` 用於檢索頁面的Analytics資料的屬性。 服務與基礎頁元件AEM( `/libs/foundation/components/page`)。 此頁元件定義以下要映射到的CQ變數 `s.pageName` 屬性：

* `pagedata.path`:該值將設定為頁面路徑。
* `pagedata.title`:該值設定為頁面標題。
* `pagedata.navTitle`:該值將設定為頁面導航標題。

的 `DefaultPageNameProvider` 服務確定這些CQ變數中哪個被映射到 `s.pageName` Analytics雲服務框架中的屬性。 然後，該服務確定用於檢索分析報告資料的相應頁屬性：

* `pagedata.path`:服務使用 `page.getPath()`

* `pagedata.title`:服務使用 `page.getTitle()`

* `pagedata.navTitle`:服務使用 `page.getNavigationTitle()`

的 `page` 對象是 [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) 頁的Java對象。

如果不將CQ變數映射到 `s.pageName` 框架中的屬性， `s.pageName` 從頁面路徑生成。 例如，具有路徑的頁面 `/content/geometrixx/en` 使用值 `content:geometrixx:en` 為 `s.pageName`。

>[!NOTE]
>
>DefaultPageNameProvider服務使用100的服務等級。

## 在分析報告中維護連續性 {#maintaining-continuity-in-analytics-reporting}

維護頁面分析資料的完整歷史記錄要求用於頁面的s.pageName屬性的值永不更改。 但是，可以輕鬆地更改基礎頁元件定義的分析屬性。 例如，移動頁面會更改 `pagedata.path` 並中斷報告歷史記錄的連續性：

* 為上一路徑收集的資料不再與頁面關聯。
* 如果不同頁使用另一頁曾經使用的路徑，則不同頁將繼承該路徑的資料。

為確保報告的連續性， `s.pageName` 應具有以下特點：

* 唯一.
* 穩定。
* 可讀。

例如，自定義頁面元件可以包括頁面屬性，作者使用該屬性為用作頁面值的頁面指定唯一ID `s.pageProperties` 屬性：

* 該頁包括一個分析變數，該變數被設定為儲存在page屬性中的唯一ID的值。
* 分析變數映射到 `s.pageProperties` 分析框架中的屬性。
* AnalyticsPageNameProvider介面的實現將檢索用於查詢頁分析資料的頁屬性的值。

>[!NOTE]
>
>請咨詢您的分析顧問，以獲得幫助，為您制定有效的策略 `s.pageName` 值。

### 實施分析頁名提供程式服務 {#implementing-an-analytics-page-name-provider-service}

實施 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 作為OSGi服務的介面，以自定義 `s.pageName` 屬性值。 「站點」頁分析和內容透視使用服務從分析檢索報表資料。

AnalyticsPageNameProvider介面定義了必須實現的兩種方法：

* `getPageName`:返回 `String` 表示用作 `s.pageName` 屬性。

* `getResource`:返回 `org.apache.sling.api.resource.Resource` 表示與 `s.pageName` 屬性。

兩種方法都 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 對象。 的 `AnalyticsPageNameContext` 類提供了有關分析調用的上下文的資訊：

* 頁資源的基本路徑。
* 的 `Framework` Analytics雲服務配置的對象。
* 的 `Resource` 頁面的對象。
* 的 `ResourceResolver` 頁面的對象。

類還為頁名提供setter。

### 示例AnalyticsPageNameProvider實現 {#example-analyticspagenameprovider-implementation}

以下示例 `AnalyticsPageNameProvider` 實現支援自定義頁面元件：

* 該元件擴展了基礎頁元件。
* 該對話框包含一個欄位，作者使用該欄位指定 `s.pageName` 屬性。
* 屬性值儲存在 `jcr:content`頁實例的節點。
* 儲存的分析屬性 `s.pageName` 調用屬性 `pagedata.pagename`。 此屬性映射到 `s.pageName` 分析框架中的屬性。

以下實施 `getPageName` 如果框架映射配置正確，則方法返回pageName節點屬性的值：

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

getResource方法的以下實現將返回該頁的Resource對象：

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

以下代碼表示整個類，包括配置服務的SCR注釋。 請注意，服務等級為200，它覆蓋預設服務。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
