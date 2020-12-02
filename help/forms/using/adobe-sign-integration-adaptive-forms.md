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
source-git-commit: f0038c1f88ea0047cbaae4fe49456a665aa67f10
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---


# 將Adobe Sign與AEM Forms整合{#integrate-adobe-sign-with-aem-forms}

Adobe Sign可針對最適化表單啟用電子簽名工作流程。 電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在典型的Adobe Sign和最適化表單案例中，使用者會填入最適化表單以申請服務&#x200B;**。**&#x200B;例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，表格會傳送給服務提供者，以做進一步的動作。 服務供應商會審核應用程式，並使用Adobe Sign來標示已核准的應用程式。 若要啟用類似的電子簽名工作流程，您可以將Adobe Sign與AEM Forms整合。

若要搭配AEM Forms使用Adobe Sign，請在AEM Cloud Services中設定Adobe Sign:

## 必備條件 {#prerequisites}

您需要下列項目才能將Adobe Sign與AEM Forms整合：

* 有效[Adobe Sign開發人員帳戶。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* [啟用SSL](/help/sites-administering/ssl-by-default.md) AEM Forms伺服器。
* [Adobe Sign API應用程式](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* Adobe Sign API應用程式的認證（用戶端ID和用戶端密碼）。
* 重新設定時，請從作者和發佈例項中移除現有的Adobe Sign設定。
* 對於作者和發佈實例，請使用[相同的加密密鑰](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 使用AEM Forms {#configure-adobe-sign-with-aem-forms}設定Adobe Sign

在具備必要條件後，請執行下列步驟，在「作者」例項上以AEM Forms設定Adobe Sign:

1. 在AEM Forms作者例項中，導覽至「工具&#x200B;****![hammer](assets/hammer.png) > **一般** >配置瀏覽器&#x200B;**」。**
1. 在&#x200B;**[!UICONTROL 配置瀏覽器]**&#x200B;頁面上，點選&#x200B;**[!UICONTROL 建立]**。
   * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定設定的&#x200B;**[!UICONTROL 標題]**，啟用&#x200B;**[!UICONTROL 雲端設定]**，然後點選&#x200B;**[!UICONTROL 建立]**。 它會為雲端服務建立組態容器。
1. 導覽至&#x200B;**工具**![ hammer](assets/hammer.png) > **雲端服務** > **Adobe Sign**，然後選取您在上述步驟中建立的設定容器。

   >[!NOTE]
   >
   >您可以執行步驟1-4以建立新的設定容器並在容器中建立Adobe Sign設定，或使用&#x200B;**Tools** ![hammer](assets/hammer.png) > **Cloud Services** > **Adobe Sign**&#x200B;中的現有`global`資料夾。 如果您在新配置容器中建立配置，請確保在建立自適應表單時在&#x200B;**[!UICONTROL 配置容器]**&#x200B;欄位中指定容器名稱。

   >[!NOTE]
   請確定雲端服務設定頁面的URL以&#x200B;**HTTPS**&#x200B;開頭。 如果沒有，請為AEM Forms伺服器啟用SSL](/help/sites-administering/ssl-by-default.md)。[

1. 在設定頁面上，點選&#x200B;**[!UICONTROL Create]**&#x200B;以在AEM Forms中建立Adobe Sign設定。
1. 在&#x200B;**[!UICONTROL 「建立Adobe Sign Configuration]**」頁面的&#x200B;**[!UICONTROL 「一般]**」標籤中，指定設定的&#x200B;**名稱**，然後點選&#x200B;**Next**。 您可以選擇指定標題並瀏覽以選取設定的縮圖。

1. 將您目前瀏覽器視窗中的URL複製至記事本。 您必須使用AEM Forms來設定Adobe Sign應用程式。

1. 設定Adobe Sign應用程式的OAuth設定：

   1. 開啟瀏覽器視窗並登入Adobe Sign開發人員帳戶。
   1. 選取為AEM Forms設定的應用程式，然後點選「設定應用程式的OAuth」。
   1. 在&#x200B;**重新導向URL**&#x200B;方塊中，新增在上一步驟中複製的HTTPS URL，然後按一下「儲存&#x200B;**a3/>」。**
   1. 為Adobe Sign應用程式啟用下列OAuth設定，然後按一下「儲存」。****
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   如需設定Adobe Sign應用程式的OAuth設定並取得索引鍵的逐步資訊，請參閱[設定應用程式的oAuth設定](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)開發人員檔案。

   ![OAuth設定](assets/oauthconfig_new.png)

1. 返回&#x200B;**「建立Adobe Sign Configuration**」頁面。 在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中，**[!UICONTROL OAuth URL]**&#x200B;欄位提及下列預設URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1** 是指預設資料庫共用。

   您可以修改資料庫共用的值。 重新啟動伺服器，以便能夠為資料庫共用使用新值。

1. 指定&#x200B;**客戶端ID**（也稱為應用程式ID）和&#x200B;**客戶端密碼**。 選擇&#x200B;**「同時**&#x200B;啟用附件的Adobe Sign」選項，將附加至最適化表單的檔案附加至要傳送以進行簽署的對應Adobe Sign檔案。

   點選「**[!UICONTROL 連線至Adobe Sign]**」。 當提示輸入認證時，請提供建立Adobe Sign應用程式時所使用之帳戶的使用者名稱和密碼。

   點選「**[!UICONTROL 建立]**」以建立Adobe Sign組態。

1. 開啟AEM Web Console。 URL為`https://'[server]:[port]'/system/console/configMgr`
1. 開啟&#x200B;**表單通用配置服務。**
1. 在&#x200B;**允許**&#x200B;欄位中，**選擇**&#x200B;所有使用者——所有使用者（匿名或登入）都可預覽附件、驗證和簽署表格，然後按一下「儲存」。**** 作者例項已設定為使用Adobe Sign。
1. 發佈設定。
1. 使用[replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html)在對應的發佈實例上建立相同的配置。

現在，Adobe Sign已與AEM Forms整合，可在最適化表單中使用。 若要[以最適化表單](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)使用Adobe Sign服務，請以最適化表單屬性指定上述建立的組態容器。



## 設定Adobe Sign排程器以同步簽署狀態{#configure-adobe-sign-scheduler-to-sync-the-signing-status}

只有在所有簽署者完成簽署程式後，才會提交啟用Adobe Sign的調適性表單。 依預設，Adobe Sign Scheduler服務會排程在每24小時後檢查（民調問答）簽署者回應。 您可以更改環境的預設間隔。 執行以下步驟以更改預設間隔：

1. 使用管理員認證登入AEM Forms伺服器，並導覽至「工具&#x200B;**** > **作業** > **Web Console**」。

   您也可以在瀏覽器視窗中開啟下列URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到並開啟&#x200B;**Adobe Sign Configuration Service**&#x200B;選項。 在&#x200B;**狀態更新排程器運算式**&#x200B;欄位中指定[cron運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression)，然後按一下&#x200B;**儲存**。 例如，要在上午00:00每天運行配置服務，請在&#x200B;**狀態更新調度程式表達式**&#x200B;欄位中指定`0 0 0 1/1 * ? *`。

Adobe Sign的同步狀態預設間隔現在已變更。

## 相關文章{#related-articles}

* [在最適化表單中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [搭配AEM Forms（視訊）使用Adobe Sign](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)

