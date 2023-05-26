---
title: 適用於AEM 6.5 Sites的Headless開發
description: 瞭解AEM 6.5強大的Headless功能(如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理您的體驗，並跨管道提供這些體驗。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 37%

---

# 適用於AEM 6.5 Sites的Headless開發 {#headless-development}

瞭解AEM 6.5強大的Headless功能(如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理您的體驗，並跨管道提供這些體驗。

## 概觀 {#overview}

Headless實施對於向您的受眾提供體驗變得越來越重要，無論他們身在何處，也不論他們使用哪個管道。

Headless 實作放棄了全堆疊和混合解決方案中的傳統頁面和元件管理，專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。它是實作網頁體驗的現代動態開發模式。

![AEM 實作模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## 比較有周邊和無周邊 {#headful-headless}

本檔案著重於AEM的完整Headless實作模型。 然而，有周邊和無周邊在 AEM 中不必是二選一。Headless功能可用來管理內容並將其傳送至各種端點，同時讓內容作者可以編輯單頁應用程式。 全部在 AEM 中。

>[!TIP]
>
>如需詳細資訊，請參閱[AEM Headful 和 Headless 技術](/help/sites-developing/headful-headless.md)文件。

## AEM 6.5和Headless {#aem-headless}

AEM 6.5是適用於Headless實作模式的彈性工具，提供三種強大的服務：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些由AEM內容片段模式編輯器中資訊架構師定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的例項化。
   * 這些是由內容作者使用AEM內容片段編輯器建立。
   * 這些檔案儲存在AEM Assets中，並在資產管理員UI中進行管理。
1. 用於傳遞的內容 API
   * AEM GraphQL API 支援內容片段傳遞。
   * AEM Assets REST API 支援內容片段 CRUD 作業。
   * 也可以使用直接內容傳送 [內容片段核心元件的JSON匯出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用 AEM Headless 的第一步 {#first-steps}

有許多資源可供您開始使用AEM Headless功能。 這些範本適用於不同的使用案例，但都能提供AEM Headless功能的完整概覽。

| 資源 | 說明 | 類型 | 對象 | 預估時間 |
|---|---|---|---|---|
| [Headless 開發人員歷程](/help/journey-headless/developer/overview.md) | **對於AEM和Headless的新使用者** 技術，從這裡開始全面介紹AEM及其headless功能，從headless的理論到您的第一個headless專案。 | 指南 | **剛接觸 AEM 和無周邊技術** 的開發人員 | 1 小時 |
| [Headless快速入門手冊](/help/sites-developing/headless/getting-started/introduction.md) | 對於需要扼要介紹關鍵 AEM 無周邊功能的&#x200B;**有經驗 AEM 使用者**，請查看此快速入門概述。 | 快速入門 | **具有 AEM 經驗**&#x200B;的開發人員、管理員 | 20 分鐘 |
| [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您偏好實作方法且熟悉AEM**，本教學課程將直接說明如何建立簡單的Headless專案。 | 教學課程 | 開發人員 | 2 小時 |
