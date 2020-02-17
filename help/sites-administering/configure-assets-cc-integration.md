---
title: 設定與Experience cloud和Creative cloud的AEM資產整合
seo-title: 設定AEM Assets與Marketing cloud和Creative cloud的整合
description: 瞭解如何設定與Experience cloud和Creative cloud整合的AEM資產。
seo-description: 瞭解如何設定與Experience cloud和Creative cloud整合的AEM資產。
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: c62a7f12ea6a988cee597516d2f73d15c3802c62

---


# 設定與Experience cloud和Creative cloud的AEM資產整合 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

如果您是Adobe Experience cloud客戶，則可以將Adobe Experience Manager(AEM)Assets中的資產與Adobe Creative cloud同步，反之亦然。 您也可以將資產與Experience cloud同步，反之亦然。 您可以透過Adobe I/O設定此同步。

設定此整合的工作流程為：

1. 使用公用閘道在Adobe I/O中建立驗證，並取得應用程式ID。
1. 使用應用程式ID在您的AEM Assets例項上建立描述檔。
1. 使用此設定，將AEM Assets中的資產與Creative cloud同步。

在後端，AEM伺服器會使用閘道驗證您的個人檔案，然後同步AEM Assets和Experience cloud之間的資料。

>[!CAUTION]
>
>AEM Assets中已停用「AEM到Creative cloud資料夾共用」功能。 進一步瞭解並尋找 [AEM和Creative cloud整合最佳實務的替代項目](/help/assets/aem-cc-integration-best-practices.md)。

![整合AEM Assets和Creative cloud時的資料流程](assets/chlimage_1-48.png)

整合AEM Assets和Creative cloud時的資料流程

>[!NOTE]
>
>在Adobe Experience cloud和Adobe Creative cloud之間共用資產需要AEM例項的管理員權限。

>[!CAUTION]
>
>Adobe Marketing cloud已重新命名為Adobe Experience Cloud。 以下程式仍提及Marketing Cloud，以反映目前的介面。 這些提及將於稍後日期變更。

## 建立應用程式 {#create-an-application}

1. 登入https://legacy-oauth.cloud.adobe.io以存取Adobe開發人員閘道介 [面](https://legacy-oauth.cloud.adobe.io/)。

   >[!NOTE]
   >
   >您需要有管理員權限才能建立應用程式ID。

1. 從左窗格，導覽至「開發人 **[!UICONTROL 員工具]** >應 **[!UICONTROL 用程式]** 」以檢視應用程式清單。
1. 按一 **[!UICONTROL 下]** 「新 ![增aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) 」以建立應用程式。
1. 從「客 **[!UICONTROL 戶端認證]** 」清單中，選擇 **[!UICONTROL 服務帳戶（JWT斷言）]**，該服務是用於伺服器驗證的伺服器到伺服器通信服務。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定應用程式的名稱和選用說明。
1. 從「組 **[!UICONTROL 織]** 」(Organization)清單中，選擇要為其同步資產的組織。
1. 從「范 **[!UICONTROL 圍]** 」清單中，選取dam-read **[!UICONTROL 、]** dam-sync **[!UICONTROL 、]********** dam-write-share和Cc-Share。
1. 按一下&#x200B;**[!UICONTROL 「建立」]**。訊息會通知應用程式已建立。

   ![成功建立應用程式以整合AEM Assets與Adobe CC的通知](assets/chlimage_1-50.png)

1. 複製 **[!UICONTROL 為新應用程式產生的應用程式ID]** 。

   >[!CAUTION]
   >
   >請確定您不會不慎複製「應用程 **[!UICONTROL 式密碼]** 」，而 **[!UICONTROL 非「應用程式ID」]**。

## 新增設定至Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}

1. 按一下您本機AEM Assets例項使用者介面上的AEM標誌，並導覽至「工具 **[!UICONTROL >]** Cloud Services **[!UICONTROL >舊]** 版Cloud Services ****」。

1. 找到 **[!UICONTROL Adobe Marketing cloud服務]** 。 如果沒有配置，請按一下「 **[!UICONTROL 立即配置]**」。 如果存在配置，請單 **[!UICONTROL 擊「顯示配置]** 」 , **[!UICONTROL [然後按一下]]** +以添加新配置。

   >[!NOTE]
   >
   >使用具有組織管理員權限的Adobe ID帳戶。

1. 在「創 **[!UICONTROL 建配置]** 」對話框中，指定新配置的標題和名稱，然後按一下「 **[!UICONTROL 建立」]**。

   ![為新組態命名以整合AEM Assets和CC](assets/chlimage_1-51.png)

1. 在「租 **[!UICONTROL 用戶URL]** 」欄位中，指定AEM資產的URL。

   >[!CAUTION]
   >
   >由於重新品牌化，如果您依需要 `https://<tenant_id>.marketing.adobe.com` 將「租用戶URL」輸入 `https://<tenant_id>.experiencecloud.adobe.com.` ，請依照下列步驟進行：
   >
   >1. 導覽至「 **工具>雲端服務>舊版雲端服務」**。
   1. 在Adobe Marketing cloud下，按一下「顯 **示設定」**。
   1. 選取設定AEM-MAC-CC同步時建立的設定。
   1. 編輯cloudservice設定，並取 **代「租用戶URL」欄位中的** marketing.adobe.com **,**&#x200B;體驗cloud.adobe.com。
   1. 保存配置。
   1. 測試Mac-sync複製代理。


1. 在「用 **[!UICONTROL 戶端ID]** 」欄位中 [，貼上您在「建立應用程式」程式結尾所復](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)制的應用程式ID。

   ![提供整合AEM Assets和Creative cloud所需的應用程式ID值](assets/cloudservices_tenant_info.png)

1. 在「同 **[!UICONTROL 步]** 」下，選 **[!UICONTROL 擇「啟用]** 」以啟用同步，然後按一下「 **[!UICONTROL 確定」]**。

   >[!NOTE]
   如果選擇 **禁用**，同步將沿單個方向運行。

1. 在設定頁面中，按一 **[!UICONTROL 下顯示公開金鑰]** ，以顯示為您的例項產生的公開金鑰。 或者，按一 **[!UICONTROL 下「下載OAuth閘道的公開金鑰]** 」以下載包含公開金鑰的檔案。 然後，開啟檔案以顯示公開金鑰。

## 啟用同步 {#enable-synchronization}

1. 使用程式「新增設定至Marketing Cloud」最後一步中提及的下列方法 [之一顯示公開金鑰](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud)。 按一 **[!UICONTROL 下顯示公開金鑰]**。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 複製公開密鑰，並將其貼上到在建立應用程式中建立的 **[!UICONTROL 應用程式的配置介面的「公]** 開密鑰」欄位中 [](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 按一 **[!UICONTROL 下更新]**。 立即將您的資產與AEM Assets例項同步。

## 測試同步 {#test-the-synchronization}

1. 按一下您本機AEM Assets例項使用者介面上的AEM標誌，並導覽至 **[!UICONTROL Tools]**> **[!UICONTROL Deployment]**> **[!UICONTROL Replication]**，以找出為同步建立的複製設定檔。
1. 在「復 **[!UICONTROL 制]** 」頁上，按一下 **[!UICONTROL 作者上的代理]**。
1. 從配置檔案清單中，按一下組織的預設複製配置檔案以將其開啟。
1. 在對話方塊中，按一下「 **[!UICONTROL 測試連線」]**。

   ![測試連接並設定組織的預設複製配置檔案](assets/chlimage_1-54.png)

1. 當複製剩餘時間完成時，在測試結果結束時檢查成功消息。

## 新增使用者至Marketing Cloud {#add-users-to-marketing-cloud}

1. 使用管理員認證登入Marketing Cloud。
1. 從滑軌移至「管理」 **** ，然後按一下／點 **[!UICONTROL 選「啟動Enterprise Dashboard]**」。
1. 在邊欄中，按一下「使 **[!UICONTROL 用者]** 」以開啟「 **[!UICONTROL 使用者管理]** 」頁面。
1. 在工具列中，按一下／點 **選** 「新 ![增aem_assets_add_icon」](assets/aem_assets_add_icon.png)。
1. 新增一或多個您想要提供與Creative cloud共用資產的使用者。

   >[!NOTE]
   只有您新增至Marketing cloud的使用者可以將AEM Assets中的資產共用至Creative Cloud。

## 在AEM Assets和Marketing cloud之間交換資產 {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. 登入AEM Assets。
1. 在「資產」主控台中，建立資料夾並上傳部分資產至該資料夾。 例如，建立資料夾 **mc-demo** ，並上傳資產至它。
1. 選取資料夾，然後按一 **下**![Share](assets/assets_share.png)assets_share。
1. 從功能表中，選取 **[!UICONTROL Adobe Marketing Cloud]** ，然後按一下「 **[!UICONTROL 共用」]**。 訊息會通知資料夾已與Marketing cloud共用。

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   在Adobe Marketing cloud中共用的內 `sling:OrderedFolder`容中，不支援共用類型的「資產」檔案夾。 如果您想要共用資料夾，在AEM Assets中建立資料夾時，請勿選取「已訂購」 **[!UICONTROL 選項]** 。

1. 重新整理AEM Assets使用者介面。 您在本機AEM Assets例項的「資產」主控台中建立的檔案夾會複製至Marketing Cloud UI。 您上傳至「AEM資產」中檔案夾的資產，會在AEM伺服器處理後，顯示在Marketing cloud中檔案夾的復本中。
1. 您也可以在Marketing cloud資料夾的複製副本中上傳資產。 處理完資產後，資產就會出現在AEM Assets的共用資料夾中。

## 在AEM Assets和Creative cloud之間交換資產 {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
「AEM到Creative cloud資料夾共用」功能已過時。 強烈建議客戶使用較新的功能，例如 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)[或AEM案頭應用程式](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)。 進一步了 [解AEM和Creative cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)。

AEM Assets可讓您與Adobe Creative cloud使用者共用包含資產的檔案夾。

1. 在「資產」主控台中，選取要與Creative cloud共用的檔案夾。
1. 在工具列中，按一 **[!UICONTROL 下]**![Share](assets/assets_share.png)assets_share。
1. 從清單中選取 **[!UICONTROL Adobe Creative Cloud]** 選項。

   >[!NOTE]
   這些選項適用於具有根目錄讀取權限的用戶。 使用者必須擁有存取Marketing cloud複製代理資訊的必要權限。

1. 在「 **[!UICONTROL Creative cloud共用]** 」頁面中，新增要與共用資料夾的使用者，並為使用者選擇角色。 按一 **[!UICONTROL 下「儲存]** 」，然後按 **[!UICONTROL 一下「確定]**」。

1. 使用您共用資料夾之使用者的認證登入Creative Cloud。 共用資料夾可在Creative cloud中使用。

AEM Assets-Marketing cloud同步的設計方式，是讓上傳資產的使用者機器例項保留修改資產的權利。 只有這些更改才會傳播到另一個實例。

例如，如果資產是從AEM Assets（內部）例項上傳，則來自此例項的資產變更會傳播至Marketing cloud例項。 不過，從Marketing cloud例項對相同資產所做的變更不會傳播至AEM例項，從Marketing cloud上傳的資產也會傳播至AEM例項。

>[!MORELIKETHIS]
* [AEM與Creative cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)
* [AEM到Creative cloud資料夾分享最佳實務](/help/assets/aem-cc-folder-sharing-best-practices.md)

