---
title: AEMAdobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: 與AEMPhoneGap整合，以便您可以使用頁面輕鬆建立AEM應用。 按此頁開始使用Adobe PhoneGap企業。
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# AEMAdobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

與AEMPhoneGap整合，以便您可以使用頁面輕鬆建立AEM應用。 PhoneGap允許用戶建立實用程式應用，讓用戶能夠處理內容。 「內容同步」使您能夠建立頁面版本控制存檔，以便與應用捆綁。

通常， ***管AEM理員*** 負責將新應用程式添加到AEM Mobile目錄，方法是使用建立嚮導建立新應用程式，或導入現有應用程式。

從這裡 ***AEM作者*** 或 *營銷商*)現在能夠使用現成模板和元件來添加和編輯頁面、拖放元件以及添加DAM中所有類型的媒體，包括影像、視頻和文本片段（內容片段）。

AEM Mobile的真正力量是 *精明* ***開發AEM人員*** 可以擴展和建立自定義Web模板和元件，以啟用 *AEM作者* 創造美妙而迷人的移動體驗。 這些模板和元件不僅針對移動應用世界進行了優化；但要與設備和伺服器AEM（任何遠程伺服器）通信到全通道服務端點。

>[!NOTE]
>
>當 *AEM作者* 相信應用已準備就緒，他們可以首先讓相關人員下載該應用 **[Adobe驗證](/help/mobile/phonegap-mobile-quickstart.md)** （可在AppStore和PlayStore中使用）以供審核和批准。 一旦他們收到綠燈，他們就可以通過AEM MobileContentSync內容發佈管理控制板直接向用戶發佈此新或更新的內容。 一個人可以承擔任何數量的角色，這取決於你和你的治理政策。

## 必備條件 {#prerequisites}

AEM Mobile只是構成整個平台的一個支AEM柱。

在與AEM Mobile合作並遵循本入門指南中的步驟之前，用戶應熟悉AEMAEM Mobile控制中心。 請參閱：

[AEM 快速入門](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心漫步](/help/mobile/phonegap-authoring-apps.md)

## 作者快速連結 {#quicklinks-for-authors}

請參閱 [為Adobe PhoneGap企業創AEM作](/help/mobile/phonegap.md) 瞭解作者的角色和責任。

## 面向開發人員的QuickLinks {#quicklinks-for-developers}

有些示例應用程式將與AEM Mobile整合，可由開發人員定制。 按一下 [用&quot;Adobe PhoneGap&quot;發展AEM企業](/help/mobile/developing-in-phonegap.md)。

在後續章節中，您將瞭解高級概念，如白色標籤您的應用程式、本地化、國際化、內容同步、目標、分析等。

## 管理員快速連結 {#quicklinks-for-administrators}

請參閱 [為Adobe PhoneGap企業管理內AEM容](/help/mobile/administer-phonegap.md) 設定和管理移動應用程式。

>[!NOTE]
>
>使用混合移動技術，您可以建立豐富的移動應用程式 *離線運行和聯機運行* 事實上，AEM Mobile的許多客戶選擇建立一些應用，以線上或離線時查看，並據此行事。
