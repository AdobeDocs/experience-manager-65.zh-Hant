---
title: 建立內容片段無頭快速入門手冊
description: 了解如何使用 AEM 的內容片段來設計、建立、規劃和使用每頁自主的內容以進行無周邊傳遞。
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
source-git-commit: 7355c149500f9e5044c9ff78af208d36ee681f56
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 67%

---

# 建立內容片段無頭快速入門手冊 {#creating-content-fragments}

了解如何使用 AEM 的內容片段來設計、建立、規劃和使用每頁自主的內容以進行無周邊傳遞。

## 什麼是內容片段？ {#what-are-content-fragments}

[您已經建立資產資料夾](create-assets-folder.md)，其中可以儲存內容片段，現在您可以建立片段了！

內容片段允許您設計、建立、規劃和發佈每頁自主的內容。它們可讓您將內容準備就緒用於多個位置和多個管道。

內容片段包含結構化內容，能以 JSON 格式傳遞。

## 如何建立內容片段 {#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段來表示他們建立的內容。這將是他們在 AEM 中的主要任務。出於本快速入門指南的目的，我們只需要建立一個。

1. 登錄AEM並從主菜單選擇 **導航 — >資產**。
1. 導航到 [資料夾。](create-assets-folder.md)
1. 點擊或按一下 **建立 — >內容片段**。
1. 內容片段的建立將分兩步顯示為嚮導。 首先選擇要用於建立內容片段的模型，然後點擊或按一下 **下一個**。
   * 可用模型取決於您為內容片段建立所在資產資料夾所定義的&#x200B;[**雲端設定**](create-assets-folder.md)。
   * 如果您收到消息 `We could not find any models`，檢查資產資料夾的配置。

   ![選取內容片段模型](assets/content-fragment-model-select.png)
1. 提供 **標題**。 **說明**, **標籤** 根據需要按一下 **建立**。

   ![建立內容片段](assets/content-fragment-create.png)
1. 點擊或按一下 **開啟** 的子菜單。

   ![內容片段已建立確認](assets/content-fragment-confirmation.png)
1. 提供內容片段編輯器中內容片段的詳細資訊。

   ![內容片段編輯器](assets/content-fragment-edit.png)
1. 點擊或按一下 **保存** 或  **保存並關閉**。

內容片段可以參考其他內容片段，必要時允許巢狀內容結構。

內容片段也可以參考 AEM 中的其他資產。在建立參考的內容片段之前，[這些資產需要儲存在 AEM](/help/assets/manage-assets.md)。

## 後續步驟 {#next-steps}

現在您已經建立了一個內容片段，您可以繼續閱讀快速入門指南的最後一部分，[建立 API 要求以存取和傳遞內容片段。](create-api-request.md)

>[!TIP]
>
>有關管理內容片段的完整詳細資訊，請參閱[內容片段文件](/help/assets/content-fragments/content-fragments.md)
