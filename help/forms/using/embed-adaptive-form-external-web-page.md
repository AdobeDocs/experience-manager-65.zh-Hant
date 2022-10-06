---
title: 在外部網頁中內嵌適用性表單
seo-title: Embed adaptive form in external web page
description: 了解如何將最適化表單嵌入外部網頁
seo-description: Learn how to embed an adaptive form in an external HTML web page
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
feature: Adaptive Forms
exl-id: 2a237f74-fdfc-4e28-841c-f69afb7b99cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---

# 在外部網頁中內嵌適用性表單{#embed-adaptive-form-in-external-web-page}

您可以 [在AEM Sites頁面中內嵌適用性表單](/help/forms/using/embed-adaptive-form-aem-sites.md) 或在AEM以外托管的網頁。 內嵌的最適化表單功能齊全，使用者無需離開頁面即可填寫及提交表單。 可協助使用者停留在網頁上其他元素的內容中，並同時與表單互動。

## 必備條件 {#prerequisites}

先執行下列步驟，再將最適化表單內嵌至外部網站

* 發佈要內嵌至AEM Forms伺服器之發佈例項的最適化表單。
* 在您的網站上建立或識別網頁，以托管最適化表單。 確保網頁可以 [從CDN讀取jQuery檔案](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) 或內嵌jQuery的本機副本。 演算最適化表單時需要jQuery。
* 當AEM伺服器和網頁位於不同網域時，請執行一節中所列的步驟， [啟用AEM Forms，將最適化表單提供至跨網域網站](#cross-site).

## 內嵌最適化表單 {#embed-adaptive-form}

您可以在網頁中插入幾行JavaScript，以內嵌最適化表單。 程式碼中的API會傳送HTTP要求至AEM伺服器，以取得最適化表單資源，並將最適化表單插入指定的表單容器中。

若要內嵌最適化表單：

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

1. 內嵌程式碼中：

   * 變更 *options.path* 變數與最適化表單的發佈URL路徑。 如果AEM伺服器在內容路徑上執行，請確定URL包含內容路徑。 一律提及適用性表單的完整名稱，包括擴充功能。   例如，上述程式碼和適用性來源位於相同的AEM表單伺服器上，因此此範例使用適用性表單/content/forms/af/locbasic.html的內容路徑。
   * 取代 *options.dataRef* 與要隨URL傳遞的屬性。 您可以將dataref變數用於 [預填最適化表單](/help/forms/using/prepopulate-adaptive-form-fields.md).
   * 取代 *options.themePath* 使用在最適化表單中設定的主題以外的主題路徑。 或者，您也可以使用請求屬性來指定主題路徑。
   * CSS_Selector是內嵌適用性表單之表單容器的CSS選取器。 例如， .customafsection css類是上述示例中的CSS選擇器。

適用性表單已內嵌於網頁中。 在內嵌的最適化表單中觀察下列項目：

* 原始適用性表單中的頁首和頁尾不包含在內嵌表單中。
* Forms入口網站的「草稿」和「提交」標籤中提供草稿和提交的表單。
* 原始最適化表單上設定的提交動作會保留在內嵌表單中。
* 適用性表單規則可在內嵌表單中保留，且完整運作。
* 在原始最適化表單中設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。
* 如果在原始表單上設定Adobe Analytics，則會在Adobe Analytics伺服器中擷取分析資料。 不過，Forms分析報表中沒有此功能。

## 示例拓撲 {#sample-topology}

內嵌最適化表單的外部網頁會傳送要求至AEM伺服器，而伺服器通常位於私人網路的防火牆後。 為確保將請求安全地導向至AEM伺服器，建議設定反向代理伺服器。

讓我們舉一個範例，說明如何在不使用Dispatcher的情況下設定Apache 2.4反向Proxy伺服器。 在此範例中，您會以 `/forms` 內容路徑與地圖 `/forms` 代理。 它可確保 `/forms` 在Apache伺服器上，會導向至AEM例項。 此拓撲有助於減少Dispatcher層的規則數，因為所有帶有前置詞的請求 `/forms` 路由至AEM伺服器。

1. 開啟 `httpd.conf` 設定檔案，並取消註解下列幾行程式碼。 或者，您也可以在檔案中新增這些程式碼行。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 在 `httpd-proxy.conf` 設定檔。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   取代 `[AEM_Instance]` 與規則中的AEM伺服器發佈URL。

如果您未在內容路徑上裝載AEM伺服器，則Apache層的代理規則將如下：

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
>如果您設定任何其他拓撲，請確定您將提交、預填和其他URL新增至Dispatcher層的允許清單。

## 最佳實務 {#best-practices}

將最適化表單內嵌至網頁時，請考量下列最佳實務：

* 請確定網頁CSS中定義的樣式規則不會與表單物件CSS衝突。 若要避免衝突，您可以使用AEM用戶端程式庫，在最適化表單主題中重複使用網頁CSS。 如需在最適化表單主題中使用用戶端程式庫的相關資訊，請參閱 [AEM Forms主題](../../forms/using/themes.md).
* 讓網頁中的表單容器使用整個視窗寬度。 它可確保為行動裝置設定的CSS規則可正常運作，而無任何變更。 如果表單容器沒有取得整個視窗寬度，您需要編寫自訂CSS，讓表單能適應不同的行動裝置。
* 使用 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API，用於取得用戶端中表單資料的XML或JSON表示法。
* 使用 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` 從HTMLDOM卸載最適化表單的API。
* 從AEM伺服器傳送回應時，設定存取控制原始標題。

## 啟用AEM Forms，將最適化表單提供至跨網域網站 {#cross-site}

1. 在AEM發佈例項上，前往AEM Web Console Configuration Manager(位於 `https://'[server]:[port]'/system/console/configMgr`.
1. 找出並開啟 **Apache Sling反向連結篩選器** 設定。
1. 在「允許的主機」欄位中，指定網頁所在的網域。 它可讓主機向AEM伺服器提出POST請求。 您也可以使用規則運算式來指定一系列外部應用程式網域。
