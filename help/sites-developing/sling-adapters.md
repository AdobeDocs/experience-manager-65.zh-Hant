---
title: 使用 Sling 介面卡
seo-title: Using Sling Adapters
description: Sling提供了適配器模式，可方便地轉換實現可適配介面的對象
seo-description: Sling offers an Adapter pattern to conveniently translate objects that implement the Adaptable interface
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 13%

---

# 使用 Sling 介面卡{#using-sling-adapters}

[吊帶](https://sling.apache.org) 提供 [適配器模式](https://sling.apache.org/site/adapters.html) 方便地轉換實現 [適應性](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 。 此介面提供泛型 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 將對象轉換為作為參數傳遞的類類型的方法。

例如，要將資源對象轉換為相應的節點對象，您只需執行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## 使用案例 {#use-cases}

有以下使用情形：

* 獲取特定於實現的對象。

   例如，基於JCR的泛型實現 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 介面提供對基礎JCR的訪問 [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)。

* 需要傳遞內部上下文對象的對象的快捷方式建立。

   例如，基於JCR [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) 保存對請求的引用 [`JCR Session`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)，這反過來對於將基於該請求會話工作的許多對象是必需的，如 [`PageManager`](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 或 [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)。

* 服務的快捷方式。

   一個罕見的案例。 `sling.getService()` 也很簡單。

### 空返回值 {#null-return-value}

`adaptTo()` 可以返回null。

原因有多種，包括：

* 實現不支援目標類型
* 處理此情況的適配器工廠不處於活動狀態(例如 由於缺少服務引用)
* 內部條件失敗
* 服務不可用

您必須優雅地處理空小寫。 對於jsp渲染，如果jsp失敗將導致內容為空，則可以接受。

### 快取 {#caching}

為了提高效能，實現可以自由地快取從 `obj.adaptTo()` 呼叫。 如果 `obj` 相同，返回的對象相同。

此快取對所有 `AdapterFactory` 基於案例。

但是，沒有一般規則 — 對象可以是新實例或現有實例。 這意味著你不能依賴任何一種行為。 所以它很重要，特別是內部 `AdapterFactory`，在此場景中對象是可重用的。

### 它的工作原理 {#how-it-works}

有多種方法 `Adaptable.adaptTo()` 可以實現：

* 物體本身；實現方法本身並映射到特定對象。
* 按 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可映射任意對象。

   對象仍必須實現 `Adaptable` 介面必須擴展 [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (通過 `adaptTo` 呼叫中央適配器管理器)。

   這允許在 `adaptTo` 現有類的機制，例如 `Resource`。

* 兩者兼有。

對於第一種情況，javadoc可以說明 `adaptTo-targets` 是可能的。 但是，對於特定子類（如基於JCR的資源），通常不可能這樣做。 在後一種情況下， `AdapterFactory` 通常是捆綁包的私有類的一部分，因此不會在客戶端API中公開，也不會在javadocs中列出。 理論上，我們有可能 `AdapterFactory` 實現 [OSGi](/help/sites-deploying/configuring-osgi.md) 服務運行時並查看其「adaptables」（源和目標）配置，但不是將它們映射到彼此。 最後，這取決於內部邏輯，而這必須記錄在案。 因此，這個引用。

## 參考 {#reference}

### Sling {#sling}

[**資源**](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>如果這是基於JCR節點的資源或引用節點的JCR屬性。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">屬性</a></td>
   <td>如果這是基於JCR屬性的資源。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>如果這是基於JCR的資源（節點或屬性）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">地圖</a></td>
   <td>如果這是基於JCR節點的資源（或其他支援值映射的資源），則返回屬性的映射。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>如果屬性是基於JCR節點的資源（或其他資源支援值映射），則返回屬性的便於使用的映射。 還可以通過使用<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> （處理空大小寫等）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">繼承值映射</a></td>
   <td>擴展 <a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">值映射</a> 這允許在查找屬性時考慮資源層次。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">可修改值映射</a></td>
   <td>擴展 <a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">值映射</a>，允許您修改該節點上的屬性。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">輸入流</a></td>
   <td>返回檔案資源的二進位內容(如果這是基於JCR節點的資源，且節點類型為 <code>nt:file</code> 或 <code>nt:resource</code>;如果這是捆綁資源；檔案內容（如果這是檔案系統資源）或二進位JCR屬性資源的資料。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>返回資源的URL(如果是基於JCR節點的資源，則返回此節點的儲存庫URL;jar捆綁URL（如果這是捆綁資源）;檔案URL（如果這是檔案系統資源）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">檔案</a></td>
   <td>如果這是檔案系統資源。</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果此資源是指令碼（例如jsp檔案），則指令碼引擎將為其註冊sling。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>如果此資源是指令碼（例如jsp檔案），其中指令碼引擎使用sling註冊，或者這是servlet資源。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">字串</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">布爾型</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">龍</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">雙</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">日曆</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">字串[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">布爾[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">長[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">日曆[]</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值[]</a></td>
   <td>如果這是基於JCR屬性的資源（且值適合），則返回值。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">標籤資源</a></td>
   <td>如果這是基於JCR節點的資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">Page</a></td>
   <td>如果這是基於JCR的資源，而節點是 <code>cq:Page</code> 或 <code>cq:PseudoPage</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">Component</a></td>
   <td>如果這是 <code>cq:Component</code> 節點資源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">設計</a></td>
   <td>如果這是設計節點(<code>cq:Page</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">範本</a></td>
   <td>如果這是 <code>cq:Template</code> 節點資源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">藍圖</a></td>
   <td>如果這是 <code>cq:Template</code> 節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">資產</a></td>
   <td>如果這是dam:Asset節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">轉譯</a></td>
   <td>如果這是dam:Asset格式副本（nt：檔案，位於dam:Assert格式副本資料夾下）</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">標記</a></td>
   <td>如果這是 <code>cq:Tag</code> 節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">用戶管理器</a></td>
   <td>如果這是基於JCR的資源且用戶具有訪問UserManager的權限，則基於JCR會話。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權項目</a></td>
   <td>「可授權」是用戶和組的通用基介面。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a></td>
   <td>用戶是可驗證和模擬的特殊授權。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">簡單搜索</a></td>
   <td>如果資源是基於JCR的資源，則在資源(或使用setSearchIn())下搜索。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">工作流狀態</a></td>
   <td>給定頁/工作流負載節點的工作流狀態。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">複製狀態</a></td>
   <td>給定資源或其jcr:content子節點的複製狀態（首先選中）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">連接器資源</a></td>
   <td>如果是基於JCR節點的資源，則返回特定類型的適配連接器資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">設定</a></td>
   <td>如果這是 <code>cq:ContentSyncConfig</code> 節點資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">配置條目</a></td>
   <td>如果這低於 <code>cq:ContentSyncConfig</code> 節點資源。</td>
  </tr>
 </tbody>
</table>

[**資源解析器**](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">會話</a></td>
   <td>如果這是基於JCR的資源解析器（預設），則請求的JCR會話。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">元件管理器</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">資產管理器</a></td>
   <td>基於JCR會話，如果這是基於JCR的資源解析器。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">標籤管理器</a></td>
   <td>基於JCR會話，如果這是基於JCR的資源解析器。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">用戶管理器</a></td>
   <td>UserManager提供了對可授權對象（即用戶和組）的訪問和維護手段。 UserManager綁定到特定會話。
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權項目</a> </td>
   <td>當前用戶。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a><br /> </td>
   <td>當前用戶。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">查詢生成器</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">外部化器</a></td>
   <td>用於外部化絕對URL，即使沒有請求對象。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 調整為：

尚無目標，但實現了Adaptible，可以用作自定義AdapterFactory中的源。

[**SlingHttpServletResponse**](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">內容處理程式</a><br /> (XML)</td>
   <td>如果這是吊帶重寫器的回應。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[頁面](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>頁的資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">標籤資源</a></td>
   <td>已標籤資源（==此）。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>頁面的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>頁面資源可以適應的所有內容。</td>
  </tr>
 </tbody>
</table>

**[元件](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 調整為：

| [Resource](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 元件的資源。 |
|---|---|
| [標籤資源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 已標籤資源（==此）。 |
| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 元件的節點。 |
| ... | 元件的資源可以適應的所有內容。 |

**[模板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** 調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>模板的資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">標籤資源</a></td>
   <td>已標籤資源（==此）。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>此模板的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>模板資源可以適應的所有內容。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

**可授權**。 **用戶** 和 **組** 適應：

| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用戶/組主節點。 |
|---|---|
| [複製狀態](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 返回用戶/組主節點的複製狀態。 |

#### DAM {#dam}

**資產** 調整為：

| [Resource](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 資產的資源。 |
|---|---|
| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 資產的節點。 |
| ... | 該資產的所有資源都可以適應。 |

#### 標記 {#tagging}

**標籤** 調整為：

| [Resource](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 標籤的資源。 |
|---|---|
| [節點](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 標籤的節點。 |
| ... | 標籤的資源可以適應的所有內容。 |

#### 其他 {#other}

此外，Sling/JCR/OCM還提供 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` 用於自定義OCM([對象內容映射](https://jackrabbit.apache.org/object-content-mapping.html))對象。
