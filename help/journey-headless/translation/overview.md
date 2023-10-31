---
title: AEM Headless 翻譯歷程
description: 從這裡開始，此歷程會逐步引導您了解如何使用 AEM 強大的翻譯工具來翻譯您的 Headless 內容。
exl-id: 1a9d4c88-b676-4168-a9ef-7d218b39129f
source-git-commit: f627bc2b58578df1b4ff6c95d87f0c64daafa1c7
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 96%

---

# AEM Headless 翻譯歷程 {#aem-headless-translation-journey}

從這裡開始，此歷程會逐步引導您了解如何使用 AEM 強大的翻譯工具來翻譯您的 Headless 內容。

## 簡介 {#introduction}

Headless 實作對於將體驗傳遞給您的對象而言越來越重要，無論您的對象身在何處，無論管道、區域或地區設定為何。

Headless 實作放棄了全堆疊解決方案中的傳統頁面和元件管理，專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。透過使用 AEM 強大的翻譯工具，這些可重複使用的片段可以輕鬆翻譯並傳遞給您的對象，無論他們身在何處。

本指南將引導您了解最重要的 Headless 翻譯主題，完成後您將會：

* 大致了解什麼是 Headless 內容傳遞。
* 對 AEM Headless 功能有基本的了解。
* 了解 AEM 的翻譯功能及其與 Headless 內容的關係。
* 能夠開始翻譯您自己的 Headless 內容。

目標是讓您對 Headless 技術、AEM 如何提供 Headless 內容以及如何翻譯它，有廣泛的了解。如果這些主題有任何一個您不熟悉，那麼這就是您理想的起點。

如果您已經熟悉 AEM、 Headless 和翻譯，那麼您可能已經掌握了此歷程的基本知識。請考慮參閱下方[其他資源章節](#additional-resources)下的已連結技術文件。

## AEM 文件歷程 {#documentation-journeys}

[文件歷程](/help/journey-documentation/home.md)提供敘述來協助剛開始使用 AEM 的讀者，讓他們能從頭到尾理解和解決業務問題，同時將採用的先前主題或 AEM 知識降至最低，藉以連結許多不同且複雜的主題和功能。

文件歷程根據最佳做法原則而設計，其中包含 Adobe 的最新研究、Adobe 顧問的成熟實作經驗以及客戶專案的意見回饋。

如果您想了解 Adobe 如何建議如何使用 AEM 解決 Headless 商務案例，[AEM Headless 歷程](/help/journey-headless/home.md)是理想起點。

## 對象 {#audience}

此歷程專為翻譯專家角色 (通常稱為翻譯專案經理或 TPM) 所設計。此歷程闡述在 AEM 中翻譯 Headless 內容的要求、步驟和方法。此歷程定義了翻譯專家必須與之互動的其他角色，但此歷程是以翻譯專家的角度出發。

歷程假設讀者具有在大型 CMS 系統上翻譯內容的經驗，但假設他們不了解 Headless 技術或 AEM。

以下是在此歷程中會互動的角色。

| 角色 | 說明 | 歷程中的角色 |
|---|---|---|
| 翻譯專家 | 定義應翻譯的內容並管理這些工作流程 | 此歷程的對象 |
| 內容作者 | 建立並管理 Headless 傳遞的內容 | 內容作者建立翻譯專家必須翻譯的內容。 |
| 管理員 | 管理 AEM 的基本設定和配置 | 翻譯專家與管理員一起進行翻譯作業所需的設定變更，例如安裝翻譯連接器。 |
| 內容架構師 | 分析必須以 Headless 方式傳遞之資料的要求並定義該資料的結構 | 翻譯專家與內容架構師一起定義內容的組織，以便輕鬆翻譯。 |

此歷程的資訊當然對所有角色都有用，但有些資訊對於某些角色可能是多餘的。請密切注意[即將到來、涵蓋其他角色的歷程。](/help/journey-documentation/home.md#journeys)

## Headless 翻譯歷程 {#the-journey}

您將在此歷程中探索許多主題。以下文章為您提供了在 AEM 中翻譯 Headless 內容的基本知識，以及詳細技術文件的連結。

儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。因此，如果您剛接觸 AEM Headless 翻譯，Adobe 建議您從頭開始，然後循序漸進。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM Headless 翻譯歷程 | 本文件 |
| 1 | [了解 Headless 內容以及如何在 AEM 中翻譯](learn-about.md) | 了解 Headless 概念、它們如何對應到 AEM 以及 AEM 翻譯理論。 |
| 2 | [AEM Headless 翻譯快速入門](getting-started.md) | 了解如何組織 Headless 內容以及 AEM 翻譯工具的運作原理。 |
| 3 | [設定翻譯整合](configure-connector.md) | 了解如何將 AEM 連接到翻譯服務。 |
| 4 | [設定翻譯規則](translation-rules.md) | 了解如何定義翻譯規則以識別要翻譯的內容。 |
| 5 | [翻譯內容](translate-content.md) | 使用翻譯整合和規則來翻譯Headless內容。 |
| 6 | [發佈翻譯內容](publish-content.md) | 了解如何發佈翻譯後的內容，並在基礎內容更新時更新翻譯。 |

## 下一步 {#what-is-next}

您現在已準備好開始您的 Adobe Headless 翻譯歷程。我們鼓勵您繼續歷程的下一部分並閱讀文章[了解 Headless 內容以及如何在 AEM 中進行翻譯](learn-about.md)

## 其他資源 {#additional-resources}

文件歷程會透過敘述方式，指導您完成複雜的相關流程和功能，向您展示 AEM 如何解決業務問題。此歷程說明了多個功能如何共同運作以解決單一業務需求。

因為這樣的歷程是設計成獨立的。然而，其中一些可以相互關聯。查看這些額外的歷程，進一步了解 AEM 的強大功能如何協同工作。

* [Headless 編寫歷程](/help/journey-headless/author/overview.md) - 從這裡開始，此歷程會逐步引導您了解 AEM 強大且靈活的 Headless 特性、其功能，以及如何在您的第一個 Headless 專案中建立內容模型。
* [Headless架構者歷程](/help/journey-headless/architect/overview.md)  — 從這裡開始瞭解Adobe Experience Manager強大且有彈性的無周邊功能，以及如何為您的專案建立內容的模型。
* [AEM Headless 開發人員歷程](/help/journey-headless/developer/overview.md) - 從這裡開始，此歷程會逐步引導您了解 AEM 強大且靈活的無周邊特性、其功能，以及如何在您的第一個開發專案中運用這些功能。
* [AEM 技術文件](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant) - 如果您已經對 AEM 和 Headless 技術有深入的了解，您可能想要直接查閱我們深入的技術文件。
   * [AEM as a Headless CMS 簡介](/help/sites-developing/headless/introduction.md)
* [AEM Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 如果您偏好做中學並為傾向技術，請加入我們的由 API 和框架組織的實作教學課程，其在探究如何建立和使用 AEM Headless 應用程式。
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
