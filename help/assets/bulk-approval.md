---
title: 查看資料夾資產和集合
description: 設定資料夾或集合中資產的審閱工作流，並與審閱人或創意合作夥伴共用以尋求反饋。
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# 查看資料夾資產和集合 {#review-folder-assets-and-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | 本文 |

設定資料夾或集合中資產的審閱工作流，並與審閱人或創意合作夥伴共用以尋求反饋。

[!DNL Adobe Experience Manager Assets] 允許您為資料夾或集合中的資產設定臨時審閱工作流，並與審閱人或創意合作夥伴共用該工作流以尋求反饋。

您可以將審閱工作流與項目關聯或建立獨立的審閱任務。

共用資產後，審閱人可以批准或拒絕這些資產。 在工作流的各個階段發送通知，以通知目標接收者有關各種任務的完成。 例如，當您共用資料夾或集合時，審閱者會收到一則通知，表明已共用了資料夾/集合以供審閱。

審閱者完成審閱（批准或拒絕資產）後，您將收到審閱完成通知。

## 為資料夾建立審閱任務 {#creating-a-review-task-for-folders}

1. 從 [!DNL Assets] 用戶介面，選擇要為其建立審閱任務的資料夾。
1. 在工具欄中，按一下 **[!UICONTROL 建立審閱任務]** ![建立審閱任務](assets/do-not-localize/create-review-task.png) 開啟 **[!UICONTROL 審閱任務]** 的子菜單。 如果在工具欄中看不到該選項，請按一下 **[!UICONTROL 更多]** ，然後選擇該選項。

1. （可選） **[!UICONTROL 項目]** 清單中，選擇要與審閱任務關聯的項目。 預設情況下， **[!UICONTROL 無]** 的雙曲餘切值。 如果不想將任何項目與審閱任務關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您具有編輯器級別權限（或更高權限）的項目在 **[!UICONTROL 項目]** 清單框。

1. 輸入審閱任務的名稱，然後從 **[!UICONTROL 分配給]** 清單框。

   >[!NOTE]
   >
   >選定項目的成員/組可作為批准者在 **[!UICONTROL 分配給]** 清單框。

1. 輸入複查任務的說明、任務優先順序和到期日。

   ![任務詳細資訊](assets/task_details.png)

1. 在「高級」頁籤中，輸入要用於建立URI的標籤。

   ![review_name](assets/review_name.png)

1. 按一下 **[!UICONTROL 提交]**，然後按一下 **[!UICONTROL 完成]** 關閉確認消息。 新任務的通知將發送給批准者。
1. 登錄到 [!DNL Assets] 作為批准者並導航至 [!DNL Assets] UI。 要批准資產，請按一下 **[!UICONTROL 通知]** 然後從清單中選擇審閱任務。

   ![資產通知](assets/aemAssetsNotification.png)

1. 在 **[!UICONTROL 審閱任務]** 頁，檢查審閱任務的詳細資訊，然後按一下 **[!UICONTROL 審閱]**。
1. 在 **[!UICONTROL 審閱任務]** 頁，選擇資產，然後按一下 **[!UICONTROL 批准/拒絕]** 批准或拒絕。

   ![審閱任務](assets/review_task.png)

1. 按一下 **[!UICONTROL 完成]** 的子菜單。 在對話框中，輸入注釋，然後按一下  **[!UICONTROL 完成]** 確認。
1. 導航到 [!DNL Assets] 開啟資料夾。 資產的審批狀態表徵圖顯示在卡視圖和清單視圖中。

   **卡視圖**

   ![查看卡視圖中顯示的狀態](assets/chlimage_1-404.png)

   **清單視圖**

   ![查看清單視圖中顯示的狀態](assets/review_status_listview.png)

## 為集合建立審閱任務 {#creating-a-review-task-for-collections}

1. 從「收集」頁中，選擇要為其建立審閱任務的收集。
1. 在工具欄中，按一下 **[!UICONTROL 建立審閱任務]** ![建立審閱任務](assets/do-not-localize/create-review-task.png) 開啟 **[!UICONTROL 審閱任務]** 的子菜單。 如果在工具欄上看不到選項，請按一下 **[!UICONTROL 更多]** ，然後選擇該選項。

1. （可選） **[!UICONTROL 項目]** 清單中，選擇要與審閱任務關聯的項目。 預設情況下， **[!UICONTROL 無]** 的雙曲餘切值。 如果不想將任何項目與審閱任務關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您具有編輯器級別權限（或更高權限）的項目在 **[!UICONTROL 項目]** 清單框。

1. 輸入審閱任務的名稱，然後從 **[!UICONTROL 分配給]** 清單框。

   >[!NOTE]
   >
   >選定項目的成員/組可作為批准者在 **[!UICONTROL 分配給]** 清單框。

1. 輸入複查任務的說明、任務優先順序和到期日。

   ![task_details_collection](assets/task_details-collection.png)

1. 按一下 **[!UICONTROL 提交]**，然後按一下 **[!UICONTROL 完成]** 關閉確認消息。 新任務的通知將發送給批准者。
1. 登錄到 [!DNL Assets] 作為批准者並導航至 [!DNL Assets] 控制台。 要批准資產，請按一下 **[!UICONTROL 通知]** 然後從清單中選擇審閱任務。
1. 在 **[!UICONTROL 審閱任務]** 頁，檢查審閱任務的詳細資訊，然後按一下 **[!UICONTROL 審閱]**。
1. 集合中的所有資產都可在審閱頁面上看到。 選擇資產並按一下 **[!UICONTROL 批准/拒絕]** 批准或拒絕資產。

   ![review_task_collection](assets/review_task_collection.png)

1. 按一下 **[!UICONTROL 完成]** 的子菜單。 在對話框中，輸入注釋，然後按一下 **[!UICONTROL 完成]** 確認。
1. 導航到「集合」控制台並開啟集合。 資產的批准狀態表徵圖將同時顯示在「卡」和「清單」視圖中。

   ![集合_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *圖：卡視圖。*

   ![集合_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *圖：清單視圖。*
