---
title: 訪問和傳遞內容片段無頭快速入門手冊
description: 瞭解如何使AEM用Assets REST API管理內容片段和GraphQLAPI來無頭地傳遞內容片段內容。
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
source-git-commit: 7355c149500f9e5044c9ff78af208d36ee681f56
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 62%

---

# 訪問和傳遞內容片段無頭快速入門手冊 {#accessing-delivering-content-fragments}

瞭解如何使AEM用Assets REST API管理內容片段和GraphQLAPI來無頭地傳遞內容片段內容。

## 什麼是 GraphQL 和 Assets REST API？ {#what-are-the-apis}

[現在您已經建立一些內容片段，](create-content-fragment.md)您可以使用 AEM 的 API 無周邊傳遞內容片段。

* [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 允許您建立存取和傳遞內容片段的要求。
   * 若要使用，[需要在 AEM 中定義和啟用端點](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)，如果需要，[安裝 GraphiQL 介面](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface)。
* [Assets REST API](/help/assets/assets-api-content-fragments.md) 允許您建立及修改內容片段 (和其他資產)。

本指南的其餘部分著重在 GraphQL 存取和內容片段傳遞。

## 如何使用GraphQL傳遞內容片段 {#how-to-deliver-a-content-fragment}

資訊架構師需要為他們的管道端點設計查詢，以便傳遞內容。通常只需要為每個模型的每個端點考慮一次這些查詢。出於本快速入門指南的目的，我們只需要建立一個。

1. 登錄AEM並訪問 [GraphiQL介面](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * 例如：`http://<host>:<port>/aem/graphiql.html`。

1. GraphiQL 是 GraphQL 的瀏覽器內查詢編輯器。您可以使用它構建查詢以檢索內容片段，以JSON形式直接傳遞這些內容片段。
   * 左面板允許您生成查詢。
   * 右面板顯示結果。
   * 查詢編輯器具有程式碼完成和快速鍵功能，可輕鬆執行查詢。
      ![GraphiQL 編輯器](assets/graphiql.png)

1. 假設我們建立的模型名為 `person`，其中包含欄位 `firstName`、`lastName` 和 `position`，我們可以建立一個簡單的查詢來擷取內容片段的內容。

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 在左側面板中輸入查詢。

<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. 按一下 **執行查詢** （右箭頭）表徵圖或使用 `Ctrl-Enter` 熱鍵和結果在右面板中顯示為JSON。
   ![GraphiQL 結果](assets/graphiql-results.png)

1. 按一下:
   * **文檔** 頁面右上角顯示上下文文檔，以幫助您構建適應您自己模型的查詢。
   * **歷史** 的子菜單。
   * **另存為** 和 **保存** 以保存查詢，之後您可以列出查詢並從中檢索查詢 **永續查詢** 面板和 **發佈**。
      ![GraphiQL 文件](assets/graphiql-documentation.png)

GraphQL 支援結構化查詢，這些查詢不僅可以針對特定資料集或個別資料物件，還可以傳遞物件的特定元素、巢狀結果、支援查詢變數等等。

GraphQL 可以避免反覆 API 要求以及過度傳遞，而是允許大量傳遞呈現作業所需的內容，作為對單一 API 查詢的回應。產生的 JSON 可用於將資料傳遞到其他網站或應用程式。

## 後續步驟 {#next-steps}

就是這樣！您現在對 AEM 無周邊內容管理有基本的了解。當然，還有更多資源可供您深入研究以全面了解可用的功能。

* **[配置瀏覽器](create-configuration.md)**  — 有關配置瀏覽器AEM的詳細資訊
* **[內容片段](/help/assets/content-fragments/content-fragments.md)** - 詳細說明如何建立和管理內容片段
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** 有關使用GraphiQL IDE的詳細資訊
* **[永續查詢](/help/sites-developing/headless/graphql-api/persisted-queries.md)** 獲取永續查詢的詳細資訊
* **[AEM Assets HTTP API 支援內容片段](/help/assets/assets-api-content-fragments.md)** - 詳細說明如何運用 CRUD 操作 (建立、讀取、更新、刪除) 透過 HTTP API 直接存取 AEM 內容。
* **[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - 詳細說明如何以無周邊方式傳遞內容片段
