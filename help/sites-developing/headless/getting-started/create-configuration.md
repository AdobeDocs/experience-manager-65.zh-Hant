---
title: 建立無頭配置快速入門手冊
description: 建立配置，作為6.5版無頭入門的AEM第一步。
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
source-git-commit: 7355c149500f9e5044c9ff78af208d36ee681f56
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 61%

---

# 建立無頭配置快速入門手冊 {#creating-configuration}

作為6.5中無頭入門的第AEM一步，您需要建立配置。

## 什麼是設定？ {#what-is-a-configuration}

設定瀏覽器提供一般 API、內容結構、解析機制用於 AEM 中的設定。

在 AEM 無周邊內容管理的環境中，將設定視為 AEM 中的工作區，您可以在其中建立內容模型，該內容模型定義未來內容和內容片段的結構。您可以有多個設定來將這些模型分開。

>[!NOTE]
>
>如果您熟悉[全堆疊 AEM 實作中的頁面範本](/help/sites-authoring/templates.md)，用於管理內容模型之設定的用法是類似的。

## 如何建立設定 {#how-to-create-a-configuration}

系統管理員一次只需建立一個設定，或者在需要新工作區來組織內容模型時建立，這個情況很少發生。出於本快速入門指南的目的，我們只需要建立一個設定。

1. 登錄AEM並從主菜單選擇 **工具 — >常規 — >配置瀏覽器**。
1. 提供 **標題** 的下界。
   * 名稱將根據標題自動生成，並根據 [命AEM名約定。](/help/sites-developing/naming-conventions.md)。它將成為儲存庫中的節點名稱。
1. 檢查以下選項：
   * **內容片段模型**
   * **GraphQL持久查詢**

   ![建立設定](assets/create-configuration.png)

1. 點選或按一下&#x200B;**建立**。

如果需要，您可以建立多個設定。設定也可以是巢狀。

>[!NOTE]
>
>除了 **內容片段模型** 和 **GraphQL持久查詢** 可能是必要的，具體取決於您的實施要求。

## 後續步驟 {#next-steps}

使用此設定，您現在可以繼續閱讀快速入門指南的第二部分，並[建立內容片段模型。](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
