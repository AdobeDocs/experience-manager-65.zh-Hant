---
title: 使用智慧型內容服務設定資產標籤
description: 瞭解如何使用智慧型內容服務在 [!DNL Adobe Experience Manager]中設定智慧型標籤和增強的智慧型標籤。
contentOwner: AG
role: 管理員
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '2171'
ht-degree: 25%

---


# 準備[!DNL Assets]進行智慧標籤{#configure-asset-tagging-using-the-smart-content-service}

在您開始使用智慧型內容服務標籤資產之前，請先將[!DNL Experience Manager Assets]與Adobe開發人員主控台整合，以運用[!DNL Adobe Sensei]的智慧型服務。 一旦設定好後，請使用幾張影像和標籤來訓練服務。

在您使用智慧型內容服務之前，請確定下列事項：

* [使用 Adobe 開發人員控制台進行整合](#integrate-adobe-io).
* [培訓智慧型內容服務](#training-the-smart-content-service)。

* 安裝最新的[[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)。

## 使用 Adobe 開發人員控制台進行整合 {#integrate-adobe-io}

當您與Adobe開發人員主控台整合時，[!DNL Experience Manager]伺服器會先使用Adobe開發人員主控台閘道驗證您的服務認證，然後再將您的要求轉送至智慧型內容服務。 若要整合，您需要擁有組織管理員權限的Adobe ID帳戶，以及為您的組織購買並啟用的智慧型內容服務授權。

若要設定智慧型內容服務，請依照下列頂層步驟：

1. 要生成公鑰，請[在[!DNL Experience Manager]中建立智慧內容服務](#obtain-public-certificate)配置。 [取得公開憑證](#obtain-public-certificate)以進行 OAuth 整合。

1. [在 Adobe 開發人員控制台中建立整合](#create-adobe-i-o-integration)，並上傳產生的公開金鑰。

1. [使用Adobe開](#configure-smart-content-service) 發人員主控台的API金鑰和其他認證來設定您的部署。

1. [測試設定](#validate-the-configuration)。

1. （可選）[啟用資產上傳的自動標籤](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

### 通過建立Smart Content Service配置{#obtain-public-certificate}獲取公共證書

公開憑證可讓您在 Adobe 開發人員控制台上驗證設定檔。

1. 在[!DNL Experience Manager]用戶介面中，訪問&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 舊Cloud Services]**。

1. 在「Cloud Services」頁中，按一下「資產智慧標籤」下的「立即配置」。********

1. 在&#x200B;**[!UICONTROL 建立配置]**&#x200B;對話框中，指定智慧標籤配置的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。

1. 在&#x200B;**[!UICONTROL 智AEM慧型內容服務]**&#x200B;對話方塊中，使用下列值：

   **[!UICONTROL 服務 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**: `https://ims-na1.adobelogin.com`

   現在將其他欄位留空（稍後將提供）。 按一下&#x200B;**[!UICONTROL 「確定」]**。

   ![Experience Manager智慧型內容服務對話方塊，以提供內容服務URL](assets/aem_scs.png)


   *圖：「智慧型內容服務」對話方塊，提供內容服務URL*

   >[!NOTE]
   >
   >以[!UICONTROL 服務URL]提供的URL無法透過瀏覽器存取，並產生404錯誤。 此配置與[!UICONTROL 服務URL]參數的值相同，工作正常。 有關整體服務狀態和維護計畫，請參見[https://status.adobe.com](https://status.adobe.com)。

1. 按一下「下載OAuth整合的公用憑證&#x200B;**[!UICONTROL 」，然後下載公用憑證檔案`AEM-SmartTags.crt`。]**

   ![為智慧標籤服務建立的設定的表示](assets/smart-tags-download-public-cert.png)


   *圖：智慧標籤服務的設定。*

#### 在證書過期時重新配置{#certrenew}

證書過期後，將不再受信任。 您無法更新已過期的憑證。若要新增憑證，請依照下列步驟進行。

1. 以管理員身分登入您的 [!DNL Experience Manager] 部署。按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到 **[!UICONTROL dam-update-service]** 使用者後按一下該使用者。按一下「**[!UICONTROL 密鑰庫]**」頁籤。

1. 刪除憑證已過期的現有 **[!UICONTROL similaritysearch]** 金鑰存放區。按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![刪除Keystore中現有的相似性搜索條目以添加安全證書](assets/smarttags_delete_similaritysearch_keystore.png)


   *圖：刪除Keystore中 `similaritysearch` 的現有條目以添加安全證書。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. 若要下載公用憑證，請按一下「下載OAuth整合的公用憑證&#x200B;]**」。**[!UICONTROL 

1. 存取[https://console.adobe.io](https://console.adobe.io)，並導覽至&#x200B;**[!UICONTROL Integrations]**&#x200B;頁面上現有的智慧型內容服務。 上傳新憑證。 如需詳細資訊，請參閱[建立Adobe開發人員主控台整合](#create-adobe-i-o-integration)中的指示。

### 建立Adobe開發人員主控台整合{#create-adobe-i-o-integration}

若要使用智慧型內容服務API，請在Adobe開發人員主控台中建立整合，以取得[!UICONTROL API金鑰](產生於Adobe開發人員主控台整合的[!UICONTROL 用戶端ID]欄位)、[!UICONTROL 技術帳戶ID]、[!UICONTROL 組織[!UICONTROL [!DNL Experience Manager]中雲端組態的資產智慧標籤服務設定]的ID]和[!UICONTROL 用戶端密碼]。

1. 在瀏覽器中存取 [https://console.adobe.io](https://console.adobe.io/)。選取適當的帳戶，並確認相關聯的組織角色是系統管理員。

1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。

1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**[!UICONTROL 「上傳您的公開金鑰」]**。提供從 [!DNL Experience Manager] 下載的憑證檔案。畫面上會顯示[!UICONTROL 已成功上傳公開金鑰]訊息。按一下&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 建立新服務帳戶(JWT)認證頁] 顯示服務帳戶的公鑰。

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 「智慧內容服務」]**。按一下&#x200B;**[!UICONTROL 「儲存已設定的 API」]**。

   此時會出現一個頁面，顯示更多關於設定的資訊。請保持此頁面的開啟，以複製並新增這些值至[!DNL Experience Manager]雲端設定的[!UICONTROL 資產智慧標籤服務設定]中，以設定智慧標籤。

   ![在「概覽」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)


   *圖：Adobe開發人員主控台整合的詳細資訊*

### 配置Smart Content Service {#configure-smart-content-service}

若要設定整合，請使用「Adobe開發人員主控台」整合中的[!UICONTROL TECHNICAL ACCOUNT ID]、[!UICONTROL ORGANIZATION ID]、[!UICONTROL CLIENT SECRET]和[!UICONTROL CLIENT ID]欄位。 建立智慧型標籤雲端設定可讓您驗證來自[!DNL Experience Manager]部署的API要求。

1. 在[!DNL Experience Manager]中，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 舊Cloud Services]**&#x200B;以開啟[!UICONTROL Cloud Services]控制台。

1. 在&#x200B;**[!UICONTROL Assets Smart Tags]**&#x200B;下，開啟上述建立的組態。 在服務設定頁上，按一下&#x200B;**[!UICONTROL 編輯]**。

1. 在「 **[!UICONTROL AEM Smart Content Service]** 」對話方塊中 **[!UICONTROL ，使用「服務URL」和「授權伺服器」欄位的預先填入值]****** 。

1. 對於[!UICONTROL Api金鑰]、[!UICONTROL 技術帳戶ID]、[!UICONTROL 組織ID]和[!UICONTROL 客戶機密碼]欄位，複製並使用[Adobe開發人員控制台整合](#create-adobe-i-o-integration)中生成的下列值。

   | [!UICONTROL 資產智慧標記服務設定] | [!DNL Adobe Developer Console] 整合欄位 |
   |--- |--- |
   | [!UICONTROL API 金鑰] | [!UICONTROL 用戶端ID] |
   | [!UICONTROL 技術帳戶 ID] | [!UICONTROL 技術帳戶ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL 用戶端密碼] | [!UICONTROL 用戶端密碼] |

### 驗證設定 {#validate-the-configuration}

完成配置後，可使用JMX MBean來驗證配置。 若要驗證，請遵循下列步驟。

1. 在`https://[aem_server]:[port]`訪問[!DNL Experience Manager]伺服器。

1. 轉至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**&#x200B;以開啟OSGi控制台。 按一下&#x200B;**[!UICONTROL Main] > [!UICONTROL JMX]**。

1. 按一下 `com.day.cq.dam.similaritysearch.internal.impl`. 它開啟&#x200B;**[!UICONTROL SimiliaritySearch雜項任務]**。

1. 按一下 `validateConfigs()`. 在&#x200B;**[!UICONTROL 驗證配置]**&#x200B;對話框中，按一下&#x200B;**[!UICONTROL 調用]**。

驗證結果會顯示在相同的對話方塊中。

### 在[!UICONTROL DAM更新資產]工作流程中啟用智慧標籤（選用）{#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在[!DNL Experience Manager]中，轉至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。

1. 在「 **[!UICONTROL 工作流模型]** 」頁面上，選擇「**[!UICONTROL DAM 更新資產]** 」工作流模型。

1. 按一下工具列中的&#x200B;**[!UICONTROL 「編輯」]**。

1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於&#x200B;**[!UICONTROL 「處理縮 圖」]**&#x200B;步驟之後 。

   ![在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟](assets/smart-tag-in-dam-update-asset-workflow.png)

   *圖：在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟。*

1. 在編輯模式中開啟步驟。在「 **[!UICONTROL 進階設定]**」下，確定已選取 **[!UICONTROL 「處理常式進階]** 」選項。

   ![設定DAM更新資產工作流程並新增智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)


   *圖：設定DAM更新資產工作流程並新增智慧標籤步驟*

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流完成，即使自動標籤步驟失敗，請選擇「忽略錯誤 **** 」。

   ![設定DAM更新資產工作流程，以新增智慧型標籤步驟並預先選取處理常式](assets/smart-tag-step-properties-workflow2.png)


   *圖：設定DAM更新資產工作流程，以新增智慧型標籤步驟並預先選取處理常式*

   若無論是否對資料夾啟用智慧標記，都要在資產上傳時標記資產，請選取&#x200B;**[!UICONTROL 「忽略智慧標記旗標」]**。

   ![設定DAM更新資產工作流程以新增智慧型標籤步驟，並選取忽略智慧型標籤標幟](assets/smart-tag-step-properties-workflow3.png)


   *圖：設定DAM更新資產工作流程以新增智慧型標籤步驟，並選取忽略智慧型標籤標幟。*

1. 按一下&#x200B;**[!UICONTROL 「確定」]**&#x200B;關閉程序步驟，然後儲存工作流程。

## 培訓智慧型內容服務{#training-the-smart-content-service}

要讓Smart Content Service識別您的業務分類，請在已包含與您的業務相關的標籤的資產集上運行該分類。 為有效地標籤您的品牌影像，智慧型內容服務要求培訓影像符合特定准則。 培訓後，服務可以對類似的資產集應用相同的分類法。

您可以多次培訓服務，以提升其套用相關標籤的能力。 在每個訓練週期後，執行標籤工作流程並檢查您的資產是否已適當標籤。

您可以定期或視需要培訓智慧型內容服務。

>[!NOTE]
>
>培訓工作流程僅在資料夾上執行。

### 訓練准則{#guidelines-for-training}

為獲得最佳效果，您訓練集中的影像符合下列准則：

**** 數量和大小：每個標籤至少30個影像。長邊至少500像素。

**一致性**:用於特定標籤的影像在視覺上類似。

例如，將所有這些影像標籤為`my-party`（用於訓練）並不好，因為它們在視覺上並不相似。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/coherence.png)

**涵蓋範圍**:在訓練中使用足夠多的影像變化。我們的想法是提供一些比較多樣的例子，讓Experience Manager學會專注於正確的事情。 如果您要在視覺上不相同的影像上套用相同的標籤，請至少包含5種不同類型的範例。

例如，對於標籤&#x200B;*model-down-pose*，為服務加入更多類似下方反白顯示影像的訓練影像，以便在標籤期間更精確地識別類似影像。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/coverage_1.png)

**干擾／妨礙**:該服務更能訓練那些分散注意力的影像（突出的背景、不相關的伴奏，如主題的物體／人）。

例如，對於標籤&#x200B;*休閒鞋*，第二個影像不是好的訓練候選影像。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於`raincoat`和`model-side-view`等標籤，請在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智慧型內容服務是否能夠訓練您的標籤並將它們套用至其他影像，取決於您用於訓練的影像品質。 為獲得最佳效果，Adobe建議您使用視覺上類似的影像來訓練每個標籤的服務。

### 定期培訓{#periodic-training}

您可以讓智慧型內容服務定期培訓資料夾中的資產和相關標籤。 開啟資產資料夾的[!UICONTROL 屬性]頁，在&#x200B;**[!UICONTROL 詳細資訊]**&#x200B;頁籤下選擇&#x200B;**[!UICONTROL 啟用智慧標籤]**，並保存更改。

![enable_smart_tags](assets/enable_smart_tags.png)

為資料夾選擇此選項後， [!DNL Experience Manager]將自動運行培訓工作流，以便對資料夾資產及其標籤進行智慧內容服務培訓。 依預設，培訓工作流程每週在星期六的凌晨12:30執行。

### 隨選培訓{#on-demand-training}

您可以在工作流程主控台(Workflow console)中，視需要訓練智慧型內容服務。

1. 在[!DNL Experience Manager]介面中，轉至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從&#x200B;**[!UICONTROL 工作流模型]**&#x200B;頁面中，選擇&#x200B;**[!UICONTROL 智慧標籤培訓]**&#x200B;工作流，然後從工具欄中按一下&#x200B;**[!UICONTROL 啟動工作流]**。
1. 在&#x200B;**[!UICONTROL 執行工作流程]**&#x200B;對話方塊中，瀏覽至包含標籤資產的裝載資料夾以訓練服務。
1. 指定工作流程的標題並新增註解。 然後，按一下&#x200B;**[!UICONTROL 運行]**。 資產和標籤會提交以供培訓。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>資料夾中的資產一旦處理好以進行培訓後，後續培訓週期中只會處理修改過的資產。

### 檢視訓練報告{#viewing-training-reports}

若要檢查智慧型內容服務是否在訓練資產集中的標籤上接受訓練，請從「報告」主控台檢閱訓練工作流程報告。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**。
1. 在&#x200B;**[!UICONTROL 資產報表]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 建立]**。
1. 選擇&#x200B;**[!UICONTROL 智慧型標籤訓練]**&#x200B;報表，然後從工具列按一下&#x200B;**[!UICONTROL Next]**。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，從工具列按一下「建立」。****
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。若要檢視報表，請按一下工具列上的&#x200B;**[!UICONTROL 檢視]**。
1. 檢閱報表的詳細資訊。

   報表會顯示您所訓練之標籤的訓練狀態。「培訓狀態」欄 **[!UICONTROL 中的綠色]** ，表示智慧型內容服務已接受標籤的培訓。黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。

   如果您在此報表中未看到標籤，請針對這些標籤重新執行培訓工作流程。

1. 若要下載報表，請從清單中選取報表，然後從工具列按一下「下載&#x200B;**[!UICONTROL 」。]**&#x200B;報表會以Microsoft Excel試算表的形式下載。

## 限制 {#limitations}

* 增強的智慧型標籤是以學習影像模型及其標籤為基礎。 這些模型在識別標籤時並不總是十分完美。 智慧型內容服務的目前版本有下列限制：

   * 無法辨識影像的細微差異。 例如，修身與普通襯衫。
   * 無法根據影像的微小圖樣／部分來識別標籤。 例如，T恤上的標誌。
   * 在[!DNL Experience Manager]支援的地區設定中支援標籤。 如需語言清單，請參閱[智慧型內容服務發行說明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

* 若要使用智慧型標籤（一般或增強功能）搜尋資產，請使用[!DNL Assets] Omnisearch（全文搜尋）。 智慧型標籤沒有個別的搜尋述詞。

>[!MORELIKETHIS]
>
>* [智慧型標籤的概觀與訓練方法](enhanced-smart-tags.md)
>* [智慧型標籤的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

