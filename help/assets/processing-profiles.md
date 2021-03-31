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
role: 業務從業人員、管理員
feature: 工作流程，資產管理，轉譯
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---


# 處理中繼資料、影像和視訊的設定檔{#profiles-for-processing-metadata-images-and-videos}

描述檔是套用至上傳至資料夾之資產的選項的方式。 例如，您可以指定要套用至您上傳之視訊資產的中繼資料描述檔和視訊編碼描述檔。 或者，要套用至影像資產的影像設定檔，以便正確裁切。

這些規則可包括新增中繼資料、智慧裁切影像或建立視訊編碼設定檔。 在中AEM，您可以建立三種配置檔案類型，這些配置檔案在以下連結中有詳細說明：

* [中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles)
* [影像描述檔](/help/assets/image-profiles.md)
* [視訊設定檔](/help/assets/video-profiles.md)

您必須擁有管理員權限才能建立、編輯和刪除中繼資料、影像或視訊描述檔。

建立中繼資料、影像或視訊描述檔後，您會將其指派給一或多個檔案夾，以用作新上傳資產的目的地。

關於在AEM Assets使用配置檔案的一個重要概念是，它們被分配給資料夾。 描述檔中包含中繼資料描述檔的設定，以及視訊描述檔或影像描述檔。 這些設定將處理資料夾的內容及其任何子資料夾。 因此，如何命名檔案和檔案夾、如何排列子檔案夾，以及如何處理這些檔案夾中的檔案，都會對描述檔處理這些資產的方式產生重大影響。
透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充份運用您的數位資產收集，並確保正確的檔案由正確的描述檔處理。

>[!NOTE]
>
>您從一個資料夾移至另一個資料夾的資產不會重新處理。 例如，假設您的資料夾1已為其分配了配置檔案A，資料夾2已為其分配了配置檔案B。 如果您將資產從資料夾1移至資料夾2，則移動的資產會保留其從資料夾1的原始處理。
>
>即使在兩個資料夾之間移動資產時，也會有相同的設定檔指派給它。

## 正在重新處理資料夾{#reprocessing-assets}中的資產

>[!NOTE]
>
>僅適用於&#x200B;*Dynamic Media-Scene7模式*&#x200B;的6.AEM4.6.0或更高版本。

您可以在已有現有處理設定檔的資料夾中重新處理資產，您稍後會加以變更。

例如，假設您建立了影像描述檔，並將其指派給資料夾。 上傳至資料夾的任何影像資產都會自動將影像描述檔套用至資產。 不過，稍後您決定將新的智慧型裁切比例新增至描述檔。 現在，您只需執行&#x200B;*Scene7:重新處理資產*&#x200B;工作流程。

您可以對第一次處理失敗的資產執行重新處理工作流程。 因此，即使您尚未編輯處理設定檔或套用處理設定檔，您仍可隨時對資產資料夾執行重新處理工作流程。

您可以選擇調整重新處理工作流的批大小，從預設的50個資產調整到1000個資產。 運行&#x200B;_Scene7時：在資料夾上重新處理資產_&#x200B;工作流程，資產會分批分組，然後傳送至Dynamic Media伺服器進行處理。 處理後，整個批集中每個資產的中繼資料會在上更新AEM。 如果批次大小很大，您可能會遇到處理延遲。 或者，如果批量太小，則可能導致往返Dynamic Media伺服器的次數過多。

請參閱[調整重新處理工作流的批大小](#adjusting-load)。

>[!NOTE]
>
>如果要將資產從Dynamic MediaClassic批量遷移到，AEM則必須在Dynamic Media伺服器上啟用遷移複製代理。 移轉完成後，請務必停用代理。
>
>必須在Dynamic Media伺服器上禁用遷移發佈代理，以便重新處理工作流如預期般工作。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**若要重新處理資料夾中的資產**:
1. 在AEM「資產」頁面中，瀏覽至資產資料夾，該資產資料夾已指派處理設定檔，且您要套用&#x200B;**Scene7:重新處理資產**&#x200B;工作流程，

   已指派處理描述檔的檔案夾，會在「卡片檢視」的檔案夾名稱正下方顯示描述檔名稱。

1. 選擇資料夾。

   * 工作流會遞歸地考慮選定資料夾中的所有檔案。
   * 如果主要選取的檔案夾中有一個或多個子檔案夾包含資產，工作流程將重新處理檔案夾階層中的每個資產。
   * 最佳實務是，您應避免在擁有超過1000個資產的檔案夾階層上執行此工作流程。

1. 在頁面左上角附近，從下拉式清單中按一下「時間軸」。]****[!UICONTROL 
1. 在頁面左下角的「注釋」欄位右側，按一下「家樂」圖示(**^**)。

   ![重新處理資產工作流程1](/help/assets/assets/reprocess-assets1.png)

1. 按一下「啟動工作流」。]****[!UICONTROL 
1. 從&#x200B;**[!UICONTROL 開始工作流程]**&#x200B;下拉式清單中，選擇&#x200B;**[!UICONTROL Scene7:重新處理資產。]**
1. （可選）在&#x200B;**輸入工作流的標題**&#x200B;文本欄位中，輸入工作流的名稱。 如有必要，可以使用名稱來引用工作流實例。

   ![重新處理資產2](/help/assets/assets/reprocess-assets2.png)

1. 按一下&#x200B;**[!UICONTROL 開始]**，然後按一下&#x200B;**[!UICONTROL 確認。]**

   要監視工作流或檢查其進度，請從主控AEM制台頁面中按一下&#x200B;**[!UICONTROL 工具>工作流。]** 在「工作流實例」頁上，選擇工作流。在菜單欄上，按一下&#x200B;**[!UICONTROL 開啟歷史記錄。]** 您也可以終止、暫停或重新命名同一「工作流實例」頁中選定的工作流。

### 調整重新處理工作流的批大小{#adjusting-load}

（可選）重新處理工作流程中的預設批次大小是每個工作50個資產。 此最佳批次大小由執行重新處理之資產的平均資產大小和MIME類型所控制。 值越高，表示您在單一重新處理工作中會擁有許多檔案。 因此，處理橫幅在資AEM產上停留較長時間。 但是，如果平均檔案大小為1 MB或以下，則建議您將值增加到幾百，但不要超過1000。 如果檔案的平均大小為數百MB,Adobe建議您將批處理大小降低至10。

**（可選）調整重新處理工作流的批大小**

1. 在Experience Manager中，按一下&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;訪問全局導航控制台，然後按一下&#x200B;**[!UICONTROL 工具]**（槌子）表徵圖> **[!UICONTROL 工作流>模型。]**
1. 在「工作流模型」頁的「卡片視圖」或「清單視圖」中，選擇&#x200B;**[!UICONTROL Scene7:重新處理資產]**。

   ![「工作流模型」頁，帶有Scene7:重新處理卡片檢視中選取的資產工作流程](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具列上，按一下「**[!UICONTROL 編輯」。]** 新的瀏覽器標籤會開啟Scene7:「重新處理資產」工作流模型頁。
1. 在Scene7:重新處理「資產」工作流程頁面，靠近右上角，按一下「編輯」**[!UICONTROL 以「解除鎖定」工作流程。]**
1. 在工作流中，選擇「Scene7批上傳」元件以開啟工具欄，然後按一下工具欄上的「配置」。****

   ![Scene7批次上傳元件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批次上傳到Scene7-步驟屬性]**&#x200B;對話框中，設定以下內容：
   * 在&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;文字欄位中，視需要輸入新的職務和說明。
   * 如果您的處理常式會進入下一個步驟，請選取「**[!UICONTROL 處理常式進階]**」。
   * 在&#x200B;**[!UICONTROL Timeout]**&#x200B;欄位中，輸入外部進程超時（秒）。
   * 在&#x200B;**[!UICONTROL Period]**&#x200B;欄位中，輸入輪詢間隔（秒）以測試外部進程的完成。
   * 在&#x200B;**[!UICONTROL 批處理欄位]**&#x200B;中，輸入在Dynamic Media伺服器批處理上載作業中要處理的最大資產數(50-1000)。
   * 如果要在到達超時時提前，請選擇&#x200B;**[!UICONTROL 超時時提前]**。 如果要在超時時繼續進入收件箱，請取消選擇。

   ![屬性對話框](/help/assets/assets-dm/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批次上載到Scene7-步驟屬性]**&#x200B;對話框的右上角，按一下&#x200B;**[!UICONTROL 完成]**。

1. 在Scene7的右上角：重新處理「資產」工作流模型頁，按一下&#x200B;**[!UICONTROL Sync]**。 當您看到&#x200B;**[!UICONTROL Synced]**&#x200B;時，工作流程執行階段模型已成功同步，並可重新處理資料夾中的資產。

   ![同步化工作流程模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 關閉顯示Scene7的瀏覽器標籤：重新處理資產工作流程模型。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite.]**
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add.]** The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All.]**
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
