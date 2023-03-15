---
title: AEM Headless 快速入門
description: 在 AEM Headless 開發人員歷程的這一部分，了解 AEM Headless 先決條件。
exl-id: a94794a4-bf8b-4f3b-a761-3f02feedd5c0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 100%

---

# AEM Headless 快速入門 {#getting-started}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，了解需要滿足哪些條件才能使用 AEM Headless 開始您自己的專案。

## 到目前為止 {#story-so-far}

在 AEM 無周邊歷程的上一個文件「[了解 CMS Headless 開發](learn-about.md)」中，您已了解了 Headless CMS 的基本理論，現在您應該：

* 了解無周邊內容傳遞的基本概念和術語
* 了解為何與何時需要無周邊
* 概略了解無周邊概念如何使用以及它們是如何相互關聯的

本文章以這些基本知識為基礎，以便您了解如何使用 AEM 實作無周邊解決方案。

## 目標 {#objective}

本文件可幫助您在自己的專案情境中了解 AEM Headless。閱讀本文件後，您應該：

* 了解 AEM 無周邊功能的基本概念。
* 了解 AEM 無周邊功能的使用先決條件。
* 明白 AEM 無周邊整合層級。
* 能夠根據範圍定義您的專案。

## AEM 基本概念 {#aem-basics}

在 AEM 中定義無周邊專案之前，了解一些基本的 AEM 概念非常重要。

### 作者執行個體 {#author}

最簡單的情況是，AEM 由一個作者執行個體和一個[發佈執行個體](#publish)組成，它們協同工作以建立、管理和發佈您的內容。

內容從作者執行個體開始。這是內容作者建立內容的地方。作者環境為作者提供了各種工具來建立、組織和重複使用他們的內容。

### 發佈執行個體 {#publish}

在作者執行個體中建立內容後，必須將其發佈以供其他服務取用。發佈執行個體包含所有已發佈的內容。

### 複製 {#replication}

複製是將內容從作者執行個體轉移到發佈執行個體的動作。當作者或具有適當權限的其他使用者發佈內容時，AEM 會自動完成此操作。

### AEM 基本概念摘要 {#aem-basics-summary}

在最簡單的層級上，在 AEM 中建立數位體驗需要以下步驟：

1. 您的內容作者會在作者執行個體中建立您的無周邊內容。
1. 當此內容準備就緒時，它會被複製到發佈執行個體。
1. 然後可以呼叫 API 來擷取此內容。

AEM Headless 提供強大的工具來管理無周邊內容，從而建構此技術基礎，[將在下一節中介紹。](#aem-headless-basics)

## AEM Headless 基本概念 {#aem-headless-basics}

AEM 的無周邊功能以幾個關鍵功能為基礎。這些將在歷程的後續部分詳細說明。現在重點只需知道它們的作用和名稱。

### 內容片段模型 {#content-fragment-models}

內容片段模型定義您在 AEM 中建和管理之資料和內容的結構。它們做為您內容的支架。選擇建立內容時，您的作者會從您定義的內容片段模型中進行選擇，這會指引他們建立內容。

### 內容片段 {#content-fragments}

內容片段允許您設計、建立、規劃和發佈每頁自主的內容。它們可讓您將內容準備就緒用於多個位置和多個管道。

內容片段包含結構化內容，能以 JSON 格式傳遞。

### GraphQL 和 REST API {#apis}

為了以無周邊方式修改您的內容，AEM 提供了兩個強大的 API。

* GraphQL API 允許您建立存取和傳遞內容片段的要求。
* 資產 REST API 允許您建立和修改內容片段 (和其他資產)。

您將在 AEM 無周邊歷程的後續部分，了解這些 API 以及如何使用它們。或者參閱下面的[其他資源](#additional-resources)章節，以取得其他文件。

## Headless 整合層級 {#integration-levels}

AEM 支援 CMS 的全無周邊模型和傳統的全堆疊或有周邊模型。但是，AEM 不僅提供這兩種獨特的選擇，而且也支援結合了兩者優勢的混合模型，從而為您的無周邊專案提供獨特的靈活性。

為了確保您了解無周邊概念，此 AEM Headless 開發人員歷程重點放在純無周邊模型，讓您在 AEM 中無需編寫程式碼即可快速開始使用。

但是，一旦您了解 AEM 無周邊功能，您就應明白混合模型帶來的額外可能性。下面列出了這些案例，以便您明白。在歷程結束時，您將更詳盡地了解這些概念，以防您的專案需要這種靈活性。

### 您有無周邊內容的外部取用者，例如單頁應用程式 (SPA)。 {#already-have-a-spa}

讓我們假設您的基本要求至少是將內容從 AEM 傳遞到現有的外部服務。

#### 層級 1：內容片段整合 - 傳統的無周邊模型 {#level-1}

此整合層級是傳統的無周邊模型，允許您的內容作者在 AEM 中建立內容，並使用 GraphQL 將以無周邊方式傳遞到任意數量的外部服務，或者使用資產 API 從外部服務編輯它們。AEM 中不需要編寫程式碼。

在此模型中，AEM 僅用於使用 AEM 內容片段建立和提供內容。內容的呈現和互動則委託給取用內容的外部應用程式，通常是單頁應用程式 (SPA)。

#### 層級 2：將 SPA 嵌入 AEM - 混合模型 {#level-2}

此整合層級是建置在層級 1 上，也允許將外部應用程式 (SPA) 嵌入到 AEM 中，以便內容作者可以在 AEM 內的外部應用程式情境中檢視內容。該應用程式也支援在 AEM 中對外部應用程式進行有限編輯。

此層級的優勢是允許內容作者以有周邊方式在 AEM 中靈活地編寫內容，他們的內容會在嵌入的外部 SPA 中依情境呈現，同時仍以無周邊方式傳遞內容。

#### 層級 3：在 AEM 中嵌入並完全啟用 SPA - 混合模型 {#level-3}

此整合層級是建置在層級 2 上，使外部 SPA 中的大部分內容都可以在 AEM 中進行編輯。

### 您沒有無周邊內容的外部取用者，例如單頁應用程式 (SPA)。 {#do-not-have-a-spa}

如果您的目標是建立一個新的 SPA 以無周邊方式取用來自 AEM 的內容，您可以使用內容片段等功能來管理您的無周邊內容，也可以使用 AEM 的 SPA 編輯器架構建置 SPA。

使用 SPA 編輯器，SPA 不僅可以取用來自 AEM 的內容，還可以由您的內容作者在 AEM 中進行完全編輯，從而為您提供在 AEM 中進行無周邊傳遞和在情境中編輯的靈活性。

## 要求和先決條件 {#requirements-prerequisites}

有許多要求必須符合，才能開始無周邊 AEM 專案。

### 知識 {#knowledge}

* GraphQL
* 使用 React 或 Angular 框架建立 SPA 的開發經驗
* 建立內容片段和使用編輯器的基本 AEM 技能

### 工具 {#tools}

* 用於測試部署專案的沙箱存取權
* 用於資料模型和測試的本機開發執行個體
* 您的無周邊 AEM 內容的現有外部 SPA 或其他取用者

## 定義您的專案 {#defining-your-project}

對於任何成功的專案，重要的是不僅要明確定義專案的要求，還要明確定義角色和責任。

### 範圍 {#scope}

明確定義專案的範圍很重要。範圍告知接收標準，並允許您設立完成的定義。

您必須問的第一個問題是「我想透過 AEM Headless 實現什麼目標？」一般來說，答案應該是您擁有或將來將擁有您使用自己的開發工具而非 AEM 建置的體驗應用程式。此體驗應用程式可以是行動應用程式、網站或任何其他面向取用內容之使用者的體驗應用程式。使用 AEM Headless 的目標是使用最先進的 API 為您的體驗應用程式提供在 AEM 中建立、儲存和管理的內容，這些 API 會直接從您的體驗應用程式呼叫 AEM Headless 以擷取內容或甚至是全 CRUD 內容。如果這不是您想要的，您可能想要[返回 AEM 文件](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)尋找符合您目標的內容。

### 角色和責任 {#roles-responsibilities}

任一專案的角色皆不相同，但在 AEM 無周邊開發方面需要考慮的重要角色是：

* [管理員](#administrator)
* [內容作者](#content-author)
* [內容架構師](#content-architect)
* [開發人員](#developer)

#### 管理員 {#administrator}

管理員負責系統的基本設定和配置。例如，管理員在 Adobe 使用者管理系統 (稱為 Identity Management System (IMS)) 中設定您的組織。Adobe 在 IMS 中建立您的組織後，管理員是組織中第一個收到來自 Adobe 的電子郵件邀請的使用者。管理員可以登入 IMS 並新增其他角色的使用者。

管理員設定好使用者後，他們將被授予存取所有 AEM 資源的權限，以完成他們的份內工作，使用 AEM Headless 傳遞體驗應用程式。

管理員應該是設定 AEM 並準備好執行階段，以使[內容作者](#content-author)能夠建立和更新內容，[開發人員](#developer)使用 API 擷取或修改內容以供體驗應用程式取用。

#### 內容作者 {#content-author}

內容作者建立和管理 AEM 無周邊傳遞的內容。內容作者使用內容片段和資產主控台等 AEM 功能來管理他們的內容。

內容作者應謹記以下最佳做法。

#### 翻譯計劃 {#translation}

在專案一開始就計劃翻譯。將「翻譯專家」視為一個獨立的角色，其職責是定義哪些內容應該翻譯，哪些內容不應該翻譯，以及哪些翻譯內容可以由區域或本機內容作者修改。

根據您需要的內容翻譯擬訂計劃。

* 您需要不同的語言還是需要不同的語言來適應地區的具體情況？
* 您是否需要圖像或影片等多媒體內容依不同地區設定而有所不同？

清楚您的內容更新工作流程。系統必須支援的核准流程是什麼？是否可以利用 AEM 工作流程來自動化此流程？

請注意，可以利用您的[內容階層](#content-hierarchy)讓翻譯變輕鬆。

請參閱[其他資源](#additional-resources)章節，了解有關 AEM 工作流程和翻譯工具的其他文件，包括指向 AEM Headless 翻譯歷程的連結。

##### 利用內容階層 {#content-hierarchy}

資料夾階層可以解決與內容管理有關的兩個主要問題：

* [翻譯](#translation) - AEM 透過在地區設定資料夾中維護內容副本，來管理內容翻譯。
* 組織 - 資料夾用於定義支援翻譯需求以及邏輯管理內容片段所需的內容階層。

AEM 允許靈活的內容結構，階層可以任意擴大。但是，重要的是要認識到，資料夾結構的任何變更都可能對 [依賴於內容路徑的現有查詢造成未預期的後果。](#developer)因此，事先明確設定的定義完善的階層可能對您的內容作者有所幫助。

資料夾也可以限制為只允許某些類型的內容 (根據內容片段模型)。建議一律明確指定階層中的所有資料夾允許哪些模型。為特定資料夾指定允許的內容：

* 防止內容作者編寫不屬於該資料夾的內容。
* 在建立內容時篩選資料夾允許的內容類型以僅顯示有效的內容類型，藉此將內容建立流程最佳化。

透過建立適當的內容結構，可以更輕鬆地跨管道協調無周邊內容的編寫，以最大限度地重複使用內容。利用跨多個管道的內容大幅提升內容生產效率和變更管理。

##### 建立良好的命名慣例 {#naming-conventions}

內容片段名稱必須對內容作者具有描述性。AEM 透明地將在存放庫層級別使用的 ID 名稱逸出和/或截斷。因此，內容作者提供的邏輯名稱應一律具可讀性並代表內容。

* 錯誤名稱：`cta_btn_1`
* 良好名稱：`Call To Action Button`

有關 AEM 頁面命名慣例的其他文件，請參閱[其他資源](#additional-resources)章節。

##### 不要過度擴展內容巢狀 {#content-nesting}

[內容片段](#content-fragments) 在 AEM 中用於建立無周邊內容。對於內容片段的內容巢狀，AEM 支援最多十層。但是請務必記住，AEM 必須迭代解析父內容片段中定義的每個參考，然後檢查所有同層級中是否有任何子參考。這些操作可以迅速累加並成為效能問題。

作為一般經驗法則，內容片段參考巢狀不應超過五層。

#### 內容架構師 {#content-architect}

內容架構師分析必須無周邊傳遞之資料的要求並定義該資料的結構。這些結構在 AEM 中稱為[內容片段模型](#content-fragment-models)。內容片段模型用作內容作者建立之內容片段的基礎。

定義內容片段模型時，一種有用的方法是建立對應到取用內容之應用程式 UX 元件的模型。

因為內容作者在建立新內容時會持續與模型互動，因此將模型與 UX 對齊有助於他們將生成的數位體驗視覺化。更進一步，您可以將圖示指派給表示 UX 元素的內容片段模型，以便作者可以根據視覺提示直覺地選擇正確的模型。

#### 開發人員 {#developer}

開發人員負責將在 AEM 中以無周邊方式建立的內容連接到該內容的取用者，通常是單頁應用程式 (SPA)、漸進式網頁應用程式 (PWA)、網路商店或 AEM 外部其他服務。

GraphQL 可作為 AEM 和無周邊內容取用者之間的「黏著劑」。GraphQL 是向 AEM 查詢必要內容的語言。

開發人員在計劃查詢時應謹記一些基本建議：

* 查詢不應依賴固定路徑 (`ByPath`) 來擷取內容片段。
   * [內容作者可完全控制內容片段階層](#content-hierarchy)，並可以進行會破壞此類查詢的變更。
   * 查詢應該改為選擇具有動態查詢參數的內容片段模型參考，以篩選結果以產生所需的裝載。
* 為獲得最佳查詢效能，在 AEM 一律使用持續性查詢。這些將在歷程後續部分中討論。
* GraphQL 以宣告方式遵循此座右銘「準確地詢問你需要什麼，並準確地得到它」。這表示在建立 GraphQL 查詢時，務必避免可能在關聯式資料庫建立的 `select *` 類型查詢。

對於[使用 AEM 的典型無周邊實作，](#level-1) 開發人員不需要 AEM 的編寫程式碼知識。

### 效能要求 {#performance-requirements}

任何專案要取得成功，在建立任何內容之前都必須考慮效能。

您必須了解您的使用者/訪客的期望和相關設計。設定服務層級目標 (SLO)，並加以測量以了解您是否滿足使用者的期望。

#### 流量模式 {#traffic-patterns}

若要了解流量和流量模式，首先要收集過去資料，然後預測未來幾年的預期成長。需要考慮的一些最重要的變數：

* 您預計每小時/每天/每月有多少次 API 呼叫，次數是否可能激增和季節性變化？
* 有多少不同的內容作者？
* 您預計有多少內容作者同時工作？
* 內容更新的頻率是多少？
* 需要多少個內容模型？
* 需要多少個模型執行個體？

#### 更新頻率 {#update-frequency}

通常不同的體驗部分具有不同的內容更新頻率。了解這一點對於能夠微調 CDN 和快取設定很重要。這也是給[內容架構師](#content-architects)的重要輸入，因為他們設計模型來表示您的內容。考慮：

* 某些類型的內容必須在一段時間後到期嗎？
* 是否存在因使用者特定而無法快取的元素？

## 下一步 {#what-is-next}

您已完成此部分的 AEM Headless 開發人員歷程，您應該：

* 了解 AEM 無周邊功能的基本概念。
* 了解 AEM 無周邊功能的使用先決條件。
* 明白 AEM 無周邊整合層級。
* 能夠根據範圍定義您的專案。

您應該繼續您的 AEM 無周邊歷程，接下來查看文件[踏上首次使用 AEM Headless 之路](path-to-first-experience.md)，您將在其中學習如何設定必要的工具，以及如何開始思考在 AEM 中建立資料模型。

## 其他資源 {#additional-resources}

雖然建議您查看文件[踏上首次使用 AEM Headless 之路](path-to-first-experience.md)，來繼續無周邊開發歷程，但以下是一些額外的內容和選用資源，對此文件提到的一些概念有更深入的探討，但它們不是繼續無周邊開發歷程的必要條件。

* [ AEM Headless 翻譯歷程](/help/journey-headless/translation/overview.md) - 此文件歷程讓您對無周邊技術、AEM 如何提供無周邊內容以及如何翻譯它，有廣泛的了解。
* [AEM Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 利用這些實作教學課程來探索如何運用各種不同方式使用 AEM 將內容傳遞到無周邊端點，並選擇適合您的方式。
* [使用 GraphQL API 進行 Headless 內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;Launch=ExperienceManager-D-1-2020.1.headless#courses) - 按照本課程說明對 AEM 中實作的 GraphQL API 有概略的了解。必須透過 AdobeID 進行驗證。
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - 此 GitHub 專案包含以 AEM GraphQL API 為重點的範例應用程式。
* [編寫概念](/help/sites-authoring/author.md) - 關於 AEM 編寫環境的技術文件，包含編寫-發佈設定的詳細說明。
* [發佈頁面](/help/sites-authoring/publishing-pages.md) - 關於在 AEM 發佈內容的技術文件。
* [命名慣例](/help/sites-developing/naming-conventions.md) - 關於 AEM 頁面命名限制的技術文件
* [多網站管理員和翻譯](/help/sites-administering/msm-and-translation.md) - 關於 AEM 強大翻譯功能的技術文件
* [AEM 工作流程](/help/sites-authoring/workflows.md) - 關於如何在 AEM 中自動化工作流程的技術文件
* [內容片段](/help/assets/content-fragments/content-fragments.md) - 關於內容片段的技術文件。
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) - 關於內容片段模型的技術文件。
* [GraphQL 技術文件](https://graphql.org) - GraphQL 定義 (外部連結)
* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) - 說明如何建立要求以存取和傳遞內容片段的技術文件
* [資產 REST API](/help/assets/assets-api-content-fragments.md) - 說明如何建立和修改內容片段 (和其他資產) 的技術文件
* [持續性查詢](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) - 關於 AEM 持續性查詢的技術文件
* [AEM Headful 和 Headless 技術 ](/help/sites-developing/headful-headless.md) - 對 AEM 中可用的無周邊整合層級的完整討論
