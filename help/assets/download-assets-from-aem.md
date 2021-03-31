---
title: 下載資產
description: 瞭解如何從 [!DNL Adobe Experience Manager] 下載資產並啟用或停用下載功能。
contentOwner: AG
role: 業務從業人員
feature: 資產管理，資產分配
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 4%

---


# 從[!DNL Adobe Experience Manager] {#download-assets-from-aem}下載資產

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接從[!DNL Adobe Experience Manager Assets]傳送含有資產連結的電子郵件。 已下載的資產會整合在ZIP檔案中。 壓縮的ZIP檔案對於匯出工作的檔案大小上限為1 GB。 每個匯出工作最多允許500個資產。

>[!NOTE]
>
>電子郵件的收件者必須是`dam-users`群組的成員，才能存取電子郵件訊息中的ZIP下載連結。 若要下載資產，成員必須擁有啟動觸發資產下載的工作流程的權限。

無法下載資產類型影像集、回轉集、混合媒體集和轉盤集。

若要下載資產，請依照下列步驟進行：

1. 在左上角，按一下標誌。 在左側導軌中，按一下「**[!UICONTROL Navigation]**」。
1. 在[!UICONTROL Navigation]頁面上，按一下&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files。]**
1. 導覽至包含您要下載之資產的檔案夾。
1. 選取資料夾或選取資料夾內的一或多個資產。
1. 在工具列上，按一下「下載」。]****[!UICONTROL 

   ![從Experience Manager資產下載資產時的可用選項](/help/assets/assets/asset-download1.png)

   *圖：下載對話方塊中提供的選項。*

1. 在「下載」對話方塊中，選取您想要的下載選項。

   | 匯出或下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選取此選項，將您下載的每個資產（包括資產）包含在資產父資料夾下巢狀的子資料夾中，並放入本機電腦上的一個資料夾。 如果未選取此選項，預設會忽略資料夾階層，並將所有資產下載至本機電腦的一個資料夾。 |
   | **[!UICONTROL 電子郵件]** | 系統會傳送電子郵件通知給使用者。 標準電子郵件範本可在下列位置取得：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您在部署期間自訂的範本可在下列位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在下列位置儲存租用戶特定的自訂範本：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選取這個選項，以原始格式下載資產，而不需任何轉譯。<br>如果原始資產有子資產，則可使用子資產選項。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產具有主要表示法——已上傳檔案的主要表示法。 它們可以有任意數量的表示。 <br> 使用這個選項，您可以選取您要下載的轉譯。可用的轉譯取決於您選取的資產。 如果資產有任何轉譯，此選項即可使用。 |
   | **[!UICONTROL 智慧裁切]** | 選取這個選項，可從中下載所選資產的所有智慧型裁切轉譯AEM。 系統會建立包含「智慧型裁切」轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選取此選項，即時產生一連串的替代轉譯。 當您選取此選項時，也可以從[影像預設集](image-presets.md)清單中選取您要動態建立的轉譯。 <br>此外，您還可以選取大小和單位、格式、色域、解析度，以及任何可選的影像修飾元，例如反轉影像。只有在啟用[!DNL Dynamic Media]時，此選項才可用。 |

1. 在對話方塊中，按一下「下載」。]**。**[!UICONTROL 

當您選擇要下載的檔案夾時，會下載該檔案夾下的完整資產階層。 若要將您下載的每個資產（包括父資料夾下巢狀的子資料夾中的資產）納入個別資料夾，請選取&#x200B;**[!UICONTROL 為每個資產建立個別資料夾]**。

## 啟用資產下載servlet {#enable-asset-download-servlet}

[!DNL Experience Manager]中的預設servlet允許通過身份驗證的用戶發出任意大的併發下載請求，以建立對他們可見的資產的ZIP檔案，這些資產可能會使伺服器和網路過載。 為了降低此功能造成的潛在DoS風險，`AssetDownloadServlet` OSGi元件預設會停用於發佈例項。

若要允許從DAM下載資產，例如，當使用資產共用共用共用或其他類似入口網站的實施時，請透過OSGi組態手動啟用servlet。 Adobe建議盡可能低地設定允許的下載大小，而不會影響日常下載需求。 高價值可能會影響效能。

1. 建立具有命名慣例的檔案夾，以發佈執行模式(`config.publish`)為目標：`/apps/<your-app-name>/config.publish`。 要定義運行模式的配置屬性，請參閱[運行模式](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)。
1. 在配置資料夾中，建立名為`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`的類型`nt:file`的檔案。
1. 使用下列填入`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。 將下載的最大大小（以位元組為單位）設定為`asset.download.prezip.maxcontentsize`的值。 下面的示例將ZIP下載的最大大小配置為不超過100 kB。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 停用資產下載servlet {#disable-asset-download-servlet}

`Asset Download Servlet`可在[!DNL Experience Manager]發佈實例上禁用，方法是更新調度程式配置以阻止任何資產下載請求。 也可以通過OSGi控制台手動禁用servlet。

1. 若要透過分派器設定來封鎖資產下載請求，請編輯`dispatcher.any`設定，並新增規則至[篩選區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)。`/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 要在Publish實例上禁用OSGi元件，請訪問`http://[aem_server]:[port]/system/console/components`處的OSGi控制台。 找到`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet`並按一下&#x200B;**[!UICONTROL 禁用]**。

>[!MORELIKETHIS]
>
>* [使用品牌入口網站下載資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [下載受DRM保護的資產](drm.md)。
>* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)。
>* [從支援的Adobe Creative Cloud應用程式內使用Adobe資產連結下載資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html)。

