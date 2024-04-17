---
title: 標籤庫
description: Granite、CQ和Sling標籤程式庫可讓您存取特定函式，以便在範本和元件的JSP指令碼中使用
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
solution: Experience Manager, Experience Manager Sites
feature: Developing,Tagging
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 0%

---

# 標籤庫{#tag-libraries}

Granite、CQ和Sling標籤程式庫可讓您存取特定函式，以便在範本和元件的JSP指令碼中使用。

## Granite標籤庫 {#granite-tag-library}

Granite標籤庫包含有用的函式。

當您開發Granite UI元件的jsp指令碼時，建議在指令碼頂部包含以下程式碼：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

全域也會宣告 [Sling資料庫](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

此 `<ui:includeClientLib>` tag包含AEM html使用者端資料庫，可以是js、css或主題資料庫。 對於不同型別的多個包含專案（例如js和css），此標籤必須在jsp中多次使用。 此標籤是便利的包裝函式，適用於 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 服務介面。

它具有下列屬性：

**類別**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有JavaScript和CSS資料庫。 主題名稱會從請求中擷取。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**主題**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有主題相關資料庫（CSS和JS）。 主題名稱會從請求中擷取。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有JavaScript程式庫。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有CSS資料庫。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主題**  — 僅指示主題或非主題程式庫的標幟。 如果省略，則包含兩個集合。 僅適用於純JS或CSS includes （不適用於類別或主題包含）。

此 `<ui:includeClientLib>` 標籤的使用方式如下：

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## CQ標籤庫 {#cq-tag-library}

CQ標籤庫包含有用的函式。

若要在指令碼中使用CQ標籤庫，指令碼必須以下列程式碼開頭：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中，taglib會自動宣告。

開發AEM元件的jsp指令碼時，建議在指令碼頂端包含下列程式碼：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它會宣告sling、CQ和jstl taglibs，並公開 [`<cq:defineObjects />`](#amp-lt-cq-defineobjects) 標籤之間。 這縮短並簡化元件的jsp程式碼。

### &lt;cq:text> {#cq-text}

此 `<cq:text>` 標籤是便利的標籤，可在JSP中輸出元件文字。

它具有下列選擇性屬性：

**屬性**  — 要使用的屬性名稱。 此名稱是相對於目前資源的名稱。

**值**  — 用於輸出的值。 如果此屬性存在，則會覆寫屬性屬性的使用。

**舊值**  — 用於差異輸出的值。 如果此屬性存在，則會覆寫屬性屬性的使用。

**escapeXml**  — 定義產生的字串中的字元&lt;、>、&amp;、&#39;和&#39;&#39;是否應轉換為對應的字元實體代碼。 預設值為false。 逸出套用在選擇性格式之後。

**格式**  — 選擇性的java.text.Format，用於格式化文字。

**noDiff**  — 抑制差異輸出的計算，即使存在差異資訊。

**標籤類別**  — 將包圍非空白輸出的元素的CSS類別名稱。 如果留空，則不會新增任何元素。

**tagName**  — 將包圍非空白輸出的元素名稱。 其預設值為DIV。

**預留位置**  — 在編輯模式下用於空或空白文字的預設值，也就是預留位置。 預設檢查會在選擇性格式化和逸出之後執行，即依照原樣寫入輸出。 其預設值為：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**預設**  — 用於空或空白文字的預設值。 預設檢查會在選擇性格式化和逸出之後執行，也就是說，會依原樣寫入輸出。

以下範例說明 `<cq:text>` 標籤可用於JSP中：

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

此 `<cq:setContentBundle>` 標籤會建立i18n本地化內容，並儲存在 `javax.servlet.jsp.jstl.fmt.localizationContext` 設定變數。

它具有下列屬性：

**語言**  — 要擷取資源套件的地區設定的語言。

**來源**  — 地區設定的來源位置。 它可以設定為下列其中一個值：

* **靜態**  — 地區設定取自 `language` 屬性（如果可用），否則從伺服器預設地區設定。

* **頁面**  — 地區設定會從目前頁面或資源的語言取得（如果有的話），否則會從 `language` 屬性（如果可用），否則從伺服器預設地區設定。

* **請求**  — 地區設定是從請求地區設定( `request.getLocale()`)。

* **自動**  — 地區設定取自 `language` 屬性（若有），否則會來自目前頁面的語言或資源（若有），否則會來自請求。

如果 `source` 屬性未設定：

* 如果 `language` 屬性已設定，則 `source` 屬性預設為&quot; `static`.

* 如果 `language` 屬性未設定， `source` 屬性預設為 `auto`.

「內容套件」可供標準JSTL使用 `<fmt:message>` 標籤之間。 依索引鍵查詢訊息有兩個方面：

1. 首先，系統搜尋轉譯之基礎資源的JCR屬性以取得翻譯。 這可讓您定義簡單元件對話方塊以編輯這些值。
1. 如果節點不包含名稱與索引鍵完全相同的屬性，則備援是從sling請求( `SlingHttpServletRequest.getResourceBundle(Locale)`)。 此套裝的語言或地區設定是由的語言和來源屬性所定義 `<cq:setContentBundle>` 標籤之間。

此 `<cq:setContentBundle>` 標籤的使用方式如下。

對於定義其語言的頁面：

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

針對使用者個人化頁面：

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

此 `<cq:include>` 標籤包含進入目前頁面的資源。

它具有下列屬性：

**排清**

* 布林值，定義在包含目標之前是否清除輸出。

**path**

* 要包含在目前要求處理中的資源物件的路徑。 如果此路徑是相對路徑，則會附加至目前資源的路徑，其指令碼包含指定的資源。 必須指定path和resourceType或指令碼。

**resourceType**

* 要包含的資源的資源型別。 如果設定了資源型別，路徑必須是資源物件的確切路徑：在這種情況下，不支援在路徑中新增引數、選擇器和副檔名。
* 如果要包含的資源是以無法解析為資源的路徑屬性指定的，則標籤可能會建立路徑及此資源型別之外的合成資源物件。
* 必須指定path和resourceType或指令碼。

**指令碼**

* 要包含的jsp指令碼。 必須指定path和resourceType或指令碼。

**ignoreComponentHierarchy**

* 此布林值會控制是否應忽略元件階層以進行指令碼解析。 如果為true，則僅遵循搜尋路徑。

**範例：**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

您是否應使用 `<%@ include file="myScript.jsp" %>` 或 `<cq:include script="myScript.jsp" %>` 是否要包含指令碼？

* 此 `<%@ include file="myScript.jsp" %>` 指示詞會通知JSP編譯器將完整的檔案加入目前的檔案中。 就好像所包含檔案的內容直接貼到原始檔案中一樣。
* 使用 `<cq:include script="myScript.jsp">` 標籤中，檔案會包含在執行階段中。

您是否應使用 `<cq:include>` 或 `<sling:include>`？

* 開發AEM元件時，Adobe建議您使用 `<cq:include>`.
* `<cq:include>` 可讓您在使用script屬性時直接依名稱包含指令檔。 這會將元件和資源型別繼承列入考量，且通常比使用選擇器和擴充功能嚴格遵守Sling的指令碼解析更簡單。

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 自AEM 5.6起已棄用。 [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 應該改用。

此 `<cq:includeClientLib>` tag包含AEM html使用者端資料庫，可以是js、css或主題資料庫。 對於不同型別的多個包含專案（例如js和css），此標籤必須在jsp中多次使用。 此標籤是便利的包裝函式，適用於 `com.day.cq.widget.HtmlLibraryManager` 服務介面。

它具有下列屬性：

**類別**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有JavaScript和CSS資料庫。 主題名稱會從請求中擷取。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**主題**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有主題相關資料庫（CSS和JS）。 主題名稱會從請求中擷取。

相當於： `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有JavaScript程式庫。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  — 以逗號分隔的使用者端程式庫類別清單。 這包括指定類別的所有CSS資料庫。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主題**  — 僅指示主題或非主題程式庫的標幟。 如果省略，則包含兩個集合。 僅適用於純JS或CSS includes （不適用於類別或主題包含）。

此 `<cq:includeClientLib>` 標籤的使用方式如下：

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineObjects> {#cq-defineobjects}

此 `<cq:defineObjects>` 標籤會公開以下定期使用的指令碼物件，以供開發人員參考。 它也會公開由定義的物件 [`<sling:defineObjects>`](#amp-lt-sling-defineobjects) 標籤之間。

**componentContext**

* 請求的目前元件內容物件(com.day.cq.wcm.api.components.ComponentContext介面)。

**元件**

* 目前資源的目前AEM元件物件(com.day.cq.wcm.api.components.Component interface)。

**currentDesign**

* 目前頁面的目前設計物件(com.day.cq.wcm.api.designer.Design介面)。

**currentpage**

* 目前的AEM WCM頁面物件(com.day.cq.wcm.api.Page介面)。

**目前樣式**

* 目前儲存格的目前樣式物件(com.day.cq.wcm.api.designer.Style介面)。

**設計工具**

* 用來存取設計資訊的設計工具物件(com.day.cq.wcm.api.designer.Designer介面)。

**editContext**

* AEM元件的編輯內容物件(com.day.cq.wcm.api.components.EditContext介面)。

**pageManager**

* 頁面層級作業的頁面管理員物件(com.day.cq.wcm.api.PageManager介面)。

**pageProperties**

* 目前頁面的頁面屬性物件(org.apache.sling.api.resource.ValueMap)。

**屬性**

* 目前資源的屬性物件(org.apache.sling.api.resource.ValueMap)。

**resourceDesign**

* 資源頁面的設計物件(com.day.cq.wcm.api.designer.Design介面)。

**resourcePage**

* 資源頁面物件(com.day.cq.wcm.api.Page介面)。
* 它具有下列屬性：

**requestname**

* 繼承自sling

**responseName**

* 繼承自sling

**resourceName**

* 繼承自sling

**nodeName**

* 繼承自sling

**logName**

* 繼承自sling

**resourceResolverName**

* 繼承自sling

**slingName**

* 繼承自sling

**componentContextName**

* 特定於wcm

**editContextname**

* 特定於wcm

**propertiesName**

* 特定於wcm

**pageManagerName**

* 特定於wcm

**currentPageName**

* 特定於wcm

**resourcePageName**

* 特定於wcm

**pagePropertiesName**

* 特定於wcm

**componentname**

* 特定於wcm

**designerName**

* 特定於wcm

**currentDesignName**

* 特定於wcm

**resourceDesignName**

* 特定於wcm

**currentStyleName**

* 特定於wcm

**範例**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中， `<cq:defineObjects />` 標籤會自動包含在內。

### &lt;cq:requestURL> {#cq-requesturl}

此 `<cq:requestURL>` 標籤會將目前的請求URL寫入JspWriter。 兩個標籤 [`<cq:addParam>`](#amp-lt-cq-addparam) 和 [`<cq:removeParam>`](#amp-lt-cq-removeparam) 和可用於此標籤內文中，在寫入前修改目前的請求URL。

它可讓您使用各種引數建立目前頁面的連結。 例如，這可讓您轉換請求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用 `addParam` 或 `removeParam` 只會變更指定引數的出現位置，所有其他引數則不受影響。

`<cq:requestURL>` 沒有任何屬性。

範例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

此 `<cq:addParam>` 標籤會將具有給定名稱和值的請求引數新增到結尾處 [`<cq:requestURL>`](#amp-lt-cq-requesturl) 標籤之間。

它具有下列屬性：

**名稱**

* 要新增的引數名稱

**值**

* 要新增之引數的值

**範例：**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

此 `<cq:removeParam>` 標籤會從結尾處移除具有指定名稱和值的請求引數 [`<cq:requestURL>`](#amp-lt-cq-requesturl) 標籤之間。 如果未提供值，則會移除具有指定名稱的所有引數。

它具有下列屬性：

**名稱**

* 要移除的引數名稱

範例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling標籤庫 {#sling-tag-library}

Sling標籤資料庫包含實用的Sling函式。

您在指令碼中使用Sling標籤庫時，指令碼必須以下列程式碼開頭：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中，則會自動宣告sling taglib。

### &lt;sling:include> {#sling-include}

此 `<sling:include>` 標籤包含進入目前頁面的資源。

它具有下列屬性：

**排清**

* 布林值，定義在包含目標之前是否清除輸出。

**resource**

* 要包含在目前要求處理中的資源物件。 必須指定資源或路徑。 如果同時指定兩者，則資源優先。

**path**

* 要包含在目前要求處理中的資源物件的路徑。 如果此路徑是相對路徑，則會附加至目前資源的路徑，其指令碼包含指定的資源。 必須指定資源或路徑。 如果同時指定兩者，則資源優先。

**resourceType**

* 要包含的資源的資源型別。 如果設定了資源型別，路徑必須是資源物件的確切路徑：在這種情況下，不支援在路徑中新增引數、選擇器和副檔名。
* 如果要包含的資源是以無法解析為資源的路徑屬性指定的，則標籤可能會建立路徑及此資源型別之外的合成資源物件。

**replaceSelectors**

* 分派時，選取器會取代為此屬性的值。

**addSelectors**

* 分派時，會將此屬性的值新增至選取器。

**replaceSuffix**

* 分派時，尾碼會由這個屬性的值取代。

>[!NOTE]
>
>資源的解析度以及隨附的指令碼 `<sling:include>` 標籤與一般sling URL解析度相同。 依預設，也會將目前請求中的選取器、擴充功能等用於包含的指令碼。 可透過標籤屬性來修改它們：例如， `replaceSelectors="foo.bar"` 可讓您覆寫選擇器。

範例：

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineObjects> {#sling-defineobjects}

此 `<sling:defineObjects>` 標籤會公開下列定期使用的指令碼物件，以供開發人員參考：

**slingRequest**

* SlingHttpServletRequest物件，可存取HTTP要求標題資訊（擴充標準HttpServletRequest），並可存取Sling特有專案，例如資源、路徑資訊和選取器。

**slingResponse**

* SlingHttpServletResponse物件，可存取伺服器所建立的HTTP回應。 這與它延伸的HttpServletResponse相同。**請求**
* 純HttpServletRequest的標準JSP要求物件。**回應**
* 標準JSP回應物件，純HttpServletResponse。

**resourceResolver**

* 目前的ResourceResolver物件。 它與slingRequest.getResourceResolver()相同

.**sling**

* SlingScriptHelper物件，包含方便使用的指令碼方法，主要是sling.include(&#39;/some/other/resource&#39;)，用於將其他資源的回應包含在此回應中（例如內嵌標題html片段）和sling.getService(foo.bar.Service.class)，以擷取Sling中可用的OSGi服務（類別標籤法取決於指令碼語言）。

**resource**

* 目前要處理的資源物件，視請求的URL而定。 它與slingRequest.getResource()相同。

**目前節點**

* 如果目前資源指向JCR節點（這通常是Sling中的情況），這可提供對Node物件的直接存取。 否則不會定義此物件。

**記錄**

* 提供SLF4J記錄器，用於從指令碼內登入Sling記錄系統，例如log.info（「執行我的指令碼」）。

* 它具有下列屬性：

**requestname**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**範例：**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL標籤庫 {#jstl-tag-library}

此 [JavaServer Pages Standard Tag Library](https://www.oracle.com/java/technologies/java-server-tag-library.html) 包含許多實用的標準標籤。 核心、格式和函式taglibs是由 `/libs/foundation/global.jsp` 如下列程式碼片段所示。

### /libs/foundation/global.jsp擷取 {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

匯入 `/libs/foundation/global.jsp` 檔案（如先前所述），您可以使用 `c`， `fmt` 和 `fn` 存取這些taglibs的前置詞。 JSTL的官方檔案可在以下網址取得： [Java™ EE 5教學課程 — JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
