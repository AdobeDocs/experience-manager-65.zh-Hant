---
title: 標籤程式庫
seo-title: Tag Libraries
description: Granite、CQ和Sling標籤程式庫可讓您存取特定函式，以便用於範本和元件的JSP指令碼中
seo-description: The Granite, CQ, and Sling tag libraries give you access to specific functions for use in the JSP script of your templates and components
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: de5eb53f6160991ca0718d61afaeed2078a4fa88
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 0%

---

# 標籤程式庫{#tag-libraries}

Granite、CQ和Sling標籤程式庫可讓您存取特定函式，以便用於範本和元件的JSP指令碼中。

## Granite標籤程式庫 {#granite-tag-library}

Granite標籤程式庫包含實用的函式。

開發Granite UI元件的jsp指令碼時，建議在指令碼頂端包含下列程式碼：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

全球同時聲明 [Sling程式庫](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

此 `<ui:includeClientLib>` 標籤包含AEM html用戶端程式庫，可以是js、css或主題程式庫。 對於不同類型的多個包含（例如js和css），此標籤需要在jsp中使用多次。 此標籤是 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 服務介面。

它具有以下屬性：

**類別**  — 逗號分隔的客戶端庫類別的清單。 這會包含指定類別的所有Javascript和CSS程式庫。 主題名稱會從請求中擷取。

等同於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**主題**  — 逗號分隔的客戶端庫類別的清單。 這將包含指定類別的所有主題相關程式庫（包括CSS和JS）。 主題名稱會從請求中擷取。

等同於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  — 逗號分隔的客戶端庫類別的清單。 這會包含指定類別的所有Javascript程式庫。

等同於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**cs**  — 逗號分隔的客戶端庫類別的清單。 這會包含指定類別的所有CSS程式庫。

等同於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主題**  — 應包含僅表示主題或非主題圖書館的旗標。 若省略，則會包含這兩個集。 僅適用於純JS或CSS包含（不適用於類別或主題包含）。

此 `<ui:includeClientLib>` 標籤在jsp中可如下使用：

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

## CQ標籤程式庫 {#cq-tag-library}

CQ標籤程式庫包含實用的函式。

若要在指令碼中使用CQ標籤程式庫，指令碼必須以下列程式碼開頭：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中，則會自動宣告taglib。

開發AEM元件的jsp指令碼時，建議在指令碼頂部包括以下代碼：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它會宣告Sling、CQ和jstl taglibs，並公開由 [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) 標籤。 這樣可縮短並簡化元件的jsp代碼。

### &lt;cq:text> {#cq-text}

此 `<cq:text>` 標籤是一種方便標籤，可在JSP中輸出元件文本。

它有下列選用屬性：

**屬性**  — 要使用的屬性名稱。 名稱是相對於目前資源。

**value**  — 用於輸出的值。 如果此屬性存在，則會覆寫屬性的使用。

**oldValue**  — 用於差異輸出的值。 如果此屬性存在，則會覆寫屬性的使用。

**escapeXml**  — 定義是否應將產生的字串中的字元&lt;、>、&amp;、&#39;和&quot;轉換為其對應的字元實體代碼。 預設值為false。 請注意，逸出會在選用的格式設定後套用。

**格式**  — 可選的java.text.Format，用於格式化文本。

**noDiff**  — 隱藏比較輸出的計算，即使存在差異資訊亦然。

**tagClass**  — 將包圍非空白輸出的元素的CSS類別名稱。 如果空白，則不會新增任何元素。

**tagName**  — 將包圍非空輸出的元素名稱。 預設為DIV。

**預留位置**  — 用於編輯模式（即佔位符）中空或空文本的預設值。 請注意，預設檢查是在可選的格式設定和逸出後執行，即按原樣寫入輸出。 預設值為：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**預設**  — 用於空或空文本的預設值。 請注意，預設檢查會在選用的格式設定和逸出後執行，亦即會依原樣寫入輸出。

以下範例說明 `<cq:text>` 標籤可用於JSP:

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

此 `<cq:setContentBundle>` 標籤會建立i18n本地化內容並將其儲存在 `javax.servlet.jsp.jstl.fmt.localizationContext` 設定變數。

它具有以下屬性：

**語言**  — 要為其檢索資源包的區域設定的語言。

**來源**  — 應從中獲取區域設定的源。 可設為下列其中一個值：

* **靜態**  — 取自 `language` 屬性（如果可用），否則從伺服器預設區域設定。

* **頁面**  — 語言環境取自當前頁面或資源的語言（如果可用），否則取自 `language` 屬性（如果可用），否則從伺服器預設區域設定。

* **請求**  — 區域設定取自請求區域設定( `request.getLocale()`)。

* **自動**  — 取自 `language` 屬性（若可用），否則來自目前頁面或資源的語言（若可用），否則來自請求。

若 `source` 屬性未設定：

* 若 `language` 屬性，則 `source` 屬性預設為&quot; `static`.

* 若 `language` 屬性未設定， `source` 屬性預設為 `auto`.

標準JSTL只能使用「內容套件」 `<fmt:message>` 標籤。 按鍵查閱的訊息為兩倍：

1. 首先，會搜尋目前呈現之基礎資源的JCR屬性以尋找翻譯。 這可讓您定義簡單元件對話方塊來編輯這些值。
1. 如果節點不包含與索引鍵完全相似的屬性，備援是從sling請求載入資源套件( `SlingHttpServletRequest.getResourceBundle(Locale)`)。 此捆綁的語言或地區由的語言和源屬性定義 `<cq:setContentBundle>` 標籤。

此 `<cq:setContentBundle>` 標籤在jsp中可以如下使用。

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

此 `<cq:include>` 標籤包含目前頁面中的資源。

它具有以下屬性：

**刷新**

* 一個布林值，定義是否在包括目標之前刷新輸出。

**路徑**

* 要包含在目前請求處理中的資源物件路徑。 如果此路徑是相對的，則會附加至目前資源的路徑，其指令碼包含指定資源。 必須指定path和resourceType或指令碼。

**resourceType**

* 要包括的資源的資源類型。 如果設定了資源類型，則路徑必須是資源對象的確切路徑：在此情況下，不支援將參數、選取器和擴充功能新增至路徑。
* 如果要包括的資源用無法解析為資源的路徑屬性指定，則標籤可以從路徑和此資源類型中建立合成資源對象。
* 必須指定path和resourceType或指令碼。

**指令碼**

* 要包括的jsp指令碼。 必須指定path和resourceType或指令碼。

**ignoreComponentHierarchy**

* 一個布林值，用於控制是否應忽略指令碼解析的元件層次。 如果為true，則只接受搜索路徑。

**範例:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

您應使用 `<%@ include file="myScript.jsp" %>` 或 `<cq:include script="myScript.jsp" %>` 來加入指令碼？

* 此 `<%@ include file="myScript.jsp" %>` 指令通知JSP編譯器將一個完整檔案包含到當前檔案中。 就像包含的檔案內容直接貼入原始檔案一樣。
* 使用 `<cq:include script="myScript.jsp">` 標籤時，檔案會包含在執行階段中。

您應使用 `<cq:include>` 或 `<sling:include>`?

* 開發AEM元件時，Adobe建議您使用 `<cq:include>`.
* `<cq:include>` 可讓您在使用指令碼屬性時，直接根據指令碼檔案的名稱包含指令碼檔案。 這會將元件和資源類型繼承納入考量，而且通常比使用選取器和擴充功能嚴格遵循Sling指令碼解析來得簡單。

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 自AEM 5.6起已過時。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 的值。

此 `<cq:includeClientLib>` 標籤包含AEM html用戶端程式庫，可以是js、css或主題程式庫。 對於不同類型的多個包含（例如js和css），此標籤需要在jsp中使用多次。 此標籤是 `com.day.cq.widget.HtmlLibraryManager` 服務介面。

它具有以下屬性：

**類別**  — 逗號分隔的客戶端庫類別的清單。 這會包含指定類別的所有Javascript和CSS程式庫。 主題名稱會從請求中擷取。

等同於： `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**主題**  — 逗號分隔的客戶端庫類別的清單。 這將包含指定類別的所有主題相關程式庫（包括CSS和JS）。 主題名稱會從請求中擷取。

等同於： `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  — 逗號分隔的客戶端庫類別的清單。 這會包含指定類別的所有Javascript程式庫。

等同於： `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**cs**  — 逗號分隔的客戶端庫類別的清單。 這會包含指定類別的所有CSS程式庫。

等同於： `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主題**  — 應包含僅表示主題或非主題圖書館的旗標。 若省略，則會包含這兩個集。 僅適用於純JS或CSS包含（不適用於類別或主題包含）。

此 `<cq:includeClientLib>` 標籤在jsp中可如下使用：

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

此 `<cq:defineObjects>` 標籤會公開下列經常使用的指令碼物件，供開發人員參考。 也會公開由 [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects) 標籤。

**componentContext**

* 請求的目前元件內容物件(com.day.cq.wcm.api.components.ComponentContext介面)。

**元件**

* 目前資源的目前AEM元件物件(com.day.cq.wcm.api.components.Component介面)。

**currentDesign**

* 目前頁面的目前設計物件(com.day.cq.wcm.api.designer.Design介面)。

**currentPage**

* 目前的AEM WCM頁面物件(com.day.cq.wcm.api.Page介面)。

**currentStyle**

* 目前儲存格的目前樣式物件(com.day.cq.wcm.api.designer.Style介面)。

**設計工具**

* 用於訪問設計資訊的設計器對象(com.day.cq.wcm.api.designer.Designer介面)。

**editContext**

* AEM元件的編輯內容物件(com.day.cq.wcm.api.components.EditContext介面)。

**pageManager**

* 頁面層級操作的頁面管理器物件(com.day.cq.wcm.api.PageManager介面)。

**pageProperties**

* 目前頁面的頁面屬性物件(org.apache.sling.api.resource.ValueMap)。

**屬性**

* 目前資源的屬性物件(org.apache.sling.api.resource.ValueMap)。

**resourceDesign**

* 資源頁的設計對象(com.day.cq.wcm.api.designer.Design介面)。

**resourcePage**

* 資源頁面物件(com.day.cq.wcm.api.Page介面)。
* 它具有以下屬性：

**requestName**

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

**editContextName**

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

**componentName**

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
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中， `<cq:defineObjects />` 標籤時，系統會自動加入。

### &lt;cq:requestURL> {#cq-requesturl}

此 `<cq:requestURL>` 標籤將當前請求URL寫入JspWriter。 兩個標籤 [ `<cq:addParam>`](#amp-lt-cq-addparam) 和 [ `<cq:removeParam>`](#amp-lt-cq-removeparam) 和可在此標籤內部使用，以在寫入前修改目前的要求URL。

它可讓您使用各種參數建立連結至目前頁面。 例如，它可讓您轉換請求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用 `addParam` 或 `removeParam` 只會變更指定參數的出現次數，其他所有參數都不會受到影響。

`<cq:requestURL>` 沒有任何屬性。

範例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

此 `<cq:addParam>` 標籤會將具有指定名稱和值的要求參數新增至外圍 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 標籤。

它具有以下屬性：

**名稱**

* 要新增的參數名稱

**值**

* 要新增之參數的值

**範例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

此 `<cq:removeParam>` 標籤會從包含的 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 標籤。 如果未提供值，則會移除所有具有指定名稱的參數。

它具有以下屬性：

**名稱**

* 要移除的參數名稱

範例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling標籤程式庫 {#sling-tag-library}

Sling標籤程式庫包含實用的Sling函式。

在指令碼中使用Sling Tag Library時，指令碼必須以下列程式碼開頭：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中，則會自動宣告sling taglib。

### &lt;sling:include> {#sling-include}

此 `<sling:include>` 標籤包含目前頁面中的資源。

它具有以下屬性：

**刷新**

* 一個布林值，定義是否在包括目標之前刷新輸出。

**resource**

* 要包含在目前請求處理中的資源物件。 必須指定資源或路徑。 如果同時指定，則資源優先。

**路徑**

* 要包含在目前請求處理中的資源物件路徑。 如果此路徑是相對的，則會附加至目前資源的路徑，其指令碼包含指定資源。 必須指定資源或路徑。 如果同時指定，則資源優先。

**resourceType**

* 要包括的資源的資源類型。 如果設定了資源類型，則路徑必須是資源對象的確切路徑：在此情況下，不支援將參數、選取器和擴充功能新增至路徑。
* 如果要包括的資源用無法解析為資源的路徑屬性指定，則標籤可以從路徑和此資源類型中建立合成資源對象。

**replaceSelectors**

* 發送時，選擇器將替換為此屬性的值。

**addSelectors**

* 在發送時，此屬性的值會新增至選取器。

**replaceSuffix**

* 發送時，尾碼將替換為此屬性的值。

>[!NOTE]
>
>包含在 `<sling:include>` 標籤與一般sling URL解析度相同。 依預設，選取器、擴充功能等。 來自目前要求的也會用於包含的指令碼。 可透過標籤屬性加以修改：例如 `replaceSelectors="foo.bar"` 可讓您覆寫選取器。

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

此 `<sling:defineObjects>` 標籤會公開下列經常使用的指令碼物件，供開發人員參考：

**slingRequest**

* SlingHttpServletRequest物件，提供HTTP要求標頭資訊的存取權 — 延伸標準HttpServletRequest — 並提供資源、路徑資訊、選取器等Sling專用項目的存取權。

**slingResponse**

* SlingHttpServletResponse物件，提供伺服器所建立HTTP回應的存取權。 這目前與其延伸的HttpServletResponse相同。**請求**
* 標準JSP請求對象，它是純HttpServletRequest。**回應**
* 標準JSP響應對象，它是純HttpServletResponse。

**resourceResolver**

* 目前的ResourceResolver物件。 它與slingRequest.getResourceResolver()相同

.**sling**

* SlingScriptHelper物件，包含指令碼的便利方法，主要是sling.include(&#39;/some/other/resource&#39;)，以包含此回應內其他資源的回應(例如 內嵌標題html片段)和sling.getService(foo.bar.Service.class)，以擷取Sling中可用的OSGi服務（類別標籤法，視指令碼語言而定）。

**資源**

* 要處理的目前資源物件，視請求的URL而定。 它與slingRequest.getResource()相同。

**currentNode**

* 如果目前資源指向JCR節點（Sling中通常為此情況），則可直接存取Node物件。 否則，此對象未定義。

**記錄**

* 提供SLF4J記錄器，以便從指令碼內記錄至Sling記錄系統，例如 log.info（&quot;正在執行我的指令碼&quot;）。

* 它具有以下屬性：

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**範例:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL標籤庫 {#jstl-tag-library}

此 [JavaServer Pages標準標籤庫](https://www.oracle.com/technetwork/java/index-jsp-135995.html) 包含許多有用的標準標籤。 核心、格式和函式標籤由 `/libs/foundation/global.jsp` 如下列程式碼片段所示。

### /libs/foundation/global.jsp的擷取 {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

匯入 `/libs/foundation/global.jsp` 檔案（如前所述），您可以使用 `c`, `fmt` 和 `fn` 訪問這些標籤的前置詞。 JSTL的正式檔案可在 [Java EE 5教學課程 — JavaServer Pages Standard標籤庫](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
