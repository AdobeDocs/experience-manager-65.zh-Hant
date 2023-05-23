---
title: 處理元資料、影像和視頻的配置檔案
description: 配置檔案一組規則，這些規則圍繞要應用於上載到資料夾的資產的選項。 指定要應用於上載的視頻資產的元資料配置檔案和視頻編碼配置檔案。 對於影像資產，還可以指定將哪些影像配置檔案應用於影像資產以使其正確裁剪。
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
role: User, Admin
feature: Workflow,Asset Management,Renditions
exl-id: 3d9367ed-5a02-43aa-abd9-24fae457d4c5
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# 用於處理元資料、影像和視頻的配置檔案{#profiles-for-processing-metadata-images-and-videos}

配置檔案是將哪些選項應用於上載到資料夾的資產的處方。 例如，您可以指定應用於上載的視頻資產的元資料配置檔案和視頻編碼配置檔案。 或者，將哪些映像配置檔案應用於映像資產以正確裁剪它們。

這些規則可以包括添加元資料、智慧裁剪影像或建立視頻編碼配置檔案。 在Adobe Experience Manager，可以建立三種類型的配置檔案，這些配置檔案在以下連結中詳細介紹：

* [中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles)
* [影像配置檔案](/help/assets/image-profiles.md)
* [視頻配置檔案](/help/assets/video-profiles.md)

您必須具有管理員權限才能建立、編輯和刪除元資料、影像或視頻配置檔案。

建立元資料、影像或視頻配置檔案後，將其分配給一個或多個資料夾，這些資料夾用作新上載資產的目標。

關於在Experience Manager Assets使用檔案的一個重要概念是將檔案分配給資料夾。 配置檔案中包括元資料配置檔案以及視頻配置檔案或影像配置檔案的形式的設定。 這些設定處理資料夾及其任何子資料夾的內容。 因此，如何命名檔案和資料夾、如何排列子資料夾以及如何處理這些資料夾中的檔案將對配置檔案處理這些資產的方式產生重大影響。
通過使用一致且適當的檔案和資料夾命名策略以及良好的元資料做法，您可以充分利用數字資產收集，並確保正確的檔案由正確的配置檔案處理。

>[!NOTE]
>
>您從一個資料夾移動到另一個資料夾的資產不會重新處理。 例如，假定您有分配了配置檔案A的資料夾1和分配了配置檔案B的資料夾2。 如果將資產從資料夾1移到資料夾2，則移動的資產將保留其從資料夾1的原始處理。
>
>即使在兩個資料夾之間移動分配了相同配置檔案的資產時也是如此。

## 重新處理資料夾中的資產 {#reprocessing-assets}

>[!NOTE]
>
>應用於 *Dynamic Media-Scene7模式* 只在Experience Manager6.4.6.0或更高版本中。

您可以在資料夾中重新處理資產，該資料夾中已有您稍後更改的現有處理配置檔案。

例如，假設您建立了「影像」配置檔案並將其分配給資料夾。 您上載到資料夾的任何映像資產都會自動將映像配置檔案應用於這些資產。 但是，稍後您決定向配置檔案添加新的智慧裁剪比率。 現在，您只需運行 *Scene7:重新處理資產* 工作流。

您可以對第一次處理失敗的資產運行重新處理工作流。 因此，即使您沒有編輯處理配置檔案或應用處理配置檔案，您仍然可以隨時在資產資料夾上運行重新處理工作流。

您可以根據需要調整重新處理工作流的批大小，從預設的50個資產調整到1000個資產。 運行 _Scene7:重新處理資產_ 工作流，資產分批分組，然後發送到Dynamic Media伺服器進行處理。 處理後，將在Experience Manager中更新整個批集中每個資產的元資料。 如果批大小較大，則處理過程可能會延遲。 或者，如果批量太小，則可能導致往返Dynamic Media伺服器的次數過多。

請參閱 [調整重新處理工作流的批大小](#adjusting-load)。

>[!NOTE]
>
>如果要從Dynamic Media Classic向Experience Manager執行大量資產遷移，則必須在Dynamic Media伺服器上啟用遷移複製代理。 遷移完成後，確保禁用代理。
>
>必須在Dynamic Media伺服器上禁用遷移發佈代理，以便重新處理工作流按預期方式工作。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**要重新處理資料夾中的資產，請執行以下操作：**

1. 在Experience Manager中，從「資產」頁導航到已為其分配了處理配置檔案並要應用其的資產資料夾 **[!UICONTROL Scene7:重新處理資產]** 工作流，

   已分配了處理配置檔案的資料夾通過「卡視圖」中資料夾名稱正下方顯示配置檔案的名稱來指示。

1. 選擇資料夾。

   * 工作流以遞歸方式考慮選定資料夾中的所有檔案。
   * 如果主選定資料夾中有一個或多個子資料夾，則工作流將重新處理資料夾層次結構中的每個資產。
   * 最佳做法是，您應避免在資產超過1000個的資料夾層次結構上運行此工作流。

1. 在頁面左上角附近，從下拉清單中選擇 **[!UICONTROL 時間軸]**。
1. 在頁面左下角的「注釋」欄位的右側，選擇克拉表徵圖( **^** )。

   ![重新處理資產工作流1](/help/assets/assets/reprocess-assets1.png)

1. 選擇 **[!UICONTROL 啟動工作流]**。
1. 從 **[!UICONTROL 啟動工作流]** 下拉清單，選擇 **[!UICONTROL Scene7:重新處理資產]**。
1. （可選）在 **輸入工作流標題** 的子菜單。 如有必要，可以使用名稱引用工作流實例。

   ![重新處理資產2](/help/assets/assets/reprocess-assets2.png)

1. 選擇 **[!UICONTROL 開始]**，然後選擇 **[!UICONTROL 確認]**。

   要監視工作流或檢查其進度，請從Experience Manager主控制台頁面選擇 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]**。 在「工作流實例」(Workflow Instances)頁面上，選擇一個工作流。 在菜單欄上，選擇 **[!UICONTROL 開啟歷史記錄]**。 您也可以從同一「工作流實例」頁終止、掛起或更名選定的工作流。

### 調整重新處理工作流的批大小 {#adjusting-load}

（可選）重新處理工作流中的預設批大小為每個作業50個資產。 此最佳批處理大小受運行重新處理的資產的平均資產大小和MIME類型的控制。 值越高，表示您在單個重新處理作業中擁有許多檔案。 因此，處理標語在Experience Manager資產上停留的時間更長。 但是，如果平均檔案大小較小（1 MB或更小）,Adobe建議您將值增加到幾個100，但最多不超過1000。 如果平均檔案大小很大，例如數百MB，則Adobe建議您將批大小最小設定為10。

**要（可選）調整重新處理工作流的批大小，請執行以下操作：**

1. 在Experience Manager中，選擇 **[!UICONTROL Adobe Experience Manager]** 要訪問全局導航控制台，請選擇 **[!UICONTROL 工具]** （錘子）表徵圖> **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在「工作流模型」頁面的「卡視圖」或「清單視圖」中，選擇 **[!UICONTROL Scene7:重新處理資產]**。

   ![「工作流模型」頁，帶有Scene7:在「卡視圖」中選擇的「重新處理資產」工作流](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具欄上，選擇 **[!UICONTROL 編輯]**。 新瀏覽器頁籤開啟Scene7:重新處理「資產」工作流模型頁。
1. 在Scene7:重新處理「資產」工作流頁，靠近右上角，選擇 **[!UICONTROL 編輯]** 「解鎖」工作流。
1. 在工作流中，選擇「Scene7批上載」元件以開啟工具欄，然後選擇 **[!UICONTROL 配置]** 的上界。

   ![Scene7批上載元件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在 **[!UICONTROL 批上載到Scene7 — 步驟屬性]** 對話框，請設定以下內容：
   * 在 **[!UICONTROL 標題]** 和 **[!UICONTROL 說明]** 文本欄位，輸入新的職務標題和說明（如果需要）。
   * 選擇 **[!UICONTROL 處理程式高級]** 你的處理員是否會進入下一步。
   * 在 **[!UICONTROL 超時]** 欄位，輸入外部進程超時（秒）。
   * 在 **[!UICONTROL 期間]** 欄位中，輸入要test的輪詢間隔（秒）以完成外部進程。
   * 在 **[!UICONTROL 批處理欄位]**，輸入在Dynamic Media伺服器批處理上載作業中要處理的最大資產數(50-1000)。
   * 選擇 **[!UICONTROL 超時時提前]** 的子菜單。 如果希望在超時時繼續收件箱，請取消選擇。

   ![「屬性」對話框](/help/assets/assets-dm/reprocess-assets3.png)

1. 在右上角 **[!UICONTROL 批上載到Scene7 — 步驟屬性]** 對話框，選擇 **[!UICONTROL 完成]**。

1. 在Scene7右上角：重新處理資產工作流模型頁，選擇 **[!UICONTROL 同步]**。 當你看到 **[!UICONTROL 已同步]**，工作流運行時模型已成功同步並準備重新處理資料夾中的資產。

   ![同步工作流模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 關閉顯示Scene7的瀏覽器頁籤：重新處理資產工作流模型。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
