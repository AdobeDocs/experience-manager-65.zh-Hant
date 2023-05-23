---
title: 你的混合應用準備好迎接AEM Mobile了嗎？
seo-title: Is your hybrid app ready for AEM Mobile?
description: 按照本頁瞭解混合應用。 中的應AEM用通常分為兩部分。 「shell」和「內容」以及此頁提供了有關這些主題的更多見解。
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

# 你的混合應用準備好迎接AEM Mobile了嗎？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

所以你已經將Hybrid PhoneGap或Cordova應用導入AEM了，現在呢？ 您可能希望將可授權內容添加到您的應用中。 要完成此任務，您需要對應用程式的結構有一個全面AEM的瞭解。 中的應AEM用通常分為兩部分。 「shell」和「content」。 「shell」由應用的靜態部分組成；如PhoneGap配置檔案、應用框架和導航控制項。 導入的存檔的內容將作為shell的一部分儲存。 在此文檔的上下文中，shell是應用程式開發AEM人員構建的Hybrid PhoneGap應用的所有非創作內容。

內容指由開發人員構建的創作的元件、模AEM板和創AEM作頁。 內容被分類為開發人員內容或創作內容。 元件、設計和頁面模板被認為是開發內容，因為它們是由開發人員構建的。 作者內容是使用元件和模板構建的頁面。 這些通常由設計者或營銷者完成。

將創作AEM的頁面添加到混合應用需要應用開發者和開發者AEM之間協調。 在應用程式中要添加創作內容的任何位置，應用程式開發人員都需要將這些頁面組織為可在中疊AEM放的結構。 應用開發人員必須能夠向開發人AEM員提供要添加已創作內容的路徑AEM，然後在混合應用中提供佔位符頁，該佔位符頁將在開發人員已創作頁面內容AEM後被替換。

為了使解釋更容易遵循，我們將使用AEMMarketing Cloud:AEM Mobile混合參考來解釋這些概念。 混合引用應用包含帶側面菜單的微信頁面。

![chlimage_1-76](assets/chlimage_1-76.png)

在本示例中，我們將編寫應用程式的歡迎頁。 看看源頭 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75)。 我們看到應用開發者已定義了歡迎頁，並為應用呈現的頁面提供了模板。 這是應用程式開發者和開發AEM者需要協調的地方。 混合引用應用中歡迎頁模板的路徑定義為「content/mobileapps/hybrid-reference-app/en/welcome.template.html」。 此路徑非常重要，AEM因為開發人員將使用相同路徑在AEM儲存庫中建立歡迎頁。

![chlimage_1-77](assets/chlimage_1-77.png)

混合應用和創作的內容使AEM用同一路徑非常重要，因為我們依靠使用內容同步將新頁面添加到混合應用的能力來覆蓋內容。 將混合應用作為導入進AEM程的一部分導入時，將設定內容同步配置。

![chlimage_1-78](assets/chlimage_1-78.png)

當從應用儀表板「下載源」時，將運行這些ContentSync指令碼來匯編混合應用的存檔檔案。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync首先導入該應用的「shell」，該應用程式儲存了混合應用程式的所有開發內容，然後導入該應用的「內容」。 現在，如果「shell」中有與「content」中路徑相同的頁面，則「shell」下的頁面將被「content」下的頁面替換。 換句話說，如果我們在中建立的頁面與AEMContentSync運行時的「content/mobileapps/hybrid-reference-app/en/welcome.template.html」路徑相同，則在混合引用應用示例中，它將覆蓋作為混合引用應用一部分的頁面，並覆蓋該位AEM置的任何內容。 覆蓋由ContentSync負責，因此，對於使用應用的人而言，對包含已創作內容的應用的更新將看AEM起來無縫，並且不需要重建應用。 因此，運行應用時，歡迎頁面將顯示如下：

![chlimage_1-80](assets/chlimage_1-80.png)
