---
title: 了解 CMS Headless 開發
description: 在 AEM Headless 開發人員歷程的這一部分中，了解 Headless 技術和使用原因。
exl-id: f0989cea-3102-43cd-976e-9a6b265d9c15
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 90%

---

# 了解 CMS Headless 開發 {#learn-about}

在 [AEM Headless 開發人員歷程](overview.md)的這一部分中，了解 Headless 技術和使用原因。

## 目標 {#objective}

本文件協助您了解 Headless 內容傳遞以及使用它的原因。閱讀本文件後，您應該：

* 了解 Headless 內容傳遞的基本概念和術語
* 了解為何與何時需要 Headless 
* 概略了解 Headless 概念如何使用以及它們是如何相互關聯的

## 全堆疊內容傳遞 {#full-stack}

自從易於使用的大型內容管理系統 (CMS) 興起以來，組織就將其作為管理訊息、品牌和通訊的中心位置。使用 CMS 做為管理體驗的中心點可以提升效率，因為就不需要在各個不同系統重複任務。

![傳統的全堆疊 CMS](assets/full-stack.png)

在全棧疊CMS中，操控內容的所有功能都在CMS中。 系統的功能構成了 CMS 堆疊的不同元件。全堆疊解決方案有很多優點。

* 只需維護一個系統。
* 內容集中管理。
* 系統的所有服務都是整合在內的。
* 內容製作可完美無縫進行。

因此，如果您想加入新管道或支援新類型的體驗，可以將一個 (或多個) 新元件插入到堆疊中，並且只有一個地方可以進行變更。

![將新管道加入到堆疊](assets/adding-channel.png)

隨著堆疊中的其他項目需要調整以適應變更，堆疊中的相依性複雜度很快就會變得明顯。

## 全堆疊傳遞的限制 {#limits}

全堆疊方法本質上會建立一個筒倉，所有體驗都集中在一個系統中。變更或新增筒倉中的一個元件，需要變更其他元件，造成變更作業耗費過多時間和成本。

對於展示系統尤其如此，在傳統設定中，展示系統通常與 CMS 緊密連結。任何新管道通常表示要對展示系統進行更新，這會影響所有其他管道。

![將管道加入到堆疊中，複雜性會隨之增加](assets/presentation-complexity.png)

當您花費更多精力來協調堆疊中所有元件的變更時，這種自然筒倉的局限性就會變得很明顯。

無論平台或接觸點為何，使用者都希望參與，這需要您靈活地提供體驗。這種多管道方法是數位體驗的標準，而全堆疊方法在某些情況下被證明是不夠靈活的。

## Headless 的頭部 {#the-head}

任何系統的頭部通常是該系統的輸出呈現器，通常採 GUI 或其他圖形輸出的形式。

例如，Headless 伺服器就像位於伺服器機房某處的機架中，並且沒有連接顯示器。若要存取它，您必須遠端連接它。在此情況下顯示器是頭部，因為它負責呈現伺服器的輸出。您作為服務的取用者，在遠端連接它時提供自己的頭部 (顯示器)。

當我們談論 Headless CMS 時，CMS 管理內容並繼續將其傳遞給取用者。然而，透過僅將&#x200B;**內容**&#x200B;以標準方式傳遞，Headless CMS 會省略最後輸出呈現作業，將內容的&#x200B;**展示**&#x200B;作業留給取用內容的服務執行。

![ Headless CMS](assets/headless-cms.png)

取用內容的服務，無論是 AR 體驗、網路商店、行動體驗、漸進式網頁應用程式 (PWA) 等，都從 Headless CMS 取用內容並提供自己的呈現操作。它們負責為您的內容提供自己的頭。

省略頭可消除複雜性來簡化 CMS。這樣做也會將呈現內容的責任轉移到實際需要內容並且通常更適合執行呈現的服務。

## 分離 {#decoupling}

透過公開一組強大且靈活的應用程式開發介面 (API)，您的所有體驗都可以利用這些 API，從而實現 Headless 傳遞。API 作為服務之間的共同語言，透過標準化內容傳遞在內容層級將服務繫結在一起，但允許它們靈活地實作自己的解決方案。

Headless 是將內容與其展示分離的範例。或是更一般的說法，就是將前端與服務堆疊的後端分離。在 Headless 設定中，展示系統 (頭) 與內容管理 (尾) 分離。兩者僅透過 API 呼叫進行互動。

這種分離表示每個取用內容的服務 (前端) 都可以根據透過 API 傳遞的相同內容建置自己的體驗，從而確保內容可重複使用和保持一致。然後，取用內容的服務可以實作自己的展示系統，從而使內容管理堆疊 (後端) 可以輕鬆地水平擴展。

## 技術基礎 {#technology}

Headless 方法可讓您建置技術堆疊，可以輕鬆快速地適應未來的數位體驗需求。

過去 CMS 的 API 通常是以 REST 為基礎。表現層狀態轉換 (REST) 以無狀態方式將資源作為文字提供。這允許使用一組預先定義的操作來讀取和修改資源。透過確保內容的無狀態表示，REST 允許 Web 上服務之間的良好交互操作性。

仍然需要強大的 REST API。然而，REST 要求可能龐大且冗長。如果您有多個取用者對您的所有管道進行 REST 呼叫，那麼會更為冗長且效能可能會受到影響。

Headless 內容傳遞通常使用 GraphQL API。GraphQL 允許類似的無狀態傳輸，但允許更有目標的查詢，減少所需查詢的總數，並提高效能。經常看到混合使用 REST 和 GraphQL 的解決方案，本質上是選擇最適合手頭工作的工具。

無論您選擇哪個 API，定義基於通用 API 的 Headless 系統，就可以使用最新的瀏覽器和其他網頁技術，例如漸進式網頁應用程式 (PWA)。API 建立了一個易於擴展和適應的標準介面。

通常，內容是在用戶端呈現。這通常表示有人在行動裝置上呼叫您的內容，您的CMS傳送內容，然後行動裝置（使用者端）負責轉譯您提供的內容。 如果裝置陳舊或速度慢，您的數位體驗同樣會很慢。

將內容與展示分離代表可以更好地控制此類用戶端效能問題。伺服器端呈現 (SSR) 將呈現內容的責任從用戶端瀏覽器轉移到伺服器。這使內容提供者能夠在需要時為對象提供一定程度的效能。

## 組織的挑戰 {#organization}

Headless 為傳遞數位體驗帶來了靈活性。但這種靈活性本身也帶來挑戰。

擁有許多不同的管道代表們每個管道都有自己的展示系統。儘管它們都透過相同的 API 取用相同的內容，但由於展示方式不同，體驗可能會有所不同。必須加以考量和關注以確保客戶體驗的一致性。

透過實施精心設計的系統、共用模式庫、利用可重複使用的設計元件以及已建立的開放式用戶端框架，可以確保一致的體驗，但這必須進行計畫。

## 未來是 Headless，未來就是現在 {#future}

數位體驗將繼續定義品牌與客戶互動的方式。 Headless 設計令人興奮的地方在於它給予我們足夠的靈活性來回應不斷進化的客戶期望。

預測未來是不可能的，但 Headless 可以讓您靈活地應對未來帶來的一切。

## AEM 和 Headless {#aem-and-headless}

隨著您繼續完成此開發人員歷程，您將了解 AEM 如何在提供其全堆疊傳遞功能的同時支援 Headless 傳遞。

作為數位體驗管理領域的產業領導者，Adobe 意識到在解決體驗創作者面臨的現實挑戰方面，理想的解決方案很少是二選一的選擇。這就是為什麼 AEM 不僅支援這兩種模型，而且還獨特地允許將兩者無縫結合，藉此融合 Headless 和全堆疊的優勢，以協助您為內容取用者提供最好服務，無論他們身在何處。

此歷程的重點是放在僅 Headless 的內容傳遞模型。然而，一旦您掌握了這些基本知識，您就可以進一步探索如何使用這兩種模型的優勢。

## 下一步 {#what-is-next}

感謝您開始 AEM Headless 歷程！您現已閱讀本文件，應該：

* 了解 Headless 內容傳遞的基本概念和術語。
* 了解為何與何時需要 Headless 。
* 概略了解 Headless 概念如何使用以及它們是如何相互關聯的。

在此基礎上繼續您的AEM Headless歷程，接下來檢閱檔案 [AEM Headless快速入門](getting-started.md) 在這裡，您將瞭解如何設定必要的工具，以及如何開始思考AEM如何進行headless內容傳送及其先決條件。

## 其他資源 {#additional-resources}

我們建議您檢閱檔案，以繼續進行Headless開發歷程的下一部分 [AEM Headless快速入門](getting-started.md)，以下是一些其他可選資源，這些資源對檔案中提到的一些概念進行了更深入的探究，但並非繼續無頭之旅所必需的。

* [AEM as a Headless CMS 簡介](/help/sites-developing/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 利用這些實作教學課程來探索如何運用各種不同方式使用 AEM 將內容傳遞到 Headless 端點，並選擇適合您的方式。
