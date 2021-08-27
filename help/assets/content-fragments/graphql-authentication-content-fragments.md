---
title: 內容片段的遠端AEM GraphQL查詢驗證
description: 了解遠端AEM GraphQL查詢所需的驗證，以保護無周邊內容的傳送安全。
feature: Content Fragments,GraphQL API
source-git-commit: 2f647fc640d3809dc684bce397831ab37fb94b07
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 內容片段的遠端AEM GraphQL查詢驗證 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[Adobe Experience Manager(AEM)內容片段傳送](/help/assets/content-fragments/graphql-api-content-fragments.md)的GraphQL API主要使用案例是接受來自第三方應用程式或服務的遠端查詢。 這些遠端查詢可能需要經過驗證的API存取，以保護無頭式內容傳送的安全。

>[!NOTE]
>
>對於測試和開發，您還可以直接使用[GraphiQL介面](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)介面訪問AEM GraphQL API。

驗證時，第三方服務需要[檢索訪問令牌](#retrieving-access-token)，該令牌隨後可以[用於GraphQL請求](#use-access-token-in-graphql-request)。

## 擷取存取權杖 {#retrieving-access-token}

<!-- 6.5.10.0 - does this page need to be migrated? -->

<!--
See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.
-->

## 在GraphQL請求中使用存取權杖 {#use-access-token-in-graphql-request}

第三方服務若要與AEM執行個體連線，其必須有&#x200B;*存取Token*。 然後，服務必須將此Token新增至POST請求的`Authorization`標題。

例如， GraphQL授權標題：

```xml
Authorization: Bearer <access_token>
```

## 權限需求 {#permission-requirements}

使用存取權杖提出的所有請求實際上會由產生權杖&#x200B;*的使用者帳戶提出*。

這表示您需要檢查帳戶是否具備執行GraphQL查詢所需的權限。

您可以在本機執行個體上使用GraphiQL來檢查此問題。
