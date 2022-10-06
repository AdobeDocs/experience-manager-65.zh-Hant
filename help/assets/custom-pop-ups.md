---
title: 使用Quickview建立自訂快顯視窗
seo-title: Use Quickview to create custom pop-ups
description: 預設的「快速檢視」用於電子商務體驗，其中會顯示包含產品資訊的快顯視窗以促進購買。 您可以觸發自訂內容以顯示在快顯視窗中。
seo-description: The default Quickview is used in ecommerce experiences whereby a pop-up is displayed with product information to drive a purchase. You can trigger custom content to display in the pop-ups.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Viewers
role: User, Admin
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# 使用Quickview建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

預設的「快速檢視」用於電子商務體驗，其中會顯示包含產品資訊的快顯視窗以促進購買。 不過，您可以觸發自訂內容以顯示在快顯視窗中。 根據檢視器，此功能可讓使用者在熱點、縮圖影像或影像地圖上選取，以查看資訊或相關內容。

Dynamic Media中的下列檢視器支援Quickview:

* 互動式影像（可點按的熱點）
* 互動式視訊（視訊播放期間可點按縮圖影像）
* 轉盤橫幅（可點按的熱點或影像地圖）

雖然每個檢視器的功能有所不同，但在所有三個支援的檢視器中，建立「快速檢視」的程式都相同。

**要使用Quickview建立自定義彈出窗口，請執行以下操作：**

1. 為已上傳的資產建立快速檢視。

   您通常會在編輯資產以用於使用的檢視器時建立快速檢視。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的檢視器</strong></td>
    <td><strong>如果要建立快速檢視，請完成這些步驟</strong></td>
    </tr>
    <tr>
    <td>互動影像</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">向影像橫幅添加熱點</a>.</td>
    </tr>
    <tr>
    <td>互動影片</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">為視訊新增互動功能</a>.</td>
    </tr>
    <tr>
    <td>輪播橫幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">向橫幅添加熱點或影像映射</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 取得檢視器內嵌程式碼，以整合您網站中的檢視器。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的檢視器</strong><br /> </td>
    <td><strong>如果您想要整合檢視器與您的網站，請完成這些步驟</strong></td>
    </tr>
    <tr>
    <td>互動式影像</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">將互動式影像與您的網站整合</a>.<br /> </td>
    </tr>
    <tr>
    <td>互動式影片<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">將互動式視訊與您的網站整合</a>.<br /> </td>
    </tr>
    <tr>
    <td>輪播橫幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">將輪播橫幅新增至您的網站頁面</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您現在使用的檢視器必須知道如何使用「快速檢視」。

   檢視器使用的處理常式稱為 `QuickViewActive`.

   **範例**
假設您在網頁上對互動式影像使用下列範例內嵌程式碼：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   處理常式會以 `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **使用上方的范常式式碼範例，有下列程式碼：**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   深入了解 `setHandlers()` 方法（如下所示）:

   * 互動式影像檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * 互動式視訊檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. 您現在必須設定 `quickViewActivate` 處理常式。

   此 `quickViewActivate` 處理常式會控制檢視器中的「快速檢視」。 處理常式包含變數清單和函式呼叫，以便與Quickview搭配使用。 內嵌程式碼提供在Quickview和範例中設定之SKU變數的對應 `loadQuickView` 函式呼叫。

   **變數對應**
將您網頁中使用的變數對應至Quickview中包含的SKU值和一般變數：

   `var *variable1*= inData.*quickviewVariable*`

   提供的內嵌程式碼有SKU變數的範例對應：

   `var sku=inData.sku`

   也可從「快速檢視」對應其他變數，如下所示：

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函式呼叫**
處理常式也需要函式呼叫，Quickview才能運作。 您的主機頁面會假設可存取函式。 內嵌程式碼提供範例函式呼叫：

   `loadQuickView(sku)`

   範例函式呼叫假設函式 `loadQuickView()` 存在且可存取。

   深入了解 `quickViewActivate` 方法（如下所示）:

   * 互動式影像檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * 互動式視訊檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * 互動式視訊檢視器中的互動式資料支援： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. 請執行下列動作：

   * 取消對內嵌程式碼的setHandlers區段的註解。
   * 映射Quickview中包含的任何其他變數。

      * 更新 `loadQuickView(sku,*var1*,*var2*)` 如果您要新增其他變數，請呼叫。
   * 建立簡單 `loadQuickView` ()在檢視器外部的頁面上運作。

      例如，下列項目會將SKU的值寫入瀏覽器主控台：

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 將測試HTML頁面上傳至Web伺服器並開啟。

      將Quickview中的變數對應並設定函式呼叫後，瀏覽器主控台會使用提供的範例函式，將變數值寫入瀏覽器主控台。



1. 您現在可以使用函式叫用快速檢視中的簡單快顯視窗。 下列範例使用 `DIV` ，以取得快顯視窗。
1. 設定快顯視窗的樣式 `DIV` 以下列方式。 視需要新增您自己的其他樣式。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 放置快顯視窗 `DIV` 在HTML頁面的正文中。

   其中一個元素的ID設定為，當使用者叫用Quickview時，ID會以SKU值更新。 此範例也包含一個簡單按鈕，可在快顯視窗顯示後重新隱藏快顯視窗。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 新增函式，以便更新快顯視窗中的SKU值；取代步驟5中建立的簡單函式，使快顯視窗可見。 並搭配下列項目：

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 將測試HTML頁面上傳至您的Web伺服器並開啟。 檢視器會顯示快顯視窗 `DIV` 當用戶調用快速視圖時。
1. **如何以全螢幕模式顯示自訂快顯視窗**

   有些檢視器（例如互動式視訊檢視器）支援以全螢幕模式顯示。 不過，如前述步驟所述，使用快顯視窗會使其在全螢幕模式中顯示在檢視器後面。

   若要在標準和全螢幕模式中顯示快顯視窗，請將快顯視窗附加至檢視器容器。 使用第二個處理方法， `initComplete`.

   此 `initComplete` 在初始化查看器後調用處理程式。

   ```xml
   "initComplete":function() { code block }
   ```

   深入了解 `init()` 方法（如下所示）:

   * 互動式影像檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * 互動式視訊檢視器： [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. 若要將前述步驟所述的快顯視窗附加至檢視器，請使用下列程式碼：

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上述程式碼中，已執行下列動作：

   * 已識別自訂快顯視窗。
   * 從DOM中移除。
   * 已識別檢視器容器。
   * 將快顯視窗附加至檢視器容器。

1. 您的整個setHandlers代碼顯示如下所示（使用了Interactive Video查看器）:

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 載入處理程式後，您會初始化檢視器：

   `*viewerInstance.*init()`

   **範例**
此範例使用互動式影像檢視器。

   `s7interactiveimageviewer.init()`

   將檢視器內嵌至主機頁面後，請確定已建立檢視器例項，且處理常式已載入，然後才使用叫用檢視器 `init()`.
