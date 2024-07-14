---
title: 適用於AEM 6.5 Sites的Headless開發
description: 瞭解AEM 6.5強大的Headless功能(例如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理您的體驗並跨管道提供這些體驗。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 35%

---

# 適用於AEM 6.5 Sites的Headless開發 {#headless-development}

瞭解AEM 6.5強大的Headless功能(例如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理您的體驗並跨管道提供這些體驗。

## 概觀 {#overview}

Headless實施對於向您的受眾提供體驗變得越來越重要，無論他們身在何處，也不論他們使用何種管道。

Headless 實作放棄了全堆疊和混合解決方案中的傳統頁面和元件管理，專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。它是實作網頁體驗的現代動態開發模式。

![AEM 實作模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## 比較有周邊和無周邊 {#headful-headless}

本檔案著重於AEM的完整Headless實作模型。 然而，有周邊和無周邊在 AEM 中不必是二選一的選擇。Headless功能可用來管理內容並將內容傳送至各種端點，同時讓內容作者可編輯單頁應用程式。 全部在 AEM 中。

>[!TIP]
>
>如需詳細資訊，請參閱 [AEM Headful 和 Headless 技術](/help/sites-developing/headful-headless.md)文件。

## AEM 6.5和Headless {#aem-headless}

AEM 6.5是適用於Headless實作模式的彈性工具，提供三種強大的服務：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些是由資訊架構師在AEM內容片段模型編輯器中定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的例項化。
   * 這些是由內容作者使用AEM內容片段編輯器所建立。
   * 儲存在AEM Assets中，並在Assets管理UI中進行管理。
1. 傳送的內容API
   * AEM GraphQL API 支援內容片段傳遞。
   * AEM Assets REST API 支援內容片段 CRUD 作業。
   * 透過[內容片段核心元件的JSON匯出，也可以進行直接內容傳送。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用 AEM Headless 的第一步 {#first-steps}

您有數個資源可開始使用AEM的Headless功能。 這些範本適用於不同的使用案例，但都能為AEM的Headless功能提供可靠的概覽。

| 資源 | 說明 | 類型 | 對象 | 預估時間 |
|---|---|---|---|---|
| [Headless 開發人員歷程](/help/journey-headless/developer/overview.md) | **對於剛開始使用AEM和Headless**&#x200B;技術的使用者，從這裡開始全面瞭解AEM及其Headless功能，從Headless的理論直到您的第一個Headless專案。 | 指南 | **剛接觸 AEM 和無周邊技術** 的開發人員 | 1 小時 |
| [Headless快速入門手冊](/help/sites-developing/headless/getting-started/introduction.md) | 對於需要扼要介紹關鍵 AEM 無周邊功能的&#x200B;**有經驗 AEM 使用者**，請查看此快速入門概述。 | 快速入門 | **具有 AEM 經驗**&#x200B;的開發人員、管理員 | 20 分鐘 |
| [開始使用AEM Headless實作教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您偏好實作方法並且熟悉AEM**，本教學課程將直接探討如何建立簡單的Headless專案。 | 教學課程 | 開發人員 | 2 小時 |
| [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html) | 此資源集合是供&#x200B;**新**&#x200B;和&#x200B;**經驗豐富的**&#x200B;開發人員使用。 | 資源集合 | 開發人員 | |
