---
title: 頁面匯出器
seo-title: 頁面匯出器
description: 瞭解如何使用AEM Page Exporter。
seo-description: 瞭解如何使用AEM Page Exporter。
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 頁面匯出器{#the-page-exporter}

AEM可讓您將頁面匯出為完整的網頁，包括影像、.js和。css檔案。

在設定匯出後，您只需在瀏覽器中以URL中的取代來請求頁面， `html``export.zip` 就可取得包含以html格式呈現的頁面和參考資產的Zip檔案下載。 頁面中的所有路徑（例如影像路徑）都會重寫，以指向zip檔案中包含的檔案或伺服器上的資源。

## 匯出頁面 {#exporting-a-page}

下列步驟說明如何匯出頁面，並假設您的網站存在匯出設定範本。 設定範本會定義匯出頁面的方式，且是您網站專屬的。 要建立配置模板，請參 [閱為站點建立頁導出器配置](#creating-a-page-exporter-configuration-for-your-site) 。

若要匯出頁面：

1. 在您的瀏覽器中，開啟頁面。 例如：
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. 開啟頁面屬性對話方塊，選取「進 **階** 」標籤並展開「 **匯出** 」欄位集。

1. 按一下放大鏡表徵圖並選擇配置模板。 選取 **geometrixx** 範本，因為它是Geometrixx網站的預設範本。 按一下 **確定**。

1. 按一 **下「確定** 」以關閉頁面屬性對話方塊。
1. 在URL中以取代 `html` 來請 `export.zip` 求頁面。

1. 將檔案 `<page-name>.export.zip` 下載至您的檔案系統。

1. 在您的檔案系統中，解壓縮檔案：

   * 頁面html檔案( `<page-name>.html`)可在 `<unzip-dir>/<page-path>`
   * 其他資源（.js檔案、.css檔案、影像……）會根據匯出範本中的設定進行定位。 在此範例中，有些資源在下 `<unzip-dir>/etc`面，有些在下 `<unzip-dir>/<page-path>`面。

1. 在瀏覽器中開啟頁面html `<unzip-dir>/<page-path>.html`檔案()以檢查演算。

## 為您的網站建立頁面匯出器設定 {#creating-a-page-exporter-configuration-for-your-site}

頁面匯出器是以「內容同步」架構為基礎。 頁面屬性對話框中可用的配置是配置模板。 它們定義了頁面的所有必需依賴項。 觸發頁面匯出時，會使用設定範本，並動態地將頁面路徑和設計路徑套用至設定。 然後使用標準的「內容同步」功能建立zip檔案。

AEM內嵌一些範本，包括：

* 預設值 `/etc/contentsync/templates/default`。 此範本：

   * 在儲存庫中未找到配置模板時是備用模板。
   * 可作為新配置模板的基礎。

* 專用於 **Geometrixx網站的** ，網址為 `/etc/contentsync/templates/geometrixx`。 此範本可做為建立新範本的範例。

要建立頁面導出器配置模板，請執行以下操作：

1. 在 **CRXDE Lite中**，建立下方的節點 `/etc/contentsync/templates`:

   * 名稱：例如， `mysite`。 選擇頁面導出器模板時，名稱將出現在頁面屬性對話框中。
   * 類型: `nt:unstructured`

1. 在範本節點（在此處調用） `mysite`下，使用下面介紹的配置節點建立節點結構。

### 頁面導出器配置節點 {#page-exporter-configuration-nodes}

配置模板由節點結構組成。 每個節點都有 `type` 一個屬性，可定義zip檔案建立過程中的特定操作。 有關type屬性的詳細資訊，請參閱「內容同步框架」頁中的「配置類型概述」部分。

以下節點可用於構建導出配置模板：

**page node** （頁面節點）頁面節點用於將頁面html複製到zip檔案。 它具有以下特點：

* 是強制節點。
* 位於下方 `/etc/contentsync/templates/<sitename>`。
* 其名稱為 `page`。
* 其節點類型為 `nt:unstructured`

節 `page` 點具有以下屬性：

* 與 `type` 值一起設定的屬性 `pages`。

* 它沒有屬性， `path` 因為目前頁面路徑會動態複製至設定。

* 其他屬性在Content sync框架的「配置類型概述」部分中介紹。

**rewrite node** 重寫節點定義如何在導出的頁面中重寫連結。 重寫的連結可以指向包含在zip檔案中的檔案或指向伺服器上的資源。

請參閱「內容同步」頁面，以取得節點的完整說 `rewrite` 明。

**設計節點** ：設計節點用於複製用於導出頁面的設計。 它具有以下特點：

* 是可選的。
* 位於下方 `/etc/contentsync/templates/<sitename>`。
* 其名稱為 `design`。
* 其節點類型為 `nt:unstructured`。

節 `design` 點具有以下屬性：

* 設 `type` 置為值的屬性 `copy`。

* 它沒有屬性， `path` 因為目前頁面路徑會動態複製至設定。

**一般節點** ：一般節點可用來將clientlibs .js或。css檔案等資源複製到zip檔案。 它具有以下特點：

* 是可選的。
* 位於下方 `/etc/contentsync/templates/<sitename>`。
* 沒有特定名稱。
* 其節點類型為 `nt:unstructured`。
* 具有Content `type` Sync框架 `type` 的「配置類型概述」部分中定義的屬性和任何相關屬性。

例如，下列設定節點會將geometrixx clientlibs .js檔案複製至zip檔案：

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

Geometrixx **** page export設定範本會顯示如何設定頁面匯出。 若要以json格式檢視瀏覽器中範本的節點結構，請要求下列URL:

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**實作自訂設定**

如您在節點結構中所注意的， **Geometrixx** page export配置模板有一個 `logo` 將屬性設定為 `type` 的節點 `image`。 這是已建立的特殊組態類型，可將影像標誌複製至zip檔案。 為符合某些特定需求，您可能需要實作自訂屬 `type` 性：若要這麼做，請參閱「內容同步」頁面中的「實作自訂更新處理常式」區段。

## 以程式設計方式匯出頁面 {#programmatically-exporting-a-page}

若要以程式設計方式匯出頁面，您可以使 [用PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服務。 此服務可讓您：

* 匯出頁面並寫入HTTP servlet回應。
* 匯出頁面，並將zip檔案儲存在特定位置。

綁定到選擇器和擴展 `export` 名的Servlet使 `zip` 用PageExporter服務。

## 疑難排解 {#troubleshooting}

如果您在下載zip檔案時遇到問題，可以刪除儲存庫中的 `/var/contentsync` 節點，然後再次傳送匯出請求。

