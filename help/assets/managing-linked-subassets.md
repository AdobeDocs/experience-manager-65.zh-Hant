---
title: 管理具有引用和多頁面的複合資產
description: 瞭解如何從 [!DNL Adobe InDesign]、 [!DNL Adobe Illustrator]和 [!DNL Adobe Photoshop]內建立數位資產的參考。 使用「頁面檢視器」功能可檢視多頁檔案的個別子資產頁面，例如PDF、INDD、PPT、PPTX和AI檔案。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# 管理複合和多頁資產 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets]可識別上傳的檔案是否包含已存在於存放庫中的資產參照。 此功能僅適用於支援的檔案格式。 如果上傳的資產包含對[!DNL Experience Manager]個資產的任何參考，系統會在上傳和參考的資產之間建立雙向連結。

除了消除備援之外，參考[!DNL Adobe Creative Cloud]應用程式中的資產可加強共同作業，並提高使用者的效率和生產力。

[!DNL Experience Manager Assets]支援雙向參考。 您可以在上傳檔案的資產詳細資訊頁面中找到引用的資產。 此外，您還可以在參照資產的資產詳細資訊頁面中檢視參照檔案。

參照是根據參照資產的路徑、檔案ID和例項ID來解析。

## [!DNL Adobe Illustrator]：新增數位資產作為參考 {#refai}

您可以從[!DNL Adobe Illustrator]檔案中參考現有的數位資產。

1. 使用[[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hant)，在本機檔案系統上擷取數位資產。 導覽至您要參考之資產的檔案系統位置。
1. 將資產從本機資料夾拖曳至[!DNL Illustrator]檔案。

1. 將[!DNL Illustrator]檔案儲存至掛載的磁碟機，或[上傳](/help/assets/manage-assets.md#uploading-assets)至[!DNL Experience Manager]存放庫。

1. 工作流程完成後，請前往資產的資產詳細資訊頁面。 對現有數位資產的參考列在&#x200B;**[!UICONTROL 參考]**&#x200B;欄的&#x200B;**[!UICONTROL 相依性]**&#x200B;下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 出現在&#x200B;**[!UICONTROL 相依性]**&#x200B;下的參考資產也可以由目前檔案以外的檔案參考。 若要檢視資產的參考檔案清單，請按一下&#x200B;**[!UICONTROL 相依性]**&#x200B;下方的資產。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 按一下工具列中的&#x200B;**[!UICONTROL 檢視內容]**。 在[!UICONTROL Properties]頁面中，參考目前資產的檔案清單會顯示在&#x200B;**[!UICONTROL Basic]**&#x200B;索引標籤的&#x200B;**[!UICONTROL References]**&#x200B;欄下。

   ![在資產詳細資料的「參考」欄中檢視Experience Manager Assets的參考](assets/asset-references.png)

   *圖：資產詳細資料中的資產參考。*

## [!DNL Adobe InDesign]：新增數位資產作為參考 {#add-aem-assets-as-references-in-adobe-indesign}

若要從[!DNL InDesign]檔案中參考數位資產，請將資產拖曳至[!DNL InDesign]檔案，或將[!DNL InDesign]檔案匯出為ZIP封存。

引用的資產已存在於[!DNL Experience Manager Assets]中。 您可以透過[設定InDesign Server](indesign.md)來擷取子資產。 [!DNL InDesign]檔案中的內嵌資產會擷取為子資產。

>[!NOTE]
>
>如果[!DNL InDesign Server]已進行代理處理，[!DNL InDesign]個檔案的預覽已內嵌於其XMP中繼資料中。 在此情況下，不會明確要求縮圖擷取。 不過，如果[!DNL InDesign Server]不是代理的，則必須明確擷取[!DNL InDesign]檔案的縮圖。

上傳INDD檔案時，會透過查詢存放庫中有`xmpMM:InstanceID`和`xmpMM:DocumentID`屬性的資產來擷取參考。

### 透過拖曳資產建立引用 {#create-references-by-dragging-aem-assets}

此程式類似於[在Adobe Illustrator](#refai)中新增數位資產作為參考。

### 透過匯出ZIP檔案來建立資產的參考 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 執行[建立工作流程模型](/help/sites-developing/workflows-models.md)中的步驟以建立工作流程。
1. 使用[!DNL Adobe InDesign]的[封裝功能](https://helpx.adobe.com/tw/indesign/how-to/indesign-package-files-for-handoff.html)匯出檔案。 [!DNL Adobe InDesign]可以將檔案和連結的資產匯出為套件。 在此案例中，匯出的資料夾包含`Links`資料夾，其中包含[!DNL InDesign]檔案中的子資產。 `Links`資料夾與INDD檔案位於相同的資料夾中。
1. 建立ZIP檔案並將其上傳至[!DNL Experience Manager]存放庫。
1. 啟動`Unarchiver`工作流程。
1. 工作流程完成時，連結資料夾中的參照會自動參照為子資產。 若要檢視引用的資產清單，請導覽至[!DNL InDesign]資產的資產詳細資訊頁面，並關閉[邊欄](/help/sites-authoring/basic-handling.md#rail-selector)。

## [!DNL Adobe Photoshop]：新增數位資產作為參考 {#refps}

1. 使用[!DNL Experience Manager]案頭應用程式來存取[!DNL Experience Manager Assets]。 下載並顯示本機檔案系統上的資產。 在[!DNL Adobe Photoshop]中使用[!UICONTROL 放置連結]功能。 請參閱[將資產放入案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hant#place-assets-in-native-documents)。

1. 儲存在[!DNL Photoshop]檔案中至掛載的磁碟機或[上傳](/help/assets/manage-assets.md#uploading-assets)至[!DNL Experience Manager]存放庫。
1. 工作流程完成後，現有[!DNL Experience Manager]資產的參考會列在資產詳細資訊頁面中。

   若要檢視參照的資產，請關閉資產詳細資訊頁面中的[邊欄](/help/sites-authoring/basic-handling.md#rail-selector)。

1. 引用的資產也包含從中引用這些資產的清單。 若要檢視參考的資產清單，請導覽至資產詳細資料頁面並關閉[邊欄](/help/sites-authoring/basic-handling.md#rail-selector)。

>[!NOTE]
>
>複合資產中的資產也可以根據其檔案ID和例項ID進行引用。 此功能僅適用於[!DNL Adobe Illustrator]和[!DNL Adobe Photoshop]版本。 對於其他人，會根據主要複合資產中連結資產的相對路徑完成參考，如同在舊版[!DNL Experience Manager]中一樣。

## 建立子資產 {#generate-subassets}

對於支援的多頁格式資產 — PDF檔案、AI檔案、[!DNL Microsoft PowerPoint]和[!DNL Apple Keynote]檔案，以及[!DNL Adobe InDesign]檔案 — [!DNL Experience Manager]可以產生與原始資產的每個個別頁面相對應的子資產。 這些子資產已連結至&#x200B;*上層*&#x200B;資產，有助於進行多頁檢視。 就所有其他目的而言，會將子資產視為[!DNL Experience Manager]中的一般資產。

子資產產生功能預設為停用。 若要啟用子資產產生功能，請執行下列步驟：

1. 以系統管理員身分登入[!DNL Experience Manager]。 存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 選取&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 按一下&#x200B;**[!UICONTROL 切換側面板]**&#x200B;並找到&#x200B;**[!UICONTROL 建立子資產]**&#x200B;步驟。 將步驟新增至工作流程。 按一下&#x200B;**[!UICONTROL 「同步」]**。

若要產生子資產，請執行下列任一項作業：

* 新資產： [!UICONTROL DAM更新Assets]工作流程會在任何上傳至[!DNL Experience Manager]的新資產上執行。 系統會自動為新多頁資產產生子資產。
* 現有的多頁資產：在執行以下任一步驟後，手動執行[!UICONTROL DAM更新Assets]工作流程：

   * 選取資產並按一下[!UICONTROL 時間軸]以開啟左側面板。 或者，使用鍵盤快速鍵`alt + 3`。 按一下「[!UICONTROL 開始工作流程]」、選取「[!UICONTROL DAM更新資產]」、按一下「[!UICONTROL 開始]」，然後按一下「[!UICONTROL 繼續]」。
   * 選取資產，然後從工具列按一下[!UICONTROL 建立] > [!UICONTROL 工作流程]。 從快顯對話方塊中，選取[!UICONTROL DAM更新資產]工作流程，按一下[!UICONTROL 開始]，然後按一下[!UICONTROL 繼續]。

尤其是Microsoft Word檔案，請執行&#x200B;**[!UICONTROL DAM Parse Word檔案]**&#x200B;工作流程。 它會從Microsoft Word檔案的內容產生`cq:Page`元件。 從檔案擷取的影像是從`cq:Page`元件參照的。 即使停用子資產產生，也會擷取這些影像。

>[!NOTE]
>
>在[!UICONTROL 處理引數]的[!UICONTROL 建立子資產程式 — 步驟屬性]中，您可以指定[!DNL Experience Manager]產生的子資產數目。 預設值為 5。若要產生所有子資產，請將此欄位留空。 如果欄位有負值，則不會產生任何子資產。

## 檢視子資產 {#viewing-subassets}

只有在產生子資產且可用於所選的多頁資產時，才會顯示子資產。 若要檢視產生的子資產，請開啟多頁資產。 在頁面的左上角區域，按一下![開啟左側邊欄](assets/do-not-localize/aem_leftrail_contentonly.png)的選項，然後從清單按一下&#x200B;**[!UICONTROL 子資產]**。 當您從清單中選取&#x200B;**[!UICONTROL 子資產]**&#x200B;時。 或者，使用鍵盤快速鍵`alt + 5`。

![檢視多頁資產的子資產](assets/view_subassets_simulation.gif)

## 檢視多頁檔案的頁面 {#view-pages-of-a-multi-page-file}

您可以使用[!DNL Experience Manager Assets]的頁面檢視器功能來檢視多頁檔案，例如PDF、INDD、PPT、PPTX和AI檔案。 開啟多頁資產，然後按一下頁面左上角的&#x200B;**[!UICONTROL 檢視頁面]**。 開啟的頁面檢視器會顯示資產的頁面，以及用來瀏覽和縮放每個頁面的控制項。

![檢視並檢視多頁資產的頁面](assets/view_multipage_asset_fmr.gif)

對於[!DNL InDesign]，您可以使用[!DNL InDesign Server]擷取頁面。 如果頁面預覽是在[!DNL InDesign]檔案建立期間儲存，則頁面擷取不需要[!DNL InDesign Server]。

工具列、左側邊欄及「頁面檢視器」控制項中有以下選項：

* **[!UICONTROL 案頭動作]**&#x200B;使用[!DNL Experience Manager]案頭應用程式開啟或顯示特定子資產。 瞭解如何[設定案頭動作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hant#desktopactions-v2) （如果您使用[!DNL Experience Manager]案頭應用程式）。

* **[!UICONTROL 屬性]**&#x200B;選項會開啟特定子資產的[!UICONTROL 屬性]頁面。

* **[!UICONTROL 註釋]**&#x200B;選項可讓您為特定子資產加上註釋。 當您開啟父資產以供檢視時，會收集並顯示您用於個別子資產的註解。

* **[!UICONTROL 頁面總覽]**&#x200B;選項會同時顯示所有子資產。

* 按一下![開啟左側邊欄的選項](assets/do-not-localize/aem_leftrail_contentonly.png)後，左側邊欄中的&#x200B;**[!UICONTROL 時間軸]**&#x200B;選項會顯示檔案的活動資料流。

## 最佳作法和限制 {#best-practice-limitation-tips}

* 在任何[!DNL Experience Manager]部署中，產生子資產可能會非常耗費資源。 如果您在上傳複雜資產時產生子資產，請在「DAM更新資產」工作流程中新增步驟。 如果您要隨選產生子資產，請建立個別的工作流程以產生子資產。 專用的工作流程可讓您略過DAM更新資產工作流程中的其他步驟，並儲存運算資源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hant)
>* [在Adobe Experience Manager中設定案頭動作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hant#desktopactions-v2)
>* [在Adobe Photoshop中建立連結智慧物件](https://helpx.adobe.com/tw/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中放置圖形](https://helpx.adobe.com/tw/indesign/using/placing-graphics.html)
