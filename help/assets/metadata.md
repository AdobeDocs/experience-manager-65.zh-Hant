---
title: 在 [!DNL Adobe Experience Manager]中管理數位資產的中繼資料。
description: '瞭解中繼資料的類型，以及如何根據資產的中繼資料自動組織和處理資產。 [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31dcf48691fa849f757579e2e57dc3a9c2bbbbee
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 10%

---


# 管理數位資產的中繼資料{#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。它可讓資產的分類和組織更輕鬆，並協助尋找特定資產的人。 透過從上傳至[!DNL Experience Manager Assets]的檔案擷取中繼資料的功能，中繼資料管理與創意工作流程整合。 透過使用資產保留和管理中繼資料的能力，您可以根據資產的中繼資料自動組織及處理資產。

## 中繼資料及其來源{#how-to-edit-or-add-metadata}

中繼資料是可搜尋之資產的其他資訊。 它會新增至資產，並在[!DNL Experience Manager]中，在您上傳資產時加以處理。 您可以編輯現有的中繼資料，將新的中繼資料屬性新增至現有欄位。 組織需要可控且可靠的中繼資料辭彙。 因此，[!DNL Experience Manager Assets]不允許隨選新增中繼資料屬性。 只有管理員和開發人員才能新增包含中繼資料的屬性或欄位。 使用者可以在現有欄位中填入中繼資料。

下列方法可用來新增中繼資料至數位資產：

* 首先，建立資產的原生應用程式會新增一些中繼資料。 例如，[Acrobat將一些元資料](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html)添加到PDF檔案中，或者攝像頭將一些基本元資料添加到照片中。 產生資產時，您可以在原生應用程式本身新增中繼資料。 例如，您可以[在LightroomAdobe中添加IPTC元資料。](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html)

* 在將資產上傳至[!DNL Experience Manager]之前，您可以使用用來建立資產的原生應用程式或使用某些其他中繼資料編輯應用程式來編輯和修改中繼資料。 當您將資產上傳至Experience Manager時，會處理中繼資料。 例如，請參閱[如何在 [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html)中使用中繼資料，並查看[!DNL Adobe Exchange]中 [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html)的[標籤面板。

* 在[!DNL Experience Manager Assets]中，您可以在[!UICONTROL 屬性]頁面中手動新增或編輯資產的中繼資料。

* 當資產上傳至DAM時，您可運用[[!DNL Experience Manager Assets]的中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles)功能，自動新增中繼資料。

## 在[!DNL Experience Manager Assets] {#add-edit-metadata}中新增或編輯中繼資料

若要編輯[!DNL Assets]使用者介面中資產的中繼資料，請依照下列步驟進行：

1. 執行下列任一項作業：

   * 從[!DNL Assets]介面中，選擇資產，然後從工具列中按一下「查看屬性」。****
   * 從資產縮圖中，選擇&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;快速動作。
   * 在資產頁面中，從工具列按一下「檢視屬性」**[!UICONTROL 「資產資訊」圖示](assets/do-not-localize/info-circle-icon.png)。]**![

   資產頁面會顯示資產的所有中繼資料。 當資產上傳（收錄）至[!DNL Experience Manager]時，會擷取中繼資料。

   ![選取資產的屬性以檢視其中繼資料](assets/asset-metadata.png)

   *圖：在資產屬性頁面上編輯或新增  中繼資料。*

1. 視需要對各種標籤下的中繼資料進行編輯，然後在完成時，按一下工具列中的「儲存&#x200B;****」以儲存您所做的變更。 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;返回[!DNL Assets] Web介面。

   >[!NOTE]
   >
   >如果文字欄位空白，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並儲存它以新增該中繼資料屬性。

對資產中繼資料所做的任何變更都會寫入原始二進位檔，作為其資料的一XMP部分。 中繼資料回寫工作流程會將中繼資料新增至原始二進位檔。 對現有屬性（如`dc:title`）所做的變更會被覆寫，而新屬性（包括如`cq:tags`的自訂屬性）會隨架構新增。

支XMP持並啟用[技術要求中所述的平台和檔案格式的回寫。](/help/sites-deploying/technical-requirements.md)

## 編輯多個資產的中繼資料屬性{#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] 可讓您同時編輯多個資產的中繼資料，以便快速將一般中繼資料變更大量傳播至資產。您也可以大量編輯多個系列的中繼資料。 使用「屬性」頁面，對多個資產或系列執行中繼資料變更：

* 將中繼資料屬性變更為公用值
* 新增或修改標籤

要自定義元資料屬性頁，包括添加、修改、刪除元資料屬性，請使用[架構編輯器](metadata-config.md#folder-metadata-schema)。

>[!NOTE]
>
>大量編輯方法適用於資料夾或系列中的可用資產。 對於跨資料夾可用或符合一般准則的資產，可在搜尋](search-assets.md#metadataupdates)後，大量更新中繼資料。[

1. 在[!DNL Assets]使用者介面中，導覽至您要編輯的資產所在的位置。
1. 選取您要編輯其常用屬性的資產。
1. 在工具列中，按一下「屬性&#x200B;****」以開啟所選資產的屬性頁面。
1. 修改各種標籤下所選資產的中繼資料屬性。
1. 若要檢視特定資產的中繼資料，請取消在清單中選取剩餘資產。 如果您取消在[!UICONTROL 屬性]頁面上選取一些資產，則不會更新這些資產的中繼資料。
1. 要為資產選擇不同的元資料模式，請按一下工具欄中的&#x200B;**[!UICONTROL Settings]** ，然後選擇模式。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。
1. 若要在包含多個值的欄位中，將新中繼資料與現有中繼資料一起附加，請選取「附 **[!UICONTROL 加模式」]**。如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。按一下&#x200B;**[!UICONTROL 提交]**。

![中繼資料結構大量套用至多個資產](assets/metadata-schema-bulk-edit.gif)

>[!CAUTION]
>
>對於單值欄位，即使您選擇「附加模式」，新元資料也不會附加到欄位中的現 **[!UICONTROL 有值]**。

## 匯入中繼資料{#import-metadata}

[!DNL Assets] 可讓您使用CSV檔案大量匯入資產中繼資料。您可以匯入CSV檔案，對最近上傳的資產或現有資產進行大量更新。 您也可以從協力廠商系統，以CSV格式大量內嵌資產中繼資料。

中繼資料匯入是非同步的，不會影響系統效能。 如果已勾選工作流程標幟，由於回寫活動，多個資產的中繼資料同時更XMP新會耗費大量資源。 在精簡伺服器使用期間規劃此類匯入，以免影響其他使用者的效能。

>[!NOTE]
>
>若要匯入自訂名稱空間上的中繼資料，請先註冊名稱空間。

1. 導覽至[!DNL Assets]使用者介面，然後從工具列按一下「建立&#x200B;**[!UICONTROL 」。]**
1. 從菜單中，選擇&#x200B;**[!UICONTROL 元資料]**。
1. 在&#x200B;**[!UICONTROL 中繼資料匯入]**&#x200B;頁面中，按一下&#x200B;**[!UICONTROL 選擇檔案]**。 選取包含中繼資料的CSV檔案。
1. 指定下列參數。 請參閱[metadata-import-sample-file.csv](/help/assets/assets/metadata-import-sample-file.csv)的範例CSV檔案。

   | 中繼資料匯入參數 | 說明 |
   |:---|:---|
   | [!UICONTROL 批次大小] | 要匯入中繼資料的批次中資產數。 預設值為 50。最大值為100。 |
   | [!UICONTROL 欄位分隔符號] | 預設值為`,`（逗號）。 您可以指定任何其他字元。 |
   | [!UICONTROL 多值分隔符號] | 中繼資料值的分隔符號。 預設值為 `|`. |
   | [!UICONTROL 啟動工作流程] | 預設為False。 設為`true`時，[!UICONTROL DAM中繼資料回寫]工作流程（將中繼資料寫入二進位資料）的預設啟動程式設定XMP有效。 啟用啟動工作流程會拖慢系統運作速度。 |
   | [!UICONTROL 資產路徑欄名稱] | 定義含資產之CSV檔案的欄名。 |

1. 從工具列按一下「匯入」。 ****&#x200B;匯入中繼資料後，通知會顯示在[!UICONTROL Notification]收件匣中。

1. 若要確認正確的匯入，請導覽至資產的[!UICONTROL 屬性]頁面，並驗證欄位中的值。

若要在匯入中繼資料時新增日期和時間戳記，請使用`YYYY-MM-DDThh:mm:ss.fff-00:00`格式記錄日期和時間。 日期和時間以`T`分隔，`hh`為24小時格式的小時，`fff`為納秒，`-00:00`為時區偏移。 例如，`2020-03-26T11:26:00.000-07:00`是2020年3月26日11:26:00.000 AM PST時間。

>[!CAUTION]
>
>如果日期格式與`YYYY-MM-DDThh:mm:ss.fff-00:00`不匹配，則不設定日期值。 匯出的中繼資料CSV檔案的日期格式為`YYYY-MM-DDThh:mm:ss-00:00`格式。 如果要導入它，請通過添加由`fff`表示的納秒值將其轉換為可接受的格式。

## 匯出中繼資料{#export-metadata}

您可以匯出CSV格式的多個資產的中繼資料。 中繼資料會以非同步方式匯出，不會影響系統的效能。 要導出元資料，[!DNL Experience Manager]將遍歷資產節點`jcr:content/metadata`及其子節點的屬性，並將元資料屬性導出為CSV檔案。

大量匯出中繼資料的幾個使用案例包括：

* 移轉資產時，匯入第三方系統中的中繼資料。
* 與更廣大的專案團隊共用資產中繼資料。
* 測試或稽核中繼資料以符合規範。
* 將中繼資料外部化，以個別地本地化。

1. 選取包含您要匯出中繼資料之資產的資產資料夾。 在工具欄中，選擇&#x200B;**[!UICONTROL 導出元資料]**。

1. 在[!UICONTROL 中繼資料匯出]對話方塊中，指定CSV檔案的名稱。 若要匯出子檔案夾中資產的中繼資料，請選取「在子檔案夾中包含資產」]**。**[!UICONTROL 

   ![匯出資料夾中所有資產的中繼資料的介面和選項匯](assets/export_metadata_page.png "出資料夾中所有資產的中繼資料的介面和選項")

1. 選擇所需的選項。 提供檔案名稱，並視需要提供日期。

1. 在&#x200B;**[!UICONTROL 要導出的屬性]**&#x200B;欄位中，指定要導出所有屬性還是要導出特定屬性。 如果選擇「選擇性屬性」以進行導出，請添加所需的屬性。

1. 在工具列中，按一下「匯出」。 ****&#x200B;訊息會確認中繼資料已匯出。 關閉訊息。

1. 開啟導出作業的收件箱通知。選擇作業，然後從工具 **[!UICONTROL 欄中]** ，按一下「開啟」。若要下載包含中繼資料的CSV檔案，請從工具列按一下「CSV下載」。 ****&#x200B;按一下 **[!UICONTROL 關閉]**。

   ![對話方塊，以下載包含大量匯出之中繼資料的CSV檔案](assets/csv_download.png)

   *圖：對話方塊，以下載包含大量匯出之中繼資料的CSV檔案。*

## 編輯系列{#collections-metadata}的中繼資料

如需詳細資訊，請參閱[檢視並編輯系列中繼資料](/help/assets/manage-collections.md#view-edit-collection-metadata)和[大量編輯多個系列的中繼資料。](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk)

## 將元資料配置檔案應用於資料夾{#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

將元資料配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承該配置檔案。 這表示您只能將一個中繼資料描述檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的檔案夾結構。

如果您指派不同的中繼資料描述檔給資料夾，新的描述檔會覆寫先前的描述檔。 舊有的資料夾資產仍維持不變。 新的描述檔會套用至稍後新增至資料夾的資產。

在用戶介面中，配置有配置檔案的資料夾將通過卡名稱中顯示的配置檔案名稱來指示。

![卡片檢視會顯示套用至資料夾的中繼資料描述檔](assets/metadata-profile-card-view-display.png)

您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理已有現有中繼資料設定檔的資料夾中的資產，而您稍後會加以變更。 請參閱編輯資料夾的處理設定檔](processing-profiles.md#reprocessing-assets)後，重新處理資料夾中的資產。[

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。 請參閱編輯資料夾的處理設定檔](processing-profiles.md#reprocessing-assets)後，重新處理資料夾中的資產。[

### 將中繼資料描述檔套用至來自[!UICONTROL Profiles]使用者介面{#applying-metadata-profiles-to-folders-from-profiles-user-interface}的資料夾

請依照下列步驟來套用中繼資料描述檔：

1. 按一下[!DNL Experience Manager]標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料描述檔]**。
1. 選擇要應用於資料夾或多個資料夾的元資料配置檔案。
1. 按一下「將中繼資料描述檔套用至資料夾」]**，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，然後按一下「完成」**[!UICONTROL 。 ****&#x200B;已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 將中繼資料描述檔套用至[!UICONTROL Properties] {#applying-metadata-profiles-to-folders-from-properties}的資料夾

1. 在左側導軌中，按一下「資產」，然後導覽至您要套用中繼資料描述檔的資料夾。****
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 選擇&#x200B;**[!UICONTROL 元資料配置檔案]**&#x200B;頁籤，然後從彈出菜單中選擇配置檔案，然後按一下&#x200B;**[!UICONTROL 保存]**。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### 從資料夾{#removing-a-metadata-profile-from-folders}中刪除元資料配置檔案

從資料夾中刪除元資料配置檔案時，任何子資料夾都會自動繼承從其父資料夾中刪除配置檔案。 不過，對檔案夾中發生的檔案處理仍維持不變。

您可以從&#x200B;**[!UICONTROL Tools]**&#x200B;菜單或從&#x200B;**[!UICONTROL Properties]**&#x200B;資料夾中刪除元資料配置檔案。

#### 通過Profiles用戶介面{#removing-metadata-profiles-from-folders-via-profiles-user-interface}從資料夾中刪除元資料配置檔案

1. 按一下[!DNL Experience Manager]標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料描述檔]**。
1. 選擇要從資料夾或多個資料夾中刪除的元資料配置檔案。
1. 按一下&#x200B;**[!UICONTROL 從資料夾中刪除元資料配置檔案]**&#x200B;並選擇要從中刪除配置檔案的資料夾或多個資料夾，然後按一下&#x200B;**[!UICONTROL Done]**。

   您可以確認中繼資料描述檔不再套用至資料夾，因為該名稱不會再顯示在資料夾名稱下方。

#### 透過屬性{#removing-metadata-profiles-from-folders-via-properties}從資料夾移除中繼資料描述檔

1. 按一下[!DNL Experience Manager]標誌並導覽&#x200B;**[!UICONTROL Assets]**，然後導覽至您要移除中繼資料描述檔的資料夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下&#x200B;**[!UICONTROL 屬性]**。
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

## 提示和限制{#best-practices-limitations}

* 透過使用者介面更新的中繼資料會變更`dc`命名空間中的中繼資料屬性。 透過HTTP API進行的任何更新都會變更`jcr`命名空間中的中繼資料屬性。 請參閱[如何使用HTTP API](/help/assets/mac-api-assets.md#update-asset-metadata)更新中繼資料。

* 匯入資產中繼資料的CSV檔案格式非常特定。 為節省心力和時間，並避免意外錯誤，您可以開始使用匯出的CSV檔案格式建立CSV。

* 使用CSV檔案匯入中繼資料時，所需的日期格式為`YYYY-MM-DDThh:mm:ss.fff-00:00`。 如果使用其他格式，則不會設定日期值。 匯出的中繼資料CSV檔案的日期格式為`YYYY-MM-DDThh:mm:ss-00:00`格式。 如果要導入它，請通過添加由`fff`表示的納秒值將其轉換為可接受的格式。

>[!MORELIKETHIS]
>
>* [中繼資料概念與理解](metadata-concepts.md)。
>* [編輯多個系列的中繼資料屬性](manage-collections.md#editing-collection-metadata-in-bulk)
>* [在Experience Manager資產中匯入和匯出中繼資料](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


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
