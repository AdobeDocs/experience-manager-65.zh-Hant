---
title: 整合Adobe Sign與AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: 瞭解如何為AEM Forms配置Adobe Sign
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 26%

---

# 整合 [!DNL Adobe Sign] AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 啟用適應表單的電子簽名工作流。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

典型 [!DNL Adobe Sign] 和自適應表單方案，用戶填充自適應表單 **申請服務**。 例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者便會審查申請並使用 [!DNL Adobe Sign] 標記已核准申請。要啟用類似的電子簽名工作流，您可以整合 [!DNL Adobe Sign] AEM [!DNL Forms]。

要使用 [!DNL Adobe Sign] AEM [!DNL Forms]配置 [!DNL Adobe Sign] 在AEM雲服務中：

## 必備條件 {#prerequisites}

您需要以下元件來整合 [!DNL Adobe Sign] AEM [!DNL Forms]:

* 主要 [Adobe Sign 開發人員帳戶.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 安 [已啟用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 伺服器。
* [Adobe Sign API 應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 應用程式的認證 (用戶端 ID 和用戶端密碼)。
* 重新配置時，刪除現有 [!DNL Adobe Sign] 從作者實例和發佈實例進行配置。
* 使用製作和發佈執行個體的[同一密碼編譯金鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 配置 [!DNL Adobe Sign] AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

先決條件就位後，請執行以下步驟來配置 [!DNL Adobe Sign] AEM [!DNL Forms] 在作者實例上：

1. 開AEM [!DNL Forms] 作者實例，導航 **工具** ![錘](assets/hammer.png) > **[!UICONTROL 常規]** > **[!UICONTROL 配置瀏覽器]**。
1. 在 **[!UICONTROL 配置瀏覽器]** 頁面，點擊 **[!UICONTROL 建立]**。
   * 查看 [配置瀏覽器](/help/sites-administering/configurations.md) 的子菜單。
1. 在 **[!UICONTROL 建立配置]** 對話框，指定 **[!UICONTROL 標題]** 對於配置，啟用 **[!UICONTROL 雲配置]**，然後點擊 **[!UICONTROL 建立]**。 它為雲服務建立配置容器。
1. 導航到 **工具** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 並選擇您在上一步中建立的配置容器。

   >[!NOTE]
   >
   >您可以執行步驟1-4以建立新配置容器並建立 [!DNL Adobe Sign] 配置或使用現有 `global` 資料夾 **工具** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**。 如果在新配置容器中建立配置，請確保在 **[!UICONTROL 配置容器]** 的子菜單。

   >[!NOTE]
   確保雲服務配置頁的URL以 **HTTPS**。 如果沒有， [啟用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 伺服器。

1. 在配置頁上，點擊 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 配置AEM [!DNL Forms]。
1. 在 **[!UICONTROL 常規]** 頁籤 **[!UICONTROL 建立Adobe Sign配置]** 頁，指定 **[!UICONTROL 名稱]** 配置和點擊 **[!UICONTROL 下一個]**。 您可以選擇指定標題並瀏覽以選擇配置的縮略圖。

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。需要配置 [!DNL Adobe Sign] 應用程式AEM[!DNL Forms]。

1. 在 **[!UICONTROL 設定]** 頁籤 **[!UICONTROL OAuth URL]** 欄位包含預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL  Adobe Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果您建立 Adobe Experience Manager 功能或元件的另一個 [!DNL Adobe Sign] 設定請確保所有 [!DNL Adobe Sign] Cloud Configurations 都指向相同分片。

   >[!NOTE]
   保留 **建立Adobe Sign配置** 的子菜單。 別關。 可以檢索 **客戶端ID** 和 **客戶端密碼** 配置OAuth設定後 [!DNL Adobe Sign] 如後續步驟中所述。


1. 設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器窗口並登錄到 [!DNL Adobe Sign] 開發者帳戶。
   1. 選擇為配置的應用程AEM序 [!DNL Forms]，然後點擊 **[!UICONTROL 為應用程式配置OAuth]**。
   1. 複製 **[!UICONTROL 客戶端ID]** 和 **[!UICONTROL 客戶端密碼]** 記事本。
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加上一步中複製的HTTPS URL。
   1. 為 [!DNL Adobe Sign] 應用程式，按一下 **[!UICONTROL 保存]**。
   * 已讀取
   * 聚合_寫入
   * 存檔_發送
   * 小部件_寫入
   * 工作流_讀取

   如需設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」開發人員文件。

   ![OAuth Config](assets/oauthconfig_new.png)

1. 返回 **[!UICONTROL 建立Adobe Sign配置]** 的子菜單。 在 **[!UICONTROL 設定]** 頁籤 **[!UICONTROL OAuth URL]** 欄位中提到預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。

   您可以修改資料庫分片的值。重新啟動伺服器，以便能夠使用資料庫分片的新值。

   >[!NOTE]
   確保您的作者和發佈實例配置指向同一分片。 如果您為一個組織建立多個Adobe Sign配置，請確保所有配置都使用相同的分片。

1. 返回 **[!UICONTROL 建立Adobe Sign配置]** 的子菜單。 在 **[!UICONTROL 設定]** 頁籤，指定 **客戶端ID** （也稱為應用程式ID）和 **客戶端密碼**。 使用 [客戶端ID與Adobe Sign應用的客戶端密碼](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 為AEM Forms創作。

1. 選擇 **[!UICONTROL 還啟用Adobe Sign附件]** 選項，將附加到自適應窗體的檔案附加到相應 [!DNL Adobe Sign] 文檔已發送以進行簽名。

1. 點擊 **[!UICONTROL 連接到Adobe Sign]**。 出現認證提示時，請提供在建立 [!DNL Adobe Sign] 應用程式時使用的帳戶使用者名稱和密碼。

1. 點擊 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 配置。

1. 開啟AEMWeb控制台。 URL為 `https://'[server]:[port]'/system/console/configMgr`
1. 開啟 **[!UICONTROL Forms通用配置服務]。**
1. 在 **[!UICONTROL 允許]** 欄位， **選擇** 所有用戶 — 所有用戶（匿名或登錄）都可以預覽附件、驗證和簽名表單，然後按一下 **[!UICONTROL 保存]。** 作者實例配置為使用 [!DNL Adobe Sign]。
1. 發佈配置。
1. 使用 [複製](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=zh-Hant) 在相應的發佈實例上建立相同的配置。

現在， [!DNL Adobe Sign] 與 [!DNL Forms] 可以在適應性形式中使用。 至 [以自適應形式使用Adobe Sign服務](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，指定在自適應窗體屬性中建立的配置容器。



## 配置 [!DNL Adobe Sign] 計畫程式以同步簽名狀態 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

安 [!DNL Adobe Sign] 只有在所有簽名者完成簽名過程後，才提交啟用的自適應表單。 預設情況下， [!DNL Adobe Sign] 計畫程式服務計畫在每24小時後檢查（輪詢）簽名者響應。 您可以為您的環境變更預設間隔。執行以下步驟以更改預設間隔：

1. 登錄到AEM [!DNL Forms] 具有管理員憑據的伺服器並導航 **工具** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。

   也可以在瀏覽器窗口中開啟以下URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 查找並開啟 **[!UICONTROL Adobe Sign配置服務]** 的雙曲餘切值。 指定 [cron表達](https://en.wikipedia.org/wiki/Cron#CRON_expression) 的 **[!UICONTROL 狀態更新計畫程式表達式]** 按一下 **[!UICONTROL 保存]**。 例如，要每天00:00運行配置服務，請指定 `0 0 0 1/1 * ? *` 的 **[!UICONTROL 狀態更新計畫程式表達式]** 的子菜單。

同步狀態的預設間隔 [!DNL Adobe Sign] 的子菜單。

## 相關文章 {#related-articles}

* [以自適應形式使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [使用Adobe Sign與AEM Forms（視頻）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
