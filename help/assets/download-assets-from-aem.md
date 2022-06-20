---
title: 下載資產
description: 瞭解如何從下載資產 [!DNL Adobe Experience Manager] 以及啟用或禁用下載功能。
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

您可以下載資產，包括靜態和動態格式副本。 或者，您也可以直接從 [!DNL Adobe Experience Manager Assets]。 下載的資產捆綁在ZIP檔案中。 壓縮的ZIP檔案對於導出作業的最大檔案大小為1 GB。 每個導出作業最多允許500個總資產。

>[!NOTE]
>
>具有讀取權限的任何用戶 `/var/dam/share` 位置可以訪問電子郵件中共用的下載連結。
>
>具有對 `/var/dam/jobs/download` 位置可以下載資產。
>
>無法下載資產類型 — 映像集、旋轉集、混合媒體集和旋轉盤集。

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**要下載資產，請執行以下步驟：**

1. 在左上角，按一下徽標。 在左滑軌中，按一下 **[!UICONTROL 導航]**。
1. 在 [!UICONTROL 導航] 的 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 導航到包含要下載的資產的資料夾。
1. 選擇資料夾或在資料夾中選擇一個或多個資產。
1. 在工具欄上，按一下 **[!UICONTROL 下載]**。
1. 在「下載」對話框中，選擇所需的下載選項。

   | 導出或下載選項 | 說明 |
   |---|---|
   | **[!UICONTROL 為每一個資產建立個別的資料夾]** | 選擇此選項可將下載的每個資產包括在嵌套在資產父資料夾下的子資料夾中的資產包括在本地電腦上的一個資料夾中。 如果未選擇此選項，預設情況下將忽略資料夾層次結構，並將所有資產下載到本地電腦中的一個資料夾中。 |
   | **[!UICONTROL 電子郵件]** | 向用戶發送電子郵件通知。 標準電子郵件模板可在以下位置使用：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 在部署過程中自定義的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在以下位置儲存特定於租戶的自定義模板：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 資產]** | 選擇此選項可以以原始格式下載資產，而不包含任何格式副本。<br>如果原始資產具有子資產，則子資產選項可用。 |
   | **[!UICONTROL 轉譯]** | 轉譯是資產的二進位表示法。資產具有主要表示形式 — 上載檔案的主要表示形式。 他們可以有任意數目的表示。 <br> 通過此選項，您可以選擇要下載的格式副本。 可用的格式副本取決於您選擇的資產。 如果資產具有任何格式副本，則此選項可用。 |
   | **[!UICONTROL 智慧裁切]** | 選擇此選項可從中下載選定資產的所有智慧裁剪格式副AEM本。 將建立帶有智慧裁剪格式副本的zip檔案並將其下載到您的本地電腦。 |
   | **[!UICONTROL 動態轉譯]** | 選擇此選項可即時生成一系列替代格式副本。 選擇此選項後，您還可以通過從 [影像預設](image-presets.md) 清單框。 <br>此外，還可以選擇大小和測量單位、格式、顏色空間、解析度以及任何可選的影像修飾符（如反相影像）。 僅當您 [!DNL Dynamic Media] 啟用。 |

1. 在對話框中，按一下 **[!UICONTROL 下載]**。

選擇要下載的資料夾後，將下載資料夾下的完整資產層次結構。 要將下載的每個資產（包括嵌套在父資料夾下的子資料夾中的資產）包括在單個資料夾中，請選擇 **[!UICONTROL 為每個資產建立單獨的資料夾]**。

## 啟用資產下載servlet {#enable-asset-download-servlet}

中的預設servlet [!DNL Experience Manager] 允許經過身份驗證的用戶發出任意大的併發下載請求，以建立他們可見的資產的ZIP檔案，這些檔案可能會使伺服器和網路過載。 為降低此功能導致的潛在DoS風險， `AssetDownloadServlet` 預設情況下，OSGi元件對於發佈實例是禁用的。

要允許從DAM下載資產，例如，當使用諸如資產共用共用或其他類似門戶的實現時，請通過OSGi配置手動啟用servlet。 Adobe建議將允許的下載大小設定得盡可能低，而不影響日常下載要求。 高值可能會影響效能。

1. 建立具有針對發佈運行模式的命名約定的資料夾(`config.publish`): `/apps/<your-app-name>/config.publish`。 要為運行模式定義配置屬性，請參見 [運行模式](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)。
1. 在配置資料夾中，建立類型檔案 `nt:file` 命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。
1. 填充 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 下面。 將下載的最大大小（以位元組為單位）設定為 `asset.download.prezip.maxcontentsize`。 下面的示例將ZIP下載的最大大小配置為不超過100 kB。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

預設情況下， `GET` 請求下載檔案， [!DNL Experience Manager] 對ZIP存檔的下載大小強制實施50 MB的限制。 通過 `POST` 請求或用戶介面不受此限制的影響。

## 禁用資產下載servlet {#disable-asset-download-servlet}

的 `Asset Download Servlet` 可在 [!DNL Experience Manager] 通過更新調度程式配置來發佈實例以阻止任何資產下載請求。 也可以通過OSGi控制台直接手動禁用servlet。

1. 要通過調度程式配置阻止資產下載請求，請編輯 `dispatcher.any` 配置並向其中添加規則 [過濾段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)。 `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 要在發佈實例上禁用OSGi元件，請訪問OSGi控制台 `http://[aem_server]:[port]/system/console/components`。 定位 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` 按一下 **[!UICONTROL 禁用]**。

>[!MORELIKETHIS]
>
>* [使用Brand Portal下載資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [下載受DRM保護的資產](drm.md)。
>* [在Win或Mac案頭上使用Experience Manager案頭應用下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)。
>* [使用受支援的Adobe Creative Cloud應用中的Adobe資產連結下載資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)。

