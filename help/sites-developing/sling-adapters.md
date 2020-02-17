---
title: 使用Sling適配器
seo-title: 使用Sling適配器
description: Sling提供Adapter模式，可方便轉譯實作Appative介面的物件
seo-description: Sling提供Adapter模式，可方便轉譯實作Appative介面的物件
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 使用Sling適配器{#using-sling-adapters}

[Sling](https://sling.apache.org) 提供Adapter [模式](https://sling.apache.org/site/adapters.html) ，可方便轉譯實作 [Appative](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) Interface的物件。 此介面提供一 [般的adpatTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 方法，可將物件轉換為作為引數傳遞的類別類型。

例如，要將資源對象轉換為相應的節點對象，您只需執行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## 使用案例 {#use-cases}

以下是使用案例：

* 取得實作專屬物件。

   例如，以JCR為基礎的通用介面實作可 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 提供對基礎JCR`的存 [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)取。

* 建立需要傳遞內部上下文對象的對象的快捷方式。

   例如，以JCR為基 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) 礎的參考會保留請求的引用 [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)，而許多將根據請求作業(如 [`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 或)運作的物件則需要此參考 [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)。

* 服務的捷徑。

   一個罕見的例 `sling.getService()` 子——也很簡單。

### 空返回值 {#null-return-value}

`adaptTo()` 可以返回null。

原因有多種，包括：

* 實作不支援目標類型
* 處理此情況的適配器工廠不活動(如 由於缺少服務引用)
* 內部條件失敗
* 服務不可用

請務必妥善處理空值大小寫。 對於jsp渲染，如果jsp失敗，則可能會導致內容為空，這是可接受的。

### 快取 {#caching}

為了改進效能，實現可自由快取從調用返回的 `obj.adaptTo()` 對象。 如果 `obj` 相同，則返回的對象相同。

此快取會針對所有基 `AdapterFactory` 礎案例執行。

但是，沒有一般規則——物件可以是新例項或現有例項。 這表示您無法依賴這兩種行為。 因此，在此場景中，物件可重 `AdapterFactory`復使用，這一點非常重要，尤其是在內部。

### 運作方式 {#how-it-works}

有多種可實 `Adaptable.adaptTo()` 施的方式：

* 物體本身；實現方法本身並映射到特定對象。
* By an [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)`, which can map artibure objects.

   對象仍必須實施接 `Adaptable` 口並且必須擴展 [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (這會將調 `adaptTo` 用傳遞給中央適配器管理器)。

   這允許將掛接 `adaptTo` 到現有類的機制中，如 `Resource`。

* 兩者的結合。

在第一種情況下，javadoc可以說明可 `adaptTo-targets` 能性。 但是，對於特定子類（如基於JCR的資源），通常不可能。 在後一種情況下，實 `AdapterFactory` 施通常是綁定的私有類的一部分，因此不在客戶端API中公開，也不列在javadoc中。 從理論上講，從 `AdapterFactory` OSGi [](/help/sites-deploying/configuring-osgi.md) service runtime訪問所有實現並查看其「適配器」（源和目標）配置是可能的，但不是將它們相互映射。 最後，這取決於內部邏輯，而內部邏輯必須加以記錄。 因此，這一參考。

## 引用 {#reference}

### Sling {#sling}

[**資源&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)適應：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>如果這是基於JCR節點的資源或引用節點的JCR屬性。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">屬性</a></td>
   <td>如果這是基於JCR屬性的資源。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>如果這是基於JCR的資源（節點或屬性）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">地圖</a></td>
   <td>如果這是基於JCR節點的資源（或其他資源支援值映射），則返回屬性的映射。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>如果屬性是基於JCR節點的資源（或其他資源支援值映射），則返回該屬性的方便使用映射。 也可以使用<br /> (控制 <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> 空大小寫等)來實現（更簡單）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>ValueMap的 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">擴充功能</a> ，可讓您在尋找屬性時，考慮資源階層。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/PersistableValueMap.html">PersistableValueMap</a></td>
   <td>如果這是基於JCR節點的資源，並且用戶有權修改該節點上的屬性。<br /> 注意：多個可持續地圖不共用其值。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>傳回「檔案」的二進位內容<code>nt:resource</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>AuthorizableResourceProvider</code><code>org.apache.sling.jackrabbit.usermanager</code><code>/system/userManager</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Page</code><code>cq:PseudoPage</code></td></tr><tr><td></td><td><code>cq:Component</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td><code>cq:Template</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Tag</code></td></tr><tr><td></td><td><code>cq:Preferences</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr></tbody></table>

[**資源解析器&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html)適用於：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">會話</a></td>
   <td>請求的JCR會話(如果這是基於JCR的資源解析器（預設）)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">設計人員</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>根據JCR會話，如果這是基於JCR的資源解析器。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>根據JCR會話，如果這是基於JCR的資源解析器。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>根據JCR會話，如果這是基於JCR的資源解析器，以及用戶是否具有訪問UserManager的權限。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授權項目</a> </td>
   <td>目前的使用者。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">使用者</a><br /> </td>
   <td>目前的使用者。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/privileges/PrivilegeManager.html">PrivilegeManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/Preferences.html">偏好設定</a></td>
   <td>當前用戶的首選項（如果這是基於JCR的資源解析器，則基於JCR會話）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/PreferencesService.html">PreferencesService</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/auth/pin/PinManager.html">PinManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">外置式</a></td>
   <td>用於外部化絕對URL，即使沒有請求物件亦然。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)適用於：

目標尚未定位，但實施了可適應性，可作為自定義AdapterFactory中的源。

[**SlingHttpServletResponse **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)適用於：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果這是吊索重寫回應。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

[**頁面&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)，可適應：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">資源</a><br /> </td>
   <td>頁面資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LakedResource</a></td>
   <td>標籤資源（==此）。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>頁面的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>頁面資源可調整的一切。</td>
  </tr>
 </tbody>
</table>

[**元件&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)適應：

| [資源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 元件的資源。 |
|---|---|
| [LakedResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 標籤資源（==此）。 |
| [節點](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 元件的節點。 |
| ... | 元件資源可適應的所有內容。 |

[**範本&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)適應：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">資源</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /></a></td>
   <td>範本的資源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LakedResource</a></td>
   <td>標籤資源（==此）。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">節點</a></td>
   <td>此模板的節點。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>範本資源可以調整的一切。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

[**可授權&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Authorizable.html)、使[**用者**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/User.html) 和 [**群組&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Group.html)，可調整：

| [節點](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用戶／組主節點。 |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 返回用戶／組主節點的複製狀態。 |

#### DAM {#dam}

[**資產適應&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html):

| [資源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 資產的資源。 |
|---|---|
| [節點](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 資產的節點。 |
| ... | 資產資源可以適應的所有項目。 |

#### 標記 {#tagging}

[**標籤&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html)適應：

| [資源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 標籤的資源。 |
|---|---|
| [節點](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 標籤的節點。 |
| ... | 標籤資源可以適應的一切。 |

#### 其他 {#other}

此外，Sling / JCR / OCM也提供自訂 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` OCM(物件內[容對應](https://jackrabbit.apache.org/object-content-mapping.html))物件。
