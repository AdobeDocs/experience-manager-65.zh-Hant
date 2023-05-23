---
title: 高級URL配置
description: 瞭解如何自定義產品和類別頁的URL。 這允許實現優化搜索引擎的URL並促進發現。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 6%

---

# 高級URL配置 {#url}

>[!NOTE]
>
>搜尋引擎最佳化 (SEO) 已成為許多行銷人員的重點考量。因此，許多項目需要解決徐工機構的AEM擔憂。 請閱讀 [SEO和URL管理最佳實踐](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 的雙曲餘切值。

[AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) 提供高級配置，以自定義產品和類別頁的URL。 許多實現將自定義這些URL以用於搜索引擎優化(SEO)。 以下視頻詳細資訊如何配置 `UrlProvider` 服務和功能 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自定義產品和類別頁的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

配置 `UrlProvider` 服務，並且需要項目必須為「CIF URL Provider配置」提供OSGI配置。

>[!NOTE]
>
>自CIF核心元件2.0.0版以來，URL提供程式配置僅提供預定義的URL格式，而不提供1.x版中的自由文本配置格式。 此外，使用選擇器傳遞URL中的資料已被尾碼取代。

### 產品頁URL格式 {#product}

這將配置產品頁的URL，並支援以下選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (預設)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

對於 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 將被產品的sku替換，例如 `VP09`
* `{{url_key}}` 將被產品的 `url_key` 屬性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 將被產品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將替換為當前選定的變型，例如 `VP09-KH-S`

自 `url_path` 已棄用，預定義的產品URL格式使用產品 `url_rewrites` 選擇路徑段最多的路徑段， `url_path` 不可用。

使用上面的示例資料，使用預設URL格式格式化的產品變型URL將看起來類似 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 類別頁URL格式 {#product-list}

這將配置類別或產品清單頁的URL，並支援以下選項：

* `{{page}}.html/{{url_path}}.html` (預設)
* `{{page}}.html/{{url_key}}.html`

對於 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 將替換為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將被類別的 `url_key` 屬性
* `{{url_path}}` 將被類別的 `url_path`

使用上面的示例資料，使用預設URL格式設定的類別頁URL將看起來類似 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
>的 `url_path` 是 `url_keys` 產品或類別的祖先和產品或類別的 `url_key` 分隔 `/` 斜線。

### 特定類別/產品頁 {#specific-pages}

可以建立 [多類別和產品頁](multi-template-usage.md) 僅用於目錄的特定類別或產品子集。

的 `UrlProvider` 預配置為在作者層實例上生成到此類頁的深度連結。 這對編輯器非常有用，編輯器使用「預覽」模式瀏覽網站，導航到特定產品或類別頁面並切換回「編輯」模式以編輯該頁面。

另一方面，在發佈層實例上，目錄頁URL應保持穩定，以避免在搜索引擎排名上失利。 由於該發佈層實例將不會在預設情況下呈現指向特定目錄頁的深度連結。 要更改此行為， _CIF URL提供程式特定頁面策略_ 可以配置為始終生成特定頁URL。

## 自定義URL格式 {#custom-url-format}

要提供自定義URL格式，項目可以 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，將實現註冊為OSGI服務。 如果可用，這些實現將替換已配置的預定義格式。 如果註冊了多個實現，則具有較高服務等級的實現用較低服務等級代替所述一個或多個實現。

自定義URL格式實現必須實現一對方法，以從給定參數構建URL，並分析URL以分別返回相同的參數。

## 與Sling映射組合 {#sling-mapping}

除 `UrlProvider`，也可以配置 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重寫和處理URL。 Archetype項AEM目還提供 [示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為埠4503（發佈）和80（調度程式）配置某些Sling映射。

## 與Dispatcher結AEM合 {#dispatcher}

還可以使用Dispatcher HTTP伺服器AEM和 `mod_rewrite` 中。 的 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 提供已包AEM含基本功能的引用Dispatcher配置 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 生成大小。

## 範例

的 [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia) 項目包括示例配置，以演示產品和類別頁的自定義URL的使用。 這允許每個項目根據其SEO需求為產品和類別頁面設定單個URL模式。 CIF的組合 `UrlProvider` 和Sling映射（如上所述）。

>[!NOTE]
>
>此配置必須與項目使用的外部域一起調整。 Sling映射基於主機名和域工作。 因此，預設情況下禁用此配置，並且必須在部署之前啟用此配置。 要執行此操作，請更名Sling映射 `hostname.adobeaemcloud.com` 資料夾 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的域名，通過添加 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 項目的配置。

## 其他資源

* [Venia參考儲存](https://github.com/adobe/aem-cif-guides-venia)
* [資AEM源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
