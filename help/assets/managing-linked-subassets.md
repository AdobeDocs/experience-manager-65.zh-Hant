---
title: 使用參考和多個頁面管理複合資產
description: 了解如何從內建立數位資產的參考資料 [!DNL Adobe InDesign], [!DNL Adobe Illustrator]，和 [!DNL Adobe Photoshop]. 使用「頁面檢視器」功能，檢視多頁檔案的個別子資產頁面，例如PDF、INDD、PPT、PPTX和AI檔案。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# 管理複合和多頁資產 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可識別上傳的檔案是否包含對存放庫中已存在資產的參考。 此功能僅支援檔案格式。 如果上傳的資產包含任何 [!DNL Experience Manager] 資產時，上傳和參考的資產之間會建立雙向連結。

除了消除備援外，還會參考 [!DNL Adobe Creative Cloud] 應用程式增強了協作，提高了用戶的效率和工作效率。

[!DNL Experience Manager Assets] 支援雙向引用。 您可以在上傳之檔案的資產詳細資料頁面中找到參考的資產。 此外，您可以在參考資產的資產詳細資訊頁面中檢視參考檔案。

參考會根據所參考資產的路徑、檔案ID和例項ID來解析。

## [!DNL Adobe Illustrator]:新增數位資產作為參考 {#refai}

您可以從 [!DNL Adobe Illustrator] 檔案。

1. 使用 [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)，在本機檔案系統上擷取數位資產。 導覽至您要參考之資產的檔案系統位置。
1. 將資產從本機資料夾拖曳至 [!DNL Illustrator] 檔案。

1. 儲存 [!DNL Illustrator] 檔案到已裝載的驅動器，或 [上傳](/help/assets/manage-assets.md#uploading-assets) 到 [!DNL Experience Manager] 存放庫。

1. 工作流程完成後，前往資產的資產詳細資訊頁面。 現有數位資產的參考資料列於 **[!UICONTROL 相依性]** 在 **[!UICONTROL 參考]** 欄。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 顯示於下方的參考資產 **[!UICONTROL 相依性]** 也可由目前檔案以外的檔案參照。 若要檢視資產參考檔案的清單，請按一下下方 **[!UICONTROL 相依性]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 按一下 **[!UICONTROL 檢視屬性]** 的上界。 在 [!UICONTROL 屬性] 頁面中，參考目前資產的檔案清單會顯示在 **[!UICONTROL 參考]** 欄中 **[!UICONTROL 基本]** 標籤。

   ![在資產詳細資料的「參考」欄中檢視Experience Manager Assets的參考](assets/asset-references.png)

   *圖：資產詳細資料中的資產參考。*

## [!DNL Adobe InDesign]:新增數位資產作為參考 {#add-aem-assets-as-references-in-adobe-indesign}

若要從 [!DNL InDesign] 檔案，將資產拖曳至 [!DNL InDesign] 檔案或匯出 [!DNL InDesign] 檔案。

引用的資產已存在於 [!DNL Experience Manager Assets]. 您可以透過 [配置InDesign Server](indesign.md). 內嵌於 [!DNL InDesign] 檔案會擷取為子資產。

>[!NOTE]
>
>若 [!DNL InDesign Server] 是代理的， [!DNL InDesign] 檔案的XMP中繼資料已內嵌預覽。 在此情況下，不會明確要求縮圖擷取。 但若 [!DNL InDesign Server] 未代理，則必須為顯式提取縮圖 [!DNL InDesign] 檔案。

上傳INDD檔案時，會查詢具有 `xmpMM:InstanceID` 和 `xmpMM:DocumentID` 屬性。

### 拖曳資產以建立參考 {#create-references-by-dragging-aem-assets}

此程式類似於 [將數位資產新增為Adobe Illustrator中的參考](#refai).

### 匯出ZIP檔案以建立資產的參考 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 執行 [建立工作流模型](/help/sites-developing/workflows-models.md) 建立新工作流。
1. 使用 [封裝功能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) of [!DNL Adobe InDesign] 導出文檔。 [!DNL Adobe InDesign] 可以將檔案和連結的資產匯出為套件。 在此情況下，匯出的資料夾包含 `Links` 包含子資產的資料夾 [!DNL InDesign] 檔案。 此 `Links` 資料夾與INDD檔案位於同一資料夾中。
1. 建立ZIP檔案並將其上傳至 [!DNL Experience Manager] 存放庫。
1. 啟動 `Unarchiver` 工作流程。
1. 工作流程完成時，「連結」資料夾中的參照會自動參照為子資產。 若要檢視參考資產的清單，請導覽至 [!DNL InDesign] 資產並關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]:新增數位資產作為參考 {#refps}

1. 使用 [!DNL Experience Manager] 案頭應用程式 [!DNL Experience Manager Assets]. 下載並顯示本機檔案系統上的資產。 使用 [!UICONTROL 置入已連結] 功能 [!DNL Adobe Photoshop]. 請參閱 [將資產置於案頭應用程式中](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. 儲存 [!DNL Photoshop] 檔案到已裝載的驅動器或 [上傳](/help/assets/manage-assets.md#uploading-assets) 到 [!DNL Experience Manager] 存放庫。
1. 工作流程完成後，會參照現有 [!DNL Experience Manager] 資產會列在資產詳細資訊頁面中。

   若要檢視參考的資產，請關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector) （位於資產詳細資訊頁面）。

1. 參考的資產也包含參考的資產清單。 若要檢視參考資產的清單，請導覽至資產詳細資訊頁面，然後關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>複合資產內的資產也可根據其檔案ID和例項ID來參照。 此功能可與 [!DNL Adobe Illustrator] 和 [!DNL Adobe Photoshop] 僅限版本。 對於其他資產，參照是根據主要複合資產中連結資產的相對路徑進行，如舊版 [!DNL Experience Manager].

## 建立子資產 {#generate-subassets}

針對支援的多頁格式資產 — PDF檔案、AI檔案、 [!DNL Microsoft PowerPoint] 和 [!DNL Apple Keynote] 檔案和 [!DNL Adobe InDesign] 檔案 —  [!DNL Experience Manager] 可產生子資產，並對應至原始資產的每個個別頁面。 這些子資產連結至 *上層* 資產，並促進多頁檢視。 至於所有其他用途，子資產在 [!DNL Experience Manager].

子資產產生預設為停用。 若要啟用子資產產生，請遵循下列步驟：

1. 登入 [!DNL Experience Manager] 管理員。 存取 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 選擇 **[!UICONTROL DAM更新資產]** 工作流程，按一下 **[!UICONTROL 編輯]**.
1. 按一下 **[!UICONTROL 切換側面板]** 並找到 **[!UICONTROL 建立子資產]** 步驟。 將步驟新增至工作流程。 按一下&#x200B;**[!UICONTROL 「同步」]**。

若要產生子資產，請執行下列其中一項操作：

* 新資產：此 [!UICONTROL DAM更新資產] 對上傳至的任何新資產執行工作流程 [!DNL Experience Manager]. 子資產會自動為新的多頁資產產生。
* 現有多頁資產：手動執行 [!UICONTROL DAM更新資產] 工作流程（遵循下列任一步驟）:

   * 選取資產，然後按一下 [!UICONTROL 時間表] 以開啟左側面板。 或者，使用鍵盤快速鍵 `alt + 3`. 按一下 [!UICONTROL 開始工作流程]，選取 [!UICONTROL DAM更新資產]，按一下 [!UICONTROL 開始]，然後按一下 [!UICONTROL 繼續].
   * 選取資產，然後按一下 [!UICONTROL 建立] > [!UICONTROL 工作流程] 的上界。 從彈出式對話方塊中，選取 [!UICONTROL DAM更新資產] 工作流程，按一下 [!UICONTROL 開始]，然後按一下 [!UICONTROL 繼續].

尤其是Microsoft Word檔案，請執行 **[!UICONTROL DAM剖析Word檔案]** 工作流程。 它會產生 `cq:Page` 元件。 從檔案擷取的影像會從 `cq:Page` 元件。 即使停用子資產產生，也會擷取這些影像。

>[!NOTE]
>
>在 [!UICONTROL 建立子資產流程 — 步驟屬性] in [!UICONTROL 處理參數]，您可以指定 [!DNL Experience Manager] 產生。 預設值為 5。若要產生所有子資產，請將欄位留空。 如果欄位為負數，則不會產生子資產。

## 檢視子資產 {#viewing-subassets}

只有產生子資產，且該子資產可供選取的多頁資產使用時，才會顯示子資產。 若要檢視產生的子資產，請開啟多頁面資產。 在頁面的左上方區域，按一下 ![開啟左側邊欄的選項](assets/do-not-localize/aem_leftrail_contentonly.png) 按一下 **[!UICONTROL 子資產]** 從清單中。 選取 **[!UICONTROL 子資產]** 從清單中。 或者，使用鍵盤快速鍵 `alt + 5`.

![檢視多頁資產的子資產](assets/view_subassets_simulation.gif)

## 檢視多頁檔案的頁面 {#view-pages-of-a-multi-page-file}

您可以使用的「頁面檢視器」功能，檢視多頁檔案，例如PDF、INDD、PPT、PPTX和AI檔案 [!DNL Experience Manager Assets]. 開啟多頁資產，然後按一下 **[!UICONTROL 檢視頁面]** 從頁面的左上角。 開啟的「頁面檢視器」會顯示資產的頁面，以及瀏覽及縮放每個頁面的控制項。

![檢視及查看多頁資產的頁面](assets/view_multipage_asset_fmr.gif)

針對 [!DNL InDesign]，您可以使用 [!DNL InDesign Server]. 如果預覽的頁面在 [!DNL InDesign] 檔案建立，然後 [!DNL InDesign Server] 不是頁面擷取的必要項目。

工具列、左側邊欄和「頁面檢視器」控制項中提供下列選項：

* **[!UICONTROL 案頭動作]** 若要開啟或顯示特定的子資產，請使用 [!DNL Experience Manager] 案頭應用程式。 了解如何 [配置案頭操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) 如果您使用 [!DNL Experience Manager] 案頭應用程式。

* **[!UICONTROL 屬性]** 選項開啟 [!UICONTROL 屬性] 特定子資產的頁面。

* **[!UICONTROL 注釋]** 選項可讓您為特定子資產加上注釋。 開啟父資產以供檢視時，您在個別子資產上使用的註解會收集並一起顯示。

* **[!UICONTROL 頁面概述]** 選項會同時顯示所有子資產。

* **[!UICONTROL 時間表]** 選項 ![開啟左側邊欄的選項](assets/do-not-localize/aem_leftrail_contentonly.png) 顯示檔案的活動資料流。

## 最佳實務和限制 {#best-practice-limitation-tips}

* 子資產產生對任何 [!DNL Experience Manager] 部署。 如果您在上傳複雜資產時產生子資產，請在「DAM更新資產」工作流程中新增步驟。 如果您要隨需產生子資產，請建立個別的工作流程以產生子資產。 專用的工作流程可讓您略過DAM更新資產工作流程中的其他步驟，並儲存計算資源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中設定案頭動作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中建立連結的智慧型物件](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中放置圖形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

