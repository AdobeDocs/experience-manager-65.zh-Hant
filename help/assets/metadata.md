---
title: 管理您的數位資產的中繼資料 [!DNL Adobe Experience Manager]。
description: 瞭解中繼資料的類型， [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 以及如何根據資產的中繼資料自動組織和處理資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b14b377e52ab10c41355f069d97508b588d82216
workflow-type: tm+mt
source-wordcount: '2423'
ht-degree: 10%

---


# 管理數位資產的中繼資料 {#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。 它可讓資產的分類和組織更輕鬆，並協助尋找特定資產的人。 中繼資料管理可從上傳至的檔案擷取中繼資 [!DNL Experience Manager Assets]料，與創意工作流程整合。 透過使用資產保留和管理中繼資料的能力，您可以根據資產的中繼資料自動組織及處理資產。

## 中繼資料及其來源 {#how-to-edit-or-add-metadata}

中繼資料是可搜尋之資產的其他資訊。 它會新增至資產，並在您 [!DNL Experience Manager] 上傳資產時加以處理。 您可以編輯現有的中繼資料，將新的中繼資料屬性新增至現有欄位。 組織需要可控且可靠的中繼資料辭彙。 因 [!DNL Experience Manager Assets] 此不允許隨選新增中繼資料屬性。 只有管理員和開發人員才能新增包含中繼資料的屬性或欄位。 使用者可以在現有欄位中填入中繼資料。

下列方法可用來新增中繼資料至數位資產：

* 首先，建立資產的原生應用程式會新增一些中繼資料。 例如， [Acrobat會將一些中繼資料新增至PDF檔案](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) ，或是相機會將一些基本中繼資料新增至像片。 產生資產時，您可以在原生應用程式本身新增中繼資料。 例如，您可以在 [Adobe Lightroom中新增IPTC中繼資料](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html)。

* 在將資產上傳至之 [!DNL Experience Manager]前，您可以使用用來建立資產的原生應用程式，或使用某些其他中繼資料編輯應用程式來編輯和修改中繼資料。 當您將資產上傳至Experience Manager時，會處理中繼資料。 例如，請參閱如何在中 [使用中繼資料 [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) ，以及 [中的標籤面板 [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html)[!DNL Adobe Exchange]。

* 在中 [!DNL Experience Manager Assets]，您可以手動新增或編輯「屬性」頁面中資產的 [!UICONTROL 中繼資料] 。

* 當資產上傳 [至DAM時](/help/assets/metadata-config.md#metadata-profiles) ，您可 [!DNL Experience Manager Assets] 以運用的中繼資料設定檔功能自動新增中繼資料。

## 在 [!DNL Experience Manager Assets] {#add-edit-metadata}

若要編輯使用者介面中資產的中繼 [!DNL Assets] 資料，請依照下列步驟進行：

1. 執行下列任一項作業：

   * 從介面 [!DNL Assets] 中，選擇資產，然後從工具 **[!UICONTROL 列按一下「檢視屬性]** 」。
   * 從資產縮圖中，選取「檢視 **[!UICONTROL 屬性]** 」快速動作。
   * 在資產頁面中，按一下工 **[!UICONTROL 具列中的「檢]**![視屬性資](assets/do-not-localize/info-circle-icon.png) 產資訊」圖示。

   資產頁面會顯示資產的所有中繼資料。 當資產上傳（收錄）至時，會擷取中繼資料 [!DNL Experience Manager]。

   ![選取資產的屬性以檢視其中繼資料](assets/asset-metadata.png)

   *圖：在資產屬性頁面上編輯或新 [!UICONTROL 增中繼資] 料。*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >如果文字欄位空白，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並儲存它以新增該中繼資料屬性。

對資產中繼資料所做的任何變更都會寫入原始二進位檔，作為其XMP資料的一部分。 中繼資料回寫工作流程會將中繼資料新增至原始二進位檔。 對現有屬性所做的變更(如 `dc:title`)會被覆寫，而新屬性(包括自訂屬性 `cq:tags`等)會隨架構新增。

支援並啟用XMP回寫功能，適用於技術需求中所述的平台 [和檔案格式。](/help/sites-deploying/technical-requirements.md)

## 編輯多個資產的中繼資料屬性 {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] 可讓您同時編輯多個資產的中繼資料，以便快速將一般中繼資料變更大量傳播至資產。 您也可以大量編輯多個系列的中繼資料。 使用「屬性」頁面，對多個資產或系列執行中繼資料變更：

* 將中繼資料屬性變更為公用值
* 新增或修改標籤

若要自訂中繼資料屬性頁面，包括新增、修改、刪除中繼資料屬性，請使用架構 [編輯器](metadata-config.md#folder-metadata-schema)。

>[!NOTE]
>
>大量編輯方法適用於資料夾或系列中的可用資產。 對於跨資料夾可用或符合一般准則的資產，可在搜尋後 [大量更新中繼資料](search-assets.md#metadataupdates)。

1. 在使 [!DNL Assets] 用者介面中，導覽至您要編輯的資產所在的位置。
1. 選取您要編輯其常用屬性的資產。
1. 在工具列中，按一 **[!UICONTROL 下「屬性]** 」以開啟所選資產的屬性頁面。

   >[!NOTE]
   >
   >當您選取多個資產時，會為資產選取最低的共同父級表單。 換言之，屬性頁面只會顯示所有個別資產屬性頁面上共用的中繼資料欄位。

1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料編輯器，請取消選取清單中的其餘資產。 中繼資料編輯器欄位會填入特定資產的中繼資料。

   >[!NOTE]
   >
   >* 在屬性頁面中，您可以取消選取資產，從資產清單中移除資產。 資產清單預設會選取所有資產。 您從清單中移除的資產的中繼資料不會更新。
   >* 在資產清單頂端，選取「標題」旁的核取方塊 **** ，以在選取資產和清除清單之間切換。


1. 若要為資產選取不同的中繼資料結構，請按一下工 **[!UICONTROL 具列中的]** 「設定」，然後選取所要的結構。
1. 儲存變更。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。按一 **[!UICONTROL 下提交]**。

   >[!CAUTION]
   >
   >對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 匯入中繼資料 {#import-metadata}

[!DNL Assets] 可讓您使用CSV檔案大量匯入資產中繼資料。 您可以匯入CSV檔案，對最近上傳的資產或現有資產進行大量更新。 您也可以從協力廠商系統，以CSV格式大量內嵌資產中繼資料。

中繼資料匯入是非同步的，不會影響系統效能。 如果已勾選工作流程標幟，由於XMP回寫活動，同步更新多個資產的中繼資料可能會耗費大量資源。 在精簡伺服器使用期間規劃此類匯入，以免影響其他使用者的效能。

>[!NOTE]
>
>若要匯入自訂名稱空間上的中繼資料，請先註冊名稱空間。

1. 導覽至使 [!DNL Assets] 用者介面，然後按一下工 **[!UICONTROL 具列中的]** 「建立」。
1. 從功能表中，選取「中繼 **[!UICONTROL 資料]**」。
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. 選取包含中繼資料的CSV檔案。
1. 指定下列參數。 請參閱中繼資料匯 [入範例檔案。csv的範例CSV檔案](assets/metadata-import-sample-file.csv)。

   | 中繼資料匯入參數 | 說明 |
   |:---|:---|
   | [!UICONTROL 批次大小] | 要匯入中繼資料的批次中資產數。 預設值為 50。最大值為100。 |
   | [!UICONTROL 欄位分隔符號] | 預設值 `,` 為（逗號）。 您可以指定任何其他字元。 |
   | [!UICONTROL 多值分隔符號] | 中繼資料值的分隔符號。 預設值為 `|`. |
   | [!UICONTROL 啟動工作流程] | 預設為False。 設為且預 `true` 設的啟動程式設定對  DAM中繼資料回寫工作流程（將中繼資料寫入二進位XMP資料）有效。 啟用啟動工作流程會拖慢系統運作速度。 |
   | [!UICONTROL 資產路徑欄名稱] | 定義含資產之CSV檔案的欄名。 |

1. Click **[!UICONTROL Import]** from the toolbar. 匯入中繼資料後，通知會顯示在「通知收件 [!UICONTROL 匣] 」中。

1. 若要確認正確的匯入，請導覽至資產的「屬 [!UICONTROL 性] 」頁面，並驗證欄位中的值。

若要在匯入中繼資料時新增日期和時間戳記，請 `YYYY-MM-DDThh:mm:ss.fff-00:00` 使用日期和時間格式。 日期和時間以24小時 `T`格式 `hh` 的小時、納秒和時區偏移 `fff``-00:00` 分隔。 例如， `2020-03-26T11:26:00.000-07:00` 是2020年3月26日太平洋標準時間上午11:26:00.000。

>[!CAUTION]
>
>如果日期格式不符 `YYYY-MM-DDThh:mm:ss.fff-00:00`合，則不設定日期值。 匯出的中繼資料CSV檔案的日期格式為格式 `YYYY-MM-DDThh:mm:ss-00:00`。 如果要匯入，請新增以表示的納秒值，將它轉換為可接受的格式 `fff`。

## Export metadata {#export-metadata}

您可以匯出CSV格式的多個資產的中繼資料。 中繼資料會以非同步方式匯出，不會影響系統的效能。 若要匯出中繼資 [!DNL Experience Manager] 料，請遍歷資產節點及其子節點的 `jcr:content/metadata` 屬性，並將中繼資料屬性匯出為CSV檔案。

大量匯出中繼資料的幾個使用案例包括：

* 移轉資產時，匯入第三方系統中的中繼資料。
* 與更廣大的專案團隊共用資產中繼資料。
* 測試或稽核中繼資料以符合規範。
* 將中繼資料外部化，以個別地本地化。

1. 選取包含您要匯出中繼資料之資產的資產資料夾。 從工具列中，選擇「匯 **[!UICONTROL 出中繼資料]**」。

1. 在「中繼 [!UICONTROL 資料匯出] 」對話方塊中，指定CSV檔案的名稱。 若要匯出子檔案夾中資產的中繼資料，請選取「 **[!UICONTROL 在子檔案夾中包含資產」]**。

   ![匯出資料夾中所有資產的中繼資料的介面和選項匯](assets/export_metadata_page.png "出資料夾中所有資產的中繼資料的介面和選項")

1. 選擇所需的選項。 提供檔案名稱，並視需要提供日期。

1. 在要導 **[!UICONTROL 出的屬性欄位中]** ，指定要導出全部屬性還是要導出特定屬性。 如果選擇「選擇性屬性」以進行導出，請添加所需的屬性。

1. 在工具列中，按一下「 **[!UICONTROL 匯出]**」。 訊息會確認中繼資料已匯出。 關閉訊息。

1. 開啟導出作業的收件箱通知。選擇作業，然後從工具 **[!UICONTROL 欄中]** ，按一下「開啟」。To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. 按一下 **[!UICONTROL 關閉]**。

   ![對話方塊，以下載包含大量匯出之中繼資料的CSV檔案](assets/csv_download.png)

   *圖：對話方塊，以下載包含大量匯出之中繼資料的CSV檔案。*

## 編輯系列的中繼資料 {#collections-metadata}

如需詳細資訊，請 [參閱檢視和編輯系列中繼資料](/help/assets/managing-collections-touch-ui.md#view-edit-collection-metadata) , [以及大量編輯多個系列的中繼資料](/help/assets/managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)。

## 將中繼資料描述檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

將元資料配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承該配置檔案。 這表示您只能將一個中繼資料描述檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的檔案夾結構。

如果您指派不同的中繼資料描述檔給資料夾，新的描述檔會覆寫先前的描述檔。 舊有的資料夾資產仍維持不變。 新的描述檔會套用至稍後新增至資料夾的資產。

在用戶介面中，配置有配置檔案的資料夾將通過卡名稱中顯示的配置檔案名稱來指示。

![卡片檢視會顯示套用至資料夾的中繼資料描述檔](assets/metadata-profile-card-view-display.png)

您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理已有現有中繼資料設定檔的資料夾中的資產，而您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](processing-profiles.md#reprocessing-assets)。

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](processing-profiles.md#reprocessing-assets)。

### 從Profiles使用者介面將中繼資料描述檔套 [!UICONTROL 用至資料夾] 。 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

請依照下列步驟來套用中繼資料描述檔：

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. 選擇要應用於資料夾或多個資料夾的元資料配置檔案。
1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 從屬性將中繼資料描述檔套用至資 [!UICONTROL 料夾] {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側導軌中，按一下「 **[!UICONTROL 資產]** 」，然後導覽至您要套用中繼資料描述檔的檔案夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下「屬 **[!UICONTROL 性」]**。

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the popup menu and click **[!UICONTROL Save]**.

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### 從資料夾移除中繼資料描述檔 {#removing-a-metadata-profile-from-folders}

從資料夾中刪除元資料配置檔案時，任何子資料夾都會自動繼承從其父資料夾中刪除配置檔案。 不過，對檔案夾中發生的檔案處理仍維持不變。

您可以從「工具」功能表內的資料夾或從資料夾內的「屬性 **[!UICONTROL 」]****** ，移除中繼資料描述檔。

#### 透過描述檔使用者介面，從資料夾移除中繼資料描述檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. 選擇要從資料夾或多個資料夾中刪除的元資料配置檔案。
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   您可以確認中繼資料描述檔不再套用至資料夾，因為該名稱不會再顯示在資料夾名稱下方。

#### 透過屬性從資料夾移除中繼資料描述檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下 [!DNL Experience Manager] 標誌並導覽「 **[!UICONTROL 資產]** 」，然後導覽至您要移除中繼資料描述檔的資料夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下「屬 **[!UICONTROL 性」]**。
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

## 提示與限制 {#best-practices-limitations}

* 透過使用者介面的中繼資料更新會變更命名空間中的中繼資料 `dc` 屬性。 透過HTTP API進行的任何更新都會變更命名空間中的中繼資料 `jcr` 屬性。 瞭解 [如何使用HTTP API更新中繼資料](/help/assets/mac-api-assets.md#update-asset-metadata)。

* 匯入資產中繼資料的CSV檔案格式非常特定。 為節省心力和時間，並避免意外錯誤，您可以開始使用匯出的CSV檔案格式建立CSV。

* 使用CSV檔案匯入中繼資料時，必要的日期格式為 `YYYY-MM-DDThh:mm:ss.fff-00:00`。 如果使用其他格式，則不會設定日期值。 匯出的中繼資料CSV檔案的日期格式為格式 `YYYY-MM-DDThh:mm:ss-00:00`。 如果要匯入，請新增以表示的納秒值，將它轉換為可接受的格式 `fff`。

>[!MORELIKETHIS]
>
>* [中繼資料概念與理解](metadata-concepts.md)。
>* [編輯多個系列的中繼資料屬性](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [在Experience Manager Assets中匯入和匯出中繼資料](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
