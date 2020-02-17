---
title: 雲端服務設定
seo-title: 雲端服務設定
description: 您可以擴充現有的例項，以建立您自己的設定
seo-description: 您可以擴充現有的例項，以建立您自己的設定
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 雲端服務設定{#cloud-service-configurations}

配置設計為提供儲存服務配置的邏輯和結構。

您可以擴充現有的例項，以建立您自己的設定。

## 概念 {#concepts}

在開發配置時，所採用的原則基於以下概念：

* 服務／適配器用於檢索配置。
* 配置（例如屬性／段落）繼承自父代。
* 依路徑從分析節點參考。
* 輕鬆擴充。
* 有彈性，可應付更複雜的組態，例如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 支援相依性(例如 [Adobe Analytics外掛程式需要](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) Adobe Analytics [](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 組態)。

## 結構 {#structure}

配置的基本路徑是：

`/etc/cloudservices`.

對於每種配置類型，都將提供一個模板和一個元件。這使得配置模板能夠滿足自定義後的大多數需求。

要為新服務提供配置，您需要：

* 建立服務頁

   `/etc/cloudservices`

* 下方：

   * 配置模板
   * 配置元件

模板和元件必須繼承基 `sling:resourceSuperType` 本模板中的：

`cq/cloudserviceconfigs/templates/configpage`

或基本元件

`cq/cloudserviceconfigs/components/configpage`

服務提供商還應提供服務頁：

`/etc/cloudservices/<service-name>`

### 範本 {#template}

您的範本將擴充基本範本：

`cq/cloudserviceconfigs/templates/configpage`

並定義指 `resourceType` 向自訂元件的元件。

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

您的元件應延伸基本元件：

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

在設定範本和元件後，您可以在下列位置新增子頁面，以新增您的設定：

`/etc/cloudservices/<service-name>`

### 內容模型 {#content-model}

內容模型會儲存為 `cq:Page` :

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

配置儲存在子節點下 `jcr:content`。

* 修正對話方塊中定義的屬性應直接儲存在 `jcr:node` 上。
* 動態元素(使 `parsys` 用或 `iparsys`)使用子節點來儲存元件資料。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

如需API的參考檔案，請參 [閱com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)。

### AEM整合 {#aem-integration}

「頁面屬性」對話方 **塊的「雲端服務** 」標籤中會列出可用服務 **(繼承自或的任** 何頁面 `foundation/components/page``wcm/mobile/components/page`)。

該頁籤還提供：

* 連結至您可啟用服務的位置
* 從路徑欄位選擇配置（服務的子節點）

#### 密碼加密 {#password-encryption}

儲存服務的使用者憑證時，所有密碼都應加密。

您可以新增隱藏的表單欄位來達成此目標。 該欄位的屬性名 `@Encrypted` 稱中應有注釋；例如，對於字 `password` 段，名稱將寫為：

`password@Encrypted`

然後，屬性將由自動加密(使 `CryptoSupport` 用服務) `EncryptionPostProcessor`。

>[!NOTE]
>
>這與標準註解類 ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` 似。

>[!NOTE]
>
>預設情況下， `EcryptionPostProcessor` 僅加密 `POST` 向發出的請求 `/etc/cloudservices`。

#### 「服務」頁的其他屬性jcr：內容節點 {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>要自動包含在頁面中的元件的參考路徑。<br /> 這用於其他功能和JS包含。<br /> 這包括包含頁面上的元件<br /> ( <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 通常在標籤之前 <code>body</code> )。<br /> 若是Analytics和Target，我們會使用它來包含其他功能，例如追蹤訪客行為的JavaScript呼叫。</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>服務的簡短說明。<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>服務的擴展說明。</td>
  </tr>
  <tr>
   <td>排名</td>
   <td>用於清單中的服務排名。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>在頁面屬性對話方塊中顯示設定的篩選。</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>服務網站的URL。</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>服務URL的標籤。</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>服務縮圖的路徑。</td>
  </tr>
  <tr>
   <td>visel</td>
   <td>頁面屬性對話方塊中的可見度；預設顯示（可選）</td>
  </tr>
 </tbody>
</table>

### 使用案例 {#use-cases}

這些服務預設提供：

* [追蹤器程式碼片段](/help/sites-administering/external-providers.md) （Google、WebTrends等）
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Scene7](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另請參閱 [建立自訂雲端服務](/help/sites-developing/extending-cloud-config-custom-cloud.md)。

