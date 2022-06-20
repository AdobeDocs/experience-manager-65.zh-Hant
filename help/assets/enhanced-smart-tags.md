---
title: 增強型智慧標記
description: 增強型智慧標記
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
source-git-commit: dd1e08bee03a6c7b07b32b0fb929d02dad467744
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 1%

---

# 瞭解、應用和建立智慧標籤 {#enhanced-smart-tags}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/enhanced-smart-tags.html?lang=en) |

處理數字資產的組織越來越多地在資產元資料中使用分類控制辭彙。 實際上，它包括一個關鍵字清單，員工、合作夥伴和客戶通常用來引用和搜索特定類別的數字資產。 使用分類控制辭彙標籤資產可確保資產易於識別和檢索。

與自然語言辭彙相比，基於業務分類標籤數字資產有助於使其與公司的業務保持一致，並確保最相關的資產出現在搜索中。

例如，汽車製造商可以用型號名稱標籤汽車影像，以便當搜索各種型號的影像以設計促銷活動時，只顯示相關影像。

要使智慧內容服務應用正確的標籤，請對其進行培訓以識別分類。 要培訓服務，首先建立一組最能描述這些資產的資產和標籤。 要幫助服務學習，請在資產上應用這些標籤並運行培訓工作流。

一旦標籤經過培訓並準備好，該服務現在就可以通過標籤工作流將這些標籤應用於資產。

在後台，智慧內容服務使用Adobe SenseiAI框架，根據標籤結構和業務分類來訓練其影像識別算法。 然後，該內容智慧被用於對不同的資產集應用相關標籤。

Smart Content Service是托管在 [!DNL Adobe Developer Console]。 要在 [!DNL Adobe Experience Manager]，系統管理員必須整合 [!DNL Experience Manager] 部署 [!DNL Adobe Developer Console]。

總之，以下是使用智慧內容服務的主要步驟：

* 入門
* 審閱資產和標籤（分類定義）
* 培訓智慧內容服務
* 自動標籤

![流程圖](assets/flowchart.gif)

## 先決條件和支援的格式 {#prerequisites}

在使用智慧內容服務之前，請確保以下內容在 [!DNL Adobe Developer Console]:

* 具有組織管理員權限的Adobe ID帳戶。
* 為您的組織啟用Smart Content Service服務。
* 將Smart Content Services Base包添加到部署，許可證 [!DNL Adobe Experience Manager Sites] 基本包和 [!DNL Assets] 附件。

該服務將智慧標籤應用於以下MIME類型的資產：

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

該服務將智慧標籤應用於以下MIME類型的資產格式副本：

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## 入門 {#onboarding}

智慧內容服務可作為附件購買 [!DNL Experience Manager]。 購買後，系統會向組織的管理員發送一封電子郵件，其中包含指向 [!DNL Adobe I/O]。

管理員可以遵循連結將智慧內容服務與 [!DNL Experience Manager]。 將服務與 [!DNL Experience Manager Assets]，請參閱 [配置智慧標籤](config-smart-tagging.md)。

當管理員配置服務並在中添加用戶時，登入過程將完成 [!DNL Experience Manager]。

## 查看資產和標籤 {#reviewing-assets-and-tags}

在上架後，您首先要確定一組標籤，這些標籤最適合在您的業務環境中描述這些映像。

接下來，查看影像以確定一組最能代表您產品以滿足特定業務需求的影像。 確保所管理集中的資產符合 [智慧內容服務培訓指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。

將資產添加到資料夾，並將標籤應用到屬性頁面中的每個資產。 然後，在此資料夾上運行培訓工作流。 管理的資產集使智慧內容服務能夠使用分類定義有效地培訓更多資產。

>[!NOTE]
>
>1. 培訓是一個不可撤銷的過程。 Adobe建議您在對標籤上的智慧內容服務進行培訓之前，早早地查看所管理的資產集中的標籤。
>1. 在培訓標籤之前，請參閱 [智慧內容服務培訓指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。
>1. 首次培訓智慧內容服務時，Adobe建議您至少在兩個不同的標籤上對其進行培訓。


## 瞭解 [!DNL Experience Manager] 使用智慧標籤搜索結果 {#understandsearch}

預設情況下， [!DNL Experience Manager] 搜索將搜索詞與 `AND` 。 使用智慧標籤不會更改此預設行為。 使用智慧標籤可添加額外 `OR` 子句，以查找與smart標籤相關的任何搜索項。 例如，請考慮搜索 `woman running`。 僅具有 `woman` 或者 `running` 預設情況下，元資料中的關鍵字不會出現在搜索結果中。 但是，標有 `woman` 或 `running` 在此類搜索查詢中顯示使用智慧標籤。 所以搜索結果是，

* 資產 `woman` 和 `running` 元資料中的關鍵字。

* 標籤了任一關鍵字的智慧資產。

首先顯示與元資料欄位中的所有搜索項相匹配的搜索結果，然後顯示與智慧標籤中任何搜索項相匹配的搜索結果。 在上例中，搜索結果的大致顯示順序是：

1. 匹配項 `woman running` 的子菜單。
1. 匹配項 `woman running` 在智慧標籤中。
1. 匹配項 `woman` 或 `running` 在智慧標籤中。

>[!CAUTION]
>
>如果Lucene索引已完成 [!DNL Adobe Experience Manager]，則基於智慧標籤的搜索不會按預期工作。

## 自動標籤資產 {#tagging-assets-automatically}

在培訓了智慧內容服務後，可以觸發標籤工作流以自動將適當的標籤應用於不同的一組類似資產。

您可以定期或在需要時運行標籤工作流。

>[!NOTE]
>
>標籤工作流在資產和資料夾上運行。

### 定期標籤 {#periodic-tagging}

您可以啟用Smart Content Service定期在資料夾中標籤資產。 開啟資產資料夾的屬性頁，選擇 **[!UICONTROL 啟用智慧標籤]** 下 **[!UICONTROL 詳細資訊]** 的子菜單。

為資料夾選擇此選項後，Smart Content Service會自動為資料夾中的資產標籤。 預設情況下，標籤工作流每天上午12:00運行。

### 按需標籤 {#on-demand-tagging}

您可以從工作流控制台或時間軸觸發標籤工作流，以立即標籤您的資產。

>[!NOTE]
>
>如果從時間軸運行標籤工作流，則一次最多可以對15個資產應用標籤。

#### 從工作流控制台標籤資產 {#tagging-assets-from-the-workflow-console}

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從 **[!UICONTROL 工作流模型]** ，選擇 **[!UICONTROL DAM智慧標籤資產]** 工作流，然後按一下 **[!UICONTROL 啟動工作流]** 的子菜單。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在 **[!UICONTROL 運行工作流]** 對話框，瀏覽到包含要自動應用標籤的資產的負載資料夾。
1. 指定工作流的標題和可選注釋。 按一下 **[!UICONTROL 運行]**。

   ![標籤對話框](assets/tagging_dialog.png)

   要驗證Smart Content Service是否正確標籤了您的資產，請導航到資產資料夾並查看標籤。

#### 從時間線標籤資產 {#tagging-assets-from-the-timeline}

1. 從 [!DNL Assets] 用戶介面，選擇包含要應用智慧標籤的資產或特定資產的資料夾。
1. 從左上角開啟 **[!UICONTROL 時間軸]**。
1. 從左側欄底部開啟操作，然後按一下 **[!UICONTROL 啟動工作流]**。

   ![啟動工作流](assets/start_workflow.png)

1. 選擇 **[!UICONTROL DAM智慧標籤資產]** ，並為工作流指定標題。
1. 按一下 **[!UICONTROL 開始]**。 工作流將標籤應用於資產。 要驗證Smart Content Service是否正確標籤了您的資產，請導航到資產資料夾並查看標籤。

>[!NOTE]
>
>在隨後的標籤循環中，只有修改的資產才用新訓練的標籤重新標籤。 但是，如果標籤工作流的最後一個標籤週期與當前標籤週期之間的間隔超過24小時，則即使未更改的資產也會被標籤。 對於定期標籤工作流，當時間差超過六個月時，將標籤未更改的資產。

## 建立或調整應用的智慧標籤 {#manage-smart-tags}

您可以建立智慧標籤以刪除分配給品牌影像的任何不準確標籤，以便只顯示最相關的標籤。

調節智慧標籤還有助於優化基於標籤的影像搜索，具體方法是確保您的影像出現在最相關標籤的搜索結果中。 本質上，它有助於消除不相關影像在搜索結果中出現的可能性。

您還可以為標籤指定更高的等級，以增加其與影像的相關性。 當搜索特定標籤時，升級影像的標籤會增加在搜索結果中出現影像的可能性。

1. 在搜索框中，使用標籤作為關鍵字來搜索資產。
1. 要標識您找不到與搜索相關的影像，請查看搜索結果。
1. 選擇影像，然後按一下 **[!UICONTROL 管理標籤]** 的子菜單。
1. 從 **[!UICONTROL 管理標籤]** 頁，查看標籤。 如果不希望根據特定標籤搜索影像，請選擇該標籤，然後按一下 **[!UICONTROL 刪除]** 的子菜單。 或者，按一下 `x` 表徵圖。
1. （可選）要為標籤分配更高的級別，請選擇標籤並按一下 **[!UICONTROL 提升]** 的子菜單。 您升級的標籤將移到 **[!UICONTROL 標籤]** 的子菜單。
1. 按一下 **[!UICONTROL 保存]** 然後按一下 **[!UICONTROL 確定]**
1. 導航到 **[!UICONTROL 屬性]** 的子菜單。 請注意，您升級的標籤被分配了更多相關性，並在搜索結果中顯示得更早。

## 提示和限制 {#tips-best-practices-limitations}

* 要訓練模型，請使用最合適的影像。 無法還原培訓或無法刪除培訓模型。 您的標籤準確性取決於當前培訓，因此請小心進行。
* 智慧內容服務的使用限制為每年最多200萬張帶標籤的影像。 處理和標籤的任何重複影像都被計算為標籤影像。
* 如果從時間軸運行標籤工作流，則一次最多可以對15個資產應用標籤。
* 智慧標籤只適用於PNG和JPG影像格式。 因此，以這兩種格式建立格式副本的受支援資產將被標籤為「智慧標籤」。
