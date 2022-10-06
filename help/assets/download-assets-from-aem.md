---
title: 下載資產
description: 了解如何從下載資產 [!DNL Adobe Experience Manager] 和啟用或停用下載功能。
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 5%

---

# 從下載資產 [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/download-assets-from-aem.html?lang=en) |

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接從傳送包含資產連結的電子郵件 [!DNL Adobe Experience Manager Assets]. 下載的資產會以ZIP檔案整合。 壓縮的ZIP檔案的檔案大小上限為1 GB。 每個匯出工作最多可允許500個資產。

>[!NOTE]
>
>任何具有讀取權限的使用者 `/var/dam/share` 位置可以存取電子郵件訊息中共用的下載連結。
>
>任何具有讀取權限的使用者 `/var/dam/jobs/download` 位置可以下載資產。
>
>無法下載資產類型 — 影像集、回轉集、混合媒體集和轉盤集。

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**若要下載資產，請依照下列步驟操作：**

1. 在左上角，按一下標誌。 在左側邊欄中，按一下 **[!UICONTROL 導覽]**.
1. 在 [!UICONTROL 導覽] 頁面，按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至包含您要下載之資產的資料夾。
1. 選取資料夾，或在資料夾內選取一或多個資產。
1. 在工具列上，按一下 **[!UICONTROL 下載]**.
1. 在「下載」對話方塊中，選取您想要的下載選項。

   | 匯出或下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選取此選項，將您下載的每個資產（包括資產的父資料夾下巢狀子資料夾中的資產），納入本機電腦上的一個資料夾。 若未選取此選項，依預設會忽略資料夾階層，而所有資產都會下載至本機電腦的一個資料夾中。 |
   | **[!UICONTROL 電子郵件]** | 會傳送電子郵件通知給使用者。 標準電子郵件範本位於下列位置：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 在部署期間自定義的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在下列位置儲存租用戶專用的自訂範本：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選取此選項即可下載原始格式的資產，而不需任何轉譯。<br>如果原始資產有子資產，則子資產選項可供使用。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產有主要表示法，即上傳之檔案的主要表示法。 它們可以有任意數量的表示。 <br> 使用此選項，您可以選取要下載的轉譯。 可用的轉譯取決於您選取的資產。 如果資產有任何轉譯，則可使用選項。 |
   | **[!UICONTROL 智慧裁切]** | 選取此選項，即可從AEM內下載所選資產的所有智慧型裁切轉譯。 會建立包含智慧型裁切轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選取此選項即時產生一系列替代轉譯。 選取此選項時，您也可以選取 [影像預設集](image-presets.md) 清單。 <br>此外，您還可以選取尺寸和單位、格式、顏色空間、解析度，以及任何可選的影像修飾符，如反相影像。 只有在您有 [!DNL Dynamic Media] 已啟用。 |

1. 在對話方塊中，按一下 **[!UICONTROL 下載]**.

選取要下載的資料夾時，會下載該資料夾下的完整資產階層。 若要將您下載的每個資產（包括父資料夾下巢狀子資料夾中的資產）包含在個別資料夾中，請選取 **[!UICONTROL 為每個資產建立個別資料夾]**.

## 啟用資產下載servlet {#enable-asset-download-servlet}

中的預設Servlet [!DNL Experience Manager] 可讓已驗證的使用者發出任意大型且同時下載的請求，以建立可見資產的ZIP檔案，而這可能會使伺服器和網路過載。 為降低此功能可能造成的DoS風險， `AssetDownloadServlet` 發佈例項的OSGi元件預設為停用。

若要允許從DAM下載資產，例如使用資產共用公域或其他類似入口的實作時，請透過OSGi設定手動啟用servlet。 Adobe建議盡可能低地設定允許的下載大小，而不影響日常下載需求。 高值可能會影響效能。

1. 建立以發佈執行模式為目標的命名慣例的資料夾(`config.publish`): `/apps/<your-app-name>/config.publish`. 要定義運行模式的配置屬性，請參閱 [執行模式](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. 在設定資料夾中，建立類型的檔案 `nt:file` 已命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. 填入 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 以下內容。 將下載的最大大小（以位元組為單位）設定為 `asset.download.prezip.maxcontentsize`. 以下範例會將ZIP下載的最大大小設定為不超過100千位元組。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

預設情況下， `GET` 請求下載檔案， [!DNL Experience Manager] 會對ZIP封存的下載大小強制執行50 MB的限制。 透過 `POST` 請求或使用者介面不受此限制影響。

## 停用資產下載servlet {#disable-asset-download-servlet}

此 `Asset Download Servlet` 可在 [!DNL Experience Manager] 更新Dispatcher設定以封鎖任何資產下載請求，以發佈執行個體。 您也可以直接透過OSGi主控台手動停用servlet。

1. 若要透過Dispatcher設定封鎖資產下載請求，請編輯 `dispatcher.any` 設定，並將規則新增至 [篩選器區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 若要在發佈執行個體上停用OSGi元件，請在 `http://[aem_server]:[port]/system/console/components`. 找出 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` 按一下 **[!UICONTROL 停用]**.

>[!MORELIKETHIS]
>
>* [使用Brand Portal下載資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [下載受DRM保護的資產](drm.md).
>* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [從支援的Adobe Creative Cloud應用程式使用Adobe資產連結下載資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html).

