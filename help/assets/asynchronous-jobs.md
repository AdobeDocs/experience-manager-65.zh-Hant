---
title: 非同步操作
description: AEM Assets會以非同步方式完成一些耗資龐大的工作，以最佳化效能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 非同步操作 {#asynchronous-operations}

為了降低對效能的不利影響，Adobe Experience Manager(AEM)Assets會非同步處理某些長期執行且資源密集的資產作業。

這些操作包括：

* 刪除許多資產
* 移動許多資產或資產，並附上許多參照
* 大量匯出／匯入資產中繼資料。
* 從遠端AEM部署擷取高於臨界值限制設定的資產。

非同步處理包括將多個作業入隊並最終以串列方式運行這些作業（取決於系統資源的可用性）。

您可以從「非同步作業狀態」頁面查看非 **[!UICONTROL 同步作業的狀態]** 。

>[!NOTE]
>
>依預設，AEM Assets中的工作會並行執行。 如果N是CPU內核數，則預設情況下，N/2個作業可以並行運行。 若要使用作業佇列的自訂設定，請從Web主控台修 **[!UICONTROL 改「非同步作業預設佇列]** 」設定。 如需詳細資訊，請參 [閱佇列設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)。

## 監視非同步操作的狀態 {#monitoring-the-status-of-asynchronous-operations}

每當AEM Assets以非同步方式處理作業時，您都會在收件匣及透過電子郵件收到通知。

要詳細查看非同步操作的狀態，請定位至「非同步作業狀 **[!UICONTROL 態」頁]** 。

1. 點選／按一下AEM標誌，然後前往「 **[!UICONTROL Operations]** > **[!UICONTROL Jobs」]**。
1. 在「非同 **[!UICONTROL 步作業狀態]** 」頁中，查看操作的詳細資訊。

   ![非同步操作的狀態和詳細資訊](assets/AsyncOperation-status.png)

   要確定特定操作的進度，請參閱「狀態」( **[!UICONTROL Status]** )列中的值。 視進度而定，會顯示下列狀態之一：

   * **[!UICONTROL 活動]**:正在處理操作

   * **[!UICONTROL 成功]**:操作完成

   * **[!UICONTROL 失敗]** 或 **[!UICONTROL 錯誤]**:無法處理操作

   * **[!UICONTROL 已排程]**:該操作已排程以便稍後處理

1. 要停止活動操作，請從清單中選擇該操作，然後從工具欄 **[!UICONTROL 中按一下]** 「停止」。

   ![stop_icon](assets/stop_icon.png)

1. 要查看額外詳細資訊（例如說明和日誌），請選擇操作並從工具欄中點 **[!UICONTROL 選]** 「開啟」。

   ![open_icon](assets/open_icon.png)

   此時將顯示作業詳細資訊頁。

   ![job_details](assets/job_details.png)

1. 要從清單中刪除操作，請從工具欄 **[!UICONTROL 中選擇]** 「刪除」。 若要下載CSV檔案中的詳細資訊，請點選「下 **[!UICONTROL 載」]**。

   >[!NOTE]
   >
   >如果作業的狀態為活動或排隊，則不能刪除作業。

## 清除完成的作業 {#purging-completed-jobs}

AEM Assets每天在上午1:00執行清除工作，以刪除已完成的超過一天的非同步工作。

您可以修改清除作業的計畫以及刪除完成作業之前保留其詳細資訊的持續時間。 您也可以設定在任何時間點保留詳細資料的已完成作業數上限。

1. 點選／按一下AEM標誌，然後前往「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**」。
1. 開啟 **[!UICONTROL Adobe CQ DAM非同步作業清除排程作業]** 。
1. 指定刪除已完成作業的閾值天數，以及保留歷史記錄中詳細資料的作業的最大天數。

   ![用於調度非同步作業清除的配置](assets/configmgr_purge_asyncjobs.png)

1. 儲存變更。

## 設定非同步處理的臨界值 {#configuring-thresholds-for-asynchronous-processing}

您可以設定AEM Assets的資產或參考臨界值數目，以非同步方式處理特定作業。

### 配置非同步刪除操作的閾值 {#configuring-thresholds-for-asynchronous-delete-operations}

如果要刪除的資產或檔案夾數量超過臨界值數目，則會非同步執行刪除作業。

1. 點選／按一下AEM標誌，然後前往「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**」。
1. 在Web控制台中，開啟「非同步刪 **[!UICONTROL 除操作作業處理」配置]** 。
1. 在「資 **[!UICONTROL 產的臨界值數目]** 」方塊中，指定資產／資料夾的臨界值數目，以便非同步處理刪除作業。

   ![delete_threshold](assets/delete_threshold.png)

1. 儲存變更。

### 配置非同步移動操作的閾值 {#configuring-thresholds-for-asynchronous-move-operations}

如果要移動的資產／資料夾或參考數量超過閾值數量，將非同步執行移動操作。

1. 點選／按一下AEM標誌，然後前往「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**」。
1. 從Web控制台中，開啟「非同步移 **[!UICONTROL 動操作作業處理」配置]** 。
1. 在「資 **[!UICONTROL 產／參考的臨界值數]** 」方塊中，指定資產／資料夾或參考的臨界值數，以便非同步處理移動作業。

   ![move_threshold](assets/move_threshold.png)

1. 儲存變更。
