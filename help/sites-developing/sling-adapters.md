---
title: 使用 Sling 介面卡
description: Sling提供轉接器模式，可方便翻譯實作轉接器介面的物件
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# 使用 Sling 介面卡{#using-sling-adapters}

[Sling](https://sling.apache.org) 提供 [介面卡模式](https://sling.apache.org/documentation/the-sling-engine/adapters.html) 方便翻譯實作 [可調整](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 介面。 此介面提供了一般 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 將物件轉譯成作為引數傳遞的類別型別的方法。

例如，若要將Resource物件轉譯為對應的Node物件，您只需執行下列動作即可：

```java
Node node = resource.adaptTo(Node.class);
```

## 使用案例 {#use-cases}

有以下使用案例：

* 取得實作特定的物件。

  例如，泛型的JCR型實作 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 介面提供對基礎JCR的存取權 [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* 需要傳遞內部前後關聯物件的物件的快速鍵建立。

  例如，以JCR為基礎 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) 保留對請求的 [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)，根據此請求工作階段工作的許多物件則需要這些資源，例如 [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) 或 [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html).

* 服務的捷徑。

  罕見情況 —  `sling.getService()` 也很簡單。

### 空值傳回值 {#null-return-value}

`adaptTo()` 傳回null。

原因有很多，包括：

* 實作不支援目標型別
* 處理此情況的介面卡工廠未啟用（例如，因為遺失服務參考）
* 內部條件失敗
* 服務無法使用

請務必謹慎處理Null案例。 對於jsp轉譯，如果會導致jsp失敗，那是可以接受的。

### 快取 {#caching}

為改善效能，實施可自由快取從傳回的物件 `obj.adaptTo()` 呼叫。 如果 `obj` 相同，則傳回的物件相同。

系統會針對所有使用者執行此快取 `AdapterFactory` 根據個案。

但是，沒有一般規則 — 物件可能是新例項或現有例項。 這表示您無法依賴任一行為。 因此，這很重要，尤其是在內部 `AdapterFactory`，表示此情境中可重複使用物件。

### 運作方式 {#how-it-works}

有多種方式可以 `Adaptable.adaptTo()` 可以實作：

* 物件本身；實作方法本身並對應至特定物件。
* 按 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可對應任意物件。

  物件仍必須實作 `Adaptable` 介面且必須擴充 [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (會傳遞 `adaptTo` 呼叫中央介面卡管理員)。

  這可讓連結至 `adaptTo` 現有類別的機制，例如 `Resource`.

* 兩者的組合。

對於第一種情況，Java™檔案可以說明 `adaptTo-targets` 是可能的。 然而，對於特定子類別（例如JCR型資源），通常無法執行此操作。 在後一種情況下，實施 `AdapterFactory` 通常是套件私用類別的一部分，因此不會顯示在使用者端API中，也不會列在Java™檔案中。 理論上來說，您可以存取 `AdapterFactory` 來自的實作 [osgi](/help/sites-deploying/configuring-osgi.md) 服務執行階段並檢視其「可調整性」（來源和目標）設定，但不會相互對應。 最後，這取決於內部邏輯，這必須記錄在案。 因此，請參閱此參考檔案。

## 參考 {#reference}

### Sling {#sling}

[**資源**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) 可調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>如果這是以JCR節點為基礎的資源，或參照節點的JCR屬性。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">屬性</a></td>
   <td>如果這是JCR屬性型資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>如果這是JCR型資源（節點或屬性）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">地圖</a></td>
   <td>如果這是JCR節點型資源（或其他支援值的資源對應），則傳回屬性的對應</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">值圖</a></td>
   <td>如果這是JCR節點型資源（或其他支援值的資源對應），則傳回方便使用的屬性對應。 也可使用（更簡單）達成<br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> （處理null大小寫等）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>延伸 <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">值圖</a> 這允許在尋找屬性時考慮資源的階層</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>的延伸 <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">值圖</a>，可讓您修改該節點上的屬性</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">輸入資料流</a></td>
   <td>傳回檔案資源的二進位內容(如果這是JCR節點型資源，且節點型別為 <code>nt:file</code> 或 <code>nt:resource</code>；若為套件資源；若為檔案系統資源，則為檔案內容)或二進位JCR屬性資源的資料</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>傳回資源的URL （如果這是JCR節點型資源，則傳回此節點的存放庫URL；如果這是套件資源，則傳回jar套件URL；如果這是檔案系統資源，則傳回檔案URL）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">檔案</a></td>
   <td>如果這是檔案系統資源</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果此資源是指令碼（例如jsp檔案），其指令碼引擎已向sling註冊</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>如果此資源是向sling註冊指令碼引擎的指令碼（例如jsp檔案），或如果這是servlet資源。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">字串</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">布林值</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">長</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">兩次</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">行事曆</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">布林值[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">行事曆[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>如果這是JCR屬性型資源（且值符合），則傳回值。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>如果這是JCR節點型資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html">頁面</a></td>
   <td>如果這是JCR節點型資源，且節點為 <code>cq:Page</code> (或 <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html">元件</a></td>
   <td>如果這是 <code>cq:Component</code> 節點資源</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Design.html">設計</a></td>
   <td>如果這是設計節點(<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html">範本</a></td>
   <td>如果這是 <code>cq:Template</code> 節點資源</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">藍圖</a></td>
   <td>如果這是 <code>cq:Template</code> 節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Asset.html">資產</a></td>
   <td>如果這是dam：Asset節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Rendition.html">轉譯</a></td>
   <td>如果這是dam：Asset轉譯（nt：file，在dam：Assert的轉譯資料夾下）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/Tag.html">標記</a></td>
   <td>如果這是 <code>cq:Tag</code> 節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html">使用者管理員</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源，而且使用者有權存取UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權項目</a></td>
   <td>「可授權專案」是「使用者」和「群組」的共同基礎介面</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a></td>
   <td>使用者是可驗證及模擬的特殊可授權專案</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/SimpleSearch.html">Simplesearch</a></td>
   <td>在資源底下搜尋(如果這是JCR型資源，則使用setSearchIn())</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">工作流程狀態</a></td>
   <td>特定頁面/工作流程裝載節點的工作流程狀態</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html">復寫狀態</a></td>
   <td>指定資源或其jcr：content子節點的復寫狀態（請先核取）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/connector/ConnectorResource.html">聯結器資源</a></td>
   <td>如果這是JCR節點型資源，則傳回適合特定型別的聯結器資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">設定</a></td>
   <td>如果這是 <code>cq:ContentSyncConfig</code> 節點資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果低於 <code>cq:ContentSyncConfig</code> 節點資源</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 可調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">工作階段</a></td>
   <td>請求的JCR工作階段（如果這是JCR型資源解析器） （預設）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">元件管理員</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Designer.html">設計工具</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/AssetManager.html">Assetmanager</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源解析程式</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/TagManager.html">標籤管理員</a></td>
   <td>根據JCR工作階段，如果這是JCR型資源解析程式</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">使用者管理員</a></td>
   <td>UserManager提供可授權物件（即使用者和群組）的存取權及維護方法。 UserManager繫結至特定工作階段
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權</a> </td>
   <td>目前使用者</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a><br /> </td>
   <td>目前使用者</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html">Querybuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>用於將絕對URL外部化，即使沒有請求物件亦然<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 可調整為：

尚未有目標，但實作可調整的，而且可以在自訂AdapterFactory中作為來源使用。

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 可調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果這是Sling重寫程式回應</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[頁面](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)** 可調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>頁面資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已標示的資源(==此)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>頁面節點</td>
  </tr>
  <tr>
   <td>...</td>
   <td>頁面資源可適應的所有內容</td>
  </tr>
 </tbody>
</table>

**[元件](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html)** 可調整為：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | 元件的資源。 |
|---|---|
| [LabeledResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html) | 已標示的資源(==此)。 |
| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 元件的節點。 |
| ... | 元件資源可適應的所有專案。 |

**[範本](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html)** 可調整為：

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">資源</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>範本的資源</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已標示的資源(==此)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>此範本的節點</td>
  </tr>
  <tr>
   <td>...</td>
   <td>可調整範本資源的所有內容。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

**可授權**， **使用者和 **群組** 適應：

| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 傳回使用者/群組主節點。 |
|---|---|
| [復寫狀態](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html) | 傳回使用者/群組主節點的復寫狀態。 |

#### DAM {#dam}

**資產** 可調整為：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | 資產的資源。 |
|---|---|
| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 資產的節點。 |
| ... | 資產資源可適應的所有內容。 |

#### 標記 {#tagging}

**標籤** 可調整為：

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | 標籤的資源。 |
|---|---|
| [節點](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 標籤的節點。 |
| ... | 標籤的資源可適應的所有內容。 |

#### 其他 {#other}

此外，Sling / JCR / OCM也提供 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` 自訂OCM ([物件內容對應](https://jackrabbit.apache.org/jcr/object-content-mapping.html))物件。
