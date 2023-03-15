---
title: Campaign Management
seo-title: Campaign Management
description: 行銷活動管理為數位行銷人員提供提供個人化內容的機會，為訪客建立專屬的體驗。 它可讓您在網路、電子郵件和行動服務上協調行銷活動，以吸引訪客。
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

行銷活動管理為數位行銷人員提供提供個人化內容的機會，為訪客建立專屬的體驗。

它可讓您在網路、電子郵件和行動服務上協調行銷活動，以吸引訪客。 您可以為特定使用者設定檔建立內容、劃分訪客、推播和促銷目標式內容，以及管理多個管道中的促銷活動。

本檔案說明組成促銷活動的各種元素。 以下檔案提供更多詳細資訊：

* [茶匙和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [電子郵件行銷](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [目標選件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [與行銷活動經理合作](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [了解分段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [設定您的行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

行銷活動管理由各種元素組成：

* **品牌**
在AEM中，品牌是頂層單位，並形成 
**促銷活動**.

* **行銷活動**
促銷活動是個人的集合 
**體驗**.

* **體驗**
重點內容會形成各種體驗，呈現給訪客的位置為 
**接觸點**. 可用的體驗類型有數種：

   * **Teaser**
      [預告頁面/段落](#teasers) 用來指引特定訪客 **區段** 關注他們興趣的內容。

      預告頁面可以：

      * 提供一系列選項供訪客選擇
      * 只顯示一個以特定訪客區段為基礎的預告段落；例如，顯示的預告段落可能取決於訪客的年齡。

      預告頁面通常是會持續特定一段時間的臨時動作，直到被下一個預告頁面取代為止。

   * **電子報**

      [電子郵件通訊](#emailmarketing) 可用來吸引使用者，並鼓勵他們造訪您的網站。 這些通常會以電子報的形式傳送至 **銷售機會** (通常分為 **清單**)。 **注意：** Adobe不打算進一步增強這一能力。 建議為 [運用Adobe Campaign及與AEM的整合](/help/sites-administering/campaign.md).

   * **Adobe Target**

      這可讓行銷人員與Adobe Target（先前的Test&amp;Target）整合，進而獲得轉換網站最佳化工具，並具備必要的功能，以持續讓其線上內容和選件與客戶更相關，進而產生更大的轉換。 Adobe Target提供直覺式介面，可讓您從單一應用程式設計及執行測試、建立對象區段及鎖定目標內容。


* **接觸點**

   這些是訪客和您的促銷活動之間的聯絡點。 接觸點會連結至您建立的體驗。

   例如，對於預告，它是預告段落所在的內容頁面，對於新聞稿，它是郵件清單。

* **銷售機會**

   您收集的訪客相關資訊以及如何與他們聯絡，是您銷售機會的基礎。 **注意：** Adobe不打算進一步增強這一能力。

   建議為 [運用Adobe Campaign及與AEM的整合](/help/sites-administering/campaign.md).

* **清單**

   銷售機會通常被分組到清單中，這樣您就可以對它們採取集體行動。 注意： **注意：** Adobe不打算進一步增強這一能力。

   建議為 [運用Adobe Campaign及與AEM的整合。](/help/sites-administering/campaign.md)

* **區段**

   網站訪客來到網站時，其興趣和目標不同。 根據網站上的活動、已註冊的設定檔資訊和其他網站上的活動等因素分析，可協助您定義區段。 接著，內容便可根據訪客所符合的區段，針對訪客的需求和興趣進行明確定位。

* **MCM**

   行銷活動管理員(MCM)是一個主控台，可讓您存取建立及控制行銷活動、品牌、體驗、接觸點、銷售機會、清單、區段和報表所需的所有功能。

   您可從各種位置存取(標示為 **行銷活動**)，或搭配URL:

   `http://localhost:4502/libs/mcm/content/admin.html`
