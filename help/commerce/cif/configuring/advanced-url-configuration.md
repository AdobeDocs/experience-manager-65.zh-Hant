---
title: 進階URL設定
description: 了解如何自訂產品和類別頁面的URL。 這可讓實施最佳化搜尋引擎的URL，並促進探索。
sub-product: 商務
doc-type: technical-video
activity: setup
audience: administrator
feature: 商務整合架構
kt: 4933
thumbnail: 34350.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 3%

---

# 進階URL設定 {#url}

[AEM CIF核心元](https://github.com/adobe/aem-core-cif-components) 件提供進階設定，可自訂產品和類別頁面的URL。許多實作會為了搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定`UrlProvider`服務和[Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要根據SEO需求設定`UrlProvider`服務，且需要專案必須提供「CIF URL提供者設定」的OSGI設定，並依照下列說明設定服務。

>[!NOTE]
>
> [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)專案，請參閱下方的範例設定，以示範產品和類別頁面的自訂URL使用方式。

### 產品頁面URL範本 {#product}

這會使用下列屬性設定產品頁面的URL:

* **產品URL範本**:會使用預留位置集定義URL的格式。預設值為`{{page}}.{{url_key}}.html#{{variant_sku}}`，最後會產生URL，例如`/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`，其中
   * `{{page}}` 取代為  `/content/venia/us/en/products/product-page`
   * `{{url_key}}` 已由Magento的 `url_key` 產品屬性取代，此處  `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` 已由目前選取的變體取代，此處  `MH01-M-Orange`
* **產品識別碼位置**:會定義用來擷取產品資料之識別碼的位置。預設值為`SELECTOR`，其他可能值為`SUFFIX`。 在上一個範例URL中，這表示將使用識別碼`chaz-kangeroo-hoodie`來擷取產品資料。
* **產品識別碼類型**:定義擷取產品資料時要使用的識別碼類型。預設值為`URL_KEY`，其他可能值為`SKU`。 在上一個範例URL中，這表示產品資料將會以`filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`之類的MagentoGraphQL篩選器擷取。

### 產品清單頁面URL範本{#product-list}

這會使用下列屬性來設定類別或產品清單頁面的URL:

* **類別URL範本**:會使用預留位置集定義URL的格式。預設值為`{{page}}.{{id}}.html`，最後會產生URL，例如`/content/venia/us/en/products/category-page.3.html`，其中
   * `{{page}}` 取代為  `/content/venia/us/en/products/category-page`
   * `{{id}}` 已由Magento的 `id` 類別屬性取代，此處  `3`
* **類別識別碼位置**:會定義用來擷取產品資料之識別碼的位置。預設值為`SELECTOR`，其他可能值為`SUFFIX`。 在上一個範例URL中，這表示將使用識別碼`3`來擷取產品資料。
* **類別識別碼類型**:定義擷取產品資料時要使用的識別碼類型。預設值和當前僅支援的值為`ID`。 在上一個範例URL中，這表示將使用`category(id:3)`之類的MagentoGraphQL篩選器擷取類別資料。

只要元件使用`UrlProvider`設定對應的資料，就可以為每個範本新增自訂屬性。 檢查`ProductListItemImpl`類的代碼，以了解其實現方式。

您也可以將`UrlProvider`服務取代為完全自訂的OSGi服務。 在此情況下，必須實作`UrlProvider`介面，並以較高的服務排名註冊該介面，以取代預設實作。

## 結合Sling對應{#sling-mapping}

除了`UrlProvider`，您也可以設定[Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)以重寫和處理URL。 AEM原型專案也提供[範例設定](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，以針對連接埠4503（發佈）和80（調度程式）設定一些Sling對應。

## 結合AEM Dispatcher {#dispatcher}

透過`mod_rewrite`模組，也可使用AEM Dispatcher HTTP伺服器來取得URL重寫。 [AEM專案原型](https://github.com/adobe/aem-project-archetype)提供參考AEM Dispatcher設定，其中已包含產生大小的基本[重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 範例

[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)專案包含範例設定，以示範產品和類別頁面的自訂URL使用方式。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別的URL模式。 已使用CIF `UrlProvider`和Sling對應的組合，如上所述。

>[!NOTE]
>
>此設定必須與專案使用的外部網域一併調整。 Sling對應會根據主機名稱和網域運作。 因此，預設情況下會停用此設定，且必須在部署前啟用。 若要這麼做，請根據使用的網域名稱，重新命名`ui.content/src/main/content/jcr_root/etc/map.publish/https`中的Sling Mapping `hostname.adobeaemcloud.com`資料夾，並將`resource.resolver.map.location="/etc/map.publish"`新增至專案的`JcrResourceResolver`設定以啟用此設定。

## 其他資源

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
