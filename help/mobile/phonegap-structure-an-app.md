---
title: 構造應用
seo-title: Structure an App
description: 按照此頁瞭解如何建立應用的結構。 本頁介紹如何構造模板和元件以及有關JavaScript和CSS客戶端的資訊。
seo-description: Follow this page to learn about how to create structure of an app. This page describes how to structure templates and components along with information on JavaScript and CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 構造應用{#structure-an-app}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

AEM Mobile項目涉及一組多樣的內容類型，包括頁面、JavaScript和CSS客戶端庫、可重用組AEM件、內容同步配置和PhoneGap應用程式外殼內容。 基於您的新AEM Mobile應用 [入門套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 是將所有不同類型的內容納入我們推薦的結構中的好方法，從長期來看，它既方便了可移植性，又可維護性。

## 頁面內容 {#page-content}

您的應用程式的頁面都應位於/content/mobileapps下方，以便AEM Mobile控制台識別這些頁面。

![chlimage_1-52](assets/chlimage_1-52.png)

按照AEM慣例，應用程式的第一頁應重定向到其中一個子級，該子級用作應用程式的預設語言(在Geometrixx和入門套件中都是「en」)。 頂級區域設定頁面通常繼承自基礎的「閃屏」元件（/libs/mobileapps/components/閃屏），該元件負責支援空中內容同步更新安裝所需的初始化(contentInit代碼可在/etc/clientlibs/mobile/content-sync/js/contentInit.js上找到)。

## 模板和元件 {#templates-and-components}

您應用的模板和元件代碼應位於/apps/中&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>。 按照慣例，您應將模板和元件代碼放在/apps/中&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>。 對於已在中與Site合作的開發人員來說，這種模式應該很AEM熟悉。 通常，在發佈實例上，會將/apps/鎖定為匿名訪問。 因此，您的原始JSP代碼被隱藏在潛在攻擊者之外。

應用程式特定模板只能通過 `allowedPaths` 模板本身上的屬性節點，並將其值設定為「/content/mobileapps(/)」。&amp;ast;)?&#39;  — 如果模板只能用於單個應用，則更具體。 的 `allowedParents` 和 `allowedChildren` 還可以利用屬性進行非常精細的控制，根據新頁面的建立位置，作者將可以使用哪些模板。

從頭建立新應用頁面元件時，建議將 `sling:resourceSuperType` 屬性到「mobileapps/components/angular/ng-page」。 這將設定您的頁面，以作為單頁應用進行創作和呈現，並使您能夠覆蓋元件可能需要更改的任何.jsp檔案。 由於ng-page根本不包含任何UI框架，因此開發人員通常最終會覆蓋（至少）「template.jsp」(從/libs/mobileapps/components/angular/ng-page/template.jsp重疊)。

可授權的頁面元件希望利用AngularJS，具有等效的 `sling:resourceSuperType` 元件位於/libs/mobileapps/components/angular/ng-component處，可以以相同方式重疊和自定義。

## JavaScript和CSS客戶端 {#javascript-and-css-clientlibs}

在客戶端庫方面，開發人員可以使用幾個選項來將它們放置在儲存庫中的位置。 以下模式可供指導，但並不難：

如果您的客戶端代碼可以獨立儲存，並且與應用程式的特定元件無關 — 這意味著它可能會在其他應用程式中重複使用 — 我們建議將它儲存在/etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>。 另一方面，如果客戶端庫是特定於單個應用程式，則可以將其嵌套為應用程式設計節點的子級；/etc/designs/phonegap//&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs。 此客戶端庫的類別不應被其他lib使用，並應根據需要用於嵌入其他lib。 按照此模式，開發人員不必在每次將客戶端庫添加到應用程式時都添加新的內容同步配置，而只需更新應用程式設計客戶端庫的「embeds」屬性。 例如，請查看位於/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all的Geometrixx客戶端所有內容同步配置節點。

如果客戶端代碼與特定元件緊密耦合，請將該代碼放在/apps/中嵌套在元件位置下方的客戶端庫中，並將其類別嵌入應用的「design」客戶端庫。

## PhoneGap配置 {#phonegap-configuration}

每個AEM Mobile應用都包含一個目錄，該目錄承載PhoneGap使用的配置檔案 [命令行介面](https://github.com/phonegap/phonegap-cli) 和 [PhoneGap生成](https://build.phonegap.com/) 將Web內容轉換為可運行的應用程式。 例如，在Geometrixx示例中，此目錄(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)作為Shell的一部分；由於它只包含不能通過空中更新的內容（如處理設備API的插件和應用程式本身的配置）而做出的設計決策。

在此目錄中，您還會找到 [科爾多瓦鈎子](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) 可用於安裝插件、將資源檔案放置在其平台特定位置以及作為生成一部分執行的其他操作。 注：作為下載每個插件作為構建的一部分的替代方法，您可以遵循Kitchen Sink應用的模式， [包含插件原始碼](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) 你其餘的應用項目。

## 後續步驟 {#the-next-steps}

一旦您瞭解了應用的結構，請參閱 [使用應用控制台建立和編輯應用](/help/mobile/phonegap-apps-console.md)。
