---
title: 混合媒體集
description: 瞭解如何在動態媒體中處理混合媒體集
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Mixed Media Sets{#mixed-media-sets}

混合媒體集可讓您在單一簡報中混合提供影像、影像集、回轉集和視訊。

混合媒體集由橫幅指定，並加上單字 **[!UICONTROL MixedMediaSet]**。 此外，如果「混合媒體集」已發佈，則會顯示「鉛筆」圖示所指示的發佈日期(以 **[!UICONTROL World]** 圖示指示)與上次修改日期(以 **** Pencil圖示表示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>如需「資產」使用者介面的詳細資訊，請參 [閱「使用Touch UI管理資產」](/help/assets/managing-assets-touch-ui.md)。

## 快速入門：混合媒體集 {#quick-start-mixed-media-sets}

要使用混合媒體集快速啟動並運行，請執行以下步驟：

1. [上傳您的資產](#uploading-assets)。

   首先，上傳混合媒體集的影像和視訊。 如有必要，請建立 [影像集](/help/assets/image-sets.md)[和回轉集](/help/assets/spin-sets.md)。 由於使用者可以在混合媒體集檢視器中放大影像，因此當您選擇影像時，請考量放大比例。 請確定影像在最大尺寸中至少為2000像素。

1. [建立混合媒體集。](#creating-mixed-media-sets)

   若要建立混合媒體集，請從「資產」頁面，點選「建立>混合媒體集 **** 」，然後命名該集合，選擇資產，然後選擇影像的顯示順序。

   請參 [閱使用選擇器。](/help/assets/working-with-selectors.md)

1. 視需要 [設定混合媒體檢視器預設](/help/assets/managing-viewer-presets.md)。

   管理員可以建立或修改混合媒體集檢視器預設集。 若要檢視您的混合媒體與檢視器預設集，請選取混合媒體集，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   請參閱「 **[!UICONTROL 工具>資產>檢視器預設集]** 」以建立或編輯檢視器預設集。

   請參閱 [新增和編輯檢視器預設集。](/help/assets/managing-viewer-presets.md)

1. [預覽混合媒體集。](#previewing-mixed-media-sets)

   選取「混合媒體集」，您就可以預覽它。 按一下縮圖圖示，以檢查所選檢視器中的混合媒體集。 您可以從左側邊欄下拉式選單 **[!UICONTROL 的「檢視器]** 」選單中選擇不同的「檢視器」。

1. [發佈混合媒體集。](#publishing-mixed-media-sets)

   發佈混合媒體集會啟動URL和內嵌字串。 此外，您必須發 [布檢視器預設集](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

1. [將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md) ，或 [內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

   AEM Assets會建立「混合媒體集」的URL呼叫，並在您發佈混合媒體集後啟動這些呼叫。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在您的網站上。

   選取「混合媒體集」，然後在左側導軌下拉式選單中選取「檢 **[!UICONTROL 視器]**」。

   請參 [閱將混合媒體集連結至網頁](/help/assets/linking-urls-to-yourwebapplication.md)[和內嵌視訊或影像檢視器](/help/assets/embed-code.md)。

如果需要，可以編輯混 [合媒體集](#editing-mixed-media-sets)。 此外，您還可以檢視和修改混 [合媒體集屬性](/help/assets/managing-assets-touch-ui.md#editing-properties)。

>[!NOTE]
>
>如果您在建立集時遇到問題，請參 [閱「疑難排解動態媒體- Scene7模式」](/help/assets/troubleshoot-dms7.md)。

## 上傳資產 {#uploading-assets}

首先，上傳混合媒體集的影像和視訊。 由於使用者可以在混合媒體集檢視器中放大影像，因此在您選擇影像時請務必考量放大影像。 請確定影像在最大尺寸中至少為2000像素。

此外，如果您想要將回轉集或影像集新增至混合媒體集，也請建立這些回轉集或影像集。

## 建立混合媒體集 {#creating-mixed-media-sets}

您可以將影像、影像集、回轉集和視訊新增至混合媒體集。 在將檔案、影像集和回轉集新增至混合媒體集之前，請確定檔案、影像集和回轉集已準備好發佈。

當您將資產新增至集合時，資產會自動以字母數字順序新增。 您可以在資產新增後手動重新排序或排序。

**建立混合媒體集**

1. 在「資產」中，導覽至您要建立混合媒體集的位置，然後按一下「建 **[!UICONTROL 立]**」，然後選 **[!UICONTROL 取「混合媒體集」]**。 您也可以從包含資產的資料夾內建立資產集。 顯示混合媒體集編輯器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 在「混合媒體集編輯器」的「標 **[!UICONTROL 題]**」中，輸入混合媒體集的名稱。 名稱會出現在混合媒體集的橫幅中。 （可選）輸入說明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >建立混合媒體集時，您可以變更混合媒體集縮圖，或允許AEM根據混合媒體集中的資產自動選取縮圖。 若要選取縮圖，請按一下「 **[!UICONTROL 變更縮圖]** 」並選取任何影像（您也可以導覽至其他檔案夾以尋找影像）。 如果您已選取縮圖，然後決定要讓AEM從混合媒體集產生縮圖，請選取「切換至 **[!UICONTROL 自動縮圖」]**。

1. 點選「資產選擇器」以選取您要納入混合媒體集的資產。 選擇它們，然後按一下「 **[!UICONTROL 選擇]**」。

   使用「資產選擇器」，您可以輸入關鍵字並點選「回報」來搜尋 **[!UICONTROL 資產]**。 您也可以套用篩選條件來調整搜尋結果。 您可以依路徑、系列、檔案類型和標籤來篩選。 選取篩選，然後從工具列點選 **[!UICONTROL 「篩選]** 」圖示。 通過選擇「視圖」圖 **[!UICONTROL 標]** ，然後選擇「清單視圖」、「列 **[!UICONTROL 視圖」]**&#x200B;或「卡片視圖 **[!UICONTROL 」來更]******&#x200B;改視圖。

   請參 [閱使用選擇器](/help/assets/working-with-selectors.md)。

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. 視需要將資產拖曳至清單上或下方，以重新排序資產(必須選取「重 **[!UICONTROL 新排序]** 」圖示)。

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果您想要新增縮圖，請按一 **下影像旁** 的+ **[!UICONTROL 縮圖]** 圖示，並導覽至您想要的縮圖。 選取完所有縮圖影像後，按一下「 **[!UICONTROL 儲存]**」。

   >[!NOTE]
   >
   >如果您想要新增資產，請點選「 **[!UICONTROL 新增資產」]**。

1. 若要刪除資產，請選取對應的核取方塊，然後點選「刪 **[!UICONTROL 除資產」]**。
1. 若要套用預設，請點選右 **[!UICONTROL 上角的]** 「預設」，然後選取要套用至資產的預設。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。您新建立的「混合媒體集」會顯示在您所建立的資料夾中。

## 編輯混合媒體集 {#editing-mixed-media-sets}

您可以直接在使用者介面中，對混合媒體集中的資產執行各種編輯工作，就像對資產 [中的任何資產一樣](/help/assets/managing-assets-touch-ui.md)。 您也可以在混合媒體集中執行下列動作：

* 將資產新增至混合媒體集。
* 在混合媒體集中重新排序資產。
* 刪除混合媒體集中的資產。
* 套用檢視器預設集。
* 變更預設縮圖。

**要編輯混合媒體集**

1. 執行下列任一項作業：

   * 將滑鼠指標暫留在「混合媒體集」資產上，然後點選「 **[!UICONTROL 編輯]** 」（鉛筆圖示）。
   * 將滑鼠指標暫留在「混合媒體集」資產上，點選「 **[!UICONTROL 選取]** （勾選圖示）」，然後點選工具列上的「 **[!UICONTROL 編輯]** 」。

   * 點選「Mixed Media Set」（混合媒體集）資產，然後點選工 **[!UICONTROL 具列上的]** 「Edit」（鉛筆圖示）。

1. 在混合媒體集編輯器中，執行下列任一操作：

   * 若要重新排序資產——在左側面板中，點選「 **[!UICONTROL 資產]** 」（圖片圖示），將資產拖曳至新位置。
   * 若要新增資產——在工具列上，點選「新增 **[!UICONTROL 資產」]**。 導覽至資產。 對於您要新增的每個資產，將滑鼠指標暫留在資產的影像（而非資產名稱）上，然後點選核取標籤圖示。 在右上角，點選「 **[!UICONTROL Select（選擇）]**」。

   * 若要刪除資產——在左側面板中，點選「 **[!UICONTROL 資產]** 」（圖片圖示），然後選取資產。 在工具列列上點選「刪 **[!UICONTROL 除資產」]**。

   * 若要依資產名稱的遞增或遞減順序排序，請在左側面板中點選「 **[!UICONTROL 資產]** 」（圖片圖示）。 在「資產」標題的 **[!UICONTROL 右側]** ，點選上或下脫字型大小圖示。

      >[!NOTE]
      >
      >    * 若要刪除整個混合媒體集，請從任何檢視模式(例如 **[!UICONTROL 卡片檢視]****[!UICONTROL 或欄檢視]**)導覽至混合媒體集。 將滑鼠指標暫留在資產上，點選核取標籤圖示以加以選取。 按鍵 **[!UICONTROL 盤上的Backspace]** ，或按一下工具列上的 **[!UICONTROL More]** （3個點），然後點選「 **[!UICONTROL Delete]**」。
         >
         >    
      * 您可以在「混合媒體集」中編輯資產，方法是導覽至該集，按一下左側導軌中的「設定成員」 **，然後點選個別資產上的「** Pencil **** 」圖示以開啟編輯視窗。


1. 編輯完 **[!UICONTROL 成時]** ，點選「儲存」。

   >[!NOTE]
   >
   >* 若要編輯混合媒體集中的資產——導覽至混合媒體集。 點選（不要選取）設定，以在「AEM設定預覽」頁面中開啟該設定。 在左側導軌中，按一下向下插入號以開啟下拉式清單，然後點選「設定 **[!UICONTROL 成員」]**。 在「設定成員」頁面中，將滑鼠指標暫留在資產上，然後點選「 **[!UICONTROL 編輯]** 」（鉛筆圖示）以開啟編輯頁面。
      >
      >
   * 要刪除整個混合媒體集——從任何查看模式（如卡片視圖或列視圖），導航到混合媒體集。 將滑鼠暫留在集合上，然後點選「 **選取」** （勾選圖示）。 按鍵 **[!UICONTROL 盤上的Backspace]** ，或點選「 **[!UICONTROL More]** （三個點的列）」，然後點選「 **[!UICONTROL Delete]**」。


## 預覽混合媒體集 {#previewing-mixed-media-sets}

如需如 [何預覽混合媒體集](/help/assets/previewing-assets.md) ，請參閱預覽資產。

## 發佈混合媒體集 {#publishing-mixed-media-sets}

如需如 [何發佈混合媒體集](/help/assets/publishing-dynamicmedia-assets.md) ，請參閱發佈資產。

>[!NOTE]
>
>如果混合媒體集未在您第一次發佈時完全進入傳送服務，您可能需要第二次發佈混合媒體集。

