---
title: 使用智慧內容服務設定資產標籤
description: 瞭解如何在中設定智慧標籤和增強智慧標籤 [!DNL Adobe Experience Manager]，使用智慧內容服務。
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 19%

---

# 準備 [!DNL Assets] 用於智慧標籤 {#configure-asset-tagging-using-the-smart-content-service}

開始使用Smart Content Services標籤資產之前，請先整合 [!DNL Experience Manager Assets] 透過Adobe Developer Console，使用智慧服務 [!DNL Adobe Sensei]. 設定好後，請使用一些影像和標籤來訓練服務。

>[!NOTE]
>
>* 新使用者無法再使用智慧內容服務 [!DNL Experience Manager Assets] 內部部署客戶。 已啟用此功能的現有內部部署客戶可以繼續使用智慧內容服務。
>* 智慧內容服務適用於現有 [!DNL Experience Manager Assets] 已啟用此功能的Managed Services客戶。
>* 新增 [!DNL Experience Manager Assets] Managed Services客戶可以依照本文所述的指示，設定智慧內容服務。

在使用智慧內容服務之前，請先確定下列事項：

* [整合Adobe Developer主控台](#integrate-adobe-io).
* [訓練智慧內容服務](#training-the-smart-content-service).

* 安裝最新版本 [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## 整合Adobe Developer主控台 {#integrate-adobe-io}

當您整合Adobe Developer Console時， [!DNL Experience Manager] 伺服器會先透過Adobe Developer主控台閘道驗證您的服務認證，再將您的要求轉送至智慧內容服務。 若要整合，您需要具有組織管理員許可權的Adobe ID帳戶，以及為貴組織購買並啟用的Smart Content Service授權。

若要設定智慧內容服務，請遵循下列最上層步驟：

1. 若要產生公開金鑰， [建立智慧內容服務](#obtain-public-certificate) 中的設定 [!DNL Experience Manager]. [取得公開憑證](#obtain-public-certificate)以進行 OAuth 整合。

1. [在 Adobe 開發人員控制台中建立整合](#create-adobe-i-o-integration)，並上傳產生的公開金鑰。

1. [設定您的部署](#configure-smart-content-service) 從Adobe Developer主控台使用API金鑰和其他認證。

1. [測試設定](#validate-the-configuration)。

1. 或者 [在資產上傳時啟用自動標籤](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### 透過建立智慧內容服務設定來取得公開憑證 {#obtain-public-certificate}

公開憑證可讓您在Adobe Developer主控台驗證設定檔。

1. 在 [!DNL Experience Manager] 使用者介面，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 舊版Cloud Service]**.

1. 在Cloud Service頁面中，按一下 **[!UICONTROL 立即設定]** 在 **[!UICONTROL 資產智慧標籤]**.

1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定智慧標籤設定的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。

1. 在 **[!UICONTROL AEM智慧內容服務]** 對話方塊，請使用下列值：

   **[!UICONTROL 服務URL]**： `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   例如 `https://smartcontent.adobe.io/apac`。您可以指定 `na`， `emea`，或， `apac` 作為託管Experience Manager作者例項的地區。

   >[!NOTE]
   >
   >如果Experience Manager託管服務在2022年9月1日之前布建，請使用以下服務URL：
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**： `https://ims-na1.adobelogin.com`

   其他欄位暫時保留空白（稍後提供）。 按一下&#x200B;**[!UICONTROL 「確定」]**。

   ![Experience Manager智慧內容服務對話方塊以提供內容服務URL](assets/aem_scs.png)


   *圖：提供內容服務URL的智慧內容服務對話方塊*

   >[!NOTE]
   >
   >提供的URL為 [!UICONTROL 服務URL] 無法透過瀏覽器存取，並產生404錯誤。 若的值相同，則組態運作正常。 [!UICONTROL 服務URL] 引數。 如需整體服務狀態和維護排程，請參閱 [https://status.adobe.com](https://status.adobe.com).

1. 按一下 **[!UICONTROL 下載公開憑證以進行OAuth整合]**，並下載公開憑證檔案 `AEM-SmartTags.crt`.

   ![為智慧標籤服務建立的設定表示法](assets/smart-tags-download-public-cert.png)


   *圖：智慧標籤服務的設定。*

#### 憑證過期時重新設定 {#certrenew}

憑證過期後，即不再受信任。 您無法更新過期的憑證。 若要新增憑證，請按照以下步驟操作。

1. 以管理員身分登入您的 [!DNL Experience Manager] 部署。按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到 **[!UICONTROL dam-update-service]** 使用者後按一下該使用者。按一下 **[!UICONTROL 金鑰存放區]** 標籤。

1. 刪除憑證已過期的現有 **[!UICONTROL similaritysearch]** 金鑰存放區。按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![刪除Keystore中現有的相似性搜尋專案，以新增安全性憑證](assets/smarttags_delete_similaritysearch_keystore.png)


   *圖：刪除現有的 `similaritysearch` 金鑰存放區中的專案以新增安全性憑證。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. 若要下載公開憑證，請按一下 **[!UICONTROL 下載公開憑證以進行OAuth整合]**.

1. 存取 [https://console.adobe.io](https://console.adobe.io) 並導覽至 **[!UICONTROL 整合]** 頁面。 上傳新憑證。 如需詳細資訊，請參閱 [建立Adobe Developer主控台整合](#create-adobe-i-o-integration).

### 建立Adobe Developer主控台整合 {#create-adobe-i-o-integration}

若要使用Smart Content Service API，請在Adobe Developer主控台中建立整合，以取得 [!UICONTROL API金鑰] (產生於 [!UICONTROL 使用者端ID] Adobe Developer欄位)， [!UICONTROL 技術帳戶ID]， [!UICONTROL 組織ID]、和 [!UICONTROL 使用者端密碼] 的 [!UICONTROL 資產智慧標籤服務設定] 中的雲端設定 [!DNL Experience Manager].

1. 在瀏覽器中存取 [https://console.adobe.io](https://console.adobe.io/)。選取適當的帳戶，並確認相關聯的組織角色是系統管理員。

1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。

1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**[!UICONTROL 「上傳您的公開金鑰」]**。提供從 [!DNL Experience Manager] 下載的憑證檔案。畫面上會顯示[!UICONTROL 已成功上傳公開金鑰]訊息。按一下&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 建立新的服務帳戶(JWT)認證] 頁面會顯示服務帳戶的公開金鑰。

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 「智慧內容服務」]**。按一下 **[!UICONTROL 儲存已設定的API]**.

   此時會出現一個頁面，顯示更多關於設定的資訊。請保持此頁面開啟，以複製這些值，並將其新增至 [!UICONTROL 資產智慧標籤服務設定] 中的雲端設定 [!DNL Experience Manager] 以設定智慧標籤。

   ![在「概覽」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)


   *圖：Adobe Developer主控台整合的詳細資料*

### 設定智慧內容服務 {#configure-smart-content-service}

>[!CAUTION]
>
>之前，使用JWT憑證進行的設定現在會在Adobe Developer Console中遭到淘汰。 2024年6月3日之後，您無法建立新的JWT憑證。 此類設定無法再建立或更新，但可以移轉至 OAuth 設定。
> 另請參閱 [為AEM設定IMS整合](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>另請參閱 [為內部部署使用者設定OAuth的步驟](#config-oauth-onprem)
> 另請參閱 [針對OAuth憑證的智慧標籤進行疑難排解](#config-smart-tagging.md)

若要設定整合，請使用 [!UICONTROL 技術帳戶ID]， [!UICONTROL 組織ID]， [!UICONTROL 使用者端密碼]、和 [!UICONTROL 使用者端ID] Adobe Developer主控台整合中的欄位。 建立智慧標籤雲端設定，可驗證來自的API請求 [!DNL Experience Manager] 部署。

1. 在 [!DNL Experience Manager]，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 舊版Cloud Service]** 以開啟 [!UICONTROL Cloud Service] 主控台。

1. 在 **[!UICONTROL 資產智慧標籤]**，開啟上面建立的設定。 在服務設定頁面上，按一下 **[!UICONTROL 編輯]**.

1. 在「 **[!UICONTROL AEM Smart Content Service]** 」對話方塊中 **[!UICONTROL ，使用「服務URL」和「授權伺服器」欄位的預先填入值]****** 。

1. 針對欄位 [!UICONTROL Api金鑰]， [!UICONTROL 技術帳戶ID]， [!UICONTROL 組織ID]、和 [!UICONTROL 使用者端密碼]，複製並使用中產生的下列值 [Adobe Developer主控台整合](#create-adobe-i-o-integration).

   | [!UICONTROL 資產智慧標籤服務設定] | [!DNL Adobe Developer Console] 整合欄位 |
   |--- |--- |
   | [!UICONTROL Api金鑰] | [!UICONTROL 使用者端ID] |
   | [!UICONTROL 技術帳戶ID] | [!UICONTROL 技術帳戶ID] |
   | [!UICONTROL 組織ID] | [!UICONTROL 組織ID] |
   | [!UICONTROL 使用者端密碼] | [!UICONTROL 使用者端密碼] |

### 為內部部署使用者設定OAuth {#config-oauth-onprem}

#### 先決條件 {#prereqs-config-oauth-onprem}

授權範圍是包含以下先決條件的OAuth字串：

* 在中建立新的OAuth整合 [開發人員主控台](https://developer.adobe.com/console/user/servicesandapis) 使用 `ClientID`， `ClientSecretID`、和 `OrgID`.
* 在此路徑新增下列檔案 `/apps/system/config in crx/de`：
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### 為內部部署使用者設定OAuth {#steps-config-oauth-onprem}

1. 在中新增或更新以下屬性 `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`：

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * 更新 `auth.token.provider.client.id` 搭配新OAuth設定的使用者端ID。
   * 更新 `auth.access.token.request` 至 `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. 將檔案重新命名為 `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. 請在中執行以下步驟 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`：
   * 透過新的OAuth整合，使用使用者端密碼更新auth.ims.client.secret屬性。
   * 將檔案重新命名為 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. 儲存內容存放庫開發主控台中的所有變更，例如CRXDE。
5. 瀏覽至 `/system/console/configMgr` 並從取代OSGi設定 `.<randomnumber>` 至 `-<randomnumber>`.
6. 刪除的舊設定 `"Access Token provider name: adobe-ims-similaritysearch"` 在 `/system/console/configMgr`.
7. 重新啟動主控台。

### 驗證設定 {#validate-the-configuration}

完成設定後，您可以使用JMX MBean來驗證設定。 若要進行驗證，請按照以下步驟操作。

1. 存取您的 [!DNL Experience Manager] 伺服器位置 `https://[aem_server]:[port]`.

1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]** 以開啟OSGi主控台。 按一下 **[!UICONTROL 主要] > [!UICONTROL JMX]**.

1. 按一下 `com.day.cq.dam.similaritysearch.internal.impl`。隨即開啟 **[!UICONTROL 相似性搜尋其他任務]**.

1. 按一下 `validateConfigs()`。在 **[!UICONTROL 驗證設定]** 對話方塊，按一下 **[!UICONTROL 叫用]**.

驗證結果會顯示在相同的對話方塊中。

### 在中啟用智慧標籤 [!UICONTROL DAM更新資產] 工作流程（選擇性） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在 [!DNL Experience Manager]，前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 在「 **[!UICONTROL 工作流模型]** 」頁面上，選擇「**[!UICONTROL DAM 更新資產]** 」工作流模型。

1. 按一下工具列中的&#x200B;**[!UICONTROL 「編輯」]**。

1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於&#x200B;**[!UICONTROL 「處理縮 圖」]**&#x200B;步驟之後 。

   ![在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟](assets/smart-tag-in-dam-update-asset-workflow.png)

   *圖：在的程式縮圖步驟之後新增智慧標籤資產步驟 [!UICONTROL DAM更新資產] 工作流程。*

1. 在編輯模式中開啟步驟。在「 **[!UICONTROL 進階設定]**」下，確定已選取 **[!UICONTROL 「處理常式進階]** 」選項。

   ![設定DAM更新資產工作流程並新增智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)


   *圖：設定DAM更新資產工作流程並新增智慧標籤步驟*

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流完成，即使自動標籤步驟失敗，請選擇「忽略錯誤 **** 」。

   ![設定DAM更新資產工作流程以新增智慧標籤步驟並選取處理常式前進](assets/smart-tag-step-properties-workflow2.png)


   *圖：設定DAM更新資產工作流程以新增智慧標籤步驟並選取處理常式前進*

   若無論是否對資料夾啟用智慧標記，都要在資產上傳時標記資產，請選取&#x200B;**[!UICONTROL 「忽略智慧標記旗標」]**。

   ![設定DAM更新資產工作流程以新增智慧標籤步驟，並選取忽略智慧標籤標幟](assets/smart-tag-step-properties-workflow3.png)


   *圖：設定DAM更新資產工作流程以新增智慧標籤步驟並選取忽略智慧標籤標幟。*

1. 按一下 **[!UICONTROL 確定]** 以關閉程式步驟，然後儲存工作流程。

## 訓練智慧內容服務 {#training-the-smart-content-service}

若要讓智慧內容服務辨識您的企業分類，請在已包含與企業相關標籤的一組資產上執行它。 為了有效標籤您的品牌影像，智慧內容服務要求培訓影像符合特定准則。 訓練之後，此服務可以將相同的分類法套用至類似的資產集。

您可以訓練服務多次，以提高其套用相關標籤的能力。 在每個訓練週期後，執行標籤工作流程並檢查您的資產是否已正確標籤。

您可以定期或依需求訓練智慧內容服務。

>[!NOTE]
>
>訓練工作流程僅在資料夾中執行。

### 訓練准則 {#guidelines-for-training}

為達到最佳效果，訓練集中的影像需符合下列准則：

**** 數量和大小：每個標籤至少30個影像。長邊至少500像素。

**一致性**：用於特定標籤的影像在視覺上類似。

例如，將所有影像標示為 `my-party` （適用於訓練），因為視覺效果不同。

![插圖影像，以示範訓練准則](/help/assets/assets/do-not-localize/coherence.png)

**涵蓋範圍**：在訓練的影像中使用足夠的變化。 我們的想法是提供一些合理多樣化的範例，讓Experience Manager學習如何聚焦於正確的事。 如果您要在視覺上相異的影像上套用相同的標籤，請至少包含每種型別的五個範例。

例如，對於標籤 *模型向下姿態*，請加入更多與下方醒目提示影像類似的培訓影像，以便服務在標籤期間更準確地識別類似影像。

![插圖影像，以示範訓練准則](/help/assets/assets/do-not-localize/coverage_1.png)

**干擾/阻礙**：此服務可針對干擾較少的影像（突出的背景、不相關的隨附，例如具有主要主題的物件/人員）提供更好的訓練。

例如，對於標籤 *休閒鞋*，第二個影像不是良好的訓練候選項。

![插圖影像，以示範訓練准則](/help/assets/assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤，例如 `raincoat` 和 `model-side-view`，請在符合資格的資產上新增兩個標籤，然後再加入以進行訓練。

![插圖影像，以示範訓練准則](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智慧型內容服務針對您的標籤進行培訓並將這些內容套用至其他影像的能力，取決於您用於培訓的影像品質。 為達到最佳效果，Adobe建議您使用視覺上相似的影像，針對每個標籤來訓練服務。

### 定期訓練 {#periodic-training}

您可以啟用智慧內容服務，定期訓練資料夾中的資產和關聯標籤。 開啟 [!UICONTROL 屬性] 第頁，請選取 **[!UICONTROL 啟用智慧標籤]** 在 **[!UICONTROL 詳細資料]** 標籤，並儲存變更。

![enable_smart_tags](assets/enable_smart_tags.png)

為資料夾選取此選項後， [!DNL Experience Manager] 自動執行培訓工作流程，以針對資料夾資產及其標籤培訓智慧內容服務。 根據預設，培訓工作流程每週於星期六凌晨12:30執行。

### 隨選培訓 {#on-demand-training}

您可以視需要從工作流程主控台訓練「智慧內容服務」。

1. 在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 從 **[!UICONTROL 工作流程模型]** 頁面，選取 **[!UICONTROL 智慧標籤培訓]** 工作流程，然後按一下 **[!UICONTROL 開始工作流程]** 工具列中的。
1. 在 **[!UICONTROL 執行工作流程]** 對話方塊，瀏覽至包含標籤資產的裝載資料夾，以培訓服務。
1. 指定工作流程的標題並新增註解。 然後，按一下 **[!UICONTROL 執行]**. 資產和標籤會提交以進行訓練。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>一旦資料夾中的資產處理完畢，用於訓練後，後續訓練週期內將僅處理修改後的資產。

### 檢視訓練報告 {#viewing-training-reports}

若要檢查智慧型內容服務是否已針對您的資產培訓集中的標籤進行培訓，請從「報表」控制檯檢閱培訓工作流程報表。

1. 在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.
1. 在 **[!UICONTROL 資產報表]** 頁面，按一下 **[!UICONTROL 建立]**.
1. 選取 **[!UICONTROL 智慧標籤培訓]** 報表，然後按一下 **[!UICONTROL 下一個]** 工具列中的。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，按一下 **[!UICONTROL 建立]** 工具列中的。
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。若要檢視報表，請按一下 **[!UICONTROL 檢視]** 工具列中的。
1. 檢閱報告的詳細資訊。

   報表會顯示您所訓練之標籤的訓練狀態。「培訓狀態」欄 **[!UICONTROL 中的綠色]** ，表示智慧型內容服務已接受標籤的培訓。黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。

   如果您在此報告中未看到您的標籤，請再次執行這些標籤的培訓工作流程。

1. 若要下載報表，請從清單中選取報表，然後按一下 **[!UICONTROL 下載]** 工具列中的。 報表會下載為Microsoft Excel試算表。

## 限制 {#limitations}

* 增強型智慧標籤是以影像及其標籤的學習模型為基礎。 這些模型並非總能完美地識別標籤。 目前版本的智慧內容服務有下列限制：

   * 無法辨認影像中的細微差異。 例如，超薄襯衫和一般適合的襯衫。
   * 無法根據影像的微小模式/部分識別標籤。 例如，T恤上的標誌。
   * 在下列語言環境中支援標籤 [!DNL Experience Manager] 支援。

* 若要搜尋具有智慧標籤（一般或增強功能）的資產，請使用 [!DNL Assets] Omnisearch （全文檢索搜尋）。 智慧標籤沒有單獨的搜尋述詞。

>[!MORELIKETHIS]
>
>* [概述及如何訓練智慧標籤](enhanced-smart-tags.md)
>* [針對OAuth憑證的智慧標籤進行疑難排解](config-oauth.md)
>* [有關智慧標籤的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
