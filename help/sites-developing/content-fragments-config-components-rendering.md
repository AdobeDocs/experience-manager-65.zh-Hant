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

有幾個 [進階服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 與內容片段的轉譯相關。 若要使用這些服務，此類元件的資源類型必須讓內容片段架構知道。

這可透過設定 [OSGi服務 — 內容片段元件設定](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>如果您不需要 [進階服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 如下所述，您可以忽略此配置。

>[!CAUTION]
>
>擴充或使用現成可用的元件時，不建議變更設定。

>[!CAUTION]
>
>您可以從頭開始撰寫僅使用內容片段API的元件，不需進階服務。 但在此情況下，您必須開發元件，以便處理適當的處理。
>
>因此，建議使用核心元件。

## 需要配置的高級服務的定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（亦即，如果片段和模型自上次發佈以來已變更，則可以透過頁面自動發佈）。
* 支援全文搜尋的內容片段。
* 管理/處理 *內容。*
* 管理/處理 *混合媒體資產。*
* 已參照片段的Dispatcher排清（如果包含片段的頁面已重新發佈）。
* 使用段落式轉譯。

如果您需要一或多個這些功能，（通常）使用現成可用的功能會比從頭開發更輕鬆。

## OSGi服務 — 內容片段元件設定 {#osgi-service-content-fragment-component-configuration}

配置需要綁定到OSGi服務 **內容片段元件設定**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊。

例如：

![cfm-01](assets/cfm-01.png)

OSGi設定為：

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
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含片段參考的屬性名稱；例如 <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Element(s)屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現的元素名稱的屬性名稱；例如<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現的變數名稱的屬性名稱；例如<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能（例如，僅呈現段落範圍），您必須遵守一些慣例：

<table>
 <tbody>
  <tr>
   <td>屬性名稱</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字串屬性，定義要輸出的段落範圍(若為 <em>單一元素演算模式</em>.</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code></li>
     <li>只有 <code>paragraphScope</code> 設為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>字串屬性，定義如果在中，如何輸出段落 <em>單一元素演算模式</em>.</p> <p>值:</p>
    <ul>
     <li><code>all</code> :轉譯所有段落</li>
     <li><code>range</code> :呈現提供的段落範圍 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一個布林值屬性，定義if標題(例如 <code>h1</code>, <code>h2</code>, <code>h3</code>)會計為段落(<code>true</code>)或否(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>這在6.5之後的里程碑中可能會有所變更。

## 範例 {#example}

例如，請參閱下列內容(在現成可用的AEM例項上):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

其中包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
