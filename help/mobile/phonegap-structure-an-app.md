---
title: 建構應用程式
seo-title: Structure an App
description: 請依照本頁面了解如何建立應用程式結構。 本頁面說明如何結構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
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

# 建構應用程式{#structure-an-app}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile專案包含一組不同的內容類型，包括頁面、JavaScript和CSS用戶端程式庫、可重複使用的AEM元件、內容同步設定，以及PhoneGap應用程式殼層內容。 讓新的AEM Mobile應用程式以 [入門套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 是將所有不同類型的內容納入我們建議的結構中的好方法，從長期來看，它可以簡化可移植性和可維護性。

## 頁面內容 {#page-content}

您應用程式的頁面應位於/content/mobileapps下方，以便AEM Mobile主控台辨識。

![chlimage_1-52](assets/chlimage_1-52.png)

根據AEM慣例，應用程式的第一頁應重新導向至其子頁，作為應用程式的預設語言(在Geometrixx和Starter Kit案例中為「en」)。 頂級區域設定頁通常繼承自基礎的「閃屏頁」元件(/libs/mobileapps/components/splash-page)，該元件負責支援安裝空中內容同步更新所需的初始化(contentInit代碼位於/etc/clientlibs/mobile/content-sync/js/contentInit.js)。

## 範本和元件 {#templates-and-components}

您應用程式的範本和元件程式碼應位於/apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 根據慣例，您應將範本和元件程式碼放入/apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 在AEM中已使用Site的開發人員應熟悉此模式。 通常後跟為/apps/，依預設會在發佈執行個體上鎖定為匿名存取。 因此，您的原始JSP代碼被隱藏起來，而不會受到潛在攻擊者的攻擊。

應用程式特定範本可設定為只顯示，方法是使用 `allowedPaths` 屬性節點，並將其值設為「/content/mobileapps(/)」。&amp;ast;)?&#39;  — 如果範本僅適用於單一應用程式，則可使用更明確的功能。 此 `allowedParents` 和 `allowedChildren` 您也可以運用屬性，根據建立新頁面的位置，對作者將可使用哪些範本進行非常細微的控制。

從草稿開始建立新的應用程式頁面元件時，建議將 `sling:resourceSuperType` 屬性至&#39;mobileapps/components/angular/ng-page&#39;。 這將設定您的頁面，以便製作和呈現為單頁應用程式，並讓您覆蓋元件可能需要變更的任何.jsp檔案。 由於ng-page完全不包含任何UI架構，因此開發人員通常會覆蓋（至少）「template.jsp」(從/libs/mobileapps/components/angular/ng-page/template.jsp重疊)。

想要運用AngularJS的可授權頁面元件有同等的 `sling:resourceSuperType` 元件(位於/libs/mobileapps/components/angular/ng-component)，可以以相同方式重疊和自訂。

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

有關用戶端程式庫，開發人員可以使用一些選項，將其放置在存放庫中。 以下模式可供指導，但並非難事。

如果您的客戶端代碼可以獨立運行，並且與應用程式的特定元件無關（這意味著該代碼可能在其他應用程式中重複使用），建議將其儲存在/etc/clientlibs/中&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. 另一方面，如果clientlib是單一應用程式專屬的，您可以將其巢狀內嵌為應用程式設計節點的子節點；/etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs。 此clientlib的類別不應供其他lib使用，並應視需要用來內嵌其他lib。 依照這種模式，開發人員不必在每次將用戶端程式庫新增至應用程式時，新增內容同步設定，而只需更新應用程式設計clientlib的「內嵌」屬性。 例如，查看位於/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all的Geometrixxclientlibs-all內容同步設定節點。

如果您的用戶端代碼與特定元件緊密耦合，請將該代碼放置在元件位於/apps/下方的巢狀用戶端程式庫中，並將其類別嵌入您應用程式的「design」clientlib中。

## PhoneGap設定 {#phonegap-configuration}

每個AEM Mobile應用程式都包含一個目錄，其中包含PhoneGap使用的組態檔 [命令行介面](https://github.com/phonegap/phonegap-cli) 和 [PhoneGap組建](https://build.phonegap.com/) 將網頁內容轉換為可執行的應用程式。 在例項的Geometrixx範例中，此目錄(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)位於殼層中；由於其僅包含無法透過空中更新的內容（例如處理裝置API的外掛程式和應用程式本身的設定），所以做出設計決策。

在此目錄中，您也會找到 [科爾多瓦鈎](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) 可用來安裝外掛程式、將資源檔案置於其平台特定位置，以及其他應在組建中執行的動作。 注意：作為下載每個外掛程式的替代項目，您可以依照Kitchen Sink應用程式和 [包含外掛程式原始碼](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) 與您其他應用程式專案搭配。

## 後續步驟 {#the-next-steps}

了解應用程式的結構後，請參閱 [使用App Console建立和編輯應用程式](/help/mobile/phonegap-apps-console.md).
