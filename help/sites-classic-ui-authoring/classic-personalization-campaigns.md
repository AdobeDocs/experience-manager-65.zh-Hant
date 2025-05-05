---
title: Campaign Management
description: 行銷活動管理為數位行銷人員提供機會，以提供個人化內容，並為訪客建立專屬體驗。 它可讓您在網路、電子郵件和行動服務之間協調行銷活動，吸引訪客參與。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Campaign Management{#campaign-management}

行銷活動管理為數位行銷人員提供機會，以提供個人化內容，並為訪客建立專屬體驗。

它可讓您在網路、電子郵件和行動服務之間協調行銷活動，吸引訪客參與。 您可以針對特定使用者設定檔建立內容、區段訪客、推播和促銷目標內容，以及管理多個管道中的行銷活動。

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
在Adobe Experience Manager (AEM)中，品牌是頂層單位，並構成&#x200B;**行銷活動**&#x200B;的集合。

* **行銷活動**
行銷活動是個別&#x200B;**體驗**&#x200B;的集合。

* **體驗**
焦點內容會形成各種體驗，在&#x200B;**接觸點**&#x200B;呈現給訪客。 有數種體驗可供使用：

   * **預告**

     [Teaser頁面/段落](#teasers)用於引導特定訪客&#x200B;**區段**&#x200B;前往關注其興趣的內容。

     Teaser頁面可以：

      * 提供訪客可從中進行選擇的一系列選項
      * 僅顯示一個以特定訪客區段為基礎的Teaser段落。 例如，顯示的Teaser段落可能會視訪客的年齡而定。

     通常，Teaser頁面是持續特定時段的暫時動作，直到它被下一個Teaser頁面取代。

   * **電子報**

     [電子郵件通訊](#emailmarketing)用於與使用者互動，並鼓勵他們造訪您的網站。 這些通常採用電子報的形式，傳送給您的&#x200B;**銷售機會** （這些銷售機會已分組為&#x200B;**清單**）。 **注意：** Adobe不打算進一步增強此功能。 建議您[使用Adobe Campaign並整合至AEM](/help/sites-administering/campaign.md)。

   * **Adobe Target**

     如此可與Adobe Target （先前的Test&amp;Target）整合，讓行銷人員擁有轉換網站最佳化工具，以及必要的功能，以便持續提供與其客戶更相關的線上內容和選件，進而提供更理想的轉換。 Adobe Target提供直覺式介面，讓您從單一應用程式設計和執行測試、建立受眾區段及鎖定目標內容。

* **接觸點**

  這些是訪客與促銷活動之間的聯絡點。 接觸點會連線至您建立的體驗。

  例如，對於Teaser，這是Teaser段落所在的內容頁面；對於電子報而言，這是郵寄清單。

* **個銷售機會**

  您收集到的訪客相關資訊以及如何聯絡這些資訊構成了潛在客戶的基礎。 **注意：** Adobe不打算進一步增強此功能。

  建議您[使用Adobe Campaign並整合至AEM](/help/sites-administering/campaign.md)。

* **清單**

  潛在客戶會分組到清單中，以便您對其採取集體行動。 注意： **注意：** Adobe不打算進一步增強此功能。

  建議您[使用Adobe Campaign並整合至AEM。](/help/sites-administering/campaign.md)

* **區段**

  網站訪客造訪網站時，有不同的興趣和目標。 根據網站上活動、註冊的設定檔資訊和其他網站上的活動等因素進行此分析，可協助您定義區段。 接著，您就可以根據訪客相符的區段，將內容鎖定在訪客的需求和興趣上。

* **MCM**

  行銷活動管理員(MCM)是一個主控台，可讓您存取建立和控制行銷活動、品牌、體驗、接觸點、銷售機會、清單、區段和報表所需的所有功能。

  可從各種位置（標示為&#x200B;**行銷活動**）存取，或是使用URL存取：

  `http://localhost:4502/libs/mcm/content/admin.html`
