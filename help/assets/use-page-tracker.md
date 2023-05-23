---
title: 使用頁面跟蹤器並在網頁中嵌入代碼
description: 瞭解如何在您的網站代碼中包括頁面跟蹤器並嵌入JavaScript代碼，以便Adobe Analytics能夠捕獲圍繞資產的使用情況資料。
contentOwner: AG
role: Architect, Admin
feature: Asset Reports
exl-id: 14d02015-df00-4566-a098-de76eaf42605
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# 使用頁面跟蹤器並在網頁中嵌入代碼 {#using-page-tracker-and-embed-code-in-web-pages}

「頁面跟蹤器」是JavaScript代碼的一部分，您將其包含在第三方網站的代碼中，以使Adobe Analytics能夠捕獲周圍的使用資料 [!DNL Adobe Experience Manager Assets] 在這些網站上。

要捕獲特定於資產的事件（如點擊等），還應在第三方網站的代碼中包含嵌入代碼。

以下示例代碼顯示包含「頁跟蹤器」代碼和「嵌入」代碼的網頁的外觀：

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## 添加頁跟蹤器代碼 {#adding-page-tracker-code}

在網站代碼的標題部分中添加頁面跟蹤器代碼。 以下代碼段顯示示例網頁中包含的Page Tracker代碼：

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## 添加嵌入代碼 {#add-embed-code}

將嵌入代碼添加到網站代碼正文中。 以下代碼段顯示示例網頁中包含的嵌入代碼：

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
