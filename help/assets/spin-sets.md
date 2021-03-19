---
title: 迴轉集
description: 瞭解如何在Dynamic Media處理回轉集
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: 回轉集，資產管理
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 9%

---


# 迴轉集{#spin-sets}

「回轉集」(Spin Set)模擬實際操作，即旋轉對象來檢查對象。 「回轉集」可讓您從任何角度檢視項目，從任何角度獲得關鍵視覺細節。

回轉集可模擬360度檢視體驗。 Dynamic Media提供單軸回轉集，檢視器可在其中旋轉項目。 此外，使用者只需按幾下滑鼠，就可「自由格式」縮放和平移任何檢視。 這樣，用戶就可以更密切地從特定的角度檢查項目。

回轉集由具有單字&#x200B;**[!UICONTROL SPINSET的橫幅指定。]** 此外，如果「回轉集」已發佈，則會顯示「 **** Worldicon」所指示的發佈日期與「Pencilicon」所指示的上次修改日期，在橫幅 **** 上。

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>如需Assets使用者介面的詳細資訊，請參閱[管理資產](/help/assets/manage-assets.md)。

## 快速入門：回轉集{#quick-start-spin-sets}

若要快速啟動並執行回轉集，請依照下列步驟進行：

1. [上傳影像以進行多次檢視。](#uploading-assets-for-spin-sets)

   至少，一維自旋集需要8-12個項目鏡頭，二維自旋集需要16-24個項目鏡頭。 拍攝時間必須定期，以呈現項目旋轉和翻轉的印象。 例如，如果一維回轉集包含12個鏡頭，請針對每個鏡頭旋轉項目30度(360/12)。

1. [建立回轉集。](#creating-spin-sets)

   若要建立回轉集，請選取「建立>回轉集」，然後命名該回轉集，選擇資產，然後選擇影像的顯示順序。****

   請參閱[使用選擇器](/help/assets/working-with-selectors.md)。

   >[!NOTE]
   >
   >您也可以透過批次集預設集自動 [建立回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。**重要：** 批集由IPS（映像生產系統）建立，作為資產接收的一部分，僅在Dynamic Media-Scene7模式中可用。

1. 視需要設定[回轉集檢視器預設集](/help/assets/managing-viewer-presets.md)。

   管理員可以建立或修改回轉集檢視器預設集。若要檢視含有檢視器預設集的回轉集，請選取該回轉集，然後在左側導軌下拉式選單中選取「檢 **視器**」。

   請參閱&#x200B;**[!UICONTROL 工具>資產>檢視器預設集]**&#x200B;以建立或編輯檢視器預設集。

   請參閱[新增和編輯檢視器預設集。](/help/assets/managing-viewer-presets.md)

1. [查看回轉集](#viewing-spin-sets)。

   您可以三種不同的方式檢視和存取以批次集預設集方式建立的集合。 （使用批集預設集建立的集，請&#x200B;*not*&#x200B;顯示在用戶介面中。）

1. [預覽回轉集。](/help/assets/previewing-assets.md)

   選取「回轉集」(Spin Set)，您就可以預覽它。 旋轉回轉集。 您可以從左側導軌下拉式選單的&#x200B;**[!UICONTROL 檢視器]**&#x200B;選單中選擇不同的檢視器。

1. [發佈回轉集。](/help/assets/publishing-dynamicmedia-assets.md)

   發佈回轉集會啟動URL和內嵌字串。 此外，您必須[發佈檢視器預設集](/help/assets/managing-viewer-presets.md)。

1. [將URL連結至您的Web應](/help/assets/linking-urls-to-yourwebapplication.md) 用程 [式或內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

   AEM Assets會建立回轉集的URL呼叫，並在您發佈回轉集後加以啟動。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選擇回轉集，然後在左側導軌下拉式功能表中，選擇&#x200B;**[!UICONTROL 檢視器。]**

   請參 [閱將回轉集連結至網頁](/help/assets/linking-urls-to-yourwebapplication.md)[和內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

如果需要，可以[編輯回轉集](#editing-spin-sets)。 此外，您還可以查看和修改[回轉集屬性](/help/assets/manage-assets.md#editing-properties)。

## 上傳回轉集的資產{#uploading-assets-for-spin-sets}

至少，一維自旋集需要8-12個項目鏡頭，二維自旋集需要16-24個項目鏡頭。 拍攝時間必須定期，以呈現項目旋轉和翻轉的印象。 例如，如果一維回轉集包含12個鏡頭，請針對每個鏡頭旋轉項目30度(360/12)。

您可以像[上傳AEM Assets的任何其他資產一樣，上傳回轉集的影像。](/help/assets/manage-assets.md)

### 擷取回轉集{#guidelines-for-shooting-spin-set-images}影像的指引

以下是回轉集影像的一些最佳實務。 一般而言，旋轉集中的影像越多，影像旋轉效果就越好。 不過，在集合中加入許多影像也會增加影像載入所花的時間。 AEM建議拍攝影像以用於回轉集的下列准則：

* 至少，在一維回轉集中使用8-12張影像，在二維回轉集中使用16-24張影像。 至少需要8張影像才能旋轉360度。 一維回轉集比較常見，因為建立二維回轉集耗費大量人力。
* 使用無損格式；建議使用TIFF和PNG。
* 遮色所有影像，讓項目出現在純白色或其他高對比背景上。 （可選）添加陰影。
* 請確定產品詳細資訊已清楚標示，並且已集中注意。
* 為具有人體模型或模特兒的時尚服裝拍攝旋轉影像。 通常，假人模型要麼是完全遮色的（使用玻璃模型），要麼在圖中顯示風格化的假人模型／服裝。 通過定義角度數，可建立模型上的回轉集。 在地板上用磁帶標籤每個角度，以引導模型向每個拍攝方向步移和查看。

## 建立回轉集{#creating-spin-sets}

本節介紹如何在中建立回轉集AEM。

>[!NOTE]
>
>您也可以透過批次集預設集自動 [建立回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。**重要：** 批集由IPS（映像生產系統）建立，作為資產接收的一部分，僅在Dynamic Media-Scene7模式中可用。
>
>請參閱[設定Dynamic Media-Scene7模式](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)中的「建立批次集預設集以自動產生影像集和回轉集」。


>[!NOTE]
>
>影像在回轉集中的顯示順序。 請務必訂購，如此旋轉360度檢視就會順暢無礙。

**要建立回轉集**

1. 在「資產」中，導覽至您要建立回轉集的位置，按一下「建 **[!UICONTROL 立]**」，然後選取「 **[!UICONTROL 回轉集」。]**&#x200B;您也可以從包含資產的資料夾內建立資產集。隨即顯示回轉集編輯器。

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 在回轉集編輯器的&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，輸入回轉集的名稱。 名稱會顯示在回轉集的橫幅中。 （可選）輸入說明。

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >建立回轉集時，您可以變更回轉集縮圖，或AEM允許根據回轉集中的資產自動選取縮圖。 若要選取縮圖，請按一下「變更縮圖&#x200B;**[!UICONTROL 」，然後選取任何影像（您也可以導覽至其他檔案夾以尋找影像）。]**&#x200B;如果您已選取縮圖，然後決定AEM要從回轉集產生縮圖，請選取「切換至自動縮圖」。]****[!UICONTROL 

1. 執行下列任一項作業：

   * 在「回轉集編輯器」頁面的左上角附近，點選「新增資產」。]****[!UICONTROL 

   * 在「回轉集編輯器」頁面的中間，點選&#x200B;**[!UICONTROL 以開啟「資產選擇器」。]**
   點選以選取您要納入回轉集中的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近點選&#x200B;**[!UICONTROL Select.]**

   使用「資產選擇器」，您可以輸入關鍵字並點選「回報」來搜尋 **[!UICONTROL 資產]**。您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後點選工具 **[!UICONTROL 列上的]** 「篩選」圖示。點選「檢視」圖示並選取「欄檢視」**[!UICONTROL 「欄檢視」]**、「卡片檢視」]**或「清單檢視」，以變更檢視。]****[!UICONTROL **[!UICONTROL 

   請參閱[使用選擇器](/help/assets/working-with-selectors.md)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在新增資產後手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以在設定清單上或下重新排序影像。

   ![將回轉集中的畫格11拖曳至新位置，以重新排序。](assets/6_5_spinset-reorderassets.png)

   將回轉集中的畫格11拖曳至新位置，以重新排序。

1. （可選）執行下列任一項作業：

   * 若要刪除影像，請選取影像並點選「刪除資產」。]****[!UICONTROL 

   * 若要套用預設，請在頁面右上角附近點選&#x200B;**[!UICONTROL Preset]**，然後選取一個預設，一次套用至所有資產。

1. 按一下「**[!UICONTROL 儲存」。]** 您新建立的「回轉集」會出現在您所建立的檔案夾中。

## 查看回轉集{#viewing-spin-sets}

您可以在使用者介面中建立回轉集，或使用[批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自動建立回轉集。 不過，使用批集預設集建立的集合，請&#x200B;*not*&#x200B;出現在使用者介面中。 您可以三種不同的方式存取透過批次集預設集建立的集合。 （即使您在使用者介面中建立回轉集，這些方法也可用）。

>[!NOTE]
>
>您也可以透過使用者介面檢視集，如[編輯回轉集](#editing-spin-sets)所述。

**要查看回轉集**

1. 開啟個別資產的屬性時。 屬性指示所選資產是成員（在&#x200B;**[!UICONTROL 整合員]**&#x200B;下）的成員。 按一下集的名稱，即可查看整個集。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 來自任何組的成員映像。選擇&#x200B;**[!UICONTROL Sets]**&#x200B;菜單以顯示資產所屬的集。

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 在搜索中，可以選擇&#x200B;**[!UICONTROL 篩選器]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;並選擇&#x200B;**[!UICONTROL 集。]**

   搜尋會傳回在UI中手動建立或透過批次集預設集自動建立的相符集。 對於自動集，搜索查詢使用與基於使用`Contains`搜索標準的搜索不同的&lt;a0/AEM>搜索標準進行。 `Starts with`將篩選器設定為&#x200B;**[!UICONTROL Sets]**&#x200B;是搜索自動集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 編輯回轉集{#editing-spin-sets}

您可以對回轉集執行多種編輯工作，例如：

* 將影像新增至回轉集。
* 在回轉集中重新排序影像。
* 刪除回轉集中的資產。
* 套用檢視器預設集。
* 刪除回轉集。

**要編輯回轉集**

1. 執行下列任一項作業：

   * 將滑鼠指標暫留在「回轉集」資產上，然後點選「**[!UICONTROL 編輯]**」（鉛筆圖示）。
   * 將滑鼠指標暫留在回轉集資產上，點選「**[!UICONTROL 選擇]**（勾選圖示）」，然後點選工具列上的「編輯&#x200B;**[!UICONTROL a3/>」。]**

   * 點選「回轉集」資產，然後點選工具列上的「編輯&#x200B;****（鉛筆圖示）」。

1. 若要編輯回轉集，請執行下列任一動作：

   * 若要重新排序影像，請將影像拖曳至新位置（選取重新排序圖示以移動項目）。
   * 若要依遞增或遞減順序排序項目，請按一下欄標題。
   * 若要新增資產或更新現有資產，請按一下「新增資產」。**** 導覽至資產，選取資產，然後點 **** 選右上角的「選取」。如果您將縮圖的AEM影像取代為其他影像，以刪除該影像，原始資產仍會顯示。
   * 若要刪除資產，請選取資產，然後按一下或點選「刪除資產」。]****[!UICONTROL 
   * 若要套用預設，請點選或按一下「預設」圖示並選取預設。
   * 要刪除整個回轉集，請導航至回轉集，選擇它，然後選擇&#x200B;**[!UICONTROL 刪除]**

   >[!NOTE]
   >
   >您可以導覽至回轉集編輯影像，點選左側導軌中的&#x200B;**[!UICONTROL 設定成員]**，然後點選個別資產上的「鉛筆」圖示以開啟編輯視窗。

1. 完成編輯時，按一下「保存」。****

## 預覽回轉集{#previewing-spin-sets}

請參閱[預覽資產](/help/assets/previewing-assets.md)。

## 發佈回轉集{#publishing-spin-sets}

請參閱[發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
