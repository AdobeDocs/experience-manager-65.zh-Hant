---
title: 存取及傳遞內容片段無頭快速入門手冊
description: 了解如何使用AEM Assets REST API管理內容片段，以及使用GraphQL API無頭傳送內容片段內容。
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
source-git-commit: f17674f535fe4ecfdf846132bfc7787384095892
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 存取及傳遞內容片段無頭快速入門手冊 {#accessing-delivering-content-fragments}

了解如何使用AEM Assets REST API管理內容片段，以及使用GraphQL API無頭傳送內容片段內容。

## 什麼是GraphQL和Assets REST API? {#what-are-the-apis}

[既然您已建立了一些內容片段，](create-content-fragment.md) 您可以使用AEM API來無端傳送。

* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) 可讓您建立存取和傳送內容片段的請求。
   * 若要使用， [需要在AEM中定義並啟用端點](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)，若需要，則 [已安裝GraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface).
* [資產REST API](/help/assets/assets-api-content-fragments.md) 可讓您建立和修改內容片段（和其他資產）。

本指南的其餘部分將著重於GraphQL存取和內容片段傳送。

## 如何使用GraphQL傳送內容片段 {#how-to-deliver-a-content-fragment}

資訊架構師需要為其管道端點設計查詢，才能傳送內容。 通常，每個模型的每個端點只需考慮這些查詢一次。 為了此快速入門手冊的目的，我們只需建立指南。

1. 登入AEM並存取 [GraphiQL介面](/help/assets/content-fragments/graphiql-ide.md):
   * 例如：`http://<host>:<port>/aem/graphiql.html`。

1. GraphiQL是GraphQL的瀏覽器內查詢編輯器。 您可以使用它建立查詢來擷取內容片段，以便以JSON形式直接傳送。
   * 左側面板可讓您建立查詢。
   * 右側面板顯示結果。
   * 查詢編輯器具有代碼完成功能和可輕鬆執行查詢的快捷鍵。
      ![GraphiQL編輯器](../assets/graphiql.png)

1. 假設我們建立的模型 `person` 使用欄位 `firstName`, `lastName`，和 `position`，我們可以建立簡單查詢來擷取內容片段的內容。

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
   ![GraphiQL query](../assets/graphiql-query.png)
-->

1. 按一下 **執行查詢** （向右箭頭）圖示，或使用 `Ctrl-Enter` 快捷鍵和結果會在右側面板中顯示為JSON。
   ![GraphiQL結果](../assets/graphiql-results.png)

1. 按一下:
   * **檔案** 顯示內容內檔案，協助您建立可適應您自己模型的查詢。
   * **歷史記錄** ，以顯示先前的查詢。
   * **另存新檔** 和 **儲存** 要保存查詢，在此之後，您可以列出並從 **持續查詢** 面板和 **發佈**.
      ![GraphiQL檔案](../assets/graphiql-documentation.png)

GraphQL可啟用結構化查詢，不僅可鎖定特定資料集或個別資料物件，還可傳送物件的特定元素、巢狀結果、支援查詢變數等。

GraphQL可以避免重複的API要求以及過度傳送，而可大量傳送要求，以回應單一API查詢時呈現所需的內容。 產生的JSON可用來傳送資料至其他網站或應用程式。

## 後續步驟 {#next-steps}

就這樣！ 您現在對AEM中無頭式內容管理有了基本的了解。 當然，您還可以透過更多資源更進一步深入了解可用功能。

* **[配置瀏覽器](create-configuration.md)**  — 如需AEM設定瀏覽器的詳細資訊
* **[內容片段](/help/assets/content-fragments/content-fragments.md)**  — 如需建立和管理內容片段的詳細資訊
* **[GraphiQL IDE](/help/assets/content-fragments/graphiql-ide.md)** 有關使用GraphiQL IDE的詳細資訊
* **[持續查詢](/help/assets/content-fragments/persisted-queries.md)** 以取得持續查詢的詳細資訊
* **[AEM Assets HTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md)**  — 如需透過CRUD作業（建立、讀取、更新、刪除）直接存取AEM內容的詳細資訊
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  — 如需如何無謂傳送內容片段的詳細資訊
