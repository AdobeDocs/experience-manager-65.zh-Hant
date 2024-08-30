---
title: 在外部網頁中內嵌適用性表單
description: 了解如何在外部網頁中嵌入調適型表單
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 2a237f74-fdfc-4e28-841c-f69afb7b99cf
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 60cc4096c4fd1b51e1d37b6e6f4cdb8806fd79eb
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 54%

---

# 在外部網頁中內嵌適用性表單{#embed-adaptive-form-in-external-web-page}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page) |
| AEM 6.5 | 本文章 |


<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文介紹使用基礎元件製作最適化Forms的舊方法。</span>

你可以[在 AEM Sites 頁面嵌入調適型表單](/help/forms/using/embed-adaptive-form-aem-sites.md)或在 AEM 外部託管的網頁嵌入調適型表單。嵌入式調適型表單功能齊全，使用者無需離開頁面即可填寫並提交表單。此功能可幫助使用者在網頁維持相關的其他元素，並同時與表單進行互動。

## 先決條件 {#prerequisites}

將調適型表單嵌入外部網站之前執行以下步驟

* Publish此最適化表單將內嵌至AEM Forms伺服器的Publish執行個體。
* 在您的網站上建立或識別可託管最適化表單的網頁。 請確定網頁可以[從CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)讀取jQuery檔案，或內嵌jQuery的本機復本。 必須有 jQuery 才可呈現調適型表單。
* 當AEM伺服器和網頁位於不同的網域時，請執行一節中列出的步驟，[啟用AEM Forms將最適化表單提供給跨網域網站](#cross-site)。

## 內嵌調適型表單 {#embed-adaptive-form}

您可以在網頁中插入幾行 JavaScript 來嵌入調適型表單。代碼中的 API 會向 AEM 伺服器發送 HTTP 請求以獲得調適型表單資源，並將調適型表單注入指定的表單容器中。

內嵌調適型表單：

1. 使用以下代碼在您的網站上建立網頁：

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
           // options.path refers to the path of the adaptive form
           // For Example: /content/forms/af/ABC, where ABC is the adaptive form
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

1. 在嵌入代碼中：

   * 使用最適化表單的發佈URL路徑變更&#x200B;*options.path*&#x200B;變數的值。 如果 AEM 伺服器在上下文路徑上執行，請確保 URL 包含上下文路徑。一律提及最適化表單的完整名稱，包括擴充功能。 例如，上述程式碼和適用性來自位於同一個AEM Forms伺服器上，因此範例使用適用性表單`/content/forms/af/locbasic.html`的內容路徑。
   * 將&#x200B;*options.dataRef*&#x200B;取代為要以URL傳遞的屬性。 您可以使用dataref變數[預填最適化表單](/help/forms/using/prepopulate-adaptive-form-fields.md)。
   * 將&#x200B;*options.themePath*&#x200B;取代為最適化表單中設定之主題以外的主題路徑。 或者，您可以使用請求屬性指定主題路徑。
   * CSS_Selector 是所嵌入調適型表單的表單容器 CSS 選擇器。例如，.customafsection css 類是上面範例中的 CSS 選擇器。

調適型表單嵌入網頁中。在嵌入式調適型表單中觀察以下內容：

* 內嵌表單中不包含原始最適化表單的頁首和頁尾。
* 草稿和提交的表單列在表單入口網站的「草稿」和「提交」標籤中。
* 在原始最適化表單上設定的提交動作會保留在內嵌表單中。
* 調適型表單規則保留在嵌入式表單中並完全發揮作用。
* 在原始最適化表單中設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。
* 如果在原始表單上設定Adobe Analytics，則Adobe Analytics伺服器會擷取分析資料。 但是，在 Forms 分析報告中不能使用。

## 範例拓撲 {#sample-topology}

嵌入式調適型表單的外部網頁會發送請求至 AEM 伺服器；伺服器通常位於私人網絡中的防火牆後面。為確保將請求安全導向 AEM 伺刷器，建議設定反向代理伺服器。

讓我們來看一個範例，說明如何在不使用Dispatcher的情況下設定Apache 2.4反向Proxy伺服器。 在此範例中，您正在裝載具有`/forms`內容路徑的AEM伺服器，並對應反向Proxy的`/forms`。 這可確保Apache伺服器上對`/forms`的任何請求都會導向到AEM執行個體。 此拓撲有助於減少Dispatcher層中的規則數量，因為所有要求都會加上前置詞`/forms`，以路由傳送至AEM伺服器。

1. 開啟 `httpd.conf` 設定檔案並取消註釋以下代碼行。或者，您可以將這些代碼行加入檔案中。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 將以下代碼行加入 `httpd-proxy.conf` 設定檔案中，以設定代理規則。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   以規則中的 AEM 伺服器發佈 URL 取代 `[AEM_Instance]`。

如果您未在內容路徑上掛載AEM伺服器，則Apache層的Proxy規則如下：

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
>如果您設定其他任何拓撲，請確定您將提交、預填和其他URL新增到Dispatcher層的允許清單。

## 最佳做法 {#best-practices}

將調適型表單嵌入網頁時，請考慮以下最佳做法：

* 確保網頁 CSS 定義的樣式規則與表單物件 CSS 不衝突。若要避免衝突，您可以使用AEM使用者端資料庫，重複使用最適化表單主題中的網頁CSS。 如需在最適化表單主題中使用使用者端資料庫的資訊，請參閱AEM Forms中的[主題](../../forms/using/themes.md)。
* 讓網頁中的表單容器使用整個視窗寬度。這樣可確保為行動裝置設定的 CSS 規則可使用，而無需任何變更。如果表單容器未採用完整的視窗寬度，您必須撰寫自訂CSS，讓表單能適應不同的行動裝置。
* 使用 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API，取得用戶端以 XML 或 JSON 表示的表單資料。
* 使用 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API 從 HTML DOM 卸載調適型表單。
* 設定從AEM伺服器傳送回應時的存取控制來源標頭。

## 啟用AEM Forms以向跨網域網站提供最適化表單 {#cross-site}

1. 在 AEM 發佈執行個體上，前往 AEM Web 主控台的 Configuration Manager：`https://'[server]:[port]'/system/console/configMgr`。
1. 找到並開啟 **Apache Sling 查閱者篩選器**&#x200B;設定。
1. 在允許的主機欄位中，指定網頁所在的網域。這樣可讓主機向 AEM 伺服器發送 POST 請求。您還可以使用規則運算式來指定一系列的外部應用程式網域。
