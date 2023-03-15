---
title: 轉譯和傳送
seo-title: Rendering and Delivery
description: 轉譯和傳送
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

# 轉譯和傳送{#rendering-and-delivery}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM內容可透過 [Sling預設Servlet](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 呈現 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 和其他格式。

這些現成可用的轉譯功能通常會依原樣執行存放庫並傳回內容。

AEM也透過Sling支援開發和部署自訂Sling轉譯器，以完全控制轉譯的結構和內容。

「內容服務預設轉譯器」可填補現成可用的Sling預設值與「自訂開發」之間的間隙，允許自訂和控制轉譯內容的許多方面，而不需開發。

下圖顯示內容服務的呈現。

![chlimage_1-15](assets/chlimage_1-15.png)

## 請求JSON {#requesting-json}

使用 **&lt;resource.caas span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />.[&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.][&lt;export-config span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />.json** 來要求JSON。]

<table>
 <tbody>
  <tr>
   <td>資源</td>
   <td>/content/entities下的實體資源<br /> 或 <br /> /content下的內容資源</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>可選</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG下找到的匯出設定<br /> <br /> 如果省略，則會套用預設匯出設定 </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>可選</strong><br /> <br /> Sling演算中使用的子項演算深度遞回</td>
  </tr>
 </tbody>
</table>

## 建立匯出設定 {#creating-export-configs}

可建立匯出設定以自訂JSON轉譯。

您可以在 */apps/mobileapps/caas/exportConfigs。*

| 節點名稱 | 配置的名稱（用於呈現選擇器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示「匯出設定」的屬性：

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
   <td>includeComponents</td>
   <td>字串[]</td>
   <td>包含所有內容</td>
   <td>sling:resourceType</td>
   <td>從JSON匯出中排除具有指定sling:resourceType之節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>字串[]</td>
   <td>排除無</td>
   <td>sling:resourceType</td>
   <td>僅包含指定sling:resourceType（來自JSON匯出）之節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>字串[]</td>
   <td>排除無</td>
   <td>屬性前置詞</td>
   <td>從JSON匯出中排除以指定前置詞開頭的屬性</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>字串[]</td>
   <td>排除無</td>
   <td>屬性名稱</td>
   <td>從JSON匯出中排除指定的屬性</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>字串[]</td>
   <td>包含所有內容</td>
   <td>屬性名稱</td>
   <td><p>if excludePropertyPrefixesset<br /> 這包括指定的屬性，儘管與所排除的前置詞匹配，</p> <p>else（忽略排除屬性）僅包含這些屬性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>字串[]</td>
   <td>包含所有內容</td>
   <td>子名稱</td>
   <td>從JSON匯出中排除指定的子項</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>字串[]<br /> <br /> </td>
   <td>排除無</td>
   <td>子名稱</td>
   <td>僅包含來自JSON匯出的指定子項，排除其他</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>字串[]<br /> <br /> </td>
   <td>不重新命名</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>使用替換項更名屬性</td>
  </tr>
 </tbody>
</table>

### 資源類型導出覆蓋 {#resource-type-export-overrides}

在 */apps/mobileapps/caas/exportConfigs。*

| 名稱 | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示屬性：

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
   <td>對於下列Sling資源類型，請勿傳回預設的CaaS json匯出。<br /> 將資源轉譯為，以傳回客戶json匯出；<br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### 現有內容服務匯出設定 {#existing-content-services-export-configs}

「內容服務」包括兩種匯出設定：

* 預設值（未指定配置）
* 頁面（轉譯網站頁面）

#### 預設匯出設定 {#default-export-configuration}

如果在請求的URI中指定了配置，則將應用內容服務預設導出配置。

&lt;resource>.caas[.&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON覆寫</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 頁面匯出設定 {#page-export-configuration}

此配置擴展了預設值，將子節點下的子節點分組。

&lt;site_page>.caas.page[.&lt;depth-int>].json

### 其他資源 {#additional-resources}

請參閱下列資源，了解「內容服務」中的其他主題：

* [開發模型](/help/mobile/administer-mobile-apps.md)
* [製作內容服務](/help/mobile/develop-content-as-a-service.md)
* [管理內容服務](/help/mobile/developing-content-services.md)
