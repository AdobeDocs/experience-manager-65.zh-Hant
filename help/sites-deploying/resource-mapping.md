---
title: 資源映射
seo-title: 資源映射
description: 瞭解如何使用資源對應來定義重導、虛名URLAEM和虛擬主機。
seo-description: 瞭解如何使用資源對應來定義重導、虛名URLAEM和虛擬主機。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: 設定
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# 資源映射{#resource-mapping}

資源對應用於定義重導、虛名URL和虛擬主機AEM。

例如，您可以使用這些映射來：

* 將所有請求前置詞`/content`，如此內部結構就會隱藏於您網站的訪客之外。
* 定義重新導向，以便將您網站的`/content/en/gateway`頁面的所有要求重新導向至`https://gbiv.com/`。

一個可能的HTTP映射會將所有請求前置詞為`localhost:4503`和`/content`。 像這樣的對應可用來隱藏內部結構，讓網站的訪客不看它允許：

`localhost:4503/content/we-retail/en/products.html`

要訪問，請使用：

`localhost:4503/we-retail/en/products.html`

因為映射將自動將前置詞`/content`添加到`/we-retail/en/products.html`。

>[!CAUTION]
>
>虛名URL不支援規則運算式模式。

>[!NOTE]
>
>如需詳細資訊，請參閱Sling說明檔案和[Mappings for Resource Resolution](https://sling.apache.org/site/resources.html)和[Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html)。

## 查看映射定義{#viewing-mapping-definitions}

映射形成兩個清單，JCR資源解析器會評估（自上而下）以查找匹配。

在Felix控制台的&#x200B;**JCR ResourceResolver**&#x200B;選項下，可檢視這些清單（連同設定資訊）;例如，`https://<*host*>:<*port*>/system/console/jcrresolver`:

* 配置
顯示目前的組態（如[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的定義）。

* 配置測試
這可讓您輸入URL或資源路徑。 按一下**解析**&#x200B;或&#x200B;**映射**&#x200B;確認系統將如何轉換條目。

* **Resolver Map**
EntriesResourceResolver.resolve方法用於將URL映射到資源的條目清單。

* **映射映**
射條目ResourceResolver.map方法用於將資源路徑映射到URL的條目清單。

這兩個清單顯示各種條目，包括由應用程式定義為預設值的條目。 這些通常旨在簡化使用者的URL。

清單將與請求匹配的規則表達式&#x200B;**模式**&#x200B;與定義要施加的重定向的&#x200B;**替換**&#x200B;配對。

例如：

**圖樣** `^[^/]+/[^/]+/welcome$`

將觸發：

**替換** `/libs/cq/core/content/welcome.html`。

若要重新導向請求：

`https://localhost:4503/welcome` &quot;

至:

`https://localhost:4503/libs/cq/core/content/welcome.html`

系統將在儲存庫中建立新的映射定義。

>[!NOTE]
>
>有許多資源可協助說明如何定義規則運算式；例如[https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在{#creating-mapping-definitions-in-aem}中創AEM建映射定義

在標準安裝中，您AEM可以找到該資料夾：

`/etc/map/http`

這是定義HTTP協定映射時使用的結構。 對於您要映射的任何其它協定，可以在`/etc/map`下建立其他資料夾(`sling:Folder`)。

#### 設定內部重新導向至/content {#configuring-an-internal-redirect-to-content}

要建立將任何請求前置詞為https://localhost:4503/的映射，請使用`/content`:

1. 使用CRXDE導航至`/etc/map/http`。

1. 建立新節點：

   * **類** `sling:Mapping`
型此節點類型用於此類映射，但其用途不是強制性的。

   * **名稱** `localhost_any`

1. 按一下&#x200B;**保存全部**。
1. **將** 以下屬性添加到此節點：

   * **名稱** `sling:match`

      * **類型** `String`

      * **值** `localhost.4503/`
   * **名稱** `sling:internalRedirect`

      * **類型** `String`

      * **值** `/content/`


1. 按一下&#x200B;**保存全部**。

這將處理下列請求：
`localhost:4503/geometrixx/en/products.html`
假設：
`localhost:4503/content/geometrixx/en/products.html`
被要求。

>[!NOTE]
>
>請參閱Sling Documentation中的[Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html)，以取得有關sling屬性的詳細資訊以及如何設定這些屬性。

>[!NOTE]
>
>您可以使用`/etc/map.publish`來保存發佈環境的配置。 然後必須複製這些檔案，並為發佈環境的[Apache Sling資源解析器](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的&#x200B;**Mapping Location**&#x200B;設定新位置(`/etc/map.publish`)。

