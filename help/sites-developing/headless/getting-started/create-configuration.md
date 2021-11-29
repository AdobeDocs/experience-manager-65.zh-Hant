---
title: 建立配置無頭快速入門手冊
description: 建立設定，這是開始使用AEM 6.5無頭功能的第一步。
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: 8ab774b8d21dd16e4873cd39ef0175ead3f2da23
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%

---

# 建立配置無頭快速入門手冊 {#creating-configuration}

開始使用AEM 6.5中的無頭功能時，您需要先建立設定。

## 什麼是配置？ {#what-is-a-configuration}

「設定瀏覽器」提供AEM中設定的一般設定API、內容結構、解析機制。

在AEM無頭式內容管理的情境中，請將設定視為AEM內可供您建立內容模型（定義未來內容和內容片段的結構）的工作場所。 您可以有多個設定來分隔這些模型。

>[!NOTE]
>
>如果您熟悉 [完整堆疊AEM實作中的頁面範本，](/help/sites-authoring/templates.md) 配置在管理內容模型時的用法類似。

## 如何建立設定 {#how-to-create-a-configuration}

管理員只需建立一次設定，或在組織內容模型時需要新工作區時，非常自然。 為了使用本快速入門手冊，我們只需建立一個配置。

1. 登入AEM並從主功能表選取 **工具 — >常規 — >配置瀏覽器**.
1. 提供 **標題** 的URL。
   * 系統會根據標題自動產生名稱，並根據 [AEM命名慣例。](/help/sites-developing/naming-conventions.md). 它將成為存放庫中的節點名稱。
1. 勾選下列選項：
   * **內容片段模型**
   * **GraphQL持久查詢**

   ![建立設定](../assets/create-configuration.png)

1. 點選或按一下 **建立**

您可以視需要建立多個設定。 配置也可嵌套。

>[!NOTE]
>
>除了 **內容片段模型** 和 **GraphQL持久查詢** 視您的實作需求而定，可能是必要的。

## 後續步驟 {#next-steps}

使用此設定，您現在可以繼續前往快速入門手冊的第二部分，以及 [建立內容片段模型。](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
