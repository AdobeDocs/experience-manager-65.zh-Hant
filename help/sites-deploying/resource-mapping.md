---
title: 資源映射
seo-title: 資源映射
description: 瞭解如何使用資源對應來定義AEM的重新導向、虛名URL和虛擬主機。
seo-description: 瞭解如何使用資源對應來定義AEM的重新導向、虛名URL和虛擬主機。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 資源映射{#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以使用這些映射來：

* 在所有請求前加 `/content` 上前置詞，如此內部結構就會對網站訪客隱藏。
* 定義重新導向，以便將網站頁 `/content/en/gateway` 面的所有請求重新導向至 `https://gbiv.com/`。

一個可能的HTTP映射會將所有請求前置詞 `localhost:4503` 與一起 `/content`。 像這樣的對應可用來隱藏內部結構，讓網站的訪客不看它允許：

`localhost:4503/content/we-retail/en/products.html`

要訪問，請使用：

`localhost:4503/we-retail/en/products.html`

因為映射會自動將前置詞添加 `/content` 到 `/we-retail/en/products.html`。

>[!CAUTION]
>
>虛名URL不支援規則運算式模式。

>[!NOTE]
>
>如需詳細資訊，請參閱Sling [檔案和Mappings for Resource Resolution](https://sling.apache.org/site/resources.html) and [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) 。

## 查看映射定義 {#viewing-mapping-definitions}

映射形成兩個清單，JCR資源解析器會評估（自上而下）以查找匹配。

在Felix控制台的 **JCR ResourceResolver** （資源解析器）選項下，可檢視這些清單（連同設定資訊）;例如， `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 設定顯示目前的設定(如 [Apache Sling Resource Resolver所定義](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver))。

* 配置測試這允許您輸入URL或資源路徑。 單 **擊解析** 或 **映射** ，確認系統將如何轉換條目。

* **Resolver Map Entries** resourceResolver.resolve方法用於將URL映射到資源的條目清單。

* **映射映射條**&#x200B;目ResourceResolver.map方法用於將資源路徑映射到URL的條目清單。

這兩個清單顯示各種條目，包括由應用程式定義為預設值的條目。 這些通常旨在簡化使用者的URL。

這些清單會將 **Pattern**（與請求相符的規則運算式）與 **Replacement** （取代）配對，後者定義要強加的重新導向。

例如：

**圖樣**`^[^/]+/[^/]+/welcome$`

將觸發：

**替換**`/libs/cq/core/content/welcome.html`。

若要重新導向請求：

`https://localhost:4503/welcome` ``

至:

`https://localhost:4503/libs/cq/core/content/welcome.html`

系統將在儲存庫中建立新的映射定義。

>[!NOTE]
>
>有許多資源可協助說明如何定義規則運算式；例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM中建立對應定義 {#creating-mapping-definitions-in-aem}

在AEM的標準安裝中，您可以找到檔案夾：

`/etc/map/http`

這是定義HTTP協定映射時使用的結構。 您可以針對 `sling:Folder`您要映射的任何其 `/etc/map` 他通訊協定，在下面建立其他資料夾()。

#### 設定內部重新導向至/content {#configuring-an-internal-redirect-to-content}

要建立將任何請求前置詞為https://localhost:4503/的映射，請執行以下操 `/content`作：

1. 使用CRXDE導航至 `/etc/map/http`。

1. 建立新節點：

   * **Type** `sling:Mapping`This node type is indered for such mappings, is its not mandactory.

   * **名稱**`localhost_any`

1. 按一下「 **全部儲存**」。
1. **將** 下列屬性新增至此節點：

   * **名稱**`sling:match`

      * **類型**`String`

      * **值**`localhost.4503/`
   * **名稱**`sling:internalRedirect`

      * **類型**`String`

      * **值**`/content/`


1. 按一下「 **全部儲存**」。

這將處理下列請求：如`localhost:4503/geometrixx/en/products.html`下所示：有人`localhost:4503/content/geometrixx/en/products.html`要求我。

>[!NOTE]
>
>請參 [閱Sling Documentation中的Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) ，以取得sling屬性的詳細資訊，以及如何設定這些屬性。

>[!NOTE]
>
>您可以使 `/etc/map.publish` 用來保存發佈環境的配置。 然後必須複製這些檔案，並為發佈環境的 `/etc/map.publish`Apache Sling Resource Resolver **的Mapping Location** （對應位置）設定新位置( [](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) )。

