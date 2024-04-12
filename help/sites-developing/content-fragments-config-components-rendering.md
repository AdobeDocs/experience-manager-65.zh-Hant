---
title: 轉譯專用內容片段設定元件
description: 轉譯專用內容片段設定元件
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 9ef9ae75-cd8c-4adb-9bcb-e951d200d492
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
source-git-commit: 2e141ab04be33fea09ed7f6608dc9dcfaf2e50f1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 6%

---

# 轉譯專用內容片段設定元件{#content-fragments-configuring-components-for-rendering}

有好幾個 [進階服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 和內容片段的演算相關。 若要使用這些服務，這類元件的資源型別必須在內容片段框架中讓使用者知道這些元件。

這可透過設定 [OSGi服務 — 內容片段元件設定](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>如果您不需要 [進階服務](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 如下所述，您可以忽略此設定。

>[!CAUTION]
>
>當您擴充或使用現成元件時，不建議變更組態。

>[!CAUTION]
>
>您可以從頭開始撰寫只使用內容片段API （不含進階服務）的元件。 但是，在這種情況下，您必須開發元件，以便處理適當的處理。
>
>因此，建議使用核心元件。

## 需要設定的進階服務定義 {#definition-of-advanced-services-that-need-configuration}

需要註冊元件的服務包括：

* 在發佈期間正確判斷相依性（也就是說，如果片段和模型自上次發佈後有所變更，請確定片段和模型可以隨頁面自動發佈）。
* 支援全文檢索搜尋的內容片段。
* 管理/處理 *中間內容。*
* 管理/處理 *混合媒體資產。*
* 參考片段的Dispatcher排清（如果重新發佈包含片段的頁面）。
* 使用段落式演算。

如果您需要這些功能中的一或多個，則（通常）會更易於使用現成功能，而不是從頭開始開發。

## OSGi服務 — 內容片段元件設定 {#osgi-service-content-fragment-component-configuration}

設定需要繫結至OSGi服務 **內容片段元件設定**：

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>另請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得更多詳細資料。

例如：

![cfm-01](assets/cfm-01.png)

OSGi設定是：

<table>
 <tbody>
  <tr>
   <td>標籤</td>
   <td>OSGi設定<br /> </td>
   <td>說明</td>
  </tr>
  <tr>
   <td><strong>資源類型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要註冊的資源型別；例如， <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>參考屬性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含片段參照的屬性名稱；例如， <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素屬性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈現之元素名稱的屬性名稱；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>變數屬性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈現之變數名稱的屬性名稱；例如，<code>variationName</code></td>
  </tr>
 </tbody>
</table>

對於某些功能（例如，僅呈現段落範圍），您必須遵循某些慣例：

<table>
 <tbody>
  <tr>
   <td>屬性名稱</td>
   <td>說明</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>字串屬性，定義段落範圍(若在 <em>單一元素轉譯模式</em>.</p> <p>格式：</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code></li>
     <li>只有在 <code>paragraphScope</code> 設為 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>字串屬性，定義在中時如何輸出段落 <em>單一元素轉譯模式</em>.</p> <p>值：</p>
    <ul>
     <li><code>all</code> ：呈現所有段落</li>
     <li><code>range</code> ：呈現以下專案提供的段落範圍： <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>布林值屬性，定義標題(例如 <code>h1</code>， <code>h2</code>， <code>h3</code>)均計算為段落(<code>true</code>)或不是(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>這可能在6.5之後的里程碑中改變。

## 範例 {#example}

如需範例，請參閱以下內容(在現成可用的AEM例項上)：

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

這包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
