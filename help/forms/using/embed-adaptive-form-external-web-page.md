---
title: 在外部網頁中內嵌適用性表單
seo-title: Embed adaptive form in external web page
description: 瞭解如何在外部網頁中嵌入自適應表單
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

你可以 [在AEM Sites頁中嵌入自適應表單](/help/forms/using/embed-adaptive-form-aem-sites.md) 或外部的網頁AEM。 嵌入式自適應表單功能齊全，用戶無需離開頁面即可填寫和提交表單。 它幫助用戶保持在網頁上其他元素的上下文中，同時與表單交互。

## 必備條件 {#prerequisites}

在將自適應表單嵌入到外部網站之前，請執行以下步驟

* 發佈要嵌入到AEM Forms伺服器發佈實例的自適應表單。
* 在您的網站上建立或標識網頁以承載自適應表單。 確保網頁可以 [從CDN讀取jQuery檔案](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) 或嵌入了jQuery的本地副本。 jQuery是呈現自適應表單所必需的。
* 當服AEM務器和網頁位於不同的域上時，請執行一節中列出的步驟。 [使AEM Forms能夠為跨域站點提供自適應表單](#cross-site)。

## 嵌入自適應表單 {#embed-adaptive-form}

通過在網頁中插入幾行JavaScript，可以嵌入自適應表單。 代碼中的API向伺服器發送HTTP請AEM求以獲取自適應表單資源，並在指定的表單容器中彈出自適應表單。

要嵌入自適應表單：

1. 在您的網站上建立包含以下代碼的網頁：

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

1. 在嵌入代碼中：

   * 更改 *選項.path* 變數，其路徑為自適應表單的發佈URL。 如果服AEM務器正在上下文路徑上運行，請確保URL包含上下文路徑。 始終提及包括擴展的自適應表單的完整名稱。   例如，上述代碼和adaptive from位於同一表單伺服器AEM上，因此該示例使用adaptive form /content/forms/af/locbasic.html的上下文路徑。
   * 替換 *選項.dataRef* 與URL一起傳遞的屬性。 可以使用dataref變數 [預填自適應表單](/help/forms/using/prepopulate-adaptive-form-fields.md)。
   * 替換 *options.themePath* 的子目錄。 或者，可以使用request屬性指定主題路徑。
   * CSS_Selector是嵌入自適應表單的表單容器的CSS選擇器。 例如，.customafsection css類是上例中的CSS選擇器。

自適應表單嵌入到網頁中。 在嵌入式自適應表單中觀察以下內容：

* 原始自適應表單中的頁眉和頁腳不包括在嵌入表單中。
* 草稿和提交的表格可在Forms門戶的「草稿和提交」頁籤中找到。
* 在原始自適應表單上配置的提交操作將保留在嵌入式表單中。
* 自適應表單規則在嵌入式表單中被保留和完全功能化。
* 在原始自適應表單中配置的體驗目標和A/Btest在嵌入式表單中不起作用。
* 如果在原始窗體上配置了Adobe Analytics，則分析資料將在Adobe Analytics伺服器中捕獲。 但是，Forms分析報告沒有提供。

## 拓撲示例 {#sample-topology}

嵌入自適應表單的外部網頁會將請求發送到伺服器AEM，伺服器通常位於專用網路中防火牆的後面。 為確保將請求安全地定向AEM到伺服器，建議設定反向代理伺服器。

讓我們看一個示例，您如何在沒有調度程式的情況下設定Apache 2.4反向代理伺服器。 在本示例中，您將使用 `/forms` 上下文路徑和映射 `/forms` 的下界。 它確保 `/forms` Apache伺服器上的實例AEM。 此拓撲有助於減少調度器層上所有請求的前置詞時的規則數 `/forms` 路由到服AEM務器。

1. 開啟 `httpd.conf` 並取消注釋以下代碼行。 或者，可以在檔案中添加這些代碼行。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 通過在中添加以下代碼行來設定代理規則 `httpd-proxy.conf` 配置檔案。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   替換 `[AEM_Instance]` 以及AEM伺服器發佈URL。

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
>如果設定了任何其他拓撲，請確保將提交、預填充和其他URL添加到調度程式層的允許清單中。

## 最佳做法 {#best-practices}

在網頁中嵌入自適應表單時，請考慮以下最佳做法：

* 確保網頁CSS中定義的樣式規則與表單對象CSS不衝突。 為避免衝突，可以使用客戶端庫在自適應表單主題中重AEM用網頁CSS。 有關在自適應表單主題中使用客戶端庫的資訊，請參見 [AEM Forms主題](../../forms/using/themes.md)。
* 使網頁中的表單容器使用整個窗口寬度。 它確保為移動設備配置的CSS規則在不進行任何更改的情況下工作。 如果表單容器不採用整個窗口寬度，則需要編寫自定義CSS以使表單適應不同的移動設備。
* 使用 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API，用於獲取客戶端中表單資料的XML或JSON表示。
* 使用 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` 從HTMLDOM卸載自適應表單的API。
* 從伺服器發送響應時設定訪問控制源報AEM頭。

## 使AEM Forms能夠為跨域站點提供自適應表單 {#cross-site}

1. 在發AEM布實例上，轉AEM到Web Console Configuration Manager `https://'[server]:[port]'/system/console/configMgr`。
1. 查找並開啟 **Apache Sling引用篩選器** 配置。
1. 在「允許的主機」欄位中，指定網頁所在的域。 它使主機能夠向伺服器發出POSTAEM請求。 也可以使用規則運算式指定一系列外部應用程式域。
