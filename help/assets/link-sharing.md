---
title: 使用連結共用資產
description: 以URL共用資產、資料夾和集合。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 5%

---

# 透過連結共用資產 {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] 可讓您與組織成員和外部實體（包括合作夥伴和廠商）以URL的形式共用資產、資料夾和集合。透過連結共用資產是讓外部使用者無須先登入[!DNL Assets]即可取得資源的便利方式。

>[!PREREQUISITES]
>
>* 您需要資料夾或要以連結形式共用的資產的編輯ACL權限。
>* 要向用戶發送電子郵件，請在[Day CQ Mail Service](#configmailservice)中配置SMTP伺服器詳細資訊。


## 共用資產 {#share-assets}

若要產生您要與使用者共用之資產的URL，請使用[!UICONTROL 連結共用]對話方塊。 具有管理員權限或在`/var/dam/share`位置具有讀取權限的用戶可以查看與他們共用的連結。

1. 在[!DNL Assets]使用者介面中，選取要以連結形式共用的資產。

1. 在工具列中，按一下&#x200B;**[!UICONTROL 共用連結]** ![共用資產圖示](assets/do-not-localize/assets_share.png)。 點擊&#x200B;**[!UICONTROL 共用]**&#x200B;後建立的連結會預先顯示在[!UICONTROL 共用連結]欄位中。 在您選擇&#x200B;**[!UICONTROL Submit]**&#x200B;之前，不會建立連結。

   ![與連結共用對話方塊](/help/assets/assets/share-assets-as-link.png)

   *圖：以連結形式共用資產的對話方塊。*

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。您可以新增一或多個使用者。

   >[!NOTE]
   >
   >如果您輸入非貴組織成員之使用者的電子郵件ID，字詞[!UICONTROL External User]會加上使用者的電子郵件ID前置詞。

1. 在&#x200B;**[!UICONTROL 主旨]**&#x200B;方塊中，輸入您要共用之資產的主旨。

1. 在&#x200B;**[!UICONTROL Message]**&#x200B;框中，輸入可選消息。

1. 在&#x200B;**[!UICONTROL 過期]**&#x200B;欄位中，指定連結停止運作的到期日和時間。 連結的預設過期時間為一天。

   ![設定共用連結的到期日](assets/Set-shared-link-expiration.png)

1. 若要讓使用者下載原始資產，請選取「**[!UICONTROL 允許下載原始檔案]**」。 若要讓使用者只下載共用資產的轉譯，請選取「**[!UICONTROL 允許下載檔案]**&#x200B;的轉譯」。

1. 按一下&#x200B;**[!UICONTROL 「共用」]**。訊息會確認連結已透過電子郵件與使用者共用。

1. 若要檢視共用資產，請按一下傳送給使用者之電子郵件中的連結。 若要產生資產的預覽，請按一下共用資產。 若要關閉預覽，請按一下&#x200B;**[!UICONTROL Back]**。 如果已共用資料夾，請按一下&#x200B;**[!UICONTROL 父資料夾]**&#x200B;以返回父資料夾。

   ![共用資產的預覽](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 僅支援產生所支援檔案類型 [的資產預覽](/help/assets/assets-formats.md)。如果共用其他MIME類型，則您只能下載資產且無法預覽。

1. 若要下載共用資產，請按一下工具列中的「**[!UICONTROL 選取]**」，按一下資產，然後從工具列按一下「**[!UICONTROL 下載]**」。

   ![下載共用資產的工具列選項](assets/chlimage_1-547.png)

1. 若要檢視已共用為連結的資產，請前往[!DNL Assets]使用者介面，然後按一下[!DNL Experience Manager]標誌。 選擇&#x200B;**[!UICONTROL 導航]**。 在「導覽」窗格中，選擇&#x200B;**[!UICONTROL 共用連結]**&#x200B;以顯示共用資產清單。

1. 若要取消共用資產，請選取資產，然後按一下工具列中的「**[!UICONTROL 取消共用]**」 。 之後會顯示確認訊息。 資產的項目會從清單中移除。

## 設定Day CQ郵件服務 {#configure-day-cq-mail-service}

1. 在[!DNL Experience Manager]首頁上，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 從服務清單中，找到&#x200B;**[!UICONTROL Day CQ Mail Service]**。
1. 按一下服務旁的&#x200B;**[!UICONTROL 編輯]**，並為&#x200B;**[!UICONTROL Day CQ Mail Service]**&#x200B;配置以下參數，並根據其名稱提及詳細資訊：

   * SMTP伺服器主機名：電子郵件伺服器主機名稱
   * SMTP伺服器埠：電子郵件伺服器埠
   * SMTP用戶：電子郵件伺服器使用者名稱
   * SMTP密碼：電子郵件伺服器密碼

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 按一下「**[!UICONTROL 儲存]**」。

## 配置最大資料大小 {#configure-maximum-data-size}

使用連結共用功能從共用的連結下載資產時，[!DNL Experience Manager]會從存放庫壓縮資產階層，然後以ZIP檔案傳回資產。 但是，在ZIP檔案中可壓縮的資料量沒有限制的情況下，會對大量資料進行壓縮，這會導致JVM記憶體不足錯誤。 為了保護系統免受因此情況而可能發生的拒絕服務攻擊，請使用Configuration Manager中&#x200B;**[!UICONTROL Max Content Size(uncompressed)]**&#x200B;參數的&#x200B;**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**&#x200B;來配置最大大小。 如果資產的未壓縮大小超過設定的值，資產下載請求就會遭到拒絕。 預設值為100 MB。

1. 按一下[!DNL Experience Manager]標誌，然後轉至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web控制台]**。
1. 在Web主控台中，找出&#x200B;**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**&#x200B;設定。
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM臨機資產共用代理Servlet]** 」設定，並修改「最大內容大小 (未壓縮) 」 **[!UICONTROL 參數的值]** 。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 儲存變更。

## 最佳實務和疑難排解 {#best-practices-and-troubleshooting}

* 資產資料夾或名稱中包含空白字元的集合可能無法共用。
* 如果使用者無法下載共用資產，請洽詢您的[!DNL Experience Manager]管理員[下載限制](#configure-maximum-data-size)是什麼。
* 如果您無法傳送包含共用資產連結的電子郵件，或如果其他使用者無法收到您的電子郵件，請洽詢您的[!DNL Experience Manager]管理員，確認是否已設定[電子郵件服務](#configure-day-cq-mail-service)。
* 如果您無法使用連結共用功能來共用資產，請確定您擁有適當的權限。 請參閱[共用資產](#share-assets)。
* 如果共用資產移至不同位置，其連結會停止運作。 重新建立連結並重新與使用者共用。

* 如果您想要將[!DNL Experience Manager]製作部署的連結共用給外部實體，請務必僅針對`GET`請求公開用於連結共用的下列URL。 基於安全原因封鎖其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   在[!DNL Experience Manager]介面中，訪問&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web控制台]**。 開啟&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置，並在&#x200B;**[!UICONTROL Domains]**&#x200B;欄位中修改以下屬性，並針對`local`、`author`和`publish`提及值。 針對`local`和`author`屬性，分別提供本機和Author例項的URL。 如果您執行單一[!DNL Experience Manager]製作例項，請對`local`和`author`屬性使用相同的值。 若為發佈例項，請提供[!DNL Experience Manager]發佈例項的URL。
