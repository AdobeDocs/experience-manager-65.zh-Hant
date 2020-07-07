---
title: 在中配置非同步操作 [!DNL Adobe Experience Manager]。
description: 以非同步方式完成一些資源密集型任務，以優化中的效能 [!DNL Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---


# 非同步操作 {#asynchronous-operations}

為了減少對效能的不利影響， [!DNL Adobe Experience Manger Assets] 請非同步處理某些長期運行和資源密集型資產操作。 非同步處理包括將多個任務入隊並最終以串列方式執行這些任務，這取決於系統資源的可用性。 這些操作包括：

* 刪除許多資產。
* 使用許多參照移動許多資產或資產。
* 大量匯出和匯入資產中繼資料。
* 從遠端部署擷 [!DNL Experience Manager] 取資產，超過設定的臨界值限制。 限制為資產數目。

您可以從「非同步作業狀態」頁面查看非同步 **[!UICONTROL 任務的狀態]** 。

>[!NOTE]
>
>預設情況下，任 [!DNL Assets] 務並行執行。 如果 `N` 是CPU內核數，則預設情況下， `N/2` 任務可以並行執行。 要使用任務隊列的自定義設定，請從 **[!UICONTROL Web Console]** 中修改非同步操作預設隊列配 [!UICONTROL 置]。 如需詳細資訊，請參 [閱佇列設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)。

## 監視非同步操作的狀態 {#monitoring-the-status-of-asynchronous-operations}

每當 [!DNL Assets] 以非同步方式處理操作時，您都會在收件匣中及透過 [!DNL Experience Manager] 電 [子郵件收](/help/sites-authoring/inbox.md) 到通知。 要詳細查看非同步操作的狀態，請定位至「非同步作業狀 **[!UICONTROL 態」頁]** 。

1. 在介面中 [!DNL Experience Manager] 按一下「 **[!UICONTROL 操作]** >作 **[!UICONTROL 業」]**。

1. 在「非同 **[!UICONTROL 步作業狀態]** 」頁中，查看操作的詳細資訊。

   ![非同步操作的狀態和詳細資訊](assets/AsyncOperation-status.png)

   要確定操作的進度，請參閱「狀 **[!UICONTROL 態]** 」列。 視進度而定，會顯示下列狀態之一：

   * **[!UICONTROL 活動]**: 正在處理操作。
   * **[!UICONTROL 成功]**: 操作完成。
   * **[!UICONTROL 失敗]** 或 **[!UICONTROL 錯誤]**:無法處理操作.
   * **[!UICONTROL 已排程]**: 該操作已排程，以便稍後處理。

1. 要停止活動操作，請從清單中選擇該操作，然後從工 **[!UICONTROL 具欄中]**![按一下停止表徵圖](assets/do-not-localize/stop_icon.svg) 。

1. 要查看額外詳細資訊（例如說明和日誌），請選擇操作，然後從工具 **[!UICONTROL 欄中]**![按一下Open](assets/do-not-localize/edit_icon.svg) open_icon。 此時將顯示任務詳細資訊頁。

   ![中繼資料匯入工作的詳細資訊](assets/job_details.png)

1. 要從清單中刪除操作，請從工具欄 **[!UICONTROL 中選擇]** 「刪除」。 若要下載CSV檔案中的詳細資訊，請按一下「下 **[!UICONTROL 載]**」。

   >[!NOTE]
   >
   >如果任務的狀態為活動或已排隊，則不能刪除該任務。

## 清除完成的任務 {#purge-completed-tasks}

[!DNL Experience Manager Assets] 每天01時執行清除任務，以刪除已完成的已超過一天的非同步任務。

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

您可以修改清除任務的調度以及刪除完成任務之前保留其詳細資訊的持續時間。 您也可以設定在任何時間點保留詳細資料的已完成任務數上限。

1. 在介面 [!DNL Experience Manager] 中，按一 **[!UICONTROL 下「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web主控台]**」。
1. 開啟 **[!UICONTROL Adobe CQ DAM非同步工作清除排程任務]** 。
1. 指定刪除已完成任務的天數閾值，以及歷史記錄中保留詳細資訊的最大任務數。 儲存變更。

   ![用於調度非同步任務清除的配置](assets/configmgr_purge_asyncjobs.png)

## 配置非同步刪除操作的閾值 {#configure-thresholds-for-asynchronous-delete-operations}

如果要刪除的資產或檔案夾數目超過設定的臨界值數目，則會非同步執行刪除作業。

1. 在介面 [!DNL Experience Manager] 中，按一 **[!UICONTROL 下「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web主控台]**」。
1. 從Web控 [!UICONTROL 制台]，開啟「非 **[!UICONTROL 同步刪除操作作業處理」配置]** 。
1. 在「資 **[!UICONTROL 產的臨界值數目]** 」方塊中，指定臨界值數目，以非同步刪除資產、檔案夾或參考。 儲存變更。

   ![設定要刪除資產的任務的臨界值限制](assets/delete_threshold.png)

## 配置非同步移動操作的閾值 {#configure-thresholds-for-asynchronous-move-operations}

如果要移動的資產、資料夾或引用數量超過設定的閾值數量，將非同步執行移動操作。

1. 在介面 [!DNL Experience Manager] 中，按一下「 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web主控台]**」。
1. 從Web控 [!UICONTROL 制台]，開啟「非同步移 **[!UICONTROL 動操作作業處理」配置]** 。
1. 在「資 **[!UICONTROL 產／參考的臨界值數目]** 」方塊中，指定臨界值數目，以非同步地移動資產、檔案夾或參考。 儲存變更。

   ![設定要移動資產之任務的臨界值限制](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager中設定電子郵件](/help/sites-administering/notification.md)。
>* [大量匯入和匯出資產中繼資料](/help/assets/metadata-import-export.md)。
>* [使用「連線資產」來共用來自遠端部署的DAM資產](/help/assets/use-assets-across-connected-assets-instances.md)。

