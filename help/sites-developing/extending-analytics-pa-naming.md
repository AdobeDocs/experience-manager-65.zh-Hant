---
title: 為Analytics實作伺服器端頁面命名
description: Adobe Analytics會使用s.pageName屬性來唯一識別頁面，並針對頁面收集資料建立關聯
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# 為Analytics實作伺服器端頁面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用`s.pageName`屬性來唯一識別頁面，並為頁面所收集的資料建立關聯。 通常您要在AEM中執行以下工作，將AEM傳送給Analytics的值指派給此屬性：

* 使用Analytics雲端服務架構將CQ變數對應至Analytics `s.pageName`屬性。 (請參閱[將元件資料與Adobe Analytics屬性對應](/help/sites-administering/adobeanalytics-mapping.md)。)

* 設計頁面元件，使其包含您對應至`s.pageName`屬性的CQ變數。 (請參閱[為自訂元件實作Adobe Analytics追蹤](/help/sites-developing/extending-analytics-components.md)。)

若要在Sites主控台和Content Insight中公開Analytics報表資料，AEM需要每個頁面的`s.pageName`屬性值。 AEM Analytics Java API定義您實作的`AnalyticsPageNameProvider`介面，以提供Sites主控台和內容深入分析的`s.pageName`屬性值。 您的`AnaltyicsPageNameProvider`服務會解析伺服器上的pageName屬性以用於報表用途，因為它可以在使用者端上使用JavaScript動態設定以用於追蹤用途。

## 預設Analytics頁面名稱提供者服務 {#the-default-analytics-page-name-provider-service}

`DefaultPageNameProvider`服務是預設服務，可決定用於擷取頁面之Analytics資料的`s.pageName`屬性值。 此服務可與AEM foundation頁面元件( `/libs/foundation/components/page`)搭配使用。 此頁面元件會定義下列要對應至`s.pageName`屬性的CQ變數：

* `pagedata.path`：值已設定為頁面路徑。
* `pagedata.title`：值已設定為頁面標題。
* `pagedata.navTitle`：值已設定為頁面導覽標題。

`DefaultPageNameProvider`服務決定哪些CQ變數對應到Analytics雲端服務架構中的`s.pageName`屬性。 然後，服務會決定用於擷取分析報表資料的適當頁面屬性：

* `pagedata.path`：服務使用`page.getPath()`

* `pagedata.title`：服務使用`page.getTitle()`

* `pagedata.navTitle`：服務使用`page.getNavigationTitle()`

`page`物件是頁面的[`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/tw/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java物件。

如果您未將CQ變數對應到架構中的`s.pageName`屬性，則會從頁面路徑產生`s.pageName`的值。 例如，路徑為`/content/geometrixx/en`的頁面使用`s.pageName`的值`content:geometrixx:en`。

>[!NOTE]
>
>DefaultPageNameProvider服務使用100的服務等級。

## 在Analytics報告中維護連續性 {#maintaining-continuity-in-analytics-reporting}

若要維護頁面的完整分析資料歷史記錄，用於頁面的s.pageName屬性值永不變更。 不過，可以輕鬆變更基礎頁面元件定義的分析屬性。 例如，移動頁面會變更`pagedata.path`的值，並中斷報告記錄的連續性：

* 針對先前路徑所收集的資料不再與頁面相關聯。
* 如果不同頁面使用另一個頁面曾經使用的路徑，則不同頁面會繼承該路徑的資料。

為確保報告連續性，`s.pageName`的值應具有以下特性：

* 獨特。
* 穩定。
* 人類看得懂的。

例如，自訂頁面元件可以包含頁面屬性，作者可使用此屬性指定作為`s.pageProperties`屬性值的頁面的唯一ID：

* 頁面包含分析變數，該變數會設定為儲存在頁面屬性中的唯一ID值。
* Analytics變數對應至Analytics框架中的`s.pageProperties`屬性。
* 您實作的AnalyticsPageNameProvider介面會擷取用於查詢頁面Analytics資料的頁面屬性值。

>[!NOTE]
>
>請向您的Analytics顧問尋求協助，為您的`s.pageName`值開發有效的策略。

### 實作Analytics頁面名稱提供者服務 {#implementing-an-analytics-page-name-provider-service}

將`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider`介面實作為OSGi服務，以自訂擷取`s.pageName`屬性值的邏輯。 網站頁面分析和內容分析會使用此服務從Analytics擷取報表資料。

AnalyticsPageNameProvider介面會定義您必須實作的兩種方法：

* `getPageName`：傳回`String`值，該值代表要用作`s.pageName`屬性的值。

* `getResource`：傳回`org.apache.sling.api.resource.Resource`物件，代表與`s.pageName`屬性關聯的頁面。

這兩種方法都將`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext`物件當作引數。 `AnalyticsPageNameContext`類別提供分析呼叫內容的相關資訊：

* 頁面資源的基底路徑。
* Analytics雲端服務設定的`Framework`物件。
* 頁面的`Resource`物件。
* 頁面的`ResourceResolver`物件。

類別也提供頁面名稱的設定器。

### AnalyticsPageNameProvider實作範例 {#example-analyticspagenameprovider-implementation}

下列範例`AnalyticsPageNameProvider`實作支援自訂頁面元件：

* 此元件會擴充基礎頁面元件。
* 此對話方塊包含一個欄位，供作者用來指定`s.pageName`屬性的值。
* 屬性值儲存在頁面執行個體之`jcr:content`節點的pageName屬性中。
* 儲存`s.pageName`屬性的分析屬性稱為`pagedata.pagename`。 此屬性對應至Analytics架構中的`s.pageName`屬性。

如果架構對應已正確設定，下列`getPageName`方法實作會傳回pageName節點屬性的值：

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

getResource方法的下列實作會傳回頁面的Resource物件：

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

下列程式碼代表整個類別，包括設定服務的SCR註解。 服務排名為200，會覆寫預設服務。

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
