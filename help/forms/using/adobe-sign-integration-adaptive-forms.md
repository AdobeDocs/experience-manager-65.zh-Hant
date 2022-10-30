---
title: 整合Adobe Sign與AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: 了解如何設定Adobe Sign for AEM Forms
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 25%

---

# 整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 啟用最適化表單的電子簽名工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在 [!DNL Adobe Sign] 和最適化表單案例，使用者會填入最適化表單 **申請服務**. 例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者便會審查申請並使用 [!DNL Adobe Sign] 標記已核准申請。若要啟用類似的電子簽名工作流程，您可以整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms].

使用 [!DNL Adobe Sign] 使用AEM [!DNL Forms]，設定 [!DNL Adobe Sign] 在AEM雲端服務中：

## 必備條件 {#prerequisites}

您需要下列項目才能整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]:

* 主要 [Adobe Sign 開發人員帳戶.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 安 [啟用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 伺服器。
* [Adobe Sign API 應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 應用程式的認證 (用戶端 ID 和用戶端密碼)。
* 重新設定時，移除現有 [!DNL Adobe Sign] 從製作執行個體和發佈執行個體進行設定。
* 使用製作和發佈執行個體的[同一密碼編譯金鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 設定 [!DNL Adobe Sign] 使用AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

準備就緒後，請執行下列步驟以設定 [!DNL Adobe Sign] 使用AEM [!DNL Forms] 在Author例項上：

1. 在AEM [!DNL Forms] 製作例項，導覽至 **工具** ![錘](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**.
1. 在 **[!UICONTROL 配置瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
   * 請參閱 [配置瀏覽器](/help/sites-administering/configurations.md) 檔案以取得詳細資訊。
1. 在 **[!UICONTROL 建立配置]** 對話框，指定 **[!UICONTROL 標題]** 若為設定，請啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 它會為雲端服務建立設定容器。
1. 導覽至 **工具** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** ，然後選取您在上述步驟中建立的設定容器。

   >[!NOTE]
   >
   >您可以執行步驟1至4來建立新的設定容器並建立 [!DNL Adobe Sign] 設定，或使用現有 `global` 資料夾 **工具** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 如果您在新設定容器中建立設定，請務必在 **[!UICONTROL 組態容器]** 欄位。

   >[!NOTE]
   確認雲端服務設定頁面的URL開頭為 **HTTPS**. 如果沒有， [啟用SSL](/help/sites-administering/ssl-by-default.md) 適用於AEM [!DNL Forms] 伺服器。

1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] AEM中的設定 [!DNL Forms].
1. 在 **[!UICONTROL 一般]** 的 **[!UICONTROL 建立Adobe Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** 針對設定並點選 **[!UICONTROL 下一個]**. 您可以選擇指定標題並瀏覽以選取設定的縮圖。

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。必須進行設定 [!DNL Adobe Sign] AEM應用程式[!DNL Forms].

1. 在 **[!UICONTROL 設定]** 標籤 **[!UICONTROL OAuth URL]** 欄位包含預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL  Adobe Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果您建立 Adobe Experience Manager 功能或元件的另一個 [!DNL Adobe Sign] 設定請確保所有 [!DNL Adobe Sign] Cloud Configurations 都指向相同分片。

   >[!NOTE]
   保留 **建立Adobe Sign設定** 頁面開啟。 不要關閉它。 您可以擷取 **用戶端ID** 和 **用戶端密碼** 配置OAuth設定後， [!DNL Adobe Sign] 應用程式，如後續步驟所述。


1. 設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入 [!DNL Adobe Sign] 開發人員帳戶。
   1. 選取為AEM設定的應用程式 [!DNL Forms]，然後點選 **[!UICONTROL 為應用程式配置OAuth]**.
   1. 複製 **[!UICONTROL 用戶端ID]** 和 **[!UICONTROL 用戶端密碼]** 記事本。
   1. 在 **[!UICONTROL 重新導向URL]** 框中，添加上一步中複製的HTTPS URL。
   1. 為啟用下列OAuth設定 [!DNL Adobe Sign] 應用程式和按一下 **[!UICONTROL 儲存]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   如需設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」開發人員文件。

   ![OAuth Config](assets/oauthconfig_new.png)

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 標籤 **[!UICONTROL OAuth URL]** 欄位提及預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。

   您可以修改資料庫分片的值。重新啟動伺服器，以便能夠將新值用於資料庫共用。

   >[!NOTE]
   請確定您的製作和發佈執行個體設定指向相同的分區。 如果您為組織建立多個Adobe Sign設定，請確定所有設定都使用相同的分區。

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 頁簽，指定 **用戶端ID** （亦稱為應用程式ID）和 **用戶端密碼**. 使用 [Adobe Sign應用程式的用戶端ID和用戶端密碼](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 為AEM Forms建立。

1. 選取 **[!UICONTROL 也啟用Adobe Sign以取得附件]** 將附加至適用性表單的檔案附加至對應 [!DNL Adobe Sign] 要簽名的文檔。

1. 點選 **[!UICONTROL 連線至Adobe Sign]**. 出現認證提示時，請提供在建立 [!DNL Adobe Sign] 應用程式時使用的帳戶使用者名稱和密碼。

1. 點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 設定。

1. 開啟AEM Web Console。 URL為 `https://'[server]:[port]'/system/console/configMgr`
1. 開啟 **[!UICONTROL Forms Common Configuration Service].**
1. 在 **[!UICONTROL 允許]** 欄位， **選取** 所有用戶 — 所有用戶（匿名或已登錄）都可以預覽附件、驗證和簽名表單，然後按一下 **[!UICONTROL 儲存].** 製作例項已設定為使用 [!DNL Adobe Sign].
1. 發佈設定。
1. 使用 [複製](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) 在對應的發佈執行個體上建立相同設定。

現在， [!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 並可在最適化表單中使用。 結束日期 [在最適化表單中使用Adobe Sign服務](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，請在適用性表單屬性中指定上述建立的設定容器。



## 設定 [!DNL Adobe Sign] 同步簽名狀態的調度程式 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

安 [!DNL Adobe Sign] 只有在所有簽署者完成簽署程式後，才會提交已啟用的最適化表單。 依預設， [!DNL Adobe Sign] 排程器服務排程在每24小時後檢查（輪詢）簽署者回應。 您可以為您的環境變更預設間隔。執行下列步驟以變更預設間隔：

1. 登入AEM [!DNL Forms] 具有管理員憑證的伺服器，並導覽至 **工具** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]**.

   您也可以在瀏覽器視窗中開啟下列URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找出並開啟 **[!UICONTROL Adobe Sign設定服務]** 選項。 指定 [cron表達](https://en.wikipedia.org/wiki/Cron#CRON_expression) 在 **[!UICONTROL 狀態更新調度程式表達式]** 欄位，按一下 **[!UICONTROL 儲存]**. 例如，要在每天00:00 am運行配置服務，請指定 `0 0 0 1/1 * ? *` 在 **[!UICONTROL 狀態更新調度程式表達式]** 欄位。

同步狀態的預設間隔為 [!DNL Adobe Sign] 現在已變更。

## 相關文章 {#related-articles}

* [在最適化表單中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [搭配使用Adobe Sign與AEM Forms（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
