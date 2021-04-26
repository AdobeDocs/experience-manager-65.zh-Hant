---
title: 進階URL設定
description: 瞭解如何自訂產品和類別頁面的URL。 這可讓實作最佳化搜尋引擎的URL，並促進搜尋。
sub-product: 商務
doc-type: technical-video
activity: setup
audience: administrator
feature: 商務整合框架
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 3%

---

# 進階URL設定{#url}

[CIF核AEM心元件提](https://github.com/adobe/aem-core-cif-components) 供進階組態，以自訂產品和類別頁面的URL。許多實作將自訂這些URL以用於搜尋引擎最佳化(SEO)。  以下視訊詳細資訊如何設定`UrlProvider`服務和[Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

要根據SEO要求配置`UrlProvider`服務，並且需要項目必須為「CIF URL提供者配置」配置提供OSGI配置，並按照下面所述配置服務。

>[!NOTE]
>
> [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)專案，請參閱下方，包含範例設定，以示範產品和類別頁面的自訂URL使用情形。

### 產品頁面URL範本{#product}

這會使用下列屬性來設定產品頁面的URL:

* **產品URL範本**:定義具有一組佔位符的URL格式。預設值為`{{page}}.{{url_key}}.html#{{variant_sku}}`，最後會產生URL，例如`/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`，其中
   * `{{page}}` 替換為  `/content/venia/us/en/products/product-page`
   * `{{url_key}}` 被Magento的 `url_key` 產品屬性所取代  `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` 已由目前選取的變體取代，此處  `MH01-M-Orange`
* **產品識別碼位置**:定義用來擷取產品資料之識別碼的位置。預設值為`SELECTOR`，其他可能值為`SUFFIX`。 在上一個範例URL中，這表示將使用識別碼`chaz-kangeroo-hoodie`來擷取產品資料。
* **產品識別碼類型**:定義擷取產品資料時要使用的識別碼類型。預設值為`URL_KEY`，其他可能值為`SKU`。 在上一個範例URL中，這表示產品資料將會以MagentoGraphQL篩選器（例如`filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`）擷取。

### 產品清單頁面URL範本{#product-list}

這會使用下列屬性來設定類別或產品清單頁面的URL:

* **類別URL範本**:定義具有一組佔位符的URL格式。預設值為`{{page}}.{{id}}.html`，最後會產生URL，例如`/content/venia/us/en/products/category-page.3.html`，其中
   * `{{page}}` 替換為  `/content/venia/us/en/products/category-page`
   * `{{id}}` 被Magento的 `id` 類別屬性所取代  `3`
* **類別識別碼位置**:定義用來擷取產品資料之識別碼的位置。預設值為`SELECTOR`，其他可能值為`SUFFIX`。 在上一個範例URL中，這表示將使用識別碼`3`來擷取產品資料。
* **類別識別碼類型**:定義擷取產品資料時要使用的識別碼類型。預設值和目前僅支援的值為`ID`。 在上一個範例URL中，這表示類別資料將會以MagentoGraphQL篩選器（例如`category(id:3)`）擷取。

只要元件使用`UrlProvider`設定對應的資料，就可以為每個範本新增自訂屬性。 請查看`ProductListItemImpl`類別的代碼，以瞭解如何實施。

您也可以將`UrlProvider`服務取代為完全自訂的OSGi服務。 在這種情況下，必須實作`UrlProvider`介面，並用較高的服務級別註冊它，以替換預設實作。

## 與Sling Mappings結合{#sling-mapping}

除了`UrlProvider`外，還可設定[Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)，以重寫和處理URL。 Archetype專AEM案也提供[範例configuration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，以設定埠4503(publish)和80(dispatcher)的某些Sling Mappings。

## 與AEMDispatcher {#dispatcher}結合

URL重寫也可以通過使AEM用帶有`mod_rewrite`模組的Dispatcher HTTP伺服器來實現。 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)提供參考AEMDispatcher配置，該配置已包括生成大小的基本[重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 範例

[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)專案包含範例組態，以示範產品和類別頁面的自訂URL使用情形。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別的URL模式。 使用CIF `UrlProvider`和Sling Mappings的組合，如上所述。

>[!NOTE]
>
>此配置必須與項目使用的外部域一起調整。 Sling Mappings會根據主機名稱和網域運作。 因此，此配置預設為禁用，在部署之前必須啟用。 若要這麼做，請根據使用的網域名稱，將`resource.resolver.map.location="/etc/map.publish"`新增至專案的`JcrResourceResolver`設定，以重新命名`ui.content/src/main/content/jcr_root/etc/map.publish/https`中的Sling Mapping `hostname.adobeaemcloud.com`資料夾，並啟用此設定。

## 其他資源

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [資AEM源映射](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
