---
title: 使用智慧型內容服務設定資產標籤。
description: 瞭解如何使用智慧型內容服務來設定智慧型標籤 [!DNL Adobe Experience Manager]，以及增強智慧型標籤。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 506b965e4f1c18230357f25532d3fdd10f526ef0
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 35%

---


# 使用智慧型內容服務設定資產標籤 {#configure-asset-tagging-using-the-smart-content-service}

您可以使 [!DNL Adobe Experience Manager] 用Adobe Developer Console與智慧型內容服務整合。 使用此配置可從中訪問Smart Content Service [!DNL Experience Manager]。

文章詳細說明了配置Smart Content Service所需的下列主要工作。 At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. [在中建立Smart Content Service](#obtain-public-certificate) 配置以 [!DNL Experience Manager] 生成公共密鑰。 [取得公開憑證](#obtain-public-certificate)以進行 OAuth 整合。

1. [在 Adobe 開發人員控制台中建立整合](#create-adobe-i-o-integration)，並上傳產生的公開金鑰。

1. [使用Adobe Developer Console的](#configure-smart-content-service) API金鑰和其他認證來設定您的部署。

1. [測試設定](#validate-the-configuration)。

1. （可選） [在資產上傳時啟用自動標籤](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

## 必備條件 {#prerequisites}

在您使用智慧型內容服務之前，請確定下列項目以在Adobe Developer Console上建立整合：

* Adobe ID 帳戶具有組織的管理員權限。

* 智慧型內容服務已為您的組織啟用。

<!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
-->

除了上述功能外，若要啟用「增強的智慧型標籤」，請另外安裝最新的 [Experience Manager Service Pack](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。

## 建立智慧型內容服務設定以取得 {#obtain-public-certificate}

公開憑證可讓您在 Adobe 開發人員控制台上驗證設定檔。

1. 在使用 [!DNL Experience Manager] 者介面中，存 **[!UICONTROL 取「工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務]**」。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. 在「建 **[!UICONTROL 立設定]** 」對話方塊中，指定「智慧標籤」設定的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。

1. 在「 **[!UICONTROL AEM智慧型內容服務]** 」對話方塊中，使用下列值：

   **[!UICONTROL 服務 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**: `https://ims-na1.adobelogin.com`

   現在將其他欄位留空（稍後將提供）。 按一下&#x200B;**[!UICONTROL 「確定」]**。

   ![Experience Manager Smart Content Service對話框，用於提供內容服務URL](assets/aem_scs.png)


   *圖： 「智慧型內容服務」對話方塊，提供內容服務URL*

   >[!NOTE]
   >
   >以服務URL提供 [!UICONTROL 的URL] 無法透過瀏覽器存取，並產生404錯誤。 設定可正常運作，且與「服務URL」參 [!UICONTROL 數值相同] 。 有關整體服務狀態和維護計畫，請參 [閱https://status.adobe.com](https://status.adobe.com)。

1. 按一 **[!UICONTROL 下「下載OAuth整合的公用憑證]**」，然後下載公用憑證檔案 `AEM-SmartTags.crt`。

   ![為智慧標籤服務建立的設定的表示](assets/smart-tags-download-public-cert.png)


   *圖： 智慧型標籤服務的設定*

### Reconfigure when a certificate expires {#certrenew}

證書過期後，將不再受信任。 您無法更新已過期的憑證。若要新增憑證，請依照下列步驟操作。

1. 以管理員身分登入您的 [!DNL Experience Manager] 部署。按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到 **[!UICONTROL dam-update-service]** 使用者後按一下該使用者。Click **[!UICONTROL Keystore]** tab.

1. 刪除憑證已過期的現有 **[!UICONTROL similaritysearch]** 金鑰存放區。按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![刪除Keystore中現有的相似性搜尋項目，以新增安全憑證](assets/smarttags_delete_similaritysearch_keystore.png)


   *圖：刪除金鑰存放區中現有的`similaritysearch`項目，以新增安全性憑證。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. 存取 [https://console.adobe.io](https://console.adobe.io) ，並導覽至「整合」頁面上現有的智慧 **[!UICONTROL 內容服務]** 。 上傳新憑證。 For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## 建立Adobe Developer Console整合 {#create-adobe-i-o-integration}

若要使用智慧型內容服務API，請在Adobe Developer Console中建立整合以取得 [!UICONTROL API金鑰] (產生於Adobe Developer Developer Integration的 [!UICONTROL CLIENT ID] 欄位)、 [!UICONTROL TECHNICAL ACCOUNT ID]、 [!DNL Experience Manager]ORGANIZATION ID、SecretClientConsole資產智慧服務設定中雲配置中標籤雲配置的智慧服務設定。

1. 在瀏覽器中存取 [https://console.adobe.io](https://console.adobe.io/)。選取適當的帳戶，並確認相關聯的組織角色是系統管理員。

1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。

1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**[!UICONTROL 「上傳您的公開金鑰」]**。提供從 [!DNL Experience Manager] 下載的憑證檔案。畫面上會顯示[!UICONTROL 已成功上傳公開金鑰]訊息。按一下&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 建立新的服務帳戶(JWT) 憑證]頁面會顯示剛設定的服務帳戶的公開金鑰。

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 「智慧內容服務」]**。按一下&#x200B;**[!UICONTROL 「儲存已設定的 API」]**。

   此時會出現一個頁面，顯示更多關於設定的資訊。請保持此頁面的開啟，以複製並新增這些值至中的 [!UICONTROL Assets Smart Tagging Service Settings] （雲端設定的資產智慧標籤服務設定）, [!DNL Experience Manager] 以設定智慧標籤。

   ![在「概覽」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)


   *圖： Adobe Developer Console中的整合詳細資訊*

## 設定智慧型內容服務 {#configure-smart-content-service}

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

## 驗證設定 {#validate-the-configuration}

完成配置後，可使用JMX MBean來驗證配置。 若要驗證，請遵循下列步驟。

1. 訪問您 [!DNL Experience Manager] 的伺服器 `https://[aem_server]:[port]`。

1. 前往「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]** 」以開啟OSGi主控台。 按一 **[!UICONTROL 下「主]>[!UICONTROL JMX]**」。

1. 按一下 `com.day.cq.dam.similaritysearch.internal.impl`. 它會開啟「相 **[!UICONTROL 似性搜尋雜項任務」]**。

1. 按一下 `validateConfigs()`. 在「驗證 **[!UICONTROL 配置」對話]** ，按一下 **[!UICONTROL 調用]**。

驗證結果會顯示在相同的對話方塊中。

## 在 [!UICONTROL DAM更新資產工作流程中啟用智慧標籤] （選用） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. 在「 **[!UICONTROL 工作流模型]** 」頁面上，選擇「**[!UICONTROL DAM 更新資產]** 」工作流模型。

1. 按一下工具列中的&#x200B;**[!UICONTROL 「編輯」]**。

1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於&#x200B;**[!UICONTROL 「處理縮 圖」]**&#x200B;步驟之後 。

   ![在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟](assets/smart-tag-in-dam-update-asset-workflow.png)

   *圖：在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟。*

1. 在編輯模式中開啟步驟。在「 **[!UICONTROL 進階設定]**」下，確定已選取 **[!UICONTROL 「處理常式進階]** 」選項。

   ![設定DAM更新資產工作流程並新增智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)


   *圖： 設定DAM更新資產工作流程並新增智慧標籤步驟*

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流完成，即使自動標籤步驟失敗，請選擇「忽略錯誤 **** 」。

   ![設定DAM更新資產工作流程，以新增智慧型標籤步驟並預先選取處理常式](assets/smart-tag-step-properties-workflow2.png)


   *圖： 設定DAM更新資產工作流程，以新增智慧型標籤步驟並預先選取處理常式*

   若無論是否對資料夾啟用智慧標記，都要在資產上傳時標記資產，請選取&#x200B;**[!UICONTROL 「忽略智慧標記旗標」]**。

   ![設定DAM更新資產工作流程以新增智慧型標籤步驟，並選取忽略智慧型標籤標幟](assets/smart-tag-step-properties-workflow3.png)


   *圖： 設定DAM更新資產工作流程以新增智慧型標籤步驟，並選取忽略智慧型標籤標幟*

1. 按一下&#x200B;**[!UICONTROL 「確定」]**&#x200B;關閉程序步驟，然後儲存工作流程。

>[!MORELIKETHIS]
>
>* [管理智慧標籤](managing-smart-tags.md)
>* [智慧型標籤的概觀與訓練方法](enhanced-smart-tags.md)
>* [培訓智慧型內容服務的准則和規則](smart-tags-training-guidelines.md)
>* [有關如何設定智慧標籤的教學課程影片](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

