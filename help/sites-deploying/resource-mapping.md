---
title: 資源對應
description: 瞭解如何使用資源對應為Adobe Experience Manager定義重新導向、虛名URL和虛擬主機。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# 資源對應{#resource-mapping}

資源對應可用來定義Adobe Experience Manager (AEM)的重新導向、虛名URL和虛擬主機。

例如，您可以使用這些對應來：

* 請在所有要求加上前置詞`/content`，使您的網站訪客無法看見內部結構。
* 定義重新導向，將網站`/content/en/gateway`頁面的所有要求重新導向至`https://gbiv.com/`。

一個可能的HTTP對應會為所有要求加上前置詞`localhost:4503`和`/content`。 類似這樣的對應可用於對網站的訪客隱藏內部結構，因為它允許：

`localhost:4503/content/we-retail/en/products.html`

存取方式：

`localhost:4503/we-retail/en/products.html`

因為對應會自動將前置詞`/content`新增至`/we-retail/en/products.html`。

>[!CAUTION]
>
>虛名URL不支援規則運算式模式。

>[!NOTE]
>
>如需進一步資訊，請參閱Sling檔案以及資源解析[&#128279;](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)和[資源](https://sling.apache.org/documentation/the-sling-engine/resources.html)的對應。

## 檢視對應定義 {#viewing-mapping-definitions}

「JCR資源解析器」會評估（由上到下）以尋找相符專案的對應表單兩個清單。

可以在Felix主控台的&#x200B;**JCR ResourceResolver**&#x200B;選項下檢視這些清單（連同組態資訊）；例如`https://<*host*>:<*port*>/system/console/jcrresolver`：

* 設定
顯示目前的設定（如[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)所定義）。

* 設定測試
這可讓您輸入URL或資源路徑。 按一下&#x200B;**解析**&#x200B;或&#x200B;**對應**&#x200B;以確認系統如何轉換專案。

* **解析器對應專案**
ResourceResolver.resolve方法用來將URL對應至資源的專案清單。

* **對應對應專案**
ResourceResolver.map方法用來將資源路徑對應至URL的專案清單。

這兩個清單會顯示各種專案，包括應用程式所定義的預設專案。 這些通常旨在簡化使用者的URL。

清單會以&#x200B;**Pattern** （符合要求的規則運算式）與定義要強制重新導向的&#x200B;**Replacement**&#x200B;配對。

例如：

**模式** `^[^/]+/[^/]+/welcome$`

將觸發：

**取代** `/libs/cq/core/content/welcome.html`。

若要重新導向請求：

`https://localhost:4503/welcome` »

至：

`https://localhost:4503/libs/cq/core/content/welcome.html`

新的對應定義會在存放庫中建立。

>[!NOTE]
>
>有許多資源可協助說明如何定義規則運算式。 例如，[https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM中建立對應定義 {#creating-mapping-definitions-in-aem}

在AEM的標準安裝中，您可以找到資料夾：

`/etc/map/http`

這是定義HTTP通訊協定的對應時使用的結構。 可以在`/etc/map`下為您要對應的任何其他通訊協定建立其他資料夾(`sling:Folder`)。

#### 設定內部重新導向至/content {#configuring-an-internal-redirect-to-content}

若要建立以`/content`為任何https://localhost:4503/請求前置詞的對應：

1. 使用CRXDE導覽至`/etc/map/http`。

1. 建立節點：

   * **型別** `sling:Mapping`
此節點型別適用於此類對應，但並不強制使用。

   * **名稱** `localhost_any`

1. 按一下&#x200B;**「儲存全部」**。
1. **新增**&#x200B;下列屬性至此節點：

   * **名稱** `sling:match`

      * **型別** `String`

      * **值** `localhost.4503/`

   * **名稱** `sling:internalRedirect`

      * **型別** `String[]`

      * **值** `/content/`

1. 按一下&#x200B;**「儲存全部」**。

這會處理如下請求：
`localhost:4503/geometrixx/en/products.html`
就好像：
`localhost:4503/content/geometrixx/en/products.html`
已被要求。

>[!NOTE]
>
>請參閱Sling檔案中的[資源](https://sling.apache.org/documentation/the-sling-engine/resources.html)，以取得有關可用Sling屬性以及如何設定這些屬性的進一步資訊。

>[!NOTE]
>
>您可以使用`/etc/map.publish`來儲存發佈環境的設定。 必須復寫這些專案，並為發佈環境的[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的&#x200B;**對應位置**&#x200B;設定新位置(`/etc/map.publish`)。
