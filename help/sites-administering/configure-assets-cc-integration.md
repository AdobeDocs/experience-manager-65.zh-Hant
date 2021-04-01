---
title: 配置AEM Assets與Experience Cloud的整合
description: 瞭解如何設定AEM Assets與Experience Cloud的整合。
contentOwner: AG
feature: 資產管理
role: 業務從業人員、架構師、管理員
translation-type: tm+mt
source-git-commit: 4cc8e60694e2aea74dfedd0bbcb8d47a208d45d1
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 1%

---


# 配置AEM Assets與Experience Cloud{#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}的整合

如果您是Adobe Experience Cloud客戶，您可以將Adobe Experience Manager資產內的資產與Adobe Creative Cloud同步，反之亦然。 您也可以將資產與Experience Cloud同步，反之亦然。 可以通過[!DNL Adobe I/O]設定此同步。 [!DNL Adobe Marketing Cloud]的更新名稱為[!DNL Adobe Experience Cloud]。

設定此整合的工作流程為：

1. 使用公用閘道在[!DNL Adobe I/O]中建立驗證，並取得應用程式ID。
1. 使用應用程式ID在您的AEM Assets例項上建立描述檔。
1. 使用此設定來同步您的資產。

在後端，伺服器會AEM使用閘道驗證您的描述檔，然後同步資產和Experience Cloud之間的資料。

>[!CAUTION]
>
>此功能在AEM Assets已過時。 在[和「Creative Cloud整合」AEM最佳實踐中查找替換項](/help/assets/aem-cc-integration-best-practices.md)。 如果您有任何疑問，請聯絡Adobe客戶服務](https://www.adobe.com/tw/account/sign-in.supportportal.html)。[

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 建立應用程式{#create-an-application}

1. 登入[https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)存取Adobe開發人員閘道介面。

   >[!NOTE]
   >
   >您需要有管理員權限才能建立應用程式ID。

1. 從左窗格，導覽至「開發人員工具&#x200B;**[!UICONTROL >**[!UICONTROL &#x200B;應用程式&#x200B;]**」，以檢視應用程式清單。]**
1. 按一下「**[!UICONTROL 新增]** ![ aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)」以建立應用程式。
1. 從&#x200B;**[!UICONTROL 客戶端憑據]**&#x200B;清單中，選擇&#x200B;**[!UICONTROL 服務帳戶（JWT斷言）]** ，該服務是用於伺服器身份驗證的伺服器到伺服器通信服務。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定應用程式的名稱和選用說明。
1. 從&#x200B;**[!UICONTROL 組織]**&#x200B;清單中，選擇要同步資產的組織。
1. 從&#x200B;**[!UICONTROL Scope]**&#x200B;清單中，選擇&#x200B;**[!UICONTROL dam-read]**、**[!UICONTROL dam-sync]**、**[!UICONTROL dam-write]**&#x200B;和&#x200B;**[!UICONTROL cc-share]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。訊息會通知應用程式已建立。

   ![成功建立將AEM Assets與AdobeCC整合的應用程式的通知](assets/chlimage_1-50.png)

1. 複製為新應用程式生成的&#x200B;**[!UICONTROL 應用程式ID]**。

   >[!CAUTION]
   >
   >請確定您不會不慎複製&#x200B;**[!UICONTROL 應用程式密碼]**，而非&#x200B;**[!UICONTROL 應用程式ID]**。

## 將新配置添加到Experience Cloud{#add-a-new-configuration}

1. 按一下您AEM本地AEM Assets實例的用戶介面上的徽標，然後導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 舊Cloud Services]**。

1. 找到&#x200B;**[!UICONTROL Adobe Experience Cloud]**&#x200B;服務。 如果不存在配置，請按一下「立即配置」。 ****&#x200B;如果配置存在，請按一下「顯示配置」 **[!UICONTROL ，然後按一下「`+` 」添加新配置。]**

   >[!NOTE]
   >
   >使用具有組織管理員權限的Adobe ID帳戶。

1. 在&#x200B;**[!UICONTROL 建立配置]**&#x200B;對話框中，指定新配置的標題和名稱，然後按一下&#x200B;**[!UICONTROL 建立]**。

   ![命名新配置以整合AEM Assets和CC](assets/chlimage_1-51.png)

1. 在&#x200B;**[!UICONTROL 租用戶URL]**&#x200B;欄位中，指定AEM Assets的URL。 在過去，如果URL定義為`https://<tenant_id>.marketing.adobe.com`，請將其變更為`https://<tenant_id>.experiencecloud.adobe.com`。

   1. 導覽至「 **工具 > 雲端服務 >舊 版雲端服務」**。在「Adobe Experience Cloud」下，按一下「顯示配置」。****
   1. 選擇要編輯的現有配置。 編輯配置並將`marketing.adobe.com`替換為`experiencecloud.adobe.com`。
   1. 儲存設定。測試MAC同步複製代理。

1. 在&#x200B;**[!UICONTROL 客戶端ID]**&#x200B;欄位中，貼上在過程[結束時複製的應用程式ID以建立應用程式](#create-an-application)。

   ![提供整合AEM Assets和Creative Cloud所需的應用程式ID值](assets/cloudservices_tenant_info.png)

1. 在&#x200B;**[!UICONTROL Synchronization]**&#x200B;下，選擇&#x200B;**[!UICONTROL Enabled]**&#x200B;啟用同步，然後按一下&#x200B;**[!UICONTROL OK]**。 如果選擇&#x200B;**disabled** ，同步將沿單個方向運行。

1. 在配置頁中，按一下「顯示公共密鑰」**[!UICONTROL 以顯示為實例生成的公共密鑰。]**&#x200B;或者，按一下「下載OAuth閘道的公開金鑰」，下載包含公開金鑰的檔案。 ****&#x200B;然後，開啟檔案以顯示公開金鑰。

## 啟用同步{#enable-synchronization}

1. 使用過程[最後一步中提及的下列方法之一顯示公鑰，向Experience Cloud](#add-a-new-configuration)添加新配置。 按一下「顯示公鑰」。****

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 複製公開密鑰並將其貼上到您在[中建立應用程式](#create-an-application)的應用程式配置介面的&#x200B;**[!UICONTROL Public Key]**&#x200B;欄位中。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 按一下&#x200B;**[!UICONTROL Update]**。 立即將您的資產與AEM Assets實例同步。

## 測試同步{#test-the-synchronization}

1. 按一下本AEM地AEM Assets實例用戶介面上的徽標，並導航至&#x200B;**[!UICONTROL 工具]****[!UICONTROL 部署]** **[!UICONTROL 複製]**以查找為同步建立的複製配置檔案。
1. 在&#x200B;**[!UICONTROL 複製]**&#x200B;頁上，按一下&#x200B;**[!UICONTROL 作者上的代理]**。
1. 從配置檔案清單中，按一下組織的預設複製配置檔案以將其開啟。
1. 在對話框中，按一下&#x200B;**[!UICONTROL 測試連接]**。

   ![測試連接並設定組織的預設複製配置檔案](assets/chlimage_1-54.png)

1. 當複製剩餘時間完成時，在測試結果結束時檢查成功消息。

## 將用戶添加到Experience Cloud{#add-users-to-experience-cloud}

1. 使用管理員憑據登錄Experience Cloud。
1. 從滑軌轉至「**[!UICONTROL 管理]**」，然後按一下／點選「啟動Enterprise Dashboard ]**」。**[!UICONTROL 
1. 從邊欄按一下「**[!UICONTROL 使用者]**」以開啟「使用者管理&#x200B;]**」頁面。**[!UICONTROL 
1. 在工具列中，按一下「新增&#x200B;**** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)」。
1. 新增一或多個您想要提供與Creative Cloud共用資產的使用者。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## AEM Assets與Experience Cloud之間交換資產{#exchange-assets-between-aem-and-experience-cloud}

1. 登入AEM Assets。
1. 在「資產」主控台中，建立資料夾並上傳部分資產至該資料夾。 例如，建立資料夾&#x200B;**mc-demo**&#x200B;並上傳資產至它。
1. 選擇該資料夾，然後按一下&#x200B;**Share** ![assets_share](assets/do-not-localize/assets_share.png)。
1. 從菜單中，選擇&#x200B;**[!UICONTROL Adobe Experience Cloud]** ，然後按一下&#x200B;**[!UICONTROL 共用]**。 一條消息通知資料夾已與Experience Cloud共用。

   >[!NOTE]
   >
   >在Adobe Experience Cloud共用時，不支援共用類型`sling:OrderedFolder`的「資產」檔案夾。 如果要共用資料夾，在AEM Assets建立資料夾時，不要選擇&#x200B;**[!UICONTROL Ordered]**&#x200B;選項。

1. 刷新AEM Assets用戶介面。 您在本地AEM Assets實例的「資產」控制台中建立的資料夾將被複製到Experience Cloud用戶介面。 您上傳至AEM Assets資料夾的資產，在伺服器處理後，會顯示在Experience Cloud中資料夾的復AEM本中。
1. 您也可以在Experience Cloud的資料夾複製副本中上傳資產。 處理完資產後，資產就會出現在AEM Assets的共用資料夾中。

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
>* [資產與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)
>* [資產到Creative Cloud資料夾共用最佳實務](/help/assets/aem-cc-folder-sharing-best-practices.md)

