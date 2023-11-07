---
title: 了解 Headless 內容以及如何在 AEM 中翻譯
description: 了解 Headless 概念、它們如何對應到 AEM 以及 AEM 翻譯理論。
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 94%

---

# 了解 Headless 內容以及如何在 AEM 中翻譯 {#learn-about}

了解 Headless 概念、它們如何對應到 AEM 以及 AEM 翻譯理論。

## 目標 {#objective}

本文件可協助您了解 Headless 內容傳遞、AEM 如何支援 Headless 以及如何翻譯這類內容。閱讀本文件後，您應該：

* 了解 Headless 內容傳遞的基本概念。
* 熟悉 AEM 如何支援 Headless 和翻譯。

## 全堆疊內容傳遞 {#full-stack}

自從易於使用的大型內容管理系統 (CMS) 興起以來，組織就將其作為管理訊息、品牌和通訊的中心位置。使用 CMS 做為管理體驗的中心點可以提升效率，因為就不需要在各個不同系統重複任務。

![傳統的全堆疊 CMS](/help/journey-headless/developer/assets/full-stack.png)

在全棧疊CMS中，所有用於操作內容的功能都在CMS中。 系統的功能構成了 CMS 堆疊的不同元件。全堆疊解決方案有很多優點。

* 只需維護一個系統。
* 內容集中管理。
* 系統的所有服務都是整合在內的。
* 內容編寫可完美無縫進行。

因此，如果必須加入新的管道，或需要支援新的體驗類型，可以將一個 (或多個) 新元件插入到堆疊，並且只有一個地方可以進行變更。

![將新管道加入到堆疊](/help/journey-headless/developer/assets/adding-channel.png)

然而，隨著堆疊中的其他項目需要調整以適應變化，堆疊中的相依性複雜度很快就會變得明顯。

## Headless 的頭部 {#the-head}

任何系統的頭部通常是該系統的輸出呈現器，通常採 GUI 或其他圖形輸出的形式。

當我們談論 Headless CMS 時，CMS 管理內容並繼續將其傳遞給取用者。然而，透過僅將&#x200B;**內容**&#x200B;以標準方式傳遞，Headless CMS 會省略最後輸出呈現作業，將內容的&#x200B;**展示**&#x200B;作業留給取用內容的服務執行。

![ Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

消費服務，不論是AR體驗、網路商店、行動體驗、漸進式網頁應用程式(PWA)等，都會從Headless CMS擷取內容，並提供專屬的轉譯。 它們負責為您的內容提供自己的頭。

省略頭可消除複雜性來簡化 CMS。這樣做也會將呈現內容的責任轉移到實際需要內容並且通常更適合執行呈現的服務。

## 在 AEM 翻譯 Headless 內容 {#translating-in-aem}

除了提供強大的工具來以全堆疊方式建立、管理和傳遞傳統網頁外，AEM 還可讓您編寫獨立內容選集並以 Headless 方式提供該內容。

AEM 的強大功能使其能夠以 Headless 方式、全堆疊方式或同時以兩種模式傳遞內容。對於翻譯專家來說，同一套翻譯工具可以套用於兩種類型的內容，為您提供統一的內容翻譯方法。

在接下來的歷程中，您將了解有關 AEM 如何翻譯內容的詳細資訊，其大致概念很簡單：

1. 透過設定整合框架來定義對翻譯服務的連接。
1. 使用翻譯規則定義應翻譯的內容。
1. 建立翻譯專案以獲取內容，並傳送到翻譯服務，然後接收結果。
1. 審查和發佈已翻譯內容。

## 下一步 {#what-is-next}

感謝您開始進行 AEM Headless 翻譯歷程！閱讀了本文件後，您應該：

* 了解 Headless 內容傳遞的基本概念。
* 熟悉 AEM 如何支援 Headless 和翻譯。

以這些知識為基礎，接下來查看文件[AEM Headless 翻譯快速入門](getting-started.md)以繼續您的 AEM Headless 翻譯歷程，您將在此文件大致了解 AEM 如何管理 Headless 內容以及它的翻譯工具。

## 其他資源 {#additional-resources}

雖然建議您查閱文件[AEM Headless 翻譯快速入門](getting-started.md)來繼續 Headless 翻譯歷程的下個部分，以下也有一些其他選擇性資源，在深入探究本文件提到的一些概念，但不是繼續 Headless 歷程的必要條件。

* [MSM 和翻譯](/help/sites-administering/msm-and-translation.md) - 詳細說明 AEM 多網站管理員以及它如何與其翻譯工具一起工作
* [AEM as a Headless CMS 簡介](/help/sites-developing/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
