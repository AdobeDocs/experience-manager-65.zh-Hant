---
title: 擴充Asset Editor
description: 瞭解如何使用自訂元件來擴充Asset Editor的功能。
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 12%

---

# 擴充Asset Editor {#extending-asset-editor}

Asset Editor是點按透過Asset Share找到的資產時開啟的頁面，可讓使用者編輯資產的方面，如中繼資料、縮圖、標題和標籤。

使用預先定義的編輯元件來設定編輯器的相關資訊，請參閱[建立和設定Asset Editor頁面](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page)。

除了使用現有的編輯器元件之外，[!DNL Adobe Experience Manager]開發人員也可以建立自己的元件。

## 建立資產編輯器範本 {#creating-an-asset-editor-template}

Geometrixx中包含下列範例頁面：

* Geometrixx範例頁面： `/content/geometrixx/en/press/asseteditor.html`
* 範例範本： `/apps/geometrixx/templates/asseteditor`
* 範例頁面元件： `/apps/geometrixx/components/asseteditor`

### 設定Clientlib {#configuring-clientlib}

[!DNL Assets]元件使用WCM edit clientlib的延伸。 clientlibs通常載入`init.jsp`。

與預設clientlib載入（在核心的`init.jsp`中）相比，[!DNL Assets]範本必須具有以下專案：

* 範本必須包含`cq.dam.edit` clientlib （而非`cq.wcm.edit`）。

* clientlib也必須包含在停用的WCM模式中(例如，載入 **publish**)，才能轉換謂語、動作和鏡頭。

在大多數情況下，複製現有的範例`init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`)應該符合這些需求。

### 設定JS動作 {#configuring-js-actions}

有些[!DNL Assets]元件需要在`component.js`中定義的JS函式。 將此檔案複製到您的元件目錄並加以連結。

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

範例在`head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`)中載入此JavaScript來源。

### 其他樣式表 {#additional-style-sheets}

有些[!DNL Assets]元件使用Widget程式庫。 若要在內容內容內容中正確呈現，必須載入其他樣式表。 標籤動作元件需要另一個專案。

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx樣式表 {#geometrixx-style-sheet}

範例頁面元件要求所有選取器必須以`.asseteditor` / `static.css` (`/etc/designs/geometrixx/static.css`)開頭。 最佳實務：將所有`.asseteditor`選取器複製到您的樣式表，並視需要調整規則。

### FormChooser：最終載入資源的調整 {#formchooser-adjustments-for-eventually-loaded-resources}

Asset Editor會使用「表單選擇器」，只要將表單選擇器和表單路徑新增至資產的URL，即可讓您編輯相同表單頁面上的資源（此案例中為資產）。

例如：

* 普通表單頁面： [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* 資產已載入表單頁面： [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

`head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`)中的範例控制代碼執行下列動作：

* 他們可偵測是否已載入資產或是否必須顯示純格式。
* 如果載入資產，則會停用WCM模式，因為parsys只能在純表單頁面上編輯。
* 如果資產已載入，他們會使用其標題，而非表單頁面上的標題。

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

在HTML部分中，使用先前的標題集（資產或頁面標題）：

```html
<title><%= title %></title>
```

## 建立簡單的表單欄位元件 {#creating-a-simple-form-field-component}

此範例說明如何建立可顯示並顯示已載入資產中繼資料的元件。

1. 在專案目錄中建立元件資料夾，例如`/apps/geometrixx/components/samplemeta`。
1. 使用下列程式碼片段新增`content.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 使用下列程式碼片段新增`samplemeta.jsp`：

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource is the asset.
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

1. 若要讓元件可用，您必須能夠加以編輯。若要讓元件可編輯，請在CRXDE Lite中新增主要型別`cq:EditConfig`的節點`cq:editConfig`。 若要移除段落，請新增單一值為`DELETE`的多值屬性`cq:actions`。

1. 導覽至瀏覽器，並在範例頁面（例如，`asseteditor.html`）上切換至設計模式並為段落系統啟用新元件。

1. 在「 **編輯** 」模式中，新元件(例如，「範例中繼資料 **」)現在可在sidekick中使用(可在「資產編輯器」**&#x200B;群組中找到 **&#x200B;**&#x200B;)。插入元件。若要儲存中繼資料，必須將其新增至中繼資料表格。

## 修改中繼資料選項 {#modifying-metadata-options}

您可以修改[中繼資料表單](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component)中可用的名稱空間。

目前可用的中繼資料定義於`/libs/dam/options/metadata`：

* 此目錄中的第一個層級包含名稱空間。
* 每個名稱空間內的專案代表中繼資料，例如本機零件專案中的結果。
* 中繼資料內容包含型別和多值選項的資訊。

可以在`/apps/dam/options/metadata`中覆寫選項：

1. 將目錄從`/libs`複製到`/apps`。

1. 移除、修改或新增專案。

>[!NOTE]
>
>如果您新增名稱空間，必須在您的存放庫/CRX中註冊它們。 否則，提交中繼資料表單將會導致錯誤。
