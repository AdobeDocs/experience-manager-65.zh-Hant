---
title: 頁面匯出器
description: 瞭解如何使用AEM Page Exporter。
translation-type: tm+mt
source-git-commit: 6aee1506b54a932bae8f2521fce4488de7d2a52a
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# 頁面匯出器{#the-page-exporter}

AEM可讓您將頁面匯出為完整的網頁，包括影像、`.js`和`.css`檔案。

在設定後，您會在URL中將`html`取代為`export.zip`，從瀏覽器要求匯出頁面。 這會產生封存(zip)檔案，其中包含以html格式呈現的頁面，以及參考的資產。 頁面中的所有路徑（例如，到映像的路徑）都會被重寫，以指向歸檔檔案中包含的檔案或伺服器上的資源。 然後，可從您的瀏覽器下載封存(zip)檔案。

>[!NOTE]
>
>視您的瀏覽器和設定而定，下載內容會是：
>* 存檔檔案(`<page-name>.export.zip`)
>* 資料夾(`<page-name>`);有效地擴展了歸檔檔案


## 導出頁面{#exporting-a-page}

下列步驟說明如何匯出頁面，並假設您的網站存在匯出範本。 匯出範本會定義頁面的匯出方式，並且是您網站專屬的。 要建立導出模板，請參閱[為站點](#creating-a-page-exporter-configuration-for-your-site)建立頁導出器配置部分。

若要匯出頁面：

1. 導覽至&#x200B;**Sites**&#x200B;主控台中的必要頁面。

1. 選擇該頁，然後開啟&#x200B;**屬性**&#x200B;對話框。

1. 選擇&#x200B;**Advanced**&#x200B;標籤。

1. 展開&#x200B;**Export**欄位以選取匯出範本。
選擇網站所需的範本，然後使用**OK**&#x200B;確認。

1. 選擇&#x200B;**保存並關閉**&#x200B;以關閉頁面屬性對話框。

1. 請求要匯出的頁面，在URL中以`export.zip`取代字尾`html`。

   例如：
   * localhost:4502/content/we-retail/language-masters/en.html

   存取方式：
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. 將存檔檔案下載到檔案系統。

1. 在您的檔案系統中，視需要解壓縮檔案。 展開後，會有與選取頁面同名的檔案夾。 此資料夾包含：

   * 子資料夾`content`，它是反映儲存庫中頁面路徑的一系列子資料夾的根

      * 在此結構中，有選定頁面的html檔案(`<page-name>.html`)
   * 其他資源（`.js`檔案、`.css`檔案、影像等） 是根據匯出範本中的設定所定位


1. 在瀏覽器中開啟頁面html檔案(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)以檢查演算。

## 為您的站點{#creating-a-page-exporter-configuration-for-your-site}建立頁面導出器配置

頁面導出器基於[內容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。 **頁面屬性**&#x200B;對話方塊中可用的配置是導出模板，用於定義頁面所需的從屬關係。

觸發頁面匯出時，會參考匯出範本，並動態套用頁面路徑和設計路徑。 然後使用標準的「內容同步」功能建立zip檔案。

現成可用的AEM安裝包含`/etc/contentsync/templates/default`下方的預設範本。

* 當在儲存庫中未找到導出模板時，此模板是備用模板。

* `default`範本顯示如何設定頁面匯出，以做為新匯出範本的基礎。

* 若要以JSON格式檢視瀏覽器中範本的節點結構，請要求下列URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

建立新頁面匯出器範本最簡單的方法是：

* 複製`default`範本，

* 為您的網站指定新名稱，

* 然後進行必要的更新。

若要建立全新範本：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在`/etc/contentsync/templates`下建立一個節點：

   * `Name`:適合您網站的名稱；例如， `<mysite>`。選擇頁面導出器模板時，名稱將出現在頁面屬性對話框中。

   * `Type`: `nt:unstructured`

2. 在模板節點（在此`mysite`中調用）下，使用下面介紹的配置節點建立節點結構。

## 為您的頁面啟用頁面匯出器範本{#activating-a-page-exporter-configuration-for-your-pages}

在設定範本後，您必須將它提供：

1. 在CRXDE中，導覽至`/content`分支中的必要頁面。 這可以是個別頁面，或子樹的根頁面。

1. 在頁面的`jcr:content`節點上，建立屬性：
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`:範本路徑；例如：  `/etc/contentsync/templates/mysite`

### 頁面導出器配置節點{#page-exporter-configuration-nodes}

範本由節點結構組成，因為它使用[內容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。  每個節點都有`type`屬性，可定義zip檔案建立過程中的特定操作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

以下節點可用於構建導出模板：

* `page`
頁面節點用於將頁面html複製到zip檔案。它具有以下特點：

   * 是強制節點。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 定義時，屬性`Name`設定為`page`。
   * 節點類型為`nt:unstructured`

   `page`節點具有以下屬性：

   * 設定了`type`值的`pages`屬性。

   * 它沒有`path`屬性，因為當前頁面路徑是動態複製到配置的。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重寫節點定義如何在導出的頁面中重寫連結。重寫的連結可以指向包含在zip檔案中的檔案或指向伺服器上的資源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
設計節點用於複製用於導出頁面的設計。它具有以下特點：

   * 是可選的。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 定義時，屬性`Name`設定為`design`。
   * 節點類型為`nt:unstructured`。

   `design`節點具有以下屬性：

   * 將`type`屬性設定為值`copy`。

   * 它沒有`path`屬性，因為當前頁路徑是動態複製到配置的。


* `generic`
通用節點用於複製諸如clientlibs等資源 
`.js` 或檔 `.css` 案到zip檔案。它具有以下特點：

   * 是可選的。
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

您也可以使用自訂設定。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

為符合某些特定需求，您可能需要實作[自訂更新處理常式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以程式設計方式匯出頁面{#programmatically-exporting-a-page}

若要以程式設計方式匯出頁面，您可使用[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服務。 此服務可讓您：

* 匯出頁面並寫入HTTP servlet回應。
* 匯出頁面，並將zip檔案儲存在特定位置。

綁定到`export`選擇器和`zip`副檔名的servlet使用PageExporter服務。

## 疑難排解 {#troubleshooting}

如果您在下載zip檔案時遇到問題，可以刪除儲存庫中的`/var/contentsync`節點，然後再次傳送匯出請求。
