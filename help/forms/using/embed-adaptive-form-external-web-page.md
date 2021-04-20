---
title: 在外部網頁中內嵌適用性表單
seo-title: 在外部網頁中內嵌適用性表單
description: 瞭解如何在外部網頁中內嵌最適化表單
seo-description: 瞭解如何在外部HTML網頁中內嵌最適化表單
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 2%

---


# 在外部網頁中內嵌適用性表單{#embed-adaptive-form-in-external-web-page}

您可以[在AEM Sites頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)或外部代管的網頁中內嵌最適化表單AEM。 內嵌的最適化表單功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的內容，並同時與表單互動。

## 必備條件 {#prerequisites}

在將最適化表單內嵌至外部網站之前，請執行下列步驟

* 發佈要嵌入到AEM Forms伺服器發佈實例的自適應表單。
* 在您的網站上建立或識別網頁以代管最適化表單。 請確定網頁可從CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)讀取jQuery檔案，或內嵌jQuery的本機副本。 [需要有jQuery才能轉換最適化表單。
* 當服AEM務器和網頁位於不同域時，請執行[部分中列出的步驟，使AEM Forms能夠向跨域站點](#cross-site)提供自適應表單。

## 內嵌最適化表單{#embed-adaptive-form}

您可以在網頁中插入幾行JavaScript，以嵌入最適化表單。 程式碼中的API會傳送HTTP要求至伺服器，以取得最AEM適化表單資源，並在指定的表單容器中插入最適化表單。

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

   * 變更&#x200B;*options.path*&#x200B;變數的值，以及最適化表單的發佈URL路徑。 如果AEM伺服器在上下文路徑上執行，請確定URL包含上下文路徑。 請務必提及最適化表單的完整名稱，包括副檔名。   例如，上述代碼和adaptive from駐留在相同的表單AEM伺服器上，因此示例使用adaptive form /content/forms/af/locbasic.html的上下文路徑。
   * 將&#x200B;*options.dataRef*&#x200B;取代為要與URL一起傳遞的屬性。 您可以使用dataref變數來預填最適化表單](/help/forms/using/prepopulate-adaptive-form-fields.md)。[
   * 將&#x200B;*options.themePath*&#x200B;取代為主題的路徑，而非在最適化表單中設定的主題。 或者，您也可以使用request屬性來指定主題路徑。
   * CSS_Selector是內嵌最適化表單之表單容器的CSS選擇器。 例如，.customafsection css類是上述範例中的CSS選擇器。

最適化表單內嵌在網頁中。 在嵌入式自適應表單中觀察以下內容：

* 原始最適化表單中的頁首和頁尾不包含在內嵌表單中。
* 可在Forms門戶的「草稿和提交」頁籤中查看草稿和提交的表格。
* 在原始最適化表單上設定的提交動作會保留在內嵌表單中。
* 自適應表單規則會保留在內嵌表單中，並具備完整功能。
* 在原始最適化表單中設定的體驗定位和A/B測試無法在內嵌表單中運作。
* 如果在原始表單上設定了Adobe Analytics，分析資料會在Adobe Analytics伺服器中擷取。 但是，Forms分析報表中不提供。

## 拓撲{#sample-topology}示例

嵌入自適應表單的外部網頁會向伺服器發送請求AEM，伺服器通常位於專用網路的防火牆後。 為確保將請求安全地導向AEM至伺服器，建議您設定反向代理伺服器。

讓我們看一個示例，說明如何在沒有調度程式的情況下設定Apache 2.4反向代理伺服器。 在此示例中，您將使用`/forms`上AEM下文路徑來托管伺服器，並映射`/forms`作為反向代理。 它可確保Apache伺服器上的`/forms`請求都定向到實AEM例。 此拓撲有助於減少調度器層的規則數，因為所有前置詞有`/forms`的請求都會路由到服AEM務器。

1. 開啟`httpd.conf`配置檔案並取消對以下代碼行的注釋。 或者，您也可以在檔案中新增這些程式碼行。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 在`httpd-proxy.conf`配置檔案中添加以下代碼行，以設定代理規則。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   在規則中，將`[AEM_Instance]`取AEM代為伺服器發佈URL。

如果未在上下文路AEM徑上裝載伺服器，則Apache層的代理規則如下：

```text
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
>如果設定了任何其他拓撲，請確保將submit、prefill和其他URL添加到調度程式層的allowlist中。

## 最佳做法{#best-practices}

在網頁中內嵌最適化表單時，請考慮下列最佳實務：

* 請確定網頁CSS中定義的樣式規則與表單物件CSS不衝突。 為避免衝突，您可以使用用戶端程式庫，在最適化表單主題中重複使用網AEM頁CSS。 如需在最適化表單主題中使用用戶端程式庫的詳細資訊，請參閱AEM Forms的[主題。](../../forms/using/themes.md)
* 讓網頁中的表格容器使用整個視窗寬度。 它可確保為行動裝置設定的CSS規則可正常運作，而不需做任何變更。 如果表單容器不佔用整個視窗寬度，您需要編寫自訂CSS，讓表單能適應不同的行動裝置。
* 使用`[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API，在用戶端中取得表單資料的XML或JSON表示法。
* 使用`[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API從HTML DOM卸載最適化表單。
* 從伺服器傳送回應時，請設定存取控制原點AEM標題。

## 讓AEM Forms向跨網域站點{#cross-site}提供適應性表單

1. 在發AEM布實例上，轉AEM到`https://'[server]:[port]'/system/console/configMgr`的Web控制台配置管理器。
1. 找到並開啟&#x200B;**Apache Sling Referrer Filter**&#x200B;組態。
1. 在「允許的主機」欄位中，指定網頁所在的網域。 它使主機能夠向伺服器發出POSTAEM請求。 您也可以使用規則運算式來指定一系列外部應用程式網域。
