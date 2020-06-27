---
title: 使用中的參考和多頁資產管理複合資產 [!DNL Adobe Experience Manager]。
description: 瞭解如何從內部建立數位資產的參考 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]。 使用頁面檢視器功能可檢視多頁檔案的個別子頁面，例如PDF、INDD、PPT、PPTX和AI檔案。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---


# 管理複合和多頁資產 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以識別已上載檔案是否包含對儲存庫中已存在資產的引用。 此功能僅適用於支援的檔案格式。 如果已上傳的資產包含資產的任 [!DNL Experience Manager] 何參考，則會在已上傳和參考的資產之間建立雙向連結。

除了消除冗餘外，在應用程式中參考資 [!DNL Adobe Creative Cloud] 產可增強協作，並提高使用者的效率和生產力。

[!DNL Experience Manager Assets] 支援雙向引用。 您可以在已上傳檔案的資產詳細資料頁面中找到參考的資產。 此外，您還可以在參考資產的資產詳細資料頁面中檢視參考檔案。

參考會根據參考資產的路徑、檔案ID和例項ID來解析。

## 將數位資產新增為 [!DNL Adobe Illustrator] {#refai}

您可以從檔案中參考現有的數位資 [!DNL Adobe Illustrator] 產。

1. 使用 [Experience Manager案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)，擷取本機檔案系統上的數位資產。 導覽至您要參考之資產的檔案系統位置。
1. 將資產從本機資料夾拖曳至檔 [!DNL Illustrator] 案。

1. 將檔案 [!DNL Illustrator] 保存到掛載的驅動器，或 [上傳](/help/assets/managing-assets-touch-ui.md#uploading-assets) 到儲存 [!DNL Experience Manager] 庫。

1. 工作流程完成後，請前往資產的資產詳細資訊頁面。 現有數位資產的參考會列在「參 **[!UICONTROL 考]** 」欄的「相 **[!UICONTROL 依性]** 」下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 出現在「相依性」( **[!UICONTROL Dependiences]** )下的引用資產也可由當前相對檔案引用。 要查看資產的引用檔案清單，請按一下「相關性」( **[!UICONTROL Dependencies)下的資產]**。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 按一下工 **[!UICONTROL 具欄中的]** 「查看屬性」。 在「屬 [!UICONTROL 性] 」頁面中，參考目前資產的檔案清單會顯示在「基本」標籤的「參考 **[!UICONTROL 」欄]** 下方 **** 。

   ![在資產詳細資訊的「引用」列中查看Experience Manager資產的引用](assets/asset-references.png)

   *圖： 資產詳細資料中的資產參考。*

## 將數位資產新增為 [!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}

若要從檔案中參考數位資 [!DNL InDesign] 產，請將資產拖曳至檔 [!DNL InDesign] 案或將檔案 [!DNL InDesign] 匯出為ZIP封存。

中已存在引用的資產 [!DNL Experience Manager Assets]。 您可以設定InDesign Server以 [擷取子資產](indesign.md)。 檔案中的內嵌資 [!DNL InDesign] 產會擷取為子資產。

>[!NOTE]
>
>如果已代 [!DNL InDesign Server] 理，檔案 [!DNL InDesign] 的預覽會內嵌在其XMP中繼資料中。 在這種情況下，不明確需要擷取縮圖。 但是，如果未 [!DNL InDesign Server] 代理，則必須明確提取檔案的縮 [!DNL InDesign] 圖。

### 拖曳資產以建立參考 {#create-references-by-dragging-aem-assets}

此程式類似於在Adobe [Illustrator中新增數位資產做為參考](#refai)。

### 匯出ZIP檔案以建立資產參考 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 執行「建立工作流 [模型」(Create workflow models](/help/sites-developing/workflows-models.md) )中的步驟以建立新工作流。
1. 使用的「封裝」功 [!DNL Adobe InDesign] 能可匯出檔案。 [!DNL Adobe InDesign] 可將檔案和連結的資產匯出為套件。 在這種情況下，匯出的檔案夾包含檔案中包含子資產的「連結」檔案 [!DNL InDesign] 夾。
1. 建立ZIP檔案並將其上傳到儲存 [!DNL Experience Manager] 庫。
1. 啟動工作 `Unarchiver` 流程。
1. 當工作流程完成時，「連結」檔案夾中的參照會自動參照為子資產。 若要檢視參考資產的清單，請導覽至資產的資產詳細資 [!DNL InDesign] 料頁面並關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector)。

## 將數位資產新增為 [!DNL Adobe Photoshop] {#refps}

1. 使用 [!DNL Experience Manager] 案頭應用程式存取 [!DNL Experience Manager Assets]。 下載並顯示本機檔案系統上的資產。 使用中 [!UICONTROL 的「置入連結] 」功能 [!DNL Adobe Photoshop]。 請參閱 [將資產置於案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. 將檔案 [!DNL Photoshop] 保存到掛載的驅動器或 [上載](/help/assets/managing-assets-touch-ui.md#uploading-assets) 到儲存庫 [!DNL Experience Manager] 。
1. 工作流程完成後，資產詳細資 [!DNL Experience Manager] 料頁面中會列出現有資產的參考。

   若要檢視參考的資產，請關閉 [資產詳細資](/help/sites-authoring/basic-handling.md#rail-selector) 料頁面中的邊欄。

1. 參考的資產也包含其參考的資產清單。 若要檢視參考資產的清單，請導覽至資產詳細資料頁面並關閉邊 [欄](/help/sites-authoring/basic-handling.md#rail-selector)。

>[!NOTE]
>
>複合資產中的資產也可以根據其檔案ID和例項ID加以參考。 此功能僅適用於 [!DNL Adobe Illustrator] 和 [!DNL Adobe Photoshop] 版本。 對於其他人，參照是根據在舊版中所做的主要複合資產中連結資產的相對路徑進行的 [!DNL Experience Manager]。

## 建立子資產 {#generate-subassets}

針對支援的多頁格式資產— PDF檔案、AI檔案 [!DNL Microsoft PowerPoint] 和 [!DNL Apple Keynote] 檔案， [!DNL Adobe InDesign] 以及檔案 [!DNL Experience Manager] 可產生對應至原始資產每個個別頁面的子資產。 這些子資產會連結至 *父資產* ，並有助於多頁檢視。 就所有其他目的而言，子資產在中會被視為一般資產 [!DNL Experience Manager]。

子資產產生預設會停用。 若要啟用子資產產生，請依照下列步驟進行：

1. 以管理員 [!DNL Experience Manager] 身分登入。 存取「 **[!UICONTROL 工具>工作流程>模型]**」。
1. 選取「 **[!UICONTROL DAM更新資產」工作流程]** ，然後按一下「 **[!UICONTROL 編輯」]**。
1. 按一 **[!UICONTROL 下「切換側面板]** 」並找出「 **[!UICONTROL 建立子資產」步驟]** 。 將步驟新增至工作流程。 按一 **[!UICONTROL 下同步]**。

若要產生子資產，請執行下列其中一項作業：

* 新資產： 「 [!UICONTROL DAM更新資產] 」工作流程會對任何上傳至的新資產執行 [!DNL Experience Manager]。 子資產會針對新的多頁資產自動產生。
* 現有多頁資產： 遵循下列任 [!UICONTROL 一步驟手動執行DAM更新資產] :

   * 選取資產，然後按一下「 [!UICONTROL 時間軸] 」以開啟左側面板。 或者，使用鍵盤快速鍵 `alt + 3`。 按一 [!UICONTROL 下「工作流]」，選取「 [!UICONTROL DAM更新資產」]，按一下「開始 [!UICONTROL 」，然後按一]下「繼續啟動」。
   * 選取資產，然後從工具 [!UICONTROL 列按一下「建立] >工作流程」。 從彈出式對話方塊中，選取「 [!UICONTROL DAM更新資產」工作流程] ，按一下「 [!UICONTROL 開始]」，然後按一下「 [!UICONTROL 繼續]」。

尤其是Microsoft Word檔案，請執行 **[!UICONTROL DAM Parse Word檔案工作流程]** 。 它會從 `cq:Page` Microsoft Word檔案的內容產生元件。 從文檔提取的影像從元件中參 `cq:Page` 考。 即使子資產產生已停用，這些影像也會擷取。

## View subassets {#viewing-subassets}

只有當子資產已產生且可用於選取的多頁資產時，才會顯示子資產。 若要檢視產生的子資產，請開啟多頁資產。 在頁面的左上方區域，按一下「選 ![項」以開啟左側邊欄](assets/do-not-localize/aem_leftrail_contentonly.png) ，然後從清單中按 **[!UICONTROL 一下子資產]** 。 當您從清單 **[!UICONTROL 中選取]** 「子資產」時。 或者，使用鍵盤快速鍵 `alt + 5`。

![檢視多頁資產的子資產](assets/view_subassets_simulation.gif)

## 檢視多頁檔案的頁面 {#view-pages-of-a-multi-page-file}

您可以使用的「頁面檢視器」功能，檢視多頁檔案，例如PDF、INDD、PPT、PPTX和AI檔案 [!DNL Experience Manager Assets]。 開啟多頁資產，然後按一 **[!UICONTROL 下頁面左上角的]** 「檢視頁面」。 開啟的「頁面檢視器」會顯示資產的頁面，以及瀏覽及縮放每個頁面的控制項。

![檢視並檢視多頁資產的頁面](assets/view_multipage_asset_fmr.gif)

對於 [!DNL InDesign]您，可以使用擷取頁面 [!DNL InDesign Server]。 如果在建立檔案時儲存頁面 [!DNL InDesign] 的預覽，則頁 [!DNL InDesign Server] 面擷取不需要。

下列選項可在工具列、左側導軌和頁面檢視器控制項中使用：

* **[!UICONTROL 案頭動作]** ，以使用案頭應用程式開啟或顯示特定 [!DNL Experience Manager] 子資產。 瞭解如何設 [定案頭動作](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) (如果您使用案頭應用 [!DNL Experience Manager] 程式)。

* **[!UICONTROL 「屬性]** 」(Properties [!UICONTROL )選項可打] 開特定子資產的「屬性」(Properties)頁面。

* **[!UICONTROL 「註解]** 」(Annotate)選項允許您為特定子資產添加註解。 當開啟父資產供檢視時，您在個別子資產上使用的註解會一起收集和顯示。

* **[!UICONTROL 「頁面概述]** 」選項可同時顯示所有子資產。

* **[!UICONTROL 按一下]** 「選項」以開啟左側邊欄後，左側邊欄中的時間軸選項 ![](assets/do-not-localize/aem_leftrail_contentonly.png) ，會顯示檔案的活動串流。

## 最佳實務與限制 {#best-practice-limitation-tips}

* 產生子資產對於任何Experience Manager部署都會耗費大量資源。 如果您要在上傳複雜資產時產生子資產，請在「DAM更新資產」工作流程中新增步驟。 如果您要隨選產生子資產，請建立個別的工作流程以產生子資產。 專用的工作流程可讓您略過DAM更新資產工作流程中的其他步驟，並儲存計算資源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中設定案頭動作](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中建立連結的智慧型物件](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中置入圖形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

