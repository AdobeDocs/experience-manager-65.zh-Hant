---
title: 設定Dynamic Media - Scene7模式
description: 了解如何設定Dynamic Media - Scene7模式。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '6940'
ht-degree: 3%

---

# 設定Dynamic Media - Scene7模式{#configuring-dynamic-media-scene-mode}

如果您使用針對不同環境（例如開發、測試和生產）設定的Adobe Experience Manager，請針對其中每個環境設定Dynamic MediaCloud Services。

## Dynamic Media - Scene7模式的架構圖 {#architecture-diagram-of-dynamic-media-scene-mode}

以下架構圖表說明Dynamic Media - Scene7模式的運作方式。

透過新架構，Experience Manager負責主要來源資產，並與Dynamic Media同步處理及發佈資產：

1. 將主要來源資產上傳至Experience Manager時，資產會複製至Dynamic Media。 此時，Dynamic Media會處理所有資產處理和轉譯產生，例如影像的視訊編碼和動態變體。
(在Dynamic Media - Scene7模式中，預設上傳檔案大小為2 GB或更小。 若要啟用上傳檔案大小2 GB至15 GB，請參閱[（選用）設定Dynamic Media - Scene7模式，以上傳大於2 GB](#optional-config-dms7-assets-larger-than-2gb)的資產。)
1. 產生轉譯後，Experience Manager可以安全地存取和預覽遠端Dynamic Media轉譯(不會將任何二進位檔傳回至Experience Manager執行個體)。
1. 內容準備好發佈及核准後，就會觸發Dynamic Media服務將內容推送至傳遞伺服器，並在CDN（內容傳遞網路）快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>下列功能清單需要您使用隨附於Adobe Experience Manager - Dynamic Media的現成可用CDN。 這些功能不支援任何其他自訂CDN。
>
>* [智慧型影像](/help/assets/imaging-faq.md)
>* [快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [熱連結保護](/help/assets/hotlink-protection.md)
>* [HTTP/2 內容傳送](/help/assets/http2.md)
>* CDN層級的URL重新導向
>* Akamai ChinaCDN（以最佳方式在中國傳送）


## 在Scene7模式中啟用Dynamic Media {#enabling-dynamic-media-in-scene-mode}

[動態](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 媒體預設為停用。若要運用Dynamic Media功能，您必須啟用此功能。

>[!WARNING]
>
>Dynamic Media - Scene7模式僅適用於&#x200B;*Experience Manager製作例項*。 因此，您必須在「Experience Manager製作」例項上設定`runmode=dynamicmedia_scene7`，而不是&#x200B;*Experience Manager發佈例項。*

若要啟用Dynamic Media，您必須在終端視窗中輸入以下內容，從命令列使用`dynamicmedia_scene7`執行模式啟動Experience Manager（使用的範例埠為4502）:

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （選用）將Dynamic Media預設集和設定從6.3移轉至6.5零停機時間 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

將Experience ManagerDynamic Media從6.3升級至6.4或6.5，現在包含零停機部署的功能。 若要將所有預設集和設定從`/etc`移轉至CRXDE Lite中的`/conf`，請務必執行下列curl命令。

>[!NOTE]
>
>如果您以相容模式運行Experience Manager實例（即安裝了相容性包），則無需運行這些命令。

對於所有升級，無論是否使用相容性套件，您都可以執行下列Linux® curl命令，以複製Dynamic Media最初隨附的預設現成檢視器預設集：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

要將您從`/etc`建立的任何自定義查看器預設集和配置遷移到`/conf`，請運行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 安裝Feature Pack 18912以大量移轉資產 {#installing-feature-pack-for-bulk-asset-migration}

Feature Pack 18912的安裝為&#x200B;*optional*。

Feature Pack 18912可讓您透過FTP大量內嵌資產，或在Experience Manager時從Dynamic Media — 混合模式或Dynamic Media Classic移轉至Dynamic Media - Scene7模式。 可從[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)取得。

如需詳細資訊，請參閱[安裝功能套件18912以取得大量資產移轉](/help/assets/bulk-ingest-migrate.md)。

## 在Cloud Services中建立Dynamic Media設定 {#configuring-dynamic-media-cloud-services}

**設定Dynamic Media**  — 在您收到含有Dynamic Media憑證的布建電子郵件後，必須開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶以變更密碼。預配電子郵件中提供的密碼是系統生成的，並且僅用於臨時密碼。 請務必更新密碼，以便使用正確的憑證來設定Dynamic MediaCloud Service。

![dynamicmediaconfiguration_updated](assets/dynamicmediaconfiguration2updated.png)

**若要在Cloud Services中建立Dynamic Media設定：**

1. 在「Experience Manager作者」模式中，選取Experience Manager標誌以存取全域導覽主控台並選取「工具」圖示，然後前往&#x200B;**[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media設定]**。
1. 在「Dynamic Media配置瀏覽器」頁的左窗格中，選擇&#x200B;**[!UICONTROL global]**（不選擇&#x200B;**[!UICONTROL global]**&#x200B;左側的資料夾表徵圖），然後選擇&#x200B;**[!UICONTROL Create]**。
1. 在&#x200B;**[!UICONTROL 建立Dynamic Media設定]**&#x200B;頁面上，輸入標題、Dynamic Media帳戶電子郵件地址、密碼，然後選取您的地區。 此資訊是透過布建電子郵件中的Adobe提供給您的。 如果您未收到電子郵件，請聯絡Adobe客戶支援。

   選擇&#x200B;**[!UICONTROL 連接到Dynamic Media]**。

   >[!NOTE]
   收到包含Dynamic Media憑證的布建電子郵件後，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶以變更密碼。 預配電子郵件中提供的密碼是系統生成的，並且僅用於臨時密碼。 請務必更新密碼，以便使用正確的憑證來設定Dynamic MediaCloud Service。

1. 連線成功時，請設定下列項目。 含星號(*)的標題為必填：

   * **[!UICONTROL 公司]**  -Dynamic Media帳戶的名稱。您有多個Dynamic Media帳戶。 例如，您可以有不同的子品牌、部門、測試或生產環境。

   * **[!UICONTROL 公司根資料夾路徑]**

   * **[!UICONTROL 發佈資產]**  — 您可從下列三個選項中選擇：
      * **** 立即表示上傳資產時，系統會擷取資產並立即提供URL/內嵌。發佈資產不需要使用者干預。
      * **[!UICONTROL 動]** 作時表示您必須先明確發佈資產，才能提供URL/內嵌連結。<br><!-- CQDOC-17478, Added March 9, 2021-->從Experience Manager6.5.8開始，「Experience Manager發佈」例項會反映精確的Dynamic Media中繼資料值，例 `dam:scene7Domain` 如和 `dam:scene7FileStatus` 僅 **[!UICONTROL 在Activationpublish模]** 式中。若要啟用此功能，請安裝Service Pack 8，然後重新啟動Experience Manager。 前往Sling Config Manager。 找到`Scene7ActivationJobConsumer Component`的配置或建立新配置)。 選取核取方塊&#x200B;**[!UICONTROL 在Dynamic Media發佈]**&#x200B;後復寫中繼資料，然後選取&#x200B;**[!UICONTROL 儲存]**。

         ![「在Dynamic Media發佈後復寫中繼資料」核取方塊](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 選擇]** 性發佈此選項可讓您控制要在Dynamic Media中發佈的資料夾。它可讓您使用智慧型裁切或動態轉譯等功能，或決定要預覽的Experience Manager中專門發佈的資料夾。 這些相同的資產是在Dynamic Media中發佈，並在公共網域中傳送的&#x200B;*not*。<br>您可以在Dynamic Media雲端設定的 **[!UICONTROL 此處]** 設定此選項，或者您可以在資料夾屬性 **[!UICONTROL 的資料夾層級選擇設定此]**&#x200B;選項。<br>請參 [閱在Dynamic Media中使用選擇性發佈](/help/assets/selective-publishing.md)。<br>如果您稍後變更此設定，或稍後在資料夾層級變更，這些變更只會影響您從此時間點上傳的新資產。資料夾中現有資產的發佈狀態會維持原狀，直到您從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;或&#x200B;**[!UICONTROL 管理出版物]**&#x200B;對話方塊手動變更為止。
   * **[!UICONTROL 安全預覽伺服器]**  — 可讓您指定安全轉譯預覽伺服器的URL路徑。也就是說，產生轉譯後，Experience Manager可以安全地存取和預覽遠端Dynamic Media轉譯(不會將任何二進位檔傳回至Experience Manager執行個體)。
除非您有使用自己公司的伺服器或特殊伺服器的特殊安排，否則Adobe建議您保留此設定的指定。

   * **[!UICONTROL 同步所有內容]**  — 預 <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->設為選取。如果您想要選擇性地包含或排除從同步至Dynamic Media的資產，請取消選取此選項。 取消選取此選項可讓您從下列兩個Dynamic Media同步模式中選擇：

   * **[!UICONTROL Dynamic Media 同步處理模式]**
      * **[!UICONTROL 預設啟用]**  — 除非您特別標示要排除的資料夾，否則預設會將設定套用至所有資料夾。  <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 預設為停用]**  — 在您明確標示選取的資料夾以同步至Dynamic Media之前，不會將設定套用至任何資料夾。若要將選取的資料夾標示為同步至Dynamic Media，請選取資產資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 屬性]**。 在&#x200B;**[!UICONTROL Details]**&#x200B;頁簽的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉清單中，從以下三個選項中選擇。 完成後，選擇&#x200B;**[!UICONTROL Save]**。 *記住：如果您選取「同步所有contentier」，則這三&#x200B;**[!UICONTROL 個選項不]**可用。* 另請參 [閱在Dynamic Media的資料夾層級使用選擇性發佈](/help/assets/selective-publishing.md)。
         * **[!UICONTROL 繼承]**  — 資料夾上沒有明確的同步值；相反，資料夾會繼承其上階資料夾中的一個同步值，或繼承雲配置中的預設模式。繼承的詳細狀態會透過工具提示顯示。
         * **[!UICONTROL 啟用子資料夾]**  — 在此子樹狀結構中包含所有項目，以便同步至Dynamic Media。資料夾特定設定會覆寫雲端設定中的預設模式。
         * **[!UICONTROL 針對子資料夾停用]**  — 排除此子樹狀結構中的所有項目，使其無法同步至Dynamic Media。

   >[!NOTE]
   DMS7不支援版本設定。 此外，延遲啟動僅適用於在「編輯動態媒體設定」頁面中的「發佈資產 ********」設定為「啟動時」，然後只適用於在首次啟動資產時。
   啟動資產後，任何更新都會立即上線發佈至S7傳送。

1. 選擇&#x200B;**[!UICONTROL 保存]**。
1. 若要在發佈Dynamic Media內容之前安全地預覽，您必須「允許清單」Experience Manager製作例項，才能連線至Dynamic Media:

   * 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。 配置時，Adobe提供了您的憑據和登錄詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

   * 在頁面右上角附近的導航欄，導航至&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**。

   * 在「影像伺服器發佈」頁面的「發佈內容」下拉式清單中，選取「測試影像伺服」**[!UICONTROL 。]**
   * 對於「客戶端地址」篩選器，請選擇&#x200B;**[!UICONTROL 添加]**。
   * 若要啟用（開啟）地址，請選取核取方塊。 輸入Experience Manager製作例項的IP位址（非Dispatcher IP）。
   * 選擇&#x200B;**[!UICONTROL 保存]**。

您現在已完成基本設定；您已準備好使用Dynamic Media - Scene7模式。

如果要進一步自訂配置，您可以選擇完成[（可選）在Dynamic Media - Scene7模式](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)中配置高級設定下的任何任務。

## （選用）在Dynamic Media - Scene7模式中設定進階設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

如果您想進一步自訂Dynamic Media - Scene7模式的設定和設定，或最佳化其效能，您可以完成下列一或多個&#x200B;*選用*&#x200B;工作：

* [（選用）設定Dynamic Media - Scene7模式，以上傳大於2 GB的資產](#optional-config-dms7-assets-larger-than-2gb)

* [（選用）Dynamic Media - Scene7模式設定的設定與設定](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（選用）調整Dynamic Media - Scene7模式的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（選用）篩選資產以進行復寫](#optional-filtering-assets-for-replication)

### （選用）設定Dynamic Media - Scene7模式，以上傳大於2 GB的資產 {#optional-config-dms7-assets-larger-than-2gb}

在Dynamic Media - Scene7模式中，預設資產上傳檔案大小為2 GB或更小。 不過，您可以選擇設定大於2 GB和高達15 GB的資產上傳。

如果您要使用此功能，請注意下列必要條件和要點：

* 您必須以Dynamic Media - Scene7模式，使用Service Pack 6.5.4.0或更新版本執行Experience Manager6.5。
* 此大型上傳功能僅支援&#x200B;[*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html)客戶。
* 請確定您的Experience Manager執行個體已使用Amazon S3或Microsoft® Azure Blob儲存。

   >[!NOTE]
   使用存取金鑰和機密金鑰設定Azure Blob儲存，因為Blob儲存設定中的AzureSas不支援此大型上傳功能。

* 已啟用Oak的[直接二進位存取下載](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)（不需要Oak的&#x200B;*直接二進位存取上傳*）。

   若要啟用「直接二進位存取」下載，請在資料存放區設定中設定屬性`presignedHttpDownloadURIExpirySeconds > 0` 。 值應足以下載較大的二進位檔，然後可能會重試。

* 超過15 GB的資產不會上傳。 （大小限制設定在下面的步驟8中。）
* 當資料夾上觸發&#x200B;**[!UICONTROL Dynamic Media重新處理]**&#x200B;資產工作流程時，會重新處理已與Dynamic Media公司同步的任何大型資產。 不過，如果資料夾中尚未同步任何大型資產，則不會上傳資產。 因此，若要同步Dynamic Media中的現有大型資產，您可以對個別資產執行&#x200B;**[!UICONTROL Dynamic Media重新處理]**&#x200B;資產工作流程。

**若要設定Dynamic Media - Scene7模式，以上傳大於2 GB的資產：**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，然後導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。

1. 在「CRXDE Lite」視窗中，執行下列其中一項操作：

   * 在左側邊欄中，導覽至下列路徑：

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 將上方的路徑複製並貼到工具列下方的CRXDE Lite路徑欄位中，然後按`Enter`。

1. 在左側邊欄中，以滑鼠右鍵按一下`fileupload`，然後從快顯功能表中選取「覆蓋節點」**[!UICONTROL 。]**

   ![覆蓋節點選項](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 在「覆蓋節點」對話框中，選擇&#x200B;**[!UICONTROL 匹配節點類型]**&#x200B;複選框以啟用（開啟）選項，然後選擇&#x200B;**[!UICONTROL 確定]**。

   ![覆蓋節點對話方塊](/help/assets/assets-dm/uploadassets15gb_b.png)

1. 從「CRXDE Lite」視窗，執行下列其中一項操作：

   * 在左側邊欄中，導覽至下列覆蓋節點路徑：

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 將上方的路徑複製並貼到工具列下方的CRXDE Lite路徑欄位中，然後按`Enter`。

1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤的&#x200B;**[!UICONTROL 名稱]**&#x200B;列下，找到`sizeLimit`。
1. 在`sizeLimit`名稱的右側，在&#x200B;**[!UICONTROL Value]**&#x200B;列下，按兩下值欄位。
1. 以位元組為單位輸入適當值，以便將大小限制增加到最大所需上傳大小。 例如，若要將上傳資產大小限制提高為10 GB，請在值欄位中輸入`10737418240`。
您可以輸入最多15 GB（`2013265920`位元組）的值。 在此情況下，超過15 GB的已上傳資產將不會上傳。


   ![大小限制值](/help/assets/assets-dm/uploadassets15gb_c.png)

1. 在CRXDE Lite窗口的左上角附近，選擇&#x200B;**[!UICONTROL Save All]**。

   *現在，請執行下列動作，為AdobeGranite工作流程外部處理程式工作處理常式設定逾時：*

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。
1. 執行下列任一操作：

   * 導覽至下列URL路徑：

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 將上方的路徑複製並貼到瀏覽器的URL欄位中。 請務必將`localhost:4502`替換為您自己的Experience Manager實例。

1. 在&#x200B;**[!UICONTROL 「AdobeGranite工作流外部進程作業處理程式」對話框的**[!UICONTROL 「最大超時」]**欄位中，將值設定為`18000`分鐘（5小時）。]**&#x200B;預設為10800分鐘（三小時）。

   ![逾時值上限](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 在對話框的右下角，選擇&#x200B;**[!UICONTROL Save]**。

   *現在，請執行下列動作，為Scene7直接二進位上傳程式步驟設定逾時：*

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。
1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 在「工作流模型」頁上，選擇&#x200B;**[!UICONTROL Dynamic Media編碼視頻]**。
1. 在工具欄上，選擇&#x200B;**[!UICONTROL Edit]**。
1. 在工作流程頁面上，連按兩下&#x200B;**[!UICONTROL Scene7直接二進位上傳]**&#x200B;處理步驟。
1. 在&#x200B;**[!UICONTROL 步驟屬性]**&#x200B;對話框的&#x200B;**[!UICONTROL Common]**&#x200B;頁簽下的&#x200B;**[!UICONTROL Advanced Settings]**&#x200B;標題下，在&#x200B;**[!UICONTROL Timeout]**&#x200B;欄位中，輸入值`18000`分鐘（5小時）。 預設值為`3600`分鐘（1小時）。
1. 選擇&#x200B;**[!UICONTROL OK]**。
1. 選擇&#x200B;**[!UICONTROL 同步]**。
1. 對&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程模型和&#x200B;**[!UICONTROL Dynamic Media重新處理]**&#x200B;工作流程模型重複步驟14-21。

### （選用）Dynamic Media - Scene7模式設定的設定與設定 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

當您處於運行模式`dynamicmedia_scene7`時，請使用Dynamic Media Classic用戶介面更改Dynamic Media設定。

上述部分工作需要您開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

設定和設定任務包括：

* [影像伺服器的發佈設定](#publishing-setup-for-image-server)
* [配置應用程式一般設定](#configuring-application-general-settings)
* [配置顏色管理](#configuring-color-management)
* [編輯支援格式的MIME類型](#editing-mime-types-for-supported-formats)
* [為不支援的格式添加MIME類型](#adding-mime-types-for-unsupported-formats)
* [建立批集預設集以自動生成影像集和回轉集](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### 影像伺服器的發佈設定 {#publishing-setup-for-image-server}

「發佈設定」設定決定預設如何從Dynamic Media傳送資產。 如果未指定任何設定，Dynamic Media會根據「發佈設定」中定義的預設設定來傳送資產。 例如，傳送不包含解析度屬性的影像請求，會產生具有預設物件解析度設定的影像。

若要設定發佈設定：在Dynamic Media Classic中，導覽至「**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**」。

「影像伺服器」螢幕建立用於傳送影像的預設設定。 請參閱UI畫面，了解每個設定的說明。

* **[!UICONTROL 請求屬性]**  — 這些設定會限制可從伺服器傳送的影像。
* **[!UICONTROL 預設請求屬性]**  — 這些設定屬於影像的預設外觀。
* **[!UICONTROL 常見縮圖屬性]**  — 這些設定與縮圖影像的預設外觀相關。
* **[!UICONTROL 目錄欄位的預設值]** — 這些設定與影像的解析度和預設縮圖類型相關。
* **[!UICONTROL 顏色管理屬性]**  — 這些設定將決定要使用的ICC顏色配置檔案。
* **[!UICONTROL 相容性屬性]**  — 此設定可讓文字層中的前導和尾隨段落，如同在3.6版中一樣處理，以提供回溯相容性。
* **[!UICONTROL 本地化支援]**  — 這些設定可讓您管理多個地區設定屬性。它也可讓您指定地區對應字串，以便定義要在檢視器中支援各種工具提示的語言。 有關設定&#x200B;**[本地化支援]**&#x200B;的詳細資訊，請參閱設定資產本地化時的注意事項[](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets)。

#### 配置應用程式一般設定 {#configuring-application-general-settings}

若要開啟「應用程式一般設定」頁面，請在「Dynamic Media Classic全域導覽列」中導覽至「**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**」。

**[!UICONTROL 伺服器]**  — 在帳戶布建時，Dynamic Media會自動為您的公司提供指派的伺服器。這些伺服器可用來建構您網站和應用程式的URL字串。 這些URL呼叫是您的帳戶專屬的。 除非Adobe客戶支援明確指示，否則請勿更改任何伺服器名稱。

**[!UICONTROL 覆寫影像]**  - Dynamic Media不允許兩個檔案具有相同的名稱。每個項目的URL ID（檔案名稱減去副檔名）必須是唯一的。 這些選項指定如何上傳取代資產：無論是取代原始檔案還是變成重複檔案。 重複資產會以「–1」重新命名（例如chair.tif已重新命名為chair-1.tif）。 這些選項會影響上傳至與原始資料夾不同的資料夾的資產，或副檔名與原始資料夾不同的資產(例如JPG、TIF或PNG)。

* **[!UICONTROL 在目前資料夾中覆寫，使用相同的基本影像名稱/擴充功能]**  — 此選項是最嚴格的取代規則。它要求您將取代影像上傳至與原始影像相同的資料夾，且取代影像的副檔名與原始影像相同。 若不符合這些要求，則會建立重複項目。

>[!NOTE]
若要與Experience Manager保持一致，請一律選擇此設定：**在當前資料夾中覆蓋，相同的基本影像名稱/副檔名**

* **[!UICONTROL 在任何資料夾中覆寫相同的基本資產名稱/副檔名]**  — 需要替換影像的副檔名與原始影像相同（例如chair.jpg必須替換chair.jpg，而非chair.tif）。不過，您可以將取代影像上傳至與原始影像不同的資料夾。 更新後的影像位於新資料夾中；在檔案的原始位置找不到檔案
* **[!UICONTROL 在任何資料夾中覆寫相同的基本資產名稱(不論副檔名為何]** ) — 此選項是包含最多的取代規則。您可以將取代影像上傳至與原始檔案不同的資料夾、以不同副檔名上傳檔案，然後取代原始檔案。 如果原始檔案位於不同的資料夾中，則替換影像位於上載到的新資料夾中。

**[!UICONTROL 預設色彩描述檔]**  — 如需詳細 [資訊，](#configuring-color-management) 請參閱設定色彩管理。

>[!NOTE]
依預設，當您選取「轉譯」時，系統會顯示15個轉譯，當您在資產的詳細資料檢視中選取「檢視器 ******** 」時，系統會顯示15個檢視器預設集。您可以提高此限制。請參閱[增加顯示](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)或[的影像預設集數目增加顯示](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)的檢視器預設集數目。

#### 配置顏色管理 {#configuring-color-management}

Dynamic Media色彩管理可讓您為資產加上色彩校正。 透過色彩校正，擷取的資產可保留其色彩空間(RGB、CMYK、灰色)和內嵌的色彩設定檔。 當您請求動態格式副本時，將使用CMYK、RGB或灰度輸出將影像顏色更正到目標顏色空間中。 請參閱[設定影像預設集](/help/assets/managing-image-presets.md)。

配置預設顏色屬性，以便在請求影像時啟用顏色校正：

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後使用布建期間提供的憑證登入您的帳戶。
1. 導覽至&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL 應用程式設定]**。
1. 展開「發 **[!UICONTROL 布設定]** 」區域並選 **[!UICONTROL 取「影像伺服器」]**。設定發 **[!UICONTROL 布例項的預設值]** ，將「發佈內容」設 **** 定為「影像伺服」。
1. 捲動至您要變更的屬性。 例如， **[!UICONTROL 色彩管理屬性]**&#x200B;區域中的屬性。

   您可以設定下列顏色校正屬性：

   * **[!UICONTROL CMYK預設顏色空間]**  — 預設CMYK顏色配置檔案的名稱
   * **[!UICONTROL 灰階預設顏色空間]**  — 預設灰階顏色配置檔案的名稱
   * **[!UICONTROL RGB預設顏色空間]**  — 預設RGB顏色配置檔案的名稱
   * **[!UICONTROL 色彩轉換演算方式]**  — 指定演算方式。可接受的值為：**[!UICONTROL 知覺]**,**[!UICONTROL 相對冷量]**,**[!UICONTROL 飽和度]**,**[!UICONTROL 絕對冷量]**。 Adobe建議預設值為&#x200B;**[!UICONTROL relative]**。

1. 選擇&#x200B;**[!UICONTROL 保存]**。

例如，您可以將「 **[!UICONTROL RGB預設顏色空間]** 」設 *為sRGB*，將「 **[!UICONTROL CMYK預設顏色空間」設為]**** WebCobatedCholor。

這麼做會執行下列動作：

* 啟用RGB和CMYK影像的顏色校正。
* 沒有顏色描述檔的RGB影像假設位於&#x200B;*sRGB*&#x200B;顏色空間中。
* 假定沒有顏色輪廓的CMYK影像位於&#x200B;*WebCobated*&#x200B;顏色空間中。
* 傳回RGB輸出的動態轉譯，會在&#x200B;*sRGB*&#x200B;色域中傳回。
* 傳回CMYK輸出的動態轉譯，會在&#x200B;*WebCobated*&#x200B;色域中傳回。

#### 編輯支援格式的MIME類型 {#editing-mime-types-for-supported-formats}

您可以定義由Dynamic Media處理的資產類型，並自訂進階資產處理參數。 例如，您可以指定資產處理參數以執行下列動作：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop檔案(.PSD)轉換為橫幅範本資產，以便個人化。
* 柵格化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝的PostScript®檔案(.EPS)。
* [視訊](/help/assets/video-profiles.md) 設定檔 [和](/help/assets/image-profiles.md) 影像設定檔可分別用來定義視訊和影像的處理。

請參閱[上傳資產](/help/assets/manage-assets.md#uploading-assets)。

**要編輯支援格式的MIME類型，請執行以下操作：**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，然後導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 在左側邊欄中，導覽至下列項目：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME類型](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選擇mime類型。
1. 在CRXDE Lite頁面的右側，下方：

   * 連按兩下&#x200B;**[!UICONTROL enabled]**&#x200B;欄位。 依預設，會啟用所有資產mime類型（設為&#x200B;**[!UICONTROL true]**），這表示資產會同步至Dynamic Media以進行處理。 如果您不想處理此資產mime類型，請將此設定變更為&#x200B;**[!UICONTROL false]**。

   * 點選兩下&#x200B;**[!UICONTROL jobParam]**&#x200B;以開啟其相關的文字欄位。 如需可用於指定mime類型的允許處理參數值清單，請參閱[支援的Mime類型](/help/assets/assets-formats.md#supported-mime-types)。

1. 執行下列任一操作：

   * 重複步驟3-4以編輯更多MIME類型。
   * 在CRXDE Lite頁面的菜單欄上，選擇&#x200B;**[!UICONTROL 全部保存]**。

1. 在頁面的左上角，選取&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以返回Experience Manager。

#### 為不支援的格式添加MIME類型 {#adding-mime-types-for-unsupported-formats}

您可以針對Experience Manager Assets中不支援的格式新增自訂MIME類型。 將MIME類型移至`image_`之前，確保Experience Manager不會刪除您在CRXDE Lite中新增的任何新節點。 同時，請確定其啟用值設為&#x200B;**[!UICONTROL false]**。

**為不支援的格式添加MIME類型：**

1. 從Experience Manager，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的瀏覽器頁簽隨即開啟，顯示&#x200B;**[!UICONTROL Adobe Experience Manager Web Console Configuration]**&#x200B;頁面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，向下捲動至名稱 *Adobe CQ Scene7 Asset MIME類型Service* ，如下列螢幕擷取所示。在名稱的右側，選擇「**[!UICONTROL 編輯配置值]**」（鉛筆表徵圖）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQ Scene7資產MIME類型Service**&#x200B;頁面上，選取任何加號圖示&lt;+>。 表格中您選取加號以新增新mime類型的位置很瑣碎。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 在您剛新增的空白文字欄位中輸入`DWG=image/vnd.dwg`。

   範例`DWG=image/vnd.dwg`僅供示範之用。 您在此處新增的MIME類型可能是任何其他不支援的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，選擇&#x200B;**[!UICONTROL Save]**。

   此時，您可以關閉開啟「Adobe Experience Manager Web Console設定」頁面的瀏覽器標籤。

1. 返回具有開啟的Experience Manager控制台的瀏覽器頁簽。
1. 從Experience Manager，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左側邊欄中，導覽至下列項目：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖曳mime類型`image_vnd.dwg`，並將其直接拖曳至樹狀目錄的`image_`上方，如下列螢幕擷取所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;頁簽中，在&#x200B;**[!UICONTROL enabled]**&#x200B;行的&#x200B;**[!UICONTROL 值]**&#x200B;列標題下，按兩下值以開啟&#x200B;**[!UICONTROL 值]**&#x200B;下拉清單。`image_vnd.dwg`
1. 在欄位中輸入`false`（或從下拉式清單中選取&#x200B;**[!UICONTROL false]**）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite頁面的左上角附近，選擇「**[!UICONTROL 全部保存]**」。

#### 建立批集預設集以自動生成影像集和回轉集 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

在資產上傳至Dynamic Media時，使用批次集預設集來自動建立影像集或回轉集。

首先，定義資產在集合中分組方式的命名慣例。 然後建立批集預設集，該預設集是一組唯一命名的、自包含的指令集。 它必須定義如何使用符合預設方式中已定義命名慣例的影像來建構集。

上傳檔案時，Dynamic Media會自動建立一組檔案，其中包含所有符合使用中預設集中所定義命名慣例的檔案。

##### 配置預設命名

建立用於任何批集預設配方的預設命名慣例。 在批集預設集定義中選取的預設命名慣例可能是貴公司為批生成集所需的全部。 系統會建立批集預設集，以使用您定義的預設命名慣例。 如果公司定義的預設命名有例外，您可以建立任意數量的批集預設集，其中包含特定內容集所需的替代自定義命名慣例。

雖然使用批次集預設集功能不需要設定預設命名慣例，但最佳實務建議您使用預設命名慣例。 它可讓您定義要分組到一組中的命名約定的任意元素，以便簡化批集建立。

或者，您可以使用沒有可用表單欄位的&#x200B;**[!UICONTROL 檢視程式碼]**。 在此檢視中，您可以完全使用規則運算式建立命名慣例定義。

定義有兩個元素：「比對」和「基本名稱」。 這些欄位可讓您定義命名約定的所有元素，並識別用於為包含這些元素的集命名的約定的一部分。 公司的個別命名慣例通常會針對每個元素使用一或多行定義。 您可以針對唯一定義使用任意數行，並將它們分組為不同的元素，例如主影像、顏色元素、替代視圖元素和色票元素。

**配置預設命名：**

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   配置時，Adobe提供了您的憑據和登錄詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在頁面頂部附近的導航欄中，導航至&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Default Naming]**。
1. 選擇 **[!UICONTROL 「查看表單]** 」或「 **[!UICONTROL 查看代碼」]** ，以指定要查看的方式並輸入有關每個元素的資訊。

   您可以選取&#x200B;**[!UICONTROL 檢視程式碼]**&#x200B;核取方塊，檢視建立與表單選取項目一併的規則運算式值。 如果表單視圖因任何原因限制您，則可以輸入或更改這些值，以幫助定義命名約定的元素。 如果無法在表單檢視中剖析您的值，表單欄位就會變成非作用中。

   >[!NOTE]
   已停用的表單欄位不會執行規則運算式正確無誤的驗證。 您會看到在結果行後面為每個元素建立的規則運算式的結果。 頁面底部會顯示完整的規則運算式。

1. 視需要展開每個元素，並輸入您要使用的命名慣例。
1. 視需要執行下列任一操作：

   * 選取&#x200B;**[!UICONTROL Add]**&#x200B;以新增元素的其他命名慣例。
   * 選擇&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除元素的命名慣例。

1. 執行下列任一操作：

   * 選擇「**[!UICONTROL 另存為]**」並鍵入預設集的名稱。
   * 如果您正在編輯現有預設集，請選擇「**[!UICONTROL 儲存]**」。

##### 建立批集預設集

Dynamic Media使用批次集預設集，將資產組織成影像集（替代影像、顏色選項、360回轉），以便在檢視器中顯示。 批次集預設集會在Dynamic Media中與資產上傳程式一起自動執行。

您可以建立、編輯和管理批集預設集。 有兩種形式的批集預設集定義：一個是您可設定的預設命名慣例，另一個是您即時建立的自訂命名慣例。

您可以使用表單欄位方法來定義批次集預設集，或使用程式碼方法來使用規則運算式。 如同在「預設命名」中，您可以在「表單檢視」中定義的同時選擇「檢視程式碼」，並使用規則運算式來建立定義。 或者，您也可以取消勾選任一個檢視，以專用使用其中一個檢視。

**要建立批集預設集，請執行以下操作：**

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   配置時，Adobe提供了您的憑據和登錄詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在頁面頂部附近的導航欄上，導航至&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Batch Set Preset]**。

   **[!UICONTROL 「檢視表單]**」（如「詳細資料」頁面右上角的設定）是預設檢視。

1. 在「預設清單」面板中，選擇&#x200B;**[!UICONTROL Add]**&#x200B;以激活螢幕右側「詳細資訊」面板中的定義欄位。
1. 在「詳細資料」面板的「預設集名稱」欄位中，輸入預設集的名稱。
1. 在「批集類型」下拉菜單中，選擇預設類型。
1. 執行下列任一操作：

   * 如果您使用先前在&#x200B;**[!UICONTROL 應用程式設定]** > **[!UICONTROL 批集預設集]** > **[!UICONTROL 預設命名]**&#x200B;下設定的預設命名慣例，請展開&#x200B;**[!UICONTROL 資產命名慣例]**，然後在「檔案命名」下拉式清單中，選取&#x200B;**[!UICONTROL 預設]**。

   * 若要在設定預設集時定義新的命名慣例，請展開&#x200B;**[!UICONTROL 資產命名慣例]**，然後在「檔案命名」下拉式清單中，選取&#x200B;**[!UICONTROL 自訂]**。

1. 對於「序列」順序，定義在影像集在Dynamic Media中分組後的顯示順序。

   依預設，您的資產依字母順序排列。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

1. 對於「設定命名和建立慣例」，請指定尾碼或前置詞至您在「資產命名慣例」中定義的基礎名稱。 此外，定義在Dynamic Media資料夾結構內建立集的位置。

   如果您定義大量集，請將集與包含資產本身的資料夾分開。 例如，建立「影像集」資料夾並將生成的集放在此處。

1. 在「詳細資訊」面板中，選擇&#x200B;**[!UICONTROL Save]**。
1. 選取新預設集名稱旁的&#x200B;**[!UICONTROL 作用中]**。

   啟動預設會確保當您將資產上傳至Dynamic Media時，會套用批次集預設集以產生該集。

##### 建立批集預設集以自動生成2D回轉集

您可以使用批集類型&#x200B;**[!UICONTROL 多軸回轉集]**&#x200B;建立自動生成2D回轉集的方式。 影像分組使用「列」和「列」規則運算式，以便在多維度陣列中的對應位置正確對齊影像資產。 在多軸回轉集中，沒有必須具有的最小或最大行數或列數。

例如，假設您要建立名為`spin-2dspin`的多軸回轉集。 您有一組回轉集影像，包含三列，每列12個影像。 這些影像的名稱如下：

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

使用此資訊，可以按如下方式建立批集類型處方：

![chlimage_1-560](assets/chlimage_1-560.png)

對回轉集的共用資產名稱部分進行分組會新增至「**[!UICONTROL 符合]**」欄位（如醒目提示）。 包含行和列的資產名稱的變數部分將分別添加到 **[!UICONTROL 行]** 和 **[!UICONTROL 列欄位中]** 。

上傳和發佈回轉集時，您會啟用「上傳工作選項」對話方塊中「批次集預設集」下方所列的2D回轉集 **[!UICONTROL 方式名稱]****** 。

**要為自動生成2D回轉集建立批集預設集，請執行以下操作：**

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   配置時，Adobe提供了您的憑據和登錄詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在頁面頂部附近的導航欄上，導航至&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Batch Set Presets]** > **[!UICONTROL Batch Set Preset]**。

   **[!UICONTROL 「檢視表單]**」（如「詳細資料」頁面右上角的設定）是預設檢視。

1. 在「預設清單」面板中，選擇&#x200B;**[!UICONTROL Add]**&#x200B;以激活螢幕右側「詳細資訊」面板中的定義欄位。
1. 在「詳細資料」面板的「預設集名稱」欄位中，輸入預設集的名稱。
1. 在「批集類型」下拉式功能表中，選擇「資產 **[!UICONTROL 集」]**。
1. 在「子類型」下拉清單中，選擇&#x200B;**[!UICONTROL 多軸回轉集]**。
1. 展開&#x200B;**[!UICONTROL 資產命名慣例]**，然後在「檔案命名」下拉式清單中，選取&#x200B;**[!UICONTROL 自訂]**。
1. 使用「 **[!UICONTROL 比對]** 」(Match **[!UICONTROL )和 (可選) 「基本名稱]** 」(Base Name)屬性，定義組成群組之影像資產的命名規則運算式。

   例如，您的常值「比對」規則運算式可能如下所示：

   `(w+)-w+-w+`

1. 展開&#x200B;**[!UICONTROL 行列位置]**，然後定義2D回轉集陣列內影像資產位置的名稱格式。

   使用括弧在檔案名中包含行或列位置。

   例如，對於您的列規則運算式，它可能如下所示：

   `\w+-R([0-9]+)-\w+`

   或

   `\w+-(\d+)-\w+`

   對於欄規則運算式，它可能如下所示：

   `\w+-\w+-C([0-9]+)`

   或

   `\w+-\w+-C(\d+)`

   上述範例僅供示範之用。 您可以建立規則運算式，但需視需要而定。

   >[!NOTE]
   如果列和欄規則運算式的組合無法判斷資產在多維度回轉集陣列內的位置，資產不會新增至集。 也會記錄錯誤。

1. 對於「設定命名和建立慣例」，請指定尾碼或前置詞至您在「資產命名慣例」中定義的基礎名稱。

   此外，定義回轉集在Dynamic Media Classic資料夾結構內建立的位置。

   如果您定義大量集，請將集與包含資產本身的資料夾分開。 例如，建立「回轉集」資料夾，將產生的集放在此處。

1. 在「詳細資訊」面板中，選擇&#x200B;**[!UICONTROL Save]**。
1. 選取新預設集名稱旁的&#x200B;**[!UICONTROL 作用中]**。

   啟動預設會確保當您將資產上傳至Dynamic Media時，會套用批次集預設集以產生該集。

### （選用）調整Dynamic Media - Scene7模式的效能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為了讓Dynamic Media - Scene7模式順利執行，Adobe建議使用下列同步效能/可擴充性微調提示：

* 更新預定義的作業參數，以處理不同的檔案格式。
* 更新預先定義的Granite工作流程（視訊資產）佇列背景工作執行緒。
* 更新預先定義的Granite暫時性工作流程（影像和非視訊資產）佇列背景工作執行緒。
* 更新最大上傳連線至Dynamic Media Classic伺服器。

#### 更新預定義的作業參數以處理不同的檔案格式

上傳檔案時，您可以調整工作參數以加快處理速度。 例如，如果您上傳PSD檔案，但不想以範本形式處理，則可將圖層擷取設為false(off)。 在這種情況下，調整的作業參數如下所示：`process=None&createTemplate=false`。

如果您確實要開啟範本建立，請使用下列參數：`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建議對PDF、PostScript®和PSD檔案使用以下「調整」作業參數：

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 檔案類型 | 建議的作業參數 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

若要更新任何這些參數，請依照[啟用MIME類型型資產/Dynamic Media Classic上傳工作參數support](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)中的步驟操作。

#### 更新Granite暫時工作流程佇列 {#updating-the-granite-transient-workflow-queue}

「Granite傳輸工作流程」佇列用於&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程。 在Dynamic Media中，它用於影像擷取和處理。

**若要更新Granite暫時工作流程佇列：**

1. 導覽至[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)並搜尋&#x200B;**佇列：Granite暫時工作流隊列**。

   >[!NOTE]
   由於OSGi PID是動態產生的，因此必須進行文字搜尋，而非直接URL。

1. 在&#x200B;**[!UICONTROL 最大並行作業]**&#x200B;欄位中，將數字更改為所需值。

   您可以增加&#x200B;**[!UICONTROL 最大並行作業數]**，以充分支援檔案的大量上傳至Dynamic Media。 確切值取決於硬體容量。 在某些情況下（即初始移轉或一次性大量上傳），您可以使用大值。 但請注意，使用大值（如內核數的2倍）可能會對其他併發活動產生負面影響。 因此，請根據您的特定使用案例來測試和調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 選擇&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite工作流程佇列 {#updating-the-granite-workflow-queue}

Granite工作流程佇列用於非暫時性的工作流程。 在Dynamic Media中，它用於透過&#x200B;**[!UICONTROL Dynamic Media編碼視訊]**&#x200B;工作流程處理視訊。

**若要更新Granite工作流程佇列：**

1. 導覽至`https://<server>/system/console/configMgr`並搜尋&#x200B;**佇列：Granite工作流隊列**。

   >[!NOTE]
   由於OSGi PID是動態產生的，因此必須進行文字搜尋，而非直接URL。

1. 在&#x200B;**[!UICONTROL 最大並行作業]**&#x200B;欄位中，將數字更改為所需值。

   您可以增加「最大並行作業數」，以充分支援檔案大量上傳至Dynamic Media。 確切值取決於硬體容量。 在某些情況下（即初始移轉或一次性大量上傳），您可以使用大值。 但請注意，使用大值（如內核數的2倍）可能會對其他併發活動產生負面影響。 因此，請根據您的特定使用案例來測試和調整值。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選擇&#x200B;**[!UICONTROL 保存]**。

#### 更新Dynamic Media Classic上傳連線 {#updating-the-scene-upload-connection}

Scene7上傳連線設定會將Experience Manager資產同步至Dynamic Media Classic伺服器。

**若要更新Dynamic Media Classic上傳連線：**

1. 導航到 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 連線數]**&#x200B;欄位和/或&#x200B;**[!UICONTROL 作用中作業逾時]**&#x200B;欄位中，視需要變更數字。

   **[!UICONTROL 連線數]**&#x200B;設定會控制允許Experience Manager至Dynamic Media上傳的HTTP連線數量上限；通常，十個連線的預先定義值就足夠了。

   **[!UICONTROL 作用中工作逾時]**&#x200B;設定決定上傳之Dynamic Media資產在傳送伺服器中發佈的等待時間。 預設情況下，此值為2100秒或35分鐘。

   對於大多數使用案例，2100的設定已足夠。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 選擇&#x200B;**[!UICONTROL 保存]**。

### （選用）篩選資產以進行復寫 {#optional-filtering-assets-for-replication}

在非Dynamic Media部署中，您會從Experience Manager製作環境復寫&#x200B;*所有*&#x200B;資產（包括影像和視訊）至Experience Manager發佈節點。 此工作流程是必要的，因為Experience Manager發佈伺服器也會傳送資產。

不過，在Dynamic Media部署中，由於資產是透過Cloud Service傳送，因此不需要將這些相同的資產複製到Experience Manager發佈節點。 這樣的「混合發佈」工作流程可避免額外的儲存成本和更長的複製資產處理時間。 其他內容（例如網站頁面）會繼續從Experience Manager發佈節點提供。

篩選器可讓您透過&#x200B;*排除*&#x200B;資產，避免複製到Experience Manager發佈節點。

#### 對復寫使用預設資產篩選器 {#using-default-asset-filters-for-replication}

如果您使用Dynamic Media進行影像處理或影片，或兩者皆使用，則可使用Adobe依原樣提供的預設篩選器。 下列篩選器預設為作用中：

|  | 篩選 | Mime類型 | 轉譯 |
| --- | --- | --- | --- |
| Dynamic Media影像傳送 | filter-image<br>filter-sets | 開頭為&#x200B;**image/**<br>&#x200B;包含&#x200B;**applications/**，結尾為&#x200B;**set**。 | 現成可用的「篩選影像」（套用至單一影像資產，包括互動式影像）和「篩選集」（套用至回轉集、影像集、混合媒體集和轉盤集）將：<br>·排除不複製原始影像和靜態影像轉譯。 |
| Dynamic Media影片傳送 | filter-video | 開頭為&#x200B;**video/** | 現成可用的「篩選視訊」將：<br>·從復寫原始視訊和靜態縮圖轉譯中排除。 |

>[!NOTE]
篩選器會套用至MIME類型，且不能是路徑專屬的。

#### 自訂復寫的資產篩選器 {#customizing-asset-filters-for-replication}

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，並導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 在左側資料夾樹中，導覽至`/etc/replication/agents.author/publish/jcr:content/damRenditionFilters`以檢閱篩選器。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 若要定義篩選器的Mime類型，可以按如下方式找到Mime類型：

   在左側邊欄中，展開`content > dam > <locate_your_asset> > jcr:content > metadata`，然後在表格中找出`dc:format`。

   下圖是資產`dc:format`路徑的範例。

   ![chlimage_1-18](assets/chlimage_1-3.png)

   請注意，資產`Fiji Red.jpg`的`dc:format`為`image/jpeg`。

   若要讓此篩選器套用至所有影像，而不論其格式為何，請將值設為`image/*`，其中`*`是套用至任何格式之所有影像的規則運算式。

   要讓篩選器僅應用於類型JPEG的影像，請輸入`image/jpeg`值。

1. 定義您要包含或排除在復寫中的轉譯。

   可用於篩選複製的字元包括：

   | 要使用的字元 | 如何篩選資產以進行復寫 |
   | --- | --- |
   | * | 萬用字元 |
   | + | 包括用於複製的資產 |
   | - | 排除復寫中的資產 |

   導航到 `content/dam/<locate your asset>/jcr:content/renditions`.

   下圖是資產轉譯的範例。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   如果只想複製原始檔案，則輸入`+original`。
