---
title: 處理中繼資料、影像和視訊的設定檔
description: 描述檔，是一組規則，其中包含要套用至上傳至資料夾之資產的選項。 指定要套用至您上傳之視訊資產的中繼資料描述檔和視訊編碼描述檔。 對於影像資產，您也可以指定要套用至影像資產的影像設定檔，以便正確裁切。
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 處理中繼資料、影像和視訊的設定檔{#profiles-for-processing-metadata-images-and-videos}

描述檔是套用至上傳至資料夾之資產的選項的方式。 例如，您可以指定要套用至您上傳之視訊資產的中繼資料描述檔和視訊編碼描述檔。 或者，要套用至影像資產的影像設定檔，以便正確裁切。

這些規則可包括新增中繼資料、智慧裁切影像或建立視訊編碼設定檔。 在AEM中，您可以建立三種描述檔類型，這些描述檔在下列連結中有詳細說明：

* [中繼資料設定檔](/help/assets/metadata-profiles.md)
* [影像描述檔](/help/assets/image-profiles.md)
* [視訊設定檔](/help/assets/video-profiles.md)

您必須擁有管理員權限才能建立、編輯和刪除中繼資料、影像或視訊描述檔。

建立中繼資料、影像或視訊描述檔後，您會將其指派給一或多個檔案夾，以用作新上傳資產的目的地。

在AEM Assets中使用描述檔的重要概念是，這些描述檔會指派給檔案夾。 描述檔中包含中繼資料描述檔的設定，以及視訊描述檔或影像描述檔。 這些設定將處理資料夾的內容及其任何子資料夾。 因此，如何命名檔案和檔案夾、如何排列子檔案夾，以及如何處理這些檔案夾中的檔案，都會對描述檔處理這些資產的方式產生重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充份運用您的數位資產收集，並確保正確的檔案由正確的描述檔處理。

>[!NOTE]
>
>您從一個資料夾移至另一個資料夾的資產不會重新處理。 例如，假設您的資料夾1已為其分配了配置檔案A，資料夾2已為其分配了配置檔案B。 如果您將資產從資料夾1移至資料夾2，則移動的資產會保留其從資料夾1的原始處理。
>
>即使在兩個資料夾之間移動資產時，也會有相同的設定檔指派給它。

## 重新處理資料夾中的資產 {#reprocessing-assets}

>[!NOTE]
>
>僅適用於 *AEM 6.4.6.0或更新版本的Dynamic Media - Scene7模式* 。

您可以在已有現有處理設定檔的資料夾中重新處理資產，而您稍後會加以變更。

例如，假設您建立了影像描述檔，並將其指派給資料夾。 上傳至資料夾的任何影像資產都會自動將影像描述檔套用至資產。 不過，稍後您決定將新的智慧型裁切比例新增至描述檔。 現在，您只需執行 *Scene7:重新處理資產* 工作流程。

您可以對第一次處理失敗的資產執行重新處理工作流程。 因此，即使您尚未編輯處理設定檔或套用處理設定檔，您仍可隨時對資產資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流的批大小，從預設的50個資產調整到1000個資產。 當您執行 _Scene7時：重新處理資料夾上的_ 「資產」工作流程，資產會分批分組，然後傳送至Dynamic Media伺服器進行處理。 在處理後，整個批次集中每個資產的中繼資料會在AEM上更新。 如果批次大小很大，您可能會遇到處理延遲。 或者，如果批次大小太小，則可能導致往返Dynamic Media伺服器的次數過多。

請參 [閱調整重新處理工作流的批大小](#adjusting-load)。

>[!NOTE]
>
>如果您要從Dynamic Media Classic將資產大量移轉至AEM，則必須在Dynamic Media伺服器上啟用Migration複製代理。 移轉完成後，請務必停用代理。
移轉發佈代理必須在Dynamic Media伺服器上停用，讓重新處理工作流程如預期般運作。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**若要重新處理資料夾中的資產**:
1. 在AEM中，從「資產」頁面導覽至資產資料夾，該資產資料夾已指派處理設定檔給該資產，且您要套用 **Scene7:重新處理資產** ,

   已指派處理描述檔的檔案夾，會在「卡片檢視」的檔案夾名稱正下方顯示描述檔名稱。

1. 選擇資料夾。

   * 工作流會遞歸地考慮選定資料夾中的所有檔案。
   * 如果主要選取的檔案夾中有一個或多個子檔案夾包含資產，工作流程將重新處理檔案夾階層中的每個資產。
   * 最佳實務是，您應避免在擁有超過1000個資產的檔案夾階層上執行此工作流程。

1. 在頁面左上角附近，從下拉式清單中按一下「時間 **[!UICONTROL 軸」]**。
1. 在頁面左下角的「注釋」欄位右側，按一下「卡拉」圖示( **^** )。

   ![重新處理資產工作流程1](/help/assets/assets/reprocess-assets1.png)

1. 按一下「 **[!UICONTROL 開始工作流程]**」。
1. 從「開 **[!UICONTROL 始工作流程]** 」下拉式清單中，選擇 **[!UICONTROL Scene7:重新處理資產]**。
1. （可選）在「輸 **入工作流的標題** 」文本欄位中輸入工作流的名稱。 如有必要，可以使用名稱來引用工作流實例。

   ![重新處理資產2](/help/assets/assets/reprocess-assets2.png)

1. 按一 **[!UICONTROL 下「開始]**」，然後按一 **[!UICONTROL 下「確認]**」。

   若要監視工作流程或檢查其進度，請從AEM主控台頁面，按一下「工具>工 **[!UICONTROL 作流程」]**。 在「工作流實例」頁上，選擇工作流。 在功能表列上，按一下「開 **[!UICONTROL 啟歷史記錄]**」。 您也可以終止、暫停或重新命名同一「工作流實例」頁中選定的工作流。

### 調整重新處理工作流的批大小 {#adjusting-load}

（可選）重新處理工作流程中的預設批次大小是每個工作50個資產。 此最佳批次大小由執行重新處理之資產的平均資產大小和MIME類型所控制。 值越高，表示您在單一重新處理工作中會擁有許多檔案。 因此，處理橫幅會在AEM資產上停留較長時間。 但是，如果平均檔案大小為1 MB或以下- adobe建議您將值增加到幾百，但不要超過1000。 如果平均檔案大小是數百兆位元組，Adobe建議您將批次大小降低至10。

**（可選）調整重新處理工作流的批大小**

1. 在Experience Manager中，點選 **[!UICONTROL Adobe Experience Manager]** ，存取全域導覽主控台，然後點選「工具 **[!UICONTROL （槌子）」圖示>「工]** 作流程>模型」 ****。
1. 在「工作流程模型」頁面的「卡片檢視」或「清單檢視」中，選取 **[!UICONTROL Scene7:重新處理資產]**。

   ![「工作流程模型」頁面與Scene7:重新處理卡片檢視中選取的資產工作流程](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具列上，按一下「編 **[!UICONTROL 輯」]**。 新的瀏覽器標籤會開啟Scene7:「重新處理資產」工作流模型頁。
1. 在Scene7:重新處理「資產」工作流程頁面，靠近右上角，點選「 **[!UICONTROL 編輯]** 」以「解除鎖定」工作流程。
1. 在工作流程中，選取「Scene7批次上傳」元件以開啟工具列，然後點選工具列 **[!UICONTROL 上的]** 「設定」。

   ![Scene7批次上傳元件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在「批 **[!UICONTROL 次上載到Scene7 —— 步驟屬性」(Batch Upload to Scene7 - Step Properties]** )對話框中，設定以下內容：
   * 在「標 **[!UICONTROL 題]** 」和「說 **** 明」文字欄位中，視需要輸入新的職稱和說明。
   * 如果您 **[!UICONTROL 的處理常式會進入下一個步驟]** ，請選取「處理常式進階」。
   * 在「超 **[!UICONTROL 時]** 」欄位中，輸入外部進程超時（秒）。
   * 在「 **[!UICONTROL 期間]** 」欄位中，輸入輪詢間隔（秒）以測試外部進程是否完成。
   * 在「批 **[!UICONTROL 次」欄位中]**，輸入動態媒體伺服器批次處理上傳工作中要處理的資產數量上限(50-1000)。
   * 如果 **[!UICONTROL 要在到達超時]** ，請選擇「超時時提前」。 如果要在到達逾時時時繼續進入收件箱，請取消選擇。
   ![屬性對話框](/help/assets/assets-dm/reprocess-assets3.png)

1. 在「批次上傳至Scene7 —— 步驟屬 **[!UICONTROL 性」對話方塊的右上角]** ，點選「 **[!UICONTROL 完成」]**。

1. 在Scene7的右上角：重新處理「資產」工作流程模型頁面，點選「 **[!UICONTROL 同步」]**。 當您看到「已 **[!UICONTROL 同步]**」時，工作流程執行階段模型已成功同步，並可重新處理資料夾中的資產。

   ![同步化工作流程模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 關閉顯示Scene7的瀏覽器標籤：重新處理資產工作流程模型。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
