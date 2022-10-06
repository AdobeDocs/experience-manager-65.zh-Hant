---
title: 選用 — 如何使用AEM建立單頁應用程式(SPA)
description: 在此選用的AEM無頭式開發人員歷程延續中，您將了解AEM如何將無頭式傳送與傳統的完整堆疊CMS功能結合，以及如何使用AEM SPA編輯器架構建立可編輯的SPA。
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 7b97bc0ffb0df6641ae71fa36c459f1368052e12
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# 如何使用AEM建立單頁應用程式(SPA) {#create-spa}

在此選用的延續中， [AEM無頭開發者歷程，](overview.md) 您了解AEM如何將無頭式傳送與傳統的完整堆疊CMS功能結合，以及如何使用AEM SPA編輯器架構建立可編輯的SPA，以及整合外部SPA，以視需要啟用編輯功能。

## 迄今為止的故事 {#story-so-far}

此時，您應已完成整個 [AEM Headless Developer Journey](overview.md) 並了解AEM中無頭式傳送的基本概念，包括：

* 無頭式內容傳送與無頭式內容傳送之間的差異。
* AEM無頭功能。
* 如何組織及AEM Headless專案。
* 如何在AEM中建立無頭式內容。
* 如何在AEM中擷取和更新無標題內容。
* 如何與AEM Headless專案同時執行。

因此，您現在要麼已上線使用您的第一個AEM Headless專案，要麼已具備完成該專案所需的所有知識。 恭喜！

那麼，為什麼您要閱讀這個額外的、可選的歷程延續？ 你可能記得 [快速入門](getting-started.md#integration-levels) 我們簡要地討論了AEM如何不僅支援無頭式傳送和傳統的完整堆疊模型，還支援結合兩者優點的混合模型。 雖然這種混合模式不是傳統的無頭模式，但可以為某些項目提供前所未有的靈活性。

本文以您對AEM Headless的了解為基礎，深入探討如何建立您自己的單頁應用程式(SPA)，而這些應用程式實際上可在AEM中編輯。 如此一來，您就可以建立內容，並無頭地傳送至SPA，但SPA在AEM中仍可編輯。

## 目標 {#objective}

本檔案可協助您了解如何使用AEM SPA Editor架構開發單頁應用程式。 閱讀本檔案後，您應：

* 了解SPA編輯器的基本功能。
* 了解針對AEM建立可完全編輯的SPA的需求。
* 了解如何將外部SPA整合至AEM。
* 了解應該或不應該如何實作伺服器端轉譯。

## 需求與必要條件 {#requirements-prerequisites}

開始使用AEM中的SPA之前，有許多需求。

### 知識 {#knowledge}

* 使用React或React架構建立SPA的開發Angular
* 基本AEM技能建立內容片段及使用編輯器
* 請務必檢閱檔案 [AEM中的Headful和Headless](/help/sites-developing/headful-headless.md) 以便了解SPA整合的各種層級。

### 工具 {#tools}

* 測試部署專案的沙箱存取權
* 用於資料建模和測試的本地開發實例
* 現有外部SPA（選用，視選擇的整合模型而定）
* AEM 專案原型

## 什麼是SPA? {#what-is-a-spa}

單頁應用程式(SPA)與傳統頁面不同，前者是在用戶端轉譯，主要是Javascript導向，需仰賴Ajax呼叫來載入資料並動態更新頁面。 根據使用者與頁面的互動，大部分或所有內容在單一頁面載入中會擷取一次，並視需要以非同步方式載入其他資源。

這可減少頁面重新整理的需求，並為使用者呈現流暢、快速的體驗，且感覺更像原生應用程式體驗。

AEM SPA編輯器可讓前端開發人員建立可整合至AEM網站的SPA，讓內容作者可像編輯任何其他AEM內容一樣輕鬆編輯SPA內容。

## 為什麼是SPA? {#why-spa}

SPA更像原生應用程式，更加快速、流暢，不僅對網頁的訪客，而且由於SPA的運作方式，對行銷人員和開發人員而言，都成為極具吸引力的體驗。

如需SPA的完整說明及使用原因，請參閱 [其他資源](#additional-resources) 區段，取得更多內部檔案的連結。

## AEM如何處理SPA

在AEM上開發單頁應用程式時，會假設前端開發人員在建立SPA時遵守標準最佳實務。 如果您是前端開發人員，請遵循這些一般最佳實務以及幾項AEM專屬原則，您的SPA將可搭配AEM及其內容製作功能運作。

* **便攜性**  — 如同任何元件，SPA元件應盡可能攜帶。 SPA應使用可移植且可重複使用的元件來建立。
* **AEM驅動器站點結構**  — 前端開發人員建立元件並擁有其內部結構，但需仰賴AEM來定義網站的內容結構。
* **動態演算**  — 所有呈現應為動態。
* **動態路由** - SPA負責路由，AEM會監聽路由並據此擷取。 任何路由都應是動態的。

如需AEM如何處理SPA的完整說明，請參閱 [其他資源](#additional-resources) 區段，取得更多內部檔案的連結。

## AEM SPA編輯器 {#aem-spa-editor}

使用通用SPA架構(例如React和Angular)建置的網站會透過動態JSON載入其內容，不提供AEM頁面編輯器必須的HTML結構才能放置編輯控制項。

若要啟用AEM內的SPA編輯功能，需要SPA的JSON輸出與AEM存放庫中的內容模型之間的對應，才能儲存內容的變更。

AEM中的SPA支援導入了精簡JS層，當載入頁面編輯器時，此層會與SPA JS程式碼互動，以便傳送事件，並啟用編輯控制項的位置以允許內容內編輯。 此功能以「內容服務API端點」概念為基礎，因為SPA的內容需透過「內容服務」載入。

如需AEM SPA編輯器的完整說明，請參閱 [其他資源](#additional-resources) 區段，取得更多內部檔案的連結。

## 調整現有SPA {#existing-spas}

如果您已有SPA,AEM支援將其內嵌至AEM，讓內容作者可在AEM編輯器中看到它。 在使用內容片段的最終應用程式內容中，若要檢視這些片段所建立的內容，這個功能會相當實用。

此外，只要進行小幅變更，您就可以在AEM編輯器中對外部SPA啟用特定編輯功能。

RemotePage元件允許在AEM中轉譯外部SPA。

如需如何讓外部SPA在AEM中可編輯的完整說明，請參閱 [其他資源](#additional-resources) 區段，取得更多內部檔案的連結。

## 下一步 {#what-is-next}

若要開始開發自己的SPA for AEM，請檢閱下列檔案：

* [SPA WKND教學課程](/help/sites-developing/spa-wknd.md)
* [React快速入門](/help/sites-developing/spa-getting-started-react.md)
* [開始使用Angular](/help/sites-developing/spa-getting-started-angular.md)

如果您需要調整現有SPA以在AEM中使用，請檢閱下列檔案：

* [RemotePage元件](/help/sites-developing/spa-remote-page.md)
* [在AEM中編輯外部SPA](/help/sites-developing/spa-edit-external.md)

請參閱下方的 [其他資源](#additional-resources) 這可讓您在AEM中深入探討SPA主題。

## 其他資源 {#additional-resources}

以下是一些額外資源，可深入探討本檔案中提及的一些概念。

* [AEM中的Headful和Headless](/help/sites-developing/headful-headless.md)  — 說明AEM中提供的不同傳送模型
* [SPA簡介和逐步說明。](/help/sites-developing/spa-walkthrough.md) - AEM中的SPA簡介
* [開發SPA for AEM](/help/sites-developing/spa-architecture.md)  — 如何開發SPA for AEM的指引
* [SPA編輯器概述](/help/sites-developing/spa-overview.md) - SPA編輯器運作方式的詳細資訊
* [伺服器端轉譯](/help/sites-developing/spa-ssr.md)  — 如何為AEM SPA配置SSR
* [SPA參考檔案](/help/sites-developing/spa-reference-materials.md) - JavaScript API參考和連結至開放原始碼AEM SPA GitHub專案
* [內容片段](/help/assets/content-fragments/content-fragments.md)  — 如何建立內容片段
* [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - Maven範本，可建立基於最佳實務的簡化Adobe Experience Manager(AEM)專案，作為網站的起點
