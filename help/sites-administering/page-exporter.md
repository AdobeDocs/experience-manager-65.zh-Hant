---
title: 頁面導出器
description: 瞭解如何使用頁面導AEM出器。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# 頁面導出器{#the-page-exporter}

允AEM許將頁面導出為包括影像的完整網頁， `.js` 和 `.css` 的子菜單。

配置後，您會通過替換 `html` 與 `export.zip` 的子菜單。 這將生成一個存檔(zip)檔案，其中包含以html格式呈現的頁面以及引用的資產。 重寫頁中的所有路徑（例如，到映像的路徑），以指向存檔中包含的檔案或指向伺服器上的資源。 然後，可以從瀏覽器下載存檔(zip)檔案。

>[!NOTE]
>
>根據您的瀏覽器和設定，下載內容將為：
>* 存檔檔案(`<page-name>.export.zip`)
>* 資料夾(`<page-name>`);有效地擴展了存檔檔案


## 導出頁面 {#exporting-a-page}

以下步驟說明如何導出頁面，並假定站點存在導出模板。 導出模板定義了導出頁面的方式並特定於您的站點。 要建立導出模板，請參閱 [為站點建立頁面導出器配置](#creating-a-page-exporter-configuration-for-your-site) 的子菜單。

要導出頁面：

1. 導航至 **站點** 控制台。

1. 選擇頁面，然後開啟 **屬性** 對話框。

1. 選擇 **高級** 頁籤。

1. 展開 **導出** 的子菜單。
選擇站點所需的模板，然後使用 **確定**。

1. 選擇 **保存並關閉** 按鈕。

1. 請求要導出的頁面，替換尾碼 `html` 與 `export.zip` 的子菜單。

   例如：
   * 本地主機：4502/content/we-retail/language-masters/en.html

   通過以下方式訪問：
   * 本地主機：4502/content/we-retail/language-masters/en.export.zip


1. 將存檔檔案下載到檔案系統。

1. 在檔案系統中，如有必要，解壓檔案。 展開後，將存在與所選頁面同名的資料夾。 此資料夾包含：

   * 子資料夾 `content`，是反映儲存庫中頁面路徑的一系列子資料夾的根

      * 在此結構中，有選定頁面的html檔案(`<page-name>.html`)
   * 其他資源(`.js` 檔案， `.css` 檔案、影像等) 根據導出模板中的設定進行定位


1. 開啟頁面html檔案(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)以檢查呈現。

## 為站點建立頁面導出器配置 {#creating-a-page-exporter-configuration-for-your-site}

頁面導出器基於 [內容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。 中可用的配置 **頁面屬性** 對話框是導出模板，用於定義頁面所需的依賴項。

觸發頁面導出時，將引用導出模板，並動態應用頁面路徑和設計路徑。 然後，使用標準內容同步功能建立zip檔案。

現成安裝包AEM括預設模板 `/etc/contentsync/templates/default`。

* 在資料庫中找不到導出模板時，此模板是回退模板。

* 的 `default` 該模板顯示如何配置頁面導出，因此可以作為新導出模板的基礎。

* 要以JSON格式查看瀏覽器中模板的節點結構，請請求以下URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

建立新頁面導出器模板的最簡單方法是：

* 複製 `default` 模板，

* 指定與您的站點相適應的新名稱，

* 然後進行所需的更新。

要建立全新模板：

1. 在 **CRXDE Lite**，在下面建立節點 `/etc/contentsync/templates`:

   * `Name`:與您的網站相稱的名稱；比如說， `<mysite>`。 選擇頁面導出器模板時，該名稱將出現在頁面屬性對話框中。

   * `Type`: `nt:unstructured`

2. 在模板節點下，在此調用 `mysite`，使用下面所述的配置節點建立節點結構。

## 為頁面激活頁面導出器模板 {#activating-a-page-exporter-configuration-for-your-pages}

配置模板後，您需要使其可用：

1. 在CRXDE中，導航到 `/content` 分支。 這可以是單個頁面，也可以是子樹的根頁面。

1. 在 `jcr:content` 該頁的節點建立屬性：
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`:模板路徑；例如： `/etc/contentsync/templates/mysite`

### 頁面導出器配置節點 {#page-exporter-configuration-nodes}

模板由節點結構組成，因為它使用 [內容同步框架](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)。  每個節點具有 `type` 屬性，該屬性定義在建立zip檔案過程中的特定操作。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

以下節點可用於生成導出模板：

* `page`
頁面節點用於將頁面html複製到zip檔案。 它具有以下特點：

   * 是必需節點。
   * 位於下面 `/etc/contentsync/templates/<mysite>`。
   * 是使用屬性定義的 `Name`設定為 `page`。
   * 節點類型為 `nt:unstructured`

   的 `page` 節點具有以下屬性：

   * A `type` 屬性集 `pages`。

   * 它沒有 `path` 屬性，因為當前頁路徑將動態複製到配置。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
重寫節點定義如何在導出的頁面中重寫連結。 重寫的連結可以指向zip檔案中包含的檔案或指向伺服器上的資源。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
設計節點用於複製用於導出頁面的設計。 它具有以下特點：

   * 是可選的。
   * 位於下面 `/etc/contentsync/templates/<mysite>`。
   * 是使用屬性定義的 `Name` 設定為 `design`。
   * 節點類型為 `nt:unstructured`。

   的 `design` 節點具有以下屬性：

   * A `type` 屬性設定為值 `copy`。

   * 它沒有 `path` 屬性，因為當前頁路徑將動態複製到配置。


* `generic`
通用節點用於複製資源（如客戶端） 
`.js` 或 `.css` 檔案到zip檔案。 它具有以下特點：

   * 是可選的。
   * 位於下面 `/etc/contentsync/templates/<mysite>`。
   * 沒有特定的名稱。
   * 節點類型為 `nt:unstructured`。
   * 具有 `type` 物業及 `type` 相關屬性。 <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例如，以下配置節點將複製 `mysite.clientlibs.js` 檔案到zip檔案：

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**實施自定義配置**

也可以進行自定義配置。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

為滿足某些特定要求，您可能需要實施 [自定義更新處理程式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 以寫程式方式導出頁面 {#programmatically-exporting-a-page}

要以寫程式方式導出頁面，可使用 [頁面導出器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI服務。 此服務允許您：

* 導出頁面並寫入HTTP Servlet響應。
* 導出頁面並在特定位置保存zip檔案。

綁定到的Servlet `export` 選擇器和 `zip` 擴展使用PageExporter服務。

## 疑難排解 {#troubleshooting}

如果您在下載zip檔案時遇到問題，可以刪除 `/var/contentsync` 的子節點，然後再次發送導出請求。
