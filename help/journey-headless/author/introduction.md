---
title: AEM Headless 內容作者歷程
description: 介紹Adobe Experience Manager強大、彈性、無頭的功能，以及如何為專案製作內容。
exl-id: 39d2218a-4f11-459d-8514-cfd312246be5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 91%

---

# 使用 AEM 編寫 Headless - 簡介 {#author-headless-introduction}

在 [AEM無頭內容製作歷程](overview.md)，您可以了解透過Adobe Experience Manager(AEM)了解製作無頭式內容所需內容的必要（基本）概念和術語。

## 目標 {#objective}

* **對象**：初學者
* **Objective**：介紹與 Headless 編寫相關的概念和術語。

## 內容管理系統 (CMS) {#content-management-system}

什麼是內容管理系統？

內容管理系統 (CMS) 顧名思義，是一種用於管理內容的電腦系統。這有點籠統，所以更準確地說，它 (通常) 用於管理您希望在您網站上提供的內容。

## Headless CMS {#headless-cms}

Headless 是一個術語，用於描述能夠有效地將內容與內容在 Web 顯示方式分離的系統。

傳統上，您會在 CMS 中管理內容，該 CMS 會負責將內容呈現在您的網頁上。

現在，無周邊表示您的內容集可以在 CMS 中進行管理，然後由一個或多個 (獨立) 應用程式存取。

這表示您的內容能以多種格式傳遞到任何裝置。這使整個流程更加靈活，也表示您無需擔心版面和格式。

>[!NOTE]
>
>如果您想了解更多關於 Headless CMS 的技術細節，「了解 CMS Headless 開發」文件提供更多資訊。

## Adobe Experience Manager {#aem-cms}

什麼是 AEM？

首先，AEM 是一個內容管理系統，具有廣泛的功能，也可以依您的要求自訂。

這表示它可以做為：

* Headless CMS
   * 若為無周邊，可將內容編寫為&#x200B;**內容片段**。
這些是內容的獨立項目，可直接由各種應用程式存取，因為它們具有預先定義結構，以**內容片段模型**為基礎。
這表示您的內容能以多種格式及內含多種功能呈現在多種裝置上。
(作為一個雙重打擊，如果你想要的話，可以在建構 AEM 網頁時使用這些片段。)

* 「傳統」CMS
   * 內容是為網頁編寫的，使用一系列元件來定義內容將如何在您的網站上呈現。即使在這裡，AEM 也非常靈活，因為您的專案團隊可以開發自訂元件。

## 內容模型 {#content-modeling}

所以內容模型 (也稱為資料模型) 是另一個技術性術語，您身為作者為什麼對它感興趣？

為了讓無周邊應用程式可以存取您的內容並進行一些操作，您的內容確實需要有預先定義的結構。您的內容可以採用自由格式，但會使應用程式&#x200B;*十分*&#x200B;不便。

基本上，定義要遵循之內容結構的流程包含設計模型，這稱為資料模型。

對於 AEM，內容架構師角色 (通常是不同的人) 將執行資料模型，以設計一系列&#x200B;**內容片段模型** - 您可用來做為內容的基礎，透過使用&#x200B;**內容片段**。

>[!NOTE]
>
>如果您想了解更多有關資料模型的資訊，可以在「AEM Headless 內容架構師歷程」下閱讀更多內容。

## 下一步 {#whats-next}

現在您已經了解了概念和術語，下一步是[學習編寫內容片段的基礎知識](basics.md)。這將介紹 AEM 的基本處理以及如何編寫內容片段。

## 其他資源 {#additional-resources}

* AEM Headless 開發人員歷程
   * [了解 CMS Headless 開發](/help/journey-headless/developer/learn-about.md)

* [AEM Headless 內容架構師歷程](/help/journey-headless/architect/overview.md)

* [AEM Headless 內容翻譯歷程](/help/journey-headless/translation/overview.md)
