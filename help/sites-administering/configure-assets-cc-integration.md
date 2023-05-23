---
title: 配置AEM Assets與Experience Cloud的整合
description: 瞭解如何配置AEM Assets與Experience Cloud的整合。
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# 配置AEM Assets與Experience Cloud的整合 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

如果您是Adobe Experience Cloud客戶，則可以將Adobe Experience Manager資產內的資產與Adobe Creative Cloud同步，反之亦然。 您還可以將資產與Experience Cloud同步，反之亦然。 您可以通過 [!DNL Adobe I/O]。 更新的名稱 [!DNL Adobe Marketing Cloud] 是 [!DNL Adobe Experience Cloud]。

要設定此整合的工作流是：

1. 在中建立身份驗證 [!DNL Adobe I/O] 使用公共網關並獲取應用程式ID。
1. 使用應用程式ID在AEM Assets實例上建立配置檔案。
1. 使用此配置可同步您的資產。

在後端，服AEM務器使用網關驗證您的配置檔案，然後在「資產」和「Experience Cloud」之間同步資料。

>[!NOTE]
>
>在中不建議使用此功能 [!DNL Assets]。 在 [和AEMCreative Cloud整合最佳做法](/help/assets/aem-cc-integration-best-practices.md)。 如果你有任何疑問， [聯繫Adobe客戶支援](https://www.adobe.com/tw/account/sign-in.supportportal.html)。

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 建立應用程式 {#create-an-application}

1. 登錄Adobe Developer網關介面 [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)。

   >[!NOTE]
   >
   >您需要管理員權限才能建立應用程式ID。

1. 從左窗格導航到 **[!UICONTROL 開發人員工具]** > **[!UICONTROL 應用程式]** 的子菜單。
1. 按一下 **[!UICONTROL 添加]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) 的子菜單。
1. 從 **[!UICONTROL 客戶端憑據]** 清單，選擇 **[!UICONTROL 服務帳戶（JWT斷言）]**，是用於伺服器身份驗證的伺服器到伺服器通信服務。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定應用程式的名稱和可選說明。
1. 從 **[!UICONTROL 組織]** 清單中，選擇要同步其資產的組織。
1. 從 **[!UICONTROL 範圍]** 清單，選擇 **[!UICONTROL 水壩讀取]**。 **[!UICONTROL 水壩同步]**。 **[!UICONTROL 水壩寫]**, **[!UICONTROL cc共用]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。消息將通知應用程式已建立。

   ![成功建立將AEM Assets與Creative Cloud融為一體的應用程式的通知](assets/chlimage_1-50.png)

1. 複製 **[!UICONTROL 應用程式ID]** 為新應用程式生成的。

   >[!CAUTION]
   >
   >確保不會無意中複製 **[!UICONTROL 應用程式密碼]** 而不是 **[!UICONTROL 應用程式ID]**。

## 將新配置添加到Experience Cloud {#add-a-new-configuration}

1. 按一下AEM本地AEM Assets實例的用戶介面上的徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 舊Cloud Services]**。

1. 查找 **[!UICONTROL Adobe Experience Cloud]** 服務。 如果沒有配置，請按一下 **[!UICONTROL 立即配置]**。 如果存在配置，請按一下 **[!UICONTROL 顯示配置]** 按一下 `+` 的子菜單。

   >[!NOTE]
   >
   >使用具有組織管理員權限的Adobe ID帳戶。

1. 在 **[!UICONTROL 建立配置]** 對話框，指定新配置的標題和名稱，然後按一下 **[!UICONTROL 建立]**。

   ![命名新配置以整合AEM Assets和Creative Cloud](assets/aem-ec-integration-config1.png)

1. 在 **[!UICONTROL 租戶URL]** 欄位，指定AEM Assets的URL。 過去，如果URL定義為 `https://<tenant_id>.marketing.adobe.com`，將其更改為 `https://<tenant_id>.experiencecloud.adobe.com`。

   1. 導覽至「 **工具 > 雲端服務 >舊 版雲端服務」**。在Adobe Experience Cloud下，按一下 **顯示配置**。
   1. 選擇要編輯的現有配置。 編輯配置並替換 `marketing.adobe.com` 至 `experiencecloud.adobe.com`。
   1. 儲存設定。TestMAC同步複製代理。

1. 在 **[!UICONTROL 客戶端ID]** 欄位，貼上您在過程末尾複製的應用程式ID [建立應用程式](#create-an-application)。

   ![提供整合AEM Assets和Creative Cloud所需的應用程式ID值](assets/cloudservices_tenant_info.png)

1. 下 **[!UICONTROL 同步]** 選擇 **[!UICONTROL 已啟用]** 啟用同步，按一下 **[!UICONTROL 確定]**。 如果選擇 **禁用**，同步工作在單個方向。

1. 在配置頁中，按一下 **[!UICONTROL 顯示公鑰]** 顯示為實例生成的公鑰。 或者，按一下 **[!UICONTROL 下載OAuth網關的公鑰]** 下載包含公鑰的檔案。 然後，開啟檔案以顯示公鑰。

## 啟用同步 {#enable-synchronization}

1. 使用過程最後一步中提到的以下方法之一顯示公鑰 [將新配置添加到Experience Cloud](#add-a-new-configuration)。 按一下 **[!UICONTROL 顯示公鑰]**。

1. 複製公鑰並將其貼上到 **[!UICONTROL 公鑰]** 在中建立的應用程式的配置介面欄位 [建立應用程式](#create-an-application)。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 按一下&#x200B;**[!UICONTROL 更新]**。立即將您的資產與AEM Assets實例同步。

## Test同步 {#test-the-synchronization}

1. 按一下AEM本地AEM Assets實例的用戶介面上的徽標並導航至 **[!UICONTROL 工具]**> **[!UICONTROL 部署]**> **[!UICONTROL 複製]**查找為同步建立的複製配置檔案。
1. 在 **[!UICONTROL 複製]** 的 **[!UICONTROL 作者代理]**。
1. 在配置檔案清單中，按一下組織的預設複製配置檔案以將其開啟。
1. 在對話框中，按一下 **[!UICONTROL Test連接]**。

   ![Test連接並設定組織的預設複製配置檔案](assets/chlimage_1-54.png)

1. 複製剩餘完成後，在test結果末尾檢查成功消息。

## 將用戶添加到Experience Cloud {#add-users-to-experience-cloud}

1. 使用管理員憑據登錄到Experience Cloud。
1. 從滑軌，轉到 **[!UICONTROL 管理]** 然後按一下 **[!UICONTROL 啟動企業儀表板]**。
1. 在滑軌上，按一下 **[!UICONTROL 用戶]** 開啟 **[!UICONTROL 用戶管理]** 的子菜單。
1. 在工具欄中，按一下 **添加** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)。
1. 添加一個或多個要提供與Creative Cloud共用資產的功能的用戶。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## AEM Assets與Experience Cloud之間的資產交換 {#exchange-assets-between-aem-and-experience-cloud}

1. 登錄AEM Assets。
1. 在「資產」控制台中，建立一個資料夾並將一些資產上載到該資料夾。 例如，建立資料夾 **mc演示** 並上傳資產。
1. 選擇資料夾並按一下 **共用** ![資產_共用](assets/do-not-localize/assets_share.png)。
1. 從菜單中，選擇 **[!UICONTROL Adobe Experience Cloud]** 的 **[!UICONTROL 共用]**。 消息將通知資料夾已與Experience Cloud共用。

   >[!NOTE]
   >
   >共用類型的Assets資料夾 `sling:OrderedFolder`，在Adobe Experience Cloud共用時不受支援。 如果要共用資料夾，在AEM Assets建立時，不要選擇 **[!UICONTROL 已訂購]** 的雙曲餘切值。

1. 刷新AEM Assets用戶介面。 在本地AEM Assets實例的Assets控制台中建立的資料夾會複製到Experience Cloud用戶介面。 您上載到AEM Assets資料夾的資產在伺服器處理後顯示在Experience Cloud中的資料夾副AEM本中。
1. 您還可以在Experience Cloud中資料夾的複製副本中上載資產。 處理後，資產將出現在AEM Assets的共用資料夾中。

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and vice versa for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [資產和Creative Cloud整合最佳做法](/help/assets/aem-cc-integration-best-practices.md)

