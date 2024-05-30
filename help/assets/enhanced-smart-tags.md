---
title: 增強型智慧標記
description: 增強型智慧標記
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---

# 瞭解、套用及組織智慧標籤 {#enhanced-smart-tags}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | 本文章 |

處理數位資產的組織越來越多地在資產中繼資料中使用分類控制的辭彙。 基本上，它包括員工、合作夥伴和客戶通常用來參照和搜尋特定類別數位資產的關鍵字清單。 使用分類控制的辭彙來標籤資產，可確保輕鬆識別和擷取資產。

相較於自然語言辭彙，根據商業分類法標籤數位資產有助於讓其與公司的業務保持一致，並確保最相關的資產出現在搜尋中。

例如，汽車生產商可以使用模型名稱來標籤汽車影像，這樣在搜尋各種模型的影像以設計促銷活動時，就只會顯示相關影像。

若要讓智慧內容服務套用正確的標籤，請訓練它來辨識您的分類。 若要訓練服務，請先組織一組最能描述這些資產的資產和標籤。 為協助服務學習，請在資產上套用這些標籤，並執行訓練工作流程。

標籤培訓完畢並準備就緒後，該服務現在就能透過標籤工作流程將這些標籤套用至資產。

在背景中，智慧內容服務會使用Adobe Sensei AI架構，根據您的標籤結構和商業分類訓練其影像識別演演算法。 然後，此內容智慧可用來將相關標籤套用至不同的資產集。

智慧型內容服務是託管於的雲端服務 [!DNL Adobe Developer Console]. 若要在中使用，請執行下列動作 [!DNL Adobe Experience Manager]，系統管理員必須整合 [!DNL Experience Manager] 部署方式 [!DNL Adobe Developer Console].

總而言之，以下是使用「智慧內容服務」的主要步驟：

* 上線
* 檢閱資產和標籤（分類定義）
* 訓練智慧內容服務
* 自動標籤

![流程圖](assets/flowchart.gif)

## 必要條件和支援的格式 {#prerequisites}

您必須先確定下列專案要建立整合，才可使用智慧內容服務 [!DNL Adobe Developer Console]：

* 具有組織管理員許可權的Adobe ID帳戶。
* 為您的組織啟用智慧內容服務。
* 若要將智慧內容服務基本套件新增至部署，請授權 [!DNL Adobe Experience Manager Sites] 基礎封裝和 [!DNL Assets] 附加元件。

此服務會將智慧標籤套用至下列MIME型別的資產：

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

此服務會將智慧標籤套用至下列MIME型別的資產轉譯：

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## 上線 {#onboarding}

智慧內容服務可以附加元件的形式購買 [!DNL Experience Manager]. 購買後，系統會傳送電子郵件給您組織的管理員，並附上連結 [!DNL Adobe I/O].

管理員可以按照連結將智慧內容服務與整合 [!DNL Experience Manager]. 若要將服務與整合 [!DNL Experience Manager Assets]，請參閱 [設定智慧標籤](config-smart-tagging.md).

當管理員設定服務並在中新增使用者時，上線流程就會完成 [!DNL Experience Manager].

## 檢閱資產和標籤 {#reviewing-assets-and-tags}

在您上線後，您首先要做的就是找出一組標籤，最能描述您企業環境中的這些影像。

接下來，檢閱影像，找出最能代表您產品的特定業務需求的一組影像。 確保組織集中的資產符合 [智慧內容服務訓練准則](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

將資產新增至資料夾，並從屬性頁面將標籤套用至每個資產。 然後，在此資料夾上執行培訓工作流程。 資產組織集可讓智慧內容服務使用您的分類定義，有效訓練更多資產。

>[!NOTE]
>
>1. 訓練是一個不可撤銷的過程。 Adobe建議您先檢閱已組織資產集中的標籤，然後再對標籤進行智慧內容服務培訓。
>1. 在訓練標籤之前，請參閱 [智慧內容服務訓練准則](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. 第一次訓練智慧內容服務時，Adobe建議您至少在兩個相異標籤上訓練。

## 瞭解 [!DNL Experience Manager] 包含智慧標籤的搜尋結果 {#understandsearch}

根據預設， [!DNL Experience Manager] 搜尋會將搜尋字詞與 `AND` 子句。 使用智慧標籤不會變更此預設行為。 使用智慧標籤會額外新增 `OR` 子句可尋找與智慧標籤相關的任何搜尋字詞。 例如，考慮搜尋 `woman running`. 資產，只有 `woman` 或只是 `running` 根據預設，中繼資料中的關鍵字不會出現在搜尋結果中。 然而，以任一專案標籤的資產 `woman` 或 `running` 使用智慧標籤會出現在此類搜尋查詢中。 所以搜尋結果是，

* 資產，具有 `woman` 和 `running` 中繼資料中的關鍵字。

* 以任一關鍵字標籤的資產。

符合中繼資料欄位中所有搜尋字詞的搜尋結果會先顯示，接著顯示符合智慧標籤中任何搜尋字詞的搜尋結果。 在上述範例中，顯示搜尋結果的大約順序為：

1. 符合的 `woman running` 於各種中繼資料欄位中。
1. 符合的 `woman running` 在智慧標籤中。
1. 符合的 `woman` 或 `running` 在智慧標籤中。

>[!CAUTION]
>
>如果Lucene索引完成於 [!DNL Adobe Experience Manager]，則根據智慧標籤進行的搜尋無法如預期運作。

## 自動標籤資產 {#tagging-assets-automatically}

在您訓練智慧內容服務後，您可以觸發標籤工作流程，以自動將適當的標籤套用至一組不同的類似資產上。

您可以定期或視需要執行標籤工作流程。

>[!NOTE]
>
>標籤工作流程會在資產和資料夾上執行。

### 定期標籤 {#periodic-tagging}

您可以啟用智慧內容服務，定期標籤資料夾中的資產。 開啟資產資料夾的屬性頁面，選取 **[!UICONTROL 啟用智慧標籤]** 在 **[!UICONTROL 詳細資料]** 標籤，並儲存變更。

為資料夾選取此選項後，智慧內容服務會自動標籤資料夾中的資產。 依預設，標籤工作流程每天凌晨12:00執行。

### 隨選標籤 {#on-demand-tagging}

您可以從工作流程控制檯或時間軸觸發標籤工作流程，以立即標籤您的資產。

>[!NOTE]
>
>如果您從時間軸執行標籤工作流程，一次最多可以對15個資產套用標籤。

#### 從工作流程控制檯標籤資產 {#tagging-assets-from-the-workflow-console}

1. 在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 從 **[!UICONTROL 工作流程模型]** 頁面，選取 **[!UICONTROL DAM智慧標籤資產]** 工作流程，然後按一下 **[!UICONTROL 開始工作流程]** 工具列中的。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在 **[!UICONTROL 執行工作流程]** 對話方塊，瀏覽至裝載資料夾，其中包含您要自動套用標籤的資產。
1. 指定工作流程的標題和可選註解。 按一下 **[!UICONTROL 執行]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   若要確認智慧內容服務是否正確標籤您的資產，請導覽至資產資料夾並檢閱標籤。

#### 從時間軸標籤資產 {#tagging-assets-from-the-timeline}

1. 從 [!DNL Assets] 在使用者介面中，選取包含要套用智慧標籤之資產或特定資產的檔案夾。
1. 從左上角，開啟 **[!UICONTROL 時間表]**.
1. 從左側邊欄底部開啟動作，然後按一下 **[!UICONTROL 開始工作流程]**.

   ![start_workflow](assets/start_workflow.png)

1. 選取 **[!UICONTROL DAM智慧標籤資產]** 工作流，並指定工作流程的標題。
1. 按一下 **[!UICONTROL 開始]**. 工作流程會在資產上套用標籤。 若要確認智慧內容服務是否正確標籤您的資產，請導覽至資產資料夾並檢閱標籤。

>[!NOTE]
>
>在後續的標籤週期中，只有已修改的資產會再次使用新訓練的標籤進行標籤。 但是，如果標籤工作流程的最後和目前標籤週期之間的間隔超過24小時，則即使未變更的資產也會標籤。 對於定期標籤工作流程，當時間間隔超過六個月時，會標籤未變更的資產。

## 組織或稽核套用的智慧標籤 {#manage-smart-tags}

您可以組織智慧標籤，移除指派給品牌影像的任何不正確標籤，以便只顯示最相關的標籤。

仲裁智慧標籤也可確保您的影像出現在最相關標籤的搜尋結果中，藉此協助調整以標籤為基礎的影像搜尋。 基本上，這有助於避免無關的影像出現在搜尋結果中。

您也可以為標籤指派較高的排名，以增加其對影像的相關性。 升級影像的標籤會增加搜尋特定標籤時，影像出現在搜尋結果中的機會。

1. 在搜尋方塊中，以標籤作為關鍵字來搜尋資產。
1. 若要識別您找不到與搜尋相關的影像，請檢閱搜尋結果。
1. 選取影像，然後按一下 **[!UICONTROL 管理標籤]** 工具列中的。
1. 從 **[!UICONTROL 管理標籤]** 頁面，檢閱標籤。 如果您不想根據特定標籤來搜尋影像，請選取標籤，然後按一下 **[!UICONTROL 刪除]** 工具列中的。 或者，按一下 `x` 出現在標籤旁的符號。
1. 或者，若要將較高排名指派給標籤，請選取標籤並按一下 **[!UICONTROL 提升]** 工具列中的。 您促銷的標籤會移至 **[!UICONTROL 標籤]** 區段。
1. 按一下 **[!UICONTROL 儲存]** 然後按一下 **[!UICONTROL 確定]**
1. 導覽至 **[!UICONTROL 屬性]** 影像的頁面。 請注意，您提升的標籤會獲得更多關聯性，並會更早出現在搜尋結果中。

## 提示和限制 {#tips-best-practices-limitations}

* 若要訓練模型，請使用最適當的影像。 訓練無法還原，或訓練模型無法移除。 您的標籤正確性取決於目前的訓練，所以請謹慎行事。
* 智慧內容服務的使用限製為每年最多200萬張標籤影像。 任何經過處理和標籤的重複影像都會計為標籤的影像。
* 如果您從時間軸執行標籤工作流程，一次最多可以對15個資產套用標籤。
* 智慧標籤僅適用於PNG和JPG影像格式。 因此，如果支援的資產擁有以這兩種格式建立的轉譯，則會使用智慧標籤標籤。

>[!MORELIKETHIS]
>
>* [概述及如何訓練智慧標籤](enhanced-smart-tags.md)
>* [設定智慧標籤](config-smart-tagging.md)
>* [針對OAuth憑證的智慧標籤進行疑難排解](config-oauth.md)
>* [有關智慧標籤的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
