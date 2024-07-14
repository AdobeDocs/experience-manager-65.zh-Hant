---
title: 頁面匯出工具
description: 瞭解如何使用Adobe Experience Manager (AEM)頁面匯出工具。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# 頁面匯出工具{#the-page-exporter}

Adobe Experience Manager (AEM)可讓您將頁面匯出為包含影像、`.js`和`.css`檔案的完整網頁。

完成設定後，您可在URL中將`html`取代為`export.zip`，以請求從瀏覽器匯出頁面。 這會產生封存(zip)檔案，其中包含以html格式呈現的頁面以及參照的資產。 頁面中的所有路徑（例如，影像的路徑）都會重新寫入，以指向封存中包含的檔案或伺服器上的資源。 接著，您就可以從瀏覽器下載封存(zip)檔案。

>[!NOTE]
>
>根據您的瀏覽器和設定，下載內容會是：
>
>* 封存檔案(`<page-name>.export.zip`)
>* 資料夾(`<page-name>`)；實際上封存檔案已經展開

## 匯出頁面 {#exporting-a-page}

下列步驟說明如何匯出頁面，並假設您的網站存在匯出範本。 匯出範本會定義頁面的匯出方式，且是您網站專屬的。 若要建立匯出範本，請參閱[為您的網站建立頁面匯出程式組態](#creating-a-page-exporter-configuration-for-your-site)。

若要匯出頁面：

1. 導覽至&#x200B;**網站**&#x200B;主控台中的必要頁面。

1. 選取頁面，然後開啟&#x200B;**屬性**&#x200B;對話方塊。

1. 選取&#x200B;**進階**&#x200B;標籤。

1. 展開&#x200B;**匯出**欄位以選取匯出範本。
為您的網站選取所需的範本，然後確認**確定**。

1. 選取&#x200B;**儲存並關閉**&#x200B;以關閉頁面屬性對話方塊。

1. 要求匯出頁面，在URL中將尾碼`html`取代為`export.zip`。

   例如：
   * localhost：4502/content/we-retail/language-masters/en.html

   存取方式：
   * localhost：4502/content/we-retail/language-masters/en.export.zip

1. 將封存檔案下載至您的檔案系統。

1. 如有必要，請在您的檔案系統中解壓縮檔案。 展開時，會有一個與所選頁面同名的資料夾。 此資料夾包含：

   * 子資料夾`content`是反映存放庫中頁面路徑的一系列子資料夾的根目錄

      * 在此結構中有所選頁面(`<page-name>.html`)的html檔案

   * 根據匯出範本中的設定，可找到其他資源（`.js`個檔案、`.css`個檔案、影像等）

1. 在瀏覽器中開啟頁面html檔案(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)，以便檢查轉譯。

## 建立網站的頁面匯出工具組態 {#creating-a-page-exporter-configuration-for-your-site}

頁面匯出工具是以[內容同步架構](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)為基礎。 **頁面屬性**&#x200B;對話方塊中可用的設定是定義頁面所需相依性的匯出範本。

觸發頁面匯出時，會參考匯出範本。 頁面路徑和設計路徑都會動態套用。 然後使用標準Content Sync功能建立zip檔案。

現成的AEM安裝包含`/etc/contentsync/templates/default`下的預設範本。

* 此範本是在存放庫中找不到匯出範本時的後援範本。

* `default`範本會顯示如何設定頁面匯出，以作為新匯出範本的基礎。

* 若要在瀏覽器中以JSON格式檢視範本的節點結構，請要求下列URL：
  `http://localhost:4502/etc/contentsync/templates/default.json`

建立頁面匯出工具範本最簡單的方法是：

* 複製`default`範本，

* 指派適合您網站的新名稱，

* 然後進行必要的更新。

若要建立全新的範本：

1. 在&#x200B;**CRXDE Lite**&#x200B;中，在`/etc/contentsync/templates`底下建立節點：

   * `Name`：適合您網站的名稱；例如，`<mysite>`。 選擇頁面匯出程式範本時，名稱會顯示在頁面屬性對話方塊中。

   * `Type`: `nt:unstructured`

2. 在範本節點（此處稱為`mysite`）下方，使用下述設定節點建立節點結構。

## 為您的頁面啟用頁面匯出工具範本 {#activating-a-page-exporter-configuration-for-your-pages}

設定範本後，使其可用：

1. 在CRXDE中導覽至`/content`分支中的必要頁面。 這可以是個別頁面，或是子樹狀結構的根頁面。

1. 在頁面的`jcr:content`節點上，建立屬性：
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`：範本的路徑；例如： `/etc/contentsync/templates/mysite`

### 頁面匯出工具組態節點 {#page-exporter-configuration-nodes}

範本包含節點結構，因為它使用[Content Sync架構](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)。 每個節點都有`type`屬性，定義了zip檔案建立過程中的特定動作。

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

下列節點可用來建置匯出範本：

* `page`
頁面節點用於將頁面html複製到zip檔案。 它具有下列特性：

   * 必要節點。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 已定義屬性`Name`設定為`page`。
   * 節點型別為`nt:unstructured`

  `page`節點有下列屬性：

   * 以值`pages`設定的`type`屬性。

   * 它沒有`path`屬性，因為目前的頁面路徑會動態複製到設定。
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重新寫入節點會定義在匯出頁面中重新寫入連結的方式。 重寫的連結可以指向zip檔案中包含的檔案或伺服器上的資源。
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
設計節點用於複製用於匯出頁面的設計。 它具有下列特性：

   * 選填。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 已定義屬性`Name`設定為`design`。
   * 節點型別為`nt:unstructured`。

  `design`節點有下列屬性：

   * 設定為值`copy`的`type`屬性。

   * 它沒有`path`屬性，因為目前的頁面路徑會動態複製到設定。

* `generic`
泛型節點用於將資源（如clientlibs `.js`或`.css`檔案）複製到zip檔案。 它具有下列特性：

   * 選填。
   * 位於`/etc/contentsync/templates/<mysite>`下方。
   * 沒有特定名稱。
   * 節點型別為`nt:unstructured`。
   * 具有`type`屬性和`type`相關屬性。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  例如，下列設定節點會將`mysite.clientlibs.js`檔案複製到zip檔：

  ```xml
  "mysite.clientlibs.js": {
      "extension": "js",
      "type": "clientlib",
      "path": "/etc/designs/mysite/clientlibs",
      "jcr:primaryType": "nt:unstructured"
  }
  ```

**實作自訂組態**

您也可以使用自訂設定。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

若要符合某些特定需求，請實作[自訂更新處理常式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## 以程式匯出頁面 {#programmatically-exporting-a-page}

若要以程式設計方式匯出頁面，您可以使用[PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服務。 此服務可讓您：

* 匯出頁面並寫入HTTP servlet回應。
* 匯出頁面，並將zip檔案儲存在特定位置。

繫結至`export`選取器及`zip`延伸模組的servlet使用PageExporter服務。

## 疑難排解 {#troubleshooting}

如果您在下載zip檔案時遇到問題，可以刪除存放庫中的`/var/contentsync`節點，然後再次傳送匯出請求。
