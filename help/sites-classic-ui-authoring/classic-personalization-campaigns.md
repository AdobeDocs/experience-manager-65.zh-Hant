---
title: 促銷活動管理
seo-title: 促銷活動管理
description: 促銷活動管理為數位行銷人員提供提供個人化內容的機會，為訪客建立專屬的體驗。 它可讓您跨網路、電子郵件和行動服務協調行銷活動，吸引訪客。
seo-description: 促銷活動管理為數位行銷人員提供提供個人化內容的機會，為訪客建立專屬的體驗。 它可讓您跨網路、電子郵件和行動服務協調行銷活動，吸引訪客。
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 促銷活動管理{#campaign-management}

促銷活動管理為數位行銷人員提供提供個人化內容的機會，為訪客建立專屬的體驗。

它可讓您跨網路、電子郵件和行動服務協調行銷活動，吸引訪客。 您可以針對特定使用者設定檔建立內容、區隔訪客、推播和促銷目標內容，並管理多個通道的促銷活動。

本檔案說明組成促銷活動的各種元素。 以下檔案提供更多詳細資訊：

* [預告與策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [電子郵件行銷](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [著陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target選件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [使用行銷活動管理員](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [瞭解區段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [設定促銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

促銷活動管理由多種元素組成：

* **品牌**&#x200B;在AEM中，品牌是頂層單位，並構成促銷活動的 **集合**。

* **促銷**&#x200B;活動促銷活動是個別體驗的 **集合**。

* **體驗**&#x200B;重點內容會形成各種體驗，呈現給訪客的觸點 **是**。 可用的體驗有幾種類型：

   * **Teaser**
      [摘要頁面／段落](#teasers) ，用來將特定訪客區 **段** ，導向關注其興趣的內容。

      摘要頁面可以：

      * 顯示一系列選項供訪客從
      * 只顯示一個以特定訪客區段為基礎的摘要段落；例如，所顯示的摘要段落可能取決於訪客的年齡。
      通常，摘要頁面是會持續特定時段的暫時動作，直到下一個摘要頁面取代為止。

   * **電子報**

      [電子郵件通訊](#emailmarketing) (E-mail Communications)用於吸引使用者，並鼓勵他們造訪您的網站。 這些通常採用電子報的形式，傳送至您的 **Lead** (通常會分組 **到Lists**)。 **** 注意：Adobe不打算進一步增強這項功能。 建議您 [運用Adobe Campaign和AEM整合](/help/sites-administering/campaign.md)。

   * **Adobe Target**

      這可讓行銷人員與Adobe Target（舊稱Test&amp;Target）整合，提供轉換網站最佳化工具，以持續提供其線上內容和服務與客戶更相關的必要功能，進而產生更高的轉換率。 Adobe target提供直覺式介面，讓您從單一應用程式設計和執行測試、建立受眾細分及鎖定內容。


* **觸點**

   這些是訪客與您促銷活動之間的聯絡點。 觸點與您建立的體驗相連。

   例如，對於廣告商，它是廣告段落所在的內容頁面，對於電子報，則是郵寄清單。

* **銷售機會**

   您收集的訪客相關資訊以及如何與他們聯絡，是您潛在客源的基礎。 **** 注意：Adobe不打算進一步增強這項功能。

   建議您 [運用Adobe Campaign和AEM整合](/help/sites-administering/campaign.md)。

* **清單**

   銷售線索通常被分組到清單中，以便您對它們採取集體行動。 **注意：注**&#x200B;意：Adobe不打算進一步增強這項功能。

   建議您 [運用Adobe Campaign和AEM整合。](/help/sites-administering/campaign.md)

* **區段**

   網站訪客在進入網站時有不同的興趣和目標。 根據網站上的活動、註冊的描述檔資訊和其他網站上的活動等因素來分析這些，可協助您定義區段。 然後，內容可根據訪客所符合的區段，特別針對訪客的需求和興趣。

* **MCM**

   行銷活動管理員(MCM)是一個主控台，可讓您存取建立及控制促銷活動、品牌、體驗、觸點、銷售機會、清單、區段和報表所需的所有功能。

   您可從各種位置(標示為 **促銷活動**)或URL存取它：

   `http://localhost:4502/libs/mcm/content/admin.html`

