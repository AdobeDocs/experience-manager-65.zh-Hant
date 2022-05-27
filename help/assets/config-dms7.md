---
title: 配置Dynamic Media-Scene7模式
description: 瞭解如何配置Dynamic Media-Scene7模式。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
source-git-commit: b14cbc4cad15b06754db8b8c992a596d4d64c096
workflow-type: tm+mt
source-wordcount: '6037'
ht-degree: 3%

---

# 配置Dynamic Media-Scene7模式{#configuring-dynamic-media-scene-mode}

如果您使用Adobe Experience Manager設定用於不同的環境，例如開發、試運行和生產，請為這些環境中的每個環境配置Dynamic MediaCloud Services。

## Dynamic Media-Scene7模式的體系結構圖 {#architecture-diagram-of-dynamic-media-scene-mode}

以下體系結構圖描述了Dynamic Media-Scene7模式的工作原理。

有了新的體系結構，Experience Manager負責主要來源資產，並與Dynamic Media進行資產處理和發佈同步：

1. 將主源資產上載到Experience Manager時，將其複製到Dynamic Media。 此時，Dynamic Media將處理所有資產處理和格式副本生成，如視頻編碼和影像的動態變型。
(在Dynamic Media-Scene7模式下，預設上載檔案大小為2 GB或更小。 要啟用2 GB到15 GB的上載檔案大小，請參見 [（可選）配置Dynamic Media-Scene7模式以上載大於2 GB的資產](#optional-config-dms7-assets-larger-than-2gb)。)
1. 生成格式副本後，Experience Manager可以安全訪問和預覽遠程Dynamic Media格式副本(不會將二進位檔案發回到Experience Manager實例)。
1. 在內容準備好發佈和批准後，它將觸發Dynamic Media服務，將內容推送到CDN（內容分發網路）上的分發伺服器並快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>以下功能清單要求您使用與Adobe Experience Manager-Dynamic Media捆綁的現成CDN。 這些功能不支援任何其他自定義CDN。
>
>* [智慧型影像](/help/assets/imaging-faq.md)
>* [快取無效](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [熱鏈路保護](/help/assets/hotlink-protection.md)
>* [HTTP/2 內容傳送](/help/assets/http2.md)
>* CDN級別的URL重定向
>* Akamai ChinaCDN（在中國實現最佳交付）


## 在Scene7模式下啟用Dynamic Media {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 預設情況下為禁用。 要利用Dynamic Media功能，必須啟用它。

>[!WARNING]
>
>Dynamic Media-Scene7模式是 *Experience Manager作者實例*。 因此，必須配置 `runmode=dynamicmedia_scene7` Experience Manager作家案， *不* Experience Manager發佈實例。

要啟用Dynamic Media，請使用 `dynamicmedia_scene7` 在終端窗口中輸入以下命令行運行模式（使用的埠示例為4502）:

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （可選）將Dynamic Media預設和配置從6.3遷移到6.5零停機時間 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

將Experience ManagerDynamic Media從6.3升級到6.4或6.5，現在包括零停機部署的能力。 從遷移所有預設和配置 `/etc` 至 `/conf` 在CRXDE Lite中，確保運行以下curl命令。

>[!NOTE]
>
>如果您在相容模式下運行Experience Manager實例，則無需運行這些命令。

對於所有升級，無論是否具有相容性軟體包，您都可以通過運行以下Linux® curl命令來複製Dynamic Media最初附帶的預設現成查看器預設：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

遷移您從中建立的任何自定義查看器預設和配置 `/etc` 至 `/conf`，運行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 安裝功能包18912以進行批量資產遷移 {#installing-feature-pack-for-bulk-asset-migration}

安裝功能包18912 *可選*。

功能包18912允許您通過FTP批量接收資產，或將資產從Dynamic Media — 混合模式或Dynamic Media Classic遷移到Dynamic Media-Scene7-Experience Manager模式。 可從 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)。

請參閱 [安裝功能包18912以進行批量資產遷移](/help/assets/bulk-ingest-migrate.md) 的子菜單。

## 在Cloud Services中建立Dynamic Media配置 {#configuring-dynamic-media-cloud-services}

**在配置Dynamic Media之前**  — 在您收到具有Dynamic Media憑據的預配電子郵件後，必須開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄帳戶以更改密碼。 預配電子郵件中提供的密碼是系統生成的，僅用於臨時密碼。 更新密碼以使用正確的憑據設定Dynamic MediaCloud Service非常重要。

![動態媒體配置更新](assets/dynamicmediaconfiguration2updated.png)

**要在Cloud Services中建立Dynamic Media配置：**

1. 在「Experience Manager作者」模式下，選擇Experience Manager徽標以訪問全局導航控制台，然後選擇「工具」表徵圖，然後轉到 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media配置]**。
1. 在「Dynamic Media配置瀏覽器」頁面的左窗格中，選擇 **[!UICONTROL 全球]** (不選擇資料夾表徵圖 **[!UICONTROL 全球]**)，然後選擇 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立Dynamic Media配置]** 頁，輸入標題、Dynamic Media帳戶電子郵件地址、密碼，然後選擇您的區域。 此資訊是通過Adobe在預配電子郵件中提供給您的。 如果您未收到電子郵件，請與Adobe客戶支援聯繫。

   選擇 **[!UICONTROL 連接到Dynamic Media]**。

   >[!NOTE]
   在您收到帶有Dynamic Media憑據的預配電子郵件後，開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄帳戶以更改密碼。 預配電子郵件中提供的密碼是系統生成的，僅用於臨時密碼。 更新密碼以使用正確的憑據設定Dynamic MediaCloud Service非常重要。

1. 連接成功後，請設定以下內容。 需要帶星號(*)的標題：

   * **[!UICONTROL 公司]** -Dynamic Media帳戶的名稱。 你有多個Dynamic Media賬戶。 例如，您可以有不同的子品牌、分部、分段或生產環境。

   <!-- UNHIDE FEBRUARY 24, 2022 See also [Configure Dynamic Media company alias account](/help/assets/dm-alias-account.md). -->

   * **[!UICONTROL 公司根資料夾路徑]**

   * **[!UICONTROL 發佈資產]**  — 您可以從以下三個選項中進行選擇：
      * **[!UICONTROL 立即]** 即當上載資產時，系統會立即接收資產並提供URL/Embed。 發佈資產不需要用戶干預。
      * **[!UICONTROL 激活後]** 表示在提供URL/嵌入連結之前，必須先顯式發佈資產。<br><!-- CQDOC-17478, Added March 9, 2021-->從Experience Manager6.5.8開始，Experience Manager發佈實例將反映準確的Dynamic Media元資料值，如 `dam:scene7Domain` 和 `dam:scene7FileStatus` 在 **[!UICONTROL 激活後]** 僅發佈模式。 要啟用此功能，請安裝Service Pack 8，然後重新啟動Experience Manager。 轉至Sling Config Manager。 查找配置 `Scene7ActivationJobConsumer Component` 或建立新的)。 選中複選框 **[!UICONTROL 在Dynamic Media發佈後複製元資料]**，然後選擇 **[!UICONTROL 保存]**。

         ![「在Dynamic Media發佈後複製元資料」複選框](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 選擇性發佈]** 此選項允許您控制在Dynamic Media發佈的資料夾。 它允許您使用智慧裁剪或動態格式副本等功能，或確定以Experience Manager形式僅發佈哪些資料夾以進行預覽。 這些資產 *不* 在Dynamic Media發佈，供在公共領域傳遞。<br>您可以在 **[!UICONTROL Dynamic Media雲配置]** 或者，如果您願意，可以選擇在資料夾的資料夾級別設定此選項 **[!UICONTROL 屬性]**。<br>請參閱 [與選擇性出版合作在Dynamic Media](/help/assets/selective-publishing.md)。<br>如果以後更改此配置，或以後在資料夾級別更改它，則這些更改僅影響從該點向前上載的新資產。 資料夾中現有資產的發佈狀態保持原樣，直到您手動將其從以下任一資料夾 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理發布]** 對話框。
   * **[!UICONTROL 安全預覽伺服器]**  — 用於指定安全格式副本預覽伺服器的URL路徑。 即，生成格式副本後，Experience Manager可以安全訪問和預覽遠程Dynamic Media格式副本(不會將二進位檔案發回到Experience Manager實例)。
除非您有使用自己公司伺服器或特殊伺服器的特殊安排，否則Adobe建議您保留指定的此設定。

   * **[!UICONTROL 同步所有內容]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->預設選擇。 如果要有選擇地包括或排除同步到Dynamic Media的資產，請取消選擇此選項。 取消選擇此選項允許您從以下兩種Dynamic Media同步模式中進行選擇：

   * **[!UICONTROL Dynamic Media 同步處理模式]**
      * **[!UICONTROL 預設啟用]**  — 預設情況下，該配置將應用於所有資料夾，除非您專門將資料夾標籤為排除。 <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 預設禁用]**  — 在明確標籤要同步到Dynamic Media的選定資料夾之前，不會將配置應用於任何資料夾。
要將所選資料夾標籤為同步到Dynamic Media，請選擇資產資料夾，然後在工具欄上，選擇 **[!UICONTROL 屬性]**。 在 **[!UICONTROL 詳細資訊]** 的 **[!UICONTROL Dynamic Media同步模式]** 下拉清單中，從以下三個選項中選擇。 完成後，選擇 **[!UICONTROL 保存]**。 *記住：如果您選擇了&#x200B;**[!UICONTROL 同步所有內容]**早些。* 另請參閱 [在Dynamic Media的資料夾級別使用「選擇性發佈」](/help/assets/selective-publishing.md)。
         * **[!UICONTROL 繼承]**  — 資料夾上沒有顯式同步值；相反，資料夾會從其祖先資料夾或雲配置中的預設模式繼承同步值。 通過工具提示顯示繼承的詳細狀態。
         * **[!UICONTROL 啟用子資料夾]**  — 包括此子樹中的所有內容以同步到Dynamic Media。 特定於資料夾的設定會覆蓋雲配置中的預設模式。
         * **[!UICONTROL 已禁用子資料夾]**  — 從同步到Dynamic Media中排除此子樹中的所有內容。

   >[!NOTE]
   不支援在Dynamic Media-Scene7模式下進行版本控制。 此外，延遲啟動僅適用於在「編輯動態媒體設定」頁面中的「發佈資產 ********」設定為「啟動時」，然後只適用於在首次啟動資產時。
   激活資產後，任何更新都會立即即時發佈到S7交付。

1. 選擇 **[!UICONTROL 保存]**。
1. 要在發佈Dynamic Media內容之前安全地預覽它，Experience Manager作者使用基於令牌的驗證，因此，預設情況下Experience Manager作者預覽Dynamic Media內容。 但是，您可以允許列出更多IP，以便用戶能夠安全地預覽內容。 要在Experience Manager中設定此操作，請參閱 [配置Dynamic Media映像伺服器的發佈設定 — 安全頁籤](/help/assets/dm-publish-settings.md#security-tab)。

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

現在您完成了基本配置；您已準備好使用Dynamic Media-Scene7模式。

如果要進一步自定義配置，您可以選擇完成以下任務 [（可選）在Dynamic Media-Scene7模式下配置高級設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)。

## （可選）在Dynamic Media-Scene7模式下配置高級設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

如果要進一步自定義Dynamic Media-Scene7模式的配置和設定，或優化其效能，可以完成以下一個或多個操作： *可選* 任務：

* [（可選）配置Dynamic Media-Scene7模式以上載大於2 GB的資產](#optional-config-dms7-assets-larger-than-2gb)

* [（可選）Dynamic Media-Scene7模式設定的設定和配置](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（可選）調整Dynamic Media-Scene7模式的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（可選）篩選複製資產](#optional-filtering-assets-for-replication)

### （可選）配置Dynamic Media-Scene7模式以上載大於2 GB的資產 {#optional-config-dms7-assets-larger-than-2gb}

在Dynamic Media-Scene7模式下，預設資產上載檔案大小為2 GB或更小。 但是，您可以根據需要配置大於2 GB和高達15 GB的資產的上載。

如果要使用此功能，請注意以下先決條件和要點：

* 您必須在Dynamic Media-Scene7模式下運行帶Service Pack 6.5.4.0或更高版本的Experience Manager6.5。
* 僅支援此大型上載功能 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 客戶。
* 請確保您的Experience Manager實例已配置AmazonS3或Microsoft® Azure Blob儲存。

   >[!NOTE]
   使用訪問密鑰和密鑰配置Azure Blob儲存，因為Blob儲存配置中的AzureSas不支援此大型上載功能。

* 橡樹 [直接二進位訪問下載](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) 已啟用(Oak *直接二進位訪問上載* 不需要)。

   要啟用直接二進位訪問下載，請設定屬性 `presignedHttpDownloadURIExpirySeconds > 0` 在資料儲存配置中。 值應足夠長，以便下載較大的二進位檔案並可能重試。

* 未上載大於15 GB的資產。 （大小限制在下面的步驟8中設定。）
* 當 **[!UICONTROL Dynamic Media重新處理]** 資產工作流在資料夾上觸發，它會重新處理任何已與Dynamic Media公司同步的大型資產。 但是，如果資料夾中尚未同步任何大型資產，則不會上載該資產。 因此，要同步Dynamic Media的現有大型資產，您可以運行 **[!UICONTROL Dynamic Media重新處理]** 單個資產的資產工作流。

**要配置Dynamic Media-Scene7模式以上載大於2 GB的資產，請執行以下操作：**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，然後導航至 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。

1. 在「CRXDE Lite」窗口中，執行下列任一操作：

   * 在左滑軌中，導航到以下路徑：

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 將上面的路徑複製並貼上到工具欄下方的CRXDE Lite路徑欄位中，然後按 `Enter`。

1. 在左滑軌中，按一下右鍵 `fileupload`，然後從彈出菜單中選擇 **[!UICONTROL 覆蓋節點]**。

   ![覆蓋節點選項](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 在「覆蓋節點」(Overlay Node)對話框上，選擇 **[!UICONTROL 匹配節點類型]** 複選框以啟用（開啟）選項，然後選擇 **[!UICONTROL 確定]**。

   ![「覆蓋節點」對話框](/help/assets/assets-dm/uploadassets15gb_b.png)

1. 在「CRXDE Lite」窗口中，執行以下任一操作：

   * 在左滑軌中，導航到以下覆蓋節點路徑：

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 將上面的路徑複製並貼上到工具欄下方的CRXDE Lite路徑欄位中，然後按 `Enter`。

1. 在 **[!UICONTROL 屬性]** 頁籤 **[!UICONTROL 名稱]** 列，定位 `sizeLimit`。
1. 在 `sizeLimit` 名稱，在 **[!UICONTROL 值]** 列，按兩下「值」欄位。
1. 輸入相應的值（以位元組為單位），以便將大小限制增加到所需的最大上載大小。 例如，要將上載資產大小限制增加到10 GB，請輸入 `10737418240` 的子菜單。
您可以輸入最大15 GB(`2013265920` 位元組)。 在這種情況下，上載的大於15 GB的資產不會上載。

   ![大小限制值](/help/assets/assets-dm/uploadassets15gb_c.png)

1. 在CRXDE Lite窗口的左上角附近，選擇 **[!UICONTROL 全部保存]**。

   *現在，通過執行以下操作來設定Adobe花崗岩工作流外部進程作業處理程式的超時：*

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台。
1. 執行下列任一操作：

   * 導航到以下URL路徑：

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 將上面的路徑複製並貼上到瀏覽器的URL欄位中。 確保替換 `localhost:4502` 你自己的Experience Manager。

1. 在 **[!UICONTROL Adobe花崗岩工作流外部進程作業處理程式]** 對話框 **[!UICONTROL 最大超時]** 欄位，將值設定為 `18000` 分鐘（五小時）。 預設為10800分鐘（3小時）。

   ![最大超時值](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 在對話框的右下角，選擇 **[!UICONTROL 保存]**。

   *現在，通過執行以下操作來設定Scene7直接二進位上載進程步驟的超時：*

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台。
1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在「工作流模型」頁面上，選擇 **[!UICONTROL Dynamic Media編碼視頻]**。
1. 在工具欄上，選擇 **[!UICONTROL 編輯]**。
1. 在工作流頁面上，按兩下 **[!UICONTROL Scene7直接二進位上載]** 處理步驟。
1. 在 **[!UICONTROL 步驟屬性]** 對話框 **[!UICONTROL 常用]** 頁籤 **[!UICONTROL 高級設定]** 標題 **[!UICONTROL 超時]** 欄位，輸入 `18000` 分鐘（五小時）。 預設值為 `3600` 分鐘（1小時）。
1. 選擇 **[!UICONTROL 確定]**。
1. 選擇 **[!UICONTROL 同步]**。
1. 對於 **[!UICONTROL DAM更新資產]** 工作流模型和 **[!UICONTROL Dynamic Media重新處理]** 工作流模型。

### （可選）Dynamic Media-Scene7模式設定的設定和配置 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [為映像伺服器配置Dynamic Media發佈設定](/help/assets/dm-publish-settings.md)
* [配置Dynamic Media常規設定](/help/assets/dm-general-settings.md)
* [配置顏色管理](#configuring-color-management)
* [編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)
* [為不支援的格式添加MIME類型](#adding-mime-types-for-unsupported-formats)
* [建立批集預設以自動生成影像集和旋轉集](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (在Dynamic Media Classic用戶介面中完成)

#### 為映像伺服器配置Dynamic Media發佈設定 {#publishing-setup-for-image-server}

「Dynamic Media發佈設定」頁建立預設設定，確定如何將資產從AdobeDynamic Media伺服器傳送到網站或應用程式。

請參閱 [為映像伺服器配置Dynamic Media發佈設定](/help/assets/dm-publish-settings.md)。

#### 配置Dynamic Media常規設定 {#configuring-application-general-settings}

配置Dynamic Media **[!UICONTROL 發佈伺服器名稱]** URL和 **[!UICONTROL 源伺服器名稱]** URL。 也可以指定 **[!UICONTROL 上載到應用程式]** 設定和 **[!UICONTROL 預設上載選項]** 都取決於您的特定用例。

請參閱 [配置Dynamic Media常規設定](/help/assets/dm-general-settings.md)。

#### 配置顏色管理 {#configuring-color-management}

Dynamic Media色彩管理允許您對正確的資產進行色彩調整。 通過顏色校正，攝取的資產保留其顏色空間(RGB、CMYK、灰色)和嵌入的顏色配置檔案。 請求動態格式副本時，影像顏色將使用CMYK、RGB或「灰色」輸出更正為目標顏色空間。

請參閱 [配置影像預設](/help/assets/managing-image-presets.md)。

>[!NOTE]
預設情況下，當您選擇 **[!UICONTROL 格式副本]** 和15個查看器預設 **[!UICONTROL 查看者]** 的子菜單。 您可以提高此限制。請參閱 [增加顯示的影像預設數](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 或 [增加顯示的查看器預設數](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)。

#### 編輯支援格式的MIME類型 {#editing-mime-types-for-supported-formats}

您可以定義由Dynamic Media處理的資產類型，並自定義高級資產處理參數。 例如，您可以指定資產處理參數以執行以下操作：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop文檔(.PSD)轉換為橫幅模板資產以進行個性化。
* 柵格化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝的PostScript®檔案(.EPS)。
* [視頻配置檔案](/help/assets/video-profiles.md) 和 [成像配置檔案](/help/assets/image-profiles.md) 可以分別定義視頻和影像的處理。

請參閱 [上載資產](/help/assets/manage-assets.md#uploading-assets)。

**要編輯支援格式的MIME類型：**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，然後導航至 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 在左滑軌中，導航到以下位置：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME類型](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選擇MIME類型。
1. 在CRXDE Lite頁的右側，在下部：

   * 按兩下 **[!UICONTROL 啟用]** 的子菜單。 預設情況下，所有資產MIME類型都已啟用(設定為 **[!UICONTROL 真]**)，這意味著這些資產被同步到Dynamic Media進行處理。 如果要排除此資產mime類型，請將此設定更改為 **[!UICONTROL 假]**。

   * 按兩下 **[!UICONTROL jobParam]** 開啟其關聯的文本欄位。 請參閱 [支援的MIME類型](/help/assets/assets-formats.md#supported-mime-types) 可用於給定mime類型的允許處理參數值清單。

1. 執行下列任一項作業：

   * 重複步驟3-4以編輯更多MIME類型。
   * 在CRXDE Lite頁的菜單欄上，選擇 **[!UICONTROL 全部保存]**。

1. 在頁面的左上角，選擇 **[!UICONTROL CRXDE Lite]** 回到Experience Manager。

#### 添加不支援格式的MIME類型 {#adding-mime-types-for-unsupported-formats}

您可以為Experience Manager Assets不支援的格式添加自定義MIME類型。 通過在CRXDE Lite之前移動MIME類型，確保Experience Manager不會刪除添加到中的任何新節點 `image_`。 另外，請確保其啟用值設定為 **[!UICONTROL 假]**。

**要為不支援的格式添加MIME類型：**

1. 從Experience Manager，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 將開啟新的瀏覽器頁籤 **[!UICONTROL Adobe Experience ManagerWeb控制台配置]** 的子菜單。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，向下捲動至名稱 *Adobe CQ Scene7 Asset MIME類型Service* ，如下列螢幕擷取所示。在名稱右側，選擇 **[!UICONTROL 編輯配置值]** （鉛筆表徵圖）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在 **Adobe CQScene7資產MIME類型服務** 的上界。 在表中選擇加號以添加新MIME類型的位置很瑣碎。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 類型 `DWG=image/vnd.dwg` 的子菜單。

   示例 `DWG=image/vnd.dwg` 僅用於演示。 您在此處添加的MIME類型可以是任何其他不受支援的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，選擇 **[!UICONTROL 保存]**。

   此時，您可以關閉瀏覽器頁籤，該頁籤具有開啟的Adobe Experience ManagerWeb控制台配置頁。

1. 返回到開啟的Experience Manager控制台的瀏覽器頁籤。
1. 從Experience Manager，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左滑軌中，導航到以下位置：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖動MIME類型 `image_vnd.dwg` 然後直接放在上面 `image_` 在樹中顯示，如下面的螢幕截圖所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 使用MIME類型 `image_vnd.dwg` 從 **[!UICONTROL 屬性]** 的 **[!UICONTROL 啟用]** 行，在 **[!UICONTROL 值]** 列標題，按兩下該值以開啟 **[!UICONTROL 值]** 的子菜單。
1. 類型 `false` 的 **[!UICONTROL 假]** )。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite頁的左上角附近，選擇 **[!UICONTROL 全部保存]**。

#### 建立批集預設以自動生成影像集和旋轉集 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

使用批集預設在資產上載到Dynamic Media時自動建立影像集或旋轉集。

首先，定義資產在集中分組的命名約定。 然後建立一個批集預設，該預設是唯一命名的、自包含的指令集。 它必須定義如何使用與預設配方中定義的命名約定相匹配的影像構建集。

上載檔案時，Dynamic Media會自動建立一個集，其中包含所有與活動預設中定義的命名約定相匹配的檔案。

##### 配置預設命名

建立用於任何批集預設處方的預設命名約定。 在批處理集預設定義中選擇的預設命名約定可能是您公司為批處理生成集所需的全部。 建立批處理集預設以使用您定義的預設命名約定。 在公司定義的預設命名存在例外的情況下，您可以建立具有特定內容集所需的備用自定義命名約定的盡可能多的批集預設。

雖然設定預設命名約定不需要使用批處理集預設功能，但最佳實踐建議您使用預設命名約定。 它允許您定義要分組到一個集中的命名約定的任意多個元素，以便可以簡化批集建立。

作為替代方法，您可以 **[!UICONTROL 查看代碼]** 沒有可用的表單域。 在此視圖中，您完全使用規則運算式建立命名約定定義。

兩個元素可用於定義，即「匹配」和「基本名稱」。 通過這些欄位，您可以定義命名約定的所有元素，並標識用於命名其所包含集的約定的部分。 公司的單個命名約定通常為這些元素中的每個元素使用一條或多條定義線。 您可以使用任意多行進行唯一定義，並將它們分組為不同的元素，如主影像、顏色元素、替代視圖元素和色板元素。

**配置預設命名：**

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的帳戶。

   您的憑據和登錄詳細資訊是在設定時由Adobe提供的。 如果您沒有此資訊，請與Adobe客戶支援聯繫。

1. 在頁面頂部附近的導航欄上，導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批集預設]** > **[!UICONTROL 預設命名]**。
1. 選擇 **[!UICONTROL 「查看表單]** 」或「 **[!UICONTROL 查看代碼」]** ，以指定要查看的方式並輸入有關每個元素的資訊。

   可以選擇 **[!UICONTROL 查看代碼]** 框中，選擇「 CSV文本」。 如果表單視圖因任何原因限制您，則可以輸入或更改這些值以幫助定義命名約定的元素。 如果無法在表單視圖中分析您的值，則表單欄位將變為非活動狀態。

   >[!NOTE]
   取消激活的表單域不會驗證規則運算式是否正確。 在「結果」(Result)行後，將看到要為每個元素生成的規則運算式的結果。 完整的規則運算式在頁面底部可見。

1. 根據需要展開每個元素並輸入要使用的命名約定。
1. 如有必要，請執行以下任一操作：

   * 選擇 **[!UICONTROL 添加]** 為元素添加其他命名約定。
   * 選擇 **[!UICONTROL 刪除]** 刪除元素的命名約定。

1. 執行下列任一項作業：

   * 選擇 **[!UICONTROL 另存為]** 鍵入預設的名稱。
   * 選擇 **[!UICONTROL 保存]** 編輯現有預設。

##### 建立批集預設

Dynamic Media使用批集預設將資產組織成一組影像（替代影像、顏色選項、360旋轉），以在查看器中顯示。 批集預設在Dynamic Media的資產上載流程旁邊自動運行。

您可以建立、編輯和管理批集預設。 有兩種形式的批集預設定義：一個用於可設定的預設命名約定，另一個用於即時建立的自定義命名約定。

您可以使用表單域方法定義批集預設或使用規則運算式的代碼方法。 與預設命名中一樣，您可以在表單視圖中定義的同時選擇查看代碼，並使用規則運算式來生成定義。 或者，您也可以取消選中任一視圖以獨佔使用一個視圖或另一個視圖。

**要建立批集預設，請執行以下操作：**

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的帳戶。

   您的憑據和登錄詳細資訊是在設定時由Adobe提供的。 如果您沒有此資訊，請與Adobe客戶支援聯繫。

1. 在頁面頂部附近的導航欄上，導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批集預設]** > **[!UICONTROL 批集預設]**。

   **[!UICONTROL 查看窗體]**，如「詳細資訊」(Details)頁面右上角所設定，則為預設視圖。

1. 在「預設清單」面板中，選擇 **[!UICONTROL 添加]** 激活螢幕右側「詳細資訊」面板中的定義欄位。
1. 在「詳細資訊」面板的「預設名稱」欄位中，鍵入預設的名稱。
1. 在「批集類型」下拉菜單中，選擇預設類型。
1. 執行下列任一項作業：

   * 如果您使用的是先前在以下位置設定的預設命名約定 **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批集預設]** > **[!UICONTROL 預設命名]**&#x200B;展開 **[!UICONTROL 資產命名約定]**，然後在「檔案命名」下拉清單中，選擇 **[!UICONTROL 預設]**。

   * 要在設定預設時定義新命名約定，請展開 **[!UICONTROL 資產命名約定]**，然後在「檔案命名」下拉清單中，選擇 **[!UICONTROL 自定義]**。

1. 對於「序列」順序，定義在將影像集分組到Dynamic Media後顯示影像的順序。

   預設情況下，資產按字母數字順序排列。 但是，可以使用逗號分隔的規則運算式清單來定義順序。

1. 對於設定命名和建立約定，指定在資產命名約定中定義的基本名稱的尾碼或前置詞。 此外，定義在Dynamic Media資料夾結構中建立集的位置。

   如果定義了大量集，請將集與包含資產本身的資料夾分開。 例如，建立「影像集」資料夾並將生成的集放在此處。

1. 在「詳細資訊」面板中，選擇 **[!UICONTROL 保存]**。
1. 選擇 **[!UICONTROL 活動]** 的子菜單。

   激活預設可確保在將資產上載到Dynamic Media時，應用批集預設來生成該集。

##### 為自動生成2D旋轉集建立批集預設

您可以使用批集類型 **[!UICONTROL 多軸旋轉集]** 建立可自動生成2D旋轉集的處方。 影像分組使用行和列規則運算式，以便影像資產在多維陣列中的相應位置中正確對齊。 在多軸旋轉集中，不存在必須具有的最小或最大行數或列數。

例如，假設要建立名為 `spin-2dspin`。 您有一組包含三行的旋轉集影像，每行有12個影像。 影像的命名如下：

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

使用此資訊，您可以按如下方式建立批集類型處方：

![chlimage_1-560](assets/chlimage_1-560.png)

將旋轉集的共用資產名稱部分的分組添加到 **[!UICONTROL 匹配]** 欄位（突出顯示）。 包含行和列的資產名稱的變數部分將分別添加到 **[!UICONTROL 行]** 和 **[!UICONTROL 列欄位中]** 。

上傳和發佈回轉集時，您會啟用「上傳工作選項」對話方塊中「批次集預設集」下方所列的2D回轉集 **[!UICONTROL 方式名稱]****** 。

**要為自動生成2D旋轉集建立批集預設：**

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的帳戶。

   您的憑據和登錄詳細資訊是在設定時由Adobe提供的。 如果您沒有此資訊，請與Adobe客戶支援聯繫。

1. 在頁面頂部附近的導航欄上，導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批集預設]** > **[!UICONTROL 批集預設]**。

   **[!UICONTROL 查看窗體]**，如「詳細資訊」(Details)頁面右上角所設定，則為預設視圖。

1. 在「預設清單」面板中，選擇 **[!UICONTROL 添加]** 激活螢幕右側「詳細資訊」面板中的定義欄位。
1. 在「詳細資訊」面板的「預設名稱」欄位中，鍵入預設的名稱。
1. 在「批集類型」下拉式功能表中，選擇「資產 **[!UICONTROL 集」]**。
1. 在「子類型」(Sub Type)下拉清單中，選擇 **[!UICONTROL 多軸旋轉集]**。
1. 展開 **[!UICONTROL 資產命名約定]**，然後在「檔案命名」下拉清單中，選擇 **[!UICONTROL 自定義]**。
1. 使用「 **[!UICONTROL 比對]** 」(Match **[!UICONTROL )和 (可選) 「基本名稱]** 」(Base Name)屬性，定義組成群組之影像資產的命名規則運算式。

   例如，字面「匹配」規則運算式可以如下所示：

   `(w+)-w+-w+`

1. 展開 **[!UICONTROL 行列位置]**，然後定義影像資產在2D旋轉集陣列中的位置的名稱格式。

   使用括弧將行或列置於檔案名中。

   例如，對於行規則運算式，它可以如下所示：

   `\w+-R([0-9]+)-\w+`

   或

   `\w+-(\d+)-\w+`

   對於列規則運算式，它可以如下所示：

   `\w+-\w+-C([0-9]+)`

   或

   `\w+-\w+-C(\d+)`

   以上示例僅供演示之用。 您可以建立規則運算式，但是您需要。

   >[!NOTE]
   如果行和列規則運算式的組合無法確定資產在多維旋轉集陣列中的位置，則不會將資產添加到該集。 還記錄錯誤。

1. 對於設定命名和建立約定，指定在資產命名約定中定義的基本名稱的尾碼或前置詞。

   同時，定義在Dynamic Media Classic資料夾結構中建立旋轉集的位置。

   如果定義了大量集，請將集與包含資產本身的資料夾分開。 例如，建立一個「旋轉集」資料夾，將生成的集放在此處。

1. 在「詳細資訊」面板中，選擇 **[!UICONTROL 保存]**。
1. 選擇 **[!UICONTROL 活動]** 的子菜單。

   激活預設可確保在將資產上載到Dynamic Media時，應用批集預設來生成該集。

### （可選）調整Dynamic Media-Scene7模式的效能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為了保持Dynamic Media-Scene7模式平穩運行，Adobe建議使用以下同步效能/可擴充性微調提示：

* 更新預定義的作業參數以處理不同的檔案格式。
* 更新預定義的Granite工作流（視頻資產）隊列工作線程。
* 更新預定義的Granite瞬態工作流（影像和非視頻資產）隊列工作線程。
* 正在更新到Dynamic Media Classic伺服器的最大上載連接。

#### 更新預定義的作業參數以處理不同的檔案格式

您可以在上載檔案時調整作業參數以加快處理速度。 例如，如果上載PSD檔案，但不想將其作為模板處理，則可以將圖層提取設定為false(off)。 在這種情況下，調諧的作業參數如下所示： `process=None&createTemplate=false`。

如果確實要開啟模板建立，請使用以下參數： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建議對PDF、PostScript®和PSD檔案使用以下「調諧」作業參數：

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 檔案類型 | 建議的作業參數 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新這些參數中的任何一個，請按照中的步驟操作 [啟用基於MIME類型的Assets/Dynamic Media Classic上載作業參數支援](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。

#### 更新Granite瞬態工作流隊列 {#updating-the-granite-transient-workflow-queue}

花崗岩傳輸工作流隊列用於 **[!UICONTROL DAM更新資產]** 工作流。 在Dynamic Media，它用於影像攝取和處理。

**要更新Granite瞬態工作流隊列，請執行以下操作：**

1. 導航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 並搜索 **隊列：花崗岩瞬態工作流隊列**。

   >[!NOTE]
   由於OSGi PID是動態生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大並行作業數]** 欄位中，將編號更改為所需的值。

   你可以增加 **[!UICONTROL 最大並行作業數]** 足以支援大量檔案上傳到Dynamic Media。 具體值取決於硬體容量。 在某些情況下 — 即初始遷移或一次性批量上載 — 您可以使用較大的值。 但請注意，使用大值（如內核數的兩倍）可能會對其他併發活動產生負面影響。 因此，根據您的特定使用情形test和調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 選擇 **[!UICONTROL 保存]**。

#### 更新Granite工作流隊列 {#updating-the-granite-workflow-queue}

花崗岩工作流隊列用於非暫態工作流。 在Dynamic Media，它用 **[!UICONTROL Dynamic Media編碼視頻]** 工作流。

**要更新Granite工作流隊列，請執行以下操作：**

1. 導航到 `https://<server>/system/console/configMgr` 並搜索 **隊列：花崗岩工作流隊列**。

   >[!NOTE]
   由於OSGi PID是動態生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大並行作業數]** 欄位中，將編號更改為所需的值。

   您可以增加最大並行作業數以充分支援將檔案重量上傳到Dynamic Media。 具體值取決於硬體容量。 在某些情況下 — 即初始遷移或一次性批量上載 — 您可以使用較大的值。 但請注意，使用大值（如內核數的兩倍）可能會對其他併發活動產生負面影響。 因此，根據您的特定使用情形test和調整值。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選擇 **[!UICONTROL 保存]**。

#### 更新Dynamic Media Classic上載連接 {#updating-the-scene-upload-connection}

Scene7上載連接設定將Experience Manager資產同步到Dynamic Media Classic伺服器。

**要更新Dynamic Media Classic上載連接：**

1. 導航到 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在 **[!UICONTROL 連接數]** 和/或 **[!UICONTROL 活動作業超時]** 欄位，根據需要更改數字。

   的 **[!UICONTROL 連接數]** 設定控制允許Experience Manager到Dynamic Media上載的HTTP連接的最大數量；通常，十個連接的預定義值就足夠了。

   的 **[!UICONTROL 活動作業超時]** 設定確定在傳遞伺服器中發佈上載的Dynamic Media資產的等待時間。 預設值為2100秒或35分鐘。

   對於大多數使用情形， 2100的設定已足夠。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 選擇 **[!UICONTROL 保存]**。

### （可選）篩選複製資產 {#optional-filtering-assets-for-replication}

在非Dynamic Media部署中，您可以複製 *全部* 從Experience Manager作者環境到「Experience Manager發佈」節點的資產（影像和視頻）。 此工作流是必需的，因為Experience Manager發佈伺服器也會傳遞資產。

但是，在Dynamic Media部署中，由於資產通過Cloud Service傳遞，因此不需要將這些資產複製到Experience Manager發佈節點。 這樣的「混合發佈」工作流避免了額外的儲存成本和複製資產所需的較長處理時間。 其他內容（如網站頁面）繼續從Experience Manager發佈節點提供。

過濾器為您提供了 *排除* 將資產複製到Experience Manager發佈節點。

#### 使用預設資產篩選器進行複製 {#using-default-asset-filters-for-replication}

如果將Dynamic Media用於成像或視頻，或同時使用兩者，則可以使用Adobe原樣提供的預設濾鏡。 預設情況下，以下篩選器處於活動狀態：

|  | 篩選 | Mime類型 | 轉譯 |
| --- | --- | --- | --- |
| Dynamic Media影像傳遞 | 濾波影像<br>過濾集 | 開始於 **影像/**<br>&#x200B;包含 **應用程式/** 結尾 **集**。 | 現成的「濾鏡影像」（適用於單個影像資產，包括互動式影像）和「濾鏡集」（適用於旋轉集、影像集、混合媒體集和旋轉盤集）將：<br>·從複製中排除原始映像和靜態映像格式副本。 |
| Dynamic Media視頻傳送 | 濾視 | 開始於 **視頻/** | 現成的「過濾視頻」將：<br>·從複製中排除原始視頻和靜態縮略圖格式副本。 |

>[!NOTE]
篩選器應用於MIME類型，且不能特定於路徑。

#### 自定義複製的資產篩選器 {#customizing-asset-filters-for-replication}

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 在左資料夾樹中，導航到 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` 來查看篩選器。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 要定義篩選器的Mime類型，可以按如下方式查找Mime類型：

   在左滑軌中，展開 `content > dam > <locate_your_asset> > jcr:content > metadata`，然後在表中找到 `dc:format`。

   下圖是資產路徑的示例 `dc:format`。

   ![chlimage_1-18](assets/chlimage_1-3.png)

   請注意 `dc:format` 為資產 `Fiji Red.jpg` 是 `image/jpeg`。

   要使此篩選器應用於所有影像，而不管其格式如何，請將值設定為 `image/*` 何處 `*` 是應用於任何格式的所有影像的規則運算式。

   要使篩選器僅應用於類型JPEG的影像，請輸入 `image/jpeg`。

1. 定義要包括或排除複製的格式副本。

   可用於篩選複製的字元包括：

   | 要使用的字元 | 它如何篩選資產以進行複製 |
   | --- | --- |
   | * | 萬用字元 |
   | + | 包括用於複製的資產 |
   | - | 從複製中排除資產 |

   導覽至 `content/dam/<locate your asset>/jcr:content/renditions`。

   下圖是資產格式副本的示例。

   ![chlimage-1-4](assets/chlimage_1-4.png)

   如果您只想複製原件，則 `+original`。
