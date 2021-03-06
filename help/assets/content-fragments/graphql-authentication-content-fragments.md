---
title: 內容片段的遠端AEM GraphQL查詢驗證
description: 了解遠端AEM GraphQL查詢所需的驗證，以保護無周邊內容的傳送安全。
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: 9278ba4fe85edca4ab5741f89c0fc0ef2cf2764d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 內容片段的遠端AEM GraphQL查詢驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

主要使用案例 [Adobe Experience Manager(AEM)用於內容片段傳送的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) 接受來自第三方應用程式或服務的遠程查詢。 這些遠端查詢可能需要經過驗證的API存取，以保護無頭式內容傳送的安全。

>[!NOTE]
>
>若要進行測試和開發，您也可以直接使用 [GraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) 介面。

為了驗證，協力廠商服務需要使用AEM帳戶使用者名稱和密碼進行驗證。

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
