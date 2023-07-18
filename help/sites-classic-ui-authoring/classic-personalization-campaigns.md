---
title: Campaign Management
description: Campaign管理為數位行銷人員提供機會，以提供個人化內容，並為訪客建立專屬體驗。 它可讓您在網路、電子郵件和行動服務之間協調行銷活動，從而吸引訪客。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: ae08247c7be0824151637d744f17665c3bd82f2d
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Campaign Management{#campaign-management}

Campaign管理為數位行銷人員提供機會，以提供個人化內容，並為訪客建立專屬體驗。

它可讓您在網路、電子郵件和行動服務之間協調行銷活動，從而吸引訪客。 您可以為特定使用者設定檔建立內容、區段訪客、推送和促銷目標式內容，以及管理多個管道中的行銷活動。

本檔案說明構成行銷活動的各種元素。 下列檔案提供更詳細的資訊：

* [Teaser和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [電子郵件行銷](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target優惠](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [使用行銷活動管理員](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [了解分段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [設定您的行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

行銷活動管理由各種元素組成：

* **品牌**
在Adobe Experience Manager (AEM)中，品牌是頂層單位，並形成集合 **行銷活動**.

* **行銷活動**
行銷活動是個人的集合 **體驗**.

* **體驗**
重點內容會形成各種體驗，並在呈現給訪客的 **接觸點**. 有多種體驗型別可供使用：

   * **Teaser**
     [Teaser頁面/段落](#teasers) 用於引導特定訪客 **區段** 專注於客戶興趣的內容。

     Teaser頁面可以：

      * 提供訪客可選擇的一系列選項
      * 僅顯示一個以特定訪客區段為基礎的Teaser段落。 例如，顯示的Teaser段落可能視訪客的年齡而定。

     通常，Teaser頁面是持續特定時段的暫時動作，直到被下一個Teaser頁面取代。

   * **電子報**

     [電子郵件通訊](#emailmarketing) 用於吸引使用者並鼓勵他們造訪您的網站。 這些通常採用電子報的形式，傳送給您的 **銷售機會** (這些類別會分組到 **清單**)。 **注意：** Adobe不打算進一步增強此功能。 建議為 [使用Adobe Campaign與AEM整合](/help/sites-administering/campaign.md).

   * **Adobe Target**

     這允許與Adobe Target （先前稱為Test&amp;Target）整合，後者為行銷人員提供轉換網站最佳化工具，以及持續提供其線上內容和優惠方案的必要功能，以便與其客戶更相關，進而提供更高的轉換。 Adobe Target提供直覺式介面，讓您從單一應用程式設計和執行測試、建立受眾區段及鎖定目標內容。

* **接觸點**

  這些是訪客與促銷活動之間的聯絡點。 接觸點會連結至您建立的體驗。

  例如，對於Teaser，這是Teaser段落所在的內容頁面；對於Newsletter，則是郵寄清單。

* **銷售機會**

  您收集到的訪客相關資訊以及如何聯絡這些資訊會形成潛在客戶的基礎。 **注意：** Adobe不打算進一步增強此功能。

  建議為 [使用Adobe Campaign與AEM整合](/help/sites-administering/campaign.md).

* **清單**

  潛在客戶會分組到清單中，以便您對其採取集體行動。 注意： **注意：** Adobe不打算進一步增強此功能。

  建議為 [使用Adobe Campaign以及與AEM的整合。](/help/sites-administering/campaign.md)

* **區段**

  網站訪客造訪網站時，有不同的興趣和目標。 根據網站上活動、註冊的設定檔資訊和其他網站上的活動等因素來分析此專案，有助於您定義區段。 接著，您就可以根據訪客相符的區段，將內容鎖定在訪客的需求和興趣上。

* **MCM**

  行銷活動管理員(MCM)是一個主控台，可讓您存取建立和控制行銷活動、品牌、體驗、接觸點、銷售機會、清單、區段和報表所需的所有功能。

  可從不同位置存取(標示為 **行銷活動**)，或以URL為例：

  `http://localhost:4502/libs/mcm/content/admin.html`
