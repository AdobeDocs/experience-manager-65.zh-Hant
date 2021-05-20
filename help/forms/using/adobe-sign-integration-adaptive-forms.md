---
title: 整合Adobe Sign與AEM Forms
seo-title: 整合Adobe Sign與AEM Forms
description: 了解如何設定Adobe Sign for AEM Forms
seo-description: 了解如何設定Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: 適用性Forms,Adobe Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 將[!DNL Adobe Sign]與AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}整合

[!DNL Adobe Sign] 啟用最適化表單的電子簽名工作流程。電子簽名改進了處理法律、銷售、工資、人力資源管理等許多領域的文檔的工作流。

在典型的[!DNL Adobe Sign]和最適化表單案例中，使用者填入最適化表單以申請服務&#x200B;**。**&#x200B;例如，信用卡申請和公民福利表。 當用戶填寫、提交和簽名申請表時，該表單被發送給服務提供商，以便採取進一步的行動。 服務提供商審核應用程式，並使用[!DNL Adobe Sign]標籤已批准的應用程式。 若要啟用類似的電子簽名工作流，您可以將[!DNL Adobe Sign]與AEM [!DNL Forms]整合。

若要搭配AEM [!DNL Forms]使用[!DNL Adobe Sign]，請在AEM雲端服務中設定[!DNL Adobe Sign]:

## 必備條件 {#prerequisites}

您需要下列項目來整合[!DNL Adobe Sign]與AEM [!DNL Forms]:

* 有效的[Adobe Sign開發人員帳戶。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* [啟用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms]伺服器。
* [Adobe Sign API應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API應用程式的憑證（用戶端ID和用戶端密碼）。
* 重新設定時，請從製作和發佈執行個體移除現有的[!DNL Adobe Sign]設定。
* 對製作和發佈執行個體使用[相同的加密金鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 使用AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}配置[!DNL Adobe Sign]

準備好必要條件後，請執行下列步驟，在製作執行個體上使用AEM [!DNL Forms]設定[!DNL Adobe Sign]:

1. 在AEM [!DNL Forms]作者例項上，導覽至&#x200B;**Tools** ![hammer](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**。
1. 在「**[!UICONTROL 設定瀏覽器]**」頁面上，點選「**[!UICONTROL 建立]**」。
   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
1. 在&#x200B;**[!UICONTROL 建立配置]**&#x200B;對話框中，為配置指定&#x200B;**[!UICONTROL 標題]**，啟用&#x200B;**[!UICONTROL 雲配置]**，然後點選&#x200B;**[!UICONTROL 建立]**。 它會為雲端服務建立設定容器。
1. 導覽至&#x200B;**工具** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**，並選取您在上述步驟中建立的設定容器。

   >[!NOTE]
   >
   >您可以執行步驟1-4建立新配置容器並在容器中建立[!DNL Adobe Sign]配置，或使用&#x200B;**Tools** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;中的現有`global`資料夾。 如果在新配置容器中建立配置，請在建立最適化表單時，確保在&#x200B;**[!UICONTROL 配置容器]**&#x200B;欄位中指定容器名稱。

   >[!NOTE]
   請確定雲端服務設定頁面的URL開頭為&#x200B;**HTTPS**。 否則，為AEM [!DNL Forms]伺服器啟用SSL](/help/sites-administering/ssl-by-default.md)。[

1. 在設定頁面上，點選&#x200B;**[!UICONTROL 建立]**&#x200B;以在AEM [!DNL Forms]中建立[!DNL Adobe Sign]設定。
1. 在&#x200B;**[!UICONTROL 建立Adobe Sign配置]**&#x200B;頁面的&#x200B;**[!UICONTROL 一般]**&#x200B;頁簽中，為配置指定&#x200B;**[!UICONTROL 名稱]**，然後點選&#x200B;**[!UICONTROL 下一步]**。 您可以選擇指定標題並瀏覽以選取設定的縮圖。

1. 將您目前瀏覽器視窗中的URL複製到記事本。 需要使用AEM[!DNL Forms]配置[!DNL Adobe Sign]應用程式。

1. 為[!DNL Adobe Sign]應用程式配置OAuth設定：

   1. 開啟瀏覽器視窗並登入[!DNL Adobe Sign]開發人員帳戶。
   1. 選擇為AEM [!DNL Forms]配置的應用程式，然後點選&#x200B;**[!UICONTROL 為應用程式配置OAuth]**。
   1. 將&#x200B;**[!UICONTROL 客戶端ID]**&#x200B;和&#x200B;**[!UICONTROL 客戶端密碼]**&#x200B;複製到記事本。
   1. 在&#x200B;**[!UICONTROL 重新導向URL]**&#x200B;方塊中，新增先前步驟中複製的HTTPS URL。
   1. 為[!DNL Adobe Sign]應用程式啟用以下OAuth設定，然後按一下&#x200B;**[!UICONTROL Save]**。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   如需設定[!DNL Adobe Sign]應用程式的OAuth設定及取得金鑰的逐步資訊，請參閱應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)開發人員檔案的[設定oAuth設定。

   ![OAuth設定](assets/oauthconfig_new.png)

1. 返回&#x200B;**[!UICONTROL 建立Adobe Sign設定]**&#x200B;頁面。 在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中， **[!UICONTROL OAuth URL]**&#x200B;欄位提及下列預設URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1** 表示預設資料庫共用。

   您可以修改資料庫共用的值。 重新啟動伺服器，以便能夠將新值用於資料庫共用。

   >[!NOTE]
   請確定您的製作和發佈執行個體設定指向相同的分區。 如果您為組織建立多個Adobe Sign設定，請確定所有設定都使用相同的分區。

1. 指定在步驟8中複製的&#x200B;**用戶端ID**（亦稱為應用程式ID）和&#x200B;**用戶端密碼**。 選擇&#x200B;**[!UICONTROL 為附件啟用Adobe Sign也]**&#x200B;選項，將附加至適用性表單的檔案附加至要簽名的相應[!DNL Adobe Sign]文檔。

   點選&#x200B;**[!UICONTROL 連線至Adobe Sign]**。 提示輸入憑據時，請提供建立[!DNL Adobe Sign]應用程式時使用的帳戶的用戶名和密碼。

   點選&#x200B;**[!UICONTROL 建立]**&#x200B;以建立[!DNL Adobe Sign]設定。

1. 開啟AEM Web Console。 URL為`https://'[server]:[port]'/system/console/configMgr`
1. 開啟&#x200B;**[!UICONTROL Forms Common Configuration Service]。**
1. 在&#x200B;**[!UICONTROL 允許]**&#x200B;欄位中， **選擇**&#x200B;所有用戶 — 所有用戶（匿名或已登錄）都可以預覽附件、驗證和簽名表單，然後按一下&#x200B;**[!UICONTROL 保存]。** 製作例項已設定為使 [!DNL Adobe Sign]用。
1. 發佈設定。
1. 使用[replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html)在對應的發佈執行個體上建立相同的配置。

現在，[!DNL Adobe Sign]已與AEM [!DNL Forms]整合，可在最適化表單中使用。 若要在適用性表單](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)中使用Adobe Sign服務，請在適用性表單屬性中指定上述建立的設定容器。[



## 配置[!DNL Adobe Sign]調度程式以同步簽名狀態{#configure-adobe-sign-scheduler-to-sync-the-signing-status}

只有所有簽署者完成簽署程式後，才會提交已啟用的[!DNL Adobe Sign]適用性表單。 預設情況下，[!DNL Adobe Sign]調度程式服務將安排在每24小時後檢查（輪詢）簽名者響應。 您可以變更環境的預設間隔。 執行下列步驟以變更預設間隔：

1. 使用管理員憑證登入AEM [!DNL Forms]伺服器，並導覽至&#x200B;**Tools** > **[!UICONTROL Operations]** > **[!UICONTROL Web主控台]**。

   您也可以在瀏覽器視窗中開啟下列URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到並開啟&#x200B;**[!UICONTROL Adobe Sign Configuration Service]**&#x200B;選項。 在&#x200B;**[!UICONTROL 狀態更新排程器運算式]**&#x200B;欄位中指定[cron運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression)，然後按一下&#x200B;**[!UICONTROL 儲存]**。 例如，要在上午00:00每天運行配置服務，請在&#x200B;**[!UICONTROL 狀態更新調度程式表達式]**&#x200B;欄位中指定`0 0 0 1/1 * ? *`。

[!DNL Adobe Sign]同步狀態的預設間隔現在已更改。

## 相關文章{#related-articles}

* [在最適化表單中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [搭配使用Adobe Sign與AEM Forms（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
