---
title: 中繼資料功能的設定和管理。
description: 配置和管理與元 [!DNL Experience Manager Assets] 資料添加和管理相關的功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c3f85314740c4e9ca8ed0c9a724b49ff4276616a
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 5%

---


# 中繼資料功能的設定與管理 [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。 它可讓資產的分類和組織更輕鬆，並協助尋找特定資產的人。 透過使用資產保留和管理中繼資料的能力，您可以根據資產的中繼資料自動組織及處理資產。 [!DNL Adobe Experience Manager Assets] 可讓管理員設定和自訂中繼資料功能，以修改預設的Adobe產品。

## 編輯中繼資料結構 {#metadata-schema}

如需詳細資訊，請參 [閱編輯中繼資料結構表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

您可以在中新增自己的名稱空間 [!DNL Experience Manager]。 就像有預先定義的名稱空間 `cq`(如、 `jcr`和 `sling`)一樣，您也可以為儲存庫元資料和XML處理提供一個命名空間。

1. 訪問節點類型管理頁 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`。
1. 若要存取命名空間管理頁面，請按 **[!UICONTROL 一下頁面頂端的]** 「命名空間」。
1. 若要新增命名空間，請 **[!UICONTROL 按一下]** 頁面底部的「新增」。
1. 在XML命名空間慣例中指定自訂命名空間。 以URI的形式指定ID，並為ID指定相關首碼。 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 設定大量中繼資料更新的限制 {#bulk-metadata-update-limit}

若要防止類似拒絕服務(DOS)的情況，請 [!DNL Enterprise Manager] 限制Sling請求中支援的參數數目。 一次更新許多資產的中繼資料時，您可能會達到限制，而且無法針對更多資產更新中繼資料。 Enterprise Manager會在日誌中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

## 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料描述檔並將它套用至資料夾。 您隨後上傳至資料夾的任何資產都會繼承您在中繼資料描述檔中設定的預設中繼資料。

### 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至「工 **[!UICONTROL 具]** >資產 **[!UICONTROL >中繼資料設定檔]** 」，然 ********&#x200B;後按一下「建立」。
1. 例如，輸入描述檔的標題，然 `Sample Metadata`後按一 **[!UICONTROL 下Create]**。 此時將顯示 [!UICONTROL 元資料配置檔案的編輯表單] 。

   ![編輯中繼資料表單](assets/metadata-edit-form.png)

1. 按一下元件，並在「設定」標籤中設 **[!UICONTROL 定其屬]** 性。 例如，按一下「說 **[!UICONTROL 明]** 」元件並編輯其屬性。

   ![在元資料配置檔案中設定元件](assets/metadata-profile-component-setting.png)

   編輯Description元件的以 **[!UICONTROL 下屬性]** :

   * **[!UICONTROL 欄位標籤]**:中繼資料屬性的顯示名稱。 僅供使用者參考。

   * **[!UICONTROL 對應至屬性]**:此屬性的值提供資產節點的相對路徑或名稱，該資產節點保存在儲存庫中。 值應一律以開頭 `./` ，因為它表示路徑位於資產的節點下。

   ![映射至中繼資料描述檔中的屬性設定](assets/metadata-profile-setting-map-property.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. 例如，如果您指定 `./jcr:content/metadata/dc:desc` 為「對應至屬性」的 **[!UICONTROL 名稱]**, [!DNL Assets] 則會將值 `dc:desc` 儲存在資產的中繼資料節點。

   * **[!UICONTROL 預設值]**:使用此屬性可為中繼資料元件新增預設值。 例如，如果您指定「我的說明」，則會將此值指派給資產中繼資 `dc:desc` 料節點的屬性。

   ![在中繼資料描述檔中設定預設描述](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >新增預設值至新的中繼資料屬性(此屬性在中已不存在。 `/jcr:content/metadata` 節點)預設不會在資產的「屬性」頁面上顯示屬性及其值。 要在資產的「屬性」頁上查看新屬 [!UICONTROL 性] ，請修改相應的架構表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| 元件 | 屬性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 欄位標籤，說 <br> 明 |
| [!UICONTROL 單行文字] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 多值文字] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 數量] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 日期] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 標準標記] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值、說 <br> 明 |

1. 按一 **[!UICONTROL 下完成]**。 中繼資料描述檔會新增至「中繼資料描述檔」頁面中的描 **[!UICONTROL 述檔清單]** 。<br>

   ![「元資料配置檔案」頁中添加的元資料配置檔案](assets/MetadataProfiles-page.png)

### 複製中繼資料描述檔 {#copying-a-metadata-profile}

1. 從「中 **[!UICONTROL 繼資料描述檔]** 」頁面中，選取中繼資料描述檔以製作其副本。

   ![複製中繼資料描述檔](assets/metadata-profile-edit-copy-option.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. 在「復 **[!UICONTROL 制中繼資料設定檔]** 」對話方塊中，輸入中繼資料設定檔新副本的標題。
1. 按一 **[!UICONTROL 下複製]**。 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

   ![在「中繼資料描述檔」頁面中新增的中繼資料描述檔復本](assets/copy-metadata-profile.png)

### 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從「中繼資 **[!UICONTROL 料描述檔]** 」頁面中，選取要刪除的描述檔。

1. 按一 **[!UICONTROL 下工具列中的刪除中繼資料]** 設定檔。
1. 在對話方塊中，按一下「 **[!UICONTROL 刪除]** 」以確認刪除作業。 元資料配置檔案將從清單中刪除。

<!-- TBD: Revisit to find out the correct config. and update these steps.
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## 資料夾的中繼資料結構 {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] 可讓您為資產資料夾建立中繼資料結構，以定義資料夾屬性頁面中顯示的配置和中繼資料。

### 添加資料夾元資料結構表單 {#add-a-folder-metadata-schema-form}

使用資料夾元資料結構表單編輯器可建立和編輯資料夾的元資料結構。

1. 在介 [!DNL Experience Manager] 面中，前往「工 **[!UICONTROL 具]** >資 **[!UICONTROL 產]** >資料 **[!UICONTROL 夾中繼資料結構]**」。
1. 在「檔案 [!UICONTROL 夾元資料結構表單」頁] ，按一下 **[!UICONTROL 建立]**。
1. 指定表單的名稱，然後按一下「建 **[!UICONTROL 立」]**。 新的架構表單列在「架構表 [!UICONTROL 單」頁中] 。

### Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

您可以編輯新增或現有的中繼資料結構表單，其中包含：

* 索引標籤
* 標籤內的表單項目。

您可以將這些表單項目映射／配置到CRX儲存庫中元資料節點中的欄位。 您可以將新標籤或表單項目新增至中繼資料結構表單。

1. 在「方案表單」頁中，選擇您建立的表單，然後從工具欄中選 **[!UICONTROL 擇]** 「編輯」選項。
1. 在「資料夾元資料結構編輯器」頁中，單 `+` 擊可向表單添加頁籤。 若要重新命名標籤，請按一下預設名稱，並在「設定」下指定新 **[!UICONTROL 名稱]**。

   ![custom_tab](assets/custom_tab.png)

   若要新增更多標籤，請按一下 `+`。 按一 `X` 下標籤以將其刪除。

1. 在作用中標籤中，從「建置表單」標籤中新增一 **[!UICONTROL 或多個元件]** 。

   ![adding_components](assets/adding_components.png)

   如果您建立多個標籤，請按一下特定標籤以新增元件。

1. 要配置元件，請選擇該元件並在「設定」頁籤中修改 **[!UICONTROL 其屬]** 性。

   如果需要，請從「設定」頁籤中刪 **[!UICONTROL 除元件]** 。

   ![configure_properties](assets/configure_properties.png)

1. 按一 **[!UICONTROL 下工具]** 列中的「儲存」以儲存變更。

#### 建立表單的元件 {#components-to-build-forms}

「構 **[!UICONTROL 建表單]** 」頁籤列出了資料夾元資料結構表單中使用的表單項。 「設 **[!UICONTROL 定]** 」標籤會顯示您在「建立表單」標籤中選取之每個項 **[!UICONTROL 目的屬性]** 。 以下是「建立表單」標籤中可用的表 **[!UICONTROL 單項目]** :

| 元件名稱 | 說明 |
|---|---|
| [!UICONTROL 區段標題] | 新增共用元件清單的區段標題。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它儲存為字串陣列。 |
| [!UICONTROL 數量] | 添加數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式] | 新增下拉式清單。 |
| [!UICONTROL 標準標記] | 新增標記. |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST參數傳送。 |

#### 編輯表單項目 {#editing-form-items}

要編輯表單項的屬性，請按一下該元件，然後在「設定」頁籤中編輯以下所有屬性或 **[!UICONTROL 子集]** 。

**[!UICONTROL 欄位標籤]**:顯示在資料夾屬性頁面上的元資料屬性的名稱。

**[!UICONTROL 對應至屬性]**:此屬性指定保存資料夾節點的CRX儲存庫中資料夾節點的相對路徑。 它開頭是&quot;**./**&quot;，表示路徑位於資料夾節點下。

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`:將值儲存在資料夾的元資料節點中作為屬性 `dc:title`。

* `./jcr:created`:在資料夾的節點顯示JCR屬性。 如果您在CRXDE中設定這些屬性，Adobe建議您將它們標示為「停用編輯」，因為這些屬性受到保護。 否則，當您儲 `Asset(s) failed to modify`存資產的屬性時，會發生錯誤「」。

要確保元資料架構表單中元件正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**:使用它來指定JSON檔案的路徑，您可在此指定選項的索引鍵值配對。

**[!UICONTROL 預留位置]**:使用此屬性可指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**:使用此屬性可指定清單中的選擇。

**[!UICONTROL 說明]**:使用此屬性可為中繼資料元件新增簡短說明。

**[!UICONTROL 類別]**:屬性與關聯的對象類。

### Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

可以從「資料夾元資料結構表單」頁刪除資料夾元資料結構表單。 要刪除表單，請選擇表單，然後從工具欄中按一下刪除選項。

![delete_form](assets/delete_form.png)

### 指派資料夾中繼資料結構 {#assign-a-folder-metadata-schema}

您可以從「資料夾元資料結構表單」頁或建立資料夾時，將資料夾元資料結構分配給資料夾。

如果為資料夾配置元資料模式，則模式表單的路徑將儲存在資料夾節 `folderMetadataSchema` 點下的屬性中 `./jcr:content`。

#### 從「資料夾元資料方案」頁指定給方案 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 在介 [!DNL Experience Manager] 面中，前往「工 **[!UICONTROL 具]** >資 **[!UICONTROL 產]** >資料 **[!UICONTROL 夾中繼資料結構]**」。
1. 從「資料夾元資料結構表單」頁中，選擇要應用於資料夾的結構結構表單。
1. 在工具列中，按一 **[!UICONTROL 下套用至資料夾]**。

1. 選擇要應用方案的資料夾，然後按一下應 **[!UICONTROL 用]**。 如果資料夾上已套用中繼資料結構，會出現警告訊息通知您即將覆寫現有的中繼資料結構。 按一 **[!UICONTROL 下覆寫]**。
1. 開啟您套用中繼資料結構之資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 在建立資料夾時分配方案 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，可以指定資料夾元資料方案。 如果系統中至少存在一個資料夾元資料模式，則「建立資料夾」對話框中將顯 **[!UICONTROL 示一個額外清單]** 。 您可以選擇所需的架構。 預設情況下，未選擇任何模式。

1. 在使用 [!DNL Experience Manager Assets] 者介面中，按一下工 **[!UICONTROL 具列中的]** 「建立」。
1. 指定資料夾的標題和名稱。
1. 從「資料夾元資料方案」清單中，選擇所需的方案。 然後，按一下「 **[!UICONTROL 建立]**」。

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構之資料夾的中繼資料屬性。
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

### 使用資料夾中繼資料結構 {#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. 要查看資料夾元資料結構表單，請選擇此頁籤。

在各欄位中輸入中繼資料值，然後按一 **[!UICONTROL 下「儲存]** 」以儲存值。 您指定的值儲存在CRX儲存庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 提示與限制 {#best-practices-limitations}

* 若要匯入自訂名稱空間上的中繼資料，請先註冊名稱空間。
* 「屬性選擇器」會顯示用於架構編輯器和搜尋表單的屬性。 屬性選擇器不會從資產中挑選中繼資料屬性。
* 升級至 [!DNL Experience Manager] 6.5之前，您可能已有預先存在的中繼資料設定檔。升級後，如果您在「中繼資料設定檔」索引標籤的 [!UICONTROL 資料夾] 「屬性」中套用  此類設定檔，則不會顯示中繼資料表格欄位。 不過，如果您套用新建立的中繼資料描述檔，表單欄位會顯示，但無法如預期般使用。 功能不會遺失，但如果您想查看（無法使用）表單欄位，請編輯並儲存現有的中繼資料設定檔。

>[!MORELIKETHIS]
>
>* [中繼資料概念與理解](metadata-concepts.md)。
>* [編輯多個系列的中繼資料屬性](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)。
>* [編輯多個系列的中繼資料屬性](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)。
>* [在Experience Manager Assets中匯入和匯出中繼資料](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)。
>* [處理中繼資料、影像和視訊的設定檔](processing-profiles.md)。
>* [最佳實務：組織您的數位資產，以使用處理設定檔](/help/assets/organize-assets.md)。
>* [XMP回寫](/help/assets/xmp-writeback.md)。

