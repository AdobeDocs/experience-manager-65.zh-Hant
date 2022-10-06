---
title: 您的混合應用程式已準備好迎接AEM Mobile嗎？
seo-title: Is your hybrid app ready for AEM Mobile?
description: 請詳閱本頁以了解混合應用程式。 AEM中的應用程式通常分為兩個部分。 「shell」和「content」以及此頁面提供關於這些主題的更深入分析。
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# 您的混合應用程式已準備好迎接AEM Mobile嗎？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

您已將Hybrid PhoneGap或Cordova應用程式匯入AEM，現在怎麼辦？ 您可能想要將可授權內容新增至應用程式。 若要完成此工作，您必須對AEM應用程式的結構有一般的了解。 AEM中的應用程式通常分為兩個部分。 &#39;shell&#39;和&#39;content&#39;。 「殼層」由應用程式的靜態部分組成；例如PhoneGap組態檔、應用程式架構和導覽控制項。 您導入的歸檔檔案的內容將作為殼的一部分儲存。 在本檔案的內容中，殼層是應用程式開發人員所建置之Hybrid PhoneGap應用程式的所有非AEM撰寫內容。

內容是指由AEM開發人員在AEM中建立的元件、範本和製作的頁面。 內容可分類為開發人員內容或撰寫內容。 元件、設計和頁面範本是開發內容，因為是由開發人員建立。 作者內容是使用元件和範本建立的頁面。 這通常由設計人員或行銷人員執行。

將製作的AEM頁面新增至您的混合式應用程式，需要應用程式開發人員與AEM開發人員進行協調。 在您想要新增製作內容的應用程式中，任何地方，應用程式開發人員都必須以可在AEM中覆蓋的結構來組織這些頁面。 應用程式開發人員必須能為AEM開發人員提供要新增AEM製作內容的路徑，然後在混合式應用程式中提供預留位置頁面，該預留位置頁面將在AEM開發人員製作頁面內容後取代。

為了更方便地遵循說明，我們將使用AEMMarketing Cloud:AEM Mobile混合參考，以說明概念。 混合參考應用程式包含含有側面功能表的歡迎頁面。

![chlimage_1-76](assets/chlimage_1-76.png)

在此範例中，我們將製作應用程式的歡迎頁面。 看看源頭 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). 我們發現應用程式開發人員已定義歡迎頁面，並提供應用程式轉譯之頁面的範本。 這是應用程式開發人員和AEM開發人員需要協調的位置。 混合參考應用程式中歡迎頁面範本的路徑定義為「content/mobileapps/hybrid-reference-app/en/welcome.template.html」。 此路徑非常重要，因為AEM開發人員會使用相同的路徑，在AEM存放庫中製作其歡迎頁面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合式應用程式和AEM製作的內容必須使用相同的路徑，因為我們仰賴使用「內容同步」覆蓋內容的功能，將新頁面新增至混合式應用程式。 在匯入程式中將混合應用程式匯入AEM時，會設定內容同步設定。

![chlimage_1-78](assets/chlimage_1-78.png)

當您從應用程式控制面板「下載來源」時，這些ContentSync指令碼會執行以匯整混合應用程式的封存檔。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync先提取應用程式的「shell」，然後提取應用程式的「content」。 現在，如果「殼層」中有與「內容」中路徑相同的頁面，則「殼層」下的頁面將會（取代）為「內容」下的頁面。 換言之，如果我們在AEM中建立頁面，當ContentSync執行時，其路徑與「content/mobileapps/hybrid-reference-app/en/welcome.template.html」相同，則在混合參考應用程式範例中，該頁面將會覆蓋屬於混合參考應用程式一部分的頁面，並包含該位置AEM中的任何頁面。 覆蓋圖會由ContentSync負責處理，因此對於使用應用程式的使用者，對具有AEM撰寫內容之應用程式的更新看起來會順暢無礙，不需要重建應用程式。 因此，當您執行應用程式時，歡迎頁面會顯示如下：

![chlimage_1-80](assets/chlimage_1-80.png)
