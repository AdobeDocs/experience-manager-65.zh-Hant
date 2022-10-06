---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM與PhoneGap整合，讓您能使用AEM頁面輕鬆建立應用程式。 請依照本頁面操作，開始使用Adobe PhoneGap Enterprise。
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

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM與PhoneGap整合，讓您能使用AEM頁面輕鬆建立應用程式。 PhoneGap可讓使用者建立公用程式應用程式，讓使用者使用內容。 「內容同步」可讓您建立頁面的版本控制封存檔，以便與應用程式捆綁。

通常， ***AEM管理員*** 負責使用建立精靈建立新應用程式，或匯入現有應用程式，將新應用程式新增至AEM Mobile目錄。

從這裡 ***AEM作者*** (或 *行銷人員*)現在可以使用現成可用的範本和元件，來新增和編輯頁面、拖放元件以及新增DAM中所有類型的媒體，包括影像、影片和文字片段（內容片段）。

AEM Mobile的真正力量是 *悟性* ***AEM開發人員*** 可擴充及建立自訂網頁範本和元件，以啟用 *AEM作者* 來建立美妙且吸引人的行動體驗。 這些範本和元件不僅針對行動應用程式領域而最佳化；但會同時與裝置和AEM伺服器（任何遠端伺服器）通訊至全通道服務端點。

>[!NOTE]
>
>當 *AEM作者* 相信應用程式已就緒，他們可以先讓相關人員透過下載應用程式 **[Adobe驗證](/help/mobile/phonegap-mobile-quickstart.md)** （可在AppStore和PlayStore中取得），以供審核和核准。 他們收到綠燈後，就能透過AEM Mobile ContentSync內容發行管理控制面板，直接將這個新或更新的內容發行給使用者。 一個人可以承擔任何角色，這取決於您和您的治理政策。

## 必備條件 {#prerequisites}

AEM Mobile只是構成完整AEM平台的一個支柱。

使用AEM Mobile並依照本快速入門手冊中的步驟操作之前，使用者應先熟悉AEM和AEM Mobile控制中心。 請參閱：

[AEM 快速入門](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心漫談](/help/mobile/phonegap-authoring-apps.md)

## 供作者使用的快速連結 {#quicklinks-for-authors}

請參閱 [在AEM中為Adobe PhoneGap Enterprise編寫](/help/mobile/phonegap.md) 了解作者的角色和責任。

## 面向開發人員的快速連結 {#quicklinks-for-developers}

有些範例應用程式將與AEM Mobile整合，可由開發人員自訂。 按一下 [使用AEM開發Adobe PhoneGap企業](/help/mobile/developing-in-phonegap.md).

在後續章節中，您將了解進階概念，例如白色標籤應用程式、本地化、國際化、內容同步、鎖定目標、分析等。

## 管理員快速連結 {#quicklinks-for-administrators}

請參閱 [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md) 來設定和管理您的行動應用程式。

>[!NOTE]
>
>使用混合移動技術，您可以建立豐富的移動應用程式， *離線運行和聯機運行* 事實上，有了AEM Mobile，許多客戶都選擇建立應用程式來檢查其上線或離線時間，並採取相應的行為。
