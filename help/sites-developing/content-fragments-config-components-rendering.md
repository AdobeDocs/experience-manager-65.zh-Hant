---
title: 轉譯專用內容片段設定元件
seo-title: Content Fragments Configuring Components for Rendering
description: 轉譯專用內容片段設定元件
seo-description: Content Fragments Configuring Components for Rendering
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
exl-id: 9ef9ae75-cd8c-4adb-9bcb-e951d200d492
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 7%

---

# 轉譯專用內容片段設定元件{#content-fragments-configuring-components-for-rendering}

有幾個 [高級服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 與內容片段的呈現相關。 要使用這些服務，此類元件的資源類型必須使內容片段框架知道它們本身。

通過配置 [OSGi服務 — 內容片段元件配置](#osgi-service-content-fragment-component-configuration)。

>[!CAUTION]
>
>如果你不需要 [高級服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 如下所述，您可以忽略此配置。

>[!CAUTION]
>
>在擴展或使用現成元件時，不建議更改配置。

>[!CAUTION]
>
>您可以從頭開始編寫僅使用Content Fragments API的元件，但不提供高級服務。 但是，在這種情況下，您必須開發元件，以便處理相應的處理。
>
>因此，建議使用核心元件。

## 需要配置的高級服務的定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 正確確定發佈期間的依賴關係（即，如果碎片和模型自上次發佈後發生更改，則可以隨頁面自動發佈它們）。
* 支援全文搜索中的內容片段。
* 管理/處理 *內容。*
* 管理/處理 *混合媒體資產。*
* 引用片段的Dispatcher刷新（如果包含片段的頁被重新發佈）。
* 使用基於段落的渲染。

如果您需要這些功能中的一個或多個，則（通常）使用現成功能比從頭開發更容易。

## OSGi服務 — 內容片段元件配置 {#osgi-service-content-fragment-component-configuration}

配置需要綁定到OSGi服務 **內容片段元件配置**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的上界。

例如：

![cfm-01](assets/cfm-01.png)

OSGi配置為：

<table>
 <tbody>
  <tr>
   <td>標籤</td>
   <td>OSGi配置<br /> </td>
   <td>說明</td>
  </tr>
  <tr>
   <td><strong>資源類型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要註冊的資源類型；例如 <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>引用屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含對片段的引用的屬性的名稱；例如 <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現的元素名稱的屬性的名稱；例如<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現的變體名稱的屬性的名稱；例如<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能（例如僅呈現段落範圍），您必須遵守一些約定：

<table>
 <tbody>
  <tr>
   <td>屬性名稱</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>一個字串屬性，它定義要輸出的段落範圍（如果在） <em>單元渲染模式</em>。</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code></li>
     <li>僅計算 <code>paragraphScope</code> 設定為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>一個字串屬性，它定義在中時如何輸出段落 <em>單元渲染模式</em>。</p> <p>值:</p>
    <ul>
     <li><code>all</code> :呈現所有段落</li>
     <li><code>range</code> :呈現由 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一個布爾屬性，它定義標題(例如， <code>h1</code>。 <code>h2</code>。 <code>h3</code>)作為段落(<code>true</code>)或不(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>這在6.5個里程碑之後可能會發生變化。

## 範例 {#example}

作為示例，請參見以下(在現成實例上AEM):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

這包括：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
