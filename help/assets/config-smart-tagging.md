---
title: 使用智慧型內容服務設定資產標籤
description: 瞭解如何使用智慧型內容服務來設定智慧型標籤 [!DNL Adobe Experience Manager]，以及增強智慧型標籤。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5599e0d4a3e52a4ad98b776b9178722c7ac47cbc
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 26%

---


# 準備 [!DNL Assets] 智慧標籤 {#configure-asset-tagging-using-the-smart-content-service}

在您開始使用智慧型內容服務標籤資產之前，請先與 [!DNL Experience ManageR Assets] Adobe Developer Console整合，以運用其智慧型服務 [!DNL Adobe Sensei]。 一旦設定好後，請使用幾張影像和標籤來訓練服務。

在您使用智慧型內容服務之前，請確定下列事項：

* [使用 Adobe 開發人員控制台進行整合](#integrate-adobe-io).
* [培訓智慧型內容服務](#training-the-smart-content-service)。

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* 安裝最新 [的Experience Manager Service Pack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。

## 使用 Adobe 開發人員控制台進行整合 {#integrate-adobe-io}

當您與Adobe Developer Console整合時，伺服器會先使用Adobe Developer Console閘道驗證您的服務認證，再將您的要求轉送至智慧型內容服務。 [!DNL Experience Manager] 若要整合，您需要擁有組織管理員權限的Adobe ID帳戶，以及為組織購買並啟用的智慧型內容服務授權。

若要設定智慧型內容服務，請依照下列頂層步驟：

1. [在中建立Smart Content Service](#obtain-public-certificate) 配置以 [!DNL Experience Manager] 生成公共密鑰。 [取得公開憑證](#obtain-public-certificate)以進行 OAuth 整合。

1. [在 Adobe 開發人員控制台中建立整合](#create-adobe-i-o-integration)，並上傳產生的公開金鑰。

1. [使用Adobe Developer Console的](#configure-smart-content-service) API金鑰和其他認證來設定您的部署。

1. [測試設定](#validate-the-configuration)。

1. （可選） [在資產上傳時啟用自動標籤](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

### 建立智慧型內容服務組態以取得公用憑證 {#obtain-public-certificate}

公開憑證可讓您在 Adobe 開發人員控制台上驗證設定檔。

1. 在使用 [!DNL Experience Manager] 者介面中，存 **[!UICONTROL 取「工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務]**」。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. 在「建 **[!UICONTROL 立設定]** 」對話方塊中，指定「智慧標籤」設定的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。

1. 在「 **[!UICONTROL AEM智慧型內容服務]** 」對話方塊中，使用下列值：

   **[!UICONTROL 服務 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**: `https://ims-na1.adobelogin.com`

   現在將其他欄位留空（稍後將提供）。 按一下&#x200B;**[!UICONTROL 「確定」]**。

   ![Experience Manager Smart Content Service對話框，用於提供內容服務URL](assets/aem_scs.png)


   *圖：「智慧型內容服務」對話方塊，提供內容服務URL*

   >[!NOTE]
   >
   >以服務URL提供 [!UICONTROL 的URL] 無法透過瀏覽器存取，並產生404錯誤。 設定可正常運作，且與「服務URL」參 [!UICONTROL 數值相同] 。 有關整體服務狀態和維護計畫，請參 [閱https://status.adobe.com](https://status.adobe.com)。

1. 按一 **[!UICONTROL 下「下載OAuth整合的公用憑證]**」，然後下載公用憑證檔案 `AEM-SmartTags.crt`。

   ![為智慧標籤服務建立的設定的表示](assets/smart-tags-download-public-cert.png)


   *圖：智慧型標籤服務的設定*

#### Reconfigure when a certificate expires {#certrenew}

證書過期後，將不再受信任。 您無法更新已過期的憑證。若要新增憑證，請依照下列步驟操作。

1. 以管理員身分登入您的 [!DNL Experience Manager] 部署。按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到 **[!UICONTROL dam-update-service]** 使用者後按一下該使用者。Click **[!UICONTROL Keystore]** tab.

1. 刪除憑證已過期的現有 **[!UICONTROL similaritysearch]** 金鑰存放區。按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![刪除Keystore中現有的相似性搜尋項目，以新增安全憑證](assets/smarttags_delete_similaritysearch_keystore.png)


   *圖：刪除金鑰存放區中現有的 `similaritysearch` 項目，以新增安全性憑證。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. 存取 [https://console.adobe.io](https://console.adobe.io) ，並導覽至「整合」頁面上現有的智慧 **[!UICONTROL 內容服務]** 。 上傳新憑證。 For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

### 建立Adobe Developer Console整合 {#create-adobe-i-o-integration}

若要使用智慧型內容服務API，請在Adobe Developer Console中建立整合以取得 [!UICONTROL API金鑰] (產生於Adobe Developer Developer Integration的 [!UICONTROL CLIENT ID] 欄位)、 [!UICONTROL TECHNICAL ACCOUNT ID]、 [!DNL Experience Manager]ORGANIZATION ID、SecretClientConsole資產智慧服務設定中雲配置中標籤雲配置的智慧服務設定。

1. 在瀏覽器中存取 [https://console.adobe.io](https://console.adobe.io/)。選取適當的帳戶，並確認相關聯的組織角色是系統管理員。

1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。

1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**[!UICONTROL 「上傳您的公開金鑰」]**。提供從 [!DNL Experience Manager] 下載的憑證檔案。畫面上會顯示[!UICONTROL 已成功上傳公開金鑰]訊息。按一下&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 建立新的服務帳戶(JWT) 憑證]頁面會顯示剛設定的服務帳戶的公開金鑰。

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 「智慧內容服務」]**。按一下&#x200B;**[!UICONTROL 「儲存已設定的 API」]**。

   此時會出現一個頁面，顯示更多關於設定的資訊。請保持此頁面的開啟狀態，以複製並新增這些值至中的 [!UICONTROL Assets智慧標籤服務設定(Smart Tagging Service Settings] of cloud configuration), [!DNL Experience Manager] 以設定智慧標籤。

   ![在「概覽」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)


   *圖：Adobe Developer Console中的整合詳細資訊*

### 設定智慧型內容服務 {#configure-smart-content-service}

若要設定整合，請使用Adobe Developer Console整合的 [!UICONTROL TECHNICAL ACCOUNT ID]、 [!UICONTROL ORGANIZATION ID]、 [!UICONTROL CLIENT SECRET和] CLIENT ID欄位的值。 建立智慧型標籤雲端設定可讓您驗證部署中的API [!DNL Experience Manager] 要求。

1. 在中， [!DNL Experience Manager]導航至「 **[!UICONTROL 工具]** > **[!UICONTROL Cloud服務]** >舊版Cloud服務 **** >開放Cloud Services主控台。

1. 在「資 **[!UICONTROL 產智慧標籤]**」下，開啟上述建立的設定。 在服務設定頁面上，按一下「 **[!UICONTROL 編輯]**」。

1. 在「 **[!UICONTROL AEM Smart Content Service]** 」對話方塊中 **[!UICONTROL ，使用「服務URL」和「授權伺服器」欄位的預先填入值]****** 。

1. 對於「Api金鑰 [!UICONTROL 」、「]Technical Account ID [!UICONTROL 」、「組織ID」和「]Client Secret [](#create-adobe-i-o-integration)」欄位，複製並使用下列在Adobe Console Developer Console整合中產生的值：

   | [!UICONTROL 資產智慧標記服務設定] | [!DNL Adobe Developer Console] 整合欄位 |
   |--- |--- |
   | [!UICONTROL API 金鑰] | [!UICONTROL 用戶端ID] |
   | [!UICONTROL 技術帳戶 ID] | [!UICONTROL 技術帳戶ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL 用戶端密碼] | [!UICONTROL 用戶端密碼] |

### 驗證設定 {#validate-the-configuration}

完成配置後，可使用JMX MBean來驗證配置。 若要驗證，請遵循下列步驟。

1. 訪問您 [!DNL Experience Manager] 的伺服器 `https://[aem_server]:[port]`。

1. 前往「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]** 」以開啟OSGi主控台。 按一 **[!UICONTROL 下「主] > [!UICONTROL JMX]**」。

1. 按一下 `com.day.cq.dam.similaritysearch.internal.impl`. 它會開啟「相 **[!UICONTROL 似性搜尋雜項任務」]**。

1. 按一下 `validateConfigs()`. 在「驗證 **[!UICONTROL 配置」對話]** ，按一下 **[!UICONTROL 調用]**。

驗證結果會顯示在相同的對話方塊中。

### 在 [!UICONTROL DAM更新資產工作流程中啟用智慧標籤] （選用） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

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


   *圖：設定DAM更新資產工作流程以新增智慧型標籤步驟，並選取忽略智慧型標籤標幟*

1. 按一下&#x200B;**[!UICONTROL 「確定」]**&#x200B;關閉程序步驟，然後儲存工作流程。

## 培訓智慧型內容服務 {#training-the-smart-content-service}

要讓Smart Content Service識別您的業務分類，請在已包含與您的業務相關的標籤的資產集上運行該分類。 為有效地標籤您的品牌影像，智慧型內容服務要求培訓影像符合特定准則。 培訓後，服務可以對類似的資產集應用相同的分類法。

您可以多次培訓服務，以提升其套用相關標籤的能力。 在每個訓練週期後，執行標籤工作流程並檢查您的資產是否已適當標籤。

您可以定期或視需要培訓智慧型內容服務。

>[!NOTE]
>
>培訓工作流程僅在資料夾上執行。

### 培訓方針 {#guidelines-for-training}

為獲得最佳效果，您的訓練集中的影像應符合下列准則：

**** 數量和大小：每個標籤至少30個影像。長邊至少500像素。

**一致性**:標籤的影像應類似視覺效果。

例如，將所有這些影像標籤為（用於訓練）並不 `my-party` 好，因為它們的視覺上不類似。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/coherence.png)

**涵蓋範圍**:培訓中的影像應該有足夠的多樣性。 其理念是提供幾個相當多樣化的範例，讓Experience Manager學會專注在正確的事物上。 如果您要在視覺上不相同的影像上套用相同的標籤，請至少包含5種不同類型的範例。

例如，對於標籤下模 *式姿勢*，請加入更多類似下方反白顯示影像的訓練影像，讓服務在標籤時更精確地識別類似影像。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/coverage_1.png)

**干擾／妨礙**:該服務更能訓練那些分散注意力的影像（突出的背景、不相關的伴奏，如主題的物體／人）。

例如，對於標籤休閒 *鞋*，第二張影像不是好的訓練候選影像。

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![示例性影像，以示訓練指南](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智慧型內容服務是否能夠訓練您的標籤並將它們套用至其他影像，取決於您用於訓練的影像品質。 為獲得最佳效果，Adobe建議您使用視覺上類似的影像來訓練每個標籤的服務。

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

## 限制 {#limitations}

* 增強的智慧型標籤是以學習影像模型及其標籤為基礎。 這些模型在識別標籤時並不總是十分完美。 智慧型內容服務的目前版本有下列限制：

   * 無法辨識影像的細微差異。 例如，修身與普通襯衫。
   * 無法根據影像的微小圖樣／部分來識別標籤。 例如，T恤上的標誌。
   * 在中支援的地區設定中 [!DNL Experience Manager] 支援標籤。 如需語言清單，請參閱智 [慧型內容服務版本注意事項](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

* 若要使用智慧型標籤（一般或增強功能）來搜尋資產，請使用 [!DNL Assets] Omnisearch（全文搜尋）。 智慧型標籤沒有個別的搜尋述詞。

>[!MORELIKETHIS]
>
>* [智慧型標籤的概觀與訓練方法](enhanced-smart-tags.md)
>* [有關如何設定智慧標籤的教學課程影片](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

