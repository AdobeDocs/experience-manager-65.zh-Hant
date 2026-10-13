---
title: 建立內容片段模型Headless快速入門手冊
description: 定義您建立的內容結構，並使用內容片段模型透過Adobe Experience Manager (AEM) Headless功能提供。
exl-id: 653e35c9-7b6a-49ae-b55d-af2ec40e257d
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
source-wordcount: '478'
ht-degree: 51%
---
# 建立內容片段模型Headless快速入門手冊 {#creating-content-fragment-models}

定義您建立的內容結構，並使用內容片段模型透過Adobe Experience Manager (AEM) Headless功能提供。

## 什麼是內容片段模型？ {#what-are-content-fragment-models}

[現在您已經建立設定，](create-configuration.md)您可以使用它來建立內容片段模型。

內容片段模型定義您在 AEM 中建和管理之資料和內容的結構。 它們做為您內容的支架。 選擇建立內容時，您的作者會從您定義的內容片段模型中進行選擇，這會指引他們建立內容。

## 如何建立內容片段模型 {#how-to-create-a-content-fragment-model}

資訊架構師只會在需要新模型時偶爾執行這些任務。 就本快速入門手冊而言，您只會建立一個模型。

1. 登入AEM，從主功能表選取&#x200B;**工具> Assets >內容片段模型**。
1. 按一下透過建立設定所建立的資料夾。

   ![模型資料夾](assets/models-folder.png)
1. 按一下「**建立**」。
1. 提供&#x200B;**模型標題**、**標籤**&#x200B;和&#x200B;**描述**。 您也可以選擇/取消選擇&#x200B;**啟用模型** 以控制模型是否在建立時立即啟用。

   ![建立模型](assets/models-create.png)
1. 在確認視窗中，按一下&#x200B;**開啟**&#x200B;以設定您的模型。

   ![確認視窗](assets/models-confirmation.png)
1. 使用&#x200B;**內容片段模型編輯器**，從&#x200B;**資料類型**&#x200B;欄拖放欄位，來建立您的內容片段模型。

   ![拖放欄位](assets/models-drag-and-drop.png)

1. 放入欄位後，您必須設定其屬性。 編輯器會自動切換到新增欄位的&#x200B;**屬性**&#x200B;標籤，您可以在其中提供必要欄位。

   ![設定屬性](assets/models-configure-properties.png)
1. 當您完成模型建立時，請按一下[儲存]。**&#x200B;**

1. 新建立之模型的模式取決於在建立模型時是否選取&#x200B;**啟用模型**：
   * 已選取 — 新模型已&#x200B;**啟用**
   * 未選取 - 新模型會以&#x200B;**草稿**&#x200B;模式建立

1. 如果尚未啟用，模型必須&#x200B;**啟用**&#x200B;才能使用。
   1. 選取您建立的模型，然後按一下[啟用]。**&#x200B;**

      ![啟用模型](assets/models-enable.png)
   1. 點選或按一下確認對話框中的&#x200B;**啟用**&#x200B;以確認要啟用模型。

      ![啟用確認對話框](assets/models-enabling.png)
1. 該模型現已啟用並可以使用。

   ![模型已啟用](assets/models-enabled.png)

**內容片段模型編輯器**&#x200B;支援許多不同的資料型別，例如簡單文字欄位、資產參考、參考其他模型和JSON資料。

您可以建立多個模型。 模型可以參考其他內容片段。 使用[設定](create-configuration.md)來組織您的模型。

## 後續步驟 {#next-steps}

現在您已透過建立模型來定義內容片段的結構，您可以移至快速入門手冊的第三部分，並[建立您用來儲存片段的資料夾。](create-assets-folder.md)

>[!TIP]
>
>如需內容片段模型的完整詳細資訊，請參閱[內容片段模型檔案](/help/assets/content-fragments/content-fragments-models.md)
