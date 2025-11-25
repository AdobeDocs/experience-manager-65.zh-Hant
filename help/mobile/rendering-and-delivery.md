---
title: 呈現和傳遞
description: 瞭解如何透過Sling預設Servlet呈現Adobe Experience Manager內容以呈現JSON和其他格式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 5%

---

# 呈現和傳遞{#rendering-and-delivery}

{{ue-over-mobile}}

可透過[Sling預設Servlet](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)輕鬆轉譯Adobe Experience Manager (AEM)內容，以轉譯[JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering)和其他格式。

這些現成可用的轉譯通常會在存放庫中移動並按原樣傳回內容。

AEM也透過Sling支援開發和部署自訂Sling轉譯器，以完全控制轉譯的結構與內容。

Content Services Default Renderer可填補現成Sling預設和自訂開發之間的空白，讓您無需開發即可自訂和控制呈現內容的許多方面。

下圖顯示內容服務的轉譯。

![chlimage_1-15](assets/chlimage_1-15.png)

## 請求JSON {#requesting-json}

使用&#x200B;**&lt;RESOURCE.caas`[.<EXPORT-CONFIG][.&lt;DEPTH-INT&gt;]`.json**&#x200B;要求JSON。

<table>
 <tbody>
  <tr>
   <td>資源</td>
   <td>/content/entities<br />下的實體資源，或<br /> /content下的內容資源</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>選擇性</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br />下找到匯出設定。如果省略，則會套用預設匯出設定 </p> </td>
  </tr>
  <tr>
   <td>深度 — 整數</td>
   <td><strong>選擇性</strong><br /> <br />呈現子項的深度遞回，如Sling呈現中所用</td>
  </tr>
 </tbody>
</table>

## 建立匯出設定 {#creating-export-configs}

可建立匯出設定來自訂JSON演算。

您可以在&#x200B;*/apps/mobileapps/caas/exportConfigs下建立設定節點。*

| 節點名稱 | 設定的名稱（用於呈現選擇器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示「匯出設定」的特性：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>預設（如果，未設定）</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>包含所有內容</td>
   <td>sling:resourceType</td>
   <td>從JSON匯出排除具有指定sling：resourceType的節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>不排除任何專案</td>
   <td>sling:resourceType</td>
   <td>僅包含具有來自JSON匯出之指定sling：resourceType的節點的詳細資料</td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>String[]</td>
   <td>不排除任何專案</td>
   <td>屬性首碼</td>
   <td>從JSON匯出排除以指定首碼開頭的屬性</td>
  </tr>
  <tr>
   <td>excludeproperties</td>
   <td>String[]</td>
   <td>不排除任何專案</td>
   <td>屬性名稱</td>
   <td>從JSON匯出排除指定的屬性</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>包含所有內容</td>
   <td>屬性名稱</td>
   <td><p>如果excludePropertyPrefixes設定<br />，這會包含指定的屬性，儘管與要排除的前置詞相符，</p> <p>否則（忽略排除屬性）僅包含這些屬性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>包含所有內容</td>
   <td>子名稱</td>
   <td>從JSON匯出排除指定的子系</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>字串[]<br /> <br /> </td>
   <td>不排除任何專案</td>
   <td>子名稱</td>
   <td>從JSON匯出僅包含指定的子項，排除其他</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>字串[]<br /> <br /> </td>
   <td>不重新命名任何專案</td>
   <td>&lt;actual_property_name&gt;，&lt;replacement_property_name&gt;</td>
   <td>使用取代重新命名屬性</td>
  </tr>
 </tbody>
</table>

### 資源型別匯出覆寫 {#resource-type-export-overrides}

在&#x200B;*/apps/mobileapps/caas/exportConfigs下建立設定節點。*

| 名稱 | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

下表顯示特性：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>預設（如果，未設定）</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>&lt;選擇器_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>對於下列sling資源型別，請勿傳回預設的CaaS json匯出。<br />將資源轉譯為；<br /> &lt;RESOURCE&gt;以傳回客戶json匯出。&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### 現有的Content Services匯出設定 {#existing-content-services-export-configs}

Content Services包含兩個匯出設定：

* 預設（未指定設定）
* 頁面（轉譯網站頁面）

#### 預設匯出設定 {#default-export-configuration}

如果在要求的URI中指定了設定，則會套用Content Services預設匯出設定。

&lt;RESOURCE>.caas[。&lt;DEPTH-INT>].json

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>excludeproperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>jcr：，sling：，cq：，oak：，pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr：text，text<br /> jcr：title，title<br /> jcr：description，description<br /> jcr：lastModified，lastModified<br /> cq：tags，tags<br /> cq：lastModified，lastModified</td>
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

此組態會延伸預設值，以包含子節點下的群組子項。

&lt;SITE_PAGE>.caas.page[。&lt;DEPTH-INT>].json

### 其他資源 {#additional-resources}

請參閱下列資源，瞭解內容服務中的其他主題：

* [開發模型](/help/mobile/administer-mobile-apps.md)
* [製作內容服務](/help/mobile/develop-content-as-a-service.md)
* [管理內容服務](/help/mobile/developing-content-services.md)
