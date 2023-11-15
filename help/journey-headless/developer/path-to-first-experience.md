---
title: 踏上首次使用 AEM Headless 之路
description: 在 AEM Headless 開發人員歷程的這一部分中，您將了解在 AEM 中實作您的第一個 Headless 體驗的步驟 (包括規劃考量事項)，並學習最佳做法以使您的操作過程盡可能順利。
exl-id: 64a87b6b-67ff-4d88-9dfb-c3e5de65bbe6
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 91%

---

# 踏上首次使用 AEM Headless 之路 {#path-to-first-experience}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，您將了解在 AEM 中實作您的第一個 Headless 體驗的步驟 (包括規劃考量事項)，並學習最佳做法以使您的操作過程盡可能順利。

## 到目前為止 {#story-so-far}

在 AEM Headless 歷程的上一個文件「[AEM Headless 快速入門](getting-started.md)」中，您已了解 Headless CMS 的基本理論，您現在應該：

* 了解 AEM Headless 功能的基本概念。
* 了解 AEM Headless 功能的使用先決條件。
* 明白 AEM Headless 整合層級。
* 能夠根據範圍定義您的專案。

本文章以這些基本知識為基礎，以便您了解如何準備您自己的 AEM Headless 專案。

## 目標 {#objective}

本文件可協助您了解實作第一個專案所需的步驟。閱讀本文件後，您應該：

* 了解設計內容的重要規劃考量事項。
* 了解在 AEM 中實作 Headless 的步驟。
* 了解需要哪些必要工具和 AEM 設定。
* 了解使您的 Headless 歷程順暢、持續高效產生內容以及確保內容快速傳遞的最佳做法。

## 要求 {#requirements}

在繼續閱讀本文件之前，務必先查閱 AEM Headless 開發人員歷程的上一篇文件[AEM Headless 快速入門](getting-started.md)，以確保您：

* 符合列出的要求。
* 已考慮您自己的專案定義，包括範圍、角色和效能。

## 為成功做規劃 {#planning-for-success}

若要開始您的第一個 AEM Headless 專案，需要確保您有一個內容模型，可支援您想要跨所有管道進行的個人化和更新。

與AEM不同，如果您是建置使用者端應用程式，也希望確保設定適當的開發環境，以便針對對AEM的API呼叫測試使用者端。

### 定義內容模型和 API {#defining-models}

您想要促成一致的體驗並管理跨管道的個人化行銷活動，您可以將每個單獨的管道和表面視為其自己獨特的內容結構來傳遞。然而，讓每個管道都有自己的內容模型將很難維護。

相反地，您應該根據組織原則，例如品牌和產品階層、商品或表面目錄或是客戶歷程中的步驟，來考慮不同表面上的內容如何相關。例如，如果您有一組表面可支援您製造的特定品牌汽車，您可能想要從內容模型開始，取得適用於整輛汽車的一般資訊，然後是較為特定項目，例如車輛啟動時到出現維修問題時所需的內容。這類模型會強制繼承一般汽車品牌內容，也允許根據所需特定情境進行變換。這也能協助在未來管理此內容的更新，因為您可以根據角色強制執行控制，例如整體行銷人員或整個汽車品牌的產品經理，對比負責「啟動汽車」體驗的作者。

當您有了內容模型並清楚需要此內容的各種用戶端，您必須確保與存取各種內容模型關聯的 GraphQL/API 會發佈到需要此內容的所有用戶端。有不同方法可以存取特定內容。您可以要求一段特定的靜態內容，這樣可以快取內容並提高效能。您也可以要求動態產生的內容，這將需要更多處理。確保客戶使用最符合其業務需求的API。

## 了解您的環境 {#understanding-environments}

AEM 有三種類型的環境：開發、中繼和生產。

開發環境 (您可以有多個) 是實驗和嘗試想法的安全地方。在專案的初始階段，Adobe 建議使用開發環境來嘗試各種版本的內容模型，並查看哪些版本為表面提供預期的輸出。

Headless 專案的中繼環境用於在新的 AEM 產品版本推送到生產環境之前對其進行驗證。在那裡保留最新的生產內容模型清單和內容子集，當您進行變更或 AEM 版本引入變更時，您就可以呈現 JSON 檔案以比較它們是否仍然提供相同的輸出。

生產環境是內容作者建立和管理其實際內容的地方。在生產環境變更模型必須小心進行，並謹記回溯相容性。

在開發階段，建議您使用開發和中繼環境。當您轉向效能測試時，您會想要移至生產環境。

### 開發人員和內容作者協力合作 {#cooperation}

開發人員需要的 AEM 開發環境是內含填入的內容模型。由於內容作者仍在建立內容，開發人員開發的用戶端將取用 AEM 的 Headless 內容。這就是 API 定義非常重要的原因。透過使用AEM SDK，開發人員可以建立測試勾點，以便建立使用者端和單元測試，確保使用者端能夠正確轉譯內容。

內容作者根據已在中繼環境定義的內容模型建立內容。使用內容片段製作工具，作者會建立內容片段或編輯現有的內容片段。 在發佈之前，作者可以與開發人員合作將內容模型推送至開發環境，或僅為作者設定開發人員環境，來預覽它在用戶端中的外觀。

## 設定 {#setup}

在 AEM 中開始使用 Headless 技術之前，您需要確保已啟用所有必要的功能。本章節概述相關要求。完成這些步驟的實際步驟將在 [AEM Headless 開發人員歷程](#overview.md)的後續部分詳細說明。

您也可以選擇檢視 [其他資源](#additional-resources) 以取得個別主題的詳細資訊。

### 設定 {#configuration}

1. 啟用內容片段
1. 啟用 GraphQL
1. 設定 Headless SDK

## 實作您的第一個 AEM Headless 應用程式

這是概述需要哪些東西才能使用 AEM 實作您的第一個無周邊應用程式以傳遞您的內容。如何執行這些步驟將在Headless 開發人員歷程的後面部分詳細描述。

1. 建立內容片段模型
1. 建立內容片段
1. 使用 GraphQL 查詢內容

## 最佳做法 {#best-practices}

 Headless 專案的成功不僅在於實作的技術，還在於良好的規劃和專案管理。以下是內容作者和開發人員在規劃專案時應牢記的幾個最佳實務。

### 組織您的內容 {#organizing-content}

* 使結構具有所需的複雜度，但盡可能保持簡單。更簡單的內容結構有助於簡化內容管理並提高系統效能。
* 您的策略要優先考慮內容重複使用。建立可跨多個高層級模型和管道重複使用的子模型和內容參考。
* 使內容結構盡可能簡單易懂，以便內容作者可以快速學習並適應編寫任務。
* 如果您有存取限制，請嘗試使您的內容模型與存取要求保持一致。
* 當您有存取要求時，它們應該推動您的內容階層。將同一組人員編輯的內容群組在一起。
* 將類似內容群組到一個資料夾中。
   * 內容作者更有可能會複製並貼上現有內容以建立新內容。 因此，在同一資料夾中完成此操作可以提高效率。
   * AEM 允許為每個資料夾設定允許的模型，因此&#x200B;**新建**&#x200B;按鈕將僅顯示該位置支援的模型。
* 如果在模型中設定了根資料夾，則內聯內容片段編輯器建立新內容片段的作業將可簡化。然後從業人員不必選擇位置，只需提供名稱即可開始編輯新參考。

### 編寫內容 {#authoring}

* 對於內容的管道特定版本，請考慮使用內容片段變化。變化與內容主版同步，以簡化內容變更管理。
* 邀請其他內容製作者審查內容並提供意見回饋 (內含註解和評論)，這些可在內容片段編輯器中取得，也可在內容片段 Admin Console 中跨片段全域取得。
* 使用盡可能少使用必要元素讓事情繼續進行。必要元素會讓工作流程無法進行。

### 編寫全域內容 {#localization}

* 建立內容翻譯規則和控管。為了降低系統負載，將翻譯工作建立為能以較長間隔執行的非同步流程。留出時間進行本地化品質控制和錯誤修正。
* 利用您的翻譯技術系統提供的所有功能，您可以將這些功能與 AEM 相整合，例如翻譯記憶庫。
* 了解多媒體內容 (例如影像和視訊) 是否需要本地化。

## 下一步 {#what-is-next}

您已完成此部分的 AEM Headless 開發人員歷程，您應該：

* 了解設計內容的重要規劃考量事項。
* 了解在 AEM 中實作 Headless 的步驟。
* 了解需要哪些必要工具和 AEM 設定。
* 了解使您的 Headless 歷程順暢、持續高效產生內容以及確保內容快速傳遞的最佳做法。

我們希望您以此基本知識為基礎，充分了解 AEM Headless 的強大功能和靈活性，以便利用在自己的專案上。為此，您有多種選擇。

### 選擇你自己的冒險 {#choose-your-path}

無論您的學習方式為何，Adobe 都希望您能順利開始您的 AEM Headless 專案。

* 如果您偏好繼續&#x200B;**了解 Headless 概念和 AEM 的 Headless 技術**，您應該建議繼續您的 AEM Headless 歷程，接著閱讀此文件[如何為您的內容建立 AEM 內容模型](model-your-content.md)，您可以在此了解如何在 AEM 中建立內容結構的模型。
* 如果您偏好&#x200B;**做中學**，您可以移至 [AEM Headless 入門實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)，在這裡您將直接進入 AEM Headless 開發，方式是實作一個簡單專案以公開 AEM Headless 內容。

## 其他資源 {#additional-resources}

雖然建議您查閱文件[如何為您的內容建立 AEM 內容模型](model-your-content.md)來繼續 Headless 開發歷程的下個部分，以下也有一些其他選擇性資源，在深入探究本文件提到的一些概念，但不是繼續 Headless 歷程的必要條件。

* [AEM Headless 翻譯歷程](/help/journey-headless/translation/overview.md) - 此文件歷程讓您對 Headless 技術、AEM 如何提供 Headless 內容以及如何翻譯它，有廣泛的了解。
* [AEM Sites 的 Headless 開發](/help/sites-developing/headless/introduction.md) - 快速介紹讓 AEM Headless 開發人員熟悉必要的功能
* [AEM Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 利用這些實作教學課程來探索如何運用各種不同方式使用 AEM 將內容傳遞到 Headless 端點，並選擇適合您的方式。
* [使用 GraphQL API 進行 Headless 內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;Launch=ExperienceManager-D-1-2020.1.headless#courses) - 按照本課程說明對 AEM 中實作的 GraphQL API 有概略的了解。必須透過 AdobeID 進行驗證。
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - 此 GitHub 專案包含以 AEM GraphQL API 為重點的範例應用程式。
* [Headless快速入門手冊](/help/sites-developing/headless/introduction.md#getting-started)  — 向已瞭解AEM的使用者快速介紹AEM Headless功能。
* [建立內容片段模型](/help/assets/content-fragments/content-fragments-models.md) - 內容片段模型的技術文件
* [建立內容片段](/help/assets/content-fragments/content-fragments.md) - 內容片段的技術文件
* [使用 GraphQL 查詢內容](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) - GraphQL API 的技術文件
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
