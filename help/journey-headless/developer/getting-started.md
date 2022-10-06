---
title: AEM Headless 快速入門
description: 在AEM無頭式開發人員歷程的這部分，了解AEM無頭式必要條件。
exl-id: a94794a4-bf8b-4f3b-a761-3f02feedd5c0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 1%

---

# AEM Headless 快速入門 {#getting-started}

在 [AEM無頭開發者歷程，](overview.md) 了解開始使用AEM Headless時自己的專案所需的項目。

## 迄今為止的故事 {#story-so-far}

在AEM無頭歷程的上一份檔案中， [了解CMS無頭開發](learn-about.md) 您學到了無頭式CMS的基本理論，現在應該：

* 了解無頭式內容傳送的基本概念和術語
* 了解需要無頭的原因和時機
* 從高層了解無頭概念的使用方式及其相互關係

本文以這些基本知識為基礎，讓您了解如何使用AEM來實作無頭式解決方案。

## 目標 {#objective}

本檔案可協助您在自己的專案內容中了解AEM Headless。 閱讀後，您應：

* 了解AEM無頭功能的基本概念。
* 了解使用AEM無頭功能的必要條件。
* 請注意AEM無頭整合層級。
* 能夠根據範圍定義專案。

## AEM基本介紹 {#aem-basics}

在AEM中定義無頭專案之前，請務必了解一些基本AEM概念。

### 製作例項 {#author}

最簡單的AEM是由製作例項和 [發佈例項](#publish) 可共同建立、管理和發佈您的內容。

內容從製作例項開始。 內容作者可在此建立其內容。 作者環境提供多種工具，供作者建立、組織和重複使用其內容。

### 發佈例項 {#publish}

內容在製作例項中建立後，就必須發佈，才可供其他服務使用。 發佈例項包含所有已發佈的內容。

### 複寫 {#replication}

復寫是將內容從製作例項傳輸至發佈例項的行為。 當作者或其他具有適當權限的使用者發佈內容時，AEM會自動完成此作業。

### AEM基本摘要 {#aem-basics-summary}

在最簡單的層級，在AEM中建立數位體驗需要下列步驟：

1. 您的內容作者會在製作例項中建立無頭內容。
1. 當此內容準備就緒時，會將其複製到發佈執行個體。
1. 接著，可呼叫API來擷取此內容。

AEM無頭式內容提供強大的工具，可管理無頭式內容，這是該技術基礎的基礎 [在下一節中說明。](#aem-headless-basics)

## AEM無頭基礎 {#aem-headless-basics}

AEM的無頭功能以幾項主要功能為基礎。 在歷程的後續部分會詳細說明這些內容。 現在，只有了解他們所做的基本知識和他們的名稱，才是重要的。

### 內容片段模型 {#content-fragment-models}

內容片段模型定義您在AEM中建立和管理的資料和內容的結構。 它們可以充當內容的支架。 選擇建立內容時，作者會從您定義的內容片段模型中選取，以引導他們建立內容。

### 內容片段 {#content-fragments}

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 它們可讓您準備內容，以便在多個位置和多個頻道中使用。

內容片段包含結構化內容，可以以JSON格式傳送。

### GraphQL和REST API {#apis}

為了無故修改您的內容，AEM提供兩個強大的API。

* GraphQL API可讓您建立存取和傳送內容片段的請求。
* 資產REST API可讓您建立及修改內容片段（和其他資產）。

您將在後續的AEM無頭歷程中，了解這些API及如何使用。 或參閱 [其他資源](#additional-resources) 以取得其他檔案。

## 無頭整合級別 {#integration-levels}

AEM支援CMS的完整無頭模式和傳統的完整堆棧模式或有頭模式。 不過，AEM不僅提供這兩種獨家選擇，還能支援結合兩者優點的混合模型，為無頭專案提供獨特的彈性。

為了確保您了解無頭概念，此AEM無頭開發人員歷程著重於純粹的無頭模型，以便您盡快上手並執行，而不需在AEM中進行編碼。

不過，一旦了解AEM無頭功能，您應注意您所面臨的其他混合可能性。 這些案例在下面列出，供您了解。 在歷程結束時，您將會更詳細地了解這些概念，以備您的專案需要這種彈性時使用。

### 您已有無頭內容的外部使用，例如單頁應用程式(SPA)。 {#already-have-a-spa}

假設您的基本需求至少是要從AEM將內容傳送至現有的外部服務。

#### 第1級：內容片段整合 — 傳統無頭模型 {#level-1}

此整合層級為傳統無周邊模式，可讓內容作者在AEM中建立內容，並透過GraphQL無邊向任何數量的外部服務提供內容，或透過Assets API從外部服務編輯內容。 AEM中不需要編碼。

在此模型中，AEM僅用於使用AEM內容片段來建立和提供內容。 轉譯以及與內容的互動會委派給耗用的外部應用程式，通常是單頁應用程式(SPA)。

#### 第2層：將SPA內嵌於AEM — 混合模型 {#level-2}

此整合層級以第一層為基礎，但也允許將外部應用程式(SPA)內嵌於AEM中，讓內容作者可以在AEM內外部應用程式的內容中檢視內容。 此應用程式也可支援在AEM內有限編輯外部應用程式。

此層級的優點在於，讓內容作者能以強大的方式，在AEM中靈活地製作內容，其內容會與內嵌的外部SPA呈現在內容中，同時仍無謂地傳送內容。

#### 第3層：AEM — 混合模型中的內嵌和完全啟用SPA {#level-3}

此整合層級可建置在第二層，方法是讓外部SPA中的大部分內容都可在AEM中編輯。

### 您尚未有無頭內容的外部使用者，例如單頁應用程式(SPA)。 {#do-not-have-a-spa}

如果您的目標是建立新的SPA，無謂地從AEM中取用內容，您可以使用內容片段等功能來管理無頭內容，也可以使用AEM SPA編輯器架構建立SPA。

使用SPA編輯器時，SPA不僅會取用AEM的內容，而且內容作者也可在AEM內完全編輯，讓您既有無頭傳送的彈性，也有在AEM內進行內容編輯的彈性。

## 需求與必要條件 {#requirements-prerequisites}

開始無頭式AEM專案前，有許多需求。

### 知識 {#knowledge}

* GraphQL
* 使用React或React架構建立SPA的開發Angular
* 基本AEM技能建立內容片段及使用編輯器

### 工具 {#tools}

* 測試部署專案的沙箱存取權
* 用於資料建模和測試的本地開發實例
* 您無頭式AEM內容的現有外部SPA或其他消費者

## 定義專案 {#defining-your-project}

對於任何成功的項目，不僅要明確界定項目的要求，還要明確其角色和責任。

### 範圍 {#scope}

必須明確界定項目範圍。 範圍會通知接受標準，並可讓您建立已完成的定義。

您必須問的第一個問題是「我要用AEM Headless達成什麼？」 一般而言，答案應該是，您擁有或將來擁有的體驗應用程式，是您使用自己的開發工具(而非使用AEM)建立的。 此體驗應用程式可以是行動應用程式、網站或任何其他面向客戶的體驗應用程式。 使用AEM Headless的目標，是透過在AEM中建立、儲存及管理的內容，為體驗應用程式提供動態API，這些最新API會呼叫AEM Headless，以直接從體驗應用程式擷取內容，甚至是完整的CRUD內容。 如果這不是你想做的，你可能想 [返回AEM檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant) 找出更符合您想要完成之目標的區段。

### 角色與責任 {#roles-responsibilities}

任何個別專案的角色各有不同，但在AEM無頭式開發內容中需考量的重要角色為：

* [管理員](#administrator)
* [內容作者](#content-author)
* [內容架構師](#content-architect)
* [開發人員](#developer)

#### 管理員 {#administrator}

管理員負責系統的基本設定和配置。 例如，管理員會在Adobe使用者管理系統內設定您的組織，請參考Identity Management系統(IMS)。 當Adobe在IMS內建立組織後，管理員是組織中第一個從Adobe收到電子郵件邀請的使用者。 管理員可登入IMS並新增其他角色的使用者。

管理員設定使用者後，即可授予他們存取所有AEM資源的權限，以完成使用者作為貢獻者，使用AEM Headless傳遞體驗應用程式。

管理員應為設定AEM並準備執行階段環境以啟用的使用者 [內容作者](#content-author) 建立和更新內容 [開發人員](#developer) 使用API來擷取或修改其體驗應用程式的內容。

#### 內容作者 {#content-author}

內容作者可建立及管理AEM無端傳送的內容。 內容作者可使用內容片段和Assets Console等AEM功能來管理其內容。

內容作者應謹記下列最佳實務。

#### 翻譯計畫 {#translation}

在項目開始時計畫翻譯。 將「翻譯專員」視為一個單獨的角色，其職責是定義哪些內容應翻譯、哪些內容不應翻譯，以及哪些翻譯內容可能由地區或地方內容製作者修改。

建立您需要的內容翻譯計畫。

* 您是否需要不同的語言或語言才能針對地區具體情況採用？
* 您是否需要針對不同地區設定不同的多媒體內容（例如影像或影片）?

請清楚了解您的內容更新工作流程。 系統必須支援哪個核准程式？ 是否可運用AEM工作流程來自動化此程式？

請注意，您的 [內容階層](#content-hierarchy) 可用來讓翻譯更輕鬆。

請參閱 [其他資源](#additional-resources) 區段，取得AEM工作流程和翻譯工具的其他檔案，包括AEM Headless Translation Journey的連結。

##### 運用內容階層 {#content-hierarchy}

資料夾階層可解決關於內容管理的兩個主要問題：

* [翻譯](#translation) - AEM借由維護地區設定特定資料夾中的內容副本來管理內容翻譯。
* 組織 — 資料夾可用來定義支援翻譯需求所需的內容階層，以及邏輯上管理內容片段。

AEM可提供彈性的內容結構，且階層可任意大小。 但是，必須認識到，資料夾結構中的任何更改都可能對現有查詢產生意外的後果 [仰賴內容路徑。](#developer) 因此，事先清楚說明的清晰階層架構對內容作者有幫助。

資料夾也可以限制為僅允許特定類型的內容（根據內容片段模型）。 建議一律明確指定階層中所有資料夾允許使用的模型。 指定指定資料夾的允許內容：

* 防止內容作者編寫不屬於資料夾的內容。
* 透過篩選資料夾中允許的內容類型，來最佳化內容建立程式，在建立期間只顯示有效的內容類型。

透過建立適當的內容結構，可更輕鬆地跨管道協調無頭式內容製作，以最大化內容重複使用。 跨多個通道利用內容可大大提高內容生產效率和更改管理。

##### 建立良好的命名慣例 {#naming-conventions}

內容片段名稱必須為內容作者的描述性名稱。 AEM會透明地處理逸出和/或截斷在存放庫層級使用的ID名稱。 因此，內容作者提供的邏輯名稱應一律可讀，並代表內容。

* 名稱錯誤： `cta_btn_1`
* 好名字： `Call To Action Button`

請參閱 [其他資源](#additional-resources) 一節，以取得AEM頁面命名慣例的其他檔案。

##### 不要過度擴展內容巢狀 {#content-nesting}

[內容片段](#content-fragments) 用於AEM中以建立無頭式內容。 AEM支援高達十個層級的內容巢狀內容片段。 不過，請務必記住，AEM必須反覆解析父內容片段中定義的每個參照，然後檢查所有同層中是否有任何子參照。 這些操作可以迅速增加，並成為效能問題。

根據一般經驗規則，內容片段參考不應巢狀內嵌超過五個層級。

#### 內容架構師 {#content-architect}

內容架構師會分析必須無條理傳送的資料需求，並定義此資料的結構。 這些結構稱為 [內容片段模型](#content-fragment-models) 在AEM中。 內容片段模型是內容作者建立之內容片段的基礎。

定義內容片段模型時，一個實用的方法是建立對應至使用內容之應用程式的UX元件的模型。

因為內容作者在建立新內容時，會持續與模型互動，將模型與UX對齊有助於他們視覺化產生的數位體驗。 更進一步，您可以將圖示指派給代表UX元素的內容片段模型，讓作者能根據視覺提示直覺選取正確的模型。

#### 開發人員 {#developer}

開發人員負責將在AEM中建立的內容無謂地連結到該內容的消費者，這些內容通常可以是單頁應用程式(SPA)、漸進式網頁應用程式(PWA)、網店或AEM外部的其他服務。

GraphQL是AEM與無周邊內容使用者之間的「膠水」。 GraphQL是用於查詢AEM以獲取必要內容的語言。

開發人員在規劃查詢時應謹記一些基本建議：

* 查詢不應依賴固定路徑(`ByPath`)來擷取內容片段。
   * [內容作者可完全控制內容片段階層](#content-hierarchy) 並可以做出會破壞此查詢的變更。
   * 查詢應改為選擇使用動態查詢參數的內容片段模型參考，以篩選結果以產生所需的裝載。
* 為獲得最佳查詢效能，請一律在AEM中使用持續查詢。 這些內容稍後會在歷程中討論。
* GraphQL是遵循以下格言的聲明性：「請求您確切需要的內容，並確實獲得這些內容。」 這表示在建立GraphQL查詢時，請一律避免 `select *`-type查詢，您可以在關係資料庫中建立。

若 [典型的使用AEM的無頭式實作，](#level-1) 開發人員不需要AEM的編碼知識。

### 效能需求 {#performance-requirements}

若要讓任何專案成功，在建立任何內容之前，必須考慮效能。

您必須了解使用者/訪客的期望值，並針對這些期望進行設計。 設定服務級別目標(SLO)，並測量它們，以了解您是否符合用戶的期望。

#### 流量模式 {#traffic-patterns}

要了解流量和流量模式，首先收集您過去了解的資訊，然後預測未來幾年的預期增長。 要考慮的一些最重要變數：

* 您預期每小時/每日/月會有多少個API呼叫，而且可能會發生尖峰和季節性？
* 有多少不同的內容作者？
* 您預計同時處理多少個內容作者？
* 內容更新的頻率為何？
* 需要多少個內容模型？
* 需要多少個模型例項？

#### 更新頻率 {#update-frequency}

不同的體驗區段通常有不同的內容更新頻率。 了解這一點對於微調CDN和快取配置非常重要。 這也是 [內容架構師](#content-architects) 來設計代表您內容的模型。 請考慮：

* 某些類型的內容必須在特定時段後過期嗎？
* 是否有特定於用戶的元素因此無法快取？

## 下一步 {#what-is-next}

現在您已完成AEM Headless Developer Journey的這一部分，您應：

* 了解AEM無頭功能的基本概念。
* 了解使用AEM無頭功能的必要條件。
* 請注意AEM無頭整合層級。
* 能夠根據範圍定義專案。

您應繼續進行AEM無頭歷程，繼續檢閱此檔案 [使用AEM無頭式的第一次體驗路徑](path-to-first-experience.md) 您可以在何處了解如何設定必要的工具，以及如何開始考慮在AEM中建立資料模型。

## 其他資源 {#additional-resources}

雖然建議您透過檢閱檔案，繼續進行無頭式開發歷程的下一個階段 [使用AEM無頭式裝置提供第一次體驗的路徑，](path-to-first-experience.md) 以下是一些額外的選用資源，可更深入探討本檔案中提及的一些概念，但您不需要繼續進行無頭歷程。

* [AEM無頭翻譯歷程](/help/journey-headless/translation/overview.md)  — 本檔案歷程可讓您廣泛了解無頭式技術、AEM如何提供無頭式內容，以及如何翻譯內容。
* [AEM無頭Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用這些實作教學課程，探索如何使用各種選項，透過AEM將內容傳遞至無頭端點，並選擇適合您的方式。
* [使用GraphQL API進行無周邊內容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  — 請參閱本課程，概略了解在AEM中實作的GraphQL API。 需要透過AdobeID進行驗證。
* [AEM指南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub專案包含醒目提示AEM GraphQL API的範例應用程式。
* [製作概念](/help/sites-authoring/author.md) - AEM製作環境的技術檔案，包括製作發佈設定的詳細資訊
* [發佈頁面](/help/sites-authoring/publishing-pages.md)  — 在AEM上發佈內容的技術檔案
* [命名慣例](/help/sites-developing/naming-conventions.md) - AEM中頁面命名限制的技術檔案
* [多站點管理員和翻譯](/help/sites-administering/msm-and-translation.md) - AEM強大翻譯功能的技術檔案
* [AEM工作流程](/help/sites-authoring/workflows.md)  — 關於如何在AEM中自動化工作流程的技術檔案
* [內容片段](/help/assets/content-fragments/content-fragments.md)  — 內容片段的技術檔案。
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 內容片段模型的技術檔案。
* [GraphQL技術檔案](https://graphql.org) - GraphQL定義（外部連結）
* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)  — 說明如何建立存取和傳送內容片段的要求的技術檔案
* [資產REST API](/help/assets/assets-api-content-fragments.md)  — 說明如何建立和修改內容片段（和其他資產）的技術檔案
* [持續查詢](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching)  — 關於AEM中持續查詢的技術檔案
* [AEM中的Headful和Headless](/help/sites-developing/headful-headless.md)  — 完整討論AEM中提供的無頭整合層級
