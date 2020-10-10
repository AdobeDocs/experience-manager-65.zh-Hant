---
title: 增強型智慧標記
description: 增強型智慧標記
contentOwner: AG
translation-type: tm+mt
source-git-commit: 78a101cdf0b4762ff9a3e7320db464df5b96300d
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 8%

---


# 增強型智慧標記 {#enhanced-smart-tags}

## 增強的智慧型標籤概觀 {#overview-of-enhanced-smart-tags}

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制辭彙。 基本上，它包含員工、合作夥伴和客戶常用來參照和搜尋特定類別數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，可確保透過標籤搜尋輕鬆識別和擷取資產。

與自然語言辭彙相比，基於業務分類法標籤數位資產有助於使其與公司業務保持一致，並確保最相關的資產出現在搜尋中。

例如，汽車製造商可以用型號名稱來標籤汽車影像，以便在搜尋各種型號的影像以設計促銷活動時，只顯示相關影像。

要使智慧內容服務應用正確的標籤，您必須對其進行培訓以識別分類。 若要訓練服務，請先組織一組最能說明這些資產的資產和標籤。 在資產上套用這些標籤，並執行培訓工作流程以協助服務學習。

一旦標籤經過訓練並準備就緒後，服務現在可以透過標籤工作流程，將這些標籤套用在資產上。

在背景中，智慧型內容服務使用Adobe Sensei AI架構，針對您的標籤結構和商業分類訓練其影像識別演算法。 然後，此內容智慧會用來將相關標籤套用至不同的資產集。

智慧型內容服務是Adobe I/O上代管的雲端服務。若要在中使 [!DNL Adobe Experience Manager]用，系統管理員必須將您的 [!DNL Experience Manager] 部署與Adobe I/O整合。

總而言之，以下是使用智慧型內容服務的主要步驟：

* 入門
* 查看資產和標籤（分類法定義）
* 培訓智慧型內容服務
* 自動標籤

![流程圖](assets/flowchart.gif)

## 必備條件 {#prerequisites}

在您使用智慧型內容服務之前，請確定以下各項以建立Adobe I/O整合：

* Adobe ID 帳戶具有組織的管理員權限。
* 您的組織已啟用智慧型內容服務。
* 智慧型內容服務基本套件只能新增至已授權基本 [!DNL Sites] 套件和 [!DNL Assets] 附加元件的部署。

## 入門 {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. 在您購買後，系統會寄送電子郵件給您組織的管理員，並附上Adobe I/O的連結。

管理員可以遵循此連結，將智慧型內容服務與整合 [!DNL Experience Manager]。 若要將服務與整合，請 [!DNL Experience Manager Assets]參閱 [設定智慧標籤](config-smart-tagging.md)。

當管理員配置服務並在中添加用戶時，上線過程將完成 [!DNL Experience Manager]。

>[!NOTE]
>
>如果您使用 [!DNL Experience Manager] 6.3或更舊版本，且需要為資產加上標籤服務，請參 [閱智慧標籤](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 智慧型標籤不使用最新的AI功能，因此不如增強的智慧型標籤服務精確。

## 檢閱資產和標籤 {#reviewing-assets-and-tags}

在您登入後，您首先想要識別一組標籤，以便在您的業務環境中最能描述這些影像。

接著，檢閱影像，以識別最能代表您產品符合特定業務需求的影像集。 確保您所策劃的資產符合智慧型內容 [服務訓練方針](smart-tags-training-guidelines.md)。

將資產新增至資料夾，並從屬性頁面將標籤套用至每個資產。 然後，在此資料夾上執行培訓工作流程。 經過組織的資產集使智慧型內容服務能夠使用您的分類定義有效地培訓更多資產。

>[!NOTE]
>
>1. 培訓是不可撤銷的過程。 Adobe建議您在標籤上訓練智慧型內容服務之前，先檢視組織中資產的標籤。
>1. 在進行標籤培訓之前，請參閱智慧型內 [容服務培訓方針](smart-tags-training-guidelines.md)。
>1. 當您第一次訓練智慧型內容服務時，Adobe建議您至少在兩個不同的標籤上進行訓練。


## 培訓智慧型內容服務 {#training-the-smart-content-service}

要讓Smart Content Service識別您的業務分類，請在已包含與您的業務相關的標籤的資產集上運行該分類。 培訓後，服務可以對類似的資產集應用相同的分類法。

您可以多次培訓服務，以提升其套用相關標籤的能力。 在每個訓練週期後，執行標籤工作流程並檢查您的資產是否已適當標籤。

您可以定期或視需要培訓智慧型內容服務。

>[!NOTE]
>
>培訓工作流程僅在資料夾上執行。

### 定期培訓 {#periodic-training}

您可以讓智慧型內容服務定期培訓資料夾中的資產和相關標籤。 開啟資 [!UICONTROL 產資料夾的] 「屬性」頁面，選取「詳細資訊 ******** 」標籤下的「啟用智慧標籤」，然後儲存變更。

![enable_smart_tags](assets/enable_smart_tags.png)

在為資料夾選擇此選項後， [!DNL Experience Manager] 將自動運行培訓工作流，以便對資料夾資產及其標籤上的Smart Content Service進行培訓。 依預設，培訓工作流程每週在星期六的凌晨12:30執行。

### 隨選培訓 {#on-demand-training}

您可以在工作流程主控台(Workflow console)中，視需要訓練智慧型內容服務。

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. 在「執 **[!UICONTROL 行工作流程]** 」對話方塊中，瀏覽至包含標籤資產的裝載資料夾，以訓練服務。
1. 指定工作流程的標題並新增註解。 然後，按一下「 **[!UICONTROL 執行]**」。 資產和標籤會提交以供培訓。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>資料夾中的資產一旦處理好以進行培訓後，後續培訓週期中只會處理修改過的資產。

### 檢視培訓報告 {#viewing-training-reports}

若要檢查智慧型內容服務是否在訓練資產集中的標籤上接受訓練，請從「報告」主控台檢閱訓練工作流程報告。

1. 在介 [!DNL Experience Manager] 面中，前往「 **[!UICONTROL 工具]** >資 **[!UICONTROL 產]** > **[!UICONTROL 報表]**」。
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。Then, click **[!UICONTROL Create]** from the toolbar.
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。To view the report, click **[!UICONTROL View]** from the toolbar.
1. 檢閱報表的詳細資訊。

   報表會顯示您所訓練之標籤的訓練狀態。「培訓狀態」欄 **[!UICONTROL 中的綠色]** ，表示智慧型內容服務已接受標籤的培訓。黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。

   如果您在此報表中未看到標籤，請針對這些標籤重新執行培訓工作流程。

1. 若要下載報表，請從清單中選取報表，然後按一下工 **[!UICONTROL 具列]** 中的下載。 報表會以Microsoft Excel試算表的形式下載。

## 自動標籤資產 {#tagging-assets-automatically}

在您訓練智慧型內容服務後，可以觸發標籤工作流程，自動將適當的標籤套用至不同的類似資產集。

您可以定期或視需要執行標籤工作流程。

>[!NOTE]
>
>標籤工作流程會同時在資產和檔案夾上執行。

### 定期標籤 {#periodic-tagging}

您可以啟用Smart Content Service以定期標籤資料夾中的資產。 開啟資產資料夾的屬性頁面，選取「詳細資 **[!UICONTROL 訊」標籤下的]** 「啟用智 **[!UICONTROL 慧標籤]** 」，並儲存變更。

在為資料夾選取此選項後，Smart Content Service會自動標籤資料夾中的資產。 預設情況下，標籤工作流每天在上午12:00運行。

### 隨選標籤 {#on-demand-tagging}

您可以從下列項目觸發標籤工作流程，以立即標籤資產：

* 工作流程主控台
* 時間軸

>[!NOTE]
>
>如果您從時間軸執行標籤工作流程，一次最多可套用15個資產。

#### 從工作流程主控台標籤資產 {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在「執 **[!UICONTROL 行工作流程]** 」對話方塊中，瀏覽至包含資產的裝載資料夾，您要自動套用標籤。
1. 指定工作流程的標題和選用的註解。 按一 **[!UICONTROL 下Run]**。

   ![tagging_dialog](assets/tagging_dialog.png)

   導覽至資產資料夾並檢閱標籤，以確認Smart Content Service是否正確標籤您的資產。 如需詳細資訊，請參 [閱管理智慧標籤](managing-smart-tags.md)。

#### 從時間軸標籤資產 {#tagging-assets-from-the-timeline}

1. 從使用 [!DNL Assets] 者介面中，選取包含您要套用智慧標籤之資產或特定資產的檔案夾。
1. 從左上角開啟時間 **[!UICONTROL 軸]**。
1. 從左側邊欄底部開啟動作，然後按一下「開 **[!UICONTROL 始工作流程」]**。

   ![start_workflow](assets/start_workflow.png)

1. 選取「 **[!UICONTROL DAM智慧型標籤資產」工作流程]** ，並指定工作流程的標題。
1. 按一 **[!UICONTROL 下開始]**。 工作流程會將您的標籤套用在資產上。 導覽至資產資料夾並檢閱標籤，以確認Smart Content Service是否正確標籤您的資產。 如需詳細資訊，請參 [閱「管理智慧標籤](managing-smart-tags.md)」。

>[!NOTE]
>
>在後續的標籤週期中，只有修改過的資產會再次使用新訓練過的標籤進行標籤。但是，如果標籤工作流程的最後一個標籤週期與目前標籤週期之間的間隔超過24小時，則甚至會標籤未更改的資產。 對於定期標籤工作流程，未變更的資產會在時間間隔超過6個月時加以標籤。

## 提示與限制 {#tips-best-practices-limitations}

* 智慧型內容服務的使用限制為每年最多200萬個標籤影像。 處理和標籤的任何重複影像都會計為標籤影像。
