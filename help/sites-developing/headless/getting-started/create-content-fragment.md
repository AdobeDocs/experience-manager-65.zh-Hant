---
title: 建立內容片段無頭快速入門手冊
description: 了解如何使用AEM內容片段來設計、建立、組織及使用無頭式傳送的獨立於頁面的內容。
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: 8ab774b8d21dd16e4873cd39ef0175ead3f2da23
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 3%

---

# 建立內容片段無頭快速入門手冊 {#creating-content-fragments}

了解如何使用AEM內容片段來設計、建立、組織及使用無頭式傳送的獨立於頁面的內容。

## 什麼是內容片段？ {#what-are-content-fragments}

[現在您已建立資產資料夾](create-assets-folder.md) 您現在可以在其中儲存內容片段！

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 它們可讓您準備內容，以便在多個位置和多個頻道中使用。

內容片段包含結構化內容，可以以JSON格式傳送。

## 如何建立內容片段 {#how-to-create-a-content-fragment}

內容作者將建立任意數量的內容片段，以代表其建立的內容。 這將是他們在AEM中的主要工作。 為了方便閱讀快速入門手冊，我們只需建立指南。

1. 登入AEM並從主功能表選取 **導覽 — >資產**.
1. 導覽至 [檔案夾。](create-assets-folder.md)
1. 點選或按一下 **建立 — >內容片段**.
1. 建立內容片段會以精靈的形式呈現，分為兩個步驟。 首先，選取您要使用哪個模型來建立內容片段，然後點選或按一下 **下一個**.
   * 可用的模型取決於 [**雲端設定** 您為「資產」資料夾定義](create-assets-folder.md) 建立內容片段時所使用的ID。
   * 如果您收到訊息 `We could not find any models`，檢查資產資料夾的設定。

   ![選取內容片段模型](../assets/content-fragment-model-select.png)
1. 提供 **標題**, **說明**，和 **標籤** 視需要，點選或按一下 **建立**.

   ![建立內容片段](../assets/content-fragment-create.png)
1. 點選或按一下 **開啟** 在確認窗口中。

   ![內容片段已建立確認](../assets/content-fragment-confirmation.png)
1. 在內容片段編輯器中提供內容片段的詳細資訊。

   ![內容片段編輯器](../assets/content-fragment-edit.png)
1. 點選或按一下 **儲存** 或  **儲存並關閉**.

內容片段可參考其他內容片段，以視需要允許巢狀內容結構。

內容片段也可以參考AEM中的其他資產。 [這些資產需要儲存在AEM](/help/assets/manage-assets.md) 建立參考內容片段之前。

## 後續步驟 {#next-steps}

現在您已建立內容片段，可以繼續前往快速入門手冊的最後部分，以及 [建立API請求以存取及傳送內容片段。](create-api-request.md)

>[!TIP]
>
>如需管理內容片段的完整詳細資訊，請參閱 [內容片段檔案](/help/assets/content-fragments/content-fragments.md)
