---
title: 使用Quickviews建立自訂快顯視窗
seo-title: 使用Quickviews建立自訂快顯視窗
description: 在電子商務體驗中使用預設的Quickview，以便顯示包含產品資訊的快顯視窗來推動購買。 您可以觸發自訂內容以顯示在快顯視窗中。
seo-description: 在電子商務體驗中使用預設的Quickview，以便顯示包含產品資訊的快顯視窗來推動購買。 您可以觸發自訂內容以顯示在快顯視窗中。
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
translation-type: tm+mt
source-git-commit: 73c2b5ee4d60eae253af537ccadccd9952300d3a

---


# 使用Quickviews建立自訂快顯視窗 {#using-quickviews-to-create-custom-pop-ups}

在電子商務體驗中使用預設的Quickview，以便顯示包含產品資訊的快顯視窗來推動購買。 不過，您可以觸發自訂內容以顯示在快顯視窗中。 根據您使用的檢視器，此功能可讓使用者按一下熱點、縮圖影像或影像地圖，以檢視資訊或相關內容。

動態媒體中的下列檢視器支援快速檢視：

* 互動式影像（可點選的熱點）
* 互動式視訊（視訊播放時可點選的縮圖影像）
* 轉盤橫幅（可點選的熱點或影像地圖）

雖然每個檢視器的功能不同，但建立Quickview的程式在所有三個支援的檢視器上都相同。

**使用Quickviews建立自訂快顯視窗**

1. 為已上傳的資產建立快速檢視。

   您通常會在編輯資產時建立快速檢視，以便與您使用的檢視器搭配使用。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的檢視器</strong></td>
    <td><strong>完成這些步驟以建立Quickview</strong></td>
    </tr>
    <tr>
    <td>互動式影像</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">將熱點添加到影像橫幅</a>。</td>
    </tr>
    <tr>
    <td>互動式影片</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">為視訊新增互動功能</a>。</td>
    </tr>
    <tr>
    <td>轉盤橫幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">將熱點或影像映射添加到橫幅</a>。<br /> </td>
    </tr>
    </tbody>
   </table>

1. 取得檢視器內嵌程式碼，將檢視器整合在您的網站中。

   <table>
    <tbody>
    <tr>
    <td><strong>您使用的檢視器</strong><br /> </td>
    <td><strong>完成這些步驟，將檢視器與您的網站整合</strong></td>
    </tr>
    <tr>
    <td>互動式影像</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">將互動式影像與您的網站整合</a>。<br /> </td>
    </tr>
    <tr>
    <td>Interactive video<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">將互動式視訊與您的網站整合</a>。<br /> </td>
    </tr>
    <tr>
    <td>轉盤橫幅</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">新增轉盤橫幅至您的網站頁面</a>。<br /> </td>
    </tr>
    </tbody>
   </table>

1. 您使用的檢視器現在需要瞭解如何使用Quickview。

   若要這麼做，檢視器會使用名為的處理常式 `QuickViewActive`。

   **範例**&#x200B;假設您在網頁上使用下列互動式影像的範例內嵌程式碼：

   ![chlimage_1-291](assets/chlimage_1-291.png)

   處理常式會使用下列方式載入檢視器 `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **使用上述範例內嵌程式碼範例，我們有下列程式碼：**

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

   如需進一步了 `setHandlers()` 解方法，請參閱：

   * 互動式影像檢視器： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_sethandlers.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_sethandlers.html)
   * 互動式視訊檢視器： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_sethandlers.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_sethandlers.html)

1. 您現在需要設定處理 `quickViewActivate` 常式。

   處理 `quickViewActivate` 常式會控制檢視器中的Quickviews。 處理常式包含變數清單和函式呼叫，以便與Quickview搭配使用。 內嵌代碼提供Quickview中SKU變數集的對應，以及範例函式 `loadQuickView` 呼叫。

   **變數對**&#x200B;應Map變數，以用於您的網頁，並與Quickview中包含的SKU值和一般變數對應：

   `var *variable1*= inData.*quickviewVariable*`

   提供的內嵌代碼具有SKU變數的範例對應：

   `var sku=inData.sku`

   也從Quickview映射其他變數，如下所示：

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **函式調**&#x200B;用處理常式也需要函式呼叫，讓Quickview運作。 您的主機頁面會假設該函式可存取。 內嵌代碼提供範例函式呼叫：

   `loadQuickView(sku)`

   示例函式調用假定該函式存 `loadQuickView()` 在且可訪問。

   如需進一步了 `quickViewActivate` 解方法，請參閱：

   * 互動式影像檢視器： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_interactive_image_event_callbacks.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_interactive_image_event_callbacks.html)
   * 互動式視訊檢視器： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_event_callbacks.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_event_callbacks.html)
   * 互動式視訊檢視器中的互動式資料支援： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_int_data_support.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_int_data_support.html)

1. 執行下列動作：

   * 取消對embed代碼的setHandlers部分的注釋。
   * 映射Quickview中包含的任何其他變數。

      * 如果您要 `loadQuickView(sku,*var1*,*var2*)` 新增其他變數，請更新呼叫。
   * 在檢視器 `loadQuickView` 外部的頁面上建立簡單()函式。

      例如，下列程式將sku值寫入瀏覽器主控台：

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 將測試HTML頁面上傳至網頁伺服器並開啟。

      在映射了Quickview中的變數並就地調用了函式後，瀏覽器控制台使用提供的示例函式將變數值寫入瀏覽器控制台。



1. 您現在可以使用函式來叫用Quickview中的簡單快顯功能。 下列範例會使用快 `DIV` 顯視窗。
1. 以下列方式設 `DIV` 定快顯視窗的樣式。 視需要新增您自己的其他樣式。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 將快顯功能 `DIV` 放在HTML頁面的正文中。

   其中一個元素會以ID設定，當使用者叫用Quickview時，ID會以sku值更新。 此範例也包含一個簡單按鈕，可在快顯視窗顯示後再次隱藏。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 新增函式以更新快顯視窗中的sku值；取代步驟5中建立的簡單函式，讓快顯視覺化。 與下列項目搭配：

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 將測試HTML頁面上傳至您的網站伺服器並開啟。 當使用者叫用Quickview時，檢 `DIV` 視器會顯示快顯視窗。
1. **如何以全螢幕模式顯示自訂快顯視窗**

   有些檢視器（例如互動式視訊檢視器）支援全螢幕模式顯示。 不過，如前述步驟所述，使用快顯功能會使它在全螢幕模式下顯示在檢視器後方。

   若要在標準和全螢幕模式中都顯示快顯視窗，請將快顯視窗附加至檢視器容器。 要完成此操作，可使用第二個處理程式方法 `initComplete`。

   在檢 `initComplete` 視器初始化後，就會叫用處理器。

   ```xml
   "initComplete":function() { code block }
   ```

   如需進一步了 `init()` 解方法，請參閱：

   * 互動式影像檢視器： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_init.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_init.html)
   * 互動式視訊檢視器： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_init.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_init.html)

1. 若要將快顯視窗（如前述步驟所述）附加至檢視器，請使用下列程式碼：

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   在上述程式碼中，我們已執行下列動作：

   * 已識別我們的自訂快顯視窗。
   * 從DOM中移除。
   * 已識別檢視器容器。
   * 已將快顯視窗連接至檢視器容器。

1. 您的整個setHandlers程式碼現在看起來應類似下列（使用互動式視訊檢視器）:

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

1. 載入處理常式後，您就會初始化檢視器：

   `*viewerInstance.*init()`

   **範例**&#x200B;此範例使用互動式影像檢視器。

   `s7interactiveimageviewer.init()`

   將檢視器內嵌至主機頁面後，請務必先建立檢視器例項，然後載入處理常式，再使用呼叫檢視器 `init()`。

