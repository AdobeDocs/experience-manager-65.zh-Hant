---
title: 擴展資產編輯器
description: 瞭解如何使用自定義元件擴展資產編輯器的功能。
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 13%

---

# 擴展資產編輯器 {#extending-asset-editor}

資產編輯器是在按一下通過資產共用找到的資產時開啟的頁面，允許用戶編輯資產的元資料、縮略圖、標題和標籤等方面。

使用預定義編輯元件的編輯器配置在 [「建立和配置資產編輯器」頁](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page)。

除了使用預先存在的編輯器元件外， [!DNL Adobe Experience Manager] 開發人員也可以建立自己的元件。

## 建立資產編輯器模板 {#creating-an-asset-editor-template}

以下示例頁包含在Geometrixx中：

* Geometrixx示例頁： `/content/geometrixx/en/press/asseteditor.html`
* 示例模板： `/apps/geometrixx/templates/asseteditor`
* 示例頁元件： `/apps/geometrixx/components/asseteditor`

### 配置客戶端庫 {#configuring-clientlib}

[!DNL Assets] 元件使用WCM編輯客戶端庫的擴展。 客戶端通常在 `init.jsp`。

與預設客戶端庫載入(在 `init.jsp`) [!DNL Assets] 模板必須具有以下內容：

* 模板必須包括 `cq.dam.edit` 客戶端庫(而不是 `cq.wcm.edit`)。

* clientlib也必須包含在停用的WCM模式中(例如，載入 **publish**)，才能轉換謂語、動作和鏡頭。

在大多數情況下，複製現有示例 `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`)應滿足這些需求。

### 配置JS操作 {#configuring-js-actions}

部分 [!DNL Assets] 元件需要在中定義的JS函式 `component.js`。 將此檔案複製到元件目錄並連結它。

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

示例將此JavaScript源載入到 `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`)。

### 其他樣式表 {#additional-style-sheets}

部分 [!DNL Assets] 元件使用小部件庫。 要在內容上下文中正確呈現，必須載入附加樣式表。 標籤操作元件需要一個。

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx樣式表 {#geometrixx-style-sheet}

示例頁元件要求所有選擇器都以 `.asseteditor` 共 `static.css` (`/etc/designs/geometrixx/static.css`)。 最佳做法：全部複製 `.asseteditor` 選擇器到樣式表，並根據需要調整規則。

### 窗體選擇器：最終載入的資源的調整 {#formchooser-adjustments-for-eventually-loaded-resources}

資產編輯器使用表單選擇器，它允許您僅通過添加表單選擇器和表單路徑到資產URL來編輯同一表單頁上的資源（在本例中為資產）。

例如：

* 純表單頁： [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* 已載入到表單頁中的資產： [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

中的示例句柄 `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`)執行以下操作：

* 它們檢測是否載入了資產或是否必須顯示純表單。
* 如果載入了資產，則會禁用WCM模式，因為只能在純表單頁面上編輯parsys。
* 如果載入了資產，則它們會使用其標題而不是表單頁面上的標題。

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

在HTML部分，使用前面的標題集（資產或頁標題）:

```html
<title><%= title %></title>
```

## 建立簡單的表單域元件 {#creating-a-simple-form-field-component}

此示例說明如何構建顯示和顯示已載入資產的元資料的元件。

1. 在項目目錄中建立元件資料夾，例如， `/apps/geometrixx/components/samplemeta`。
1. 添加 `content.xml` 以下代碼段：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 添加 `samplemeta.jsp` 以下代碼段：

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. 若要讓元件可用，您必須能夠加以編輯。要使元件可編輯，請在CRXDE Lite中添加節點 `cq:editConfig` 主類型 `cq:EditConfig`。 為了能夠移除段落，請新增多值屬性 `cq:actions` ，其中單一值 `DELETE`為。

1. 導航到瀏覽器，並在示例頁面上(例如， `asseteditor.html`)切換到設計模式，並啟用段落系統的新元件。

1. 在「 **編輯** 」模式中，新元件(例如，「範例中繼資料 **」)現在可在sidekick中使用(可在「資產編輯器」**&#x200B;群組中找到 **** )。插入元件。若要儲存中繼資料，必須將其新增至中繼資料表格。

## 修改元資料選項 {#modifying-metadata-options}

可以修改中可用的命名空間 [元資料表單](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component)。

當前可用的元資料在中定義 `/libs/dam/options/metadata`:

* 此目錄內的第一級包含命名空間。
* 每個命名空間中的項表示元資料，如本地部件項的結果。
* 元資料內容包含類型和多值選項的資訊。

可以在 `/apps/dam/options/metadata`:

1. 從中複製目錄 `/libs` 至 `/apps`。

1. 刪除、修改或添加項目。

>[!NOTE]
>
>如果添加新命名空間，則必須在儲存庫/CRX中註冊它們。 否則，提交元資料表單將導致錯誤。
