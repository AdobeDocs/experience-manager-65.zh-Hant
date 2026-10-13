---
title: AEM Headful 和 Headless 技術
description: AEM 專案可以在 Headful 和 Headless 模型中實作，但這不必是二選一。 AEM 提供了在一個專案中利用兩種模型優勢的靈活性。
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 75%
---
# AEM Headful 和 Headless 技術 {#headful-headless}

Adobe Experience Manager 專案可以在 Headful 和 Headless 模型中實作，但這不必是二選一。 AEM 提供了在一個專案中利用兩種模型優勢的靈活性。 本檔案提供不同模型的概觀，並說明SPA整合的等級。

## 概觀 {#overview}

AEM 提供了強大的工具來在單一平台管理內容的建立和傳遞。 這是內容管理的傳統「 Headful 」模型，內容作者和開發人員在同一個平台上工作，將體驗傳遞給內容取用者。

AEM 還可用於簡單地管理內容，允許由另一個平台管理內容的呈現和傳遞作業。 這是內容管理的「 Headless 」模型，內容作者和開發人員在不同平台上工作，將體驗傳遞給內容取用者。

但這不需要是二選一的選擇。 AEM 提供了前所未有的靈活性，使您能夠在專案中利用這兩種模型的優勢。

![AEM 實作模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

在Headful或完整棧疊模式中，內容是在AEM存放庫中管理的，而根據Java、HTL等的AEM元件是用來呈現內容以供使用者體驗。 在此模型中，內容的建立、樣式設定、內容的呈現和傳遞都在 AEM 中進行。

在 Headless 模型中，內容在 AEM 存放庫中管理，但透過 REST 和 GraphQL 等 API 傳遞到另一個系統以呈現內容以提供使用者體驗。 在此模型中，內容是在 AEM 中建立，但樣式設定、內容的呈現和傳遞都在另一個平台進行。

單頁應用程式 (SPA) 通常是 AEM Headless 傳遞內容的目的地。 但是，這些 SPA 不需要完全在 AEM 外部。 AEM 可讓您決定您的 SPA 整合到 AEM 中的程度。 讓我們舉個例子。

## 網路商店範例 {#web-shop-example}

假設您的公司有一個網路商店 SPA。 其中包含所有產品詳細資料和影像。 然後，您導入 AEM 以推動您的行銷工作，例如促銷網站、部落格和活動內容。 如何整合這兩者？ AEM 提供一系列選項：

* **允許系統獨立運作。**
* **透過GraphQL從AEM提供有限內容的網路商店。** 內容可由AEM中的作者建立，但只能透過網路商店SPA檢視。
* **在AEM中內嵌網站商店SPA。** 內容可由AEM中的作者建立，以及在AEM中的網頁商店內容中檢視，但無法操作。
* **在AEM中內嵌網站商店SPA，並啟用可編輯的點。** 內容可由AEM中的作者建立，並在AEM的網頁商店環境中檢視，且作者在AEM中操控網頁商店SPA內容的能力有限。
* **在AEM中內嵌網站商店SPA，並啟用整個區域以進行編輯。** 內容可由AEM中的作者建立，並在AEM的網頁商店環境中檢視，且作者在AEM中操控網頁商店SPA內容的能力有限。

下一節將更詳細地探討這些整合層級。

>[!NOTE]
>
>當然，您也可以使用AEM SPA Editor架構，將Web Shop SPA重新實作為功能齊全的AEM SPA [。](/help/sites-developing/spa-walkthrough.md) 如果您已有AEM，且想要建立網站商店或其他SPA，建議使用此方法，但此檔案不在此範圍內。

## SPA 整合層級 {#integration-levels}

SPA 整合在 AEM 中的四個層級。

* **層級 0：無整合**
  * SPA 和 AEM 個別存在，不交換任何資訊。
  * 內容在兩個不同系統中獨立建立、管理和傳遞。
* **層級 1：內容片段整合**
  * [內容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用於建立和管理有限內容供 SPA 使用。
  * SPA 透過 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 擷取此內容
  * 有些內容在 AEM 中管理，有些在外部系統中管理。
  * 內容只能在 SPA 中查看。
* **層級 2：將 SPA 嵌入 AEM**
  * [內容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用於建立和管理內容供 SPA 使用。
  * SPA 透過 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 擷取此內容
  * 有些內容在 AEM 中管理，有些在外部系統中管理。
  * 可以在 AEM 中依情境查看內容。
  * 可以在 AEM 中編輯有限內容。
* **層級 3：在 AEM 中嵌入並完全啟用 SPA**
  * [內容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用於建立和管理內容供 SPA 使用。
  * SPA 透過 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 擷取此內容
  * 可以在 AEM 中依情境查看內容。
  * 大部分內容可以在 AEM 中編輯。

層級 1 是典型 Headless 實作的範例。 但是，內容作者只能在 SPA 中依情境查看他們的內容。 AEM 只是一種編寫工具。

AEM 的優勢和靈活性在層級 2 和層級 3 變得顯著，同時仍保留 SPA 的優勢。 內容作者可以在 AEM 中建立內容，也可以在 AEM 中依情境查看內容。 SPA 可在 AEM 中加以編寫，但仍做為 SPA 傳遞。

## 實作整合層級 {#implementing}

AEM 中有不同的工具可用，取決於您選擇的整合層級。 每個層級都建立在之前使用的工具之上。 以下清單連結到相關資源。

* **層級 1：** 內容片段和 [AEM Headless 架構](/help/sites-developing/headless/introduction.md)可用於將 AEM 內容傳遞到 SPA。
* **層級 2：** 除了層級 1：
  * [RemotePage 元件](/help/sites-developing/spa-remote-page.md) 可用於將外部 SPA 嵌入到 AEM 中，AEM 內容可在情境中查看。
  * 還可以啟用 SPA 上的某些點以[允許在 AEM 中進行有限編輯。](/help/sites-developing/spa-edit-external.md)
* **層級 3：** 除了層級 2：
  * 可以啟用 SPA 的整個區域以允許在 AEM 中進行全面編輯。
