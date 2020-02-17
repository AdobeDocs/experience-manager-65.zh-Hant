---
title: 標籤庫
seo-title: 標籤庫
description: Granite、CQ和Sling標籤庫可讓您存取特定函式，以用於範本和元件的JSP指令碼
seo-description: Granite、CQ和Sling標籤庫可讓您存取特定函式，以用於範本和元件的JSP指令碼
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 標籤庫{#tag-libraries}

Granite、CQ和Sling標籤庫可讓您存取特定函式，以用於範本和元件的JSP指令碼。

## Granite標籤庫 {#granite-tag-library}

Granite標籤庫包含實用的函式。

當您開發Granite UI元件的jsp指令碼時，建議在指令碼頂端加入下列程式碼：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

全域也會宣告 [Sling程式庫](/help/sites-developing/taglib.md#sling-tag-library)。

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

標 `<ui:includeClientLib>` 簽「包含AEM html用戶端程式庫」，可以是js、css或主題程式庫。 對於不同類型的多個包含項目（例如js和css），此標籤需要在jsp中多次使用。 此標籤是服務介面周圍的便利 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 包裝函式。

它具有以下屬性：

**類別** -逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有Javascript和CSS程式庫。 主題名稱會從請求中擷取。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**theme** —— 逗號分隔的客戶端庫類別清單。 這將包含指定類別的所有主題相關程式庫（CSS和JS）。 主題名稱會從請求中擷取。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** —— 逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有Javascript程式庫。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** —— 逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有CSS程式庫。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主題** -應包含僅表示主題或非主題圖書館的旗標。 若省略，則會包含這兩組資料。 僅適用於純JS或CSS包含（不適用於類別或主題包含）。

標 `<ui:includeClientLib>` 簽可在jsp中使用如下：

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

CQ標籤庫包含實用的函式。

若要在指令碼中使用CQ標籤庫，指令碼必須以下列程式碼開頭：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>當該文 `/libs/foundation/global.jsp` 件包含在指令碼中時，會自動聲明taglib。

當您開發AEM元件的jsp指令碼時，建議在指令碼頂端加入下列程式碼：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它會宣告sling、CQ和jstl taglibs，並公開由標籤定義的常用指令碼 [ 物 `<cq:defineObjects />`](#amp-lt-cq-defineobjects) 件。 如此可縮短並簡化元件的jsp程式碼。

### <cq:text> {#cq-text}

標 `<cq:text>` 記是便利的標籤，可在JSP中輸出元件文本。

它具有以下可選屬性：

**property** —— 要使用的屬性名稱。 名稱是相對於當前資源的。

**value** —— 用於輸出的值。 如果此屬性存在，則覆寫屬性的使用。

**oldValue** —— 用於比較輸出的值。 如果此屬性存在，則覆寫屬性的使用。

**escapeXml** —— 定義結果字串中的字元&lt;、>、&amp;、&#39;和&quot;是否應轉換為其對應的字元實體代碼。 預設值為false。 請注意，逸出符號會套用在選用格式設定之後。

**format** —— 用於設定文本格式的可選java.text.Format。

**noDiff** —— 隱藏比較輸出的計算，即使存在比較資訊也是如此。

**tagClass** —— 將包含非空白輸出之元素的CSS類別名稱。 如果為空白，則不會新增任何元素。

**tagName** —— 將包含非空輸出的元素名稱。 預設為DIV。

**placeholder** —— 用於編輯模式（即佔位符）中空文本的預設值。 請注意，預設檢查是在可選格式設定和逸出後執行的，即按原樣寫入輸出。 預設為：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** —— 用於空文本或空文本的預設值。 請注意，預設檢查是在可選格式設定後執行的，並逸出（即按原樣寫入輸出）。

有些範例 `<cq:text>` 說明如何在JSP中使用標籤：

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

### <cq:setContentBundle> {#cq-setcontentbundle}

標 `<cq:setContentBundle>` 簽會建立i18n本地化內容，並將它儲存在設定 `javax.servlet.jsp.jstl.fmt.localizationContext` 變數中。

它具有以下屬性：

**語言** -要為其檢索資源包的語言環境的語言。

**source** —— 應從中獲取地區設定的源。 它可設為下列其中一個值：

* **static** —— 語言環境取自屬性(如果可 `language` 用)，否則取自伺服器預設語言環境。

* **page** —— 語言環境取自當前頁面或資源的語言（如果可用），否則取自屬性（如果可用），否則取 `language` 自伺服器預設語言環境。

* **request** —— 區域設定取自請求區域設定( `request.getLocale()`)。

* **auto** —— 語言環境從屬性（如果可用）取 `language` 得，否則從當前頁或資源的語言（如果可用）取得，從請求取得。

如果未 `source` 設定屬性：

* 如果設 `language` 定了屬性，則屬 `source` 性預設為&#39;&#39; `static`。

* 如果未 `language` 設定屬性，則屬 `source` 性預設為 `auto`。

標準JSTL標籤可使用「內容包」 `<fmt:message>` 。 按鍵查閱的訊息是兩倍：

1. 首先，搜索當前呈現的基礎資源的JCR屬性以查找轉換。 這可讓您定義簡單的元件對話方塊來編輯這些值。
1. 如果節點不包含名稱完全類似金鑰的屬性，備援是從sling請求( `SlingHttpServletRequest.getResourceBundle(Locale)`)載入資源搭售。 此捆綁包的語言或區域設定由標籤的語言和源屬性定 `<cq:setContentBundle>` 義。

標 `<cq:setContentBundle>` 簽可在jsp中如下使用。

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

### <cq:include> {#cq-include}

標 `<cq:include>` 記將資源包含到當前頁中。

它具有以下屬性：

**flash**

* 一個布爾值，用於定義是否在包括目標之前刷新輸出。

**路徑**

* 要包含在當前請求處理中的資源對象的路徑。 如果此路徑是相對的，則會將其附加到指令碼包含給定資源的當前資源的路徑。 必須指定path和resourceType或指令碼。

**resourceType**

* 要包括的資源的資源類型。 如果設定了資源類型，則路徑必須是資源對象的確切路徑：在這種情況下，不支援將參數、選擇器和擴充功能新增至路徑。
* 如果要包含的資源是使用無法解析為資源的路徑屬性指定的，則標籤可以建立路徑外的合成資源對象和此資源類型。
* 必須指定path和resourceType或指令碼。

**指令碼**

* 要包含的jsp指令碼。 必須指定path和resourceType或指令碼。

**ignoreComponentHierarchy**

* 一個布爾值，控制是否應忽略元件層次以便指令碼解析。 如果為true，則只考慮搜索路徑。

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

您應使用或 `<%@ include file="myScript.jsp" %>` 加入 `<cq:include script="myScript.jsp" %>` 指令碼嗎？

* 該指 `<%@ include file="myScript.jsp" %>` 令通知JSP編譯器將一個完整檔案包含到當前檔案中。 就像所包含檔案的內容直接貼到原始檔案中一樣。
* 使用標 `<cq:include script="myScript.jsp">` 記時，檔案會包含在執行時期中。

您應使用 `<cq:include>` 還是 `<sling:include>`?

* 開發AEM元件時，Adobe建議您使用 `<cq:include>`。
* `<cq:include>` 允許您在使用指令碼屬性時直接按指令碼檔案的名稱包含指令碼檔案。 這會考慮元件與資源類型繼承，而且通常比使用選擇器與擴充功能嚴格符合Sling指令碼解析度更簡單。

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 已自AEM 5.6起停用。應 [ 該 `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 改用。

標 `<cq:includeClientLib>` 簽「包含AEM html用戶端程式庫」，可以是js、css或主題程式庫。 對於不同類型的多個包含項目（例如js和css），此標籤需要在jsp中多次使用。 此標籤是服務介面周圍的便利 `com.day.cq.widget.HtmlLibraryManager` 包裝函式。

它具有以下屬性：

**類別** -逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有Javascript和CSS程式庫。 主題名稱會從請求中擷取。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**theme** —— 逗號分隔的客戶端庫類別清單。 這將包含指定類別的所有主題相關程式庫（CSS和JS）。 主題名稱會從請求中擷取。

相當於：writeThemeInclude `com.day.cq.widget.HtmlLibraryManager#`

**js** —— 逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有Javascript程式庫。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** —— 逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有CSS程式庫。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主題** -應包含僅表示主題或非主題圖書館的旗標。 若省略，則會包含這兩組資料。 僅適用於純JS或CSS包含（不適用於類別或主題包含）。

標 `<cq:includeClientLib>` 簽可在jsp中使用如下：

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

### <cq:defineObjects> {#cq-defineobjects}

標 `<cq:defineObjects>` 簽會公開下列常用的指令碼物件，可供開發人員參考。 它還會公開由標籤定義的 [`<sling:defineObjects>`](#amp-lt-sling-defineobjects) 對象。

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

**設計師**

* 用於訪問設計資訊的設計器對象(com.day.cq.wcm.api.designer.Designer介面)。

**editContext**

* AEM元件的編輯上下文物件(com.day.cq.wcm.api.components.EditContext介面)。

**pageManager**

* 頁面層級作業的頁面管理器物件(com.day.cq.wcm.api.PageManager介面)。

**pageProperties**

* 目前頁面的頁面屬性物件(org.apache.sling.api.resource.ValueMap)。

**屬性**

* 目前資源的屬性物件(org.apache.sling.api.resource.ValueMap)。

**resourceDesign**

* 資源頁面的設計物件(com.day.cq.wcm.api.designer.Design介面)。

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

* wcm的特定

**editContextName**

* wcm的特定

**屬性名稱**

* wcm的特定

**pageManagerName**

* wcm的特定

**currentPageName**

* wcm的特定

**resourcePageName**

* wcm的特定

**pagePropertiesName**

* wcm的特定

**componentName**

* wcm的特定

**designerName**

* wcm的特定

**currentDesignName**

* wcm的特定

**resourceDesignName**

* wcm的特定

**currentStyleName**

* wcm的特定

**範例**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>當檔 `/libs/foundation/global.jsp` 案包含在指令碼中時，就會自 `<cq:defineObjects />` 動包含標籤。

### <cq:requestURL> {#cq-requesturl}

標 `<cq:requestURL>` 記將當前請求URL寫入JspWriter。 這兩個標 [ 記和 `<cq:addParam>`](#amp-lt-cq-addparam) ，可在此標籤 [`<cq:removeParam>`](#amp-lt-cq-removeparam) 的內文中使用，以在寫入之前修改目前的請求URL。

它可讓您建立包含各種參數之目前頁面的連結。 例如，它可讓您轉換請求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用或僅 `addParam` 更改 `removeParam` 給定參數的出現情況，則所有其它參數都不受影響。

`<cq:requestURL>` 沒有任何屬性。

範例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

標 `<cq:addParam>` 簽會將具有指定名稱和值的請求參數新增至封閉的 [ 標 `<cq:requestURL>`](#amp-lt-cq-requesturl) 簽。

它具有以下屬性：

**名稱**

* 要添加的參數的名稱

**值**

* 要添加的參數值

**範例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

標 `<cq:removeParam>` 記會從封閉的標籤中移除具有指定名稱和值的請求 [ 參 `<cq:requestURL>`](#amp-lt-cq-requesturl) 數。 如果未提供值，則會移除所有具有給定名稱的參數。

它具有以下屬性：

**名稱**

* 要刪除的參數的名稱

範例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling Tag Library {#sling-tag-library}

Sling標籤庫包含實用的Sling函式。

當您在指令碼中使用Sling Tag Library時，指令碼必須以下列程式碼開頭：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>當檔 `/libs/foundation/global.jsp` 案包含在指令碼中時，sling taglib會自動宣告。

### <sling:include> {#sling-include}

標 `<sling:include>` 記將資源包含到當前頁中。

它具有以下屬性：

**flash**

* 一個布爾值，用於定義是否在包括目標之前刷新輸出。

**資源**

* 要包含在當前請求處理中的資源對象。 必須指定資源或路徑。 如果同時指定了兩者，則資源優先。

**路徑**

* 要包含在當前請求處理中的資源對象的路徑。 如果此路徑是相對的，則會將其附加到指令碼包含給定資源的當前資源的路徑。 必須指定資源或路徑。 如果同時指定了兩者，則資源優先。

**resourceType**

* 要包括的資源的資源類型。 如果設定了資源類型，則路徑必須是資源對象的確切路徑：在這種情況下，不支援將參數、選擇器和擴充功能新增至路徑。
* 如果要包含的資源是使用無法解析為資源的路徑屬性指定的，則標籤可以建立路徑外的合成資源對象和此資源類型。

**replaceSelectors**

* 在調度時，選擇器將替換為此屬性的值。

**addSelectors**

* 在調度時，此屬性的值將添加到選擇器中。

**replaceSuffix**

* 調度時，尾碼將由此屬性的值替換。

>[!NOTE]
>
>標籤中包含的資源和指令碼的解析 `<sling:include>` 度與一般sling URL解析度相同。 依預設，選擇器、擴充功能等。 從目前的要求中，也會使用隨附的指令碼。 可透過標籤屬性來修改這些屬性：例如， `replaceSelectors="foo.bar"` 允許覆寫選擇器。

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

### <sling:defineObjects> {#sling-defineobjects}

標 `<sling:defineObjects>` 簽會公開下列常用的指令碼物件，可供開發人員參考：

**slingRequest**

* SlingHttpServletRequest物件，提供HTTP要求標頭資訊的存取權——擴充標準HttpServletRequest —— 並提供對Sling特定資源、路徑資訊、選擇器等的存取權。

**slingResponse**

* SlingHttpServletResponse物件，提供伺服器建立之HTTP回應的存取權。 這目前與其延伸的HttpServletResponse相同。**請求**
* 標準JSP請求對象，它是純HttpServletRequest。**回應**
* 標準JSP響應對象，它是純HttpServletResponse。

**resourceResolver**

* 當前ResourceResolver對象。 它與slingRequest.getResourceResolver()相同

.**sling**

* SlingScriptHelper物件，包含指令碼的便利方法，主要是sling.include(&#39;/some/other/resource&#39;)，以包含此回應內其他資源的回應(例如 內嵌html片段)和sling.getService(foo.bar.Service.class)，以擷取Sling中可用的OSGi服務（Class notation，視指令碼語言而定）。

**資源**

* 要處理的當前資源對象，具體取決於請求的URL。 它與slingRequest.getResource()相同。

**currentNode**

* 如果目前資源指向JCR節點（Sling中通常是這種情況），這可讓您直接存取Node物件。 否則，不定義此對象。

**日誌**

* 提供SLF4J Logger，以從指令碼登入Sling記錄系統，例如 log.info(&quot;Executing my script&quot;)。

* 它具有以下屬性：

**requestName**

**responseName**

**nodeName**

**logName resourceResolverName**

**slingName**

**範例:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL標籤庫 {#jstl-tag-library}

JavaServer [Pages標準標籤庫](https://www.oracle.com/technetwork/java/index-jsp-135995.html) (JavaServer Pages Standard Tag Library)包含許多有用的標準標籤。 核心、格式和函式標語由下列程式碼 `/libs/foundation/global.jsp` 片段中所定義。

### /libs/foundation/global.jsp的摘錄 {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

如前所述 `/libs/foundation/global.jsp` 匯入檔案後，您可以使用 `c`、 `fmt``fn` 和字首來存取這些標語。 JSTL的正式檔案可在 [Java EE 5教學課程- javaServer Pages標準標籤庫中取得](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)。
