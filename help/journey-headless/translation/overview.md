---
title: AEM無頭翻譯歷程
description: 從這裡開始，使用AEM功能強大的翻譯工具，引導您完成無頭內容的轉譯。
index: true
hide: false
hidefromtoc: false
source-git-commit: 7cf68868e0963930bde9fcda647822a03914b61d
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 2%

---

# AEM無頭翻譯歷程 {#aem-headless-translation-journey}

從這裡開始，使用AEM功能強大的翻譯工具，引導您完成無頭內容的轉譯。

## 簡介 {#introduction}

無頭式實作對於將體驗提供給對象（無論對象在何處、不論管道、地區或地區）來說日益重要。

無頭實作會放棄頁面和元件管理，如同在完整堆疊解決方案中的傳統做法，並著重於建立不受管道影響、可重複使用的內容片段及其跨管道傳送。 透過使用AEM功能強大的翻譯工具，這些可重複使用的片段可輕鬆翻譯，並傳送給您的對象（無論其在何處）。

本指南會引導您了解最重要的無頭翻譯主題，以便您在完成時：

* 概略了解何謂無頭式內容傳送。
* 了解AEM無頭功能。
* 了解AEM翻譯功能，以及這些功能與無頭內容的相關性。
* 能夠開始翻譯您自己的無頭內容。

目標是讓您廣泛了解無頭式技術、AEM如何提供無頭式內容，以及如何翻譯內容。 如果您不熟悉其中的任何主題，這是您理想的起點。

如果您已熟悉AEM、無頭式和翻譯，您可能已具備此歷程的基本知識。 請考慮參考以下連結的技術檔案： [下方的其他資源一節。](#additional-resources)

## AEM檔案歷程 {#documentation-journeys}

[檔案歷程](/help/journey-documentation/home.md) 將許多不同的、可能複雜的主題和特徵聯繫起來，提供一種敘述，幫助讀者從頭到尾理解並解決業務問題，同時假定事先的主題或AEM知識最少。

說明檔案歷程是根據最佳實務原則而設計，根據Adobe的最新研究、Adobe顧問經驗證的實作經驗，以及客戶專案的意見回饋。

如果您想了解Adobe建議如何使用AEM解決無頭式業務案例， [AEM無頭歷程](/help/journey-headless/home.md) 是開始的位置。

## 對象 {#audience}

此歷程專為翻譯專家人員而設計，通常稱為翻譯項目經理或TPM。 此歷程說明在AEM中轉譯無頭內容的需求、步驟和方法。 歷程可能會定義翻譯專家必須與之互動的其他角色，但歷程的觀點是翻譯專家。

此歷程假設讀者在大型CMS系統上具備翻譯內容的經驗，但假設您不具備無頭式技術或AEM的知識。

以下是在此歷程中互動的角色。

| 角色 | 說明 | 歷程中的角色 |
|---|---|---|
| 翻譯專家 | 定義應翻譯的內容並管理這些工作流程 | 此歷程的受眾 |
| 內容作者 | 建立和管理無謂傳送的內容 | 內容作者建立翻譯專家必須翻譯的內容。 |
| 管理員 | 管理AEM的基本設定和配置 | 翻譯專家會與管理員合作，進行翻譯所需的配置更改，例如安裝翻譯連接器。 |
| 內容架構師 | 分析必須無謂傳送的資料需求，並定義此資料的結構 | 翻譯專家會與內容架構師合作，定義內容的組織，以便輕鬆翻譯。 |

此歷程中的資訊當然對所有角色都有用，但某些資訊對某些角色可能是多餘的。 請繼續觀看 [即將到來的歷程，涵蓋其他角色。](/help/journey-documentation/home.md#journeys)

## 無頭翻譯歷程 {#the-journey}

您將在此歷程中探索許多主題。 以下文章提供您在轉譯AEM中無頭內容的基礎知識，並連結至詳細的技術檔案。

雖然您可以直接前往歷程的特定部分，但許多概念都是以先前文章中的概念為基礎而建立。 因此，如果您剛接觸AEM中的無頭翻譯，建議您從頭開始，依序進行。

| # | 文章 | 說明 |
|---|---|---|
| 0 | AEM無頭翻譯歷程 | 此文檔 |
| 1 | [了解無頭內容，以及如何在AEM中翻譯](learn-about.md) | 了解無頭概念、它們如何對應至AEM，以及AEM翻譯理論。 |
| 2 | [開始使用AEM無頭翻譯](getting-started.md) | 了解如何組織無頭內容，以及AEM翻譯工具的運作方式。 |
| 3 | [配置翻譯連接器](configure-connector.md) | 了解如何將AEM連線至翻譯服務。 |
| 4 | [配置翻譯規則](translation-rules.md) | 了解如何定義翻譯規則，以識別翻譯內容。 |
| 5 | [翻譯內容](translate-content.md) | 使用翻譯連接器和規則來翻譯無頭內容。 |
| 6 | [發佈翻譯的內容](publish-content.md) | 了解如何發佈翻譯內容，並在更新基礎內容時更新翻譯。 |

## 下一步 {#what-is-next}

您現在已準備好開始無Adobe頭翻譯歷程。 我們鼓勵您繼續前往歷程的下一個部分並閱讀文章 [了解無頭內容，以及如何在AEM中翻譯](learn-about.md)

## 其他資源 {#additional-resources}

說明檔案歷程會告訴您AEM如何透過提供敘述來解決業務問題，以引導您完成複雜、相互關聯的流程和功能。 歷程說明多個功能如何搭配運作以滿足單一業務需求。

因此，這些旅程的設計是獨立的。 但是，其中許多是可以相互關聯的。 請查看這些其他歷程，深入了解AEM強大功能如何搭配運作。

* [無頭製作歷程](/help/journey-headless/author/overview.md)  — 從這裡開始，引導您一路探索AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個無頭式專案中建立內容模型。
* [無頭架構師歷程](/help/journey-headless/architect/overview.md)  — 從這裡開始，介紹Adobe Experience Manager強大、靈活、無頭的功能，以及如何為專案建立內容模型。
* [AEM Headless Developer Journey](/help/journey-headless/developer/overview.md)  — 從這裡開始，逐步引導您了解AEM強大且有彈性的無頭式功能、其功能，以及如何在您的第一個開發專案中運用這些功能。
* [AEM技術檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)  — 如果您已對AEM和無頭技術有明確的了解，您可直接諮詢我們的深入技術檔案。
* [AEM Headless教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 如果您偏好從實踐中學習，而且在技術上有傾向，請利用我們按API和架構組織的實作教學課程，探索如何建立和使用以AEM Headless建置的應用程式。
