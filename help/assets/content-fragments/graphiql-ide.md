---
title: 在 AEM 中使用 GraphiQL IDE
description: 了解如何在 Adobe Experience Manager 中使用 GraphiQL IDE。
source-git-commit: 42ef4694a3301ae1cd34766ce4c19f4b0e2f2c38
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 94%

---

# 使用 GraphiQL IDE {#graphiql-ide}

標準的實施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE可與Adobe Experience Manager的GraphQL API(AEM)搭配使用。

>[!NOTE]
>
>GraphiQL 包含在 AEM 的所有環境中 (但只有在您配定端點時才可存取/可見)。
>
>在先前版本，需要套件來安裝 GraphiQL IDE。如果您已安裝，現在可以將其移除。

>[!NOTE]
>您必須在[設定瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)中[設定您的端點](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint)，才能使用 GraphiQL IDE。

**GraphiQL** 工具可讓您透過以下方式測試和偵錯 GraphQL 查詢：

* 選擇適合您要用於查詢之 Sites 設定的&#x200B;**端點**
* 直接輸入新查詢
* 建立和存取&#x200B;**[持續性查詢](/help/assets/content-fragments/persisted-queries.md)**
* 執行查詢以立即查看結果
* 管理&#x200B;**查詢變數**
* 儲存和管理&#x200B;**持續性查詢**
* 發佈或取消發佈&#x200B;**持續性查詢** (例如，to/from `dev-publish`)
* 查看您之前查詢的&#x200B;**歷史記錄**
* 使用&#x200B;**文件總管**&#x200B;以存取文件；協助您學習並了解可用的方法。

您可以從以下任一方式存取查詢編輯器：

* **工具** -> **一般** -> **GraphQL 查詢編輯器**
* 直接；例如 `http://localhost:4502/aem/graphiql.html`

![GraphiQL 介面](assets/cfm-graphiql-interface.png "GraphiQL 介面")

您可以在您的系統上使用 GraphiQL，以便您的用戶端應用程式可以使用 GET 要求來要求查詢，和用於發佈查詢。如果是用於生產，您可以[將查詢移至您的生產環境](/help/assets/content-fragments/persisted-queries.md#transfer-persisted-query-production)。最初是生產編寫以使用查詢驗證新編寫的內容，最後是生產發佈以供上線取用。

## 選取您的端點 {#selecting-endpoint}

第一步，您必須選取您要用於查詢的&#x200B;**[端點](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint)**。此端點適合您要用於查詢的 Sites 設定。

這可以從右上角的下拉清單中取得。

## 建立並保留新查詢 {#creating-new-query}

您可以在編輯器中輸入新查詢 - 它位於左側中間面板，GraphiQL 標誌正下方。

>[!NOTE]
>
>如果您已經選取持續性查詢，並顯示在編輯器面板中，請選取 `+` (**持續性查詢** 旁邊) 以清空編輯器，為您的新查詢做好準備。

只要開始輸入，編輯器也會：

* 使用游標懸停以顯示有關元素的其他資訊
* 提供像是語法醒目提示、自動完成、自動建議等功能

>[!NOTE]
>
>GraphQL 查詢通常以 `{` 字元開頭。
>
>以 `#` 開頭的行將被忽略。

使用&#x200B;**另存新檔**&#x200B;保留您的新查詢。

## 更新持續性查詢 {#updating-persisted-query}

從&#x200B;**[持續性查詢](/help/assets/content-fragments/persisted-queries.md)**&#x200B;面板 (最左側) 的清單中選取要更新的查詢。

查詢將顯示在編輯器面板中。視需要進行變更，然後使用&#x200B;**儲存**&#x200B;將更新提交到持續性查詢。

## 執行查詢 {#running-queries}

您可以立即執行新查詢，也可以載入並執行持續性查詢。若要載入持續性查詢，請從清單中選取 - 查詢將顯示在編輯器面板中。

在任何一種情況下，編輯器面板顯示的查詢，都是在您執行以下操作時會執行的查詢：

* 按一下/點選&#x200B;**執行查詢**&#x200B;圖示
* 使用鍵盤組合 `Control-Enter`

## 查詢變數 {#query-variables}

<!-- more details needed here? -->

GraphiQL IDE 也可讓您管理[查詢變數](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-variables)。

例如：

![GraphQL 變數](assets/cfm-graphqlapi-03.png "GraphQL 變數")

<!--
## Managing cache for your persisted queries {#managing-cache}

[Persisted queries](/help/headless/graphql-api/persisted-queries.md) are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application. By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL).

>[!NOTE]
>
>Custom rewrite rules on the Dispatcher might override defaults from AEM publish. 
>
>In the case that you are sending TTL-based cache-control headers from the dispatcher, based on a location match pattern, then, if necessary, you might want to exclude `/graphql/execute.json/*` from the matches.

Using GraphQL you can configure the HTTP Cache Headers  to control these parameters for your individual persisted query.

1. The **Headers** option is accessible via the three vertical dots to the right of the persisted query name (far left panel):

   ![Persisted Query HTTP Cache Headers](assets/cfm-graphqlapi-headers-01.png "Persisted Query HTTP Cache Headers")

1. Selecting this will open the **Cache Configuration** dialog:

   ![Persisted Query HTTP Cache Header Settings](assets/cfm-graphqlapi-headers-02.png "Persisted Query HTTP Cache Header Settings")

1. Select the appropriate parameter, then adjust the value as required:

   * **cache-control** - **max-age**
     Caches can store this content for specified number of seconds. Typically this is the browser TTL (Time To Live).
   * **surrogate-control** - **s-maxage**
     Same as max-age but applies specifically to proxy caches.
   * **surrogate-control** - **stale-while-revalidate**
     Caches may continue to serve a cached response after it becomes stale, for up to the specified number of seconds.
   * **surrogate-control** - **stale-if-error**
     Caches may continue to serve a cached response in case of or origin error, for up to the specified number of seconds.

1. Select **Save** to persist the changes.
-->

## 發佈持續性查詢 {#publishing-persisted-queries}

選取您的 [持續查詢](/help/assets/content-fragments/persisted-queries.md) 從清單（左側面板），您可以使用 **發佈** 和 **取消發佈** 動作。 這會將其啟動到發佈環境 (例如，`dev-publish`)，以便應用程式在測試時輕鬆存取。

>[!NOTE]
>
>持續性查詢快取 `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} 之定義的預設值為 2 小時 (7200 秒)。

## 複製 URL 以直接存取查詢 {#copy-url}

**複製 URL** 選項可讓您模擬查詢，方法是複製用於直接存取持續性查詢的 URL，然後查看結果。然後可以將其用於測試；例如，在瀏覽器中存取：

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

例如：

`http://localhost:4502/graphql/execute.json/global/article-list-01`

在瀏覽器使用此 URL，您可以確認結果：

![GraphiQL - 複製 URL](assets/cfm-graphiql-copy-url.png "GraphiQL - 複製 URL")

**複製 URL**&#x200B;選項可透過持續性查詢名稱右側的垂直三點存取 (最左側面板)：

![GraphiQL - 複製 URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - 複製 URL")

## 刪除持續性查詢 {#deleting-persisted-queries}

**刪除**&#x200B;選項也可透過持續性查詢名稱右側的垂直三點存取 (最左側面板)。

<!-- what happens if you try to delete something that is still published? -->


## 在生產環境中安裝持續性查詢 {#installing-persisted-query-production}

使用 GraphiQL 開發和測試持續性查詢後，最終目標是[將其傳送到生產環境](/help/assets/content-fragments/persisted-queries.md#transfer-persisted-query-production)以供應用程式使用。

## 鍵盤快速鍵 {#keyboard-shortcuts}

有一系列鍵盤快速鍵可用來直接存取 IDE 中的動作圖示：

* 修飾查詢：`Shift-Control-P`
* 合併查詢：`Shift-Control-M`
* 執行查詢：`Control-Enter`
* 自動完成：`Control-Space`

>[!NOTE]
>
>在某些鍵盤上，`Control` 鍵標記為 `Ctrl`。
