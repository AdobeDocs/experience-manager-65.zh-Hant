---
title: 將Adobe Sign與AEM Forms整合
seo-title: Integrate Adobe Sign with AEM Forms
description: 瞭解如何設定適用於AEM Forms的Adobe Sign
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 762e918a2c65898fc518f131d44421fb82ce4d6f
workflow-type: tm+mt
source-wordcount: '1973'
ht-degree: 19%

---

# 整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 啟用最適化表單的電子簽章工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在標準 [!DNL Adobe Acrobat Sign] 和最適化表單情境下，用戶會填寫最適化表單來申請服務。例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者便會審查申請並使用 [!DNL Adobe Acrobat Sign] 標記已核准申請。AEM Forms支援適用於政府的Adobe Acrobat Sign和Adobe Acrobat Sign Solutions。 根據您的授權和需求，您可以將AEM Forms與以下任一解決方案整合或連線：

* [將AEM Forms與Adobe Acrobat Sign連線](#adobe-sign)
* [連線適用於政府的AEM Forms與Adobe Acrobat Sign Solutions](#adobe-acrobat-sign-for-government)

## 將AEM Forms與Adobe Acrobat Sign連線 {#adobe-sign}

若要連線 **[!DNL AEM Forms]** 替換為 **[!DNL Adobe Acrobat Sign]**，設定「先決條件」區段中列出的軟體和帳戶，並將Adobe Sign連線至您的所有AEM Forms作者和發佈執行個體：

## 必備條件 {#prerequisites}

您需要下列專案才能整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]：

* 主要 [Adobe Sign 開發人員帳戶.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 一個 [SSL已啟用](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 伺服器。
* [Adobe Sign API 應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] API 應用程式的認證 (用戶端 ID 和用戶端密碼)。
* 重新設定時，移除現有的 [!DNL Adobe Sign] 來自作者和發佈執行個體的設定。
* 使用製作和發佈執行個體的[同一密碼編譯金鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 設定 [!DNL Adobe Sign] 使用AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

已具備下列先決條件後，請執行以下步驟來設定 [!DNL Adobe Sign] 使用AEM [!DNL Forms] 在作者執行個體上：

1. 在AEM上 [!DNL Forms] 作者執行個體，導覽至 **工具** ![槌子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 於 **[!UICONTROL 設定瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
   * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 針對設定，啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 它會建立設定容器。
1. 導覽至 **工具** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 並選取您在上一步中建立的設定容器。

   >[!NOTE]
   >
   >您可以執行步驟1至4來建立新的設定容器並建立 [!DNL Adobe Sign] 容器中的設定或使用現有的 `global` 資料夾位於 **工具** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 如果您在新設定容器中建立設定，請務必在 **[!UICONTROL 設定容器]** 欄位建立最適化表單時。

   >[!NOTE]
   >
   確定「Cloud Services設定」頁面的URL開頭為 **HTTPS**. 如果沒有， [啟用SSL](/help/sites-administering/ssl-by-default.md) 適用於AEM [!DNL Forms] 伺服器。

1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] AEM中的設定 [!DNL Forms].
1. 在 **[!UICONTROL 一般]** 的標籤 **[!UICONTROL 建立Adobe Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** 設定並點選 **[!UICONTROL 下一個]**. 您可以選擇指定標題並瀏覽以選取設定的縮圖。

1. 將您目前瀏覽器視窗中的 URL 複製到筆記本。需要設定 [!DNL Adobe Sign] 使用AEM的應用程式[!DNL Forms].

1. 在 **[!UICONTROL 設定]** 標籤， **[!UICONTROL OAuth URL]** 欄位包含預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。您可以修改資料庫分片的值。確保[!DNL  Adobe Sign] Cloud Configurations 指向[正確的分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果您建立 Adobe Experience Manager 功能或元件的另一個 [!DNL Adobe Sign] 設定請確保所有 [!DNL Adobe Sign] Cloud Configurations 都指向相同分片。

   >[!NOTE]
   >
   保留 **建立Adobe Sign設定** 頁面開啟。 不要關閉它。 您可以擷取 **使用者端ID** 和 **使用者端密碼** 設定的OAuth設定後 [!DNL Adobe Sign] 應用程式，如未來步驟所述。


1. 設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定：

   1. 開啟瀏覽器視窗並登入 [!DNL Adobe Sign] 開發人員帳戶。
   1. 選取為AEM設定的應用程式 [!DNL Forms]，然後點選 **[!UICONTROL 設定應用程式的OAuth]**.
   1. 複製 **[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]** 記事本。
   1. 在 **[!UICONTROL 重新導向URL]** 方塊中，新增在上一步中複製的HTTPS URL。
   1. 啟用下列OAuth設定 [!DNL Adobe Sign] 應用程式並按一下 **[!UICONTROL 儲存]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   如需設定 [!DNL Adobe Sign] 應用程式的 OAuth 設定並取得金鑰的逐步資訊，請參閱「[設定應用程式的 OAuth 設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」開發人員文件。

   ![OAuth Config](assets/oauthconfig_new.png)

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 標籤， **[!UICONTROL OAuth URL]** 欄位提及預設URL。 URL 的格式是：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指預設的資料庫分片。

   您可以修改資料庫分片的值。重新啟動伺服器，以便能夠使用資料庫分片的新值。

   >[!NOTE]
   >
   確保您的作者和發佈執行個體設定指向相同分片。 如果您為組織建立多個Adobe Sign設定，請確定所有設定都使用相同分片。

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 索引標籤中，指定 **使用者端ID** （也稱為應用程式ID）和 **使用者端密碼**. 使用 [Adobe Sign應用程式的使用者端ID和使用者端密碼](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 已為AEM Forms建立。

1. 選取 **[!UICONTROL 也啟用附件的Adobe Sign]** 用於將附加到最適化表單的檔案附加至對應 [!DNL Adobe Sign] 檔案已傳送供簽署。

1. 點選 **[!UICONTROL 連線至Adobe Sign]**. 出現認證提示時，請提供在建立 [!DNL Adobe Sign] 應用程式時使用的帳戶使用者名稱和密碼。

1. 點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 設定。

1. 開啟AEM Web Console。 URL是 `https://'[server]:[port]'/system/console/configMgr`
1. 開啟 **[!UICONTROL Forms通用設定服務].**
1. 在 **[!UICONTROL 允許]** 欄位， **選取** 所有使用者 — 所有使用者（匿名或登入）都可以預覽附件、驗證和簽署表單，以及按一下 **[!UICONTROL 儲存].** 作者執行個體已設定為使用 [!DNL Adobe Sign].
1. 發佈設定。
1. 使用 [復寫](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=zh-Hant) 以在對應的發佈執行個體上建立相同的設定。

現在， [!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 並準備用於調適型表單。 至 [在最適化表單中使用Adobe Sign服務](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，請在最適化表單屬性中指定上述建立的設定容器。

## 連線適用於政府的AEM Forms與Adobe Acrobat Sign Solutions {#adobe-acrobat-sign-for-government}

將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線是多步驟流程。 其中涉及：

* 為您的AEM執行個體建立重新導向URL
* 與適用於政府團隊的Adobe Sign解決方案共用重新導向URL和範圍
* 從Adobe Sign團隊接收認證
* 使用收到的認證連線AEM Forms與適用於政府的Adobe Acrobat Sign Solutions

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 開始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

開始將AEM Forms與Adobe Acrobat Sign解決方案連線之前，

* 確保您的 [適用於政府的Adobe Acrobat Sign Solutions](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 已布建帳戶。
* 您的AEM [!DNL Forms] 伺服器為 [SSL已啟用](/help/sites-administering/ssl-by-default.md) .
* 您的AEM [!DNL Forms] 伺服器正在使用 [相同的加密金鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) 用於製作和發佈例項。

### 將AEM Forms連結至適用於政府的Adobe Acrobat Sign Solutions {#connect-adobe-acrobat-sign-for-government}

#### 為您的AEM執行個體建立重新導向URL

1. 在您的AEM Forms執行個體上，導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 於 **[!UICONTROL 設定瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 針對設定，啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 它會建立設定容器。 確定容器/資料夾名稱未包含任何空格。

1. 導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 並開啟您在上一步建立的設定容器。 建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。
1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Acrobat Sign] AEM Forms中的設定。
1. 將您目前瀏覽器視窗的URL從URL複製到記事本。 此URL稱為 `re-direct URL`. 在下一節中，您共用 `re-direct URL` 和 `Scopes` Adobe Sign團隊和要求認證（使用者端ID和使用者端密碼）。

>[!NOTE]
>
>
* A `re-direct URL` 應包含 [頂層](https://en.wikipedia.org/wiki/Top-level_domain) 網域。 例如 `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* 請勿使用本機URL做為 `re-direct URL`. 例如，`https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`。


#### 與Adobe Sign團隊共用重新導向URL和範圍並接收認證

適用於政府解決方案的Adobe Acrobat Sign團隊需要 `re-direct URL` 以及要為您的Adobe Acrobat Sign應用程式啟用的特定範圍（如下所列），以產生認證（使用者端ID和使用者端密碼），讓您將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線。

共用 `scopes` （如下所列）和 `re-direct URL` 建立並記錄上一節的最後一步，並請您的Adobe Acrobat Sign政府解決方案代表 [Adobe Professional Services團隊成員](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_範圍_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

代表會產生認證並與您共用。 在下一節中，您會使用認證（使用者端ID和使用者端密碼）來將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線。

#### 使用收到的憑證將AEM Forms與適用於政府的Adobe Acrobat Sign Solutions連線

1. 開啟 `re-direct URL` 在您的瀏覽器中。 您已建立並記下 `re-direct URL` 在的最後一個步驟中 [在您的AEM執行個體上建立重新導向URL](#create-redirect-url) 區段。

1. 在 **[!UICONTROL 一般]** 的標籤 **[!UICONTROL 建立Adobe Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** ，然後點選「 」 **[!UICONTROL 下一個]**. 您可以選擇指定 **[!UICONTROL 標題]** 並瀏覽以選取 **[!UICONTROL 縮圖]** 用於設定。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 設定]** 的標籤 **[!UICONTROL 建立Adobe Sign設定]** 頁面，用於 **[!UICONTROL 選取解決方案]** 選項，選取 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![適用於政府的Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-for-govt.png)

1. 在 **[!UICONTROL 電子郵件]** 已歸檔，請為政府帳戶指定與您的Adobe Acrobat Sign Solutions相關聯的電子郵件地址。

1. 此 **[!UICONTROL OAuth URL]** 欄位會指定Adobe Sign資料庫分片。 欄位包含預設URL。 請勿變更URL。

1. 使用Adobe Acrobat Sign為政府解決方案代表共用的認證([Adobe Professional Services團隊成員])在上一節中為[**[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]**]。

1. 選取 **[!UICONTROL 為附件啟用Adobe Acrobat Sign]** 將最適化表單附加的檔案附加至對應 [!DNL Adobe Acrobat Sign] 檔案已傳送供簽署。

1. 點選 **[!UICONTROL 連線至Adobe Sign]**. 出現認證提示時，請提供在建立 [!DNL Adobe Acrobat Sign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認存取時 `Adobe Acrobat Sign for Government Solutions` 和，按一下 **[!UICONTROL 允許存取]**. 如果認證正確且您允許 [!DNL AEM Forms] 存取您的 [!DNL Adobe Acrobat Sign] 開發人員帳戶，則會出現與以下訊息相似的成功訊息。

   ![Adobe Acrobat Sign雲端設定成功](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   出現認證提示時，請提供在建立 [!DNL Adobe Acrobat Sign] 應用程式時使用的帳戶使用者名稱和密碼。當要求確認存取時 `your account`，然後按一下 **[!UICONTROL 允許存取]**.

1. 點選 **[!UICONTROL 建立]** 以建立設定。
1. 開啟AEM Web Console。 URL是 `https://'[server]:[port]'/system/console/configMgr`
1. 開啟 **[!UICONTROL Forms通用設定服務].**
1. 在 **[!UICONTROL 允許]** 欄位， **選取** 所有使用者 — 所有使用者（匿名或登入）都可以預覽附件、驗證和簽署表單，以及按一下 **[!UICONTROL 儲存].** 作者執行個體已設定為使用 [!DNL Adobe Sign].

1. 發佈設定。
1. 使用 [復寫](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=zh-Hant) 以在對應的發佈執行個體上建立相同的設定。

現在，您可以 [在最適化表單中使用新增Adobe Acrobat Sign欄位](working-with-adobe-sign.md) 或 [AEM工作流程](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). 確保您將用於Cloud Service設定的設定容器新增至啟用的所有最適化Forms [!DNL Adobe Acrobat Sign]. 您可從最適化表單的屬性指定設定容器。


## 設定 [!DNL Adobe Sign] 同步簽名狀態的排程器 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

一個 [!DNL Adobe Sign] 啟用的最適化表單只會在所有簽署者完成簽署程式後提交。 根據預設， [!DNL Adobe Sign] 排程器服務已排程為每24小時檢查（輪詢）簽署者回應。 您可以為您的環境變更預設間隔。執行以下步驟來變更預設間隔：

1. 登入AEM [!DNL Forms] 含管理員憑證的伺服器，並導覽至 **工具** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.

   您也可以在瀏覽器視窗中開啟下列URL：
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到並開啟 **[!UICONTROL Adobe Sign設定服務]** 選項。 指定 [cron運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 在 **[!UICONTROL 狀態更新排程器運算式]** 欄位並按一下 **[!UICONTROL 儲存]**. 例如，若要在每日午夜12點執行設定服務，請指定 `0 0 0 1/1 * ? *` 在 **[!UICONTROL 狀態更新排程器運算式]** 欄位。

同步狀態的預設間隔 [!DNL Adobe Sign] 現已變更。

## 相關文章 {#related-articles}

* [在最適化表單中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign具有表單中心工作流程](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [將Adobe Sign與AEM Forms搭配使用（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
