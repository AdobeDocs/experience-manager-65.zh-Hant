---
title: 雲端服務設定
seo-title: Cloud Service Configurations
description: 您可以擴展現有實例以建立您自己的配置
seo-description: You can extend the existing instances to create your own configurations
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# 雲端服務設定{#cloud-service-configurations}

配置設計為提供用於儲存服務配置的邏輯和結構。

您可以擴展現有實例以建立您自己的配置。

## 概念 {#concepts}

在開發配置時使用的原則基於以下概念：

* 服務/適配器用於檢索配置。
* 配置（例如屬性/段落）從父級繼承。
* 按路徑從分析節點引用。
* 易於擴展。
* 具有靈活性，可滿足更複雜的配置，如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 支援依賴項(例如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 插件需要 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 配置)。

## 結構 {#structure}

配置的基本路徑是：

`/etc/cloudservices`。

對於每種配置類型，都將提供一個模板和一個元件。這樣，就可以擁有配置模板，這些模板在自定義後可以滿足大多數需要。

要為新服務提供配置，您需要：

* 建立服務頁

   `/etc/cloudservices`

* 下：

   * 配置模板
   * 配置元件

模板和元件必須繼承 `sling:resourceSuperType` 從基本模板：

`cq/cloudserviceconfigs/templates/configpage`

分別是基元

`cq/cloudserviceconfigs/components/configpage`

服務提供商還應提供服務頁：

`/etc/cloudservices/<service-name>`

### 範本 {#template}

您的模板將擴展基本模板：

`cq/cloudserviceconfigs/templates/configpage`

定義 `resourceType` 指向自定義元件。

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### 元件 {#components}

您的元件應擴展基本元件：

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

在設定模板和元件後，您可以通過在以下位置添加子頁來添加配置：

`/etc/cloudservices/<service-name>`

### 內容模型 {#content-model}

內容模型儲存為 `cq:Page` 下：

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

配置儲存在子節點下 `jcr:content`。

* 在對話框中定義的固定屬性應儲存在 `jcr:node` 直接輸入。
* 動態元素(使用 `parsys` 或 `iparsys`)使用子節點儲存元件資料。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

有關API的參考文檔，請參見 [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)。

### 集AEM成 {#aem-integration}

可用服務列於 **Cloud Services** 頁籤 **頁面屬性** 對話框(繼承自 `foundation/components/page` 或 `wcm/mobile/components/page`)。

該頁籤還提供：

* 指向可啟用服務的位置的連結
* 從路徑欄位中選擇配置（服務的子節點）

#### 密碼加密 {#password-encryption}

儲存服務的用戶憑據時，應加密所有密碼。

可以通過添加隱藏表單域來實現此目的。 此欄位應具有注釋 `@Encrypted` 在屬性名稱中；即 `password` 欄位名稱將寫為：

`password@Encrypted`

然後將自動加密該屬性(使用 `CryptoSupport` 服務) `EncryptionPostProcessor`。

>[!NOTE]
>
>這與標準類似 ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` 注釋。

>[!NOTE]
>
>預設情況下， `EcryptionPostProcessor` 僅加密 `POST` 請求 `/etc/cloudservices`。

#### 服務頁jcr：內容節點的其他屬性 {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>元件引用</td>
   <td>要自動包括在頁面中的元件的引用路徑。<br /> 這用於附加功能和JS包含。<br /> 這包括頁面上的元件，其中<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 包含(通常在 <code>body</code> 標籤)。<br /> 在分析和目標中，我們使用它來包括其他功能，如跟蹤訪問者行為的JavaScript調用。</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>服務的簡短說明。<br /> </td>
  </tr>
  <tr>
   <td>說明擴展</td>
   <td>服務的擴展說明。</td>
  </tr>
  <tr>
   <td>排名</td>
   <td>用於清單中的服務排名。</td>
  </tr>
  <tr>
   <td>可選子項</td>
   <td>用於在頁面屬性對話框中顯示配置的篩選器。</td>
  </tr>
  <tr>
   <td>服務URL</td>
   <td>服務網站的URL。</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>服務URL的標籤。</td>
  </tr>
  <tr>
   <td>縮略圖路徑</td>
   <td>服務縮略圖的路徑。</td>
  </tr>
  <tr>
   <td>可見</td>
   <td>頁面屬性對話框中的可見性；預設可見（可選）</td>
  </tr>
 </tbody>
</table>

### 使用案例 {#use-cases}

這些服務預設提供：

* [跟蹤器代碼段](/help/sites-administering/external-providers.md) (Google、WebTrends等)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)

<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另請參閱 [建立自定義Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md)。
