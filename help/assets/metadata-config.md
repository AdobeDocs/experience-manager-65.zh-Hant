---
title: 中繼資料功能的設定和管理。
description: 配置和管理 [!DNL Experience Manager Assets] 與中繼資料新增和管理相關的功能。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 4%

---

# 中繼資料功能的設定及管理 [!DNL Assets] {#config-metadata}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/metadata-profiles.html?lang=en) |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。 它可讓資產分類和組織更輕鬆，並協助尋找特定資產的人。 您可以使用資產保留和管理中繼資料，並根據資產的中繼資料自動組織和處理資產。 [!DNL Adobe Experience Manager Assets] 可讓管理員設定和自訂中繼資料功能，以修改預設Adobe方案。

## 編輯中繼資料結構 {#metadata-schema}

如需詳細資訊，請參閱 [編輯中繼資料結構表單](metadata-schemas.md#edit-metadata-schema-forms).

## 在中註冊自訂命名空間 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

您可以在中新增您自己的命名空間 [!DNL Experience Manager]. 就像有預先定義的命名空間，例如 `cq`, `jcr`，和 `sling`，您可以擁有儲存庫中繼資料和XML處理的命名空間。

1. 訪問節點類型管理頁 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. 若要存取命名空間管理頁面，請按一下 **[!UICONTROL 命名空間]** 頁面頂端。
1. 若要新增命名空間，請按一下 **[!UICONTROL 新增]** 頁面底部。
1. 在XML命名空間約定中指定自訂命名空間。 以URI的形式指定ID以及ID的相關前置詞。 按一下「**[!UICONTROL 儲存]**」。

## 配置批量元資料更新的限制 {#bulk-metadata-update-limit}

為了防止發生類似DOS的情況， [!DNL Enterprise Manager] 限制Sling要求中支援的參數數量。 一次更新多個資產的中繼資料時，您可能會達到上限，且不會針對更多資產更新中繼資料。 Enterprise Manager會在記錄檔中產生下列警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

要更改限制，請訪問 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]** 並變更 **[!UICONTROL 最大POST參數]** in **[!UICONTROL Apache Sling要求參數處理]** OSGi配置。

## 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾內的資產。 建立中繼資料設定檔並將其套用至資料夾。 您稍後上傳至資料夾的任何資產都會繼承您在中繼資料設定檔中設定的預設中繼資料。

### 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]** 按一下 **[!UICONTROL 建立]**.
1. 輸入設定檔的標題，例如 `Sample Metadata`，然後按一下 **[!UICONTROL 建立]**. 此 [!UICONTROL 編輯表單] 中繼資料設定檔的。

   ![編輯中繼資料表單](assets/metadata-edit-form.png)

1. 按一下元件，並在 **[!UICONTROL 設定]** 標籤。 例如，按一下 **[!UICONTROL 說明]** 元件並編輯其屬性。

   ![在中繼資料描述檔中設定元件](assets/metadata-profile-component-setting.png)

   編輯下列屬性 **[!UICONTROL 說明]** 元件：

   * **[!UICONTROL 欄位標籤]**:中繼資料屬性的顯示名稱。 僅供使用者參考。

   * **[!UICONTROL 對應至屬性]**:此屬性的值提供儲存在儲存庫中的資產節點的相對路徑或名稱。 值應一律以開頭 `./` 因為它表示路徑位於資產的節點下。

   ![對應至中繼資料設定檔中的屬性設定](assets/metadata-profile-setting-map-property.png)

   您為指定的值 **[!UICONTROL 對應至屬性]** 會儲存為資產中繼資料節點下的屬性。 例如，如果您指定 `./jcr:content/metadata/dc:desc` 作為的名稱 **[!UICONTROL 對應至屬性]**, [!DNL Assets] 儲存值 `dc:desc` 在資產的中繼資料節點。 Adobe建議您只將一個欄位對應至中繼資料結構中的指定屬性。 否則，系統會挑選對應至屬性的最新新增欄位。

   * **[!UICONTROL 預設值]**:使用此屬性為元資料元件添加預設值。 例如，如果您指定「My description」，則會將此值指派給屬性 `dc:desc` 在資產的中繼資料節點。

   ![在中繼資料設定檔中設定預設說明](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >將預設值新增至新中繼資料屬性(不存在於 `/jcr:content/metadata` 節點)不會在資產的上顯示屬性及其值 [!UICONTROL 屬性] 頁面。 若要檢視資產上的新屬性 [!UICONTROL 屬性] 頁，修改相應的架構表單。

1. （選用）在 **[!UICONTROL 建置表單]** 標籤，將更多元件添加到 [!UICONTROL 編輯表單]，並在 **[!UICONTROL 設定]** 標籤。 下列屬性適用於 **[!UICONTROL 建置表單]** 標籤：

| Component | 屬性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 欄位標籤， <br> 說明 |
| [!UICONTROL 單行文字] | 欄位標籤， <br> 對應至屬性， <br> 預設值 |
| [!UICONTROL 多值文字] | 欄位標籤， <br> 對應至屬性， <br> 預設值 |
| [!UICONTROL 數字] | 欄位標籤， <br> 對應至屬性， <br> 預設值 |
| [!UICONTROL 日期] | 欄位標籤， <br> 對應至屬性， <br> 預設值 |
| [!UICONTROL 標準標記] | 欄位標籤， <br> 對應至屬性， <br> 預設值， <br> 說明 |

1. 按一下 **[!UICONTROL 完成]**. 中繼資料描述檔會新增至 **[!UICONTROL 中繼資料設定檔]** 頁面。<br>

   ![在「中繼資料描述檔」頁面中新增的中繼資料描述檔](assets/MetadataProfiles-page.png)

### 複製中繼資料設定檔 {#copying-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面，選擇元資料配置檔案以製作其副本。

   ![複製中繼資料設定檔](assets/metadata-profile-edit-copy-option.png)

1. 按一下 **[!UICONTROL 複製]** 的上界。
1. 在 **[!UICONTROL 複製中繼資料設定檔]** 對話框，輸入元資料配置檔案新副本的標題。
1. 按一下 **[!UICONTROL 複製]**. 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

   ![在「中繼資料描述檔」頁面中新增的中繼資料描述檔復本](assets/copy-metadata-profile.png)

### 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從 **[!UICONTROL 中繼資料設定檔]** 頁面，選擇要刪除的配置檔案。

1. 按一下 **[!UICONTROL 刪除中繼資料設定檔]** 的下一頁。
1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 確認刪除操作。 元資料設定檔會從清單中刪除。

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
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

[!DNL Adobe Experience Manager Assets] 可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的配置和中繼資料。

### 新增資料夾中繼資料結構表單 {#add-a-folder-metadata-schema-form}

使用資料夾中繼資料結構Forms編輯器，建立和編輯資料夾的中繼資料結構。

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**.
1. 在 [!UICONTROL 資料夾中繼資料結構Forms] 頁面，按一下 **[!UICONTROL 建立]**.
1. 指定表單的名稱，然後按一下 **[!UICONTROL 建立]**. 新架構表單會列於 [!UICONTROL 綱要Forms] 頁面。

### 編輯資料夾中繼資料結構表單 {#edit-folder-metadata-schema-forms}

您可以編輯新增或現有的中繼資料結構表單，其中包括：

* 索引標籤
* 標籤內的表單項目。

您可以將這些表單項目對應/設定至CRX存放庫中中繼資料節點內的欄位。 您可以將新索引標籤或表單項目新增至中繼資料結構表單。

1. 在「方案Forms」頁中，選擇您建立的表單，然後選擇 **[!UICONTROL 編輯]** 選項。
1. 在「資料夾元資料結構編輯器」頁中，按一下 `+` 將索引標籤新增至表單。 若要重新命名索引標籤，請按一下預設名稱，並在 **[!UICONTROL 設定]**.

   ![custom_tab](assets/custom_tab.png)

   若要新增更多索引標籤，請按一下 `+`. 若要刪除，請按一下 `X` 在標籤上。

1. 在作用中標籤中，從 **[!UICONTROL 建置表單]** 標籤。

   ![adding_components](assets/adding_components.png)

   如果您建立多個標籤，請按一下特定標籤以新增元件。

1. 若要設定元件，請選取元件，並修改其屬性，位於 **[!UICONTROL 設定]** 標籤。

   如有必要，請從 **[!UICONTROL 設定]** 標籤。

   ![configure_properties](assets/configure_properties.png)

1. 若要儲存變更，請選取 **[!UICONTROL 儲存]** 的上界。

#### 建立表單的元件 {#components-to-build-forms}

此 **[!UICONTROL 建置表單]** 索引標籤會列出您在資料夾中繼資料結構表單中使用的表單項目。 此 **[!UICONTROL 設定]** 索引標籤會顯示您在 **[!UICONTROL 建置表單]** 標籤。 以下是 **[!UICONTROL 建置表單]** 標籤：

| 元件名稱 | 說明 |
|---|---|
| [!UICONTROL 區段標題] | 新增區段標題，以取得通用元件清單。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 會儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 會儲存為字串陣列。 |
| [!UICONTROL 數字] | 新增數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式] | 新增下拉式清單。 |
| [!UICONTROL 標準標記] | 新增標記. |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 資產儲存時會以POST參數的形式傳送。 |

#### 編輯表單項目 {#editing-form-items}

要編輯表單項的屬性，請按一下元件並編輯以下屬性的全部或子集，位於 **[!UICONTROL 設定]** 標籤。

**[!UICONTROL 欄位標籤]**:顯示在資料夾屬性頁面上的元資料屬性的名稱。

**[!UICONTROL 對應至屬性]**:此屬性指定儲存CRX儲存庫中資料夾節點的相對路徑。 開頭為「**./**&quot; ，表示路徑位於資料夾節點下。

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`:將值儲存在資料夾的中繼資料節點，作為屬性 `dc:title`.

* `./jcr:created`:在資料夾的節點顯示JCR屬性。 如果您在CRXDE中設定這些屬性，Contaign建議您將它們標示為「停用編輯」，因為這些屬性受到保護。 否則，錯誤&#39; `Asset(s) failed to modify`「 」會在您儲存資產的屬性時發生。

若要確保元件在中繼資料結構表單中正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**:使用它來指定JSON檔案的路徑，您可在此指定選項的索引鍵值配對。

**[!UICONTROL 預留位置]**:使用此屬性可指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**:使用此屬性可指定清單中的選擇。

**[!UICONTROL 說明]**:使用此屬性可為中繼資料元件新增簡短說明。

**[!UICONTROL 類別]**:屬性關聯的對象類。

### 刪除資料夾元資料結構表單 {#delete-folder-metadata-schema-forms}

您可以從「資料夾元資料結構」「Forms」頁中刪除資料夾元資料結構表單。 若要刪除表單，請選取表單，然後按一下工具列中的刪除選項。

![delete_form](assets/delete_form.png)

### 指派資料夾中繼資料結構 {#assign-a-folder-metadata-schema}

您可以從「資料夾元資料結構」Forms頁或建立資料夾時，將資料夾元資料結構分配給資料夾。

如果為資料夾配置元資料架構，架構表單的路徑將儲存在 `folderMetadataSchema` 下資料夾節點的屬性 `./jcr:content`.

#### 從「資料夾元資料結構」頁指定到結構 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**.
1. 從「資料夾元資料結構Forms」頁中，選擇要應用於資料夾的結構表單。
1. 在工具列中，按一下 **[!UICONTROL 應用於資料夾]**.

1. 選擇要應用架構的資料夾，然後按一下 **[!UICONTROL 套用]**. 如果資料夾上已套用中繼資料結構，警告訊息會通知您即將覆寫現有的中繼資料結構。 按一下 **[!UICONTROL 覆寫]**.
1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   若要檢視資料夾中繼資料欄位，請按一下 **[!UICONTROL 資料夾中繼資料]** 標籤。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 建立資料夾時指派結構 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，您可以指派資料夾中繼資料結構。 如果系統中至少存在一個資料夾元資料架構，則會在 **[!UICONTROL 建立資料夾]** 對話框。 您可以選取所需的結構。 預設情況下，不選擇任何架構。

1. 從 [!DNL Experience Manager Assets] 使用者介面，按一下 **[!UICONTROL 建立]** 的上界。
1. 指定資料夾的標題和名稱。
1. 從「資料夾元資料結構」清單中，選擇所需的結構。 然後，按一下 **[!UICONTROL 建立]**.

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。
1. 若要檢視資料夾中繼資料欄位，請按一下 **[!UICONTROL 資料夾中繼資料]** 標籤。

### 使用資料夾中繼資料結構 {#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。A **[!UICONTROL 資料夾中繼資料]** 標籤 [!UICONTROL 屬性] 頁面。 要查看資料夾元資料結構表單，請選擇此頁籤。

在各種欄位中輸入中繼資料值，然後按一下 **[!UICONTROL 儲存]** 來儲存值。 您指定的值會儲存在CRX存放庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 提示和限制 {#best-practices-limitations}

* 若要匯入自訂命名空間上的中繼資料，請先註冊命名空間。
* 屬性選擇器顯示架構編輯器和搜尋表單中使用的屬性。 屬性選擇器不會從資產中挑選中繼資料屬性。
* 在升級至之前，您可能已有之前的中繼資料設定檔 [!DNL Experience Manager] 6.5.升級後，若您在資料夾中套用此設定檔 [!UICONTROL 屬性] in [!UICONTROL 中繼資料設定檔] 索引標籤中，中繼資料表單欄位不會顯示。 不過，如果您套用新建立的中繼資料設定檔，表單欄位會顯示，但無法如預期使用。 功能並未遺失，但如果您想查看（無法使用）表單欄位，請編輯並儲存現有的中繼資料設定檔。

>[!MORELIKETHIS]
>
>* [中繼資料概念與了解](metadata-concepts.md).
>* [編輯多個集合的中繼資料屬性](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Experience Manager Assets中的中繼資料匯入和匯出](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [處理中繼資料、影像和視訊的設定檔](processing-profiles.md).
>* [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).
>* [XMP回寫](/help/assets/xmp-writeback.md).

