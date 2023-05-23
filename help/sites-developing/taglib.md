---
title: 標籤庫
seo-title: Tag Libraries
description: Granite、CQ和Sling標籤庫使您能夠訪問特定函式，以在模板和元件的JSP指令碼中使用
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

# 標籤庫{#tag-libraries}

Granite、CQ和Sling標籤庫使您能夠訪問特定的函式，以便在模板和元件的JSP指令碼中使用。

## 花崗岩標籤庫 {#granite-tag-library}

Granite標籤庫包含有用的函式。

在開發Granite UI元件的jsp指令碼時，建議在指令碼頂部包含以下代碼：

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

全球同行還宣佈 [Sling庫](/help/sites-developing/taglib.md#sling-tag-library)。

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

的 `<ui:includeClientLib>` 標籤包AEM含html客戶端庫，它可以是js、css或主題庫。 對於不同類型的多個inclusion，例如js和css，需要在jsp中多次使用此標籤。 此標籤是包含 ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` 服務介面。

它具有以下屬性：

**類別**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有Javascript和CSS庫。 主題名稱從請求中提取。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**主題**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有主題相關庫（CSS和JS）。 主題名稱從請求中提取。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**j**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有Javascript庫。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**cs**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有CSS庫。

相當於： `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**主題**  — 應包括僅表示主題或非主題庫的標誌。 如果省略，則包括兩個集。 僅適用於純JS或CSS包括（不適用於類別或主題包括）。

的 `<ui:includeClientLib>` 標籤可在jsp中使用如下：

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

要在指令碼中使用CQ標籤庫，指令碼必須以以下代碼開頭：

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中，將自動聲明taglib。

開發元件的jsp腳AEM本時，建議在指令碼頂部包括以下代碼：

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

它聲明sling、CQ和jstl標籤，並公開由 [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) 標籤。 這縮短並簡化了元件的jsp代碼。

### &lt;cq:text> {#cq-text}

的 `<cq:text>` tag是在JSP中輸出元件文本的便利標籤。

它具有以下可選屬性：

**屬性**  — 要使用的屬性的名稱。 該名稱相對於當前資源。

**值**  — 用於輸出的值。 如果存在此屬性，則會覆蓋屬性屬性的使用。

**舊值**  — 用於差異輸出的值。 如果存在此屬性，則會覆蓋屬性屬性的使用。

**轉義Xml**  — 定義生成字串中的字元&lt;、>、&amp;、「和」是否應轉換為相應的字元實體代碼。 預設值為false。 請注意，轉義在可選格式設定後應用。

**格式**  — 用於設定文本格式的可選java.text.Format。

**無差異**  — 禁止計算差異輸出，即使存在差異資訊。

**標籤類**  — 將環繞非空輸出的元素的CSS類名。 如果為空，則不添加任何元素。

**標籤名稱**  — 將圍繞非空輸出的元素的名稱。 預設為DIV。

**佔位符**  — 在編輯模式（即佔位符）中用於null或空文本的預設值。 請注意，預設檢查是在可選格式設定和轉義後執行的，即按原樣寫入輸出。 預設為：

`<div><span class="cq-text-placeholder">&para;</span></div>`

**預設**  — 用於null或空文本的預設值。 請注意，預設檢查是在可選格式設定和轉義後執行的，即按原樣寫入輸出。

一些示例 `<cq:text>` 標籤可用於JSP:

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

的 `<cq:setContentBundle>` 標籤建立i18n本地化上下文並將其儲存在 `javax.servlet.jsp.jstl.fmt.localizationContext` 配置變數。

它具有以下屬性：

**語言**  — 要檢索資源包的區域設定的語言。

**源**  — 應從中獲取區域設定的源。 它可以設定為以下值之一：

* **靜態**  — 從 `language` 屬性（如果可用），否則從伺服器預設區域設定。

* **頁**  — 語言環境取自當前頁面或資源的語言（如果可用），否則取自 `language` 屬性（如果可用），否則從伺服器預設區域設定。

* **請求**  — 區域設定是從請求區域設定( `request.getLocale()`)。

* **自動**  — 從 `language` 屬性（如果可用），否則從當前頁或資源的語言（如果可用），否則從請求中。

如果 `source` 未設定屬性：

* 如果 `language` 屬性已設定， `source` 屬性預設值為「 `static`。

* 如果 `language` 屬性未設定， `source` 屬性預設值 `auto`。

標準JSTL可簡單使用「內容包」 `<fmt:message>` 標籤。 按鍵查找消息的方式有兩種：

1. 首先，搜索當前呈現的基礎資源的JCR屬性以查找翻譯。 這允許您定義一個簡單元件對話框來編輯這些值。
1. 如果節點不包含與鍵名完全相同的屬性，則回退是從sling請求載入資源包( `SlingHttpServletRequest.getResourceBundle(Locale)`)。 此捆綁包的語言或區域設定由的語言和源屬性定義 `<cq:setContentBundle>` 標籤。

的 `<cq:setContentBundle>` 標籤可在jsp中按如下方式使用。

對於定義其語言的頁面：

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

對於用戶個性化頁面：

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

的 `<cq:include>` 標籤包括當前頁中的資源。

它具有以下屬性：

**衝**

* 一個布爾值，用於定義是否在包括目標之前刷新輸出。

**路徑**

* 要包括在當前請求處理中的資源對象的路徑。 如果此路徑相對，則它將附加到其指令碼包含給定資源的當前資源的路徑。 必須指定path和resourceType或指令碼。

**資源類型**

* 要包括的資源的資源類型。 如果設定了資源類型，則路徑必須是資源對象的準確路徑：在這種情況下，不支援向路徑添加參數、選擇器和擴展。
* 如果要包括的資源是使用無法解析為資源的路徑屬性指定的，則標籤可以在路徑和此資源類型之外建立合成資源對象。
* 必須指定path和resourceType或指令碼。

**指令碼**

* 要包括的jsp指令碼。 必須指定path和resourceType或指令碼。

**ignoreComponentHierarchy**

* 一個布爾值，用於控制是否應忽略元件層次結構以進行指令碼解析。 如果為true，則只尊重搜索路徑。

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

您是否使用 `<%@ include file="myScript.jsp" %>` 或 `<cq:include script="myScript.jsp" %>` 要加入指令碼嗎？

* 的 `<%@ include file="myScript.jsp" %>` 指令通知JSP編譯器將一個完整檔案包含到當前檔案中。 就好像所包含檔案的內容被直接貼上到原始檔案中。
* 使用 `<cq:include script="myScript.jsp">` 標籤，檔案在運行時包含。

您是否使用 `<cq:include>` 或 `<sling:include>`?

* 開發組AEM件時，Adobe建議您使用 `<cq:include>`。
* `<cq:include>` 允許您在使用script屬性時按指令碼檔案的名稱直接包含指令碼檔案。 這會考慮元件和資源類型的繼承，並且通常比使用選擇器和擴展嚴格遵守Sling的指令碼解析更簡單。

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` 自5.6AEM以來已棄用。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) 應改為使用。

的 `<cq:includeClientLib>` 標籤包AEM括html客戶端庫，它可以是js、css或主題庫。 對於不同類型的多個inclusion，例如js和css，需要在jsp中多次使用此標籤。 此標籤是包含 `com.day.cq.widget.HtmlLibraryManager` 服務介面。

它具有以下屬性：

**類別**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有Javascript和CSS庫。 主題名稱從請求中提取。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**主題**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有主題相關庫（CSS和JS）。 主題名稱從請求中提取。

相當於： `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**j**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有Javascript庫。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**cs**  — 以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有CSS庫。

相當於： `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**主題**  — 應包括僅表示主題或非主題庫的標誌。 如果省略，則包括兩個集。 僅適用於純JS或CSS包括（不適用於類別或主題包括）。

的 `<cq:includeClientLib>` 標籤可在jsp中使用如下：

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

的 `<cq:defineObjects>` 標籤顯示以下經常使用的指令碼對象，這些對象可由開發人員引用。 它還顯示由 [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects) 標籤。

**元件上下文**

* 請求的當前元件上下文對象(com.day.cq.wcm.api.components.ComponentContext介面)。

**元件**

* 當前AEM資源的當前元件對象(com.day.cq.wcm.api.components.Component介面)。

**當前設計**

* 當前頁面的當前設計對象(com.day.cq.wcm.api.designer.Design介面)。

**當前頁**

* 當前AEMWCM頁對象(com.day.cq.wcm.api.Page介面)。

**當前樣式**

* 當前單元格的當前樣式對象(com.day.cq.wcm.api.designer.Style介面)。

**設計師**

* 用於訪問設計資訊(com.day.cq.wcm.api.designer.Designer介面)的designer對象。

**編輯上下文**

* 元件的編輯上AEM下文對象(com.day.cq.wcm.api.components.EditContext介面)。

**頁面管理器**

* 頁面級操作的頁面管理器對象(com.day.cq.wcm.api.PageManager介面)。

**頁屬性**

* 當前頁的頁屬性對象(org.apache.sling.api.resource.ValueMap)。

**屬性**

* 當前資源的屬性對象(org.apache.sling.api.resource.ValueMap)。

**資源設計**

* 資源頁的設計對象(com.day.cq.wcm.api.designer.Design介面)。

**資源頁**

* 資源頁對象(com.day.cq.wcm.api.Page介面)。
* 它具有以下屬性：

**請求名稱**

* 從吊具中遺傳

**響應名稱**

* 從吊具中遺傳

**資源名稱**

* 從吊具中遺傳

**節點名稱**

* 從吊具中遺傳

**日誌名稱**

* 從吊具中遺傳

**resourceResolverName**

* 從吊具中遺傳

**slingName**

* 從吊具中遺傳

**元件上下文名稱**

* 特定於wcm

**編輯上下文名稱**

* 特定於wcm

**屬性名稱**

* 特定於wcm

**pageManager名稱**

* 特定於wcm

**當前頁名**

* 特定於wcm

**資源頁名**

* 特定於wcm

**pagePropertiesName**

* 特定於wcm

**元件名稱**

* 特定於wcm

**設計器名稱**

* 特定於wcm

**當前設計名稱**

* 特定於wcm

**資源設計名稱**

* 特定於wcm

**當前樣式名稱**

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
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中， `<cq:defineObjects />` 標籤將自動包含。

### &lt;cq:requestURL> {#cq-requesturl}

的 `<cq:requestURL>` 標籤將當前請求URL寫入JspWriter。 這兩個標籤 [ `<cq:addParam>`](#amp-lt-cq-addparam) 和 [ `<cq:removeParam>`](#amp-lt-cq-removeparam) 並且可在此標籤的正文中使用，以在寫入當前請求URL之前對其進行修改。

它允許您建立指向當前頁面的連結，這些連結的參數不同。 例如，它使您能夠轉換請求：

`mypage.html?mode=view&query=something` 到 `mypage.html?query=something`.

使用 `addParam` 或 `removeParam` 僅更改給定參數的出現，所有其它參數均不受影響。

`<cq:requestURL>` 沒有任何屬性。

範例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

的 `<cq:addParam>` 標籤將具有給定名稱和值的請求參數添加到封閉 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 標籤。

它具有以下屬性：

**名稱**

* 要添加的參數的名稱

**值**

* 要添加的參數的值

**範例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

的 `<cq:removeParam>` 標籤從封閉中刪除具有給定名稱和值的請求參數 [ `<cq:requestURL>`](#amp-lt-cq-requesturl) 標籤。 如果未提供值，則刪除所有具有給定名稱的參數。

它具有以下屬性：

**名稱**

* 要刪除的參數的名稱

範例:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling標籤庫 {#sling-tag-library}

Sling標籤庫包含有用的Sling功能。

在指令碼中使用Sling Tag庫時，指令碼必須以以下代碼開頭：

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>當 `/libs/foundation/global.jsp` 檔案包含在指令碼中，sling taglib將自動聲明。

### &lt;sling:include> {#sling-include}

的 `<sling:include>` 標籤包括當前頁中的資源。

它具有以下屬性：

**衝**

* 一個布爾值，用於定義是否在包括目標之前刷新輸出。

**resource**

* 要包括在當前請求處理中的資源對象。 必須指定資源或路徑。 如果同時指定了這兩項，則資源優先。

**路徑**

* 要包括在當前請求處理中的資源對象的路徑。 如果此路徑相對，則它將附加到其指令碼包含給定資源的當前資源的路徑。 必須指定資源或路徑。 如果同時指定了這兩項，則資源優先。

**資源類型**

* 要包括的資源的資源類型。 如果設定了資源類型，則路徑必須是資源對象的準確路徑：在這種情況下，不支援向路徑添加參數、選擇器和擴展。
* 如果要包括的資源是使用無法解析為資源的路徑屬性指定的，則標籤可以在路徑和此資源類型之外建立合成資源對象。

**replaceSelectors**

* 調度時，選擇器將替換為此屬性的值。

**addSelectors**

* 調度時，此屬性的值將添加到選擇器中。

**replaceSuffix**

* 調度時，尾碼將替換為此屬性的值。

>[!NOTE]
>
>包含在 `<sling:include>` 標籤與普通sling URL解析度相同。 預設情況下，選擇器、擴展等。 當前請求中的指令碼也用於包含的指令碼。 可以通過標籤屬性修改這些屬性：例如 `replaceSelectors="foo.bar"` 允許您覆蓋選定器。

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

的 `<sling:defineObjects>` 標籤顯示以下經常使用的指令碼對象，這些對象可由開發人員引用：

**sling請求**

* SlingHttpServletRequest對象，提供對HTTP請求標頭資訊的訪問 — 擴展了標準的HttpServletRequest — 並提供對Sling特定內容的訪問，如資源、路徑資訊、選擇器等。

**sling響應**

* SlingHttpServletResponse對象，提供對伺服器建立的HTTP響應的訪問。 這當前與它擴展的HttpServletResponse相同。**請求**
* 標準JSP請求對象是純HttpServletRequest。**回應**
* 標準JSP響應對象，它是純HttpServletResponse。

**資源解析器**

* 當前ResourceResolver對象。 它與slingRequest.getResourceResolver()相同

.**吊**

* SlingScriptHelper對象，包含指令碼的方便方法，主要是sling.include(&#39;/some/other/resource&#39;)，用於包括此響應中其他資源的響應(例如 嵌入標頭html代碼段)和sling.getService(foo.bar.Service.class)，以檢索Sling（類表示法，具體取決於指令碼語言）中提供的OSGi服務。

**resource**

* 要處理的當前資源對象，具體取決於請求的URL。 它與slingRequest.getResource()相同。

**當前節點**

* 如果當前資源指向JCR節點（Sling中通常是這樣），則這將直接訪問Node對象。 否則，未定義此對象。

**日誌**

* 提供SLF4J記錄器，用於從指令碼內登錄到Sling日誌系統，例如 log.info（&quot;正在執行我的指令碼&quot;）。

* 它具有以下屬性：

**請求名稱**

**響應名稱**

**節點名稱**

1 **ogName resourceResolverName**

**slingName**

**範例:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL標籤庫 {#jstl-tag-library}

的 [JavaServer頁面標準標籤庫](https://www.oracle.com/technetwork/java/index-jsp-135995.html) 包含許多有用的標籤。 核心、格式和函式標語由 `/libs/foundation/global.jsp` 如以下代碼段所示。

### /libs/foundation/global.jsp的摘錄 {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

導入 `/libs/foundation/global.jsp` 檔案（如前所述），您可以使用 `c`。 `fmt` 和 `fn` 訪問這些目標的前置詞。 《聯合國貿易貿易協定》的正式檔案可查閱： [Java EE 5教程 — JavaServer頁面標準標籤庫](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)。
