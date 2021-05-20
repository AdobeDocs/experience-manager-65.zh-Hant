---
title: 建構應用程式
seo-title: 建構應用程式
description: 請依照本頁面了解如何建立應用程式結構。 本頁面說明如何結構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
seo-description: 請依照本頁面了解如何建立應用程式結構。 本頁面說明如何結構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 建構應用程式{#structure-an-app}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile專案包含一組不同的內容類型，包括頁面、JavaScript和CSS用戶端程式庫、可重複使用的AEM元件、內容同步設定，以及PhoneGap應用程式殼層內容。 將您的新AEM Mobile應用程式設定在[入門套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)上，是將所有不同類型的內容整合到我們建議結構中的好方法，從長遠來看，可輕鬆移植和維護。

## 頁面內容{#page-content}

您應用程式的頁面應位於/content/mobileapps下方，以便AEM Mobile主控台辨識。

![chlimage_1-52](assets/chlimage_1-52.png)

根據AEM慣例，應用程式的第一頁應重新導向至其子頁，作為應用程式的預設語言(在Geometrixx和Starter Kit案例中為「en」)。 頂級區域設定頁通常繼承自基礎的「閃屏頁」元件(/libs/mobileapps/components/splash-page)，該元件負責支援安裝空中內容同步更新所需的初始化(contentInit代碼位於/etc/clientlibs/mobile/content-sync/js/contentInit.js)。

## 模板和元件{#templates-and-components}

您應用程式的範本和元件程式碼應位於/apps/&lt;brand name>/&lt;app name>。 根據慣例，您應將範本和元件程式碼放置在/apps/&lt;brand name>/&lt;app name>中。 在AEM中已使用Site的開發人員應熟悉此模式。 通常後跟為/apps/，依預設會在發佈執行個體上鎖定為匿名存取。 因此，您的原始JSP代碼被隱藏起來，而不會受到潛在攻擊者的攻擊。

只能通過使用模板本身上的`allowedPaths`屬性節點並將其值設定為「/content/mobileapps(/)，將應用程式特定模板配置為顯示。&amp;ast;)?&#39;  — 如果範本僅適用於單一應用程式，則可使用更明確的功能。 也可以運用`allowedParents`和`allowedChildren`屬性，根據建立新頁面的位置，對作者可使用的範本執行非常細微的控制。

從草稿開始建立新應用程式頁面元件時，建議將其`sling:resourceSuperType`屬性設為「mobileapps/components/angular/ng-page」。 這將設定您的頁面，以便製作和呈現為單頁應用程式，並讓您覆蓋元件可能需要變更的任何.jsp檔案。 由於ng-page完全不包含任何UI架構，因此開發人員通常會覆蓋（至少）「template.jsp」(從/libs/mobileapps/components/angular/ng-page/template.jsp重疊)。

可授權的頁面元件（希望運用AngularJS）位於/libs/mobileapps/components/angular/ng-component，具有等同的`sling:resourceSuperType`元件，可以以相同方式重疊和自訂。

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

有關用戶端程式庫，開發人員可以使用一些選項，將其放置在存放庫中。 以下模式可供指導，但並非難事。

如果您的客戶端代碼可以獨立運行，並且與應用程式的特定元件無關（這表示該代碼可能在其他應用程式中重複使用），建議將其儲存在/etc/clientlibs/&lt;brand name>/&lt;lib name>中。 另一方面，如果clientlib是單一應用程式專屬的，您可以將其巢狀內嵌為應用程式設計節點的子節點；/etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs。 此clientlib的類別不應供其他lib使用，並應視需要用來內嵌其他lib。 依照這種模式，開發人員不必在每次將用戶端程式庫新增至應用程式時，新增內容同步設定，而只需更新應用程式設計clientlib的「內嵌」屬性。 例如，查看位於/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all的Geometrixxclientlibs-all內容同步設定節點。

如果您的用戶端代碼與特定元件緊密耦合，請將該代碼放置在元件位於/apps/下方的巢狀用戶端程式庫中，並將其類別嵌入您應用程式的「design」clientlib中。

## PhoneGap配置{#phonegap-configuration}

每個AEM Mobile應用程式都包含一個目錄，其中包含PhoneGap [命令列介面](https://github.com/phonegap/phonegap-cli)和[PhoneGap組建](https://build.phonegap.com/)所使用的組態檔，以將您的Web內容轉換為可執行的應用程式。 在例項的Geometrixx範例中，此目錄(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)位於殼層中；由於其僅包含無法透過空中更新的內容（例如處理裝置API的外掛程式和應用程式本身的設定），所以做出設計決策。

在此目錄中，您也會找到數個[Cordova hooks](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide)，可用來安裝外掛程式、將資源檔案置於其平台特定位置，以及其他應在組建中執行的動作。 注意：除了在組建中下載每個外掛程式，您還可以依照Kitchen Sink應用程式的模式，並在其餘的應用程式專案中遵循[包含外掛程式原始碼](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins)。

## 後續步驟{#the-next-steps}

了解應用程式的結構後，請參閱使用App Console建立和編輯應用程式](/help/mobile/phonegap-apps-console.md)。[
