---
title: 呈現和交付
seo-title: Rendering and Delivery
description: 呈現和交付
seo-description: null
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 7%

---

# 呈現和交付{#rendering-and-delivery}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

可AEM以通過 [Sling預設Servlet](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 呈現 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 等格式。

這些現成的呈現方式通常沿著儲存庫移動並按原樣返回內容。

通AEM過Sling，還支援開發和部署自定義Sling投標器以完全控制呈現的模式和內容。

Content Services預設呈現器填補了現成Sling Defaults和Custom Development之間的空白，允許定制和控制呈現內容的許多方面而不進行開發。

下圖顯示了內容服務的呈現。

![chlimage_1-15](assets/chlimage_1-15.png)

## 請求JSON {#requesting-json}

使用 **&lt;resource.caas span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />。[&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />。][&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.json** 請求JSON。]

<table>
 <tbody>
  <tr>
   <td>資源</td>
   <td>/content/entities下的實體資源<br /> 或 <br /> /content下的內容資源</td>
  </tr>
  <tr>
   <td>導出配置</td>
   <td><p><strong>可選</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG下找到的導出配置<br /> <br /> 如果省略，將應用預設導出配置 </p> </td>
  </tr>
  <tr>
   <td>深度 — 整型</td>
   <td><strong>可選</strong><br /> <br /> 用於繪製子項的深度遞歸</td>
  </tr>
 </tbody>
</table>

## 建立導出配置 {#creating-export-configs}

可以建立導出配置以自定義JSON呈現。

可以在下面建立配置節點 */apps/mobileapps/caas/exportConfigs。*

| 節點名稱 | 配置的名稱（用於呈現選擇器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示了導出配置的屬性：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>預設值（如果，未設定）</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>includeComponents（包括元件）</td>
   <td>字串[]</td>
   <td>包括所有</td>
   <td>sling:resourceType</td>
   <td>從JSON導出中排除具有指定sling:resourceType的節點的詳細資訊</td>
  </tr>
  <tr>
   <td>排除元件</td>
   <td>字串[]</td>
   <td>排除</td>
   <td>sling:resourceType</td>
   <td>僅包含指定sling:resourceType的節點的詳細資訊（來自JSON導出）</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>字串[]</td>
   <td>排除</td>
   <td>屬性前置詞</td>
   <td>排除從JSON導出中以指定前置詞開頭的屬性</td>
  </tr>
  <tr>
   <td>排除屬性</td>
   <td>字串[]</td>
   <td>排除</td>
   <td>屬性名稱</td>
   <td>從JSON導出中排除指定的屬性</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>字串[]</td>
   <td>包括所有</td>
   <td>屬性名稱</td>
   <td><p>if excludePropertyPrefixesset<br /> 這包括指定的屬性，儘管與被排除的前置詞匹配，</p> <p>else(忽略的排除屬性僅包括這些屬性</p> </td>
  </tr>
  <tr>
   <td>包括子項</td>
   <td>字串[]</td>
   <td>包括所有</td>
   <td>子名稱</td>
   <td>從JSON導出中排除指定的子項</td>
  </tr>
  <tr>
   <td>排除子項</td>
   <td>字串[]<br /> <br /> </td>
   <td>排除</td>
   <td>子名稱</td>
   <td>僅包括JSON導出中指定的子項，排除其他</td>
  </tr>
  <tr>
   <td>更名屬性</td>
   <td>字串[]<br /> <br /> </td>
   <td>更名</td>
   <td>&lt;actual_property_name&gt;。&lt;replacement_property_name&gt;</td>
   <td>使用替換項更名屬性</td>
  </tr>
 </tbody>
</table>

### 資源類型導出覆蓋 {#resource-type-export-overrides}

在下面建立配置節點 */apps/mobileapps/caas/exportConfigs。*

| 名稱 | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示了屬性：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>預設值（如果，未設定）</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>字串[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>對於以下sling資源類型，不要返回預設的CaaSjson導出。<br /> 通過將資源呈現為，返回客戶json導出；<br /> &lt;resource&gt;。&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### 現有Content Services導出配置 {#existing-content-services-export-configs}

Content Services包括兩種導出配置：

* 預設（未指定配置）
* 頁（用於呈現網站頁）

#### 預設導出配置 {#default-export-configuration}

如果在請求的URI中指定了配置，則將應用Content Services預設導出配置。

&lt;resource>.caa[。&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>排除屬性</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr：文本，文本<br /> jcr：標題，標題<br /> jcr：說明，說明<br /> jcr:lastModified,lastModified<br /> cq：標籤，標籤<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents（包括元件）</td>
   <td> </td>
  </tr>
  <tr>
   <td>排除元件</td>
   <td> </td>
  </tr>
  <tr>
   <td>包括子項</td>
   <td> </td>
  </tr>
  <tr>
   <td>排除子項</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON覆蓋</td>
   <td>基礎/元件/影像<br /> wcm/foundation/元件/影像<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 頁面導出配置 {#page-export-configuration}

此配置擴展了預設值，以包括子節點下的子節點分組。

&lt;site_page>.caas.page[。&lt;depth-int>].json

### 其他資源 {#additional-resources}

請參閱以下資源，瞭解Content Services中的其他主題：

* [開發模式](/help/mobile/administer-mobile-apps.md)
* [創作內容服務](/help/mobile/develop-content-as-a-service.md)
* [管理Content Services](/help/mobile/developing-content-services.md)
