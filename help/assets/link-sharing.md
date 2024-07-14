---
title: 使用連結共用資產
description: 以URL形式共用資產、資料夾和集合。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 7%

---

# 以連結形式共用資產 {#asset-link-sharing}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager Assets]可讓您以URL的形式與組織成員和外部實體（包括合作夥伴和廠商）共用資產、資料夾和集合。 透過連結共用資產是一種便利的方法，讓外部對象無需先登入[!DNL Assets]即可使用資源。

>[!PREREQUISITES]
>
>* 您需要`Edit ACL`許可權，才能存取您要以連結形式共用的資料夾或資產。
>* 若要傳送電子郵件給使用者，請在[天CQ郵件服務](#configmailservice)中設定SMTP伺服器詳細資料。

## 共用資產 {#share-assets}

若要產生您要與使用者共用之資產的URL，請使用[!UICONTROL 連結共用]對話方塊。

* 具有管理員許可權或在`/var/dam/share`位置具有讀取許可權的使用者可以檢視與他們共用的連結。
* 在`/var/dam/jobs/download`位置擁有讀取許可權的使用者可以從共用連結下載資產。

1. 在[!DNL Assets]使用者介面中，選取要共用作為連結的資產。

1. 在工具列中按一下&#x200B;**[!UICONTROL 共用連結]** ![共用資產圖示](assets/do-not-localize/assets_share.png)。 按一下&#x200B;**[!UICONTROL 共用]**&#x200B;後建立的連結會預先顯示在[!UICONTROL 共用連結]欄位中。 除非您選取&#x200B;**[!UICONTROL 提交]**，否則不會建立連結。

   ![與連結共用的對話方塊](assets/share-assets-as-link.png)

   *圖：要以連結形式共用資產的對話方塊。*

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。您可以新增一或多個使用者。

   >[!NOTE]
   >
   >如果您輸入的使用者電子郵件識別碼不是您組織的成員，則字詞[!UICONTROL 外部使用者]會以使用者的電子郵件識別碼為前置詞。

1. 在&#x200B;**[!UICONTROL 主旨]**&#x200B;方塊中，輸入您要共用之資產的主旨。

1. 在&#x200B;**[!UICONTROL 訊息]**&#x200B;方塊中，輸入選擇性訊息。

1. 在&#x200B;**[!UICONTROL 過期]**&#x200B;欄位中，指定連結停止運作的過期日期和時間。 連結的預設到期時間為一天。

   ![設定共用連結的到期日](assets/Set-shared-link-expiration.png)

1. 若要讓使用者下載原始資產，請選取&#x200B;**[!UICONTROL 允許下載原始檔案]**。 若要讓使用者僅下載共用資產的轉譯，請選取&#x200B;**[!UICONTROL 允許下載檔案的轉譯]**。

1. 按一下&#x200B;**[!UICONTROL 共用]**。 系統會顯示訊息，確認會透過電子郵件將連結分享給使用者。

1. 若要檢視共用資產，請按一下傳送給使用者之電子郵件中的連結。 若要產生資產的預覽，請按一下共用資產。 若要關閉預覽，請按一下[上一步]。**** 如果您已共用資料夾，請按一下&#x200B;**[!UICONTROL 父資料夾]**&#x200B;以返回父資料夾。

   ![共用資產預覽](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager]僅支援產生[受支援檔案型別](/help/assets/assets-formats.md)的資產預覽。 如果其他MIME型別已共用，您只能下載資產且無法預覽。

1. 若要下載共用資產，請按一下工具列中的&#x200B;**[!UICONTROL 選取]**、按一下資產，然後按一下工具列中的&#x200B;**[!UICONTROL 下載]**。

   ![下載共用資產的工具列選項](assets/chlimage_1-547.png)

1. 若要檢視您以連結形式共用的資產，請前往[!DNL Assets]使用者介面並按一下[!DNL Experience Manager]標誌。 選擇&#x200B;**[!UICONTROL 導覽]**。 在[導覽]窗格中，選擇&#x200B;**[!UICONTROL 共用連結]**&#x200B;以顯示共用資產清單。

1. 若要取消共用資產，請選取該資產，然後按一下工具列中的[取消共用]。**** 隨後會顯示確認訊息。 資產的專案會從清單中移除。

## 設定Day CQ郵件服務 {#configure-day-cq-mail-service}

1. 在[!DNL Experience Manager]首頁上，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。
1. 從服務清單中找出&#x200B;**[!UICONTROL Day CQ Mail Service]**。
1. 按一下服務旁的&#x200B;**[!UICONTROL 編輯]**，並設定&#x200B;**[!UICONTROL Day CQ Mail Service]**&#x200B;的下列引數，並針對其名稱提及詳細資料：

   * smtp伺服器主機名稱：電子郵件伺服器主機名稱
   * SMTP伺服器連線埠：電子郵件伺服器連線埠
   * SMTP使用者：電子郵件伺服器使用者名稱
   * SMTP密碼：電子郵件伺服器密碼

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 按一下「**[!UICONTROL 儲存]**」。

## 設定資料大小上限 {#configure-maximum-data-size}

當您從使用連結共用功能的連結下載資產時，[!DNL Experience Manager]會從存放庫壓縮資產階層，然後以ZIP檔案傳回資產。 但是，由於沒有可壓縮至ZIP檔案的資料量限制，因此大量資料會遭到壓縮，導致JVM出現記憶體不足錯誤。 若要保護系統免受因此情況而導致的潛在拒絕服務攻擊，請在Configuration Manager中使用&#x200B;**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**&#x200B;的&#x200B;**[!UICONTROL Max Content Size （未壓縮）]**&#x200B;引數設定大小上限。 如果資產的未壓縮大小超過設定值，則會拒絕資產下載請求。 預設值為100 MB。

1. 按一下[!DNL Experience Manager]標誌，然後移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。
1. 在Web主控台中，找出&#x200B;**[!UICONTROL Day CQ DAM臨機資產共用代理Servlet]**&#x200B;設定。
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM臨機資產共用代理Servlet]** 」設定，並修改「最大內容大小 (未壓縮) 」 **[!UICONTROL 參數的值]** 。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 儲存變更。

## 最佳作法和疑難排解 {#best-practices-and-troubleshooting}

* 名稱中包含空白字元的資產資料夾或集合可能無法共用。
* 如果使用者無法下載共用的資產，請向您的[!DNL Experience Manager]管理員查詢[下載限制](#configure-maximum-data-size)為何。
* 如果您無法傳送包含共用資產連結的電子郵件，或其他使用者無法收到您的電子郵件，請向您的[!DNL Experience Manager]管理員確認是否已設定[電子郵件服務](#configure-day-cq-mail-service)。
* 如果您無法使用連結共用功能來共用資產，請確定您擁有適當的許可權。 請參閱[共用資產](#share-assets)。
* 如果共用資產移至其他位置，其連結會停止運作。 重新建立連結，並與使用者重新共用。

* 如果您想要將[!DNL Experience Manager]作者部署中的連結分享至外部實體，請確定您僅公開`GET`要求中用於連結分享的下列URL。 基於安全考量封鎖其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  在[!DNL Experience Manager]介面中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。 開啟&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;設定，並修改&#x200B;**[!UICONTROL 網域]**&#x200B;欄位中的下列屬性，其中含有針對`local`、`author`和`publish`提及的值。 針對`local`和`author`屬性，請分別提供本機和作者執行個體的URL。 如果您執行單一[!DNL Experience Manager]作者執行個體，請對`local`和`author`屬性使用相同的值。 針對Publish執行個體，請提供[!DNL Experience Manager] Publish執行個體的URL。
