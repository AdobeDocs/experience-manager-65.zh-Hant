---
title: 使用Smart Content Service配置資產標籤
description: 瞭解如何在中配置智慧標籤和增強的智慧標籤 [!DNL Adobe Experience Manager]，使用Smart Content Service。
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 24%

---

# 準備 [!DNL Assets] 用於智慧標籤 {#configure-asset-tagging-using-the-smart-content-service}

在開始使用Smart Content Services標籤資產之前，請整合 [!DNL Experience Manager Assets] 與Adobe Developer控制台一起利用 [!DNL Adobe Sensei]。 配置後，使用幾個影像和標籤來培訓服務。

>[!NOTE]
>
>* Smart Content Services不再可用於新 [!DNL Experience Manager Assets] 內部客戶。 已啟用此功能的現有本地客戶可以繼續使用Smart Content Services。
>* Smart Content Services可用於現有 [!DNL Experience Manager Assets] Managed Services客戶，他們已啟用此功能。
>* 新建 [!DNL Experience Manager Assets] Managed Services客戶可以按照本文中所述的說明來設定Smart Content Services。


在使用Smart Content Service之前，請確保：

* [使用 Adobe 開發人員控制台進行整合](#integrate-adobe-io).
* [培訓智慧內容服務](#training-the-smart-content-service)。

* 安裝最新 [[!DNL Experience Manager] 服務包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)。

## 使用 Adobe 開發人員控制台進行整合 {#integrate-adobe-io}

當您與Adobe Developer控制台整合時， [!DNL Experience Manager] 伺服器在將請求轉發到Smart Content Service之前，使用Adobe Developer控制台網關驗證您的服務憑據。 要整合，您需要一個對組織具有管理員權限的Adobe ID帳戶，以及為您的組織購買並啟用的智慧內容服務許可證。

要配置Smart Content Service，請執行以下頂級步驟：

1. 要生成公鑰， [建立智慧內容服務](#obtain-public-certificate) 配置 [!DNL Experience Manager]。 [取得公開憑證](#obtain-public-certificate)以進行 OAuth 整合。

1. [在 Adobe 開發人員控制台中建立整合](#create-adobe-i-o-integration)，並上傳產生的公開金鑰。

1. [配置部署](#configure-smart-content-service) 使用API密鑰和來自Adobe Developer控制台的其他憑據。

1. [測試設定](#validate-the-configuration)。

1. （可選） [啟用資產上載時的自動標籤](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

### 通過建立Smart Content Service配置獲取公共證書 {#obtain-public-certificate}

公開憑證可讓您在 Adobe 開發人員控制台上驗證設定檔。

1. 在 [!DNL Experience Manager] 用戶介面，訪問 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 舊Cloud Services]**。

1. 在Cloud Services頁中，按一下 **[!UICONTROL 立即配置]** 在 **[!UICONTROL 資產智慧標籤]**。

1. 在 **[!UICONTROL 建立配置]** 對話框，指定智慧標籤配置的標題和名稱。 按一下&#x200B;**[!UICONTROL 建立]**。

1. 在 **[!UICONTROL 智AEM能內容服務]** 對話框，使用以下值：

   **[!UICONTROL 服務 URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   比如說， `https://smartcontent.adobe.io/apac`。 可以指定 `na`。 `emea`，或 `apac` 作為Experience Manager作者實例的托管區域。

   >[!NOTE]
   >
   >如果在2022年9月1日之前設定了Experience Manager托管服務，請使用以下服務URL:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授權伺服器]**: `https://ims-na1.adobelogin.com`

   將其他欄位留空（稍後提供）。 按一下&#x200B;**[!UICONTROL 「確定」]**。

   ![Experience Manager智慧內容服務對話框以提供內容服務URL](assets/aem_scs.png)


   *圖：提供內容服務URL的智慧內容服務對話框*

   >[!NOTE]
   >
   >提供的URL [!UICONTROL 服務URL] 無法通過瀏覽器訪問，並生成404錯誤。 配置工作正常，其值與 [!UICONTROL 服務URL] 的下界。 有關總體服務狀態和維護計畫，請參見 [https://status.adobe.com](https://status.adobe.com)。

1. 按一下 **[!UICONTROL 下載用於OAuth整合的公共證書]**，並下載公共證書檔案 `AEM-SmartTags.crt`。

   ![為智慧標籤服務建立的設定的表示](assets/smart-tags-download-public-cert.png)


   *圖：智慧標籤服務的設定。*

#### 證書過期時重新配置 {#certrenew}

證書過期後，它不再受信任。 您無法更新已過期的憑證。要添加證書，請執行以下步驟。

1. 以管理員身分登入您的 [!DNL Experience Manager] 部署。按一 **[!UICONTROL 下「工具]** >安 **[!UICONTROL 全性]** >使 **[!UICONTROL 用者]**」。

1. 找到 **[!UICONTROL dam-update-service]** 使用者後按一下該使用者。按一下 **[!UICONTROL 密鑰庫]** 頁籤。

1. 刪除憑證已過期的現有 **[!UICONTROL similaritysearch]** 金鑰存放區。按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![刪除密鑰庫中的現有相似性搜索條目以添加安全證書](assets/smarttags_delete_similaritysearch_keystore.png)


   *圖：刪除現有 `similaritysearch` 的子目錄。*

1. 導覽至「 **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** >舊 **[!UICONTROL 版雲端服務」]**。按一 **[!UICONTROL 下「資產智慧標籤]** >顯 **[!UICONTROL 示設定]** >可 **[!UICONTROL 用設定」]**。按一下所需的設定。

1. 要下載公共證書，請按一下 **[!UICONTROL 下載用於OAuth整合的公共證書]**。

1. 訪問 [https://console.adobe.io](https://console.adobe.io) 並導航至 **[!UICONTROL 整合]** 的子菜單。 上載新證書。 有關詳細資訊，請參閱中的說明 [建立Adobe Developer控制台整合](#create-adobe-i-o-integration)。

### 建立Adobe Developer控制台整合 {#create-adobe-i-o-integration}

要使用Smart Content Service API，請在Adobe Developer控制台中建立整合以獲取 [!UICONTROL API密鑰] (生成於 [!UICONTROL 客戶端ID] 欄位), [!UICONTROL 技術帳戶ID]。 [!UICONTROL 組織ID], [!UICONTROL 客戶端密碼] 為 [!UICONTROL 資產智慧標籤服務設定] 雲配置 [!DNL Experience Manager]。

1. 在瀏覽器中存取 [https://console.adobe.io](https://console.adobe.io/)。選取適當的帳戶，並確認相關聯的組織角色是系統管理員。

1. 以任何所需的名稱建立專案。按一下&#x200B;**[!UICONTROL 「新增 API」]**。

1. 在&#x200B;**[!UICONTROL 新增 API]** 頁面上選取&#x200B;**[!UICONTROL 「Experience Cloud」]**，然後選取&#x200B;**[!UICONTROL 「智慧內容」]**。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**[!UICONTROL 「上傳您的公開金鑰」]**。提供從 [!DNL Experience Manager] 下載的憑證檔案。畫面上會顯示[!UICONTROL 已成功上傳公開金鑰]訊息。按一下&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 建立新服務帳戶(JWT)憑據] 頁顯示服務帳戶的公鑰。

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 選取產品設定檔]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 「智慧內容服務」]**。按一下&#x200B;**[!UICONTROL 「儲存已設定的 API」]**。

   此時會出現一個頁面，顯示更多關於設定的資訊。保持此頁面的開啟狀態，以複製和在 [!UICONTROL 資產智慧標籤服務設定] 雲配置 [!DNL Experience Manager] 配置智慧標籤。

   ![在「概覽」索引標籤中，您可以檢閱為整合提供的資訊。](assets/integration_details.png)


   *圖：Adobe Developer控制台整合詳細資訊*

### 配置智慧內容服務 {#configure-smart-content-service}

要配置整合，請使用 [!UICONTROL 技術帳戶ID]。 [!UICONTROL 組織ID]。 [!UICONTROL 客戶端密碼], [!UICONTROL 客戶端ID] 的子菜單。 建立智慧標籤雲配置允許驗證來自 [!DNL Experience Manager] 部署。

1. 在 [!DNL Experience Manager]，導航 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 舊Cloud Services]** 開啟 [!UICONTROL Cloud Services] 控制台。

1. 在 **[!UICONTROL 資產智慧標籤]**，開啟上面建立的配置。 在「服務設定」頁上，按一下 **[!UICONTROL 編輯]**。

1. 在「 **[!UICONTROL AEM Smart Content Service]** 」對話方塊中 **[!UICONTROL ，使用「服務URL」和「授權伺服器」欄位的預先填入值]****** 。

1. 對於欄位 [!UICONTROL API密鑰]。 [!UICONTROL 技術帳戶ID]。 [!UICONTROL 組織ID], [!UICONTROL 客戶端密碼]，複製並使用中生成的以下值 [Adobe Developer控制台整合](#create-adobe-i-o-integration)。

   | [!UICONTROL 資產智慧標記服務設定] | [!DNL Adobe Developer Console] 整合域 |
   |--- |--- |
   | [!UICONTROL API 金鑰] | [!UICONTROL 客戶端ID] |
   | [!UICONTROL 技術帳戶 ID] | [!UICONTROL 技術帳戶ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL 用戶端密碼] | [!UICONTROL 客戶端密碼] |

### 驗證設定 {#validate-the-configuration}

完成配置後，可以使用JMX MBean驗證配置。 要驗證，請執行以下步驟。

1. 訪問 [!DNL Experience Manager] 伺服器 `https://[aem_server]:[port]`。

1. 轉到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** 開啟OSGi控制台。 按一下 **[!UICONTROL 主] > [!UICONTROL JMX]**。

1. 按一下 `com.day.cq.dam.similaritysearch.internal.impl`. 開啟 **[!UICONTROL 相似性搜索雜項任務]**。

1. 按一下 `validateConfigs()`. 在 **[!UICONTROL 驗證配置]** 對話框，按一下 **[!UICONTROL 調用]**。

驗證結果顯示在同一對話框中。

### 在 [!UICONTROL DAM更新資產] 工作流（可選） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在 [!DNL Experience Manager]，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。

1. 在「 **[!UICONTROL 工作流模型]** 」頁面上，選擇「**[!UICONTROL DAM 更新資產]** 」工作流模型。

1. 按一下工具列中的&#x200B;**[!UICONTROL 「編輯」]**。

1. 展開「側面板」以顯示步驟。拖 **[!UICONTROL 曳DAM Workflow]**  (DAM工作流程) 區段中可用的智慧型標籤資產步驟，並將其置於&#x200B;**[!UICONTROL 「處理縮 圖」]**&#x200B;步驟之後 。

   ![在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟](assets/smart-tag-in-dam-update-asset-workflow.png)

   *圖：在「DAM 更新資產」工作流程中，在處理縮圖步驟之後新增智慧標記資產步驟。*

1. 在編輯模式中開啟步驟。在「 **[!UICONTROL 進階設定]**」下，確定已選取 **[!UICONTROL 「處理常式進階]** 」選項。

   ![配置DAM更新資產工作流和添加智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)


   *圖：配置DAM更新資產工作流和添加智慧標籤步驟*

1. 在「參 **[!UICONTROL 數]** 」頁籤中，如果希望工作流完成，即使自動標籤步驟失敗，請選擇「忽略錯誤 **** 」。

   ![配置DAM更新資產工作流以添加智慧標籤步驟並選擇處理程式高級](assets/smart-tag-step-properties-workflow2.png)


   *圖：配置DAM更新資產工作流以添加智慧標籤步驟並選擇處理程式高級*

   若無論是否對資料夾啟用智慧標記，都要在資產上傳時標記資產，請選取&#x200B;**[!UICONTROL 「忽略智慧標記旗標」]**。

   ![配置DAM更新資產工作流以添加智慧標籤步驟並選擇忽略智慧標籤標誌](assets/smart-tag-step-properties-workflow3.png)


   *圖：配置DAM更新資產工作流以添加智慧標籤步驟並選擇忽略智慧標籤標誌。*

1. 按一下&#x200B;**[!UICONTROL 「確定」]**&#x200B;關閉程序步驟，然後儲存工作流程。

## 培訓智慧內容服務 {#training-the-smart-content-service}

要使智慧內容服務識別您的業務分類，請在已包含與您的業務相關標籤的一組資產上運行它。 為了有效標籤您的品牌影像，Smart Content Service要求培訓影像符合某些准則。 培訓後，該服務可以對類似的資產集應用相同的分類。

您可以對服務進行多次培訓，以提高其應用相關標籤的能力。 在每個培訓週期後，運行標籤工作流並檢查是否對您的資產進行了適當標籤。

您可以定期或按要求培訓智慧內容服務。

>[!NOTE]
>
>培訓工作流僅在資料夾上運行。

### 培訓指南 {#guidelines-for-training}

為獲得最佳效果，培訓集中的影像符合以下准則：

**** 數量和大小：每個標籤至少30個影像。長邊至少500像素。

**一致性**:用於特定標籤的影像在視覺上相似。

例如，將所有這些影像標籤為 `my-party` （用於培訓），因為它們在視覺上不相似。

![說明性影像為培訓指南的範例](/help/assets/assets/do-not-localize/coherence.png)

**覆蓋範圍**:在培訓中使用足夠多的影像。 其理念是提供一些比較多樣的例子讓Experience Manager學會專注於正確的事情 如果在視覺上不相同的影像上應用相同的標籤，請至少包括五種不同類型的示例。

例如，對於標籤 *模型下姿態*，包括與下面突出顯示的影像類似的更多培訓影像，以便服務在標籤期間更準確地識別類似影像。

![說明性影像為培訓指南的範例](/help/assets/assets/do-not-localize/coverage_1.png)

**分心/妨礙**:該服務對分散度較小的影像（突出背景、不相關的伴奏，如主題對象/人）進行更好的訓練。

例如，對於標籤 *休閒鞋*&#x200B;第二幅不是很好的訓練對象。

![說明性影像為培訓指南的範例](/help/assets/assets/do-not-localize/distraction.png)

**** 完整性：如果影像符合多個標籤的資格，請先新增所有適用的標籤，再加入影像以進行訓練。例如，對於標籤，例如 `raincoat` 和 `model-side-view`，在包括合格資產以進行培訓之前，先將這兩個標籤添加到合格資產。

![說明性影像為培訓指南的範例](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智慧內容服務在您的標籤上進行培訓並將其應用於其他影像的能力取決於您用於培訓的影像質量。 為獲得最佳效果，Adobe建議您使用視覺上相似的影像來為每個標籤培訓服務。

### 定期培訓 {#periodic-training}

您可以啟用Smart Content Service定期培訓資料夾中的資產和關聯標籤。 開啟 [!UICONTROL 屬性] 頁面，選擇 **[!UICONTROL 啟用智慧標籤]** 下 **[!UICONTROL 詳細資訊]** 的子菜單。

![enable_smart_tags](assets/enable_smart_tags.png)

為資料夾選擇此選項後， [!DNL Experience Manager] 自動運行培訓工作流，對資料夾資產及其標籤進行培訓。 預設情況下，培訓工作流每週在星期六上午12:30運行。

### 按需培訓 {#on-demand-training}

只要需要，可從工作流控制台培訓智慧內容服務。

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從 **[!UICONTROL 工作流模型]** ，選擇 **[!UICONTROL 智慧標籤培訓]** 工作流，然後按一下 **[!UICONTROL 啟動工作流]** 的子菜單。
1. 在 **[!UICONTROL 運行工作流]** 對話框，瀏覽到包含標籤資產的負載資料夾以培訓服務。
1. 指定工作流的標題並添加註釋。 然後，按一下 **[!UICONTROL 運行]**。 資產和標籤將提交以供培訓。

   ![工作流_對話框](assets/workflow_dialog.png)

>[!NOTE]
>
>一旦對資料夾中的資產進行處理以進行培訓，則在後續培訓週期中僅處理修改的資產。

### 查看培訓報告 {#viewing-training-reports}

要檢查Smart Content Service是否在資產培訓集中的標籤上接受培訓，請從「報告」控制台查看培訓工作流報告。

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報告]**。
1. 在 **[!UICONTROL 資產報表]** 的 **[!UICONTROL 建立]**。
1. 選擇 **[!UICONTROL 智慧標籤培訓]** 報告，然後按一下 **[!UICONTROL 下一個]** 的子菜單。
1. 指定報表的標題和說明。在「 **[!UICONTROL 排程報表]**」下，保 **[!UICONTROL 留「現在]** 」選項。如果您想要排程報表以供稍後使用，請選 **[!UICONTROL 取]** 「稍後」並指定日期和時間。然後，按一下 **[!UICONTROL 建立]** 的子菜單。
1. 在「資 **[!UICONTROL 產報表]** 」頁面中，選取您產生的報表。要查看報告，請按一下 **[!UICONTROL 視圖]** 的子菜單。
1. 查看報告的詳細資訊。

   報表會顯示您所訓練之標籤的訓練狀態。「培訓狀態」欄 **[!UICONTROL 中的綠色]** ，表示智慧型內容服務已接受標籤的培訓。黃色表示服務未針對特定標籤進行完整訓練。在這種情況下，請使用特定標籤新增更多影像，並執行培訓工作流程，以完全在標籤上訓練服務。

   如果在此報告中未看到標籤，請再次運行這些標籤的培訓工作流。

1. 要下載報告，請從清單中選擇它，然後按一下 **[!UICONTROL 下載]** 的子菜單。 報告以MicrosoftExcel電子錶格的形式下載。

## 限制 {#limitations}

* 增強的智慧標籤基於影像及其標籤的學習模型。 這些模型在識別標籤方面並不總是十分完美。 Smart Content Service的當前版本具有以下限制：

   * 無法識別影像中的細微差異。 例如，修身襯衫和普通襯衫。
   * 無法根據影像的微小圖案/部分來識別標籤。 例如，T恤上的徽標。
   * 在以下區域中支援標籤： [!DNL Experience Manager] 中支援。

* 要搜索具有智慧標籤（常規或增強）的資產，請使用 [!DNL Assets] Omnisearch（全文搜索）。 智慧標籤沒有單獨的搜索謂詞。

>[!MORELIKETHIS]
>
>* [智慧標籤概述及如何培訓](enhanced-smart-tags.md)
>* [關於智慧標籤的視頻教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

