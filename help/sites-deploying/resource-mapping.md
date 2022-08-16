---
title: 資源映射
seo-title: Resource Mapping
description: 瞭解如何使用資源映射為定義重定向、虛AEM擬URL和虛擬主機。
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: 7c24379c01f247f5ad45e3ecd40f3edef4ac3cfb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# 資源映射{#resource-mapping}

資源映射用於定義重定向、虛擬URL和虛擬主AEM機。

例如，可以使用這些映射：

* 將所有請求前置詞為 `/content` 這樣內部結構就不會被訪問您網站的人看到。
* 定義重定向，以便向 `/content/en/gateway` 將網站的頁面重定向到 `https://gbiv.com/`。

一個可能的HTTP映射將所有請求前置詞為 `localhost:4503` 與 `/content`。 這樣的映射可用於在網站訪問者允許的情況下隱藏內部結構：

`localhost:4503/content/we-retail/en/products.html`

要訪問，使用：

`localhost:4503/we-retail/en/products.html`

因為映射將自動添加前置詞 `/content` 至 `/we-retail/en/products.html`。

>[!CAUTION]
>
>虛榮型URL不支援規則運算式模式。

>[!NOTE]
>
>請參閱Sling文檔， [資源解析的映射](https://sling.apache.org/site/resources.html) 和 [資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 的上界。

## 查看映射定義 {#viewing-mapping-definitions}

映射形成兩個清單，JCR資源解析程式會計算（自上而下）以查找匹配項。

這些清單可在 **JCR資源解析器** Felix控制台選項；比如說， `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 配置顯示當前配置(如 [Apache Sling資源解析器](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver))。

* 配置Test這允許您輸入URL或資源路徑。 按一下 **解決** 或 **地圖** 確認系統將如何轉換條目。

* **解析程式映射項**
ResourceResolver.resolve方法用於將URL映射到Resources的條目清單。

* **映射映射條目**
ResourceResolver.map方法用於將資源路徑映射到URL的條目清單。

這兩個清單顯示各種條目，包括應用程式定義為預設值的條目。 這些URL通常旨在簡化用戶的URL。

清單對a **圖案**，與請求匹配的規則運算式， **替換** 定義強制重定向。

例如：

**圖案** `^[^/]+/[^/]+/welcome$`

將觸發：

**替換** `/libs/cq/core/content/welcome.html`。

要重定向請求：

`https://localhost:4503/welcome` &quot;

至:

`https://localhost:4503/libs/cq/core/content/welcome.html`

在儲存庫內建立新的映射定義。

>[!NOTE]
>
>有許多資源可以幫助解釋如何定義規則運算式；例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在中建立映射定AEM義 {#creating-mapping-definitions-in-aem}

在標準安裝中，AEM您可以找到資料夾：

`/etc/map/http`

這是定義HTTP協定映射時使用的結構。 其他資料夾( `sling:Folder`) `/etc/map` 用於您要映射的其他協定。

#### 配置內部重定向到/content {#configuring-an-internal-redirect-to-content}

建立將任何請求前置詞為https://localhost:4503/的映射 `/content`:

1. 使用CRXDE導航到 `/etc/map/http`。

1. 建立新節點：

   * **類型** `sling:Mapping`
此節點類型用於此類映射，但其使用並非必需。

   * **名稱** `localhost_any`

1. 按一下 **全部保存**。
1. **添加** 此節點的以下屬性：

   * **名稱** `sling:match`

      * **類型** `String`

      * **值** `localhost.4503/`
   * **名稱** `sling:internalRedirect`

      * **類型** `String[]`

      * **值** `/content/`


1. 按一下 **全部保存**。

這將處理請求，例如：
`localhost:4503/geometrixx/en/products.html`
如：
`localhost:4503/content/geometrixx/en/products.html`
已被要求。

>[!NOTE]
>
>請參閱 [資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 中，瞭解有關sling屬性以及如何配置這些屬性的詳細資訊。

>[!NOTE]
>
>您可以使用 `/etc/map.publish` 以保存發佈環境的配置。 然後必須複製這些檔案，並且新位置( `/etc/map.publish`) **映射位置** 的 [Apache Sling資源解析器](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 的子菜單。
