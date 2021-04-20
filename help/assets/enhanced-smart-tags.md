---
title: 增強型智慧標記
description: 增強型智慧標記
contentOwner: AG
feature: Smart Tags, Search
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 1%

---


# 瞭解、套用和組織智慧型標籤{#enhanced-smart-tags}

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制辭彙。 基本上，它包含員工、合作夥伴和客戶常用來參照和搜尋特定類別數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，可確保資產可輕鬆識別和擷取。

與自然語言辭彙相比，基於業務分類法標籤數位資產有助於使其與公司業務保持一致，並確保最相關的資產出現在搜尋中。

例如，汽車製造商可以用型號名稱來標籤汽車影像，以便在搜尋各種型號的影像以設計促銷活動時，只顯示相關影像。

要讓Smart Content Service套用正確的標籤，請對其進行培訓以識別您的分類。 若要訓練服務，請先組織一組最能說明這些資產的資產和標籤。 若要協助服務學習，請在資產上套用這些標籤，然後執行培訓工作流程。

一旦標籤經過訓練並準備就緒後，服務現在可以透過標籤工作流程，將這些標籤套用在資產上。

在背景中，智慧型內容服務使用Adobe SenseiAI架構，針對您的標籤結構和商業分類訓練其影像識別演算法。 然後，此內容智慧會用來將相關標籤套用至不同的資產集。

智慧型內容服務是位於[!DNL Adobe Developer Console]的雲端服務。 要在[!DNL Adobe Experience Manager]中使用它，系統管理員必須將[!DNL Experience Manager]部署與[!DNL Adobe Developer Console]整合。

總而言之，以下是使用智慧型內容服務的主要步驟：

* 入門
* 查看資產和標籤（分類法定義）
* 培訓智慧型內容服務
* 自動標籤

![流程圖](assets/flowchart.gif)

## 先決條件和支援的格式{#prerequisites}

在使用智慧型內容服務之前，請確定以下內容以在[!DNL Adobe Developer Console]上建立整合：

* 具有組織管理員權限的Adobe ID帳戶。
* 為您的組織啟用智慧型內容服務。
* 要將Smart Content Services基本包添加到部署中，請許可[!DNL Adobe Experience Manager Sites]基本包和[!DNL Assets]附加模組。

此服務將智慧標籤套用至下列MIME類型的資產：

* image/jpeg
* image/tiff
* image/png
* image/bmp
* image/gif
* image/pjpeg
* image/x-portable-anymap
* image/x-portable-bitmap
* image/x-portable-graymap
* image/x-portable-pixmap
* 影像/x-rgb
* image/x-xbitmap
* image/x-xpixmap
* image/x-icon
* 影像/photoshop
* image/x-photoshop
* 影像/psd
* image/vnd.adobe.photoshop

此服務將「智慧標籤」套用至下列MIME類型的資產轉譯：

* image/jpeg
* image/pjpeg
* image/png

## 入門 {#onboarding}

智慧型內容服務可作為[!DNL Experience Manager]的附加元件購買。 購買後，系統會傳送電子郵件給您組織的管理員，並附上[!DNL Adobe I/O]的連結。

管理員可以遵循該連結將Smart Content Service與[!DNL Experience Manager]整合。 要將服務與[!DNL Experience Manager Assets]整合，請參閱[配置智慧標籤](config-smart-tagging.md)。

當管理員配置服務並在[!DNL Experience Manager]中添加用戶時，上線過程將完成。

>[!NOTE]
>
>如果您使用[!DNL Experience Manager] 6.3或更舊版本，並需要為資產提供標籤服務，請參閱[智慧標籤](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 智慧型標籤不使用最新的AI功能，因此不如增強的智慧型標籤服務精確。

## 檢閱資產和標籤{#reviewing-assets-and-tags}

在上線後，您首先想要識別一組標籤，以便在您的業務環境中最能描述這些影像。

接著，檢閱影像，以識別最能代表您產品符合特定業務需求的影像集。 確保組織集中的資產符合[智慧型內容服務訓練方針](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。

將資產新增至資料夾，並從屬性頁面將標籤套用至每個資產。 然後，在此資料夾上執行培訓工作流程。 經過組織的資產集使智慧型內容服務能夠使用您的分類定義有效地培訓更多資產。

>[!NOTE]
>
>1. 培訓是不可撤銷的過程。 Adobe建議您先檢閱組織中資產的標籤，然後再對標籤上的智慧型內容服務進行訓練。
>1. 在培訓標籤之前，請參閱[智慧型內容服務培訓方針](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。
>1. 當您第一次訓練智慧型內容服務時，Adobe建議您至少在兩個不同的標籤上進行訓練。


## 瞭解[!DNL Experience Manager]搜尋結果與智慧標籤{#understandsearch}

依預設，[!DNL Experience Manager]搜尋會將搜尋詞與`AND`子句結合。 使用智慧型標籤不會變更此預設行為。 使用智慧型標籤會新增額外的`OR`子句，以尋找與智慧型標籤相關的搜尋詞。 例如，請考慮搜索`woman running`。 預設情況下，中繼資料中只包含`woman`或`running`關鍵字的資產不會出現在搜尋結果中。 但是，使用智慧標籤標籤以`woman`或`running`標籤的資產會出現在此類搜尋查詢中。 所以搜索結果是，

* 中繼資料中具有`woman`和`running`關鍵字的資產。

* 使用任一關鍵字標籤智慧資產。

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 在各種中繼資料欄位中符合`woman running`。
1. 在智慧型標籤中符合`woman running`。
1. 在智慧標籤中符合`woman`或`running`。

>[!CAUTION]
>
>如果在[!DNL Adobe Experience Manager]中完成Lucene索引，則基於智慧標籤的搜索將無法如預期般運作。

## 自動標籤資產{#tagging-assets-automatically}

在您訓練智慧型內容服務後，可以觸發標籤工作流程，自動將適當的標籤套用至不同的類似資產集。

您可以定期或視需要執行標籤工作流程。

>[!NOTE]
>
>標籤工作流程會同時在資產和檔案夾上執行。

### 定期標籤{#periodic-tagging}

您可以啟用Smart Content Service以定期標籤資料夾中的資產。 開啟資產資料夾的屬性頁，在&#x200B;**[!UICONTROL Details]**&#x200B;頁籤下選擇&#x200B;**[!UICONTROL 啟用智慧標籤]**，並保存更改。

在為資料夾選取此選項後，Smart Content Service會自動標籤資料夾中的資產。 預設情況下，標籤工作流每天在上午12:00運行。

### 隨選標籤{#on-demand-tagging}

您可以從工作流程主控台或時間軸觸發標籤工作流程，以立即標籤您的資產。

>[!NOTE]
>
>如果您從時間軸執行標籤工作流程，一次最多可套用15個資產。

#### 從工作流程控制台{#tagging-assets-from-the-workflow-console}標籤資產

1. 在[!DNL Experience Manager]介面中，轉至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從&#x200B;**[!UICONTROL 工作流模型]**&#x200B;頁面中，選擇&#x200B;**[!UICONTROL DAM智慧標籤資產]**&#x200B;工作流，然後從工具欄中按一下&#x200B;**[!UICONTROL 啟動工作流]**。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在&#x200B;**[!UICONTROL 執行工作流程]**&#x200B;對話方塊中，瀏覽至包含您要自動套用標籤之資產的裝載資料夾。
1. 指定工作流程的標題和選用的註解。 按一下&#x200B;**[!UICONTROL 運行]**。

   ![tagging_dialog](assets/tagging_dialog.png)

   若要確認Smart Content Service是否正確標籤您的資產，請導覽至資產資料夾並檢閱標籤。

#### 從時間軸{#tagging-assets-from-the-timeline}標籤資產

1. 從[!DNL Assets]使用者介面中，選取包含您要套用智慧標籤之資產或特定資產的檔案夾。
1. 從左上角開啟&#x200B;**[!UICONTROL 時間軸]**。
1. 從左側邊欄底部開啟動作，然後按一下「開始工作流程」。****

   ![start_workflow](assets/start_workflow.png)

1. 選擇&#x200B;**[!UICONTROL DAM智慧型標籤資產]**&#x200B;工作流程，並指定工作流程的標題。
1. 按一下&#x200B;**[!UICONTROL 開始]**。 工作流程會套用資產上的標籤。 若要確認Smart Content Service是否正確標籤您的資產，請導覽至資產資料夾並檢閱標籤。

>[!NOTE]
>
>在後續的標籤週期中，只有修改過的資產會再次使用新訓練的標籤進行標籤。 不過，如果標籤工作流程的最後一個與目前標籤週期之間的間隔超過24小時，則即使未變更的資產也會被標籤。 對於定期標籤工作流程，未變更的資產會在時間間隔超過6個月時加以標籤。

## 組織或協調套用的智慧型標籤{#manage-smart-tags}

您可以組織智慧型標籤，移除指派給品牌影像的任何不正確標籤，以便只顯示最相關的標籤。

協調智慧型標籤也有助於調整以標籤為基礎的影像搜尋，確保影像出現在搜尋結果中，以找出最相關的標籤。 基本上，它有助於消除不相關影像在搜尋結果中顯示的機率。

您也可以指派較高的排名給標籤，以提高其與影像的關聯性。 促銷影像的標籤會增加在搜尋特定標籤時在搜尋結果中顯示的影像機率。

1. 在搜尋方塊中，使用標籤作為關鍵字來搜尋資產。
1. 若要識別與您的搜尋無關的影像，請檢閱搜尋結果。
1. 選擇該影像，然後按一下工具欄中的「管理標籤」。****
1. 在&#x200B;**[!UICONTROL 管理標籤]**&#x200B;頁面中，檢閱標籤。 如果您不想根據特定標籤來搜尋影像，請選取標籤，然後從工具列按一下「刪除」。 ****&#x200B;或者，按一下標籤旁出現的`x`符號。
1. 或者，若要指派較高的排名給標籤，請選取標籤，然後從工具列按一下「提升」。 ****&#x200B;您促銷的標籤會移至&#x200B;**[!UICONTROL Tags]**&#x200B;區段。
1. 按一下&#x200B;**[!UICONTROL 保存]** ，然後按一下&#x200B;**[!UICONTROL 確定]**
1. 導覽至影像的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面。 請注意，您所促銷的標籤會被指派為更相關的標籤，並會出現在搜尋結果的前面。

## 提示和限制{#tips-best-practices-limitations}

* 智慧型內容服務的使用限制為每年最多200萬個標籤影像。 處理和標籤的任何重複影像都會計為標籤影像。
* 如果您從時間軸執行標籤工作流程，一次最多可套用15個資產。
* 智慧型標籤僅適用於PNG和JPG影像格式。 因此，以這兩種格式建立轉譯的受支援資產，會以「智慧標籤」加以標籤。
