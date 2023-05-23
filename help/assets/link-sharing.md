---
title: 使用連結共用資產
description: 以URL形式共用資產、資料夾和集合。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 6%

---

# 將資產作為連結共用 {#asset-link-sharing}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 允許您與組織成員和外部實體（包括合作夥伴和供應商）以URL形式共用資產、資料夾和集合。 通過連結共用資產是一種方便的方式，使外部各方無需首先登錄即可獲得資源 [!DNL Assets]。

>[!PREREQUISITES]
>
>* 您需要 `Edit ACL` 對要作為連結共用的資料夾或資產的權限。
>* 要向用戶發送電子郵件，請在中配置SMTP伺服器詳細資訊 [第CQ天郵件服務](#configmailservice)。


## 共用資產 {#share-assets}

要為要與用戶共用的資產生成URL，請使用 [!UICONTROL 連結共用] 對話框。

* 具有管理員權限或具有讀取權限的用戶 `/var/dam/share` 位置可以查看與它們共用的連結。
* 具有讀取權限的用戶 `/var/dam/jobs/download` 位置可以從共用連結下載資產。

1. 在 [!DNL Assets] 用戶介面，選擇要作為連結共用的資產。

1. 在工具欄中，按一下 **[!UICONTROL 共用連結]** ![共用資產表徵圖](assets/do-not-localize/assets_share.png)。 按一下後將建立的連結 **[!UICONTROL 共用]** 在 [!UICONTROL 共用連結] 的子菜單。 在您選擇之前不會建立連結 **[!UICONTROL 提交]**。

   ![與連結共用對話](assets/share-assets-as-link.png)

   *圖：將資產作為連結共用的對話框。*

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。您可以添加一個或多個用戶。

   >[!NOTE]
   >
   >如果您輸入了非您組織成員的用戶的電子郵件ID，則 [!UICONTROL 外部用戶] 前置詞為用戶的電子郵件ID。

1. 在 **[!UICONTROL 主題]** 框中，輸入要共用的資產的主題。

1. 在 **[!UICONTROL 消息]** 框中，輸入可選消息。

1. 在 **[!UICONTROL 到期]** 欄位，指定連結停止工作的到期日期和時間。 連結的預設過期時間為一天。

   ![設定共用連結的到期日期](assets/Set-shared-link-expiration.png)

1. 要允許用戶下載原始資產，請選擇 **[!UICONTROL 允許下載原始檔案]**。 要允許用戶僅下載共用資產的格式副本，請選擇 **[!UICONTROL 允許下載檔案的格式副本]**。

1. 按一下 **[!UICONTROL 共用]**。 一條消息確認該連結通過電子郵件與用戶共用。

1. 要查看共用資產，請按一下發送到用戶的電子郵件中的連結。 要生成資產預覽，請按一下共用資產。 要關閉預覽，請按一下 **[!UICONTROL 後退]**。 如果已共用資料夾，請按一下 **[!UICONTROL 父資料夾]** 的子菜單。

   ![共用資產預覽](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 支援僅生成資產預覽 [支援的檔案類型](/help/assets/assets-formats.md)。 如果共用其他MIME類型，則只能下載資產，無法預覽。

1. 要下載共用資產，請按一下 **[!UICONTROL 選擇]** 在工具欄上，按一下資產，然後 **[!UICONTROL 下載]** 的子菜單。

   ![下載共用資產的工具欄選項](assets/chlimage_1-547.png)

1. 要查看已作為連結共用的資產，請轉到 [!DNL Assets] 用戶介面，然後按一下 [!DNL Experience Manager] 徽標。 選擇 **[!UICONTROL 導航]**。 在導航窗格中，選擇 **[!UICONTROL 共用連結]** 顯示共用資產清單。

1. 要取消共用資產，請選擇該資產並按一下 **[!UICONTROL 取消共用]** 的子菜單。 隨後將顯示確認消息。 資產的條目將從清單中刪除。

## 配置第一天CQ郵件服務 {#configure-day-cq-mail-service}

1. 在 [!DNL Experience Manager] 首頁，導航 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 從服務清單中，找到 **[!UICONTROL 第CQ天郵件服務]**。
1. 按一下 **[!UICONTROL 編輯]** 在服務旁邊，並為 **[!UICONTROL 第CQ天郵件服務]** 詳細資訊與他們的姓名相對照：

   * SMTP伺服器主機名：電子郵件伺服器主機名
   * SMTP伺服器埠：電子郵件伺服器埠
   * SMTP用戶：電子郵件伺服器用戶名
   * SMTP密碼：電子郵件伺服器密碼

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 按一下「**[!UICONTROL 儲存]**」。

## 配置最大資料大小 {#configure-maximum-data-size}

使用「連結共用」功能從共用的連結下載資產時， [!DNL Experience Manager] 從儲存庫壓縮資產層次結構，然後以ZIP檔案返回資產。 但是，在對ZIP檔案中可壓縮的資料量沒有限制的情況下，大量資料會受到壓縮，這會導致JVM中記憶體不足錯誤。 要保護系統免受由於此情況而可能發生的拒絕服務攻擊，請使用 **[!UICONTROL 最大內容大小（未壓縮）]** 參數 **[!UICONTROL 第CQ天DAM臨時資產共用代理Servlet]** 中。 如果資產的未壓縮大小超過配置值，則資產下載請求被拒絕。 預設值為100 MB。

1. 按一下 [!DNL Experience Manager] 標識，然後 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在Web控制台中，找到 **[!UICONTROL 第CQ天DAM臨時資產共用代理Servlet]** 配置。
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM臨機資產共用代理Servlet]** 」設定，並修改「最大內容大小 (未壓縮) 」 **[!UICONTROL 參數的值]** 。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 儲存變更。

## 最佳實踐和故障排除 {#best-practices-and-troubleshooting}

* 名稱中包含空白的資產資料夾或集合可能無法共用。
* 如果用戶無法下載共用資產，請與 [!DNL Experience Manager] 管理員 [下載限制](#configure-maximum-data-size) 。
* 如果您無法發送電子郵件，並且其連結指向共用資產，或者其他用戶無法接收您的電子郵件，請與您的 [!DNL Experience Manager] 的 [電子郵件服務](#configure-day-cq-mail-service) 是否已配置。
* 如果無法使用連結共用功能共用資產，請確保您具有相應的權限。 請參閱 [資產](#share-assets)。
* 如果共用資產被移動到其他位置，則其連結將停止工作。 重新建立連結並與用戶重新共用。

* 如果要共用來自 [!DNL Experience Manager] 將部署作為外部實體，確保僅公開下列用於連結共用的URL, `GET` 僅請求。 出於安全原因阻止其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   在 [!DNL Experience Manager] 介面，訪問 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 開啟 **[!UICONTROL 第CQ天連結外部化程式]** 配置並修改 **[!UICONTROL 域]** 欄位中所引用的值 `local`。 `author`, `publish`。 對於 `local` 和 `author` 屬性，分別提供本地實例和作者實例的URL。 如果你運行 [!DNL Experience Manager] 作者實例，使用相同值 `local` 和 `author` 屬性。 對於發佈實例，請提供 [!DNL Experience Manager] 發佈實例。
