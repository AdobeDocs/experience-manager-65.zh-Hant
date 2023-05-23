---
title: 6.AEM5站點無頭開發
description: 瞭解AEM6.5的強大無頭功能(如內容模型、內容片段和GraphQLAPI)如何協同工作，使您能夠集中管理您的體驗並跨渠道提供服務。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 37%

---

# 6.AEM5站點無頭開發 {#headless-development}

瞭解AEM6.5的強大無頭功能(如內容模型、內容片段和GraphQLAPI)如何協同工作，使您能夠集中管理您的體驗並跨渠道提供服務。

## 概觀 {#overview}

無頭實施對於向受眾提供體驗越來越重要，無論他們身在何處，無論渠道如何。

Headless 實作放棄了全堆疊和混合解決方案中的傳統頁面和元件管理，專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。它是實作網頁體驗的現代動態開發模式。

![AEM 實作模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## 比較有周邊和無周邊 {#headful-headless}

本文檔重點介紹的完全無頭實施模AEM式。 然而，有周邊和無周邊在 AEM 中不必是二選一。無頭功能可用於管理內容並將內容交付到各種端點，同時還使您的內容作者能夠編輯單頁應用程式。 全部在 AEM 中。

>[!TIP]
>
>如需詳細資訊，請參閱[AEM Headful 和 Headless 技術](/help/sites-developing/headful-headless.md)文件。

## AEM6.5和無頭 {#aem-headless}

AEM6.5是一種靈活的工具，可提供三種功能強大的服務，用於無頭實施模式：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些定義由「內容片段模型」編輯AEM器中的資訊架構師定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的實例化。
   * 這些是由內容作者使用內容片AEM段編輯器建立的。
   * 它們儲存在AEM Assets，並在Assets Admin UI中進行管理。
1. 用於傳遞的內容 API
   * AEM GraphQL API 支援內容片段傳遞。
   * AEM Assets REST API 支援內容片段 CRUD 作業。
   * 還可以通過 [內容片段核心元件的JSON導出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用 AEM Headless 的第一步 {#first-steps}

有許多資源可供您開始使用無頭AEM功能。 它們用於不同的使用情形，但都提供了無頭功能AEM的實體概述。

| 資源 | 說明 | 類型 | 對象 | 預估時間 |
|---|---|---|---|---|
| [Headless 開發人員歷程](/help/journey-headless/developer/overview.md) | **對於新用戶和無AEM頭用戶** 從無頭理論開始，從AEM與你的第一個無頭項目一起生活開始，全面介紹其無頭特性。 | 指南 | **剛接觸 AEM 和無周邊技術** 的開發人員 | 1 小時 |
| [無頭入門指南](/help/sites-developing/headless/getting-started/introduction.md) | 對於需要扼要介紹關鍵 AEM 無周邊功能的&#x200B;**有經驗 AEM 使用者**，請查看此快速入門概述。 | 快速啟動 | **具有 AEM 經驗**&#x200B;的開發人員、管理員 | 20 分鐘 |
| [無頭AEM動手教程入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果你喜歡親力親為，並且熟AEM悉**，本教程直接介紹如何建立簡單的無頭項目。 | 教學課程 | 開發人員 | 2 小時 |
