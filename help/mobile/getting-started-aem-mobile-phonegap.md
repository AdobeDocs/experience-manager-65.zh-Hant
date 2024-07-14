---
title: AEM Adobe PhoneGap
description: AEM已與PhoneGap整合，因此您可以使用AEM頁面輕鬆建立應用程式。 請依照本頁面的說明開始使用Adobe PhoneGap Enterprise。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM已與PhoneGap整合，因此您可以使用AEM頁面輕鬆建立應用程式。 PhoneGap可讓使用者建立公用程式應用程式，讓使用者處理內容。 「內容同步」可讓您建立頁面的版本化封存，以便與應用程式整合。

通常，***AEM管理員***&#x200B;會使用建立精靈建立應用程式，或匯入現有應用程式，負責將新應用程式新增至AEM Mobile目錄。

從這裡，***AEM作者*** （或&#x200B;*行銷人員*）現在可以使用現成的範本和元件來新增和編輯頁面、拖放元件，以及從DAM新增所有型別的媒體，包括影像、影片和文字片段（內容片段）。

AEM Mobile的真正力量是&#x200B;*精明的* ***AEM Developer***&#x200B;可以擴充及建立自訂Web範本和元件，讓&#x200B;*AEM Author*&#x200B;能夠建立美妙且吸引人的行動體驗。 這些範本和元件不僅已針對行動應用程式世界最佳化，而且可與裝置和AEM伺服器（任何遠端伺服器）通訊，以連線全通路服務端點。

>[!NOTE]
>
>當&#x200B;*AEM作者*&#x200B;認為應用程式已就緒時，他們可以先讓利害關係人下載具有&#x200B;**[Adobe驗證](/help/mobile/phonegap-mobile-quickstart.md)** （可在AppStore和PlayStore中使用）的應用程式以進行檢閱和核准。 收到綠燈後，他們就能透過AEM Mobile ContentSync內容發行管理控制面板，直接發行這項新內容或更新內容給使用者。 可由一個人擔任任意數量的角色，具體取決於您和您的治理政策。

## 先決條件 {#prerequisites}

AEM Mobile只是構成完整AEM平台的支柱之一。

在使用AEM Mobile並按照本快速入門手冊中的步驟操作之前，使用者應該熟悉AEM和AEM Mobile控制中心。 請參閱：

[AEM快速入門](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心逐步解說](/help/mobile/phonegap-authoring-apps.md)

## 作者的快速連結 {#quicklinks-for-authors}

請參閱[在AEM](/help/mobile/phonegap.md)中為Adobe PhoneGap Enterprise製作，瞭解作者的角色和責任。

## 開發人員快速連結 {#quicklinks-for-developers}

有些範例應用程式會與AEM Mobile整合，並可由開發人員自訂。 按一下[使用AEM](/help/mobile/developing-in-phonegap.md)開發Adobe PhoneGap Enterprise。

在後續章節中，您將瞭解如白色標籤、您的應用程式、本地化、國際化、ContentSync、目標定位、分析等進階概念。

## 管理員快速連結 {#quicklinks-for-administrators}

請參閱[使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)，以設定和管理您的行動應用程式。

>[!NOTE]
>
>使用混合式行動技術，您可以建立使用AEM Mobile *離線和線上執行*&#x200B;的豐富行動應用程式，事實上，許多客戶選擇建立應用程式，以檢查他們線上上或離線時的狀態，並據此採取相應的行動。
