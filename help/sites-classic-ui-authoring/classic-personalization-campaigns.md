---
title: Campaign Management
seo-title: Campaign Management
description: 營銷活動管理為數字營銷商提供了提供個性化內容的機會，從而為訪問者建立專用體驗。 它使您能夠通過Web、電子郵件和移動服務協調您的營銷活動，從而吸引您的訪問者。
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# Campaign Management{#campaign-management}

營銷活動管理為數字營銷商提供了提供個性化內容的機會，從而為訪問者建立專用體驗。

它使您能夠通過Web、電子郵件和移動服務協調您的營銷活動，從而吸引您的訪問者。 您可以建立內容、段訪問者、推送和升級特定用戶配置檔案的目標內容以及跨多個渠道管理市場活動。

本文檔描述了構成市場活動的各種要素。 以下文檔提供了更多詳細資訊：

* [預告和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [電子郵件營銷](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [目標產品](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [使用市場營銷活動經理](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [了解分段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [設定您的活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

市場活動管理由多種要素組成：

* **品牌**
在AEM中，品牌是頂級單元，並形成 
**行銷活動**.

* **市場活動**
市場活動是個人的集合 
**體驗**.

* **體驗**
這些重點內容形成了各種經驗，並呈現在 
**接觸點**. 有幾種可用體驗：

   * **Teaser**
      [預告頁/段落](#teasers) 用於引導特定訪問者 **段** 關注他們興趣的內容。

      預告頁可以：

      * 為訪問者提供一系列可供選擇的選項
      * 只顯示一個基於特定訪客段的預告段；例如，所顯示的預告段落可能取決於訪問者的年齡。

      通常，預告頁是臨時操作，將持續一段特定時間，直到被下一個預告頁替換為止。

   * **通訊**

      [電子郵件通信](#emailmarketing) 用於吸引用戶並鼓勵他們訪問您的網站。 這些通常以新聞稿的形式發送給您 **銷售線索** (通常分為 **清單**)。 **注：** Adobe並沒有計畫進一步增強這一能力。 建議是 [利用Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

   * **Adobe Target**

      這允許與Adobe Target(以前是Test&amp;目標公司)整合，這為營銷人員提供了轉換網站優化工具，使他們能夠持續製作其線上內容並提供與客戶更相關的服務，從而實現更大的轉換。 Adobe Target為設計和執行test、建立受眾段和瞄準內容提供了直觀的介面 — 所有這一切都來自單個應用程式。


* **接觸點**

   這些是訪問者與您的活動之間的聯繫點。 觸點與您建立的體驗相連。

   例如，對於預告，它是預告段落所在的內容頁面，對於新聞稿，它是郵寄清單。

* **銷售機會**

   您收集的有關訪問者的資訊以及如何聯繫他們是您銷售線索的基礎。 **注：** Adobe並沒有計畫進一步增強這一能力。

   建議是 [利用Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

* **清單**

   銷售線索通常被分組到清單中，以便您可以對它們採取集體行動。 注： **注：** Adobe並沒有計畫進一步增強這一能力。

   建議是 [利用Adobe Campaign和整合AEM。](/help/sites-administering/campaign.md)

* **區段**

   站點訪問者在訪問站點時有不同的興趣和目標。 根據網站上的活動、註冊的配置檔案資訊和其他網站上的活動等因素分析此資訊，有助於您定義網段。 然後，內容可以根據訪問者的需要和興趣根據他們匹配的段來特別針對訪問者的需求和興趣。

* **MCM**

   市場營銷活動經理(MCM)是一個控制台，它允許您訪問建立和控制您的市場活動、品牌、經驗、聯繫點、銷售線索、清單、段和報表所需的所有功能。

   可以從不同位置訪問(標為 **市場活動**)，或使用，例如URL:

   `http://localhost:4502/libs/mcm/content/admin.html`
