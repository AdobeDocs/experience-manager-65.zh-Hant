---
title: 使用智慧型內容服務設定資產標籤。
description: 瞭解如何使用智慧型內容服務，在Adobe Experience Manager中設定智慧型標籤和增強的智慧型標籤。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f3d699f35c7b1ef832a0857fa2fa41aed1fe5a4e
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 15%

---


# 使用智慧型內容服務設定資產標籤 {#configure-asset-tagging-using-the-smart-content-service}

您可以使 [!DNL Adobe Experience Manager] 用Adobe Developer Console與智慧型內容服務整合。 使用此配置可從中訪問Smart Content Service [!DNL Experience Manager]。

文章詳細說明了配置Smart Content Service所需的下列主要工作。 在後端，伺服器會先 [!DNL Experience Manager] 使用Adobe Developer Console閘道驗證您的服務認證，然後再將您的要求轉送至智慧型內容服務。

* 在中建立Smart Content Service配置 [!DNL Experience Manager] 以生成公開密鑰。 取得OAuth整合的公用憑證。
* 在Adobe Developer Console中建立整合，並上傳產生的公開金鑰。
* 使用Adobe [!DNL Experience Manager] Developer Console的API金鑰和其他認證來設定您的例項。
* （可選）在資產上傳時啟用自動標籤。

## 必備條件 {#prerequisites}

在使用智慧型內容服務之前，請確定下列項目以建立Adobe Developer Console的整合：

* 具有組織管理員權限的Adobe ID帳戶。
* 您的組織已啟用智慧型內容服務。

## 取得公開憑證 {#obtain-public-certificate}

公開憑證可讓您在Adobe Developer Console上驗證您的個人檔案。

1. 在使用 [!DNL Experience Manager] 者介面中，存 **[!UICONTROL 取「工具>雲端服務]**>舊 **[!UICONTROL 版雲端服務」]**。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. 在「建 **[!UICONTROL 立設定]** 」對話方塊中，指定「智慧標籤」設定的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。
1. 在「 **[!UICONTROL AEM智慧型內容服務]** 」對話方塊中，使用下列值：

   **[!UICONTROL 服務 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**: `https://ims-na1.adobelogin.com`

   現在將其他欄位留空（稍後將提供）。 按一下 **[!UICONTROL 確定]**。

   ![Experience Manager Smart Content Service對話框，用於提供內容服務URL](assets/aem_scs.png)

1. 按一 **[!UICONTROL 下「下載OAuth整合的公用憑證]**」，然後下載公用憑證檔案 `AEM-SmartTags.crt`。

   ![為智慧標籤服務建立的設定的表示](assets/smart-tags-download-public-cert.png)

### 證書過期時重新配置 {#certrenew}

證書過期後，將不再受信任。 您無法為過期的憑證續約。 若要新增憑證，請依照下列步驟進行。

1. Log in your [!DNL Experience Manager] deployment as an administrator. 按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到並按 **[!UICONTROL 一下dam-update-service使用者]** 。 按一下「密鑰 **[!UICONTROL 庫]** 」頁籤。
1. 刪除具有過 **[!UICONTROL 期證書的]** 現有相似性search密鑰庫。 Click **[!UICONTROL Save &amp; Close]**.

   ![刪除Keystore中現有的相似性搜尋項目，以新增安全憑證](assets/smarttags_delete_similaritysearch_keystore.png)

   *圖： 刪除Keystore中`similaritysearch`的現有條目，以添加新的安全證書。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. 若要下載公用憑證，請按一下「 **[!UICONTROL 下載OAuth整合的公用憑證」]**。
1. 存取 [https://console.adobe.io](https://console.adobe.io) ，並導覽至「整合」頁面上現有的智慧 **[!UICONTROL 內容服務]** 。 上傳新憑證。 如需詳細資訊，請參閱「建立Adobe開發人 [員主控台」整合中的指示](#create-adobe-i-o-integration)。

## 建立Adobe Developer Console整合 {#create-adobe-i-o-integration}

若要使用Smart Content Service API，請在Adobe Developer Console中建立整合，以產生API金鑰、技術帳戶ID、組織ID和用戶端密碼。

1. 在瀏 [覽器中](https://console.adobe.io/) ，存取https://console.adobe.io。 選擇適當的帳戶並驗證關聯的組織角色是系統管理員。
1. 建立任何所需名稱的專案。 按一 **[!UICONTROL 下新增API]**。
1. 在「新 **[!UICONTROL 增API]** 」頁面上，選 **[!UICONTROL 取「Experience Cloud]** 」並選 **[!UICONTROL 取「智慧內容]**」。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 選擇 **[!UICONTROL 上傳公開金鑰]**。 提供從下載的憑證檔案 [!DNL Experience Manager]。 會顯 [!UICONTROL 示成功上傳的公開金鑰] 。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. [!UICONTROL 建立新的服務帳戶(JWT)憑據頁] ，顯示剛配置的服務帳戶的公鑰。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 在「選擇 **[!UICONTROL 產品配置檔案]** 」頁上，選擇 **[!UICONTROL Smart Content Services]**。 按一 **[!UICONTROL 下「儲存已設定的API]**」。 一個頁面會顯示更多有關設定的資訊。 在中進一步設定智慧標籤時，請保持此頁面的開啟狀態，以複製並新增這些值至Experience Manager [!DNL Experience Manager]。

   ![在「概述」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)

## 設定智慧型內容服務 {#configure-smart-content-service}

若要設定整合，請使用Adobe Developer Console整合中的「技術帳戶ID」、「組織ID」、「用戶端密碼」、「授權伺服器」和API金鑰欄位的值。 建立智慧型標籤雲端設定可讓您驗證來自例項的API [!DNL Experience Manager] 請求。

1. 在中 [!DNL Experience Manager]，導覽至「 **[!UICONTROL 工具>雲端服務>舊版雲端服務」以開啟]** Cloud Services  Console。
1. 在「資 **[!UICONTROL 產智慧標籤]**」下，開啟上述建立的設定。 在服務設定頁面上，按一下「 **[!UICONTROL 編輯]**」。
1. 在「 **[!UICONTROL AEM Smart Content Service]** 」對話方塊中 **[!UICONTROL ，使用「服務URL」和「授權伺服器」欄位的預先填入值]****** 。
1. 對於「 **[!UICONTROL API金鑰]**」、「 **[!UICONTROL Technical Account Id]**」、「 **[!UICONTROL Organization Id]**」和「Client Secret **[!UICONTROL 」欄位，請使]**&#x200B;用上述產生的值。

## 驗證配置 {#validate-the-configuration}

完成配置後，可使用JMX MBean來驗證配置。 若要驗證，請遵循下列步驟。

1. 訪問您 [!DNL Experience Manager] 的伺服器 `https://[aem_server]:[port]`。

1. 前往「 **[!UICONTROL 工具>作業> Web Console]** 」以開啟OSGi主控台。 按一 **[!UICONTROL 下「主要> JMX]**」。
1. 按一 **[!UICONTROL 下com.day.cq.dam.similaritysearch.internal.impl]**。 它會開啟「相 **[!UICONTROL 似性搜尋雜項任務」]**。
1. 按一 **[!UICONTROL 下validateConfigs()]**。 在「驗證 **[!UICONTROL 配置」對話]** ，按一下 **[!UICONTROL 調用]**。

   驗證結果會顯示在相同的對話方塊中。

## 在DAM更新資產工作流程中啟用智慧標籤（可選） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在中， [!DNL Experience Manager]請轉至「工 **[!UICONTROL 具」>「工作流」>「模型」]**。
1. 在「工 **[!UICONTROL 作流模型]** 」頁面上，選擇 **** 「DAM更新資產」工作流模型。
1. 從工具 **[!UICONTROL 列按一下]** 「編輯」。
1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於「處理縮 **[!UICONTROL 圖」步驟之後]** 。

   ![在 [!UICONTROL DAM更新資產工作流程中，在流程縮圖步驟之後新增智慧型標籤資產步驟] 。](assets/smart-tag-in-dam-update-asset-workflow.png)

   *圖： 在[!UICONTROL DAM Update Asset工作流程中，在流程縮圖步驟之後新增智慧型標籤資產步驟]。*

1. 在編輯模式中開啟步驟。在「 **[!UICONTROL 進階設定]**」下，確定已選 **[!UICONTROL 取「處理常式進階]** 」選項。

   ![設定DAM更新資產工作流程並新增智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流完成，即使自動標籤步驟失敗，請選擇「忽略錯誤 **** 」。

   ![設定DAM更新資產工作流程，以新增智慧型標籤步驟並預先選取處理常式](assets/smart-tag-step-properties-workflow2.png)

   若要在資產上傳時標籤資產，而不論資料夾上是否啟用智慧型標籤，請選取「忽略智慧 **[!UICONTROL 型標籤標籤」]**。

   ![設定DAM更新資產工作流程以新增智慧型標籤步驟，並選取忽略智慧型標籤標幟](assets/smart-tag-step-properties-workflow3.png)

1. 按一下 **[!UICONTROL 確定]** ，關閉流程步驟，然後保存工作流。

>[!MORELIKETHIS]
>
>* [管理智慧標籤](managing-smart-tags.md)
>* [智慧型標籤的概觀與訓練方法](enhanced-smart-tags.md)
>* [培訓智慧型內容服務的准則和規則](smart-tags-training-guidelines.md)
>* [有關如何設定智慧標籤的教學課程影片](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

