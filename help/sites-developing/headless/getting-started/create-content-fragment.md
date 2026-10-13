---
title: 建立內容片段Headless快速入門手冊
description: 了解如何使用 AEM 的內容片段來設計、建立、規劃和使用每頁自主的內容以進行 Headless 傳遞。
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
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
source-wordcount: '378'
ht-degree: 60%
---
# 建立內容片段Headless快速入門手冊 {#creating-content-fragments}

了解如何使用 AEM 的內容片段來設計、建立、規劃和使用每頁自主的內容以進行 Headless 傳遞。

## 什麼是內容片段？ {#what-are-content-fragments}

[您已經建立資產資料夾](create-assets-folder.md)，其中可以儲存內容片段，現在您可以建立片段了！

內容片段可讓您設計、建立、策劃和發佈不受頁面影響的內容。 可讓您準備內容以用於多個位置和多個管道。

內容片段包含結構化內容，能以 JSON 格式傳遞。

## 如何建立內容片段 {#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段來表示他們建立的內容。 這將是他們在 AEM 中的主要任務。 出於本快速入門指南的目的，我們只需要建立一個。

1. 登入AEM，從主功能表選取&#x200B;**導覽> Assets**。
1. 導覽至您先前建立的[資料夾。](create-assets-folder.md)
1. 按一下&#x200B;**建立>內容片段**。
1. 內容片段的建立以兩步驟的精靈呈現。 請先選取您要使用哪個模式來建立內容片段，然後按一下[下一步]。****
   * 可用模型取決於您為內容片段建立所在資產資料夾所定義的&#x200B;[**雲端設定**](create-assets-folder.md)。
   * 如果您收到訊息`We could not find any models`，請檢查資產資料夾的設定。

   ![選取內容片段模型](assets/content-fragment-model-select.png)
1. 視需要提供&#x200B;**標題**、**描述**&#x200B;和&#x200B;**標籤**，然後按一下&#x200B;**建立**。

   ![建立內容片段](assets/content-fragment-create.png)
1. 在確認視窗中按一下&#x200B;**開啟**。

   ![已建立的內容片段確認](assets/content-fragment-confirmation.png)
1. 在內容片段編輯器中提供內容片段的詳細資訊。

   ![內容片段編輯器](assets/content-fragment-edit.png)
1. 按一下&#x200B;**儲存**&#x200B;或&#x200B;**儲存並關閉**。

內容片段可以參考其他內容片段，必要時允許巢狀內容結構。

內容片段也可以參考 AEM 中的其他資產。 在建立參考的內容片段之前，[這些資產需要儲存在 AEM](/help/assets/manage-assets.md)。

## 後續步驟 {#next-steps}

現在您已經建立了一個內容片段，您可以繼續閱讀快速入門指南的最後一部分，[建立 API 要求以存取和傳遞內容片段。](create-api-request.md)

>[!TIP]
>
>如需有關管理內容片段的完整詳細資訊，請參閱[內容片段文件](/help/assets/content-fragments/content-fragments.md)
