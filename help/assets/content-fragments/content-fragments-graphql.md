---
title: 使用內容片段搭配GraphQL的無周邊內容傳送
description: 了解如何搭配GraphQL使用AEM內容片段進行無周邊內容傳送。
feature: Content Fragments
role: User
source-git-commit: 819df6d6123575b378676dda200064725de47b84
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# 使用內容片段搭配GraphQL的無周邊內容傳送 {#headless-content-delivery-using-content-fragments-with-graphQL}

透過Adobe Experience Manager(AEM)，您可以使用內容片段，搭配AEM GraphQL API（以標準GraphQL為基礎的自訂實作），以無條件提供結構化內容，以便在您的應用程式中使用。 自訂單一API查詢的功能可讓您擷取並傳送您要/需要呈現的特定內容（作為單一API查詢的回應）。

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>Adobe Experience Manager(AEM)中目前有兩種（個別）的情況使用GraphQL:
>
>* [AEM商務會透過GraphQL從商務平台取用資料](/help/commerce/cif/integrating/magento.md)。
>* [AEM內容片段可與AEM GraphQL API（以標準GraphQL為基礎的自訂實作）搭配使用，提供結構化內容以供您的應用程式使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 無頭式CMS {#headless-cms}

無頭式內容管理系統(CMS)是：

* &quot;*無頭式內容管理系統（或無頭式CMS）是從頭到尾構建的僅後端內容管理系統(CMS)，它是一個內容儲存庫，可通過API訪問內容以在任何設備上顯示。*

   請參閱[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

就在AEM中編寫內容片段而言，這表示：

* 您可以使用內容片段來製作主要不打算直接在格式化頁面上(1:1)發的內容。

* 內容片段的內容將根據內容片段模型以預先決定的方式建構。 這可簡化應用程式的存取，進而處理您的內容。

## GraphQL — 概觀 {#graphql-overview}

GraphQL為：

* &quot;*..API的查詢語言，以及使用您現有資料完成這些查詢的執行階段。*&quot;。

   請參閱[GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api)可讓您對[內容片段](/help/assets/content-fragments/content-fragments.md)執行（複雜）查詢；每個查詢都根據特定模型類型。 之後，您的應用程式就可以使用傳回的內容。

## AEM GraphQL API {#aem-graphql-api}

針對Adobe Experience，已開發標準GraphQL API的自訂實作。 如需詳細資訊，請參閱[AEM GraphQL API以搭配內容片段](/help/assets/content-fragments/graphql-api-content-fragments.md)使用。

AEM GraphQL API實作以[GraphQL Java程式庫](https://graphql.org/code/#java)為基礎。

## 與AEM GraphQL API搭配使用的內容片段 {#content-fragments-use-with-aem-graphql-api}

[內](#content-fragments) 容片段可作為AEM查詢的GraphQL基礎，如下：

* 它們可讓您設計、建立、組織和發佈不受頁面影響的內容。
* [內容片段模型](#content-fragments-models)透過定義的資料類型提供所需的結構。
* 定義模型時可用的[片段參考](#fragment-references)可用來定義其他結構層。

![與GraphQL搭配使用的內](assets/cfm-nested-01.png "容片段與GraphQL搭配使用")

### 內容片段 {#content-fragments}

內容片段:

* 包含結構化內容。

* 它們以[內容片段模型](#content-fragments-models)為基礎，該模型預先定義所產生片段的結構。

### 內容片段模型 {#content-fragments-models}

以下[內容片段模型](/help/assets/content-fragments/content-fragments-models.md):

* 用於產生[結構](https://graphql.org/learn/schema/)，一次&#x200B;**啟用**。

* 提供GraphQL所需的資料類型和欄位。 它們可確保您的應用程式只要求可能的項目，並接收預期的項目。

* 資料類型&#x200B;**[片段參考](#fragment-references)**&#x200B;可在模型中使用以參考其他內容片段，因此引入其他層級的結構。

### 片段參考 {#fragment-references}

**[片段參考](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 與GraphQL搭配使用時尤其受到關注。

* 是定義內容片段模型時可使用的特定資料類型。

* 參考另一個片段，取決於特定內容片段模型。

* 可讓您擷取結構化資料。

   * 定義為&#x200B;**multifeed**&#x200B;時，主片段可以參照（擷取）多個子片段。

### JSON預覽 {#json-preview}

若要協助您設計和開發內容片段模型，您可以預覽[JSON輸出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 學習如何搭配AEM使用GraphQL — 範例內容與查詢 {#learn-graphql-with-aem-sample-content-queries}

如需使用AEM GraphQL API的簡介，請參閱[學習如何搭配AEM使用GraphQL — 範例內容與查詢](/help/assets/content-fragments/content-fragments-graphql-samples.md) 。

## 教學課程 — 開始使用AEM無周邊和GraphQL

尋找實作教學課程？ 查看[開始使用AEM無周邊和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端對端教學課程，說明如何在無周邊CMS情境下，使用AEM GraphQL API建置和公開內容，並供外部應用程式使用。
