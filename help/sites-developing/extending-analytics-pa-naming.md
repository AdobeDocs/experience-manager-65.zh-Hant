---
title: 為Analytics實作伺服器端頁面命名
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics使用s.pageName屬性來唯一識別頁面，並為頁面收集的資料建立關聯
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

# 為Analytics實作伺服器端頁面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用 `s.pageName` 屬性來唯一識別頁面，以及為頁面收集的資料建立關聯。 通常，您會在AEM中執行下列工作，將值指派給AEM傳送至Analytics的此屬性：

* 使用Analytics雲端服務架構將CQ變數對應至Analytics `s.pageName` 屬性。 (請參閱 [將元件資料與Adobe Analytics屬性對應](/help/sites-administering/adobeanalytics-mapping.md).)

* 設計頁面元件，使其包含您對應至的CQ變數 `s.pageName` 屬性。 (請參閱 [為自訂元件實作Adobe Analytics追蹤](/help/sites-developing/extending-analytics-components.md).)

若要在Sites主控台和Content Insight中公開Analytics報表資料，AEM需要 `s.pageName` 屬性。 AEM Analytics Java API定義 `AnalyticsPageNameProvider` 實作的介面，以便Sites Console和Content Insights能夠使用 `s.pageName` 屬性。 您的 `AnaltyicsPageNameProvider` 服務會解析伺服器上的pageName屬性以用於報告用途，因為可使用用戶端上的Javascript以動態方式設定，以用於追蹤用途。

## 預設Analytics頁面名稱提供者服務 {#the-default-analytics-page-name-provider-service}

此 `DefaultPageNameProvider` 服務是決定 `s.pageName` 屬性，用於擷取頁面的Analytics資料。 此服務可與AEM基礎頁面元件( `/libs/foundation/components/page`)。 此頁面元件會定義下列CQ變數，這些變數應對應至 `s.pageName` 屬性：

* `pagedata.path`:值會設為頁面路徑。
* `pagedata.title`:值會設為頁面標題。
* `pagedata.navTitle`:值會設為頁面導覽標題。

此 `DefaultPageNameProvider` 服務會決定將哪些CQ變數對應至 `s.pageName` 屬性。 接著，服務會決定要用於擷取分析報表資料的適當頁面屬性：

* `pagedata.path`:服務使用 `page.getPath()`

* `pagedata.title`:服務使用 `page.getTitle()`

* `pagedata.navTitle`:服務使用 `page.getNavigationTitle()`

此 `page` 物件是 [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) 頁面的Java物件。

若您未將CQ變數對應至 `s.pageName` 框架中的屬性， `s.pageName` 會從頁面路徑產生。 例如，具有路徑的頁面 `/content/geometrixx/en` 使用值 `content:geometrixx:en` for `s.pageName`.

>[!NOTE]
>
>DefaultPageNameProvider服務使用100的服務排名。

## 維護Analytics報表的連續性 {#maintaining-continuity-in-analytics-reporting}

維護頁面分析資料的完整歷史記錄需要用於頁面的s.pageName屬性的值不會變更。 不過，基礎頁面元件定義的分析屬性可輕鬆變更。 例如，移動頁面會變更 `pagedata.path` 並中斷報表歷史記錄的連續性：

* 針對上一路徑收集的資料不再與頁面相關聯。
* 如果不同頁面使用另一個頁面曾經使用的路徑，則不同頁面會繼承該路徑的資料。

為確保報告的連續性， `s.pageName` 應具有下列特性：

* 唯一.
* 穩定。
* 人類看得懂。

例如，自訂頁面元件可包含頁面屬性，供作者用來為頁面指定唯一ID，作為 `s.pageProperties` 屬性：

* 頁面包含的分析變數，會設為儲存在頁面屬性中之唯一ID的值。
* 分析變數會對應至 `s.pageProperties` 屬性。
* 您實施的AnalyticsPageNameProvider介面會擷取頁面屬性的值，以用於查詢頁面Analytics資料。

>[!NOTE]
>
>請洽詢您的Analytics顧問，以取得協助，為您的 `s.pageName` 值。

### 實作Analytics頁面名稱提供者服務 {#implementing-an-analytics-page-name-provider-service}

實作 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 介面作為OSGi服務，以自訂擷取 `s.pageName` 屬性值。 「網站頁面分析」和「內容分析」使用服務從Analytics擷取報表資料。

AnalyticsPageNameProvider介面定義您必須實作的兩種方法：

* `getPageName`:傳回 `String` 代表要用作 `s.pageName` 屬性。

* `getResource`:傳回 `org.apache.sling.api.resource.Resource` 代表與 `s.pageName` 屬性。

這兩種方法會採用 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 物件作為參數。 此 `AnalyticsPageNameContext` 類別提供analytics呼叫內容的相關資訊：

* 頁面資源的基本路徑。
* 此 `Framework` Analytics雲端服務設定的物件。
* 此 `Resource` 物件。
* 此 `ResourceResolver` 物件。

類還為頁名提供setter。

### 範例AnalyticsPageNameProvider實作 {#example-analyticspagenameprovider-implementation}

下列範例 `AnalyticsPageNameProvider` 實作支援自訂頁面元件：

* 元件會擴充基礎頁面元件。
* 對話方塊包含作者用來指定 `s.pageName` 屬性。
* 屬性值儲存在 `jcr:content`頁面例項的節點。
* 儲存的Analytics屬性 `s.pageName` 屬性被呼叫 `pagedata.pagename`. 此屬性已對應至 `s.pageName` 屬性。

以下是 `getPageName` 如果框架映射配置正確，則方法返回pageName節點屬性的值：

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

getResource方法的下列實施會傳回頁面的Resource物件：

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

以下代碼表示整個類，包括配置服務的SCR注釋。 請注意，服務排名為200，會覆寫預設服務。

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
