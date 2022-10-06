---
title: 資產範本
description: 了解資產範本，位於 [!DNL Adobe Experience Manager Assets] 以及如何使用資產範本建立行銷宣傳資料。
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# 資產範本 {#asset-templates}

資產範本是特殊的資產類別，可協助您快速重新調整視覺化豐富內容的用途，以用於數位和列印媒體。 資產範本包含兩個部分：固定訊息區段和可編輯區段。 固定報文傳送部分可包含專有內容，如品牌徽標和禁用編輯的版權資訊。 可編輯的區段可包含欄位中的視覺和文字內容，可編輯這些欄位以自訂訊息。

在保護全球標牌的同時進行有限編輯的靈活性，使資產範本成為快速調整內容和發佈內容的理想砌塊，並可作為各種功能的內容成品。 重新調整內容用途有助於降低管理列印和數位頻道的成本，並在這些頻道間提供全方位且一致的體驗。

身為行銷人員，您可以在 [!DNL Experience Manager Assets] 並使用單一基本範本，輕鬆建立多個個人化的列印體驗。 您可以建立各種類型的行銷宣傳資料，包括小冊子、傳單、明信片、名片等，以便向客戶清晰地傳達您的行銷訊息。 您也可以從現有或新的打印輸出組合多頁打印輸出。 最重要的是，您可以輕鬆同時提供數位和列印體驗，為使用者提供一致且整合的體驗。

雖然資產範本大多為 [!DNL Adobe InDesign] 檔案，熟練程度 [!DNL Adobe InDesign] 不是創造恆星物品的障礙。 您不需要映射 [!DNL Adobe InDesign] 範本，以及建立目錄時需要的產品欄位。 您可以直接在Web介面上以WYSIWYG模式編輯模板。 不過， [!DNL Adobe InDesign] 若要處理編輯變更，您必須先設定 [!DNL Experience Manager Assets] 整合 [!DNL Adobe InDesign Server].

編輯功能 [!DNL Adobe InDesign] 網頁介面的範本有助於促進創意與行銷人員之間更緊密的協作。 內容速度的提高縮短了營銷抵押品的上市時間。

您可以使用資產範本達成下列目標：

* 從Web介面修改可編輯的範本欄位。
* 控制文本的基本樣式，例如字型大小、樣式和標籤級別的類型。
* 使用內容選擇器變更範本內的影像。
* 預覽範本編輯。
* 合併多個模板檔案以建立多頁對象。

當您為抵押品選擇模板時， [!DNL Experience Manager Assets] 建立可編輯的範本復本。 原始範本會保留，以確保您的全域標牌保持不變，且可重複使用以強製品牌一致性。

您可以以INDD、PDF或JPG格式，匯出父資料夾內更新的檔案。 您也可以將這些格式的輸出下載到您的本機檔案系統。

## 建立抵押品 {#creating-a-collateral}

假設您想要製作可打印的數位宣傳資料，例如手冊、傳單和廣告，以供即將推出的活動之用，並與全球特賣店分享。 根據範本建立宣傳資料有助於跨管道提供統一的客戶體驗。 設計人員可以使用創意解決方案(例如 [!DNL InDesign] 並上傳範本至 [!DNL Experience Manager Assets] 為了你。 建立宣傳資料之前，請先將一個或多個INDD模板上載到，並在 [!DNL Experience Manager] 事先。

1. 在 [!DNL Experience Manager] 介面按一下 [!UICONTROL 資產].

1. 從選項中，選擇 **[!UICONTROL 範本]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 按一下 **[!UICONTROL 建立]**，然後從菜單中選擇要建立的抵押品。 例如，選擇 **[!UICONTROL 手冊]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 上傳一或多個INDD範本，並可在 [!DNL Experience Manager] 事先。 選擇手冊的模板，然後按一下 **[!UICONTROL 下一個]**.
1. 指定手冊的名稱和可選說明。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （選用）按一下 **[!UICONTROL 標籤]** 並為手冊選擇一個或多個標籤。 按一下 **[!UICONTROL 確認]** 以確認您的選取。
1. 按一下&#x200B;**[!UICONTROL 建立]**。對話方塊會確認已建立新手冊。 按一下 **[!UICONTROL 開啟]** 以編輯模式開啟手冊。

   <!--![chlimage_1-106](assets/.png) -->

   或者，關閉對話框，導航到您開始的「模板」頁中的資料夾，以查看您建立的手冊。 宣傳品的類型會顯示在其縮圖上的卡片視圖中。 例如，在此例中， [!UICONTROL 手冊] 會顯示在縮圖上。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 編輯宣傳品 {#editing-a-collateral}

建立宣傳資料後，您可以立即編輯它。 或者，您也可以從 [!UICONTROL 範本] 頁面或資產頁面。

1. 要開啟宣傳資料進行編輯，請執行以下操作之一：

   * 開啟您在 [建立抵押品](/help/assets/asset-templates.md#creating-a-collateral).
   * 從「模板」頁，導航至建立宣傳品的資料夾，然後按一下 [!UICONTROL 編輯] 對宣傳資料縮圖快速採取行動。
   * 在宣傳品的資產頁面中，按一下 **[!UICONTROL 編輯]** 的上界。
   * 選擇宣傳品並按一下 **[!UICONTROL 編輯]** 的上界。

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   資產尋找器和文字編輯器會顯示在頁面左側。 文字編輯器預設為開啟。

   您可以使用文字編輯器來修改要顯示在文字欄位中的文字。 您可以在標籤層級修改字型大小、樣式、顏色和類型。

   使用資產尋找器，您可以在中瀏覽或搜尋影像 [!DNL Experience Manager Assets] 並將範本中可編輯的影像取代為您所選擇的影像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可編輯的項目會顯示在右側。 讓欄位可在 [!DNL Experience Manager Assets]，範本中的對應欄位必須在中加上標籤 [!DNL InDesign]. 換言之，它們應在 [!DNL InDesign].

   >[!NOTE]
   >
   >確保 [!DNL Experience Manager] 部署與 [!DNL InDesign Server] 啟用 [!DNL Experience Manager Assets] 從中擷取資料 [!DNL InDesign] 範本，並讓其可供編輯。 如需詳細資訊，請參閱 [將Experience Manager Assets與InDesign Server整合](/help/assets/indesign.md).

1. 要修改可編輯欄位中的文本，請按一下可編輯欄位清單中的文本欄位，並編輯欄位中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以使用提供的選項編輯文本屬性，例如字型樣式、顏色和大小。

1. 按一下 **[!UICONTROL 預覽]** 來預覽文本更改。

1. 要交換影像，請按一下 **[!UICONTROL 資產尋找器]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. 從可編輯欄位清單中選取影像欄位，然後從資產選擇器拖曳所需影像至可編輯欄位。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您也可以使用關鍵字、標籤，並根據其發佈狀態來搜尋影像。 您可以瀏覽 [!DNL Experience Manager Assets] 儲存庫，並導覽至所需影像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 按一下 **[!UICONTROL 預覽]** 來預覽影像。
1. 要編輯多頁宣傳資料中的特定頁，請使用底部的頁導航器。

1. 按一下 **[!UICONTROL 預覽]** 在工具列上預覽所有變更。 按一下 **[!UICONTROL 完成]** 以保存對宣傳資料的編輯更改。

   >[!NOTE]
   >
   >只有當宣傳品中可編輯的影像欄位沒有缺少任何表徵圖時，才會啟用「預覽」和「完成」選項。 如果您的宣傳資料中缺少表徵圖，那是因為 [!DNL Experience Manager] 無法解析 [!DNL InDesign] 範本。 通常， [!DNL Experience Manager] 在下列情況下無法解析影像：
   >
   >* 映像未嵌入到基礎 [!DNL InDesign] 範本。
   >* 從本地檔案系統連結影像。

   >
   >啟用 [!DNL Experience Manager] 要解析影像，請執行以下操作：
   >
   >* 建立時內嵌影像 [!DNL InDesign] 範本(請參閱 [關於連結和嵌入式圖形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >* 裝載 [!DNL Experience Manager] 將遺失的圖示對應至本機檔案系統，然後將 [!DNL Experience Manager].

   >
   >如需使用的詳細資訊 [!DNL InDesign] 文檔，請參閱 [使用InDesign檔案的最佳實務Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. 若要為手冊產生PDF轉譯，請在對話方塊中選取「Acrobat」選項，然後按一下 **[!UICONTROL 繼續]**.
1. 宣傳資料建立在您開始使用的資料夾中。 要查看格式副本，請開啟宣傳資料並選擇 **[!UICONTROL 轉譯]** 從GlobalNav清單中。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 從轉譯清單按一下PDF轉譯，以下載PDF檔案。 開啟PDF檔案以審核宣傳資料。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合併抵押品 {#merge-collateral}

1. 在 [!DNL Experience Manager] 介面按一下 [!UICONTROL 資產] （導覽頁面）。

1. 從選項中，選擇 **[!UICONTROL 範本]**.

1. 按一下 **[!UICONTROL 建立]** 和選擇 **[!UICONTROL 合併]** 的上界。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 從 [!UICONTROL 範本合併] 頁面，按一下 **[!UICONTROL 合併]** ![新增資產](assets/do-not-localize/assets_add_icon.png).

1. 導航到要合併的宣傳品的位置，按一下要合併的宣傳品的縮圖以選擇它們。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您也可以從Omnisearch方塊搜尋範本。

   您可以瀏覽 [!DNL Experience Manager Assets] 儲存庫或集合，並導覽至所需範本的位置，然後選取它們以合併。

   您可以套用各種篩選器以搜尋所需的範本。 例如，您可以根據檔案類型或標籤來搜尋範本。

1. 按一下 **[!UICONTROL 下一個]** 的上界。
1. 在 **[!UICONTROL 預覽和重新排序]** 螢幕中，視需要重新排列模板，並預覽要合併的模板選擇。 然後，按一下 **[!UICONTROL 下一個]** 的上界。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在 [!UICONTROL 配置模板] 螢幕中，指定宣傳品的名稱。 （可選）指定您認為適當的任何標籤。 如果要以PDF格式導出輸出，請選擇 **[!UICONTROL Acrobat(.PDF)]**. 預設情況下，抵押品會以JPG和 [!DNL InDesign] 格式。 要更改多頁宣傳資料的顯示縮圖，請按一下 **[!UICONTROL 變更縮圖]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 按一下 **[!UICONTROL 儲存]** 然後按一下 **[!UICONTROL 確定]** ，以關閉對話方塊。 多頁宣傳資料建立在您開始使用的資料夾中。

   >[!NOTE]
   >
   >您以後不能編輯合併的宣傳資料，也不能使用它建立其他宣傳資料。

## 最佳實務和限制 {#best-practices-limitations-tips}

* 此 [!DNL InDesign] 編輯器 [!DNL Experience Manager] 可在標籤層級運作，且單一標籤下的所有文字都視為單一實體。 若要在編輯時保留文字格式和樣式，請個別標籤每個段落（或使用不同樣式的文字）。
