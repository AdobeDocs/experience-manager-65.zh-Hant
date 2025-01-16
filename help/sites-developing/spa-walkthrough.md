---
title: SPA 簡介和逐步解說
description: 本文章介紹 SPA 的概念，並逐步解說如何使用基本 SPA 應用程式進行編寫，說明它與基礎 AEM SPA 編輯器的關係。
topic-tags: spa
content-type: reference
exl-id: 95990112-2afc-420a-a7c7-9613f40d4c4a
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 65%

---


# SPA 簡介和逐步解說 {#spa-introduction-and-walkthrough}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用 SPA 框架建立網站，而作者則想在 AEM 中為使用這類框架建立網站，順暢地編輯內容。

SPA 編輯器提供了一個全面的解決方案來支援在 AEM 中使用 SPA。本文章逐步解說如何使用基本 SPA 應用程式進行編寫，並說明它與基礎 AEM SPA 編輯器的關係。

{{ue-over-spa}}

## 簡介 {#introduction}

### 文章目標 {#article-objective}

本文章介紹 SPA 的基本概念，然後透過使用簡單 SPA 應用程式來示範基本的內容編輯，逐步引導讀者了解 SPA 編輯器。然後深入探討頁面的結構以及 SPA 應用程式如何與 AEM SPA 編輯器相關及互動。

此簡介和逐步解說的目的是向 AEM 開發人員示範 SPA 為何相關、其一般運作方式、AEM SPA 編輯器如何處理 SPA，以及它與標準 AEM 應用程式有何不同。

## 要求 {#requirements}

逐步解說是以標準 AEM 功能和範例 WKND SPA 專案應用程式為基礎。若要依此逐步解說操作，您必須具備以下項目。

* [AEM 6.5.4或更新版本](/help/release-notes/release-notes.md)
   * 您必須擁有系統的管理員權限。
* [GitHub 提供的範例 WKND SPA 專案應用程式](https://github.com/adobe/aem-guides-wknd-spa)
   * 下載[最新版的React應用程式。](https://github.com/adobe/aem-guides-wknd-spa/releases)其名稱將類似於`wknd-spa-react.all.classic-X.Y.Z-SNAPSHOT.zip`。
   * 下載應用程式的[最新範例影像](https://github.com/adobe/aem-guides-wknd-spa/releases)。 它的名稱類似於`wknd-spa-sample-images-X.Y.Z.zip`。
   * [使用封裝管理員](/help/sites-administering/package-manager.md)安裝封裝，就像在AEM中安裝任何其他封裝一樣。
   * 出於本逐步解說的目的，應用程式不需要使用 Maven 安裝。

>[!CAUTION]
>
>此檔案僅將[WKND Spa Project應用程式](https://github.com/adobe/aem-guides-wknd-spa)用於示範用途。 請勿用於任何專案工作。
>
>任何AEM專案都應該使用[AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，該原型支援使用React或Angular的SPA專案，並使用SPA SDK。

### 什麼是 SPA？ {#what-is-a-spa}

單頁應用程式 (SPA) 與傳統頁面的不同之處在於它是在用戶端呈現並且主要由 JavaScript 驅動，依賴 Ajax 呼叫來載入資料和動態更新頁面。在單頁載入時一次擷取大部分或所有內容，並根據使用者與頁面的互動，視需要非同步載入其他資源。

這減少了頁面重新整理的需要，讓使用者擁有順暢、快速且像是使用原生應用程式的體驗。

AEM SPA 編輯器允許前端開發人員建立可整合到 AEM 網站的 SPA，從而允許內容作者輕鬆編輯 SPA 內容，像編輯任何其他 AEM 內容一樣輕鬆。

### 為什麼是 SPA？ {#why-a-spa}

由於 SPA 的運作本質，SPA 可以更流暢、快速且像是原生應用程式，不僅對網頁訪客而且對行銷人員和開發人員來說都是一種極具吸引力的體驗。

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**位訪客**

* 訪客在與內容互動時希望獲得類似原生的體驗。
* 有明確資料代表頁面生成越快，就越可能發生轉換。

**行銷人員**

* 行銷人員希望提供豐富的、類似原生的體驗，以吸引訪客與內容完全互動。
* 個人化可以使這些體驗更具吸引力。

**開發人員**

* 開發人員希望清楚分開內容和展示之間的考量點。
* 乾淨的分隔讓系統可延伸性更高，並允許獨立的前端開發。

### SPA 如何運作？ {#how-does-a-spa-work}

SPA的主要構想是減少伺服器呼叫和相依性，以將伺服器呼叫造成的延遲降至最低，讓SPA接近原生應用程式的回應速度。

在傳統的循序網頁中，僅載入即時頁面所需的資料。這表示當訪客移至另一個頁面時，將呼叫伺服器以取得額外資源。訪客與頁面上的元素互動時，可能需要額外的呼叫。 由於頁面必須趕上訪客的要求，因此這些多次呼叫可能會讓人產生延滯或延遲的感覺。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

為了提供更具流動性的體驗，其接近訪客從行動原生應用程式中期望的體驗，SPA會在第一次載入時載入訪客的所有必要資料。 雖然這在開始時可能需要較長的時間，但之後就不需要額外呼叫伺服器。

在使用者端轉譯後，頁面元素的反應速度會更快，訪客與頁面的互動也更立即。 系統會非同步呼叫任何可能需要的額外資料，以最大化頁面速度。

>[!NOTE]
>
>如需SPA如何在AEM中運作的技術詳細資訊，請參閱文章[AEM中的SPA快速入門](/help/sites-developing/spa-getting-started-react.md)。
>
>若要進一步瞭解SPA編輯器的設計、架構和技術工作流程，請參閱文章[SPA編輯器概觀](/help/sites-developing/spa-overview.md)。

## SPA 的內容編輯體驗 {#content-editing-experience-with-spa}

當SPA建置為使用AEM SPA編輯器時，內容作者會注意到編輯和建立內容時沒有差異。 可以使用常用的 AEM 功能，作者的工作流程無需變更。

1. 在 AEM 編輯 WKND SPA 專案應用程式。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

   ![步驟1](assets/spa-walkthrough-step-1.png)

1. 選取標題元件，並注意其他元件會出現類似的工具列。 選取&#x200B;**編輯**。

   ![步驟2](assets/spa-walkthrough-step-2.png)

1. 在AEM中正常編輯內容。 變更會持續存在。

   ![步驟3](assets/spa-walkthrough-step-3.png)

   >[!NOTE]
   >
   >如需就地文字編輯器和SPA的詳細資訊，請參閱[SPA編輯器概觀](spa-overview.md#requirements-limitations)。

1. 使用資產瀏覽器將新影像拖放到影像元件中。

   ![步驟4](assets/spa-walkthrough-step-4.png)

1. 變更已保留。

   ![步驟5](assets/spa-walkthrough-step-5.png)

如同任何非SPA應用程式一樣，也支援其他撰寫工具，例如拖放頁面上的其他元件、重新排列元件及修改版面。

>[!NOTE]
>
>SPA 編輯器不會修改應用程式的 DOM。SPA 自行負責 DOM。
>
>若要了解其運作原理，請繼續閱讀本文的下一章節：[SPA 應用程式和 AEM SPA 編輯器](#spa-apps-and-the-aem-spa-editor)。

## SPA 應用程式和 AEM SPA 編輯器 {#spa-apps-and-the-aem-spa-editor}

體驗SPA為一般使用者的行為方式，然後檢查SPA頁面，有助於更清楚瞭解SAP應用程式如何與AEM中的SPA編輯器搭配運作。

### 使用 SPA 應用程式 {#using-an-spa-application}

1. 將 WKND SPA 專案應用程式載入到發佈伺服器，或使用頁面編輯器&#x200B;**頁面資訊**&#x200B;選單的&#x200B;**如發佈時檢視**&#x200B;選項。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![步驟1](assets/spa-walkthrough-step-1-1.png)

   請注意頁面結構，包括導覽至子頁面、氣象Widget和文章。

1. 使用選單導覽到子頁面，可以看到頁面立即載入，無需重新整理。

   ![步驟2](assets/spa-walkthrough-step-1-2.png)

1. 開啟瀏覽器內建的開發人員工具，並在您瀏覽子頁面時監控網路活動。

   ![步驟3](assets/spa-walkthrough-step-1-3.png)

   當您在應用程式中從一個頁面移動到另一個頁面時，流量非常小。該頁面不會重新載入，只會要求新影像。

   SPA 完全在用戶端管理內容和路由。

那麼如果在子頁面間瀏覽時頁面沒有重新載入，它是如何載入？

下一節[載入SPA應用程式](#loading-an-spa-application)深入探討載入SPA的機制，以及如何以同步和非同步方式載入內容。

### 載入 SPA 應用程式 {#loading-an-spa-application}

1. 如果尚未載入，請將 WKND SPA 專案應用程式載入至發佈伺服器，或使用頁面編輯器&#x200B;**頁面資訊**&#x200B;選單的&#x200B;**如發佈時檢視**&#x200B;選項。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![步驟1](assets/spa-walkthrough-step-1-1.png)

1. 使用瀏覽器的內建工具檢視頁面的來源。
1. 來源的內容極為有限。

   * 頁面的內文中沒有任何內容。它主要由樣式表和對各種指令碼 (例如 `clientlib-react.min.js`) 的呼叫所組成。
   * 這些指令碼是此應用程式的主要驅動程式，負責呈現所有內容。

1. 使用瀏覽器的內建工具檢查頁面。查看完全載入之 DOM 的內容。

   ![步驟4](assets/spa-walkthrough-step-1-4.png)

1. 切換至開發人員工具的&#x200B;**網路**&#x200B;標籤，然後重新載入頁面。

   忽略影像要求時，為頁面載入的主要資源為頁面本身、CSS、React JavaScript、其相依性以及該頁面的JSON資料。

   ![步驟5](assets/spa-walkthrough-step-1-5.png)

1. 在新索引標籤中載入 `react.model.json`。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![步驟6](assets/spa-walkthrough-step-1-6.png)

   AEM SPA 編輯器使用 [AEM 內容服務](/help/assets/content-fragments/content-fragments.md)將頁面的全部內容以 JSON 模型傳遞。

   透過實作特定的介面，Sling 模型為 SPA 提供必要的資訊。JSON 資料的傳遞工作向下委派給每個元件 (從頁面到段落到元件等)。

   每個元件會選取要公開的內容以及呈現的方式（使用HTL的伺服器端或使用React的使用者端）。 本文章重點介紹使用 React 進行用戶端呈現。

1. 此模型還可以將頁面群組在一起，以便同步載入，從而減少所需的頁面重新載入次數。

   在 WKND SPA 專案應用程式範例中，`home`、`page-1`、`page-2` 和 `page-3` 頁面是同步載入的，因為訪客通常會造訪所有這些頁面。

   此行為不是強制性的，而且完全可定義的。

   ![步驟7](assets/spa-walkthrough-step-1-7.png)

1. 若要檢視此行為差異，請重新載入頁面並清除開發人員工具的網路活動。 導覽到頁面選單中的 `page-1`，可以看到唯一的網路活動是要求 `page-1` 的影像。`page-1` 本身不需要載入。

   ![步驟8](assets/spa-walkthrough-step-1-8.png)

### 與 SPA 編輯器的互動 {#interaction-with-the-spa-editor}

使用範例WKND SPA Project應用程式，可清楚瞭解應用程式在發佈時的行為和載入方式，使用內容服務進行JSON內容傳送和非同步載入資源。

此外，內容作者可在 AEM 中使用 SPA 編輯器順暢地建立內容。

在下一章節中，我們將探討允許 SPA 編輯器將 SPA 元件與 AEM 元件相關聯並實現此無縫編輯體驗的合約。

1. 在編輯器中載入 WKND SPA 專案應用程式，並切換到&#x200B;**預覽**&#x200B;模式。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. 使用瀏覽器的內建開發人員工具，檢查頁面的內容。使用選取工具，在頁面上選取一個可編輯的元件並查看元素詳細資料。

   元件有新的資料屬性`data-cq-data-path`。

   ![步驟2](assets/spa-walkthrough-step-2-2.png)

   例如

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   此路徑允許擷取和關聯每個元件的編輯情境設定物件。

   這是編輯器將其識別為 SPA 中的可編輯元件所需的唯一標記屬性。根據此屬性，SPA編輯器將決定與元件相關聯的可編輯組態，以便載入正確的框架、工具列等。

   也會新增一些特定類別名稱，用於標記預留位置和資產拖放功能。

   >[!NOTE]
   >
   >這是AEM中伺服器端轉譯頁面的行為變更，其中每個可編輯元件都插入`cq`元素。
   >
   >
   >SPA中的這個方法移除插入自訂元素的必要性，僅依賴其他資料屬性，讓前端開發人員更容易使用標籤。

## 後續步驟 {#next-steps}

現在您已經了解 AEM 中的 SPA 編輯體驗，以及 SPA 與 SPA 編輯器的關係，接下來要更深入地了解如何建立 SPA。

* [AEM中的SPA快速入門](/help/sites-developing/spa-getting-started-react.md)顯示如何建置基本SPA以在AEM中使用SPA編輯器
* [SPA 編輯器概述](/help/sites-developing/spa-overview.md)更深入地介紹 AEM 和 SPA 之間的通訊模型。
* [為 AEM 開發 SPA](/help/sites-developing/spa-architecture.md) 介紹如何讓前端開發人員為 AEM 開發 SPA，以及 SPA 如何與 AEM 架構互動。

