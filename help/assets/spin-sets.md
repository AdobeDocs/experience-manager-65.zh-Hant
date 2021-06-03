---
title: 迴轉集
description: 了解如何在Dynamic Media中使用回轉集
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: 回轉集，資產管理
role: Business Practitioner, Administrator
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 11%

---

# 迴轉集{#spin-sets}

回轉集模擬轉動物件的真實行為，以檢查物件。 「回轉集」可讓您從任何角度檢視項目，從任何角度取得關鍵的視覺詳細資訊。

回轉集可模擬360度的檢視體驗。 Dynamic Media提供單軸回轉集，供檢視器旋轉項目。 此外，使用者只需按幾下滑鼠，即可「自由格式」縮放及平移任何檢視。 這樣，用戶可以從特定角度更仔細地檢查項目。

「回轉集」由字為&#x200B;**[!UICONTROL SPINSET]**&#x200B;的橫幅指定。 此外，如果已發佈回轉集，則會顯示以&#x200B;**[!UICONTROL World]**&#x200B;圖示指示的發佈日期與上次修改日期（以&#x200B;**[!UICONTROL Pencil]**&#x200B;圖示表示）在橫幅上。

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>如需Assets使用者介面的資訊，請參閱[管理資產](/help/assets/manage-assets.md)。

## 快速入門：回轉集{#quick-start-spin-sets}

若要使用回轉集快速上手並執行，請執行下列步驟：

1. [上傳多次檢視的影像。](#uploading-assets-for-spin-sets)

   一維自旋集至少需要8-12個項目的鏡頭，二維自旋集至少需要16-24個。 必須定期拍攝照片，以給人以項目正在旋轉和被翻轉的印象。 例如，如果一維度回轉集包含12個鏡頭，則對每個鏡頭將項目旋轉30度(360/12)。

1. [建立回轉集。](#creating-spin-sets)

   若要建立回轉集，請選取「**[!UICONTROL 建立>回轉集]**」，然後命名該集，選擇資產，然後選擇影像的顯示順序。

   請參閱[使用選取器](/help/assets/working-with-selectors.md)。

   >[!NOTE]
   >
   >您也可以透過批次集預設集自動 [建立回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。**重要：** 批集由IPS(Image Production System)建立，作為資產擷取的一部分，僅可在Dynamic Media - Scene7模式中使用。

1. 視需要設定[回轉集檢視器預設集](/help/assets/managing-viewer-presets.md)。

   管理員可以建立或修改回轉集檢視器預設集。若要檢視含有檢視器預設集的回轉集，請選取該回轉集，然後在左側導軌下拉式選單中選取「檢 **視器**」。

   請參閱&#x200B;**[!UICONTROL 工具>資產>檢視器預設集]**&#x200B;以建立或編輯檢視器預設集。

   請參閱[添加和編輯查看器預設集。](/help/assets/managing-viewer-presets.md)

1. [檢視回轉集](#viewing-spin-sets)。

   您可以透過三種不同方式的批次集預設集來檢視和存取所建立的集。 （使用批集預設集建立的集，請在用戶介面中顯示&#x200B;*not*。）

1. [預覽回轉集。](/help/assets/previewing-assets.md)

   選取回轉集，即可預覽。 旋轉回轉集。 您可以從&#x200B;**[!UICONTROL 檢視器]**&#x200B;選單中選擇不同的檢視器，該選單可從左側導軌下拉式選單中取得。

1. [發佈回轉集。](/help/assets/publishing-dynamicmedia-assets.md)

   發佈回轉集會啟用URL和內嵌字串。 此外，您必須[發佈檢視器預設集](/help/assets/managing-viewer-presets.md)。

1. [將URL連結至您的Web](/help/assets/linking-urls-to-yourwebapplication.md) 應用程 [式，或內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

   AEM Assets會為回轉集建立URL呼叫，並在您發佈回轉集後啟用它們。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們嵌入您的網站。

   選取「回轉集」，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   請參 [閱將回轉集連結至網頁](/help/assets/linking-urls-to-yourwebapplication.md)[和內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

如果需要，可以[編輯回轉集](#editing-spin-sets)。 此外，還可以查看和修改[回轉集屬性](/help/assets/manage-assets.md#editing-properties)。

## 上傳回轉集的資產{#uploading-assets-for-spin-sets}

一維自旋集至少需要8-12個項目的鏡頭，二維自旋集至少需要16-24個。 必須定期拍攝照片，以給人以項目正在旋轉和被翻轉的印象。 例如，如果一維度回轉集包含12個鏡頭，則對每個鏡頭將項目旋轉30度(360/12)。

您可以像在AEM Assets](/help/assets/manage-assets.md)中上傳任何其他資產一樣，上傳回轉集的影像。[

### 回轉集{#guidelines-for-shooting-spin-set-images}影像擷取指南

以下是回轉集影像的一些最佳實務。 一般而言，旋轉集中的影像越多，影像旋轉效果就越好。 但是，集合中包含許多影像也會增加影像載入所花費的時間。 AEM建議在回轉集中拍攝影像時使用下列准則：

* 至少在一維回轉集中使用8-12個影像，在二維回轉集中使用16-24個影像。 至少需要8張影像才能使旋轉360度。 一維回轉集較常見，因為建立二維回轉集需耗費大量人力。
* 使用無損格式；建議使用TIFF和PNG。
* 遮罩所有影像，使項目出現在純白色或其他高對比背景上。 （可選）添加陰影。
* 請確定產品詳細資訊清晰明瞭，且清晰明瞭。
* 給裝模特或模特的時尚服裝拍照。 通常，人體模型要麼是完全遮罩的（使用玻璃人體模型），要麼是影像中顯示了造型化的人體模型/服裝。 通過定義角度數，可以建立模型上的回轉集。 在地板上用膠帶標出每個角度，以引導模型向各拍攝方向走動和查看。

## 建立回轉集{#creating-spin-sets}

本節說明如何在AEM中建立回轉集。

>[!NOTE]
>
>您也可以透過批次集預設集自動 [建立回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。**重要：** 批集由IPS(Image Production System)建立，作為資產擷取的一部分，僅可在Dynamic Media - Scene7模式中使用。
>
>請參閱[設定Dynamic Media - Scene7模式](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)中的「建立批集預設集以自動產生影像集和回轉集」。


>[!NOTE]
>
>影像在回轉集中的顯示順序。 請務必訂購，使回轉為360度的平滑檢視。

**若要建立回轉集：**

1. 在「資產」中，導覽至您要建立回轉集的位置，按一下「建 **[!UICONTROL 立]**」，然後選取「 **[!UICONTROL 回轉集」]**。您也可以從包含資產的資料夾內建立資產集。隨即顯示回轉集編輯器。

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 在回轉集編輯器的&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，輸入回轉集的名稱。 名稱會顯示在回轉集的橫幅中。 （可選）輸入說明。

   ![6_5_spinset_spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >建立回轉集時，您可以變更回轉集縮圖，或允許AEM根據回轉集中的資產自動選取縮圖。 若要選取縮圖，請按一下「**[!UICONTROL 變更縮圖]**」並選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您已選取縮圖，然後決定要AEM從回轉集產生縮圖，請選取「**[!UICONTROL 切換至自動縮圖]**」。

1. 執行下列任一操作：

   * 在「回轉集編輯器」頁面的左上角附近，點選「**[!UICONTROL 新增資產]**」。

   * 在「回轉集編輯器」頁面的中間附近，點選&#x200B;**[!UICONTROL 點選以開啟「資產選取器」]**。
   點選以選取您要納入回轉集的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近，點選「 **[!UICONTROL Select]** 」。

   使用「資產選擇器」，您可以輸入關鍵字並點選「回報」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後點選工具 **[!UICONTROL 列上的]** 「篩選」圖示。點選「檢視」圖示並選取「欄檢視」、「卡片檢視」或「清 **[!UICONTROL 單檢視」]**, **[!UICONTROL 以變更]**&#x200B;檢視 ****。

   請參閱[使用選取器](/help/assets/working-with-selectors.md)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 將資產新增至資產集時，資產會以英數字元順序自動新增。 新增資產後，您可以手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以在設定的清單上或下重新排序影像。

   ![將回轉集中的影格拖曳至新位置，重新排序影格11。](assets/6_5_spinset-reorderassets.png)

   將回轉集中的影格拖曳至新位置，重新排序影格11。

1. （選用）執行下列任一操作：

   * 若要刪除影像，請選取影像並點選&#x200B;**[!UICONTROL 刪除資產]**。

   * 若要套用預設集，在頁面右上角附近，點選&#x200B;**[!UICONTROL Preset]**，然後選取一個預設集，一次套用至所有資產。

1. 按一下「**[!UICONTROL 儲存]**」。新建立的回轉集會顯示在您建立該回轉集的資料夾中。

## 查看回轉集{#viewing-spin-sets}

您可以在使用者介面中建立回轉集，或自動使用[批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。 但是，使用批集預設集建立的集，do *not*&#x200B;將出現在用戶介面中。 您可以透過三種不同方式存取透過批次集預設集建立的集。 （即使您在使用者介面中建立回轉集，這些方法仍可供使用）。

>[!NOTE]
>
>您也可以透過使用者介面來檢視集，如[編輯回轉集](#editing-spin-sets)所述。

**若要檢視回轉集**

1. 開啟個別資產的屬性時。 屬性指明所選資產是的成員（在&#x200B;**[!UICONTROL 整合員]**&#x200B;下）。 按一下集的名稱，即可查看整個集。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 來自任何組的成員映像。選擇&#x200B;**[!UICONTROL 集]**&#x200B;菜單以顯示資產所屬的集。

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 在搜尋中，您可以選取「篩 **[!UICONTROL 選器]**」，然後展開「 **[!UICONTROL 動態媒體]** 」並選 **[!UICONTROL 取「集]**」。

   搜尋會傳回在UI中手動建立或透過批次集預設集自動建立的相符集。 對於自動集，搜索查詢使用`Starts with`搜索標準執行，該搜索標準不同於基於使用`Contains`搜索標準的AEM搜索。 將篩選器設定為&#x200B;**[!UICONTROL Sets]**&#x200B;是搜索自動集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 編輯回轉集{#editing-spin-sets}

您可以對回轉集執行各種編輯工作，例如：

* 將影像新增至回轉集。
* 重新排序回轉集中的影像。
* 刪除回轉集中的資產。
* 套用檢視器預設集。
* 刪除回轉集。

**若要編輯回轉集**

1. 執行下列任一操作：

   * 將滑鼠指標暫留在「回轉集」資產上，然後點選「**[!UICONTROL 編輯]**」（鉛筆圖示）。
   * 暫留在「回轉集」資產上，點選「**[!UICONTROL 選取]**」（核取標籤圖示），然後點選工具列上的「**[!UICONTROL 編輯]**」。

   * 點選「回轉集」資產，然後點選工具列上的「 **[!UICONTROL 編輯]**（鉛筆圖示）」。

1. 若要編輯回轉集，請執行下列任一操作：

   * 若要重新排序影像，請拖曳影像至新位置（選取重新排序圖示以移動項目）。
   * 若要依遞增或遞減順序排序項目，請按一下欄標題。
   * 若要新增資產或更新現有資產，請按一下「新增資產」**[!UICONTROL 「]**」。 導覽至資產，選取資產，然後點選右上角的&#x200B;**[!UICONTROL 選取]**。
如果您以其他影像取代縮圖，以刪除AEM用於縮圖的影像，仍會顯示原始資產。
   * 若要刪除資產，請選取資產，然後按一下或點選「**[!UICONTROL 刪除資產]**」。
   * 若要套用預設集，請點選或按一下「預設集」圖示，然後選取預設集。
   * 若要刪除整個回轉集，請導覽至回轉集，選取該回轉集，然後選取&#x200B;**[!UICONTROL Delete]**

   >[!NOTE]
   >
   >您可以導覽至回轉集，點選左側導軌中的「設定成員&#x200B;****」，然後點選個別資產上的「鉛筆」圖示以開啟編輯視窗，以編輯影像。

1. 完成編輯時，按一下「**[!UICONTROL 儲存]**」。

## 預覽回轉集{#previewing-spin-sets}

請參閱「預覽資產」[。](/help/assets/previewing-assets.md)

## 發佈回轉集{#publishing-spin-sets}

請參閱[發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
