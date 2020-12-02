---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM與PhoneGap整合，讓您可以使用AEM頁面輕鬆建立應用程式。 請依照本頁開始使用Adobe PhoneGap Enterprise。
seo-description: AEM與PhoneGap整合，讓您可以使用AEM頁面輕鬆建立應用程式。 請依照本頁開始使用Adobe PhoneGap Enterprise。
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

AEM與PhoneGap整合，讓您可以使用AEM頁面輕鬆建立應用程式。 PhoneGap可讓使用者建立公用程式應用程式，讓使用者使用內容。 內容同步可讓您建立版本控制的頁面封存，以便與應用程式搭售。

通常，***AEM Administrator***&#x200B;負責將新應用程式新增至AEM Mobile目錄，方法是使用建立精靈建立新應用程式，或匯入現有的應用程式。

從這裡，***AEM Author***（或&#x200B;*Marketer*）現在可以使用現成可用的範本和元件來新增和編輯頁面、拖放元件以及新增DAM中所有類型的媒體，包括影像、視訊和文字片段（內容片段）。

AEM Mobile的真正功能是&#x200B;*savv* ***AEM Developer***&#x200B;可擴充並建立自訂的網頁範本和元件，讓&#x200B;*AEM Author*&#x200B;建立精美而引人入勝的行動體驗。 這些範本和元件不僅針對行動應用程式世界最佳化；但是，您可以與裝置和AEM伺服器（任何遠端伺服器）通訊，以全通道服務端點。

>[!NOTE]
>
>當&#x200B;*AEM Author*&#x200B;認為應用程式已準備就緒時，他們可以先讓利益相關者下載具有&#x200B;**[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)**&#x200B;的應用程式（可在AppStore和PlayStore中取得）以進行審核和核准。 在他們收到綠燈後，就可以透過AEM Mobile ContentSync內容發行管理儀表板，直接將此新內容或更新內容發佈給其使用者。 一個人可以承擔任何角色，這取決於您和您的治理政策。

## 必備條件 {#prerequisites}

AEM Mobile只是構成完整AEM平台的一個支柱。

在使用AEM Mobile之前，並依照本快速入門手冊中的步驟進行，使用者應先熟悉AEM和AEM Mobile控制中心。 請參閱：

[AEM快速入門](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心的逐步說明](/help/mobile/phonegap-authoring-apps.md)

## 作者的QuickLinks {#quicklinks-for-authors}

請參閱AEM[中的「編寫Adobe PhoneGap企業版」，以瞭解作者的角色和責任。](/help/mobile/phonegap.md)

## 開發人員的QuickLinks {#quicklinks-for-developers}

有些範例應用程式會與AEM Mobile整合，而且可由開發人員自訂。 按一下「使用AEM開發Adobe PhoneGap Enterprise」（[使用AEM](/help/mobile/developing-in-phonegap.md)）。

在後續章節中，您將瞭解進階概念，例如白色標示您的應用程式、本地化、國際化、ContentSync、定位、分析等。

## {#quicklinks-for-administrators}管理員的QuickLinks

請參閱[使用AEM](/help/mobile/administer-phonegap.md)管理Adobe PhoneGap Enterprise的內容，以設定和管理您的行動應用程式。

>[!NOTE]
>
>使用混合行動技術，您可以建立多樣化行動應用程式，讓&#x200B;*離線執行，而且實際上使用AEM Mobile的*&#x200B;可讓許多客戶選擇建立應用程式，以檢查他們線上上或離線時的表現，並據以執行。
