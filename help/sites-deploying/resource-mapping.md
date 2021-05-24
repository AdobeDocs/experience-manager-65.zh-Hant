---
title: 資源映射
seo-title: 資源映射
description: 了解如何使用資源對應來定義AEM的重新導向、虛名URL和虛擬主機。
seo-description: 了解如何使用資源對應來定義AEM的重新導向、虛名URL和虛擬主機。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: 設定
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# 資源映射{#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以將這些對應用於：

* 為所有要求加上前置詞`/content`，以便對網站的訪客隱藏內部結構。
* 定義重新導向，以便將所有要求重新導向至您網站的`/content/en/gateway`頁面。`https://gbiv.com/`

一個可能的HTTP對應會將所有要求以`/content`前置詞`localhost:4503`。 像這樣的對應可用來隱藏內部結構，讓網站的訪客無法看到它允許的內容：

`localhost:4503/content/we-retail/en/products.html`

以使用：

`localhost:4503/we-retail/en/products.html`

因為對應會自動將首碼`/content`新增至`/we-retail/en/products.html`。

>[!CAUTION]
>
>虛名URL不支援規則運算式模式。

>[!NOTE]
>
>如需詳細資訊，請參閱Sling檔案，以及[資源解析度](https://sling.apache.org/site/resources.html)和[資源](https://sling.apache.org/site/mappings-for-resource-resolution.html)的對應。

## 查看映射定義{#viewing-mapping-definitions}

對應會形成兩個清單，JCR資源解析器會評估這些清單（由上到下）以尋找相符項目。

您可以在Felix主控台的&#x200B;**JCR ResourceResolver**&#x200B;選項下檢視這些清單（連同設定資訊）;例如， `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 設定
顯示目前的設定（如[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)所定義）。

* 配置測試
這可讓您輸入URL或資源路徑。 按一下**解析**&#x200B;或&#x200B;**映射**&#x200B;以確認系統將如何轉換條目。

* **解析程**
式映射條目ResourceResolver.resolve方法將URL映射到資源時使用的條目清單。

* **映射映**
射條目ResourceResolver.map方法用於將資源路徑映射到URL的條目清單。

這兩個清單顯示各種條目，包括由應用程式定義為預設的條目。 這通常是為了簡化使用者的URL。

清單將&#x200B;**Pattern**（與請求匹配的規則表達式）與&#x200B;**Replacement**&#x200B;配對，後者定義了對施加的重定向。

例如：

**圖樣** `^[^/]+/[^/]+/welcome$`

將觸發：

**取代** `/libs/cq/core/content/welcome.html`。

若要重新導向請求：

`https://localhost:4503/welcome` &quot;

至:

`https://localhost:4503/libs/cq/core/content/welcome.html`

系統會在存放庫內建立新的對應定義。

>[!NOTE]
>
>有許多資源可協助說明如何定義規則運算式；例如[https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM {#creating-mapping-definitions-in-aem}中建立對應定義

在標準的AEM安裝中，您可以找到資料夾：

`/etc/map/http`

這是定義HTTP通訊協定的對應時使用的結構。 可在`/etc/map`下建立其他資料夾(`sling:Folder`)，以用於您要映射的任何其他協定。

#### 設定內部重新導向至/content {#configuring-an-internal-redirect-to-content}

若要建立將任何要求以`/content`加上前置詞的對應至https://localhost:4503/:

1. 使用CRXDE導覽至`/etc/map/http`。

1. 建立新節點：

   * **** `sling:Mapping`
類型此節點類型用於此類映射，但其用途不是強制性的。

   * **名稱** `localhost_any`

1. 按一下「**全部保存**」。
1. **** 將下列屬性新增至此節點：

   * **名稱** `sling:match`

      * **類型** `String`

      * **值** `localhost.4503/`
   * **名稱** `sling:internalRedirect`

      * **類型** `String`

      * **值** `/content/`


1. 按一下「**全部保存**」。

這會處理下列請求：
`localhost:4503/geometrixx/en/products.html`
如同：
`localhost:4503/content/geometrixx/en/products.html`
被請求。

>[!NOTE]
>
>請參閱Sling檔案中的[資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) ，進一步了解可用的Sling屬性及其設定方式。

>[!NOTE]
>
>您可以使用`/etc/map.publish`來保留發佈環境的設定。 接著，必須復寫這些變數，並為發佈環境的[Apache Sling資源解析器](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的&#x200B;**對應位置**&#x200B;設定的新位置(`/etc/map.publish`)。
