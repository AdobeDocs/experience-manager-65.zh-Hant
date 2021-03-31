---
title: 擴充資產編輯器
description: 瞭解如何使用自訂元件擴充資產編輯器的功能。
contentOwner: AG
role: 業務從業人員、管理員
feature: 開發人員工具
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 13%

---


# 擴充資產編輯器{#extending-asset-editor}

「資產編輯器」是當透過「資產共用」找到的資產被點按時開啟的頁面，可讓使用者編輯資產的元資料、縮圖、標題和標籤等方面。

使用預定義編輯元件的編輯器配置在[建立和配置資產編輯器頁面](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page)中。

除了使用預先存在的編輯器元件外，[!DNL Adobe Experience Manager]開發人員也可建立自己的元件。

## 建立資產編輯器範本{#creating-an-asset-editor-template}

下列範例頁面包含在Geometrixx中：

* Geometrixx範例頁面：`/content/geometrixx/en/press/asseteditor.html`
* 範例範本：`/apps/geometrixx/templates/asseteditor`
* 範例頁面元件：`/apps/geometrixx/components/asseteditor`

### 配置Clientlib {#configuring-clientlib}

[!DNL Assets] 元件使用WCM edit clientlib的擴展。clientlibs通常載入在`init.jsp`中。

與預設clientlib載入（在核心的`init.jsp`中）相比，[!DNL Assets]模板必須具有以下內容：

* 範本必須包含`cq.dam.edit` clientlib（而非`cq.wcm.edit`）。

* clientlib也必須包含在停用的WCM模式中(例如，載入 **publish**)，才能轉換謂語、動作和鏡頭。

在大多數情況下，複製現有的示例`init.jsp`(`/apps/geometrixx/components/asseteditor/init.jsp`)應滿足這些需求。

### 設定JS動作{#configuring-js-actions}

有些[!DNL Assets]元件需要`component.js`中定義的JS函式。 將此檔案複製到元件目錄並將其連結。

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

範例會在`head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`)中載入此JavaScript來源。

### 其他樣式表{#additional-style-sheets}

有些[!DNL Assets]元件使用Widget程式庫。 若要在內容內容內容中正確呈現，必須載入其他樣式表。 標籤動作元件需要一個。

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx樣式表{#geometrixx-style-sheet}

範例頁面元件要求所有選擇器都以`static.css`(`/etc/designs/geometrixx/static.css`)的`.asseteditor`開頭。 最佳實務：將所有`.asseteditor`選擇器複製到樣式表並視需要調整規則。

### 表單選擇器：對最終載入的資源的調整{#formchooser-adjustments-for-eventually-loaded-resources}

資產編輯器使用表單選擇器，您只需新增表單選擇器和表單路徑至資產的URL，即可編輯相同表單頁面上的資源（在本例中為資產）。

例如：

* 純格式頁面：[http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* 資產已載入表單頁面：[http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

`head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`)中的示例句柄執行以下操作：

* 它們會偵測是否已載入資產或必須顯示純格式。
* 如果資產已載入，則會停用WCM模式，因為parsys只能在純格式頁面上編輯。
* 如果資產已載入，則會使用其標題，而非表單頁面上的標題。

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

在HTML部分中，請使用前面的標題集（資產或頁面標題）:

```html
<title><%= title %></title>
```

## 建立簡單表單域元件{#creating-a-simple-form-field-component}

此範例說明如何建立元件，以顯示已載入資產的中繼資料。

1. 在項目目錄中建立元件資料夾，例如`/apps/geometrixx/components/samplemeta`。
1. 使用下列程式碼片段新增`content.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 使用下列程式碼片段新增`samplemeta.jsp`:

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

1. 若要讓元件可用，您必須能夠加以編輯。要使元件可編輯，請在CRXDE Lite中添加主類型`cq:EditConfig`的節點`cq:editConfig`。 為了能夠移除段落，請新增多值屬性 `cq:actions` ，其中單一值 `DELETE`為。

1. 導覽至您的瀏覽器，並在範例頁面（例如`asseteditor.html`）切換至設計模式，並啟用段落系統的新元件。

1. 在「 **編輯** 」模式中，新元件(例如，「範例中繼資料 **」)現在可在sidekick中使用(可在「資產編輯器」**&#x200B;群組中找到 **** )。插入元件。若要儲存中繼資料，必須將其新增至中繼資料表格。

## 修改元資料選項{#modifying-metadata-options}

您可以修改[中繼資料表單](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component)中可用的名稱空間。

`/libs/dam/options/metadata`中定義了當前可用的元資料：

* 此目錄內的第一級包含名稱空間。
* 每個命名空間中的項目代表中繼資料，例如產生本機零件項目。
* 中繼資料內容包含類型和多值選項的資訊。

可在`/apps/dam/options/metadata`中覆寫選項：

1. 將目錄從`/libs`複製到`/apps`。

1. 移除、修改或新增項目。

>[!NOTE]
>
>如果添加新名稱空間，則必須在儲存庫/CRX中註冊。 否則，提交中繼資料表格將會產生錯誤。
