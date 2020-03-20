---
title: 在Experience Manager中使用參考和多頁資產管理複合資產
description: 瞭解如何從InDesign、Illustrator和Photoshop建立AEM資產的參考。 使用頁面檢視器功能可檢視多頁檔案的個別子頁面，例如PDF、INDD、PPT、PPTX和AI檔案。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# 管理複合和多頁資產 {#managing-compound-assets}

Adobe Experience Manager(AEM)資產可識別已上傳的檔案是否包含對儲存庫中已存在資產的參考。 此功能僅適用於支援的檔案格式。 如果已上傳的資產包含任何AEM資產的參考，則會在已上傳和參考的資產之間建立雙向連結。

除了消除冗餘外，在Adobe Creative Cloud應用程式中參考AEM資產可增強協同作業，並提高使用者的效率和生產力。

AEM Assets支援雙向參照。 您可以在已上傳檔案的資產詳細資料頁面中找到參考的資產。 此外，您也可以在參考資產的資產詳細資料頁面中，檢視AEM資產的參考檔案。

參考會根據參考資產的路徑、檔案ID和例項ID來解析。

## 在Adobe Illustrator中新增AEM Assets做為參考 {#refai}

您可以從Adobe Illustrator檔案中參考現有的AEM資產。

1. 使用 [AEM案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)，將AEM Assets存放庫載入本機電腦上的磁碟機。 在掛載的驅動器中，導航到要引用的資產的位置。
1. 將資產從已掛載的磁碟機拖曳至Illustrator檔案。

1. 將Illustrator檔案儲存至已載入的磁碟機，或 [上傳](/help/assets/managing-assets-touch-ui.md#uploading-assets) 至AEM儲存庫。

1. 工作流程完成後，請前往資產的資產詳細資訊頁面。 現有AEM資產的參考會列在「參考」(References) **[!UICONTROL 欄的]** 「相依性」( **[!UICONTROL Dependencies]** )下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 出現在「相依性」( **[!UICONTROL Dependiences]** )下的引用資產也可由當前相對檔案引用。 要查看資產的引用檔案清單，請按一下「相關性」( **[!UICONTROL Dependencies)下的資產]**。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 按一下工 **[!UICONTROL 具欄中的]** 「查看屬性」。 在「屬 [!UICONTROL 性] 」頁面中，參考目前資產的檔案清單會顯示在「基本」標籤的「參考 **[!UICONTROL 」欄]** 下方 **** 。

   ![在資產詳細資訊的「引用」列中查看Experience Manager資產的引用](assets/asset-references.png)

   *圖：資產詳細資料中的資產參考*

## 在Adobe InDesign中新增AEM資產作為參考 {#add-aem-assets-as-references-in-adobe-indesign}

若要從InDesign檔案中參考AEM資產，請將AEM資產拖曳至InDesign檔案，或將InDesign檔案匯出為ZIP檔案。

AEM Assets中已存在參考的資產。 您可以設定InDesign伺服 [器以擷取子資產](/help/assets/indesign.md)。 InDesign檔案中的內嵌資產會擷取為子資產。

>[!NOTE]
>
>如果InDesign伺服器已代理，InDesign檔案的預覽會內嵌在其XMP中繼資料中。 在這種情況下，不明確需要擷取縮圖。 不過，如果InDesign伺服器未代理，則必須明確擷取InDesign檔案的縮圖。

### 拖曳資產以建立參考 {#create-references-by-dragging-aem-assets}

此程式類似於在Adobe Illustrator [中新增AEM資產做為參考](#refai)。

### 匯出ZIP檔案以建立資產參考 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 執行「建立工作流 [模型」(Create workflow models](/help/sites-developing/workflows-models.md) )中的步驟以建立新工作流。
1. 使用Adobe InDesign的「封裝」功能來匯出檔案。
Adobe InDesign可將檔案和連結的資產匯出為套件。 在這種情況下，匯出的檔案夾包含InDesign檔案中包含子資產的「連結」檔案夾。
1. 建立ZIP檔案並上傳至AEM儲存庫。
1. 啟動工作 `Unarchiver` 流程。
1. 當工作流程完成時，「連結」檔案夾中的參照會自動參照為子資產。 若要檢視參考資產的清單，請導覽至InDesign資產的資產詳細資訊頁面，然後關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector)。

## 在Adobe Photoshop中新增AEM資產作為參考 {#refps}

1. 使用WebDav用戶端，將AEM Assets裝載為磁碟機。
1. 若要在Photoshop檔案中建立AEM資產的參考，請使用Photoshop的「置入」連結功能，導覽至已載入磁碟機中的對應資產。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. 將Photoshop檔案儲存至已載入的磁碟機，或 [上傳](/help/assets/managing-assets-touch-ui.md#uploading-assets) 至AEM儲存庫。
1. 工作流程完成後，現有AEM資產的參考會列在資產詳細資料頁面中。

   若要檢視參考的資產，請關閉 [資產詳細資](/help/sites-authoring/basic-handling.md#rail-selector) 料頁面中的邊欄。

1. 參考的資產也包含其參考的資產清單。 若要檢視參考資產的清單，請導覽至資產詳細資料頁面並關閉邊 [欄](/help/sites-authoring/basic-handling.md#rail-selector)。

>[!NOTE]
>
>複合資產中的資產也可以根據其檔案ID和例項ID加以參考。 此功能僅適用於Adobe Illustrator和Adobe Photoshop版本。 對其他人而言，參照是以主要複合資產中連結資產的相對路徑為基礎，就像在舊版AEM中一樣。

## 建立子資產 {#generate-subassets}

針對支援的多頁格式資產— PDF檔案、AI檔案、Microsoft PowerPoint和Apple Keynote檔案，以及Adobe InDesign檔案— AEM可產生子資產，以對應至原始資產的每個個別頁面。 這些子資產會連結至 *父資產* ，並有助於多頁檢視。 對於所有其他用途，子資產在AEM中會視為一般資產。

子資產產生預設會停用。 若要啟用子資產產生，請依照下列步驟進行：

1. 以管理員身分登入Experience Manager。 存取「 **[!UICONTROL 工具>工作流程>模型]**」。
1. 選取「 **[!UICONTROL DAM更新資產」工作流程]** ，然後按一下「 **[!UICONTROL 編輯」]**。
1. 按一 **[!UICONTROL 下「切換側面板]** 」並找出「 **[!UICONTROL 建立子資產」步驟]** 。 將步驟新增至工作流程。 按一 **[!UICONTROL 下同步]**。

若要產生子資產，請執行下列其中一項作業：

* 新資產：「 [!UICONTROL DAM更新資產] 」工作流程會對任何上傳至AEM的新資產執行。 子資產會針對新的多頁資產自動產生。
* 現有多頁資產：遵循下列任 [!UICONTROL 一步驟手動執行DAM更新資產] :

   * 選取資產，然後按一下「 [!UICONTROL 時間軸] 」以開啟左側面板。 或者，使用鍵盤快速鍵 `alt + 3`。 按一 [!UICONTROL 下「工作流]」，選取「 [!UICONTROL DAM更新資產」]，按一下「開始 [!UICONTROL 」，然後按一]下「繼續啟動」。
   * 選取資產，然後從工具 [!UICONTROL 列按一下「建立] >工作流程」。 從彈出式對話方塊中，選取「 [!UICONTROL DAM更新資產」工作流程] ，按一下「 [!UICONTROL 開始]」，然後按一下「 [!UICONTROL 繼續]」。

尤其是Microsoft Word檔案，請執行 **[!UICONTROL DAM Parse Word檔案工作流程]** 。 它會從 `cq:Page` Microsoft Word檔案的內容產生元件。 從文檔提取的影像從元件中參 `cq:Page` 考。 即使子資產產生已停用，這些影像也會擷取。

## View subassets {#viewing-subassets}

只有當子資產已產生且可用於選取的多頁資產時，才會顯示子資產。 若要檢視產生的子資產，請開啟多頁資產。 在頁面的左上方區域，按一下「左側 ![邊欄圖示](assets/do-not-localize/aem_leftrail_contentonly.png) 」，然後按 **[!UICONTROL 一下清單中的「子資產]** 」。 當您從清單 **[!UICONTROL 中選取]** 「子資產」時。 或者，使用鍵盤快速鍵 `alt + 5`。

![檢視多頁資產的子資產](assets/view_subassets_simulation.gif)

## 檢視多頁檔案的頁面 {#view-pages-of-a-multi-page-file}

您可以使用AEM Assets的「頁面檢視器」功能，檢視多頁檔案，例如PDF、INDD、PPT、PPTX和AI檔案。 開啟多頁資產，然後按一 **[!UICONTROL 下頁面左上角的]** 「檢視頁面」。 開啟的「頁面檢視器」會顯示資產的頁面，以及瀏覽及縮放每個頁面的控制項。

![檢視並檢視多頁資產的頁面](assets/view_multipage_asset_fmr.gif)

若是InDesign，您可以使用InDesign伺服器擷取頁面。 如果在InDesign檔案建立期間儲存了頁面預覽，則頁面擷取不需要InDesign Server。

下列選項可在工具列、左側導軌和頁面檢視器控制項中使用：

* **[!UICONTROL 案頭動作]** ，以使用AEM案頭應用程式開啟或顯示特定子資產。 瞭解如果您 [使用AEM案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) ，如何設定案頭動作。

* **[!UICONTROL 「屬性]** 」(Properties [!UICONTROL )選項可打] 開特定子資產的「屬性」(Properties)頁面。

* **[!UICONTROL 「註解]** 」(Annotate)選項允許您為特定子資產添加註解。 當開啟父資產供檢視時，您在個別子資產上使用的註解會一起收集和顯示。

* **[!UICONTROL 「頁面概述]** 」選項可同時顯示所有子資產。

* **[!UICONTROL 按一下]** 「左側欄」圖示後，左側 ![欄的時間軸選項](assets/do-not-localize/aem_leftrail_contentonly.png) ，會顯示檔案的活動串流。
