---
title: 影像集
description: 瞭解如何在Dynamic Media使用映像集
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
feature: Image Sets,Asset Management
role: User, Admin
exl-id: 2a536745-fa13-4158-8761-2ac5b6e1893e
source-git-commit: d83a647d8ac5466ba09230c584d5d501aab55274
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 7%

---

# 影像集 {#image-sets}

「影像集」為用戶提供了整合的查看體驗，用戶可以通過選擇縮略圖來查看項目的不同視圖。 「影像集」(Image Sets)允許您顯示項目的替代視圖，而查看器提供了縮放工具，用於仔細檢查影像。

影像集由帶字的標題指定 `IMAGESET`。 此外，如果已發佈影像集，則會顯示以 **[!UICONTROL World]** 圖示表示的發佈日期與上次修改日期(以 **** Pencil圖示表示)在橫幅上。

![影像集](assets/chlimage_1-339.png)

在「影像集」中，還可以通過建立「影像集」和添加縮略圖來建立色板。

當您希望以不同顏色、圖案或完成顯示項目時，此應用程式非常有用。 要使用顏色色板建立影像集，您需要為要向用戶呈現的每種不同顏色、圖案或完成一幅影像。 每種顏色、圖案或光潔度還需要一個顏色、圖案或光潔度色板。

例如，假設您要顯示具有不同顏色鈔票的大寫影像；賬單是紅的，綠的，藍的。 在這個例子中，你需要三針相同的帽子。 你需要一張紅的，一張綠的，一張藍的。 還需要紅色、綠色和藍色色板。 顏色色板用作用戶在「色板集查看器」中選擇的縮略圖，以查看紅色開單、綠色開單或藍色開單的帽。

>[!NOTE]
>
>有關Assets用戶介面的資訊，請參閱 [管理資產](/help/assets/manage-assets.md)。

建立映像集時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 限制類型 | 最佳實踐 | 強加的限制 |
| --- | --- | --- |
| 每集重複的資產數 | 無重複項 | 20 |
| 每集的最大影像數 | 每組5-10頁影像 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md)。

## 快速啟動：影像集 {#quick-start-image-sets}

**要快速啟動並運行：**

1. [上載多個視圖的主源映像](#uploading-assets-in-image-sets)。

   首先上載映像集的映像。 選擇影像時，請記住客戶可以在「影像集查看器」中放大影像。 確保影像在最大尺寸中至少為2000像素，以便獲得最佳縮放細節。 Dynamic Media可以每張渲染高達250萬像素的影像。 例如，您可以使用5000 x 5000 MP的映像或任何其他大小組合，最多25 MP。

   請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 影像集支援的格式清單。

<!--    Adobe Experience Manager Assets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

1. [建立映像集](#creating-image-sets)。

   在影像集中，用戶在影像集查看器中選擇縮略圖。

   要在資產中建立映像集，請轉到 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]**。 然後，添加影像並選擇 **[!UICONTROL 保存]**。

   還可以通過 [批集預設](/help/assets/config-dms7.md)。
   >[!IMPORTANT]
   >
   >批集由IPS（映像生產系統）建立，作為資產接收的一部分，並且僅在Dynamic Media-Scene7模式下可用。

   請參閱 [準備映像集資產以上載和上載檔案](#uploading-assets-in-image-sets)。

   請參閱 [使用選擇器](/help/assets/working-with-selectors.md)。

1. 添加 [影像集查看器預設](/help/assets/managing-viewer-presets.md)，根據需要。

   管理員可以建立或修改「影像集查看器預設」。 要使用查看器預設查看影像集，請選擇影像集，然後在左欄下拉菜單中選擇 **[!UICONTROL 查看者]**。

   導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 查看器預設]** 。要使

1. （可選） [查看影像集](/help/assets/image-sets.md#viewing-image-sets) 是使用批集預設建立的。
1. [預覽影像集](/help/assets/previewing-assets.md)。

   選擇「影像集」(Image Set)，您可以預覽它。 選擇縮略圖表徵圖，以便在選定的查看器中檢查影像集。 您可以從 **[!UICONTROL 查看者]** 菜單開啟它。

1. [發佈映像集](/help/assets/publishing-dynamicmedia-assets.md)。

   發佈映像集將激活URL和嵌入代碼。 此外，您必須 [發佈任何自定義查看器預設](/help/assets/managing-viewer-presets.md) 你創造的。 已發佈現成查看器預設。

1. [將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md) 或 [嵌入視頻或影像查看器](/help/assets/embed-code.md)。

   Experience Manager Assets會建立映像集的URL調用，並在您發佈映像集後激活它們。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們嵌入到您的網站中。

   選取「影像集」，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   請參閱 [將影像集連結到網頁](/help/assets/linking-urls-to-yourwebapplication.md) 和 [嵌入視頻或影像查看器](/help/assets/embed-code.md)。

要編輯映像集，請參閱 [編輯影像集](#editing-image-sets)。 此外，您還可以查看和編輯 [影像集屬性](/help/assets/manage-assets.md#editing-properties)。

如果建立集時遇到問題，請參閱中的影像和集 [診斷Dynamic Media-Scene7模式](/help/assets/troubleshoot-dms7.md#images-and-sets)。

## 在映像集中上載資產 {#uploading-assets-in-image-sets}

首先上載映像集的映像。 選擇影像時，請記住客戶可以在「影像集查看器」中放大影像。 請確定影像在最大尺寸中至少為2000像素。影像集支援多種影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

可以像您一樣上載映像集的映像 [上載資產中的任何其他資產](/help/assets/manage-assets.md#uploading-assets)。

請參閱 [Dynamic Media — 支援的光柵影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 影像集支援的格式清單。

### 準備映像集資產以供上載 {#preparing-image-set-assets-for-upload}

在建立映像集之前，請確保映像的大小和格式正確。

要建立多視圖影像集，需要顯示來自不同視點的項目或顯示同一項目不同方面的影像。 其目標是突出顯示項目的重要功能，以便查看者能夠完整瞭解項目的外觀或行為。

因為用戶可以在影像集中縮放影像，所以請確保影像在最大尺寸中至少為2000像素。 <!-- Assets support many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

>[!NOTE]
>
>此外，如果使用縮略圖來指示產品色板，則必須執行以下操作：
>
>您需要使用小畫或同一影像的不同鏡頭，以不同的顏色、圖案或結束顯示。 您還需要與不同顏色、圖案或結束相對應的縮略圖檔案。 例如，要顯示縮略圖，並且影像集以黑色、棕色和綠色顯示同一夾克，您需要：
>
>* 同一件夾克的黑色，棕色和綠色。
>* 黑色、棕色和綠色縮略圖。


## 建立映像集 {#creating-image-sets}

可以通過用戶介面或API建立映像集。 本節介紹如何在UI中建立映像集。

>[!NOTE]
>
>還可以通過 [批集預設](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。
>**重要提示：** 批集由IPS（映像生產系統）建立，作為資產接收的一部分，並且僅在Dynamic Media-Scene7模式下可用。

在將資產添加到集時，系統會按字母數字順序自動添加這些資產。 添加資產後，可以手動重新排序或對其排序。

>[!NOTE]
>
>檔案名中具有「，」（逗號）的資產不支援映像集。

建立映像集時，Adobe建議採用以下最佳做法並強制實施以下限制：

| 限制類型 | 最佳實踐 | 強加的限制 |
| --- | --- | --- |
| 每集重複的資產數 | 無重複項 | 20 |
| 每集的最大影像數 | 每組5-10頁影像 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md)。

**要建立映像集：**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，然後轉到 **[!UICONTROL 導航]** > **[!UICONTROL 資產]**。 導航到要建立映像集的位置，然後轉到 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]** 開啟「影像集編輯器」頁。

   您也可以從包含資產的資料夾內建立資產集。

   ![6_5映像集 — 建立下拉](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁中， **[!UICONTROL 標題]** 欄位中，輸入影像集的名稱。 該名稱出現在影像集的標題中。 （可選）輸入說明。

   ![6_5 — 映像集建立新集](assets/6_5_imageset-creatingnewset.png)

1. 執行下列任一操作：

   * 在「影像集編輯器」頁的左上角附近，選擇 **[!UICONTROL 添加資產]**。

   * 在「影像集編輯器」頁面的中間，選擇 **[!UICONTROL 點擊以開啟資產選擇器]**。
   選擇要包括在映像集中的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近，選擇 **[!UICONTROL 選擇]**。

   使用「資產選擇器」，您可以輸入關鍵字並點選或按一下「退貨」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選擇篩選器，然後選擇 **[!UICONTROL 篩選]** 的子菜單。 點選「檢視」圖示並選取「欄檢視」、「卡片檢視」或「清 **[!UICONTROL 單檢視」]**, **[!UICONTROL 以變更]**&#x200B;檢視 ****。

   請參閱 [使用選擇器](/help/assets/working-with-selectors.md)。

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 在將資產添加到集時，系統會按字母數字順序自動添加這些資產。 添加資產後，可以手動重新排序或排序。

   如有必要，將資產的「重新排序」表徵圖拖動到資產檔案名的右側，以在設定清單上或下重新排序影像。

   ![6_5映像集 — 重新排序資產](assets/6_5_imageset-reorderassets.png)

   如果要更改縮覽圖或色板，請選擇 **+** **縮略圖** 表徵圖，然後導航到所需的縮略圖或色板。 選擇完所有影像後，選擇 **[!UICONTROL 保存]**。

1. （可選）執行下列任一操作：

   * 要刪除影像，請選擇影像並選擇 **[!UICONTROL 刪除資產]**。

   * 要應用預設，請選擇靠近頁面右上角的 **[!UICONTROL 預設]**，然後選擇一個預設以立即應用於所有資產。
   >[!NOTE]
   >
   >建立影像集時，可以更改影像集縮略圖，或允許Experience Manager根據影像集中的資產自動選擇縮略圖。 要選擇縮略圖，請選擇 **[!UICONTROL 更改縮略圖]** 在「影像集編輯器」頁面的「標題」欄位上方，選擇任何影像（您也可以導航到其他資料夾以查找影像）。 如果已選擇縮略圖，然後決定要Experience Manager從影像集生成縮略圖，請選擇 **[!UICONTROL 切換到]** > **[!UICONTROL 自動縮略圖]**。

1. 選擇 **[!UICONTROL 保存]**。 您新建立的映像集將顯示在您建立的資料夾中。

## 查看影像集 {#viewing-image-sets}

可以在用戶介面中建立影像集或自動使用 [批集預設](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。

>[!IMPORTANT]
>
>批集由IPS建立 [影像生成系統] 作為資產攝取的一部分，僅在Dynamic Media-Scene7模式下提供。)

但是，使用批集預設建立的集，請執行 *不* 在用戶介面中。 您可以用三種不同的方式查看這些集。 （即使您在用戶介面中建立了影像集，這些方法也可用）。

* 開啟單個資產的屬性。 屬性指明引用的選定資產或其成員的設定。 如果要查看整個集，請選擇集的名稱。

   ![6_5_imageset-asset屬性](assets/6_5_imageset-assetproperties2.png)

* 來自任何組的成員映像。選擇 **[!UICONTROL 集]** 的子菜單。

   ![6_5-imageset-setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜索中，您可以選擇 **[!UICONTROL 篩選]**，然後展開 **[!UICONTROL Dynamic Media]** 選擇 **[!UICONTROL 集]**。

   搜索返回在UI中手動建立或通過批集預設自動建立的匹配集。 對於自動集，搜索查詢使用「開始於」搜索標準進行，該搜索標準不同於基於使用「包含」搜索標準的Experience Manager搜索。 將篩選器設定為 **[!UICONTROL 集]** 是搜索自動集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以通過用戶介面查看集，如中所述 [編輯影像集](#editing-image-sets)。

## 編輯影像集 {#editing-image-sets}

可以對影像集執行各種編輯任務，如：

* 向映像集添加映像。
* 對影像集中的影像重新排序。
* 刪除映像集中的資產。
* 應用查看器預設。
* 刪除映像集。

**編輯映像集：**

1. 執行下列任一操作：

   * 將滑鼠懸停在影像集資產上，然後選擇 **[!UICONTROL 編輯]** （鉛筆表徵圖）。
   * 將滑鼠懸停在影像集資產上，選擇 **[!UICONTROL 選擇]** （複選標籤表徵圖），然後選擇 **[!UICONTROL 編輯]** 的上界。
   * 在映像集資產上選擇，然後選擇 **[!UICONTROL 編輯]** 表徵圖)。

1. 要編輯「影像集」中的影像，請執行以下任一操作：

   * 要重新排序資產，請將影像拖到新位置（選擇重新排序表徵圖以移動項目）。
   * 要按升序或降序對項排序，請選擇列標題。
   * 要添加資產或更新現有資產，請選擇 **[!UICONTROL 添加資產]**。 定位至資產，選擇它，然後選擇 **[!UICONTROL 選擇]** 靠近頁面右上角。

      >[!NOTE]
      >
      >如果通過將縮覽圖替換為另一影像來刪除Experience Manager用於縮覽圖的影像，則仍會顯示原始資產。
   * 要刪除資產，請選擇它並選擇 **[!UICONTROL 刪除資產]**。
   * 要應用預設，請選擇靠近頁面右上角的 **[!UICONTROL 預設]**，然後選擇查看器預設。
   * 要添加或更改縮略圖，請選擇資產右側旁邊的縮略圖表徵圖。 導航到新縮略圖或色板資產，選擇它，然後選擇 **[!UICONTROL 選擇]**。
   * 要刪除整個映像集，請導航到映像集，選擇它，然後選擇 **[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >通過導航到影像集，可編輯影像集中的影像，選擇 **[!UICONTROL 設定成員]** 在左欄中，然後選擇單個資產上的「鉛筆」表徵圖以開啟編輯窗口。

1. 選擇 **[!UICONTROL 保存]** 編輯。

## 預覽影像集 {#previewing-image-sets}

請參閱 [預覽資產](/help/assets/previewing-assets.md)。

## 發佈映像集 {#publishing-image-sets}

請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
