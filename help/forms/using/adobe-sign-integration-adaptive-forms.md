---
title: 將Adobe Sign與AEM Forms整合
seo-title: 將Adobe Sign與AEM Forms整合
description: 瞭解如何為AEM Forms配置Adobe Sign
seo-description: 瞭解如何為AEM Forms配置Adobe Sign
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: 最適化Forms,Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# 將[!DNL Adobe Sign]與AEM[!DNL Forms]{#integrate-adobe-sign-with-aem-forms}整合

[!DNL Adobe Sign] 可針對最適化表單啟用電子簽名工作流程。電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在典型的[!DNL Adobe Sign]和適應性表單場景中，用戶填充適應性表單以申請服務&#x200B;**。**&#x200B;例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，表格會傳送給服務提供者，以做進一步的動作。 服務提供商會審查應用程式，並使用[!DNL Adobe Sign]標籤批准的應用程式。 若要啟用類似的電子簽名工作流程，您可將[!DNL Adobe Sign]與AEM[!DNL Forms]整合。

若要搭配使用[!DNL Adobe Sign]AEM和[!DNL Forms]，請在AEM Cloud Services中設定[!DNL Adobe Sign]:

## 必備條件 {#prerequisites}

您需要以下各項才能將[!DNL Adobe Sign]與AEM[!DNL Forms]整合：

* 有效[Adobe Sign開發人員帳戶。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* [啟用SSL的](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms]伺服器。
* [Adobe SignAPI應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API應用程式的認證（用戶端ID和用戶端密碼）。
* 重新設定時，請從作者和發佈例項中移除現有的[!DNL Adobe Sign]設定。
* 對於作者和發佈實例，請使用[相同的加密密鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 將[!DNL Adobe Sign]配置AEM為[!DNL Forms] {#configure-adobe-sign-with-aem-forms}

先決條件就位後，請執行下列步驟，在「作者」例項上將AEM[!DNL Adobe Sign]設定為[!DNL Forms]:

1. 在AEM[!DNL Forms]作者實例上，導航至&#x200B;**工具**![hammer](assets/hammer.png) > **[!UICONTROL 一般]** >配置瀏覽器&#x200B;]**。**[!UICONTROL 
1. 在&#x200B;**[!UICONTROL 配置瀏覽器]**&#x200B;頁面上，點選&#x200B;**[!UICONTROL 建立]**。
   * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定設定的&#x200B;**[!UICONTROL 標題]**，啟用&#x200B;**[!UICONTROL 雲端設定]**，然後點選&#x200B;**[!UICONTROL 建立]**。 它會為雲端服務建立組態容器。
1. 導覽至&#x200B;**工具**![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**，然後選取您在上述步驟中建立的組態容器。

   >[!NOTE]
   >
   >您可以執行步驟1-4以建立新配置容器並在容器中建立[!DNL Adobe Sign]配置，或使用&#x200B;**工具**![槌](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;中的現有`global`資料夾。 如果您在新配置容器中建立配置，請確保在建立自適應表單時在&#x200B;**[!UICONTROL 配置容器]**&#x200B;欄位中指定容器名稱。

   >[!NOTE]
   請確定雲端服務設定頁面的URL以&#x200B;**HTTPS**&#x200B;開頭。 否則，[為[!DNL Forms]伺服器啟AEM用SSL](/help/sites-administering/ssl-by-default.md)。

1. 在配置頁面上，點選&#x200B;**[!UICONTROL Create]**&#x200B;以在AEM[!DNL Forms]中建立[!DNL Adobe Sign]組態。
1. 在&#x200B;**[!UICONTROL 建立Adobe Sign配置]**&#x200B;頁的&#x200B;**[!UICONTROL 常規]**&#x200B;頁籤中，為配置指定&#x200B;**[!UICONTROL 名稱]**&#x200B;並點選&#x200B;**[!UICONTROL Next]**。 您可以選擇指定標題並瀏覽以選取設定的縮圖。

1. 將您目前瀏覽器視窗中的URL複製至記事本。 必須使用[!DNL Forms]配置[!DNL Adobe Sign]AEM應用程式。

1. 為[!DNL Adobe Sign]應用程式設定OAuth設定：

   1. 開啟瀏覽器視窗並登入[!DNL Adobe Sign]開發人員帳戶。
   1. 選擇為[!DNL Forms]配AEM置的應用程式，然後按一下&#x200B;**[!UICONTROL 為應用程式配置OAuth。]**
   1. 將&#x200B;**[!UICONTROL 客戶端ID]**&#x200B;和&#x200B;**[!UICONTROL 客戶端密碼]**&#x200B;複製到記事本。
   1. 在&#x200B;**[!UICONTROL 重新導向URL]**&#x200B;方塊中，新增上一步驟所複製的HTTPS URL。
   1. 為[!DNL Adobe Sign]應用程式啟用下列OAuth設定，然後按一下「儲存」。****
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   如需設定[!DNL Adobe Sign]應用程式的OAuth設定並取得索引鍵的逐步資訊，請參閱[設定應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)開發人員檔案的oAuth設定。

   ![OAuth設定](assets/oauthconfig_new.png)

1. 返回&#x200B;**[!UICONTROL 建立Adobe Sign配置]**&#x200B;頁。 在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中，**[!UICONTROL OAuth URL]**&#x200B;欄位提及下列預設URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1** 是指預設資料庫共用。

   您可以修改資料庫共用的值。 重新啟動伺服器，以便能夠為資料庫共用使用新值。

   >[!NOTE]
   請確定您的作者和發佈例項設定指向相同的分片。 如果您為組織建立多個Adobe Sign配置，請確保所有配置都使用相同的分片。

1. 指定在步驟8中編寫的&#x200B;**用戶端ID**（也稱為應用程式ID）和&#x200B;**用戶端密碼**。 選擇&#x200B;**[!UICONTROL EnableAdobe Sign for attachments also]**&#x200B;選項，將附加到自適應表單的檔案附加到相應的[!DNL Adobe Sign]文檔，以進行簽名。

   點選&#x200B;**[!UICONTROL 連線至Adobe Sign]**。 當提示輸入憑證時，請提供建立[!DNL Adobe Sign]應用程式時所使用之帳戶的使用者名稱和密碼。

   點選「**[!UICONTROL 建立]**」以建立[!DNL Adobe Sign]組態。

1. 開啟AEMWeb Console。 URL為`https://'[server]:[port]'/system/console/configMgr`
1. 開啟&#x200B;**[!UICONTROL Forms通用配置服務]。**
1. 在&#x200B;**[!UICONTROL 允許]**&#x200B;欄位中，**選擇**&#x200B;所有使用者——所有使用者（匿名或登入）都可預覽附件、驗證和簽署表格，然後按一下「儲存]」。**[!UICONTROL ** 作者例項已設定為使用 [!DNL Adobe Sign]。
1. 發佈設定。
1. 使用[replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html)在對應的發佈實例上建立相同的配置。

現在，[!DNL Adobe Sign]已與[!DNL Forms]整AEM合，並可用於最適化表單。 若要[以最適化表單](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)使用Adobe Sign服務，請以最適化表單屬性指定上述建立的組態容器。



## 設定[!DNL Adobe Sign]排程器以同步簽署狀態{#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Sign]啟用的最適化表單，必須在所有簽署者完成簽署程式後才會送出。 依預設，[!DNL Adobe Sign]排程器服務會排程在每24小時後檢查（輪詢）簽署者回應。 您可以更改環境的預設間隔。 執行以下步驟以更改預設間隔：

1. 使用管理員AEM憑證登入[!DNL Forms]伺服器，並導覽至&#x200B;**工具** > **[!UICONTROL 作業]** > **[!UICONTROL Web Console]**。

   您也可以在瀏覽器視窗中開啟下列URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到並開啟&#x200B;**[!UICONTROL Adobe Sign配置服務]**&#x200B;選項。 在&#x200B;**[!UICONTROL 狀態更新排程器運算式]**&#x200B;欄位中指定[cron運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression)，然後按一下&#x200B;**[!UICONTROL 儲存]**。 例如，要在上午00:00每天運行配置服務，請在&#x200B;**[!UICONTROL 狀態更新調度程式表達式]**&#x200B;欄位中指定`0 0 0 1/1 * ? *`。

[!DNL Adobe Sign]的同步狀態預設間隔現在已變更。

## 相關文章{#related-articles}

* [以最適化形式使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [使用Adobe Sign與AEM Forms（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)


