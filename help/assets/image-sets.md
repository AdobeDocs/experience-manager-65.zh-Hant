---
title: 影像集
description: 瞭解如何在Dynamic Media使用影像集
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
feature: 影像集，資產管理
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 15%

---


# 影像集 {#image-sets}

「影像集」為使用者提供整合的檢視體驗，讓使用者按一下縮圖影像，即可看到不同的項目檢視。 「影像集」可讓您呈現項目的替代檢視，而檢視器則提供縮放工具，以密切檢查影像。

影像集由具有單字的橫幅指定 `IMAGESET`。此外，如果已發佈影像集，則會顯示以 **[!UICONTROL World]** 圖示表示的發佈日期與上次修改日期(以 **** Pencil圖示表示)在橫幅上。

![chlimage_1-135](assets/chlimage_1-339.png)

在影像集中，您也可以建立「影像集」並新增縮圖，以建立色票。

當您想要以不同的顏色、圖樣或完成顯示項目時，此應用程式特別有用。 若要使用色票建立影像集，您需要針對要呈現給使用者的不同顏色、圖樣或修飾建立一個影像。 您也需要一種顏色、圖樣或修飾色板來表示每種顏色、圖樣或修飾。

例如，假設您想要呈現不同色彩表的頂蓋影像；賬單是紅的，綠的，藍的。 在這種情況下，你需要三杯相同的帽子。 你需要一張紅的，一張綠的，一張藍的。 您也需要紅色、綠色和藍色色票。 顏色色票會當做使用者在「色票集檢視器」中按一下的縮圖，以查看紅嘴、綠嘴或藍嘴的帽子。

>[!NOTE]
>
>如需Assets使用者介面的詳細資訊，請參閱[管理資產](/help/assets/manage-assets.md)。

## 快速入門：影像集{#quick-start-image-sets}

要快速啟動並運行，請執行以下操作：

1. [上傳多個檢視的主要來源影像。](#uploading-assets-in-image-sets)

   首先，上傳影像集的影像。 由於使用者可在影像集檢視器中放大影像，因此當您選擇影像時，請考慮放大影像。 請確定影像在最大尺寸中至少有2000像素，以獲得最佳縮放細節。 Dynamic Media每幅影像的轉譯率高達2500萬像素。 例如，您可使用5000 x 5000百萬像素影像或任何其他大小的組合，最高2500萬像素。

   AEM Assets支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

1. [建立影像集。](#creating-image-sets)

   在「影像集」中，使用者按一下「影像集檢視器」中的縮圖影像。

   若要在「資產」中建立影像集，請點選或按一下「建立>影像集」。**** 然後，新增影像，然後按一下「 **[!UICONTROL 儲存」。]**

   您也可以透過[批次集預設集](/help/assets/config-dms7.md)自動建立影像集。
   >[!IMPORTANT]
   >
   >批集由IPS（映像生產系統）建立，作為資產接收的一部分，並且僅在Dynamic Media-Scene7模式中可用。

   請參閱[準備要上傳和上傳檔案的影像集資產](#uploading-assets-in-image-sets)。

   請參閱[使用選擇器。](/help/assets/working-with-selectors.md)

1. 視需要新增[影像集檢視器預設集](/help/assets/managing-viewer-presets.md)。

   管理員可以建立或修改影像集檢視器預設集。 若要使用檢視器預設集來檢視您的影像集，請選取影像集，然後在左側導軌下拉式功能表中，選取「檢視器」。]****[!UICONTROL 

   請參閱&#x200B;**[!UICONTROL 工具>資產>檢視器預設集]**&#x200B;以建立或編輯檢視器預設集。

1. （可選）[檢視使用批集預設集建立的影像集](/help/assets/image-sets.md#viewing-image-sets)。
1. [預覽影像集。](/help/assets/previewing-assets.md)

   選取「影像集」，您就可以預覽它。 按一下縮圖圖示，以檢查所選檢視器中的影像集。 您可以從左側導軌下拉式選單的&#x200B;**[!UICONTROL 檢視器]**&#x200B;選單中選擇不同的檢視器。

1. [發佈影像集。](/help/assets/publishing-dynamicmedia-assets.md)

   發佈影像集會啟動URL和內嵌代碼。 此外，您必須[發佈您所建立的任何自訂檢視器預設集](/help/assets/managing-viewer-presets.md)。 現成可用的檢視器預設集已發佈。

1. [將URL連結至您的Web應](/help/assets/linking-urls-to-yourwebapplication.md) 用程 [式或內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

   AEM Assets會建立影像集的URL呼叫，並在您發佈影像集後加以啟動。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選擇「影像集」，然後在左側導軌下拉式選單中，選取「**[!UICONTROL 檢視器」。]**

   請參 [閱連結影像集至網頁](/help/assets/linking-urls-to-yourwebapplication.md)[和內嵌影片或影像檢視器](/help/assets/embed-code.md)。

要編輯影像集，請參閱[編輯影像集。](#editing-image-sets) 此外，您還可以檢視和編輯 [影像集屬性](/help/assets/manage-assets.md#editing-properties)。

如果建立集時遇到問題，請參閱[疑難排解Dynamic Media-Scene7模式](/help/assets/troubleshoot-dms7.md#images-and-sets)中的映像和集。

## 上傳影像集{#uploading-assets-in-image-sets}中的資產

首先，上傳影像集的影像。 由於使用者可在影像集檢視器中放大影像，因此當您選擇影像時，請考慮放大影像。 請確定影像在最大尺寸中至少為2000像素。「影像集」支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

您可以像[上傳資產](/help/assets/manage-assets.md#uploading-assets)中的任何其他資產一樣，上傳影像集的影像。

### 準備上傳{#preparing-image-set-assets-for-upload}的影像集資產

在建立影像集之前，請確定影像的大小和格式正確。

若要建立多檢視影像集，您需要顯示來自不同視點的項目或顯示相同項目不同方面的影像。 其目標是強調項目的重要功能，讓檢視者可完整瞭解項目的外觀或行為。

因為使用者可以在影像集中縮放影像，所以請確定影像在最大尺寸中至少為2000像素。 Assets支援許多影像檔案格式，但建議使用無損TIFF、PNG和EPS影像。

>[!NOTE]
>
>此外，如果您使用縮圖來表示產品色票，則需要執行下列動作：
>
>您需要相同影像的暈映或不同像片，以不同的顏色、圖樣或光潔度顯示。 您也需要對應不同顏色、圖樣或修飾的縮圖檔案。 例如，若要以影像集呈現縮圖，並以黑色、棕色和綠色顯示相同的外套，您需要：
>
>* 黑色、棕色和綠色的相同夾克。
>* 黑色、棕色和綠色縮圖。


## 建立影像集{#creating-image-sets}

您可以透過使用者介面或API來建立影像集。 本節說明如何在UI中建立影像集。

>[!NOTE]
>
>您也可以透過[批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自動建立影像集。
>**重要：**&#x200B;批集由IPS（映像生產系統）建立，作為資產接收的一部分，僅在Dynamic Media-Scene7模式中可用。

當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在資產新增後手動重新排序或排序。

>[!NOTE]
>
>檔案名稱中具有&quot;,&quot;（逗號）的資產不支援影像集。

**若要建立影像集**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台，然後點選「導 **[!UICONTROL 覽>資產」。]**&#x200B;導覽至您要建立影像集的位置，然後點選「建 **[!UICONTROL 立>影像集]** 」以開啟「影像集編輯器」頁面。

   您也可以從包含資產的資料夾內建立資產集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁面的&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，輸入影像集的名稱。 名稱會出現在影像集的橫幅中。 （可選）輸入說明。

   ![6_5-影像集——建立新集](assets/6_5_imageset-creatingnewset.png)

1. 執行下列任一項作業：

   * 在「影像集編輯器」頁面的左上角附近，點選「新增資產」。]****[!UICONTROL 

   * 在「影像集編輯器」頁面的中間，點選&#x200B;**[!UICONTROL 以開啟「資產選擇器」。]**
   點選以選取您要納入影像集的資產。 選取的資產上面有核取標籤圖示。完成後，在頁面右上角附近點選&#x200B;**[!UICONTROL Select.]**

   使用「資產選擇器」，您可以輸入關鍵字並點選或按一下「退貨」來搜尋 **[!UICONTROL 資產。]**&#x200B;您也可以套用篩選條件來調整搜尋結果。您可以依路徑、系列、檔案類型和標籤來篩選。選取篩選，然後點選工具 **[!UICONTROL 列上的]** 「篩選」圖示。點選「檢視」圖示並選取「欄檢視」**[!UICONTROL 「欄檢視」]**、「卡片檢視」]**或「清單檢視」，以變更檢視。]****[!UICONTROL **[!UICONTROL 

   請參閱[使用選擇器。](/help/assets/working-with-selectors.md)

   ![6_5-影像集——新增資產](assets/6_5_imageset-addingassets.png)

1. 當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在新增資產後手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以在設定清單上或下重新排序影像。

   ![6_5-影像集——重新排序資產](assets/6_5_imageset-reorderassets.png)

   如果您想要變更縮圖或色票，請按一 **下影像旁** 的+ **縮圖** 圖示，並導覽至您想要的縮圖或色票。選擇完所有影像後，按一下「保存」。]****[!UICONTROL 

1. （可選）執行下列任一項作業：

   * 若要刪除影像，請選取影像並點選「刪除資產」。]****[!UICONTROL 

   * 若要套用預設，請在頁面右上角附近點選&#x200B;**[!UICONTROL Preset]**，然後選取一個預設，一次套用至所有資產。
   >[!NOTE]
   >
   >建立影像集時，您可以變更影像集縮圖，或允許AEM根據影像集中的資產自動選取縮圖。若要選取縮圖，請點選「影像集編輯器」頁面上「標題」欄位上方的「變更縮圖 **** 」，然後選取任何影像 (您也可以導覽至其他檔案夾以尋找影像)。如果您已選取縮圖，然後決定AEM要從影像集產生縮圖，請選取「切換至&#x200B;]****[!UICONTROL &#x200B;自動縮圖」。]****[!UICONTROL 

1. 按一下「**[!UICONTROL 儲存」。]** 您新建立的「影像集」會顯示在您所建立的檔案夾中。

## 查看影像集{#viewing-image-sets}

您可以在使用者介面中建立影像集，或使用[批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自動建立影像集。

>[!IMPORTANT]
>
>批集由IPS [映像生產系統]建立，作為資產接收的一部分，僅在Dynamic Media-Scene7模式中可用。)

不過，使用批集預設集建立的集合，請&#x200B;*not*&#x200B;出現在使用者介面中。 您可以以三種不同的方式檢視這些集。 （即使您在使用者介面中建立影像集，這些方法也可用）。

* 開啟個別資產的屬性。 屬性指出所選資產被參考或成員的設定。 按一下集的名稱，即可查看整個集。

   ![6_5_imageset-asset屬性](assets/6_5_imageset-assetproperties2.png)

* 來自任何組的成員映像。選擇&#x200B;**[!UICONTROL Sets]**&#x200B;菜單以顯示資產所屬的集。

   ![6_5_imageset-setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜索中，可以選擇&#x200B;**[!UICONTROL Filter]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;並選擇&#x200B;**[!UICONTROL Sets.]**

   搜尋會傳回在UI中手動建立或透過批次集預設集自動建立的相符集。 對於自動集，搜索查詢使用「從」搜索標準執行，該搜索標準與基於「包含」搜索標準AEM的搜索標準不同。 將篩選器設定為&#x200B;**[!UICONTROL Sets]**&#x200B;是搜索自動集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以透過使用者介面來檢視集，如[編輯影像集](#editing-image-sets)所述。

## 編輯影像集{#editing-image-sets}

您可以對影像集執行多種編輯工作，例如：

* 將影像新增至影像集。
* 在影像集中重新排序影像。
* 刪除影像集中的資產。
* 套用檢視器預設集。
* 刪除影像集。

**若要編輯影像集**

1. 執行下列任一項作業：

   * 將滑鼠指標暫留在「影像集」資產上，然後點選「**[!UICONTROL 編輯]**」（鉛筆圖示）。
   * 將滑鼠指標暫留在影像集資產上，點選「**[!UICONTROL 選擇]**」（勾選圖示），然後點選工具列上的「編輯」。****
   * 點選影像集資產，然後點選工具列上的&#x200B;**[!UICONTROL Edit]**（鉛筆圖示）。

1. 若要編輯影像集中的影像，請執行下列任一項作業：

   * 若要重新排序資產，請將影像拖曳至新位置（選取重新排序圖示以移動項目）。
   * 若要依遞增或遞減順序排序項目，請按一下欄標題。
   * 若要新增資產或更新現有資產，請按一下「新增資產」。**** 導覽至資產，選取資產，然後點 **** 選頁面右上角的「選取」。

      >[!NOTE]
      >
      >如果您將縮圖的AEM影像取代為其他影像，以刪除該影像，原始資產仍會顯示。
   * 若要刪除資產，請選取資產並點選或按一下「刪除資產」。]****[!UICONTROL 
   * 若要套用預設，請在頁面右上角附近點選&#x200B;**[!UICONTROL Preset]**，然後選取檢視器預設集。
   * 若要新增或變更縮圖，請選取資產右側的縮圖圖示。 導覽至新的縮圖或色票資產，選取它，然後點選&#x200B;**[!UICONTROL 選擇。]**
   * 若要刪除整個影像集，請導覽至影像集，選取它，然後點選「刪除」。]****[!UICONTROL 

   >[!NOTE]
   >
   >您可以導覽至影像集，點選左側導軌中的「設定成員 **** 」，然後點選個別資產上的「鉛筆」圖示以開啟編輯視窗，以編輯影像集中的影像。

1. 完成編輯時，點選「**[!UICONTROL 儲存]**」。

## 預覽影像集{#previewing-image-sets}

請參閱[預覽資產](/help/assets/previewing-assets.md)。

## 發佈影像集{#publishing-image-sets}

請參閱[發佈資產](/help/assets/publishing-dynamicmedia-assets.md)。
