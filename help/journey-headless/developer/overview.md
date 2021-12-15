---
title: AEM Headless Developer Journey
description: AEM無頭CMS檔案。 從這裡開始，引導您逐步了解AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個開發專案中運用這些功能。
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---

# AEM Headless Developer Journey {#aem-headless-developer-journey}

從這裡開始，引導您逐步了解AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個無頭式開發專案中運用這些功能。 本歷程提供您開發第一個無頭應用程式所需的所有AEM檔案。

## 簡介 {#introduction}

無頭實作會放棄頁面和元件管理，如同在完整堆疊解決方案中的傳統做法，並著重於建立不受管道影響、可重複使用的內容片段及其跨管道傳送。 這是實作數位體驗的現代化、動態開發模式。

本指南會帶您了解AEM中最無頭式的實作主題，讓您在完成時：

* 全面了解無頭式內容的傳遞方式及其優點。
* 了解AEM無頭功能，以及它們如何共同合作以提供無頭體驗。
* 能夠採取實作第一個AEM無頭專案的前幾個步驟。

## AEM檔案歷程 {#documentation-journeys}

[檔案歷程](/help/journey-documentation/home.md) 將許多不同的、可能複雜的主題和特徵聯繫起來，提供一種敘述，幫助讀者從頭到尾理解並解決業務問題，同時假定事先的主題或AEM知識最少。

說明檔案歷程是根據最佳實務原則而設計，根據Adobe的最新研究、Adobe顧問經驗證的實作經驗，以及客戶專案的意見回饋。

如果您想了解Adobe建議如何使用AEM解決無頭式業務案例， [AEM無頭歷程](/help/journey-headless/home.md) 是開始的位置。

>[!TIP]
>
> 如果您偏好 **學習** 且在技術上有傾向，請造訪AEM Headless教學課程，這些教學課程由API和架構組織，並可在 [「其他資源」部分](#additional-resources) 在此文檔的末尾。

## 對象 {#audience}

此歷程專為開發人員角色而設計，從開發人員的角度規劃AEM Headless專案的需求、步驟和方法。 歷程會定義開發人員在成功的專案中必須與其互動的其他角色，但歷程的觀點是開發人員的角色。

以下是在此歷程中互動的角色。

| 角色 | 說明 | 此歷程中的角色 |
|---|---|---|
| 開發人員（目標受眾） | 具有開發無頭應用程式的經驗，這些應用程式會從不同的來源消費內容 | 鎖定此歷程的受眾 |
| 內容作者 | 建立和管理無謂傳送的內容 | 內容作者建立開發人員無端提供的內容。 |
| 管理員 | 管理AEM的基本設定和配置 | 開發人員與管理員合作，以變更開發所需的設定。 |
| 內容架構師 | 分析必須無謂傳送的資料需求，並定義此資料的結構 | 開發人員與內容架構師合作，了解資料的結構，以及無端傳送資料的需求。 |

此歷程中的資訊當然對所有角色都有用，但某些資訊對某些角色可能是多餘的。 請繼續觀看 [即將到來的歷程，涵蓋其他角色。](/help/journey-documentation/home.md#journeys)

## 無頭式開發人員歷程 {#the-journey}

您將在此歷程中探索許多主題。 以下文章提供您AEM中無頭的基礎知識，並連結至詳細的技術檔案。

雖然您可以直接前往歷程的特定部分，但許多概念都是以先前文章中的概念為基礎而建立。 因此，如果您剛接觸AEM中的無頭部，建議您從頭開始，依序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM Headless Developer Journey | 此文檔 |
| 1 | [了解CMS無頭開發](learn-about.md) | 了解無頭技術及其使用時機。 |
| 2 | [AEM Headless 快速入門](getting-started.md) | 了解AEM Headless必要條件 |
| 3 | [使用AEM Headless的第一次體驗路徑](path-to-first-experience.md) | 設定您的開發環境，並了解如何將簡單應用程式與AEM Headless整合 |
| 4 | [如何建立內容模型](model-your-content.md) | 了解如何建立內容結構的模型。 然後，使用內容片段模型和內容片段來實現Adobe Experience Manager(AEM)的結構，以便跨頻道重複使用。 |
| 5 | [如何透過AEM傳送API存取您的內容](access-your-content.md) | 了解如何使用GraphQL查詢來存取您的內容片段內容。 |
| 6 | [如何透過AEM Assets API更新您的內容](update-your-content.md) | 了解如何使用REST API存取和更新您的內容片段內容。 |
| 7 | [如何將所有內容放在一起 — 您的應用程式和AEM Headless中的內容](put-it-all-together.md) | 了解如何取得您的AEM專案，並準備以使用AEM Headless SDK上線。 |
| 8 | [選用 — 如何使用AEM建立單頁應用程式(SPA)](create-spa.md) | 了解AEM無頭功能後，請探索如何結合無頭和無頭傳送，並了解如何使用AEM SPA Editor架構建立可編輯的SPA。 |

<!-- HM-Links
|8|[How to go live with your headless application](go-live.md)|Learn how to deploy application live and take your local code in Git and move it to Cloud Manager Git for CI/CD pipeline.|
|9|[Optional - How to create single page applications (SPAs) with AEM](create-spa.md)|Once you understand AEM's headless features, explore how to combine headful and headless delivery and learn how you can create editable SPAs using AEM's SPA Editor framework.|
-->

## 下一步 {#what-is-next}

您現在已準備好開始Adobe無頭歷程。 我們鼓勵您繼續前往歷程的下一個部分並閱讀文章 [了解CMS無頭開發。](learn-about.md)

### 選擇自己的冒險 {#choose-your-path}

不過，無論您的學習風格如何，Adobe都希望您在開始使用AEM Headless專案時能成功。 所以請考慮這兩個選擇。

* 如果您偏好繼續 **了解無頭概念和AEM無頭技術**，您應依建議繼續進行AEM無頭歷程，接下來檢閱檔案 [如何將內容模型為AEM內容模型](model-your-content.md) 可在此了解如何在AEM中建立內容結構模型。
* 如果您偏好 **學習**，您可以跳到 [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) 透過實作簡單專案來公開AEM無頭式內容，您將直接進入AEM開發。

## 其他資源 {#additional-resources}

說明檔案歷程會告訴您AEM如何透過提供敘述來解決業務問題，以引導您完成複雜、相互關聯的流程和功能。 歷程說明多個功能如何搭配運作以滿足單一業務需求。

因此，這些旅程的設計是獨立的。 但是，其中許多是可以相互關聯的。 請查看這些其他歷程，深入了解AEM強大功能如何搭配運作。

* [AEM Headless教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 如果您偏好從實踐中學習，而且在技術上有傾向，請利用我們按API和架構組織的實作教學課程，探索如何建立和使用以AEM Headless建置的應用程式。
* [AEM無頭翻譯歷程](/help/journey-headless/translation/overview.md)  — 本檔案歷程可讓您廣泛了解無頭式技術、AEM如何提供無頭式內容，以及如何翻譯內容。
* [無頭製作歷程](/help/journey-headless/author/overview.md)  — 從這裡開始，引導您一路探索AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個無頭式專案中建立內容模型。
* [無頭架構師歷程](/help/journey-headless/architect/overview.md)  — 從這裡開始，介紹Adobe Experience Manager強大、靈活、無頭的功能，以及如何為專案建立內容模型。
* [AEM技術檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)  — 如果您已對AEM和無頭技術有明確的了解，您可直接諮詢我們的深入技術檔案。
