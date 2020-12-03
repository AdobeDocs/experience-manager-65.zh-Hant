---
title: 實作Analytics的伺服器端頁面命名
seo-title: 實作Analytics的伺服器端頁面命名
description: Adobe Analytics使用s.pageName屬性來唯一識別頁面，並關聯為頁面收集的資料
seo-description: Adobe Analytics使用s.pageName屬性來唯一識別頁面，並關聯為頁面收集的資料
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---


# 實作Analytics的伺服器端頁面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用`s.pageName`屬性來唯一識別頁面，並關聯為頁面收集的資料。 通常，您會在AEM中執行下列工作，以指派值給AEM傳送至Analytics的此屬性：

* 使用Analytics雲端服務架構將CQ變數對應至Analytics `s.pageName`屬性。 （請參閱[將元件資料與Adobe Analytics屬性對應](/help/sites-administering/adobeanalytics-mapping.md)）。

* 設計頁面元件，使其包含您對應至`s.pageName`屬性的CQ變數。 （請參閱[實作自訂元件的Adobe Analytics追蹤](/help/sites-developing/extending-analytics-components.md)）。

若要在「網站」主控台和「內容分析」中公開Analytics報表資料，AEM需要每個頁面的`s.pageName`屬性值。 AEM Analytics Java API定義您實作的`AnalyticsPageNameProvider`介面，以提供「網站」主控台和「內容前瞻分析」的`s.pageName`屬性值。 您的`AnaltyicsPageNameProvider`服務會解析伺服器上的pageName屬性以用於報告，因為它可使用用戶端上的Javascript動態設定，以用於追蹤目的。

## 預設分析頁面名稱提供者服務{#the-default-analytics-page-name-provider-service}

`DefaultPageNameProvider`服務是預設服務，可決定`s.pageName`屬性的值，以用於擷取頁面的Analytics資料。 此服務可與AEM基礎頁面元件(`/libs/foundation/components/page`)搭配運作。 此頁元件定義下列要映射到`s.pageName`屬性的CQ變數：

* `pagedata.path`:值會設為頁面路徑。
* `pagedata.title`:值會設為頁面標題。
* `pagedata.navTitle`:此值會設為頁面導覽標題。

`DefaultPageNameProvider`服務會決定這些CQ變數中哪些變數會對應至Analytics雲端服務架構中的`s.pageName`屬性。 然後，服務會決定用於擷取分析報表資料的適當頁面屬性：

* `pagedata.path`:服務使用  `page.getPath()`

* `pagedata.title`:服務使用  `page.getTitle()`

* `pagedata.navTitle`:服務使用  `page.getNavigationTitle()`

`page`對象是頁面的[ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java對象。

如果您未將CQ變數對應至架構中的`s.pageName`屬性，則會從頁面路徑產生`s.pageName`的值。 例如，路徑`/content/geometrixx/en`的頁面使用`s.pageName`的值`content:geometrixx:en`。

>[!NOTE]
>
>DefaultPageNameProvider服務使用100的服務排名。

## 在Analytics報表中維持連續性{#maintaining-continuity-in-analytics-reporting}

若要維持頁面分析資料的完整歷史記錄，需要用於頁面的s.pageName屬性值永遠不變。 不過，基礎頁面元件所定義的分析屬性可輕鬆變更。 例如，移動頁面會變更`pagedata.path`的值，並中斷報告歷史記錄的連續性：

* 為先前路徑收集的資料不再與頁面相關聯。
* 如果不同頁面使用其他頁面曾經使用的路徑，則不同頁面會繼承該路徑的資料。

為確保報告的連續性，`s.pageName`的值應具有以下特性：

* 唯一.
* 穩定。
* 人類可讀。

例如，自訂頁面元件可包含作者用來為頁面指定唯一ID的頁面屬性，該唯一ID用作`s.pageProperties`屬性的值：

* 該頁面包含分析變數，其設定為儲存在頁面屬性中之唯一ID的值。
* 分析變數會對應至Analytics架構中的`s.pageProperties`屬性。
* 您對AnalyticsPageNameProvider介面的實作會擷取用於查詢頁面Analytics資料的頁面屬性值。

>[!NOTE]
>
>請洽詢您的Analytics顧問，以取得針對`s.pageName`值制定有效策略的協助。

### 實施Analytics頁面名稱提供者服務{#implementing-an-analytics-page-name-provider-service}

將`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider`介面實作為OSGi服務，以自定義檢索`s.pageName`屬性值的邏輯。 「網站」頁面分析和「內容分析」使用服務從Analytics擷取報表資料。

AnalyticsPageNameProvider介面定義您必須實作的兩種方法：

* `getPageName`:傳回 `String` 代表要用作屬性的值的 `s.pageName` 值。

* `getResource`:傳回 `org.apache.sling.api.resource.Resource` 代表與屬性關聯之頁面的物 `s.pageName` 件。

這兩種方法都以`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext`物件為參數。 `AnalyticsPageNameContext`類別提供分析呼叫的上下文相關資訊：

* 頁面資源的基本路徑。
* Analytics雲端服務設定的`Framework`物件。
* 頁面的`Resource`物件。
* 頁面的`ResourceResolver`物件。

類還為頁面名稱提供setter。

### 範例AnalyticsPageNameProvider實施{#example-analyticspagenameprovider-implementation}

以下範例`AnalyticsPageNameProvider`實作支援自訂頁面元件：

* 該元件擴展了基礎頁元件。
* 該對話框包含作者用於指定`s.pageName`屬性值的欄位。
* 屬性值儲存在頁面實例的`jcr:content`節點的pageName屬性中。
* 儲存`s.pageName`屬性的分析屬性稱為`pagedata.pagename`。 此屬性會映射至Analytics架構中的`s.pageName`屬性。

如果框架映射配置正確，則`getPageName`方法的以下實現返回pageName節點屬性的值：

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

getResource方法的以下實現返回該頁的Resource對象：

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

以下代碼代表整個類，包括配置服務的SCR注釋。 請注意，服務排名為200，會覆寫預設服務。

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

