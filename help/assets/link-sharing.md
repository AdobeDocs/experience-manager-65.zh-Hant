---
title: 使用連結分享資產
description: 將資產、檔案夾和系列共用為URL。
contentOwner: AG
role: 業務從業人員
feature: 連結共用，資產管理
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 5%

---


# 透過連結{#asset-link-sharing}共用資產

[!DNL Adobe Experience Manager Assets] 可讓您與組織成員和外部實體（包括合作夥伴和廠商）以URL形式共用資產、檔案夾和系列。透過連結分享資產是讓外部使用者可使用資源的便利方式，而不需要先登入[!DNL Assets]。

>[!PREREQUISITES]
>
>* 您需要對要作為連結共用的資料夾或資產具有編輯ACL權限。
>* 要向用戶發送電子郵件，請在[Day CQ Mail Service](#configmailservice)中配置SMTP伺服器詳細資訊。


## 共用資產 {#sharelink}

若要產生您要與使用者共用之資產的URL，請使用「連結共用」對話方塊。 具有管理員權限或在`/var/dam/share`位置具有讀取權限的用戶可以查看與他們共用的連結。

1. 在[!DNL Assets]使用者介面中，選取要以連結形式共用的資產。
1. 在工具列中，按一下「共用連結&#x200B;**** ![共用資產」圖示](assets/do-not-localize/assets_share.png)。

   按一下[!UICONTROL Share]後將建立的連結會提前顯示在[!UICONTROL Share Link]欄位中。 連結的預設有效期為一天。

   ![與連結共用對話方塊](assets/Link-sharing-dialog-box.png)

   *圖：將資產共用為連結的對話方塊。*

   >[!NOTE]
   >
   >如果您想要將[!DNL Experience Manager]作者部署的連結共用給外部實體，請確定您只針對`GET`請求公開下列URL（用於連結共用）。 出於安全原因，封鎖其他URL。
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. 在[!DNL Experience Manager]介面中，訪問&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。

1. 開啟&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置，並在&#x200B;**[!UICONTROL Domains]**&#x200B;欄位中修改以下屬性，其值針對`local`、`author`和`publish`提及。 對於`local`和`author`屬性，請分別提供本機實例和作者實例的URL。 如果運行單個[!DNL Experience Manager]作者實例，`local`和`author`屬性的值都相同。 對於「發佈」例項，請提供[!DNL Experience Manager]發佈例項的URL。

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。您可以新增一或多個使用者。

   ![直接從「連結共用」對話方塊分享資產連結](assets/Asset-Sharing-LinkShareDialog.png)

   *圖：直接從「連結共用」對話方 [!UICONTROL 塊共用] 資產連結。*

   >[!NOTE]
   >
   >如果您輸入非您組織成員之使用者的電子郵件ID，則「外部使用者」([!UICONTROL External User)]會加上使用者的電子郵件ID前置詞。

1. 在&#x200B;**[!UICONTROL Subject]**&#x200B;方塊中，輸入您要共用之資產的主旨。

1. 在&#x200B;**[!UICONTROL 消息]**&#x200B;框中，輸入可選消息。

1. 在&#x200B;**[!UICONTROL Expiration]**&#x200B;欄位中，指定連結停止運作的到期日和時間。 依預設，有效期是從您共用連結之日起的一週設定。

   ![設定共用連結的到期日](assets/Set-shared-link-expiration.png)

1. 若要讓使用者下載原始資產以及轉譯，請選取「允許下載原始檔案」**[!UICONTROL 。]**&#x200B;依預設，使用者只能下載您以連結形式共用之資產的轉譯。

1. 按一下&#x200B;**[!UICONTROL 「共用」]**。訊息會確認連結已透過電子郵件與使用者共用。

1. 若要檢視共用資產，請按一下傳送給使用者之電子郵件中的連結。 共用資產會顯示在[!UICONTROL Adobe Marketing Cloud]頁面中。

   ![共用資產可在Adobe Marketing Cloud使用](assets/chlimage_1-545.png)

1. 若要產生資產的預覽，請按一下共用資產。 要關閉預覽並返回至&#x200B;**[!UICONTROL Marketing Cloud]**&#x200B;頁面，請按一下工具欄中的&#x200B;**[!UICONTROL 上一步]**。 如果您已共用資料夾，請按一下「父資料夾&#x200B;****」以返回父資料夾。

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 支援僅產生支援之檔案類 [型之資產的預覽](/help/assets/assets-formats.md)。如果共用其他MIME類型，則只能下載資產，無法預覽。

1. 若要下載共用資產，請按一下工具列中的「選擇&#x200B;****」、按一下資產，然後按一下工具列中的「下載&#x200B;****」。

   ![下載共用資產的工具列選項](assets/chlimage_1-547.png)

1. 若要檢視您已共用為連結的資產，請前往[!DNL Assets]使用者介面，然後按一下[!DNL Experience Manager]標誌。 選擇&#x200B;**[!UICONTROL Navigation]**。 在導覽窗格中，選擇&#x200B;**[!UICONTROL 共用連結]**&#x200B;以顯示共用資產清單。

1. 若要取消共用資產，請選取資產，然後從工具列按一下「取消共用&#x200B;****」。 之後會出現確認訊息。 資產的項目會從清單中移除。

## 配置Day CQ Mail Service {#configmailservice}

1. 在[!DNL Experience Manager]首頁上，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 從服務清單中，找到&#x200B;**[!UICONTROL Day CQ Mail Service]**。
1. 按一下服務旁邊的&#x200B;**[!UICONTROL Edit]** ，並為&#x200B;**[!UICONTROL Day CQ Mail Service]**&#x200B;配置以下參數，並根據其名稱提及詳細資訊：

   * SMTP伺服器主機名：電子郵件伺服器主機名
   * SMTP伺服器埠：電子郵件伺服器端
   * SMTP用戶：電子郵件伺服器使用者名稱
   * SMTP密碼：電子郵件伺服器密碼

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 按一下「**[!UICONTROL 儲存]**」。

## 配置最大資料大小{#maxdatasize}

當您使用「連結共用」功能從共用的連結下載資產時，[!DNL Experience Manager]會從儲存庫壓縮資產階層，然後以ZIP檔案傳回資產。 但是，在ZIP檔案中壓縮的資料量沒有限制的情況下，大量資料會遭受壓縮，造成JVM中記憶體錯誤。 要防止系統因此遭受潛在的拒絕服務攻擊，請使用Configuration Manager中[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]的&#x200B;**[!UICONTROL Max Content Size（未壓縮）]**&#x200B;參數配置最大大小。 如果資產的未壓縮大小超過設定的值，資產下載請求便會遭拒。 預設值為100 MB。

1. 按一下[!DNL Experience Manager]徽標，然後轉到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在Web控制台中，找到&#x200B;**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**&#x200B;配置。
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM臨機資產共用代理Servlet]** 」設定，並修改「最大內容大小 (未壓縮) 」 **[!UICONTROL 參數的值]** 。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 儲存變更。

## 最佳實務與疑難排解{#bestpractices}

* 資產檔案夾或名稱中包含空白字元的系列可能無法共用。
* 如果使用者無法下載共用資產，請洽詢您的[!DNL Experience Manager]管理員[下載限制](#maxdatasize)是什麼。
* 如果您無法傳送含有共用資產連結的電子郵件，或如果其他使用者無法收到您的電子郵件，請洽詢您的[!DNL Experience Manager]管理員，以瞭解[電子郵件服務是否已設定。](#configmailservice)
* 如果您無法使用連結共用功能來共用資產，請確定您擁有適當的權限。 請參閱[共用資產](#sharelink)。
* 如果共用資產移至不同位置，其連結將停止運作。 重新建立連結並與使用者重新共用。
