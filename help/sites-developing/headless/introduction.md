---
title: AEM 6.5 Sites無頭開發
description: 了解AEM 6.5的無周邊功能（例如內容模型、內容片段和GraphQL API）如何搭配運作，讓您集中管理體驗，並跨管道提供體驗。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# AEM 6.5 Sites無頭開發 {#headless-development}

了解AEM 6.5的無周邊功能（例如內容模型、內容片段和GraphQL API）如何搭配運作，讓您集中管理體驗，並跨管道提供體驗。

## 總覽 {#overview}

無頭式實作對於將體驗提供給對象（無論對象在何處、無論管道為何）越來越重要。

無頭實作會放棄頁面和元件管理，如同傳統的完整堆疊和混合解決方案一樣，著重於建立不受管道影響、可重複使用的內容片段及其跨管道傳送。 這是實作Web體驗的現代化、動態開發模式。

![AEM實作模型](assets/aem-implementation-models.png)

## 比較Headful和Headless {#headful-headless}

本檔案著重於AEM的完整無頭式實作模型。 不過，在AEM中，無頭與無頭並非二進位選擇。 無頭功能可用來管理內容，並將內容傳遞至各種端點，同時讓內容作者編輯單頁應用程式。 全部在AEM。

>[!TIP]
>
>請參閱檔案 [AEM中的Headful和Headless](/help/sites-developing/headful-headless.md) 以取得更多資訊。

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
1. 傳遞的內容API
   * AEM GraphQL API支援內容片段傳送。
   * AEM Assets REST API支援內容片段CRUD操作。
   * 您也可以透過 [內容片段核心元件的JSON匯出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用AEM Headless的第一步 {#first-steps}

有許多資源可供您開始使用AEM無頭功能。 這些範本適用於不同的使用案例，但都能提供AEM無頭功能的實體概述。

| 資源 | 說明 | 類型 | 對象 | Est. 時間 |
|---|---|---|---|---|
| [無頭式開發人員歷程](/help/journey-headless/developer/overview.md) | **適用於剛接觸AEM和無頭的使用者** 技術，請從這裡開始，全面介紹AEM及其無頭式功能，從無頭式理論到與您的第一個無頭式專案同時運作。 | 指南 | 開發人員 **新增至AEM及無頭** | 1小時 |
| [無頭入門手冊](/help/sites-developing/headless/getting-started/introduction.md) | **適用於經驗豐富的AEM使用者** 若需要主要AEM無頭功能的簡短摘要，請查看此快速入門概述。 | 快速入門 | 開發人員、管理員 **使用AEM體驗** | 20分鐘 |
| [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您偏好實作方法，且熟悉AEM**，本教學課程會直接深入探討如何建立簡單的無標題專案。 | 教學課程 | 開發人員 | 2小時 |
