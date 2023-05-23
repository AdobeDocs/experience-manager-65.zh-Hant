---
title: 擴展搜索功能
description: 擴展的搜索功能 [!DNL Adobe Experience Manager Assets] 超出違約範圍。
contentOwner: AG
role: Developer
feature: Search
exl-id: 9e33d1c0-232b-458a-ad6a-f595aa541a5a
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 19%

---

# 擴展資產搜索 {#extending-assets-search}

可以擴展 [!DNL Adobe Experience Manager Assets] 搜索功能。 出局了， [!DNL Experience Manager Assets] 按字串搜索資產。

搜索通過QueryBuilder介面完成，因此可以使用多個謂詞自定義搜索。 可以覆蓋以下目錄中的預設謂詞集： `/apps/dam/content/search/searchpanel/facets`。

您還可以向 [!DNL Assets] 管理面板。

>[!CAUTION]
>
>截至 [!DNL Experience Manager] 6.4，不建議使用經典UI。 Adobe建議使用啟用觸摸的UI。 有關自定義，請參見 [搜索小面](/help/assets/search-facets.md)。

## 覆蓋 {#overlaying}

要覆蓋預配置謂詞，請複製 `facets` 節點 `/libs/dam/content/search/searchpanel` 至 `/apps/dam/content/search/searchpanel/` 或指定其他 `facetURL` 屬性 `searchpanel` 配置(預設為 `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`)。

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>預設情況下，位於 `/apps` 不存在，因此建立它。 確保節點類型與下面 `/libs`。

## 添加頁籤 {#adding-tabs}

通過在 [!DNL Assets] 管理介面。 要建立其他頁籤：

1. 建立資料夾結構 `/apps/wcm/core/content/damadmin/tabs,`如果尚不存在，並複製 `tabs` 節點 `/libs/wcm/core/content/damadmin` 然後貼上。
1. 根據需要建立和配置第二個頁籤。

   >[!NOTE]
   >
   >當您建立 `siteadminsearchpanel`，確保設定 `id` 屬性以防止窗體衝突。

## 建立自定義謂語 {#creating-custom-predicates}

[!DNL Assets] 附帶一組預定義謂詞，可用於自定義資產共用頁。 以此方式自定義資產份額的內容 [建立和配置資產共用頁](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)。

除了使用預先存在的謂語， [!DNL Experience Manager] 開發人員也可以使用 [查詢生成器API](/help/sites-developing/querybuilder-api.md)。

建立自定義謂詞需要有關 [小部件框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)。

最佳做法是複製現有謂詞並調整它。 示例謂詞位於 **/libs/cq/search/components/謂語**。

### 示例：生成簡單屬性謂詞 {#example-build-a-simple-property-predicate}

要生成屬性謂詞，請執行以下操作：

1. 在項目目錄中建立元件資料夾，例如 **/apps/weretail/components/titlepredates**。
1. 添加 **內容.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 新增 `titlepredicate.jsp`.

   ```java
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. 若要讓元件可用，您必須能夠加以編輯。若要讓元件可編輯，請在CRXDE中新增主要類型 **cq:EditConfig的節點cq:editConfig******。為了能夠移除段落，請新增多值屬性 **cq:actions** ，其中單一值 **為DELETE**。
1. 導航到瀏覽器，並在示例頁面上(例如， **press.html**)切換到設計模式，並啟用謂詞段落系統的新元件(例如， **左**)。

1. 在 **編輯** 模式下，新元件現在可在sidekick中使用(在 **搜索** 組)。 在 **謂語** 並鍵入搜索詞，例如， **菱形** 然後按一下放大鏡開始搜索。

   >[!NOTE]
   >
   >搜索時，請確保準確鍵入術語，包括正確的大小寫。

### 示例：生成簡單組謂詞 {#example-build-a-simple-group-predicate}

要生成組謂詞，請執行以下操作：

1. 在項目目錄中建立元件資料夾，例如 **/apps/weretail/components/picspredicat**。
1. 添加 **內容.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 添加 **titlepredicate.jsp**:

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. 若要讓元件可用，您必須能夠加以編輯。若要讓元件可編輯，請在CRXDE中新增主要類型 **cq:EditConfig的節點cq:editConfig******。為了能夠移除段落，請新增多值屬性 **cq:actions** ，其中單一值 **為DELETE**。
1. 導航到瀏覽器，並在示例頁面上(例如， **press.html**)切換到設計模式，並啟用謂詞段落系統的新元件(例如， **左**)。
1. 在 **編輯** 模式下，新元件現在可在sidekick中使用(在 **搜索** 組)。 在 **謂語** 的雙曲餘切值。

## 已安裝的謂詞小部件 {#installed-predicate-widgets}

以下謂詞可用作預配置的ExtJS小部件。

### 全文謂詞 {#fulltextpredicate}

| 屬性 | 類型 | 說明 |
|---|---|---|
| 謂詞名稱 | 字串 | 謂詞的名稱。 預設為 `fulltext` |
| 搜索回調 | 函數 | 用於觸發事件搜索的回調 `keyup`。 預設為 `CQ.wcm.SiteAdmin.doSearch` |

### 屬性謂詞 {#propertypredicate}

| 屬性 | 類型 | 說明 |
|---|---|---|
| 謂詞名稱 | 字串 | 謂詞的名稱。 預設為 `property` |
| 屬性名稱 | 字串 | JCR屬性的名稱。 預設為 `jcr:title` |
| defaultValue | 字串 | 預填充的預設值。 |

### 路徑謂詞 {#pathpredicate}

| 屬性 | 類型 | 說明 |
|---|---|---|
| 謂詞名稱 | 字串 | 謂詞的名稱。 預設為 `path` |
| 根路徑 | 字串 | 謂詞的根路徑。 預設為 `/content/dam` |
| pathFieldPredicateName | 字串 | 預設為 `folder` |
| showFlatOption | 布林值 | 要顯示複選框的標誌 `search in subfolders`。 預設為true。 |

### 日期謂詞 {#datepredicate}

| 屬性 | 類型 | 說明 |
|---|---|---|
| 謂詞名稱 | 字串 | 謂詞的名稱。 預設為 `daterange` |
| 屬性名稱 | 字串 | JCR屬性的名稱。 預設為 `jcr:content/jcr:lastModified` |
| defaultValue | 字串 | 預填充預設值 |

### 選項謂詞 {#optionspredicate}

| 屬性 | 類型 | 說明 |
|---|---|---|
| 標題 | 字串 | 添加附加的頂級標題 |
| 謂詞名稱 | 字串 | 謂詞的名稱。 預設為 `daterange` |
| 屬性名稱 | 字串 | JCR屬性的名稱。 預設為 `jcr:content/metadata/cq:tags` |
| 崩潰 | 字串 | 折疊級別。 預設為 `level1` |
| 觸發器搜索 | 布林值 | 用於在檢查時觸發搜索的標誌。 預設為false |
| 搜索回調 | 函數 | 回調以觸發搜索。 預設為 `CQ.wcm.SiteAdmin.doSearch` |
| 搜索超時時間 | 數字 | 觸發searchCallback之前超時。 預設為800毫秒 |

## 自定義搜索結果 {#customizing-search-results}

「資產共用」頁面上搜索結果的顯示由所選鏡頭控制。 [!DNL Experience Manager Assets] 附帶一組預定義的鏡頭，可用於自定義資產共用頁面。 以此方式自定義資產份額的內容 [「建立和配置資產共用」頁](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)。

除了使用現有的鏡片， [!DNL Experience Manager] 開發商也可以自己製作鏡片。
