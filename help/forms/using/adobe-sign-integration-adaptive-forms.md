---
title: 將Adobe Sign與AEM Forms整合
seo-title: 將Adobe Sign與AEM Forms整合
description: 瞭解如何為AEM Forms設定Adobe Sign
seo-description: 瞭解如何為AEM Forms設定Adobe Sign
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 將Adobe Sign與AEM Forms整合{#integrate-adobe-sign-with-aem-forms}

Adobe Sign可針對最適化表單啟用電子簽名工作流程。 電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在典型的Adobe sign和最適化表單案例中，使用者會填入最適化表單以 **申請服務**。 例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，表格會傳送給服務提供者，以做進一步的動作。 服務供應商會審核應用程式，並使用Adobe Sign來標示已核准的應用程式。 若要啟用類似的電子簽名工作流程，您可以將Adobe Sign與AEM Forms整合。

若要搭配AEM Forms使用Adobe Sign，請在AEM Cloud services中設定Adobe Sign:

## 必備條件 {#prerequisites}

您需要下列項目才能將Adobe Sign與AEM Forms整合：

* 有效的 [Adobe sign開發人員帳戶。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 啟用 [SSL的](/help/sites-administering/ssl-by-default.md) AEM Forms伺服器。
* Adobe [Sign API應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* Adobe Sign API應用程式的認證（用戶端ID和用戶端密碼）。

## 使用AEM Forms設定Adobe Sign {#configure-adobe-sign-with-aem-forms}

在具備必要條件後，請執行下列步驟，在「作者」例項上以AEM Forms設定Adobe Sign:

1. 在AEM Forms作者例項上，導覽至「工 **具** > ![](assets/hammer.png) 一般 **>** 設定瀏覽器 ****」。
1. 在「設定瀏 **[!UICONTROL 覽器]** 」頁面上，點 **[!UICONTROL 選「建立」]**。
1. 在「建 **[!UICONTROL 立設定]** 」對話方塊中，指定設定的 **[!UICONTROL Title]** ，啟用「 **[!UICONTROL Cloud設定」]**、「建立 **** Create」。 它會為雲端服務建立組態容器。
1. 導覽至「 **工具** > ![](assets/hammer.png) Cloud Services **>** Adobe Sign **** 」，然後選取您在上述步驟中建立的設定容器。

   >[!NOTE]
   >
   >請確定雲端服務設定頁面的URL以 **HTTPS開頭**。 若未啟用， [請為AEM](/help/sites-administering/ssl-by-default.md) Forms伺服器啟用SSL。

1. 在設定頁面上，點選「 **[!UICONTROL 建立]** 」以在AEM Forms中建立Adobe Sign設定。
1. 在「建 **[!UICONTROL 立Adobe Sign設定]** 」頁面的「一般 **[!UICONTROL 」標籤中，為設定和Next]** (下一 ********&#x200B;步)指定名稱。 您可以選擇指定標題並瀏覽以選取設定的縮圖。

   複製目前瀏覽器視窗中的URL。 您必須使用AEM Forms來設定Adobe Sign應用程式。

1. 設定Adobe Sign應用程式的OAuth設定：

   1. 開啟瀏覽器視窗並登入Adobe Sign開發人員帳戶。
   1. 選取為AEM Forms設定的應用程式，然後點選「設定應用程式的OAuth」。
   1. 在「重 **新導向URL** 」方塊中，新增在上一步驟中複製的HTTPS URL，然後按一下「 **儲存」**。
   1. 為Adobe Sign應用程式啟用下列OAuth設定，然後按一下「儲 **存**」。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read
   如需設定Adobe Sign應用程式的OAuth設定並取得索引鍵的逐步資訊，請參閱應用程式開發人員文 [件的設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobeio/adobeio-documentation/master/sign/gstarted/configure_oauth.md) oAuth設定。

   ![OAuth設定](assets/oauthconfig_new.png)

1. 返回「建立 **Adobe Sign設定」頁面** 。 在「設 **[!UICONTROL 定]** 」標籤中， **[!UICONTROL OAuth URL]** 欄位提及下列預設URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1是指** 預設的資料庫共用。

   可以修改資料庫共用的值。 重新啟動伺服器，以便能夠為資料庫共用使用新值。

1. 指定 **用戶端ID** （也稱為應用程式ID）和用戶 **端密碼**。 選取「 **Enable Adobe Sign for attachments andlo** （啟用附件的Adobe Sign）」選項，將附加至最適化表單的檔案附加至要傳送以供簽署的對應Adobe Sign檔案。

   Tap **[!UICONTROL Connect to Adobe Sign]**. 當提示輸入認證時，請提供建立Adobe Sign應用程式時所使用之帳戶的使用者名稱和密碼。

   點選 **[!UICONTROL 「建立]** 」以建立Adobe Sign設定。

1. 開啟AEM Web Console。 URL是 `https://[server]:[port]/system/console/configMgr`
1. 開啟 **Forms Common Configuration Service。**
1. 在「允 **許** 」欄位中，選 **取「所有使用者** -所有使用者（匿名或登入）」，可預覽附件、驗證和簽署表格，然後按一下「儲 **存」。** 作者例項已設定為使用Adobe Sign。
1. 在 [Publish](/help/sites-deploying/deploy.md) 例項上，登入並開啟下列URL:

   `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`

1. 重複步驟1至12，以使用AEM Forms設定Adobe Sign。 使用相同的設定標題（如步驟3所指定）和相同的名稱（如步驟6所指定）來復製作者實例上所設定的設定。

   現在，Adobe Sign已與AEM Forms整合，可在最適化表單中使用。 若要 [在最適化表單中使用Adobe Sign服務](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，請在最適化表單屬性中指定上方建立的組態容器。

## 設定Adobe Sign排程器以同步簽署狀態 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

只有在所有簽署者完成簽署程式後，才會提交啟用Adobe Sign的調適性表單。 依預設，Adobe Sign Scheduler服務會排程在每24小時後檢查（民調問答）簽署者回應。 您可以更改環境的預設間隔。 執行以下步驟以更改預設間隔：

1. 使用管理員認證登入AEM Forms伺服器，並導覽至「工 **具** > **作業** > **Web Console**」。

   您也可以在瀏覽器視窗中開啟下列URL:
   `https://[localhost]:[port]/system/console/configMgr`

1. 找到並開啟 **Adobe Sign Configuration Service選項** 。 在「狀態更 [新排程器運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 」欄位中指 **定cron運算式，然後按一下「** 儲存 ****」。 例如，要每天00:00 am運行配置服務，請在「狀態更新調度器運 `0 0 0 1/1 * ? *` 算式」 **欄位中指定** 。

Adobe Sign的同步狀態預設間隔現在已變更。

## 相關文章 {#related-articles}

* [在最適化表單中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [搭配AEM Forms（視訊）使用Adobe Sign](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)

