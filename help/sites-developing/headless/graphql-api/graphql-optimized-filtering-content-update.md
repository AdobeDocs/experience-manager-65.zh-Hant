---
title: 更新您的內容片段，以達到最佳化 GraphQL 篩選
description: 了解如何更新您的內容片段，以便在 Adobe Experience Manager 中達到最佳化 GraphQL 篩選，並實現無周邊內容傳遞。
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 42%

---


# 更新您的內容片段，以達到最佳化 GraphQL 篩選 {#updating-content-fragments-for-optimized-graphql-filtering}

若要最佳化GraphQL篩選器的效能，請執行程式來更新您的內容片段。

>[!NOTE]
>
>更新您的內容片段後，您可以遵循的建議 [最佳化GraphQL查詢](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## 必備條件 {#prerequisites}

確保您至少擁有6.5.17.0版的AEM。

## 更新您的內容片段 {#updating-content-fragments}

若要執行此程式，請使用下列步驟：

1. [設定OSGi設定](/help/sites-deploying/configuring-osgi.md) 的 **內容片段移轉工作設定**：

   ![OSGi內容片段移轉工作設定](assets/cfm-graphql-update-01.png "OSGi內容片段移轉工作設定")

1. 在對話方塊中，設定這兩個引數如下：

   * **ContentFragmentMigration：Enabled** ： `1`
   * **ContentFragmentMigration：強制** ： `1`

1. **儲存** 規格 — 更新程式開始。

1. 等候程式完成。 當屬性為 `cfGlobalVersion` 顯示於 `/content/dam` 且已設為 `1`.

1. 返回OSGi設定以停用程式。

   在的對話方塊中 **內容片段移轉工作設定** 請依照以下方式設定這兩個引數：

   * **ContentFragmentMigration：Enabled** ： `0`
   * **ContentFragmentMigration：強制** ： `0`

## 限制 {#limitations}

請注意下列限制：

* GraphQL 篩選器的效能最佳化只有在完全更新所有內容片段後才有可能 (由 JCR 節點 `/content/dam` 的 `cfGlobalVersion` 屬性存在來表示)

* 如果在執行更新程序後從內容套組 (使用 `crx/de`) 匯入內容片段，則在再次執行更新程序之前，GraphQL 查詢結果中不會考慮這些內容片段。