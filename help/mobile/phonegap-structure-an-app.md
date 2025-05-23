---
title: 建構應用程式
description: 請依照本頁面的說明進行，瞭解如何建立應用程式的結構。 本頁面說明如何建構範本和元件，以及JavaScript和CSS Clientlibs的相關資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# 建構應用程式{#structure-an-app}

{{ue-over-mobile}}

AEM Mobile專案涉及多樣化的內容型別集，包括頁面、JavaScript和CSS使用者端資料庫、可重複使用的AEM元件、Content Sync設定和PhoneGap應用程式殼層內容。 以[入門套件](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)為基礎使用新的AEM Mobile應用程式，是將所有不同型別的內容整合到我們建議的結構中的好方法，以簡化長期的可攜性和可維護性。

## 頁面內容 {#page-content}

您應用程式的頁面應該全都位於/content/mobileapps下方，以便AEM Mobile主控台可辨識這些頁面。

![chlimage_1-52](assets/chlimage_1-52.png)

根據AEM慣例，應用程式的第一個頁面應為重新導向至其子項之一，做為應用程式的預設語言(在Geometrixx和入門套件案例中均為「en」)。 頂級地區設定頁面通常會繼承自foundation「splash-page」元件(/libs/mobileapps/components/splash-page)，該元件會負責支援安裝Over-the-Air Content Sync更新所需的初始化(contentInit程式碼位於/etc/clientlibs/mobile/content-sync/js/contentInit.js)。

## 範本和元件 {#templates-and-components}

您應用程式的範本和元件程式碼應位於/apps/&lt;brand name>/&lt;app name>中。 依照慣例，您應該將範本和元件程式碼放在/apps/&lt;brand name>/&lt;app name>中。 已經在AEM中操作過Site的開發人員應該熟悉此模式。 通常會接著執行，因為/apps/預設會被鎖定以供發佈執行個體匿名存取。 因此，您的原始JSP程式碼會隱藏起來，不讓潛在攻擊者看到。

應用程式專屬的範本可設定為僅透過使用範本本身上的`allowedPaths`屬性節點，並將其值設定為&#39;/content/mobileapps(/)來呈現。&amp;amp；ast；)？&#39;  — 或甚至是更具體的專案（如果範本只能用於單一應用程式）。 `allowedParents`和`allowedChildren`屬性也可用來進行微調控制，以根據建立新頁面的位置，讓作者可以使用哪些範本。

從頭開始建立應用程式頁面元件時，建議將其`sling:resourceSuperType`屬性設為&#39;mobileapps/components/angular/ng-page&#39;。 這會將您的頁面設定為以單頁應用程式進行製作和呈現，並讓您覆蓋元件可能需要變更的任何.jsp檔案。 由於ng-page完全不包含任何UI架構，開發人員通常最後會重疊（至少）「template.jsp」(從/libs/mobileapps/components/angular/ng-page/template.jsp重疊)。

想要使用AngularJS的可編寫頁面元件在/libs/mobileapps/components/angular/ng-component有同等的`sling:resourceSuperType`元件，可以相同方式加以覆蓋和自訂。

## JavaScript與CSS Clientlibs {#javascript-and-css-clientlibs}

在使用者端資料庫中，開發人員有一些選項可讓您選擇將資料放在存放庫中的位置。 以下模式僅供參考，並非硬性要求。

如果您的使用者端程式碼可以獨立運作，而且與應用程式的特定元件無關（這表示它可以在其他應用程式中重複使用），Adobe建議將其儲存在/etc/clientlibs/&lt;brand name>/&lt;lib name>中。 另一方面，如果clientlib是單一應用程式所專屬，您可以將它巢狀內嵌，做為應用程式設計節點( /etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs)的子系。 請勿將此clientlib的類別搭配其他程式庫使用；請視需要嵌入其他程式庫。 遵循此模式可讓開發人員無須在每次將使用者端程式庫新增至應用程式時都新增新的Content Sync設定，而只需更新應用程式設計clientlib的「embeds」屬性。 例如，檢視/content/phonegap/geometrixx-outdoors/en/jcr：content/pge-app/app-config/clientlibs-all中的Geometrixxclientlibs-all Content Sync設定節點。

如果您的使用者端程式碼與特定元件緊密結合，請將該程式碼放置在巢狀內嵌於/apps/中元件位置下方的使用者端程式庫中，並將其類別內嵌至應用程式的「設計」clientlib。

## PhoneGap設定 {#phonegap-configuration}

每個AEM Mobile應用程式都包含一個目錄，其中主控了PhoneGap [命令列介面](https://github.com/phonegap/phonegap-cli)和位於`https://build.phonegap.com/`的PhoneGap Build所使用的設定檔案，以將您的網頁內容轉換為可執行的應用程式。 舉例來說，在Geometrixx範例中，此目錄(/content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content)位於殼層中；之所以會做出設計決策，是因為其中僅包含無法直接更新的內容，例如處理裝置API和應用程式本身設定的外掛程式。

在此目錄中，您也會找到一些[Cordova鉤點](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide)，可用來安裝外掛程式、將資源檔案放置在其平台特定位置，以及其他應在組建中執行的動作。 注意：除了在建置中下載每個外掛程式之外，您也可以遵循Kitchen Sink應用程式的模式，並將外掛程式原始程式碼<!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) -->包含在您的其他應用程式專案中。

## 後續步驟 {#the-next-steps}

瞭解應用程式的結構後，請參閱[使用應用程式主控台建立和編輯應用程式](/help/mobile/phonegap-apps-console.md)。
