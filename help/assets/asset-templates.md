---
title: 中的資產模板 [!DNL Adobe Experience Manager Assets]。
description: 瞭解資產範本 [!DNL Adobe Experience Manager Assets] ，以及如何使用資產範本建立行銷文宣。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---


# Asset templates {#asset-templates}

資產範本是一類特殊的資產，可協助您快速將視覺化豐富的內容重新用於數位和印刷媒體。 資產範本包含兩個部分：固定訊息區段和可編輯區段。 固定訊息區段可包含專屬內容，例如品牌標誌和禁止編輯的版權資訊。 可編輯的區段可在欄位中包含視覺和文字內容，可編輯這些內容以自訂訊息。

在確保全球標牌安全的同時，靈活地進行有限的編輯，使資產模板成為快速調整內容和分發內容的理想構件，以便用於各種功能的內容製品。 重新調整內容用途有助於降低管理印刷和數位通道的成本，並跨這些通道提供全方位且一致的體驗。

身為行銷人員，您可以在內部儲存及管理範本， [!DNL Experience Manager Assets] 並使用單一基本範本輕鬆建立多種個人化的列印體驗。 您可以建立各種類型的行銷文宣，包括簡介手冊、傳單、明信片、名片等，以便向客戶清楚傳達行銷訊息。 您也可以從現有或新的列印輸出組合多頁列印輸出。 最重要的是，您可以輕鬆同時提供數位和印刷體驗，為使用者提供一致、整合的體驗。

雖然資產範本大多是 [!DNL Adobe InDesign] 檔案，但熟悉程 [!DNL Adobe InDesign] 度並不妨礙製作亮眼的文物。 建立目錄時，您不需將范 [!DNL Adobe InDesign] 本的欄位與您的產品欄位對應。 您可以直接在Web介面上，在WYSIWYG模式下編輯範本。 不過，若 [!DNL Adobe InDesign] 要處理編輯變更，您必須先設定為 [!DNL Experience Manager Assets] 與整合 [!DNL Adobe InDesign Server]。

從網頁介面編 [!DNL Adobe InDesign] 輯範本的能力，有助於促進創意人員與行銷人員之間更緊密的協作。 內容速度的提高縮短了行銷資料的上市時間。

您可以使用資產範本達成下列目標：

* 從網頁介面修改可編輯的範本欄位。
* 控制文字的基本樣式，例如字型大小、樣式和標籤層級的文字。
* 使用內容選擇器變更範本內的影像。
* 預覽範本編輯。
* 合併多個範本檔案以建立多頁對象。

當您為宣傳品選擇模板時， [!DNL Experience Manager Assets] 將建立可編輯的模板副本。 原始範本會保留，以確保全域標牌保持完整，並可重複使用以強製品牌一致性。

您可以以INDD、PDF或JPG格式匯出父資料夾中的更新檔。 您也可以將這些格式的輸出下載至本機檔案系統。

## 建立宣傳品 {#creating-a-collateral}

假設您想要建立數位可列印的宣傳品，例如簡介手冊、傳單和廣告，以便在即將到來的宣傳活動中展示，並與全球的經銷商分享。 根據範本建立宣傳品有助於跨通道提供統一的客戶體驗。 設計人員可以使用創意解決方案（例如單頁或多頁）建立促銷活動範本，並 [!DNL InDesign] 為您上傳范 [!DNL Experience Manager Assets] 本。 在建立宣傳品之前，請先將一或多個INDD範本上傳至並提 [!DNL Experience Manager] 供使用。

1. 在介面 [!DNL Experience Manager] 中，按一下「 [!UICONTROL 資產」]。

1. 從選項中選擇「模 **[!UICONTROL 板」]**。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 按一下 **[!UICONTROL 建立]**，然後從菜單中選擇要建立的宣傳品。 例如，選擇「手 **[!UICONTROL 冊」]**。

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 將一或多個INDD範本上傳至並提 [!DNL Experience Manager] 前使用。 選擇手冊的範本，然後按一下「下 **[!UICONTROL 一步]**」。

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. 指定手冊的名稱和選用說明。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可選）按一 **[!UICONTROL 下「標籤]** 」，然後為手冊選取一或多個標籤。 按一 **[!UICONTROL 下「確認]** 」以確認您的選擇。

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. 按一下&#x200B;**[!UICONTROL 建立]**。對話方塊會確認已建立新的手冊。 按一 **[!UICONTROL 下「開啟]** 」，以編輯模式開啟手冊。

   <!--![chlimage_1-106](assets/.png) -->

   或者，關閉對話方塊並導覽至您開始使用的「範本」頁面中的資料夾，以檢視您建立的手冊。 在卡片檢視中，文宣的類型會出現在其縮圖上。 例如，在此例中，縮圖上會顯 [!UICONTROL 示「手冊] 」一詞。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 編輯宣傳品 {#editing-a-collateral}

您可以在建立宣傳品後立即加以編輯。 或者，您也可以從「範本」頁 [!UICONTROL 面或資產] 頁面開啟它。

1. 要開啟文宣進行編輯，請執行下列操作之一：

   * 開啟您在「建立宣傳品」步驟7中建立的宣傳品(在本例中 [為手冊)](/help/assets/asset-templates.md#creating-a-collateral)。
   * 從「模板」頁面，導航到建立宣傳品的資料夾，然後按一下宣傳品縮圖上的「 [!UICONTROL Edit] quick action（編輯快速操作）」。
   * 在宣傳品的資產頁面中，按一下工 **[!UICONTROL 具列中的]** 「編輯」。
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   資產搜尋器和文字編輯器會顯示在頁面的左側。 文字編輯器預設為開啟。

   您可以使用文字編輯器修改要在文字欄位中顯示的文字。 您可以在標籤層級修改字型大小、樣式、顏色和文字。

   使用資產搜尋器，您可以瀏覽或搜尋範本中的影 [!DNL Experience Manager Assets] 像，並將範本中可編輯的影像取代為您選擇的影像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可編輯的內容會顯示在右側。 若要在中編輯欄位，范 [!DNL Experience Manager Assets]本中的對應欄位必須在中標籤 [!DNL InDesign]。 換言之，它們應在中標示為可編輯 [!DNL InDesign]。

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >請確定您的 [!DNL Experience Manager] 部署已與整合， [!DNL InDesign Server] 以便 [!DNL Experience Manager Assets] 從範本擷取資料並 [!DNL InDesign] 加以編輯。 如需詳細資訊，請 [參閱將Experience Manager Assets與InDesign Server整合](/help/assets/indesign.md)。

1. 若要修改可編輯欄位中的文字，請按一下可編輯欄位清單中的文字欄位，然後編輯欄位中的文字。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以編輯文字屬性，例如字型樣式、顏色和大小，使用提供的選項。

1. 按一 **[!UICONTROL 下「預覽]** 」以預覽文字變更。

   ![檢視變更](assets/view-changes.png)

1. 若要交換影像，請按一下「資 **[!UICONTROL 產搜尋器」]**。

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. 從可編輯欄位清單中選取影像欄位，然後從資產選擇器拖曳所要的影像至可編輯欄位。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您也可以使用關鍵字、標籤，並根據其發佈狀態來搜尋影像。 您可以瀏覽整個存 [!DNL Experience Manager Assets] 儲庫，並瀏覽到所需映像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 按一 **[!UICONTROL 下「預覽]** 」以預覽影像。

   ![檢視變更](assets/view-changes.png)

1. 要編輯多頁宣傳品中的特定頁面，請使用底部的頁面導覽器。

   ![頁面導覽器](assets/page-navigator.png)

1. 按一 **[!UICONTROL 下工具列上的]** 「預覽」，以預覽所有變更。 按一下 **[!UICONTROL 完成]** ，保存對宣傳品的編輯更改。

   >[!NOTE]
   >
   >只有當宣傳品中可編輯的影像欄位沒有任何缺少的表徵圖時，才會啟用「預覽」和「完成」選項。 如果您的宣傳品中缺少圖示，則是因 [!DNL Experience Manager] 為無法解析範本中的影 [!DNL InDesign] 像。 通常， [!DNL Experience Manager] 在下列情況下無法解析影像：
   >
   >* 影像未內嵌在基礎範本 [!DNL InDesign] 中。
   >* 從本機檔案系統連結影像。

   >
   >若要啟 [!DNL Experience Manager] 用解析影像，請執行下列動作：
   >
   >* 在建立範本時內嵌影 [!DNL InDesign] 像(請參閱 [關於連結和內嵌圖形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >* 載入 [!DNL Experience Manager] 您的本機檔案系統，然後將遺失的圖示與中的現有資產對應 [!DNL Experience Manager]。

   >
   >如需有關使用檔案的詳 [!DNL InDesign] 細資訊，請 [參閱Experience Manager中使用InDesign檔案的最佳實務](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)。

1. 若要產生手冊的PDF轉譯，請在對話方塊中選取Acrobat選項，然後按一下「繼 **[!UICONTROL 續]**」。
1. 宣傳品是在您開始使用的資料夾中建立的。 要查看轉譯，請開啟宣傳品並從「GlobalNav」列 **[!UICONTROL 表中選擇]** 「轉譯」。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 按一下轉譯清單中的PDF轉譯，以下載PDF檔案。 開啟PDF檔案以檢閱文宣。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合併宣傳品 {#merge-collateral}

1. 在介面 [!DNL Experience Manager] 中，按一 [!UICONTROL 下導覽頁面上的] 「資產」。

1. 從選項中選擇「模 **[!UICONTROL 板」]**。

1. 按一 **[!UICONTROL 下「建立]** 」，然後從選 **[!UICONTROL 單選擇「合併]** 」。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 在「範本 [!UICONTROL 合併] 」頁面中，按一 **[!UICONTROL 下「合]** 並 ![新增資產](assets/do-not-localize/assets_add_icon.png)」。

1. 導航到要合併的宣傳品的位置，按一下要合併的宣傳品的縮圖以選擇它們。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您也可以從Omnisearch方塊中搜尋範本。

   您可以瀏覽儲存庫 [!DNL Experience Manager Assets] 或系列，並導航到所需模板的位置，然後選擇這些模板進行合併。

   ![chlimage_1-124](assets/chlimage_1-329.png)

   您可以套用各種篩選條件來搜尋所需的範本。 例如，您可以根據檔案類型或標籤來搜尋範本。

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Click **[!UICONTROL Next]** from the toolbar.
1. 在「預 **[!UICONTROL 覽與重新排序]** 」畫面中，視需要重新排列範本，並預覽要合併的範本選擇。 然後，從工具 **[!UICONTROL 列按一下]** 「下一步」。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在「配 [!UICONTROL 置模板] 」螢幕中，指定宣傳品的名稱。 （可選）指定您認為適當的任何標籤。 如果您想要匯出PDF格式的輸出，請選 **[!UICONTROL 取Acrobat(.PDF)]**。 預設情況下，文宣將導出為JPG和格 [!DNL InDesign] 式。 要更改多頁文宣的顯示縮略圖，請按一下「更改縮 **[!UICONTROL 略圖」]**。

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 按一 **[!UICONTROL 下「儲存]** 」，然後按一 **[!UICONTROL 下對話方塊中的「確定]** 」以關閉對話方塊。 多頁宣傳資料是在您開始使用的資料夾中建立。

   >[!NOTE]
   >
   >您以後無法編輯合併的宣傳品，也無法用它來建立其他宣傳品。

## 最佳實務與限制 {#best-practices-limitations-tips}

* 編輯 [!DNL InDesign] 器在標 [!DNL Experience Manager] 記層級運作，而單一標籤下的所有文字都視為單一實體。 若要在編輯時保留文字格式和樣式，請個別標籤每個段落（或使用不同樣式的文字）。
