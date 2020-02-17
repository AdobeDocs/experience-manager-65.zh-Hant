---
title: 建構應用程式
seo-title: 建構應用程式
description: 請依照本頁來瞭解如何建立應用程式結構。 本頁說明如何建構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
seo-description: 請依照本頁來瞭解如何建立應用程式結構。 本頁說明如何建構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 建構應用程式{#structure-an-app}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

AEM mobile專案包含多種內容類型，包括頁面、JavaScript和CSS用戶端程式庫、可重複使用的AEM元件、內容同步設定和PhoneGap應用程式殼層內容。 以 [](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) Starter Kit為基礎建立新的AEM mobile應用程式，是將所有不同類型的內容整合到我們建議結構中的好方法，從長遠來看，可輕鬆移植性和可維護性。

## 頁面內容 {#page-content}

您應用程式的頁面都應位於/content/mobileapps下方，以便讓AEM mobile主控台識別。

![chlimage_1-52](assets/chlimage_1-52.png)

根據AEM慣例，您應用程式的第一頁應重新導向至其子系，做為應用程式的預設語言（在Geometrixx和Starter kit案例中均為&#39;en&#39;）。 頂層地區設定頁面通常繼承自基礎的「splash-page」元件(/libs/mobileapps/components/splash-page)，其中負責支援安裝空中內容同步更新所需的初始化(contentInit程式碼可在/etc/clientlibs/mobile/content-sync/js/contentInit.js上找到)。

## 範本和元件 {#templates-and-components}

您應用程式的範本和元件代碼應位於/apps/&lt;brand name>/&lt;app name>。 根據慣例，您應將範本和元件程式碼置於/apps/&lt;brand name>/&lt;app name>中。 對於已在AEM中與Site合作的開發人員而言，這種模式應該很熟悉。 通常會隨附於發佈例項上，預設會鎖定/apps/以匿名方式存取。 因此，您的原始JSP程式碼會隱藏在潛在攻擊者之外。

應用程式特定範本可設定為只顯示，方法是使用範本本身的 `allowedPaths` 屬性節點，並將其值設為&#39;/content/mobileapps(/)。&amp;ast;?&#39; -或者，如果範本僅適用於單一應用程式，則更具體的功能。 您也 `allowedParents` 可運 `allowedChildren` 用和屬性，根據建立新頁面的位置，精確控製作者可使用哪些範本。

從頭開始建立新的應用程式頁面元件時，建議將其屬性設 `sling:resourceSuperType` 定為「mobileapps/components/angular/ng-page」。 如此可將您的頁面設定為製作和轉換為單一頁面應用程式，並讓您覆蓋元件可能需要變更的任何。jsp檔案。 由於ng-page完全不包含任何UI架構，因此開發人員通常會覆蓋（至少）&#39;template.jsp&#39;(從/libs/mobileapps/components/angular/ng-page/template.jsp覆蓋)。

想要運用AngularJS的可授權頁面元件，在/libs/mobileapps/components/angular/ng-component中有等同的元件，可以以相同的方式重疊和自訂。 `sling:resourceSuperType`

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

在客戶端庫方面，開發人員有一些選項可供選擇，以將它們放在儲存庫中。 以下是可供引導的，但並非難點。

如果您的客戶端代碼可以獨立運行，並且與應用程式的特定元件無關（也就是說，該代碼可以在其他應用程式中重複使用），我們建議將其儲存在/etc/clientlibs/&lt;brand name>/&lt;lib name>中。 另一方面，如果clientlib是單一應用程式專屬的，您可以將它當成應用程式設計節點的子系巢狀內嵌；/etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs。 此clientlib的類別不應被其他lib使用，而且應當用於根據需要嵌入其他lib。 依照此模式，開發人員不必在每次將用戶端程式庫新增至應用程式時新增內容同步設定，而只需更新應用程式設計clientlib的「內嵌式」屬性。 例如，請查看位於/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all的Geometrixx clientlibs-all內容同步設定節點。

如果您的用戶端程式碼與特定元件緊密連結，請將該程式碼放在元件位置/apps/下方巢狀的用戶端程式庫中，然後將其類別內嵌在您應用程式的&#39;design&#39;clientlib中。

## PhoneGap設定 {#phonegap-configuration}

每個AEM mobile應用程式都包含一個目錄，其中主控PhoneGap命令列介面和 [](https://github.com/phonegap/phonegap-cli)[](https://build.phonegap.com/) PhoneGap組建版本所使用的設定檔案，以將您的Web內容轉換為可執行的應用程式。 例如，在Geometrixx範例中，此目錄(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)位於Shell的一部分；由於它僅包含無法透過無線方式更新的內容，例如處理裝置API的外掛程式和應用程式本身的組態，所以作出設計決定。

在此目錄中，您也會找到許多 [](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) Cordova掛接，這些掛接可用來安裝外掛程式、將資源檔案置於其平台特定位置，以及其他應在建立時執行的動作。 注意：除了下載每個外掛程式做為組建版本的一部分，您可以依照Kitchen Sink應用程式的模式，並將外掛程式原始碼 [加入其餘的應用程式專案](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) 。

## 後續步驟 {#the-next-steps}

一旦您瞭解應用程式的「結構」後，請參閱「使 [用App Console建立和編輯應用程式」](/help/mobile/phonegap-apps-console.md)。
