---
title: 在外部網頁中內嵌最適化表單
seo-title: 在外部網頁中內嵌最適化表單
description: 瞭解如何在外部網頁中內嵌最適化表單
seo-description: 瞭解如何在外部HTML網頁中內嵌最適化表單
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
translation-type: tm+mt
source-git-commit: 92a64c8a1ba38f592d18355b8233cb79a2575301

---


# 在外部網頁中內嵌最適化表單{#embed-adaptive-form-in-external-web-page}

您可以 [在AEM網站頁面或AEM以外代管的網頁中](/help/forms/using/embed-adaptive-form-aem-sites.md) ，內嵌最適化表單。 內嵌的最適化表單功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的內容，並同時與表單互動。

## 必備條件 {#prerequisites}

在將最適化表單內嵌至外部網站之前，請執行下列步驟

* 發佈要內嵌至AEM Forms伺服器發佈例項的最適化表單。
* 在您的網站上建立或識別網頁以代管最適化表單。 請確定網頁可以 [從CDN讀取jQuery檔案](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) ，或內嵌jQuery的本機副本。 需要有jQuery才能轉換最適化表單。
* 當AEM伺服器和網頁位於不同網域時，請執行區段中所列的步驟，讓 [AEM Forms為跨網域網站提供最適化表單](#cross-site)。

## 內嵌最適化表單 {#embed-adaptive-form}

您可以在網頁中插入幾行JavaScript，以嵌入最適化表單。 程式碼中的API會傳送HTTP要求給AEM伺服器，以取得最適化表單資源，並在指定的表單容器中插入最適化表單。

要嵌入最適化表單：

1. 使用下列程式碼在您的網站上建立網頁：

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the publish URL of the adaptive form
           // For Example: https:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. 在內嵌的程式碼中：

   * 變更 *options.path變數的值* ，以及最適化表單的發佈URL路徑。 如果AEM伺服器是在內容路徑上執行，請確定URL包含內容路徑。 例如，上述程式碼和adaptive from位於相同的aem表單伺服器上，因此此範例使用adaptive form /content/forms/af/locbasic.html的上下文路徑。
   * 將 *options.dataRef* 取代為要以URL傳遞的屬性。 您可以使用dataref變數來預 [先填寫最適化表格](/help/forms/using/prepopulate-adaptive-form-fields.md)。
   * 將 *options.themePath* 取代為主題的路徑，而非在最適化表單中設定的主題。 或者，您也可以使用request屬性來指定主題路徑。
   * CSS_Selector是內嵌最適化表單之表單容器的CSS選擇器。 例如，.customafsection css類是上述範例中的CSS選擇器。

最適化表單內嵌在網頁中。 在嵌入式自適應表單中觀察以下內容：

* 原始最適化表單中的頁首和頁尾不包含在內嵌表單中。
* 草稿和提交的表單可在表單入口網站的「草稿和提交」標籤中使用。
* 在原始最適化表單上設定的提交動作會保留在內嵌表單中。
* 自適應表單規則會保留在內嵌表單中，並具備完整功能。
* 在原始最適化表單中設定的體驗定位和A/B測試無法在內嵌表單中運作。
* 如果Adobe Analytics是在原始表單上設定，則分析資料會在Adobe Analytics伺服器中擷取。 但是，Forms分析報表中不提供它。

## 拓撲示例 {#sample-topology}

內嵌最適化表單的外部網頁會傳送要求至AEM伺服器，而AEM伺服器通常位於私人網路的防火牆後方。 為確保請求安全地導向至AEM伺服器，建議您設定反向代理伺服器。

讓我們看一個示例，說明如何在沒有調度程式的情況下設定Apache 2.4反向代理伺服器。 在此範例中，您會以內容路徑和反向 `/forms` proxy的對應來代 `/forms` 管AEM伺服器。 它可確保Apache伺服器上 `/forms` 的任何要求都會導向至AEM例項。 此拓撲可協助減少發送器層的規則數，因為所有請求都以路由前置， `/forms` 並且會路由到AEM伺服器。

1. 開啟設 `httpd.conf` 定檔案並取消註解下列程式碼行。 或者，您也可以在檔案中新增這些程式碼行。

   ```
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 在設定檔案中新增下列程式碼行，以設定代 `httpd-proxy.conf` 理規則。

   ```
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   在規 `[AEM_Instance`則中以AEM伺服器發佈URL取代]。

如果您未將AEM伺服器載入內容路徑，Apache層的Proxy規則將如下：

```java
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>如果設定了任何其他拓撲，請確保在調度程式層將提交、預填充和其他URL列入白名單。

## Best practices {#best-practices}

在網頁中內嵌最適化表單時，請考慮下列最佳實務：

* 請確定網頁CSS中定義的樣式規則與表單物件CSS不衝突。 若要避免衝突，您可以使用AEM用戶端程式庫，在最適化表單主題中重複使用網頁CSS。 如需在最適化表單主題中使用用戶端程式庫的詳細資訊，請參 [閱「AEM表單中的主題」](../../forms/using/themes.md)。
* 讓網頁中的表格容器使用整個視窗寬度。 它可確保為行動裝置設定的CSS規則可正常運作，而不需做任何變更。 如果表單容器不佔用整個視窗寬度，您需要編寫自訂CSS，讓表單能適應不同的行動裝置。
* 使用 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API在用戶端中取得表單資料的XML或JSON表示法。
* 使用 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API從HTML DOM中卸載最適化表單。
* 從AEM伺服器傳送回應時，請設定存取控制原點標題。

## 啟用AEM Forms，以針對跨網域網站提供最適化表單 {#cross-site}

1. 在AEM作者例項上，請前往AEM Web Console Configuration Manager(網址為 `https://[server]:[port]/system/console/configMgr`)。
1. 找到並開啟 **Apache Sling Referrer Filter設定** 。
1. 在「允許的主機」欄位中，指定網頁所在的網域。 它可讓主機向AEM伺服器發出POST請求。 您也可以使用規則運算式來指定一系列外部應用程式網域。

