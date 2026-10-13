---
title: 更新您的內容片段，以達到最佳化 GraphQL 篩選
description: 瞭解如何更新您的內容片段，以用於Adobe Experience Manager中最佳化的GraphQL篩選，以進行Headless內容傳送。
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
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
source-wordcount: '249'
ht-degree: 50%
---
# 更新您的內容片段，以達到最佳化 GraphQL 篩選 {#updating-content-fragments-for-optimized-graphql-filtering}

若要最佳化 GraphQL 篩選器的效能，可執行一個程序來更新您的內容片段。

>[!NOTE]
>
>更新內容片段後，您可以依照[最佳化 GraphQL 查詢](/help/sites-developing/headless/graphql-api/graphql-optimization.md)的建議進行。

## 先決條件 {#prerequisites}

請確定您至少有6.5.17.0個AEM版本。

## 更新您的內容片段 {#updating-content-fragments}

若要執行此程式，請使用下列步驟：

1. [設定&#x200B;**內容片段移轉工作設定**&#x200B;的OSGi設定](/help/sites-deploying/configuring-osgi.md)：

   ![OSGi內容片段移轉工作設定](assets/cfm-graphql-update-01.png "OSGi內容片段移轉工作設定")

1. 在對話方塊中，設定這兩個引數如下：

   * **ContentFragmentMigration:Enabled** ： `1`
   * **ContentFragmentMigration:Enforce** ： `1`

1. **儲存**&#x200B;規格 — 更新程式開始。

1. 請等候程式完成。 當屬性`cfGlobalVersion`出現在`/content/dam`上且設定為`1`時，程式已完成。

1. 返回OSGi設定以停用程式。

   在&#x200B;**內容片段移轉工作設定**&#x200B;的對話方塊中，設定這兩個引數如下：

   * **ContentFragmentMigration:Enabled** ： `0`
   * **ContentFragmentMigration:Enforce** ： `0`

## 限制 {#limitations}

留意以下限制：

* GraphQL 篩選器的效能最佳化只有在完全更新所有內容片段後才有可能 (由 JCR 節點 `/content/dam` 的 `cfGlobalVersion` 屬性存在來表示)

* 如果在執行更新程序後從內容套組 (使用 `crx/de`) 匯入內容片段，則在再次執行更新程序之前，GraphQL 查詢結果中不會考慮這些內容片段。
