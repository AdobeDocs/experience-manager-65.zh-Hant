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
source-git-commit: 014731aa9c5c4d7d419ff8b037142b47e7b7da01
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 4%

---

# 進階URL設定 {#url}

>[!NOTE]
>
> 搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，許多AEM專案都需要解決SEO疑慮。 請閱讀 [SEO和URL管理最佳作法](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 以取得其他資訊。

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 提供進階設定，可自訂產品和類別頁面的URL。 許多實作會為了搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定 `UrlProvider` 服務與功能 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要設定 `UrlProvider` 服務（根據SEO需求和需求）必須提供「CIF URL提供者設定」的OSGI設定。

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

若 [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 將替換為產品的sku，例如 `VP09`
* `{{url_key}}` 將被產品的 `url_key` 屬性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 將被產品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將替換為目前選取的變體，例如 `VP09-KH-S`

由於 `url_path` 已遭取代，預先定義的產品URL格式會使用產品的 `url_rewrites` 並挑選路徑區段最多的區段，若 `url_path` 無法使用。

使用上述範例資料，使用預設URL格式格式化的產品變體URL看起來會像 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 類別頁面URL格式 {#product-list}

這可設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

若 [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將替換為類別的 `url_key` 屬性
* `{{url_path}}` 將替換為類別的 `url_path`

使用上述範例資料，使用預設URL格式格式化的類別頁面URL看起來會像 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 此 `url_path` 是 `url_keys` 產品或類別的祖先和產品或類別的 `url_key` 分隔 `/` 斜線。

### 特定類別/產品頁面 {#specific-pages}

您可以建立 [多類別和產品頁面](multi-template-usage.md) 僅適用於目錄的特定類別或產品子集。

此 `UrlProvider` 已預先設定，以在製作層級例項上產生連結至此類頁面的深層連結。 對於編輯者來說，這很實用，他們可以使用預覽模式瀏覽網站、導覽至特定產品或類別頁面，然後切換回編輯模式以編輯頁面。

另一方面，在發佈層級例項上，目錄頁面url應保持穩定，以免在搜尋引擎排名上失去增益。 因為該發佈層級例項預設不會呈現特定目錄頁面的深層連結。 若要變更此行為， _CIF URL提供者特定頁面策略_ 可設定為一律產生特定頁面url。

## 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，專案可在 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，並將實作註冊為OSGI服務。 這些實作（若有）將取代已設定的預先定義格式。 如果已註冊多個實施，則服務排名較高的實施會以較低的服務排名取代該實施。

自訂URL格式實施必須實作一對方法，以從指定參數建立URL，並剖析URL以分別傳回相同參數。

## 結合Sling對應 {#sling-mapping}

除了 `UrlProvider`，也可以設定 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重寫及處理URL。 AEM原型專案也提供 [範例設定](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為連接埠4503（發佈）和80（調度程式）設定某些Sling對應。

## 結合AEM Dispatcher {#dispatcher}

URL重寫也可透過使用AEM Dispatcher HTTP伺服器來達成 `mod_rewrite` 模組。 此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 提供參考AEM Dispatcher設定，其中已包含基本 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) ，取代所產生的大小。

## 範例

此 [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) 專案包含設定範例，以示範產品和類別頁面的自訂URL使用方式。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別的URL模式。 CIF的組合 `UrlProvider` 和Sling對應已使用，如上所述。

>[!NOTE]
>
>此設定必須與專案使用的外部網域一併調整。 Sling對應會根據主機名稱和網域運作。 因此，預設情況下會停用此設定，且必須在部署前啟用。 若要這麼做，請重新命名Sling對應 `hostname.adobeaemcloud.com` 資料夾 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的網域名稱，並借由新增 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 專案的設定。

## 其他資源

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
