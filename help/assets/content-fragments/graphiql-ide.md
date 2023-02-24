---
title: 在AEM中使用GraphiQL IDE
description: 了解如何使用Adobe Experience Manager中的GraphiQL IDE。
source-git-commit: 42ef4694a3301ae1cd34766ce4c19f4b0e2f2c38
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# 使用GraphiQL IDE {#graphiql-ide}

標準的實施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE可與Adobe Experience Manager的GraphQL API(AEM)搭配使用。

>[!NOTE]
>
>GraphiQL包含在AEM的所有環境中（但只有在配置端點時才能存取/顯示）。
>
>在以前的版本中，安裝GraphiQL IDE時需要一個包。 如果您已安裝此程式碼，現在可將其移除。

>[!NOTE]
>您必須 [已配置端點](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint) 在 [配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md) ，然後再使用GraphiQL IDE。

此 **GraphiQL** 工具可讓您測試和偵錯GraphQL查詢，方法是：

* 選取 **端點** 適合您要用於查詢的Sites設定
* 直接輸入新查詢
* 建立和存取， **[持續查詢](/help/assets/content-fragments/persisted-queries.md)**
* 運行查詢以立即查看結果
* 管理 **查詢變數**
* 儲存並管理 **持續查詢**
* 發佈或取消發佈， **持續查詢** (例如，從 `dev-publish`)
* 請參閱 **歷史記錄** 您以前的查詢
* 使用 **檔案總管** 查閱檔案；可協助您了解和了解可用的方法。

您可以透過下列任一項存取查詢編輯器：

* **工具** -> **一般** -> **GraphQL查詢編輯器**
* 直接；例如， `http://localhost:4502/aem/graphiql.html`

![GraphiQL介面](assets/cfm-graphiql-interface.png "GraphiQL介面")

您可以在系統上使用GraphiQL，以便客戶端應用程式可以使用GET請求來請求查詢，並發佈查詢。 就生產用途而言，您可以 [將查詢移至生產環境](/help/assets/content-fragments/persisted-queries.md#transfer-persisted-query-production). 最初供生產製作者使用以驗證含有查詢的新撰寫內容，最後供生產發佈以供即時使用。

## 選取端點 {#selecting-endpoint}

作為第一步，您需要選取 **[端點](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint)** 用於查詢。 端點適合您要用於查詢的Sites配置。

這可從右上角的下拉式清單取得。

## 建立新查詢並保留 {#creating-new-query}

您可以在編輯器中輸入新查詢，該編輯器位於中左側面板中，直接位於GraphiQL徽標下。

>[!NOTE]
>
>如果您已選取保存的查詢，並在編輯器面板中顯示，請選取 `+` (旁邊 **持續查詢**)以空白編輯器，為新查詢做好準備。

開始打字，編輯還說：

* 使用滑鼠移過來顯示有關元素的其他資訊
* 提供語法醒目提示、自動完成、自動建議等功能

>[!NOTE]
>
>GraphQL查詢通常以 `{` 字元。
>
>以 `#` 會被忽略。

使用 **另存新檔** 以保留新查詢。

## 更新保存的查詢 {#updating-persisted-query}

從 **[持續查詢](/help/assets/content-fragments/persisted-queries.md)** 面板（最左邊）。

查詢將顯示在編輯器面板中。 進行您需要的任何變更，然後使用 **儲存** 將更新提交到持續查詢。

## 正在運行查詢 {#running-queries}

您可以立即運行新查詢，也可以載入並運行持續查詢。 若要載入持續查詢，請從清單中選取該查詢 — 該查詢將顯示在編輯器面板中。

無論是哪種情況，編輯器面板中顯示的查詢都是將在您執行下列任一操作時執行的查詢：

* 按一下/點選 **執行查詢** 圖示
* 使用鍵盤組合 `Control-Enter`

## 查詢變數 {#query-variables}

<!-- more details needed here? -->

GraphiQL IDE還允許您管理 [查詢變數](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-variables).

例如：

![GraphQL變數](assets/cfm-graphqlapi-03.png "GraphQL變數")

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

## 發佈持續查詢 {#publishing-persisted-queries}

選取您的 [持續查詢](/help/assets/content-fragments/persisted-queries.md) 從清單（左側面板），您可以使用 **發佈** 和 **取消發佈** 動作。 這會將它們啟用至您的發佈環境(例如 `dev-publish`)，讓應用程式在測試時輕鬆存取。

>[!NOTE]
>
>持續查詢快取的定義 `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value}的預設值為2小時（7200秒）。

## 複製URL以直接存取查詢 {#copy-url}

此 **複製URL** 選項可讓您複製用來直接存取持續查詢並查看結果的URL，以模擬查詢。 這可用於測試；例如，透過在瀏覽器中存取：

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

例如：

`http://localhost:4502/graphql/execute.json/global/article-list-01`

在瀏覽器中使用此URL可確認結果：

![GraphiQL — 複製URL](assets/cfm-graphiql-copy-url.png "GraphiQL — 複製URL")

此 **複製URL** 選項可透過持續查詢名稱右側的三個垂直點來存取（最左側面板）:

![GraphiQL — 複製URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL — 複製URL")

## 刪除持續查詢 {#deleting-persisted-queries}

此 **刪除** 您也可以透過持續查詢名稱右側的三個垂直點（最左側面板）來存取選項。

<!-- what happens if you try to delete something that is still published? -->


## 在生產環境上安裝持續查詢 {#installing-persisted-query-production}

使用GraphiQL開發和測試持續存在的查詢後，最終目標是 [將其傳輸到生產環境](/help/assets/content-fragments/persisted-queries.md#transfer-persisted-query-production) 供應用程式使用。

## 鍵盤快速鍵 {#keyboard-shortcuts}

在IDE中，有一系列鍵盤快捷鍵提供了對操作表徵圖的直接訪問：

* Prettify Query:  `Shift-Control-P`
* 合併查詢：  `Shift-Control-M`
* 執行查詢：  `Control-Enter`
* 自動完成：  `Control-Space`

>[!NOTE]
>
>在一些鍵盤上， `Control` 索引鍵標示為 `Ctrl`.
