---
title: 轉譯專用內容片段設定元件
seo-title: 轉譯專用內容片段設定元件
description: 轉譯專用內容片段設定元件
seo-description: 轉譯專用內容片段設定元件
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 9%

---


# 轉譯專用內容片段設定元件{#content-fragments-configuring-components-for-rendering}

有幾個[進階服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)與內容片段的呈現有關。 要使用這些服務，此類元件的資源類型必須使內容片段框架自己知道。

這是通過配置[OSGi服務——內容片段元件配置](#osgi-service-content-fragment-component-configuration)來完成的。

>[!CAUTION]
>
>如果您不需要下面所述的[advanced services](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)，則可以忽略此配置。

>[!CAUTION]
>
>當您擴充或使用現成可用的元件時，不建議您變更組態。

>[!CAUTION]
>
>您可以從頭開始編寫僅使用內容片段API的元件，而不需進階服務。 不過，在這種情況下，您必須開發元件，以便處理適當的處理。
>
>因此，建議使用核心元件。

## 需要配置{#definition-of-advanced-services-that-need-configuration}的高級服務的定義

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（即，如果片段和模型自上次發佈後已變更，請確定它們可自動與頁面一起發佈）。
* 支援全文搜尋的內容片段。
* 管理／處理&#x200B;*中間內容。*
* 管理／處理&#x200B;*混合媒體資產。*
* Dispatcher flush for referenced fragments(if a page containing a fragment is re-published)。
* 使用段落式演算。

如果您需要一或多個這些功能，則（通常）使用現成可用的功能會比較容易，而不是從頭開發。

## OSGi服務——內容片段元件配置{#osgi-service-content-fragment-component-configuration}

配置需要綁定到OSGi服務&#x200B;**內容片段元件配置**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>如需詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

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
   <td>要註冊的資源類型；例如，<br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含對片段的引用的屬性的名稱；例如，<code>fragmentPath</code>或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要渲染的元素名稱的屬性的名稱；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現的變數名稱的屬性名稱；例如，<code>variationName</code></td>
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
   <td><p>字串屬性，定義在<em>單一元素演算模式</em>中要輸出的段落範圍。</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或<code>1-3</code>或<code>1-3;6;7-8</code> <code>*-3;5-*</code></li>
     <li>僅當<code>paragraphScope</code>設為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>字串屬性，定義在<em>單一元素演算模式</em>中如何輸出段落。</p> <p>值:</p>
    <ul>
     <li><code>all</code> :來呈現所有段落</li>
     <li><code>range</code> :來轉換 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一種布林屬性，定義標題（例如<code>h1</code>、<code>h2</code>、<code>h3</code>）是否被計為段落(<code>true</code>)<code>false</code></td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>這在6.5之後的里程碑中可能會改變。

## 範例 {#example}

例如，請參閱下列（在現成可用的AEM例項上）:

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

