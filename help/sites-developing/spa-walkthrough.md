---
title: SPA簡介與逐步說明
seo-title: SPA簡介與逐步說明
description: 本文介紹SPA的概念，並逐步說明如何使用基本的SPA應用程式來製作內容，並說明它與基礎的AEM SPA編輯器的關係。
seo-description: 本文介紹SPA的概念，並逐步說明如何使用基本的SPA應用程式來製作內容，並說明它與基礎的AEM SPA編輯器的關係。
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA簡介與逐步說明{#spa-introduction-and-walkthrough}

單頁應用程式(SPA)可為網站使用者提供引人入勝的體驗。 開發人員希望能夠使用SPA架構建立網站，而作者則想在AEM中順暢地編輯內容，以供使用此類架構建立的網站使用。

SPA Editor提供完整的解決方案，以支援AEM中的SPA。 本文逐步說明如何使用基本的SPA應用程式來製作內容，並說明它與基礎的AEM SPA編輯器有何關聯。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 簡介 {#introduction}

### 文章目標 {#article-objective}

介紹了SPA的基本概念，並通過簡單的SPA應用程式演示了SPA編輯器的基本內容編輯過程。 接著深入探討頁面的建構，以及SPA應用程式與AEM SPA編輯器的關聯與互動方式。

本簡介和逐步說明的目的，在於向AEM開發人員示範SPA的相關性、SPA的一般運作方式、AEM SPA編輯器如何處理SPA，以及它與標準AEM應用程式有何不同。

此逐步解說以標準AEM功能和範例We.Retail Journal應用程式為基礎。 必須符合下列要求：

* [AEM 6.4版（含Service Pack 2或更新版本）
   ](/help/release-notes/sp-release-notes.md)
* [請在此處安裝GitHub上提供的範例We.Retail Journal應用程式。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

### 什麼是SPA? {#what-is-a-spa}

單頁應用程式(SPA)與傳統頁面不同，它是由用戶端轉譯，主要是Javascript導向，依賴Ajax呼叫來載入資料並動態更新頁面。 大部分或所有內容在單一頁面載入時都會擷取一次，並根據使用者與頁面的互動，視需要以非同步方式載入其他資源。

這可降低頁面重新整理的需求，並為使用者呈現順暢、快速且更像原生應用程式體驗的體驗。

AEM SPA編輯器可讓前端開發人員建立可整合至AEM網站的SPA，讓內容製作者編輯SPA內容就像編輯其他AEM內容一樣輕鬆。

### 為什麼選擇SPA? {#why-a-spa}

SPA就像原生應用程式，不但對網頁的訪客，而且由於SPA的運作方式，對行銷人員和開發人員而言，都是極具吸引力的體驗。

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**訪客**

* 訪客在與內容互動時，需要類似原生的體驗。
* 有清楚的資料顯示，頁面越快，轉換的可能性就越大。

**行銷人員**

* 行銷人員想要提供豐富、原生的體驗，以吸引訪客充份參與內容。
* 個人化可讓這些體驗更吸引人。

**開發人員**

* 開發人員希望將內容與簡報之間的顧慮完全分開。
* 清潔分離使系統更具可擴充性，並允許獨立的前端開發。

### SPA如何運作？ {#how-does-a-spa-work}

SPA的主要思想是減少對伺服器的呼叫和依賴，以將伺服器呼叫所造成的延遲降至最低，讓SPA接近原生應用程式的回應速度。

在傳統的循序網頁中，只會載入立即頁面所需的資料。 這表示當訪客移至另一個頁面時，會呼叫伺服器以取得其他資源。 當訪客與頁面上的元素互動時，可能需要額外呼叫。 這些多次呼叫會產生延遲或延遲感，因為頁面必須趕上訪客的要求。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

為了提供更流暢的體驗，SPA會在第一次載入時載入訪客的所有必要資料，以接近訪客對行動裝置、原生應用程式的期望。 雖然這一步可能需要稍長時間，但卻不需要額外的伺服器呼叫。

透過在用戶端上演算，頁面元素的反應更快，而訪客與頁面的互動也會立即生效。 可能需要的任何額外資料都會以非同步方式呼叫，以最大化頁面速度。

>[!NOTE]
>
>如需SPA在AEM中運作的技術詳細資訊，請參閱「AEM中 [SPA快速入門」文章](/help/sites-developing/spa-getting-started-react.md)。
>
>如需詳細瞭解SPA編輯器的設計、架構和技術工作流程，請參閱 [SPA編輯器概觀](/help/sites-developing/spa-overview.md)。

## SPA的內容編輯體驗 {#content-editing-experience-with-spa}

當建立SPA以運用AEM SPA編輯器時，內容作者在編輯和建立內容時不會察覺任何差異。 共同的AEM功能可供使用，而且不需要變更作者的工作流程。

>[!NOTE]
>
>此逐步解說以標準AEM功能和範例We.Retail Journal應用程式為基礎。 必須符合下列要求：
>
>* [AEM 6.4版（含Service Pack 2）](/help/release-notes/sp-release-notes.md)
>* [請在此處安裝GitHub上提供的範例We.Retail Journal應用程式。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)
>



1. 在AEM中編輯We.Retail Journal應用程式。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. 選取標題元件，並注意工具列會像其他元件一樣顯示。 選擇 **編輯**。

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. 在AEM中編輯內容時，請注意這些變更會持續存在。

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

1. 使用「資產瀏覽器」將新影像拖放至影像元件。

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. 此變更會持續存在。

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

其他製作工具（例如在頁面上拖放其他元件、重新排列元件以及修改版面）都支援，就像任何非SPA應用程式一樣。

>[!NOTE]
>
>SPA編輯器不會修改應用程式的DOM。 SPA本身負責DOM。
>
>若要瞭解其運作方式，請繼續閱讀本文章「 [SPA應用程式」和「AEM SPA編輯器」的下一節](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)。

## SPA應用程式與AEM SPA編輯器 {#spa-apps-and-the-aem-spa-editor}

體驗SPA對一般使用者的運作方式，然後檢查SPA頁面，有助於進一步瞭解SAP應用程式如何與AEM中的SPA編輯器搭配運作。

### 使用SPA應用程式 {#using-an-spa-application}

1. 在發佈伺服器上或使用頁面編輯器中的「頁面資訊」選單中的「檢視為已發佈 **」選項，載****** 入We.Retail Journal應用程式。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   請注意頁面結構，包括子頁面導覽、氣象工具集和文章。

1. 使用功能表導覽至子頁面，並查看頁面會立即載入，而不需重新整理。

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. 當您導覽子頁面時，開啟瀏覽器的內建開發人員工具並監控網路活動。

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   當您在應用程式中從頁面移至頁面時，流量很少。 不會重新載入頁面，只會要求新影像。

   SPA完全在用戶端管理內容和路由。

因此，如果頁面在子頁面導覽時未重新載入，該頁面的載入方式為何？

下一節「載 [](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)入SPA應用程式」深入探討載入SPA的機制，以及如何同步和非同步載入內容。

### 載入SPA應用程式 {#loading-an-spa-application}

1. 如果尚未載入，請在發佈伺服器上載入We.Retail Journal應用程式，或使用頁面編輯器中「頁面資訊」選單的「檢視為已發佈 ******** 」選項來載入。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. 使用瀏覽器的內建工具來檢視頁面來源。
1. 請注意，來源的內容非常有限。

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   頁面的內文中沒有任何內容。 它主要由樣式表和對React指令碼的調用組成 `we-retail-journal-react.js`。

   此React指令碼是此應用程式的主要驅動程式，負責轉譯所有內容。

1. 使用瀏覽器的內建工具來檢查頁面。 檢視已完全載入的DOM內容。

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. 切換到「檢查器」中的「網路」頁籤並重新載入該頁。

   忽略影像要求時，請注意，載入頁面的主要資源是頁面本身、CSS、React Javascript、其相依性，以及頁面的JSON資料。

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. 在新標 `react.model.json` 簽中載入。

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA編輯器運用 [AEM Content Services](/help/assets/content-fragments.md) ，以JSON模型的形式提供頁面的完整內容。

   透過實施特定介面，Sling Models提供SPA所需的資訊。 JSON資料的傳送會下放至每個元件（從頁面、段落、到元件等）。

   每個元件都會選擇它公開的內容及呈現方式（伺服器端與HTL或用戶端與React）。 當然，本文著重於使用React進行用戶端轉換。

1. 模型也可以將頁面群組在一起，以便同步載入，以減少所需的頁面重新載入次數。

   在We.Retail Journal的範例中，由於訪客通常會 `home`瀏覽所有 `blog`這 `aboutus` 些頁面，因此會同步載入、和頁面。 不過， `weather` 頁面會以非同步方式載入，因為訪客不太可能造訪。

   此行為並非強制性，且完全可定義。

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. 要查看此行為差異，請重新載入頁面並清除檢查器的網路活動。 導覽至頁面功能表中的部落格和我們的頁面，並查看沒有報告任何網路活動。

   導覽至天氣頁面，並查看該頁面 `weather.model.json` 的非同步呼叫。

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### 與SPA編輯器互動 {#interaction-with-the-spa-editor}

使用範例We.Retail Journal應用程式，您就可清楚看出應用程式的運作方式和發佈時的載入方式，並運用內容服務來傳送JSON內容以及非同步載入資源。

此外，對於內容作者，使用SPA編輯器建立內容在AEM中十分順暢。

在下節中，我們將探索讓SPA編輯器將SPA中的元件與AEM元件建立關聯的合約，並獲得順暢的編輯體驗。

1. 在編輯器中載入We.Retail Journal應用程式並切換到「預 **覽** 」模式。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. 使用瀏覽器的內建開發人員工具，檢查頁面內容。 使用選取工具，在頁面上選取可編輯的元件並檢視元素詳細資訊。

   請注意，元件有新的資料屬性 `data-cq-data-path`。

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   例如

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   此路徑允許檢索和關聯每個元件的編輯上下文配置對象。

   這是編輯器將其識別為SPA中可編輯的元件所需的唯一標籤屬性。 根據此屬性，SPA編輯器將確定與元件關聯的可編輯配置，以便正確的框架、工具欄等。 已載入。

   此外，還新增了某些特定類別名稱，以標籤預留位置和資產拖放功能。

   >[!NOTE]
   >
   >這是AEM中伺服器端轉譯頁面的行為變更，其中每個可編輯元件都 `cq` 會插入元素。
   >
   >
   >SPA中的此方法不需要插入自訂元素，只需額外的資料屬性，讓前端開發人員更容易進行標籤。

## 後續步驟 {#next-steps}

現在，您已瞭解AEM的SPA編輯體驗，以及SPA與SPA編輯器的關係，深入瞭解如何建立SPA。

* [AEM中的SPA快速入門(Getting Started with SPAs in AEM](/help/sites-developing/spa-getting-started-react.md) )說明如何建立基本SPA來搭配AEM中的SPA編輯器運作
* [SPA編輯器概觀](/help/sites-developing/spa-overview.md) (SPA Editor Overview)深入探討AEM與SPA之間的通訊模型。
* [針對AEM開發SPA](/help/sites-developing/spa-architecture.md) ，說明如何吸引前端開發人員來開發AEM的SPA，以及SPA如何與AEM的架構互動。
