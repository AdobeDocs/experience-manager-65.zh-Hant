---
title: 使用連結共用資產
description: 以URL形式共用資產、資料夾和集合。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 6%

---

# 以連結形式共用資產 {#asset-link-sharing}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager Assets] 可讓您和組織成員及外部實體（包括合作夥伴和廠商）以URL形式共用資產、資料夾和集合。 透過連結共用資產是一種便利的方式，讓外部對象無需先登入即可使用資源 [!DNL Assets].

>[!PREREQUISITES]
>
>* 您需要 `Edit ACL` 您要共用作為連結的資料夾或資產的許可權。
>* 若要傳送電子郵件給使用者，請在中設定SMTP伺服器詳細資訊 [Day CQ郵件服務](#configmailservice).

## 共用資產 {#share-assets}

若要產生您要與使用者共用之資產的URL，請使用 [!UICONTROL 連結共用] 對話方塊。

* 具有管理員許可權或讀取許可權的使用者位於 `/var/dam/share` 位置可檢視與其共用的連結。
* 擁有讀取許可權的使用者： `/var/dam/jobs/download` 位置可從共用連結下載資產。

1. 在 [!DNL Assets] 使用者介面，選取要以連結形式共用的資產。

1. 在工具列中按一下 **[!UICONTROL 共用連結]** ![共用資產圖示](assets/do-not-localize/assets_share.png). 按一下後建立的連結 **[!UICONTROL 共用]** 會預先顯示在 [!UICONTROL 共用連結] 欄位。 在您選取之前，不會建立連結 **[!UICONTROL 提交]**.

   ![具有連結共用的對話方塊](assets/share-assets-as-link.png)

   *圖：以連結形式共用資產的對話方塊。*

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。您可以新增一或多個使用者。

   >[!NOTE]
   >
   >如果您輸入的使用者電子郵件識別碼不是您組織的成員，則您輸入的文字 [!UICONTROL 外部使用者] 都會以使用者的電子郵件ID為前置詞。

1. 在 **[!UICONTROL 主旨]** 方塊中，輸入您要共用之資產的主旨。

1. 在 **[!UICONTROL 訊息]** 方塊中，輸入選填訊息。

1. 在 **[!UICONTROL 有效期]** 欄位中，指定連結停止運作的到期日與時間。 連結的預設到期時間為一天。

   ![設定共用連結的到期日](assets/Set-shared-link-expiration.png)

1. 若要讓使用者下載原始資產，請選取 **[!UICONTROL 允許下載原始檔案]**. 若要讓使用者僅下載共用資產的轉譯，請選取 **[!UICONTROL 允許下載檔案轉譯]**.

1. 按一下 **[!UICONTROL 共用]**. 訊息會確認透過電子郵件與使用者共用連結。

1. 若要檢視共用資產，請按一下傳送給使用者之電子郵件中的連結。 若要產生資產的預覽，請按一下共用資產。 若要關閉預覽，請按一下 **[!UICONTROL 返回]**. 如果您已共用資料夾，請按一下 **[!UICONTROL 父資料夾]** 以返回父資料夾。

   ![共用資產預覽](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 僅支援產生的資產預覽 [支援的檔案型別](/help/assets/assets-formats.md). 如果其他MIME型別已共用，您只能下載資產且無法預覽。

1. 若要下載共用資產，請按一下 **[!UICONTROL 選取]** 在工具列中按一下資產，然後按一下 **[!UICONTROL 下載]** 工具列中的。

   ![下載共用資產的工具列選項](assets/chlimage_1-547.png)

1. 若要檢視您以連結形式共用的資產，請前往 [!DNL Assets] 使用者介面，然後按一下 [!DNL Experience Manager] 標誌。 選擇 **[!UICONTROL 導覽]**. 在「導覽」窗格中，選擇 **[!UICONTROL 共用的連結]** 以顯示共用資產清單。

1. 若要取消共用資產，請選取該資產，然後按一下 **[!UICONTROL 取消共用]** 工具列中的。 隨後會顯示確認訊息。 資產的專案會從清單中移除。

## 設定Day CQ郵件服務 {#configure-day-cq-mail-service}

1. 在 [!DNL Experience Manager] 首頁，瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
1. 從服務清單中，找出 **[!UICONTROL Day CQ郵件服務]**.
1. 按一下 **[!UICONTROL 編輯]** 並設定下列引數，用於 **[!UICONTROL Day CQ郵件服務]** 詳細資訊將對照其名稱提及：

   * smtp伺服器主機名稱：電子郵件伺服器主機名稱
   * SMTP伺服器連線埠：電子郵件伺服器連線埠
   * SMTP使用者：電子郵件伺服器使用者名稱
   * SMTP密碼：電子郵件伺服器密碼

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 按一下「**[!UICONTROL 儲存]**」。

## 設定資料大小上限 {#configure-maximum-data-size}

當您從使用連結共用功能的連結下載資產時， [!DNL Experience Manager] 從存放庫壓縮資產階層，然後以ZIP檔案傳回資產。 但是，由於沒有可壓縮至ZIP檔案的資料量限制，因此大量資料會遭到壓縮，導致JVM出現記憶體不足錯誤。 若要保護系統免受由於此狀況而導致的拒絕服務攻擊，請使用 **[!UICONTROL 最大內容大小（未壓縮）]** 的引數 **[!UICONTROL Day CQ DAM臨機資產共用代理Servlet]** 在Configuration Manager中。 如果資產的未壓縮大小超過設定值，則會拒絕資產下載請求。 預設值為100 MB。

1. 按一下 [!DNL Experience Manager] 標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
1. 在Web主控台中，找到 **[!UICONTROL Day CQ DAM臨機資產共用代理Servlet]** 設定。
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM臨機資產共用代理Servlet]** 」設定，並修改「最大內容大小 (未壓縮) 」 **[!UICONTROL 參數的值]** 。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 儲存變更。

## 最佳作法和疑難排解 {#best-practices-and-troubleshooting}

* 名稱中包含空白字元的資產資料夾或集合可能無法共用。
* 如果使用者無法下載共用的資產，請洽詢您的 [!DNL Experience Manager] 管理員什麼 [下載限制](#configure-maximum-data-size) 是。
* 如果您無法傳送包含共用資產連結的電子郵件，或其他使用者無法收到您的電子郵件，請洽詢您的 [!DNL Experience Manager] 管理員，如果 [電子郵件服務](#configure-day-cq-mail-service) 是否已設定。
* 如果您無法使用連結共用功能來共用資產，請確定您擁有適當的許可權。 另請參閱 [共用資產](#share-assets).
* 如果共用資產移至其他位置，其連結會停止運作。 重新建立連結，並與使用者重新共用。

* 如果您想要共用您網站的連結 [!DNL Experience Manager] 將作者部署至外部實體，請確保您僅公開以下用於連結共用的URL，例如 `GET` 僅請求。 基於安全考量封鎖其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  在 [!DNL Experience Manager] 介面，存取 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**. 開啟 **[!UICONTROL Day CQ連結外部化器]** 設定並修改中的下列屬性 **[!UICONTROL 網域]** 具有提及值的欄位 `local`， `author`、和 `publish`. 對於 `local` 和 `author` 屬性，分別提供本機和作者執行個體的URL。 如果您執行單一 [!DNL Experience Manager] 編寫執行個體，將相同的值用於 `local` 和 `author` 屬性。 對於發佈執行個體，提供 [!DNL Experience Manager] 發佈執行個體。
