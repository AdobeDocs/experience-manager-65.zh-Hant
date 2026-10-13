---
title: 在 AEM 中管理 GraphQL 端點
description: 瞭解如何在Adobe Experience Manager中管理GraphQL端點以進行Headless內容傳送。
exl-id: a59a5e50-0787-4c1c-a83d-bb3eac1479a8
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
source-wordcount: '510'
ht-degree: 90%
---
# 在 AEM 中管理 GraphQL 端點 {#graphql-aem-endpoint}

端點是用於存取 AEM GraphQL 的路徑。 使用此路徑，您 (或您的應用程式) 可以：

* 存取 GraphQL 結構描述，
* 傳送您的 GraphQL 查詢，
* 接收 (對您的 GraphQL 查詢) 的回應。

在 AEM 有兩種端點類型：

* 全域
  * 可供所有網站使用。
  * 此端點可以使用來自所有 Sites 設定的所有內容片段模型 (在[設定瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中定義)。
  * 如果內容片段模型應該在 Sites 設定之間共用，則應在全域 Sites 設定下建立該模型。
* Sites 設定：
  * 對應至[設定瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中定義的 Sites 設定。
  * 專屬於指定的網站/專案。
  * Sites 設定專屬端點將使用來自該特定 Sites 設定的內容片段模型以及來自全域 Sites 設定的內容片段模型。

>[!CAUTION]
>
>內容片段編輯器可以允許一個 Sites 設定的內容片段參考另一個 Sites 設定的內容片段 (透過原則)。
>
>在這種情況下，並非所有內容都可以使用 Sites 設定專屬端點進行擷取。
>
>內容作者應該控制這種情況；例如，考慮將共用的內容片段模型放在全域 Sites 設定下可能會有用。

AEM 全域端點的 GraphQL 存放庫路徑：

`/content/cq:graphql/global/endpoint`

為此，您的應用程式可以在要求 URL 中使用以下路徑：

`/content/_cq_graphql/global/endpoint.json`

若要啟用 AEM GraphQL 端點，您需要：

* [啟用您的 GraphQL 端點](#enabling-graphql-endpoint)
* [發佈您的 GraphQL 端點](#publishing-graphql-endpoint)

## 啟用 GraphQL 端點 {#enabling-graphql-endpoint}

若要啟用 GraphQL 端點，您首先需要有適當的設定。 請參閱[內容片段 - 設定瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果[尚未啟用使用內容片段模型](/help/assets/content-fragments/content-fragments-configuration-browser.md)，則&#x200B;**建立**&#x200B;選項將無法使用。

若要啟用對應的端點：

1. 導覽至&#x200B;**工具**、**Assets**，然後選取&#x200B;**GraphQL**。
1. 選取「**建立**」。
1. **建立新的 GraphQL 端點**&#x200B;對話框隨即開啟。 您可以在這裡指定：
   * **名稱**：端點名稱，您可以輸入任何文字。
   * **使用以下方式提供的 GraphQL 結構描述**：使用下拉選單選取所需的網站/專案。

   >[!NOTE]
   >
   >下列警告會顯示在對話方塊中：
   >
   >* *如果未妥善管理，GraphQL 端點可能會導致資料安全性和效能問題。 在建立端點之後，請確定設定適當的許可權。*

1. 使用&#x200B;**建立**&#x200B;確認。
1. **後續步驟** 對話框將提供安全性主控台的直接連結，以便您可以確保新建立的端點具有合適的權限。

   >[!CAUTION]
   >
   >每個人都可以存取此端點。 這可能帶來安全性問題，尤其是在發佈執行個體上，因為 GraphQL 查詢會給伺服器帶來沉重的負載。
   >
   >您可以在端點上設定適合您使用案例的 ACL。

## 發佈您的 GraphQL 端點 {#publishing-graphql-endpoint}

選取新端點並&#x200B;**發佈**，使其在所有環境中完全可用。

>[!CAUTION]
>
>每個人都可以存取此端點。
>
>這可能為發佈執行個體帶來安全性問題，因為 GraphQL 查詢會給伺服器帶來沉重的負載。
>
>在端點上設定適合您使用案例的ACL。
