---
title: 頁面匯出工具
description: 了解如何使用AEM Page Exporter。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# 頁面導出器{#the-page-exporter}

AEM可讓您將頁面匯出為完整的網頁，包含影像、`.js`和`.css`檔案。

設定後，您會在URL中將`html`取代為`export.zip`，以從瀏覽器要求頁面匯出。 這會產生封存(zip)檔案，其中包含以html格式呈現的頁面，以及參照的資產。 頁面中的所有路徑（例如，到影像的路徑）都會被重寫，以指向包含在存檔中的檔案，或指向伺服器上的資源。 然後，您就可以從瀏覽器下載封存(zip)檔案。

>[!NOTE]
>
>視您的瀏覽器和設定而定，下載會是：
>* 存檔檔案(`<page-name>.export.zip`)
>* 資料夾(`<page-name>`);有效地擴展了歸檔檔案


## 匯出頁面{#exporting-a-page}

下列步驟說明如何匯出頁面，並假設您的網站有匯出範本。 匯出範本會定義頁面的匯出方式，且是您網站專屬的。 要建立導出模板，請參閱為您的站點](#creating-a-page-exporter-configuration-for-your-site)建立頁面導出器配置部分。[

要導出頁面，請執行以下操作：

1. 導覽至&#x200B;**Sites**&#x200B;主控台中的必要頁面。

1. 選擇該頁，然後開啟&#x200B;**屬性**&#x200B;對話框。

1. 選擇&#x200B;**Advanced**&#x200B;頁簽。

1. 展開&#x200B;**Export**欄位以選取匯出範本。
選取網站所需的範本，然後使用**OK**&#x200B;確認。

1. 選擇&#x200B;**Save &amp; Close**&#x200B;以關閉頁面屬性對話框。

1. 請求要匯出的頁面，在URL中將尾碼`html`取代為`export.zip`。

   例如：
   * localhost:4502/content/we-retail/language-masters/en.html

   可透過下列方式存取：
   * localhost:4502/content/we-retail/language-masters/en.export


1. 將存檔檔案下載到檔案系統。

1. 在您的檔案系統中，視需要解壓縮檔案。 展開後，會出現與所選頁面同名的資料夾。 此資料夾包含：

   * 子資料夾`content`，它是反映儲存庫中頁面路徑的一系列子資料夾的根

      * 在此結構中，有選定頁面的html檔案(`<page-name>.html`)
   * 其他資源（`.js`檔案、`.css`檔案、影像等） 是根據匯出範本中的設定來定位


1. 在瀏覽器中開啟頁面html檔案(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)以檢查呈現。

## 為您的站點{#creating-a-page-exporter-configuration-for-your-site}建立頁面導出器配置

頁面匯出器以[內容同步架構](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)為基礎。 **頁面屬性**&#x200B;對話方塊中可用的設定是可定義頁面所需相依性的匯出範本。

觸發頁面匯出時，會參考匯出範本，並動態套用頁面路徑和設計路徑。 然後會使用標準的「內容同步」功能來建立zip檔案。

現成可用的AEM安裝包含`/etc/contentsync/templates/default`下的預設範本。

* 若儲存庫中找不到匯出範本，此範本即為後援範本。

* `default`範本會顯示如何設定頁面匯出，以便作為新匯出範本的基礎。

* 若要以JSON格式檢視瀏覽器中範本的節點結構，請要求下列URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

建立新頁面匯出器範本最簡單的方法是：

* 複製`default`範本，

* 為您的網站指派合適的新名稱，

* 然後進行必要的更新。

若要建立全新範本：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在`/etc/contentsync/templates`下建立節點：

   * `Name`:與您的網站相稱的名稱；例如 `<mysite>`。選擇頁面導出器模板時，該名稱將出現在頁面屬性對話框中。

   * `Type`: `nt:unstructured`

2. 在範本節點下方（稱為`mysite`），使用下述配置節點建立節點結構。

## 為您的頁{#activating-a-page-exporter-configuration-for-your-pages}激活頁面導出器模板

設定範本後，您必須讓範本可供使用：

1. 在CRXDE中，導覽至`/content`分支中的必要頁面。 這可以是個別頁面，或子樹的根頁面。

1. 在頁面的`jcr:content`節點上建立屬性：
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`:範本路徑；例如：  `/etc/contentsync/templates/mysite`

### 頁面導出器配置節點{#page-exporter-configuration-nodes}

範本包含節點結構，因為它使用[內容同步架構](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。  每個節點都有一個`type`屬性，定義了zip檔案建立過程中的特定操作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

以下節點可用來建立匯出範本：

* `page`
頁面節點可用來將頁面html複製到zip檔案。其特點如下：

   * 是強制節點。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 已使用設為`page`的屬性`Name`來定義。
   * 節點類型為`nt:unstructured`

   `page`節點具有以下屬性：

   * 以`pages`值設定的`type`屬性。

   * 它沒有`path`屬性，因為目前頁面路徑會動態複製到設定。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重寫節點定義如何在匯出的頁面中重寫連結。重寫的連結可以指向zip檔案中包含的檔案或指向伺服器上的資源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
設計節點用於複製用於導出頁面的設計。其特點如下：

   * 為選用。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 以設為`design`的屬性`Name`定義。
   * 節點類型為`nt:unstructured`。

   `design`節點具有以下屬性：

   * 設為`copy`值的`type`屬性。

   * 它沒有`path`屬性，因為目前頁面路徑會動態複製到設定。


* `generic`
一般節點可用來複製clientlibs等資源 
`.js` 或 `.css` 檔案。其特點如下：

   * 為選用。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 沒有特定名稱。
   * 節點類型為`nt:unstructured`。
   * 具有`type`屬性和`type`相關屬性。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例如，以下配置節點將`mysite.clientlibs.js`檔案複製到zip檔案：

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**實作自訂設定**

您也可以進行自訂設定。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

為了滿足某些特定需求，您可能需要實作[自訂更新處理常式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以程式設計方式導出頁面{#programmatically-exporting-a-page}

若要以程式設計方式匯出頁面，您可以使用[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服務。 此服務可讓您：

* 匯出頁面並寫入HTTP servlet回應。
* 匯出頁面並在特定位置儲存zip檔案。

綁定到`export`選擇器和`zip`擴展的Servlet使用PageExporter服務。

## 疑難排解 {#troubleshooting}

如果您在下載zip檔案時遇到問題，可以刪除存放庫中的`/var/contentsync`節點，然後再次傳送匯出請求。
