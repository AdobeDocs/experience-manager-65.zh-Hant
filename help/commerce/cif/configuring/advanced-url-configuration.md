---
title: 進階URL設定
description: 了解如何自訂產品和類別頁面的URL。 這可讓實施最佳化搜尋引擎的URL，並促進探索。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: fd973cb3693872e4850f860a625cab70553d2754
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 4%

---

# 進階URL設定 {#url}

>[!NOTE]
>
> 搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，許多AEM專案都需要解決SEO疑慮。 如需詳細資訊，請參閱[SEO和URL管理最佳實務](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 。

[AEM CIF核心元](https://github.com/adobe/aem-core-cif-components) 件提供進階設定，可自訂產品和類別頁面的URL。許多實作會為了搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定`UrlProvider`服務和[Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要根據SEO要求設定`UrlProvider`服務，且需要專案必須提供「CIF URL提供者設定」的OSGI設定。

>[!NOTE]
>
> 自AEM CIF核心元件2.0.0版起，URL提供者設定僅提供預先定義的url格式，而非1.x版中可使用的自由文字設定格式。 此外，在URL中使用選取器傳遞資料的做法已取代為尾碼。

### 產品頁面URL格式 {#product}

這可設定產品頁面的URL並支援下列選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (預設)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

在[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)中：

* `{{page}}` 將替換為  `/content/venia/us/en/products/product-page`
* `{{sku}}` 將替換為產品的sku，例如  `VP09`
* `{{url_key}}` 會由產品的屬性取 `url_key` 代，例如  `lenora-crochet-shorts`
* `{{url_path}}` 將被產品的取代， `url_path`例如  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將替換為目前選取的變體，例如  `VP09-KH-S`

使用上述範例資料，使用預設URL格式格式化的產品變體URL看起來會像`/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 類別頁面URL格式 {#product-list}

這可設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

在[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)中：

* `{{page}}` 將替換為  `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將替換為類別的屬 `url_key` 性
* `{{url_path}}` 將替換為類別的  `url_path`

使用上述範例資料，使用預設URL格式設定的類別頁面URL看起來會像`/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
> `url_path`是產品或類別祖先的`url_keys`與產品或類別的`url_key`的串連，以`/`斜線分隔。

## 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，專案可實作[`UrlFormat`介面](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html)，並將實作記錄為OSGI服務，以類別頁面或產品頁面url格式使用。 `UrlFormat#PROP_USE_AS`服務屬性指示要替換的配置預定義格式：

* `useAs=productPageUrlFormat`，將取代已設定的產品頁面url格式
* `useAs=categoryPageUrlFormat`，將取代已設定的類別頁面url格式

如果註冊為OSGI服務的`UrlFormat`有多個實現，則服務排名較高的實現將服務排名較低的實現替換。

`UrlFormat`必須實作一對方法，以從指定的參數地圖建立URL，並剖析URL以傳回相同的參數地圖。 參數與上述相同，只有對於類別，才向`UrlFormat`提供額外的`{{uid}}`參數。

## 結合Sling對應 {#sling-mapping}

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
