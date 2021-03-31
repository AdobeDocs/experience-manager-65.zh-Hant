---
title: 使用參考和多頁管理複合資產
description: 瞭解如何從 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]建立數位資產的參考。 使用頁面檢視器功能可檢視多頁檔案的個別子頁面，例如PDF、INDD、PPT、PPTX和AI檔案。
contentOwner: AG
role: 業務從業人員、管理員
feature: 資產管理
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 0%

---


# 管理複合和多頁資產{#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以識別已上載檔案是否包含對儲存庫中已存在資產的引用。此功能僅適用於支援的檔案格式。 如果已上傳的資產包含對[!DNL Experience Manager]資產的任何參考，則會在已上傳和參考的資產之間建立雙向連結。

除了消除冗餘外，在[!DNL Adobe Creative Cloud]應用程式中參考資產可增強協作，並提高使用者的效率和生產力。

[!DNL Experience Manager Assets] 支援雙向引用。您可以在已上傳檔案的資產詳細資料頁面中找到參考的資產。 此外，您還可以在參考資產的資產詳細資料頁面中檢視參考檔案。

參考會根據參考資產的路徑、檔案ID和例項ID來解析。

## [!DNL Adobe Illustrator]:新增數位資產做為參考  {#refai}

您可以從[!DNL Adobe Illustrator]檔案中參考現有的數位資產。

1. 使用[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)擷取本機檔案系統上的數位資產。 導覽至您要參考之資產的檔案系統位置。
1. 將資產從本機資料夾拖曳至[!DNL Illustrator]檔案。

1. 將[!DNL Illustrator]檔案保存到掛載的驅動器，或將[upload](/help/assets/manage-assets.md#uploading-assets)保存到[!DNL Experience Manager]儲存庫。

1. 工作流程完成後，請前往資產的資產詳細資訊頁面。 現有數位資產的參考列在&#x200B;**[!UICONTROL 參考]**&#x200B;欄的&#x200B;**[!UICONTROL 相依性]**&#x200B;下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 出現在&#x200B;**[!UICONTROL Dependencies]**&#x200B;下的引用資產也可以由當前檔案以外的檔案引用。 要查看資產的引用檔案清單，請按一下&#x200B;**[!UICONTROL Dependencies]**&#x200B;下的資產。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 按一下工具欄中的&#x200B;**[!UICONTROL 查看屬性]**。 在[!UICONTROL Properties]頁中，引用當前資產的檔案清單會顯示在&#x200B;**[!UICONTROL Basic]**&#x200B;頁籤的&#x200B;**[!UICONTROL References]**&#x200B;列下。

   ![在資產詳細資訊的「引用」列中查看Experience Manager資產的引用](assets/asset-references.png)

   *圖：資產詳細資料中的資產參考。*

## [!DNL Adobe InDesign]:新增數位資產做為參考  {#add-aem-assets-as-references-in-adobe-indesign}

若要從[!DNL InDesign]檔案中參考數位資產，請將資產拖曳至[!DNL InDesign]檔案，或將[!DNL InDesign]檔案匯出為ZIP封存。

[!DNL Experience Manager Assets]中已存在引用的資產。 您可以通過[配置InDesign Server](indesign.md)提取子資產。 [!DNL InDesign]檔案中的內嵌資產會擷取為子資產。

>[!NOTE]
>
>如果[!DNL InDesign Server]已代理，[!DNL InDesign]檔案的預覽會內嵌在其中繼資料XMP中。 在這種情況下，不明確需要擷取縮圖。 但是，如果[!DNL InDesign Server]未代理，則必須明確提取[!DNL InDesign]檔案的縮圖。

上載INDD檔案時，通過查詢儲存庫中具有`xmpMM:InstanceID`和`xmpMM:DocumentID`屬性的資產來獲取引用。

### 拖曳資產{#create-references-by-dragging-aem-assets}以建立參考

此程式類似於在Adobe Illustrator](#refai)中添加數字資產作為引用。[

### 匯出ZIP檔案{#create-references-to-aem-assets-by-exporting-a-zip-file}以建立資產參考

1. 執行[建立工作流模型](/help/sites-developing/workflows-models.md)中的步驟以建立新工作流。
1. 使用[!DNL Adobe InDesign]的[封裝功能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html)來匯出檔案。 [!DNL Adobe InDesign] 可將檔案和連結的資產匯出為套件。在這種情況下，導出的資料夾包含`Links`資料夾，該資料夾包含[!DNL InDesign]檔案中的子資產。 `Links`資料夾與INDD檔案位於相同的資料夾中。
1. 建立ZIP檔案並將其上傳到[!DNL Experience Manager]儲存庫。
1. 啟動`Unarchiver`工作流。
1. 當工作流程完成時，「連結」檔案夾中的參照會自動參照為子資產。 若要檢視反向連結資產的清單，請導覽至[!DNL InDesign]資產的資產詳細資訊頁面，然後關閉[Rail](/help/sites-authoring/basic-handling.md#rail-selector)。

## [!DNL Adobe Photoshop]:新增數位資產做為參考  {#refps}

1. 使用[!DNL Experience Manager]案頭應用程式存取[!DNL Experience Manager Assets]。 下載並顯示本機檔案系統上的資產。 使用[!DNL Adobe Photoshop]中的[!UICONTROL Place Linked]功能。 請參閱[將資產置於案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. 將[!DNL Photoshop]檔案保存到掛載的驅動器或將[upload](/help/assets/manage-assets.md#uploading-assets)保存到[!DNL Experience Manager]儲存庫。
1. 工作流程完成後，資產詳細資料頁面中會列出現有[!DNL Experience Manager]資產的參考。

   若要檢視參考的資產，請關閉資產詳細資料頁面中的[Rail](/help/sites-authoring/basic-handling.md#rail-selector)。

1. 參考的資產也包含其參考的資產清單。 若要檢視參考資產的清單，請導覽至資產詳細資料頁面並關閉[Rail](/help/sites-authoring/basic-handling.md#rail-selector)。

>[!NOTE]
>
>複合資產中的資產也可以根據其檔案ID和例項ID加以參考。 此功能僅適用於[!DNL Adobe Illustrator]和[!DNL Adobe Photoshop]版本。 對於其他人，參照是根據主複合資產中連結資產的相對路徑進行的，如在舊版[!DNL Experience Manager]中所做的那樣。

## 建立子資產{#generate-subassets}

針對支援的多頁格式資產— PDF檔案、AI檔案、[!DNL Microsoft PowerPoint]和[!DNL Apple Keynote]檔案，以及[!DNL Adobe InDesign]檔案— [!DNL Experience Manager]可產生對應至原始資產每個個別頁面的子資產。 這些子資產會連結至&#x200B;*parent*&#x200B;資產，並有助於多頁檢視。 對於所有其他目的，子資產在[!DNL Experience Manager]中會被視為一般資產。

子資產產生預設會停用。 若要啟用子資產產生，請依照下列步驟進行：

1. 以管理員身份登錄到[!DNL Experience Manager]。 訪問&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 型號]**。
1. 選擇「**[!UICONTROL DAM更新資產]**」工作流，然後按一下「編輯&#x200B;**[!UICONTROL 」。]**
1. 按一下「**[!UICONTROL 切換側面板]**」並找到「建立子資產&#x200B;]**」步驟。**[!UICONTROL &#x200B;將步驟新增至工作流程。 按一下&#x200B;**[!UICONTROL 「同步」]**。

若要產生子資產，請執行下列其中一項作業：

* 新資產：[!UICONTROL DAM更新資產]工作流程會針對上傳至[!DNL Experience Manager]的任何新資產執行。 子資產會針對新的多頁資產自動產生。
* 現有多頁資產：遵循下列任一步驟手動執行[!UICONTROL DAM更新資產]工作流程：

   * 選取資產，然後按一下「時間軸]」以開啟左側面板。 [!UICONTROL 或者，使用鍵盤快速鍵`alt + 3`。 按一下「開始工作流程」，選擇「[!UICONTROL DAM更新資產」，按一下「[!UICONTROL 開始]」，然後按一下「[!UICONTROL 繼續」。]]
   * 選擇資產，然後從工具列按一下「建立 > [!UICONTROL 工作流程]」。 從彈出式對話方塊中，選擇[!UICONTROL DAM Update Asset]工作流程，按一下[!UICONTROL Start]，然後按一下[!UICONTROL Contered]。

特別是對於Microsoft Word文檔，請執行&#x200B;**[!UICONTROL DAM Parse Word Documents]**&#x200B;工作流。 它從Microsoft Word文檔的內容生成`cq:Page`元件。 從文檔中提取的影像是從`cq:Page`元件中引用的。 即使子資產產生已停用，這些影像也會擷取。

## 檢視子資產{#viewing-subassets}

只有當子資產已產生且可用於選取的多頁資產時，才會顯示子資產。 若要檢視產生的子資產，請開啟多頁資產。 在頁面的左上方區域，按一下「![選項」以開啟左側導軌](assets/do-not-localize/aem_leftrail_contentonly.png)，然後按一下清單中的「子資產」。 ****&#x200B;從清單中選擇&#x200B;**[!UICONTROL 子資產]**&#x200B;時。 或者，使用鍵盤快速鍵`alt + 5`。

![檢視多頁資產的子資產](assets/view_subassets_simulation.gif)

## 檢視多頁檔案{#view-pages-of-a-multi-page-file}的頁面

您可以使用[!DNL Experience Manager Assets]的頁面檢視器功能，檢視多頁檔案，例如PDF、INDD、PPT、PPTX和AI檔案。 開啟多頁資產，然後從頁面左上角按一下「檢視頁面」。 ****&#x200B;開啟的「頁面檢視器」會顯示資產的頁面，以及瀏覽及縮放每個頁面的控制項。

![檢視並檢視多頁資產的頁面](assets/view_multipage_asset_fmr.gif)

對於[!DNL InDesign]，您可以使用[!DNL InDesign Server]擷取頁面。 如果在[!DNL InDesign]檔案建立期間儲存頁面預覽，則頁面擷取不需要[!DNL InDesign Server]。

工具列、左側導軌和頁面檢視器控制項中提供下列選項：

* **[!UICONTROL 案頭]** 動作，以使用案頭應用程式開啟或揭示特定 [!DNL Experience Manager] 子資產。瞭解如果您使用[!DNL Experience Manager]案頭應用程式，如何設定Desktop Actions](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)。[

* **[!UICONTROL 「屬]** 性」(Properties)選項打  開特定子資產的「屬性」(Properties)頁。

* **[!UICONTROL Annotateoption可]** 讓您為特定子資產加上註解。當開啟父資產供檢視時，您在個別子資產上使用的註解會一起收集和顯示。

* **[!UICONTROL 「頁面]** 概述」選項會同時顯示所有子資產。

* **[!UICONTROL 按一]** 下「選項」以開啟左側欄位後，左側欄位 ![的「時間](assets/do-not-localize/aem_leftrail_contentonly.png) 線」選項會顯示檔案的活動串流。

## 最佳做法和限制{#best-practice-limitation-tips}

* 子資產開發對於任何[!DNL Experience Manager]部署都會耗費大量資源。 如果您要在上傳複雜資產時產生子資產，請在「DAM更新資產」工作流程中新增步驟。 如果您要隨選產生子資產，請建立個別的工作流程以產生子資產。 專用的工作流程可讓您略過DAM更新資產工作流程中的其他步驟，並儲存計算資源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager配置案頭操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop建立連結的智慧型物件](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign置入圖形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

