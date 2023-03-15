---
title: AEM 6.5 Sites無頭開發
description: 了解AEM 6.5的強大無頭功能(例如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理體驗，並跨管道提供體驗。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 37%

---

# AEM 6.5 Sites無頭開發 {#headless-development}

了解AEM 6.5的強大無頭功能(例如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理體驗，並跨管道提供體驗。

## 概觀 {#overview}

無頭式實作對於將體驗提供給對象（無論對象在何處、無論管道為何）越來越重要。

Headless 實作放棄了全堆疊和混合解決方案中的傳統頁面和元件管理，專注於建立管道中立、可重複使用的內容片段及其跨管道傳遞。它是實作網頁體驗的現代動態開發模式。

![AEM 實作模型](assets/aem-implementation-models.png)

## 比較有周邊和無周邊 {#headful-headless}

本檔案著重於AEM的完整無頭式實作模型。 然而，有周邊和無周邊在 AEM 中不必是二選一。無頭功能可用來管理內容，並將內容傳遞至各種端點，同時讓內容作者編輯單頁應用程式。 全部在 AEM 中。

>[!TIP]
>
>如需詳細資訊，請參閱[AEM Headful 和 Headless 技術](/help/sites-developing/headful-headless.md)文件。

## AEM 6.5和無頭 {#aem-headless}

AEM 6.5是無頭式實作模型的彈性工具，提供三種強大的服務：

1. 內容模型
   * 內容模型是內容的結構化表示。
   * 這些由AEM內容片段模型編輯器中的資訊架構師定義。
   * 內容模型是內容片段的基礎。
1. 內容片段
   * 內容片段是內容模型的實例化。
   * 這些是由內容作者使用AEM內容片段編輯器建立。
   * 這些資產會儲存在AEM Assets中，並在Assets管理UI中進行管理。
1. 用於傳遞的內容 API
   * AEM GraphQL API 支援內容片段傳遞。
   * AEM Assets REST API 支援內容片段 CRUD 作業。
   * 您也可以透過 [內容片段核心元件的JSON匯出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用 AEM Headless 的第一步 {#first-steps}

有許多資源可供您開始使用AEM無頭功能。 這些範本適用於不同的使用案例，但都能提供AEM無頭功能的實體概述。

| 資源 | 說明 | 類型 | 對象 | 預估時間 |
|---|---|---|---|---|
| [Headless 開發人員歷程](/help/journey-headless/developer/overview.md) | **適用於剛接觸AEM和無頭的使用者** 技術，請從這裡開始，全面介紹AEM及其無頭式功能，從無頭式理論到與您的第一個無頭式專案同時運作。 | 指南 | **剛接觸 AEM 和無周邊技術** 的開發人員 | 1 小時 |
| [無頭入門手冊](/help/sites-developing/headless/getting-started/introduction.md) | 對於需要扼要介紹關鍵 AEM 無周邊功能的&#x200B;**有經驗 AEM 使用者**，請查看此快速入門概述。 | 快速入門 | **具有 AEM 經驗**&#x200B;的開發人員、管理員 | 20 分鐘 |
| [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您偏好實作方法，且熟悉AEM**，本教學課程會直接深入探討如何建立簡單的無標題專案。 | 教學課程 | 開發人員 | 2 小時 |
