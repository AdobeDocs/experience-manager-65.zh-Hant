---
title: Generate a URL to shared assets
description: This article describes how to share assets, folders, and collections within Experience Manager Assets as a URL to external parties.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 6%

---


# Share asset via a link {#asset-link-sharing}

Adobe Experience Manager Assets可讓您與組織成員及外部實體（包括合作夥伴和廠商）以URL形式共用資產、資料夾和系列。 Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Assets.

>[!NOTE]
>
>You require Edit ACL permission on the folder or the asset that you want to share as a link.

## 共用資產 {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them.

>[!NOTE]
>
>Before you share a link with users, ensure that Day CQ Mail Service is configured. An error occurs if you attempt to share a link without first [configuring Day CQ Mail Service](/help/assets/link-sharing.md#configmailservice).

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click the **[!UICONTROL Share Link]** ![assets_share](assets/assets_share.png).

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   ![Dialog with the Link Share](assets/Link-sharing-dialog-box.png)

   *Figure: The dialog to share assets as a link.*

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If you want to share links from your Experience Manager Author instance to external entities, ensure that you only expose the following URLs (which are used for link sharing) for `GET` requests only. Block other URLs to ensure security of Experience Manager Author.
   >
   >* http://[aem_server]:[port]/linkshare.html
   >* http://[aem_server]:[port]/linksharepreview.html
   >* http://[aem_server]:[port]/linkexpired.html


   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. In Experience Manager interface, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. For the `local` and `author` properties, provide the URL for the local and the author instance respectively. Both `local` and `author` properties have the same value if you run a single Experience Manager Author instance. 例如， `publish`提供Experience Manager發佈例項的URL。

1. 在「連結共用」對話方 **[!UICONTROL 塊的電子郵件地址方塊中]** ，輸入您要共用連結之使用者的電子郵件ID。您也可以與多位使用者共用連結。

   如果使用者是您組織的成員，請從顯示在輸入區域下方清單中的建議電子郵件ID中選取使用者的電子郵件ID。 對於外部使用者，輸入完整的電子郵件ID，然後從清單中選取它。

   要啟用發送給用戶的電子郵件，請在第CQ天郵件服務中配置SMTP服 [務器詳細資訊](#configmailservice)。

   ![直接從「連結共用」對話方塊分享資產連結](assets/Asset-Sharing-LinkShareDialog.png)

   *圖： 直接從「連結共用」對話方[!UICONTROL 塊共用資產連結]。*

   >[!NOTE]
   >
   >如果您輸入非您組織成員之使用者的電子郵件ID，則「外部使用者  」字詞會加上使用者的電子郵件ID前置詞。

1. In the **[!UICONTROL Subject]** field, enter a subject for the asset you want to share.

1. 在「消 **[!UICONTROL 息]** 」欄位中，輸入可選消息。

1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.

   ![設定共用連結的到期日](assets/Set-shared-link-expiration.png)

1. 若要讓使用者下載原始影像以及轉譯，請選取「允 **[!UICONTROL 許下載原始檔案」]**。

   >[!NOTE]
   >
   >依預設，使用者只能下載您以連結形式共用之資產的轉譯。

1. 按一下&#x200B;**[!UICONTROL 「共用」]**。訊息會確認連結是透過電子郵件與使用者共用。
1. 若要檢視共用資產，請按一下傳送給使用者之電子郵件中的連結。 共用資產會顯示在 **[!UICONTROL Adobe Marketing Cloud頁面中]** 。

   ![chlimage_1-260](assets/chlimage_1-545.png)

   若要切換至清單檢視，請按一下工具列中的版面選項。

1. 若要產生資產的預覽，請按一下共用資產。 To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >Experience Manager支援產生下列MIME類型資產的預覽： JPG、PNG、GIF、BMP、INDD、PDF和PPT。 您只能下載其他MIME類型的資產。

1. 若要下載共用資產，請按一 **[!UICONTROL 下工具列中的]** 「選取」、按一下資產，然後按一下工具列 **[!UICONTROL 中的「下載]** 」。

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. 若要檢視您共用為連結的資產，請前往「資產」UI，然後按一下「Experience Manager」標誌。 從清 **[!UICONTROL 單選擇]** 「導覽」，以顯示「導覽」窗格。
1. 從「導覽」窗格中，選 **[!UICONTROL 擇「共用連結]** 」以顯示共用資產清單。
1. 若要取消共用資產，請選取資產，然後按一下工 **[!UICONTROL 具列中的]** 「取消共用」。 之後會出現確認訊息。 資產的項目會從清單中移除。

## 配置日CQ郵件服務 {#configmailservice}

1. 在Experience Manager首頁上，導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web主控台]**」。
1. 從服務清單中，找到 **[!UICONTROL Day CQ Mail Service]**。
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * SMTP伺服器主機名： 電子郵件伺服器主機名
   * SMTP server port: email server port
   * SMTP user: email server user name
   * SMTP password: email server password

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 配置最大資料大小 {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. 為防止系統因此遭受潛在的拒絕服務攻擊，請使用 **[!UICONTROL Configuration Manager中Day CQ的]** Max Content Size（未壓縮）  Day CQ DAM Adhoc Asset Share Proxy Servlet參數配置最大大小。 If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click the Experience Manager logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. 從Web主控台中，找到 **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet設定]** 。
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM臨機資產共用代理Servlet]** 」設定，並修改「最大內容大小 (未壓縮) 」 **[!UICONTROL 參數的值]** 。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 儲存變更。

## Best practices and troubleshooting {#bestpractices}

* Asset folders or Collections that contain a whitespace in their name may not get shared.
* If users cannot download the shared assets, check with your Experience Manager administrator what the [download limits](#maxdatasize) are.
* 如果您無法傳送含有共用資產連結的電子郵件，或如果其他使用者無法收到您的電子郵件，請洽詢您的Experience Manager管理員，以確認是否已 [設定](#configmailservice) 電子郵件服務。
* 如果您無法使用連結共用功能來共用資產，請確定您擁有適當的權限。 請參閱 [分享資產](#sharelink)。
