---
title: AEM無頭式內容架構者歷程
description: 介紹Adobe Experience Manager強大、靈活、無頭的功能，以及如何為專案建立內容模型。
exl-id: 49ba0d6d-dde4-42e2-92fd-c7655c0eebc0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# 使用AEM建立無頭的內容模型 — 簡介 {#architect-headless-introduction}

在 [AEM無頭式內容架構者歷程](overview.md)，您可以了解透過Adobe Experience Manager(AEM)了解無頭式內容傳送內容模型所需的（基本）概念和術語。

本檔案可協助您了解無頭式內容傳送、AEM如何支援無頭式內容，以及如何針對無頭式內容建立內容模型。 閱讀後，您應：

* 了解無頭式內容傳送的基本概念。
* 請熟悉AEM如何支援無頭和內容模型。

## 目標 {#objective}

* **對象**:入門者
* **目標**:介紹與無頭內容建模相關的概念和術語。

## 完整堆疊內容傳送 {#full-stack}

自易用、大規模的內容管理系統(CMS)興起以來，企業一直將它們作為管理報文傳送、品牌推廣和通信的中心位置。 將CMS作為管理體驗的中心點，可消除在不同系統中複製任務的需求，進而提高效率。

![傳統的全堆棧CMS。](/help/journey-headless/developer/assets/full-stack.png)

在全堆棧CMS中，用於操作內容的所有功能都在CMS中。 系統的功能構成了CMS堆棧的不同元件。 該全棧解決方案具有許多優點。

* 有一個系統要維護。
* 內容是集中管理的。
* 系統的所有服務均已整合。
* 內容製作順暢。

因此，如果需要新增管道或需要支援新體驗類型，可以將一（或多個）新元件插入堆疊中，而且只有一個位置可進行變更。

![將新通道新增至堆疊](/help/journey-headless/developer/assets/adding-channel.png)

但是，由於堆棧中的其他項目需要調整以適應更改，因此堆棧內的依賴項的複雜性很快變得明顯。

## 無頭的頭 {#the-head}

任何系統的頭通常是該系統的輸出渲染器，通常以GUI或其它圖形輸出的形式。

當我們討論無頭式CMS時， CMS會管理內容並繼續將內容提供給消費者。 不過，若只傳送 **內容** 無頭式CMS以標準化的方式省略了最終輸出呈現，而 **簡報** 內容到消費服務。

![無頭式CMS](/help/journey-headless/developer/assets/headless-cms.png)

無論是AR體驗、網站商店、行動體驗、漸進式網頁應用程式(PWA)等等，使用的服務都會從無頭式CMS接收內容，並提供自己的轉譯。 他們負責為您的內容提供自己的頭腦。

省略頭部可移除複雜性，簡化CMS。 這麼做也會將內容呈現的責任轉移到實際需要內容且通常更適合這類呈現的服務。

## 內容模型 {#content-modeling}

內容模型（也稱為資料模型）是您的專業，因此在為無頭建模時需要考慮哪些事項？

為了讓無頭應用程式能夠訪問您的內容並執行某些操作，內容確實需要有一個預定義的結構。 你的內容可以自由形式，但它會創造生活 *very* 應用程式複雜。

對於AEM，您身為內容架構師，將執行內容模型以設計一系列 **內容片段模型**. 這些定義內容作者建立 **內容片段** 保存內容的。

### 存取內容 {#access-content}

這更像是一個開發細節 — 但也許你會感興趣，只是為了完成這個故事。

一旦您建立了內容片段模型，且作者已使用這些模型產生內容後，無頭式應用程式就需要存取此內容。

Adobe Experience Manager(AEM)可以使用AEM GraphQL API選擇性地存取內容片段，以僅傳回所需的內容。 使用API，開發人員可以制定用於選擇特定內容的查詢。此選擇過程基於 *您的* 內容片段模型。

這表示您的專案可實現無頭式傳送結構化內容，以便用於您的應用程式。

## 下一步 {#whats-next}

既然您已經學過概念和術語，下一步就是 [了解使用內容片段模型建立模型的基本知識](basics.md).

## 其他資源 {#additional-resources}

* AEM Headless Developer Journey
   * [了解CMS無頭開發](/help/journey-headless/developer/learn-about.md)
   * [了解如何建立內容模型](/help/journey-headless/developer/model-your-content.md)
