---
title: AEM Headless 開發人員歷程
description: AEM Headless CMS 文件。從這裡開始，逐步引導您瞭解AEM強大且有彈性的無周邊功能、其功能，以及如何在您的第一個開發專案中使用這些功能。
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: 487136be68e04fd74affe43790587b37d4c3d3ef
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 74%

---

# AEM Headless 開發人員歷程 {#aem-headless-developer-journey}

從這裡開始，逐步引導您瞭解AEM強大且有彈性的無周邊功能、其功能，以及如何在您的第一個Headless開發專案中使用這些功能。 此歷程提供您開發第一個Headless應用程式所需的所有AEM Headless檔案。

## 簡介 {#introduction}

Headless 實作放棄了全堆疊解決方案中的傳統頁面和元件管理，專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。它是實作數位體驗的現代動態開發模式。

本指南將引導您瞭解AEM中最常使用的Headless實作主題，以便在完成後：

* 充分了解什麼是 Headless 內容傳遞及其優勢。
* 了解 AEM 的 Headless 功能以及它們如何協同工作以傳遞 Headless 體驗。
* 能夠邁出實作您第一個 AEM Headless 專案的第一步。

## AEM 文件歷程 {#documentation-journeys}

[文件歷程](/help/journey-documentation/home.md)提供敘述來協助剛開始使用 AEM 的讀者，讓他們能從頭到尾理解和解決業務問題，同時將採用的先前主題或 AEM 知識降至最低，藉以連結許多不同且複雜的主題和功能。

文件歷程根據最佳做法原則而設計，其中包含 Adobe 的最新研究、Adobe 顧問的成熟實作經驗以及客戶專案的意見回饋。

如果您想了解 Adobe 如何建議如何使用 AEM 解決 Headless 商務案例，[AEM Headless 歷程](/help/journey-headless/overview.md)是理想起點。

>[!TIP]
>
>如果您偏好使用 **透過執行來學習** 如有技術傾向，請造訪AEM Headless教學課程，這些教學課程會依API和框架組織，並可在以下網址取得： [其他資源區段](#additional-resources) （位於本檔案結尾）。

## 對象 {#audience}

此歷程專為開發人員所設計，從開發人員的角度闡述了 AEM Headless 專案的要求、步驟和方法。此歷程定義了為使專案成功開發人員必須與之互動的其他角色，但歷程是以開發人員的角度出發。

以下是在此歷程中會互動的角色。

| 角色 | 說明 | 此歷程中的角色 |
|---|---|---|
| 開發人員 (目標對象) | 有經驗曾開發取用不同來源之內容的 Headless 應用程式 | 此歷程的目標對象 |
| 內容作者 | 建立和管理以 Headless 方式傳遞的內容 | 內容作者建立開發人員以 Headless 方式傳遞的內容。 |
| 管理員 | 管理 AEM 的基本設定和配置 | 開發人員與管理員合作以進行開發所需的設定變更。 |
| 內容架構師 | 分析必須以 Headless 方式傳遞之資料的要求並定義該資料的結構 | 開發人員與內容架構師合作，了解資料結構和 Headless 傳遞資料的要求。 |

此歷程的資訊可能對所有角色都有用，但有些資訊對於某些角色可能是多餘的。請密切注意[即將到來、涵蓋其他角色的歷程。](/help/journey-documentation/home.md#journeys)

## Headless 開發人員歷程 {#the-journey}

您將在此歷程中探索許多主題。以下文章為您提供 AEM Headless 的基本知識，以及詳細外部技術文件的連結。

儘管您可以直接進入歷程的特定部分，但許多概念都是以先前文章中的概念為基礎。因此，如果您是 AEM Headless 新手，Adobe 建議您從頭開始，然後循序漸進。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM Headless 開發人員歷程 | 本文件 |
| 1 | [了解 CMS Headless 開發](learn-about.md) | 了解 Headless 技術以及使用時機。 |
| 2 | [AEM Headless快速入門](getting-started.md) | 了解 AEM Headless 先決條件 |
| 3 | [踏上首次使用 AEM Headless 之路](path-to-first-experience.md) | 設定您的開發環境並了解如何將簡單的應用程式與 AEM Headless 相整合 |
| 4 | [如何建立為您的內容建立模型](model-your-content.md) | 瞭解如何建立內容結構的模型。 然後使用內容片段模型和內容片段實現 Adobe Experience Manager (AEM) 的結構，以便跨管道重複使用。 |
| 5 | [如何透過 AEM Delivery API 存取您的內容](access-your-content.md) | 了解如何使用 GraphQL 查詢來存取您的內容片段內容。 |
| 6 | [如何透過 AEM Assets API 更新您的內容](update-your-content.md) | 了解如何使用 REST API 來存取並更新您的內容片段內容。 |
| 7 | [如何在 AEM Headless 中將您的應用程式和內容組合在一起](put-it-all-together.md)  | 了解如何取用 AEM 專案並使其準備就緒可上線與 AEM Headless SDK 搭配使用。 |
| 8 | [如何將 Headless 應用程式上線](go-live.md) | 瞭解如何即時部署應用程式，並在Git中取得本機程式碼，並將其移動到Cloud Manager Git以用於CI/CD管道。 |
| 9 | [選擇性 - 如何使用 AEM 建立單頁應用程式 (SPA)](create-spa.md) | 瞭解AEM Headless功能後，探索如何結合Headless和Headless傳遞，並瞭解如何使用AEM SPA Editor框架建立可編輯的SPA。 |

## 下一步 {#what-is-next}

您現在已準備好開始您的 Adobe Headless 歷程。我們鼓勵您繼續下一段歷程並閱讀文章 [瞭解CMS Headless開發。](learn-about.md)

### 選擇你自己的冒險 {#choose-your-path}

不過，Adobe希望您隨著開始使用AEM Headless專案而成功，無論您的學習風格如何。 因此，請考慮這兩個選項。

* 如果您希望繼續&#x200B;**了解 Headless 概念和 AEM Headless 技術**，您應該接著檢閱此文件[如何為您的內容建立 AEM 內容模型](model-your-content.md)來繼續您的 AEM Headless 歷程，此文件可讓您了解如何在 AEM 為內容結構建立模型。
* 如果您偏好&#x200B;**做中學**，您可以移至 [AEM Headless 入門實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，在這裡您將直接進入 AEM Headless 開發，方式是實作一個簡單專案以公開 AEM Headless 內容。

## 其他資源 {#additional-resources}

文件歷程會透過敘述方式，指導您完成複雜的相關流程和功能，向您展示 AEM 如何解決業務問題。此歷程說明了多個功能如何共同運作以解決單一業務需求。

因此，歷程的設計宗旨是獨立自主。 但是，其中數個可以相互關聯。 查看這些額外的歷程，進一步了解 AEM 的強大功能如何協同工作。

* [AEM Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 如果您偏好做中學並為傾向技術，請加入我們的由 API 和框架組織的實作教學課程，其在探究如何建立和使用 AEM Headless 應用程式。
* [AEM Headless 翻譯歷程](/help/journey-headless/translation/overview.md) - 此文件歷程讓您對 Headless 技術、AEM 如何提供 Headless 內容以及如何翻譯它，有廣泛的了解。
* [Headless 製作歷程](/help/journey-headless/author/overview.md) - 從這裡開始，此歷程會逐步引導您了解 AEM 強大且靈活的 Headless 特性、其功能，以及如何在您的第一個 Headless 專案中建立內容模型。
* [Headless架構者歷程](/help/journey-headless/architect/overview.md)  — 從這裡開始瞭解Adobe Experience Manager強大且有彈性的無周邊功能，以及如何為您的專案建立內容的模型。
* [AEM技術檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)  — 如果您已對AEM和Headless技術有一定的瞭解，則可能需要直接參閱深入的技術檔案。

   * [AEM as a Headless CMS 簡介](/help/sites-developing/headless/introduction.md)

* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
