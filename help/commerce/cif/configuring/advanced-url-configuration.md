---
title: 進階URL設定
description: 瞭解如何自訂產品和類別頁面的URL。 實作可藉此最佳化搜尋引擎的URL並促進探索。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 3%

---

# 進階URL設定 {#url}

>[!NOTE]
>
>搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，許多AEM專案中的SEO考量都必須解決。 另請參閱 [SEO和URL管理最佳作法](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 以取得其他資訊。

[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 提供進階設定，以便自訂產品和類別頁面的URL。 許多實施會針對搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定 `UrlProvider` 的服務與功能 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

若要設定 `UrlProvider` 服務必須根據SEO需求和需求提供「CIF URL提供者設定」的OSGI設定。

>[!NOTE]
>
>自AEM CIF核心元件2.0.0版開始，「URL提供者」設定僅提供預先定義的URL格式，而非1.x版已知的自由文字可設定格式。 此外，在URL中使用選取器傳遞資料的功能，已由尾碼取代。

### 產品頁面URL格式 {#product}

這會設定產品頁面的URL，並支援下列選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (預設)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

如果有 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 已取代為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 由產品的SKU取代，例如， `VP09`
* `{{url_key}}` 由產品的 `url_key` 屬性，例如， `lenora-crochet-shorts`
* `{{url_path}}` 由產品的 `url_path`例如， `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 由目前選取的變體取代，例如， `VP09-KH-S`

由於 `url_path` 已過時，預先定義的產品URL格式使用產品的 `url_rewrites` 並挑選具有最多路徑區段的路徑作為替代方案，如果 `url_path` 無法使用。

在上述範例資料中，使用預設URL格式的產品變體URL看起來像 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 類別頁面URL格式 {#product-list}

這會設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

如果有 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 已取代為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 由類別的 `url_key` 屬性
* `{{url_path}}` 由類別的 `url_path`

在上述範例資料中，使用預設URL格式格式的類別頁面URL看起來像 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>此 `url_path` 是以下專案的串連： `url_keys` 產品或類別的祖先以及產品或類別的 `url_key` 分隔方式 `/` slash。

### 特定類別 — /產品頁面 {#specific-pages}

可以建立 [多個類別和產品頁面](multi-template-usage.md) 僅針對類別或目錄產品的特定子集。

此 `UrlProvider` 已預先設定，可在作者層級例項上產生這些頁面的深層連結。 這對編輯器很有用，編輯器會使用預覽模式瀏覽網站、導覽至特定產品或類別頁面，然後切換回編輯模式以編輯頁面。

另一方面，在發佈層級執行個體上，目錄頁面URL應保持穩定，以免失去搜尋引擎排名之類的評分。 因為發佈層執行個體預設不會轉譯特定目錄頁面的深層連結。 若要變更此行為， _CIF URL提供者特定頁面策略_ 可設定為一律產生特定頁面url。

## 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，讓專案可實作 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，並將實作註冊為OSGI服務。 這些實施（如果可用）會取代已設定的預先定義格式。 如果註冊了多個實作，則服務排名較高的實作會取代服務排名較低的實作。

自訂URL格式實作必須實作一對方法，用於從指定引數建置URL並剖析URL以分別傳回相同的引數。

## 與Sling對應結合 {#sling-mapping}

除了 `UrlProvider`，也可以設定 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以重寫及處理URL。 AEM Archetype專案也提供 [設定範例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為連線埠4503 （發佈）和80 (Dispatcher)設定一些Sling對應。

## 與AEM Dispatcher結合 {#dispatcher}

透過以下方式使用AEM Dispatcher HTTP伺服器也可實現URL重寫： `mod_rewrite` 模組。 此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 提供已包含基本設定的AEM Dispatcher參考設定 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 以產生的大小。

## 範例

此 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) project包含示範產品和類別頁面使用自訂URL的設定範例。 如此一來，每個專案就能根據SEO需求，為產品和類別頁面設定個別的URL模式。 CIF的組合 `UrlProvider` 並如上所述使用Sling對應。

>[!NOTE]
>
>此設定必須使用專案使用的外部網域進行調整。 Sling對應是根據主機名稱和網域來運作。 因此，此設定預設為停用，必須在部署之前啟用。 若要這麼做，請重新命名Sling對應 `hostname.adobeaemcloud.com` 資料夾位置 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的網域名稱並通過以下方式啟用此設定： `resource.resolver.map.location="/etc/map.publish"` 至 `JcrResourceResolver` 專案的設定。

## 其他資源

* [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
