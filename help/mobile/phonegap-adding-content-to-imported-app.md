---
title: 您的混合應用程式是否已準備好適用於AEM Mobile?
seo-title: 您的混合應用程式是否已準備好適用於AEM Mobile?
description: 請依照本頁瞭解混合應用程式。 AEM中的應用程式通常分為兩個部分。 'shell'和'content'和本頁提供這些主題的更多見解。
seo-description: 請依照本頁瞭解混合應用程式。 AEM中的應用程式通常分為兩個部分。 'shell'和'content'和本頁提供這些主題的更多見解。
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 您的混合應用程式是否已準備好適用於AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

所以您已將Hybrid phoneGap或Cordova應用程式匯入AEM，現在該怎麼辦？ 您可能會想要新增可授權的內容至您的應用程式。 若要完成這項工作，您必須對AEM應用程式的結構有大致的瞭解。 AEM中的應用程式通常分為兩個部分。 &#39;shell&#39;和&#39;content&#39;。 「shell」包含應用程式的靜態部分；例如PhoneGap設定檔案、應用程式架構和導覽控制項。 您導入的歸檔檔案的內容將作為殼的一部分進行儲存。 在本檔案中，shell是應用程式開發人員建立之Hybrid PhoneGap應用程式中，所有非AEM製作的內容。

內容是指在AEM開發人員建立的AEM中編寫的元件、範本和編寫的頁面。 內容可歸類為開發人員內容或撰寫內容。 元件、設計和頁面範本被視為開發內容，因為這些範本是由開發人員建立。 作者內容是使用元件和範本建立的頁面。 這些作業通常由設計人員或行銷人員完成。

將編寫的AEM頁面新增至您的Hybrid應用程式時，應用程式開發人員與AEM開發人員必須進行協調。 在您想要新增創作內容的應用程式中，應用程式開發人員必須以可在AEM中覆蓋的結構來組織這些頁面。 應用程式開發人員必須能夠提供AEM開發人員AEM製作內容的新增路徑，然後在Hybrid應用程式中提供預留位置頁面，在AEM開發人員製作頁面內容後，該預留位置頁面將會被取代。

為了讓說明更容易遵循，我們將使用AEM Marketing Cloud:AEM Mobile Hybrid Reference，以說明概念。 混合參考應用程式包含附加選單的歡迎頁面。

![chlimage_1-76](assets/chlimage_1-76.png)

在此範例中，我們將製作應用程式的歡迎頁面。 瀏覽來源https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75 [](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75)。 我們看到應用程式開發人員已定義歡迎頁面，並提供應用程式轉譯之頁面的範本。 這是應用程式開發人員和AEM開發人員需要協調的地方。 混合參考應用程式中歡迎頁面範本的路徑定義為「content/mobileapps/hybrid-reference-app/en/welcome.template.html」。 此路徑非常重要，因為AEM開發人員會使用相同的路徑，在AEM儲存庫中編寫其歡迎頁面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合應用程式和AEM製作的內容使用相同路徑很重要，因為我們依賴使用「內容同步」來覆蓋內容的能力，將新頁面新增至混合應用程式。 當「混合應用程式」匯入AEM做為匯入程式的一部分時，就會設定「內容同步」設定。

![chlimage_1-78](assets/chlimage_1-78.png)

當您從應用程式儀表板「下載來源」時，會執行這些ContentSync指令碼來組合混合應用程式的封存。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync會先提取應用程式的&#39;shell&#39;，然後提取應用程式的&#39;content&#39;。 現在，如果&#39;shell&#39;中有與&#39;content&#39;路徑相同的頁面，&#39;shell&#39;下的頁面將（取代）&#39;content&#39;下的頁面。 換言之，如果我們在AEM中建立與「content/mobileapps/hybrid-reference-app/en/welcome.template.html」路徑相同的頁面（當ContentSync執行時），在「混合參考應用程式」範例中，該頁面將覆蓋屬於Hybrid Reference應用程式一部分的頁面，以及位於該位置的AEM中的任何頁面。 覆蓋由ContentSync負責處理，因此對於使用應用程式的人，使用AEM製作內容的應用程式更新看起來會很順暢，而且不需要重建應用程式。 因此，當您執行應用程式時，歡迎頁面會顯示如下：

![chlimage_1-80](assets/chlimage_1-80.png)
