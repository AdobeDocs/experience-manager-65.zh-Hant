---
title: 對內容片段的遠端Adobe Experience Manager GraphQL查詢的驗證
description: 瞭解遠端Adobe Experience Manager GraphQL查詢所需的驗證，以確保Headless內容傳送的安全。
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 對內容片段的遠端Adobe Experience Manager GraphQL查詢的驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

的主要使用案例 [用於內容片段傳送的Adobe Experience Manager (AEM) GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 是接受來自協力廠商應用程式或服務的遠端查詢。 這些遠端查詢可能需要經過驗證的API存取，以保護Headless內容傳送。

>[!NOTE]
>
>若要進行測試和開發，您也可以使用直接存取AEM GraphQL API [GraphiQL介面](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

為了進行驗證，第三方服務需要使用AEM帳戶使用者名稱和密碼進行驗證。

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
