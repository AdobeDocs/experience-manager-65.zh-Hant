---
title: 迴轉集
description: 瞭解如何在Dynamic Media處理旋轉集
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 9%

---

# 迴轉集{#spin-sets}

「旋轉集」(Spin Set)模擬轉動對象以檢查對象的真實行為。 「旋轉集」(Spin Sets)允許從任何角度查看項目，從任何角度獲取關鍵可視詳細資訊。

「旋轉集」(Spin Set)模擬360°的觀看體驗。 Dynamic Media提供單軸旋轉集，查看者可以在其中旋轉項目。 此外，用戶只需點擊幾下滑鼠即可「自由格式」縮放和平移任何視圖。 這樣，用戶就可以從特定的角度更仔細地檢查項目。

「旋轉集」由帶單詞的標題指定 **[!UICONTROL 旋轉集]**。 此外，如果發佈了旋轉集，則發佈日期由 **[!UICONTROL 世界]** 表徵圖與上次修改日期一起在標題上，由 **[!UICONTROL 鉛筆]** 表徵圖。

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>有關Assets用戶介面的資訊，請參閱 [管理資產](/help/assets/manage-assets.md)。

建立「旋轉集」時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 限制類型 | 最佳實踐 | 強加的限制 |
| --- | --- | --- |
| 每2D集的最大行/列數 | 每組12-18頁圖片 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md)。

## 快速啟動：旋轉集 {#quick-start-spin-sets}

要使用旋轉集快速啟動並運行，請執行以下步驟：

1. [上載多個視圖的影像](#uploading-assets-for-spin-sets)。

   對於一維自旋集，至少需要8-12個項的投影，對於二維自旋集，需要16-24個投影。 必須定期拍攝照片，以給出項目正在旋轉並被翻轉的印象。 例如，如果一維自旋集包含12個鏡頭，則對每個鏡頭旋轉項目30°(360/12)。

   請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 清單。

1. [建立旋轉集](#creating-spin-sets)。

   要建立旋轉集，請選擇 **[!UICONTROL 建立>旋轉集]** 然後命名集，選擇資產，然後選擇影像的顯示順序。

   請參閱 [使用選擇器](/help/assets/working-with-selectors.md)。

   >[!NOTE]
   >
   >您也可以透過批次集預設集自動 [建立回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。**重要提示：** 批集由IPS（映像生產系統）建立，作為資產接收的一部分，並且僅在Dynamic Media-Scene7模式下可用。

1. 設定 [旋轉集查看器預設](/help/assets/managing-viewer-presets.md)，根據需要。

   管理員可以建立或修改回轉集檢視器預設集。若要檢視含有檢視器預設集的回轉集，請選取該回轉集，然後在左側導軌下拉式選單中選取「檢 **視器**」。

   請參閱 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 查看器預設]** 。要使

   請參閱 [添加和編輯查看器預設](/help/assets/managing-viewer-presets.md)。

1. [查看旋轉集](#viewing-spin-sets)。

   可以以三種不同方式查看和訪問通過批集預設建立的集。 (使用批集預設建立的集，確定 *不* 顯示在用戶介面中。)

1. [預覽旋轉集](/help/assets/previewing-assets.md)。

   選擇「旋轉集」(Spin Set)，可預覽它。 旋轉旋轉集。 您可以從 **[!UICONTROL 查看者]** 菜單開啟它。

1. [發佈旋轉集](/help/assets/publishing-dynamicmedia-assets.md)。

   發佈旋轉集將激活URL和嵌入字串。 此外，您必須 [發佈查看器預設](/help/assets/managing-viewer-presets.md)。

1. [將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md) 或 [嵌入視頻或影像查看器](/help/assets/embed-code.md)。

   Adobe Experience Manager資產為旋轉集建立URL調用，並在發佈旋轉集後激活它們。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們嵌入到您的網站中。

   選取「回轉集」，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   請參閱 [將旋轉集連結到網頁](/help/assets/linking-urls-to-yourwebapplication.md) 和 [嵌入視頻或影像查看器](/help/assets/embed-code.md)。

如有必要，你可以 [編輯旋轉集](#editing-spin-sets)。 此外，您還可以查看和修改 [旋轉集屬性](/help/assets/manage-assets.md#editing-properties)。

## 上載旋轉集的資產 {#uploading-assets-for-spin-sets}

對於一維自旋集，至少需要8-12個項的投影，對於二維自旋集，需要16-24個投影。 必須定期拍攝照片，以給出項目正在旋轉並被翻轉的印象。 例如，如果一維自旋集包含12個鏡頭，則對每個鏡頭旋轉項目30°(360/12)。

可以像上載一樣上載旋轉集的影像 [上傳任何其他資產到Experience Manager Assets](/help/assets/manage-assets.md)。

請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 清單。

### 捕獲旋轉集影像的准則 {#guidelines-for-shooting-spin-set-images}

以下是圍繞旋轉集映像的一些最佳做法。 通常，「旋轉集」中的影像越多，影像旋轉效果越好。 但是，在集合中包含許多影像也會增加載入影像所花的時間。 Experience Manager建議在旋轉集中使用拍攝影像的以下准則：

* 至少在一維自旋集中使用8-12個影像，在二維自旋集中使用16-24個影像。 要能轉彎360度，最少需要8幅影像。 由於建立二維自旋集是勞動密集型的，因此一維自旋集比較常見。
* 使用無損格式；建議使用TIFF和PNG。
* 遮罩所有影像，使項目出現在純白色或其它高對比度背景上。 （可選）添加陰影。
* 確保產品詳細資訊亮點良好，並集中注意。
* 為時尚服裝製作假人或模特的假象。 通常，人體模型要麼被蒙版（使用玻璃人體模型），要麼在影像中顯示一個風格化的人體模型/服裝。 通過定義角度數，可建立模型上的旋轉集。 用底板上的磁帶標籤每個角度，以便引導模型按照每個鏡頭的方向進行步驟和查看。

## 建立旋轉集 {#creating-spin-sets}

本節介紹如何在Experience Manager中建立旋轉集。

>[!NOTE]
>
>您也可以透過批次集預設集自動 [建立回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。**重要提示：** 批集由IPS（映像生產系統）建立，作為資產接收的一部分，並且僅在Dynamic Media-Scene7模式下可用。
>
>請參閱中的「建立批集預設以自動生成影像集和旋轉集」 [配置Dynamic Media-Scene7模式](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。

>[!NOTE]
>
>影像在自旋集中出現的順序。 請務必訂購它們，使旋轉為360°的平滑視圖。

建立「旋轉集」時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 限制類型 | 最佳實踐 | 有限強加 |
| --- | --- | --- |
| 每2D集的最大行/列數 | 每組12-18頁圖片 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md)。

**要建立旋轉集：**

1. 在資產中，導航到要建立旋轉集的位置，選擇 **[!UICONTROL 建立]**，然後選擇 **[!UICONTROL 旋轉集]**。 您也可以從包含資產的資料夾內建立資產集。隨即顯示回轉集編輯器。

   ![6_5_spinset建立下拉菜單](assets/6_5_spinset-createpulldownmenu.png)

1. 在旋轉集編輯器中，在 **[!UICONTROL 標題]** 欄位中，輸入「旋轉集」的名稱。 該名稱出現在「旋轉集」的標題中。 （可選）輸入說明。

   ![6_5_spinset-spinsetedortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >建立旋轉集時，可以更改旋轉集縮略圖，或允許Experience Manager根據旋轉集中的資產自動選擇縮略圖。 要選擇縮略圖，請選擇 **[!UICONTROL 更改縮略圖]** 並選擇任何影像（您也可以導航到其他資料夾以查找影像）。 如果已選擇了縮略圖，然後決定要Experience Manager從旋轉集生成縮略圖，請選擇 **[!UICONTROL 切換到自動縮略圖]**。

1. 執行下列任一操作：

   * 在「旋轉集編輯器」頁的左上角附近，選擇 **[!UICONTROL 添加資產]**。

   * 在「旋轉集編輯器」頁的中間附近，選擇 **[!UICONTROL 點擊以開啟資產選擇器]**。
   點擊以選擇要包括在旋轉集中的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近，選擇 **[!UICONTROL 選擇]**。

   使用「資產選擇器」，您可以輸入關鍵字並點選「回報」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選擇篩選器，然後選擇 **[!UICONTROL 篩選]** 的子菜單。 點選「檢視」圖示並選取「欄檢視」、「卡片檢視」或「清 **[!UICONTROL 單檢視」]**, **[!UICONTROL 以變更]**&#x200B;檢視 ****。

   請參閱 [使用選擇器](/help/assets/working-with-selectors.md)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在將資產添加到集時，系統會按字母數字順序自動添加這些資產。 添加資產後，可以手動重新排序或排序。

   如有必要，將資產的「重新排序」表徵圖拖動到資產檔案名的右側，以在設定清單上或下重新排序影像。

   ![通過將旋轉集拖動到新位置來重新排序幀11](assets/6_5_spinset-reorderassets.png)。

   通過將旋轉集拖動到新位置來重新排序旋轉集中的幀11。

1. （可選）執行下列任一操作：

   * 要刪除影像，請選擇影像並選擇 **[!UICONTROL 刪除資產]**。

   * 要應用預設，請選擇靠近頁面右上角的 **[!UICONTROL 預設]**，然後選擇一個預設以立即應用於所有資產。

1. 選取&#x200B;**[!UICONTROL 儲存]**。新建立的「旋轉集」(Spin Set)會顯示在您建立時的資料夾中。

## 查看旋轉集 {#viewing-spin-sets}

可以在用戶介面中或自動使用 [批集預設](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。 但是，使用批集預設建立的集，請執行 *不* 在用戶介面中。 您可以以三種不同方式訪問通過批集預設建立的集。 （即使在用戶介面中建立了旋轉集，這些方法也可用）。

>[!NOTE]
>
>也可以通過用戶介面查看集，如中所述 [編輯旋轉集](#editing-spin-sets)。

**要查看旋轉集：**

1. 開啟單個資產的屬性時。 屬性指明選定資產是的成員(在 **[!UICONTROL 集的成員]**)。 選擇集的名稱，以便您可以查看整個集。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 來自任何組的成員映像。選擇 **[!UICONTROL 集]** 的子菜單。

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 在搜尋中，您可以選取「篩 **[!UICONTROL 選器]**」，然後展開「 **[!UICONTROL 動態媒體]** 」並選 **[!UICONTROL 取「集]**」。

   搜索返回在UI中手動建立或通過批集預設自動建立的匹配集。 對於自動集，搜索查詢使用 `Starts with` 與基於使用的Experience Manager搜索不同的搜索標準 `Contains` 搜索條件。 將篩選器設定為 **[!UICONTROL 集]** 是搜索自動集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 編輯旋轉集 {#editing-spin-sets}

可以對旋轉集執行各種編輯任務，如：

* 將影像添加到旋轉集。
* 重新排序「旋轉集」中的影像。
* 刪除旋轉集中的資產。
* 應用查看器預設。
* 刪除旋轉集。

**編輯旋轉集：**

1. 執行下列任一操作：

   * 將滑鼠懸停在旋轉集資產上，然後選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）。
   * 將滑鼠懸停在旋轉集資產上，選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖），然後選擇 **[!UICONTROL 編輯]** 的上界。

   * 在「旋轉集」資產上選擇，然後選擇 **[!UICONTROL 編輯]** 表徵圖)。

1. 要編輯「旋轉集」，請執行以下任一操作：

   * 要重新排序影像，請將影像拖到新位置（選擇重新排序表徵圖以移動項目）。
   * 要按升序或降序對項排序，請選擇列標題。
   * 要添加資產或更新現有資產，請選擇 **[!UICONTROL 添加資產]**。 定位至資產，選擇它，然後選擇 **[!UICONTROL 選擇]** 靠近右上角。
如果通過將縮覽圖替換為另一影像來刪除Experience Manager用於縮覽圖的影像，則仍會顯示原始資產。
   * 要刪除資產，請選擇它並選擇 **[!UICONTROL 刪除資產]**。
   * 要應用預設，請選擇「預設」表徵圖並選擇預設。
   * 要刪除整個旋轉集，請導航到旋轉集，選擇它，然後選擇 **[!UICONTROL 刪除]**

   >[!NOTE]
   >
   >通過導航到旋轉集，可編輯旋轉集中的影像，選擇 **[!UICONTROL 設定成員]** 在左欄中，然後選擇單個資產上的「鉛筆」表徵圖以開啟編輯窗口。

1. 選擇 **[!UICONTROL 保存]** 編輯。

## 預覽旋轉集 {#previewing-spin-sets}

請參閱 [預覽資產](/help/assets/previewing-assets.md)。

## 發佈旋轉集 {#publishing-spin-sets}

請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
