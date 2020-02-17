---
title: 演算和傳送
seo-title: 演算和傳送
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 演算和傳送{#rendering-and-delivery}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

AEM內容可輕鬆透過 [Sling Default Servlets轉譯](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) ，以轉譯 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 和其他格式。

這些現成可用的呈現方式通常會沿儲存庫移動，並按原樣返回內容。

AEM透過Sling也支援開發和部署自訂sling轉譯器，以完全控制轉譯的架構和內容。

Content Services預設轉譯器可填補現成可用的Sling Defaults和自訂開發之間的空隙，允許自訂和控制轉譯內容的許多方面，毋需開發。

下圖顯示內容服務的轉換。

![chlimage_1-15](assets/chlimage_1-15.png)

## 請求JSON {#requesting-json}

使 **用&lt;RESOURCE.caas[。&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** to request JSON.

<table>
 <tbody>
  <tr>
   <td>資源</td>
   <td>/content/entities下的實體資源<br /> ，或 <br /> /content下的內容資源</td>
  </tr>
  <tr>
   <td>匯出設定</td>
   <td><p><strong>可選</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG下找到的匯出設定<br /><br /> ，若省略，則會套用預設匯出設定 </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>可選</strong><br /> SLING <br /> 深度遞回，可呈現子系，如Sling演算中所用</td>
  </tr>
 </tbody>
</table>

## 建立導出配置 {#creating-export-configs}

可建立匯出設定以自訂JSON轉譯。

您可以在 */apps/mobileapps/caas/exportConfigs下建立設定節點。*

| 節點名稱 | 配置的名稱（用於渲染選擇器） |
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
   <td>includeComponents</td>
   <td>String[]</td>
   <td>包含一切</td>
   <td>sling:resourceType</td>
   <td>從JSON匯出中排除具有指定sling:resourceType之節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>排除</td>
   <td>sling:resourceType</td>
   <td>僅包含指定sling:resourceType自JSON匯出之節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>排除</td>
   <td>屬性前置詞</td>
   <td>從JSON匯出排除以指定字首開頭的屬性</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>排除</td>
   <td>屬性名稱</td>
   <td>從JSON匯出排除指定的屬性</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>包含一切</td>
   <td>屬性名稱</td>
   <td><p>如果excludePropertyPrefixes set<br /> this includes specified properties，儘管與要排除的前置詞匹配，</p> <p>else（忽略排除屬性）僅包含這些屬性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>包含一切</td>
   <td>子名稱</td>
   <td>從JSON匯出排除指定的子系</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>String[]<br /> <br /> </td>
   <td>排除</td>
   <td>子名稱</td>
   <td>僅包含JSON匯出中指定的子系，排除其他</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>更名</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>使用替換項更名屬性</td>
  </tr>
 </tbody>
</table>

### 資源類型導出覆蓋 {#resource-type-export-overrides}

在 */apps/mobileapps/caas/exportConfigs下建立設定節點。*

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
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>對於下列sling資源類型，請勿傳回預設的CaaS json匯出。<br /><br /> 將資源轉譯為：以傳回客戶json匯出；&lt;資源&gt;。&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### 現有Content services匯出設定 {#existing-content-services-export-configs}

Content services包含兩種匯出組態：

* 預設值（未指定配置）
* 頁面（以呈現網站頁面）

#### 預設匯出設定 {#default-export-configuration}

如果在請求的URI中指定了配置，則將應用Content services預設導出配置。

&lt;RESOURCE>.caas[.&lt;DEPTH-INT>].json

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

&lt;SITE_PAGE>.caas.page[。&lt;DEPTH-INT>].json

### 其他資源 {#additional-resources}

請參閱以下資源，瞭解Content services中的其他主題：

* [開發模型](/help/mobile/models-in-repository.md)
* [編寫內容服務](/help/mobile/develop-content-as-a-service.md)
* [管理內容服務](/help/mobile/developing-content-services.md)

