---
title: 中繼資料功能的設定和管理。
description: 配置和管理與元資料添加和管理相關的 [!DNL Experience Manager Assets] 功能。
contentOwner: AG
role: Business Practitioner, Administrator
feature: Metadata
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 5%

---


# [!DNL Assets] {#config-metadata}中中繼資料功能的設定與管理

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] 保留每個資產的中繼資料。它可讓資產的分類和組織更輕鬆，並協助尋找特定資產的人。 透過使用資產保留和管理中繼資料的能力，您可以根據資產的中繼資料自動組織及處理資產。 [!DNL Adobe Experience Manager Assets] 可讓管理員設定和自訂中繼資料功能，以修改預設Adobe方案。

## 編輯中繼資料結構{#metadata-schema}

如需詳細資訊，請參閱[編輯中繼資料結構表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在[!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}中註冊自訂命名空間

您可以在[!DNL Experience Manager]中添加自己的名稱空間。 就像有預先定義的名稱空間（例如`cq`、`jcr`和`sling`）一樣，您也可以擁有儲存庫中繼資料和XML處理的名稱空間。

1. 訪問節點類型管理頁`https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`。
1. 要訪問命名空間管理頁，請按一下頁面頂部的&#x200B;**[!UICONTROL 名稱空間]**。
1. 若要新增命名空間，請按一下頁面底部的&#x200B;**[!UICONTROL New]**。
1. 在XML命名空間慣例中指定自訂命名空間。 以URI的形式指定ID，並為ID指定相關首碼。 按一下「**[!UICONTROL 儲存]**」。

## 設定大量中繼資料更新的限制{#bulk-metadata-update-limit}

若要防止類似拒絕服務(DOS)的情況，[!DNL Enterprise Manager]會限制Sling請求中支援的參數數。 一次更新許多資產的中繼資料時，您可能會達到限制，而且無法針對更多資產更新中繼資料。 Enterprise Manager會在日誌中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

若要變更限制，請存取&#x200B;**[!UICONTROL 工具]**>**[!UICONTROL 操作]**>**[!UICONTROL Web主控台]**，並變更&#x200B;**[!UICONTROL Apache Sling請求參數處理]** OSGi組態中的&#x200B;**[!UICONTROL 最大POST參數]**&#x200B;值。

## 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料描述檔並將它套用至資料夾。 您隨後上傳至資料夾的任何資產都會繼承您在中繼資料描述檔中設定的預設中繼資料。

### 新增中繼資料設定檔{#adding-a-metadata-profile}

1. 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料描述檔]**」，然後按一下「建立&#x200B;**[!UICONTROL a7/>」。]**
1. 輸入描述檔的標題，例如`Sample Metadata`，然後按一下「建立&#x200B;**[!UICONTROL 」。]**&#x200B;將顯示元資料配置檔案的[!UICONTROL 編輯表單]。

   ![編輯中繼資料表單](assets/metadata-edit-form.png)

1. 按一下元件，並在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中設定其屬性。 例如，按一下&#x200B;**[!UICONTROL Description]**&#x200B;元件並編輯其屬性。

   ![在元資料配置檔案中設定元件](assets/metadata-profile-component-setting.png)

   編輯&#x200B;**[!UICONTROL Description]**&#x200B;元件的以下屬性：

   * **[!UICONTROL 欄位標籤]**:中繼資料屬性的顯示名稱。僅供使用者參考。

   * **[!UICONTROL 對應至屬性]**:此屬性的值提供資產節點的相對路徑或名稱，該資產節點保存在儲存庫中。值應始終以`./`開頭，因為它表示路徑位於資產節點下。

   ![映射至中繼資料描述檔中的屬性設定](assets/metadata-profile-setting-map-property.png)

   您為&#x200B;**[!UICONTROL 映射至屬性]**&#x200B;指定的值會儲存為資產中繼資料節點下的屬性。 例如，如果您指定`./jcr:content/metadata/dc:desc`作為&#x200B;**[!UICONTROL 映射至屬性]**&#x200B;的名稱，[!DNL Assets]會將值`dc:desc`儲存在資產的中繼資料節點。

   * **[!UICONTROL 預設值]**:使用此屬性可為中繼資料元件新增預設值。例如，如果您指定「我的說明」，則此值會指派給資產中繼資料節點上的屬性`dc:desc`。

   ![在中繼資料描述檔中設定預設描述](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >新增預設值至新的中繼資料屬性(此屬性在中已不存在。 `/jcr:content/metadata` 節點)預設不會在資產的「屬性」頁面上顯示屬性及其值。要查看資產「 [!UICONTROL 屬性]」頁上的新屬性，請修改相應的模式表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| 元件 | 屬性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 欄位標籤， <br>說明 |
| [!UICONTROL 單行文字] | 欄位標籤， <br>映射到屬性， <br>預設值 |
| [!UICONTROL 多值文字] | 欄位標籤， <br>映射到屬性， <br>預設值 |
| [!UICONTROL 數量] | 欄位標籤， <br>映射到屬性， <br>預設值 |
| [!UICONTROL 日期] | 欄位標籤， <br>映射到屬性， <br>預設值 |
| [!UICONTROL 標準標記] | 欄位標籤， <br>映射到屬性， <br>預設值， <br>說明 |

1. 按一下&#x200B;**[!UICONTROL Done]**。 元資料配置檔案將添加到&#x200B;**[!UICONTROL 元資料配置檔案]**&#x200B;頁中的配置檔案清單。<br>

   ![「元資料配置檔案」頁中添加的元資料配置檔案](assets/MetadataProfiles-page.png)

### 複製元資料配置檔案{#copying-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料描述檔]**&#x200B;頁面中，選取中繼資料描述檔以製作其副本。

   ![複製中繼資料描述檔](assets/metadata-profile-edit-copy-option.png)

1. 按一下工具欄中的&#x200B;**[!UICONTROL Copy]**。
1. 在&#x200B;**[!UICONTROL 複製元資料配置檔案]**&#x200B;對話框中，輸入元資料配置檔案新副本的標題。
1. 按一下&#x200B;**[!UICONTROL Copy]**。 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

   ![在「中繼資料描述檔」頁面中新增的中繼資料描述檔復本](assets/copy-metadata-profile.png)

### 刪除元資料配置檔案{#deleting-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料描述檔]**&#x200B;頁面中，選取要刪除的描述檔。

1. 按一下工具欄中的&#x200B;**[!UICONTROL 刪除元資料配置檔案]**。
1. 在對話框中，按一下&#x200B;**[!UICONTROL Delete]**&#x200B;以確認刪除操作。 元資料配置檔案將從清單中刪除。

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

## 資料夾{#folder-metadata-schema}的中繼資料結構

[!DNL Adobe Experience Manager Assets] 可讓您為資產資料夾建立中繼資料結構，以定義資料夾屬性頁面中顯示的配置和中繼資料。

### 從{#add-a-folder-metadata-schema-form}中添加資料夾元資料架構

使用資料夾元資料結構Forms編輯器建立和編輯資料夾的元資料結構。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**。
1. 在[!UICONTROL 資料夾元資料結構Forms]頁上，按一下&#x200B;**[!UICONTROL 建立]**。
1. 指定表單的名稱，然後按一下「建立&#x200B;**[!UICONTROL 」。]**&#x200B;新模式表單列在[!UICONTROL 模式Forms]頁中。

### 編輯資料夾元資料結構表單{#edit-folder-metadata-schema-forms}

您可以編輯新增或現有的中繼資料結構表單，其中包含：

* 索引標籤
* 標籤內的表單項目。

您可以將這些表單項目映射／配置到CRX儲存庫中元資料節點中的欄位。 您可以將新標籤或表單項目新增至中繼資料結構表單。

1. 在「方案Forms」頁中，選擇您建立的表單，然後從工具欄中選擇&#x200B;**[!UICONTROL 編輯]**&#x200B;選項。
1. 在「資料夾元資料結構編輯器」頁中，按一下`+`將頁籤添加到窗體中。 若要重新命名標籤，請按一下預設名稱，並在&#x200B;**[!UICONTROL Settings]**&#x200B;下指定新名稱。

   ![custom_tab](assets/custom_tab.png)

   要添加更多頁籤，請按一下`+`。 按一下標籤上的`X`以刪除它。

1. 在活動頁籤中，從&#x200B;**[!UICONTROL 構建表單]**&#x200B;頁籤添加一個或多個元件。

   ![adding_components](assets/adding_components.png)

   如果您建立多個標籤，請按一下特定標籤以新增元件。

1. 要配置元件，請選擇該元件並在&#x200B;**[!UICONTROL Settings]**&#x200B;頁籤中修改其屬性。

   如果需要，請從&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中刪除元件。

   ![configure_properties](assets/configure_properties.png)

1. 按一下工具欄中的&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。

#### 建立表單的元件{#components-to-build-forms}

**[!UICONTROL 建立表單]**&#x200B;標籤列出您在資料夾中繼資料結構表單中使用的表單項目。 **[!UICONTROL Settings]**&#x200B;標籤顯示您在&#x200B;**[!UICONTROL Build Form]**&#x200B;標籤中選擇的每個項目的屬性。 以下列出&#x200B;**[!UICONTROL Build Form]**&#x200B;標籤中可用的表單項：

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

#### 編輯表單項目{#editing-form-items}

要編輯表單項的屬性，請按一下元件，並在&#x200B;**[!UICONTROL Settings]**&#x200B;頁籤中編輯以下所有屬性或屬性子集。

**[!UICONTROL 欄位標籤]**:顯示在資料夾屬性頁面上的元資料屬性的名稱。

**[!UICONTROL 對應至屬性]**:此屬性指定保存資料夾節點的CRX儲存庫中資料夾節點的相對路徑。開頭為&quot;**。/**&quot;，表示路徑位於資料夾節點下。

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`:將值儲存在資料夾的元資料節點中作為屬性 `dc:title`。

* `./jcr:created`:在資料夾的節點顯示JCR屬性。如果您在CRXDE中設定這些屬性，Adobe建議您將它們標示為「停用編輯」，因為它們受到保護。 否則，在保存資產屬性時，將發生錯誤「 `Asset(s) failed to modify`」。

要確保元資料架構表單中元件正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**:使用它來指定JSON檔案的路徑，您可在此指定選項的索引鍵值配對。

**[!UICONTROL 預留位置]**:使用此屬性可指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**:使用此屬性可指定清單中的選擇。

**[!UICONTROL 說明]**:使用此屬性可為中繼資料元件新增簡短說明。

**[!UICONTROL 類別]**:屬性與關聯的對象類。

### 刪除資料夾元資料架構表單{#delete-folder-metadata-schema-forms}

可以從「資料夾元資料結構」「Forms」頁刪除資料夾元資料結構表單。 要刪除表單，請選擇表單，然後從工具欄中按一下刪除選項。

![delete_form](assets/delete_form.png)

### 指派資料夾中繼資料結構{#assign-a-folder-metadata-schema}

您可以從「資料夾元資料結構」「Forms」頁或在建立資料夾時將資料夾元資料結構分配給資料夾。

如果為資料夾配置元資料模式，則模式表單的路徑將儲存在`./jcr:content`下資料夾節點的`folderMetadataSchema`屬性中。

#### 從「資料夾元資料結構」頁{#assign-to-a-schema-from-the-folder-metadata-schema-page}分配到結構

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**。
1. 從「資料夾元資料結構」「Forms」頁中，選擇要應用於資料夾的結構形式。
1. 在工具欄中，按一下&#x200B;**[!UICONTROL 應用到資料夾]**。

1. 選擇要應用模式的資料夾，然後按一下&#x200B;**[!UICONTROL Apply]**。 如果資料夾上已套用中繼資料結構，會出現警告訊息通知您即將覆寫現有的中繼資料結構。 按一下&#x200B;**[!UICONTROL 覆寫]**。
1. 開啟您套用中繼資料結構之資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   要查看資料夾元資料欄位，請按一下&#x200B;**[!UICONTROL 資料夾元資料]**&#x200B;頁籤。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 建立資料夾{#assign-a-schema-when-creating-a-folder}時分配模式

建立資料夾時，可以指定資料夾元資料方案。 如果系統中至少存在一個資料夾元資料模式，則在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話框中會顯示一個額外清單。 您可以選擇所需的架構。 預設情況下，未選擇任何模式。

1. 在[!DNL Experience Manager Assets]使用者介面中，從工具列按一下「建立&#x200B;**[!UICONTROL 」。]**
1. 指定資料夾的標題和名稱。
1. 從「資料夾元資料方案」清單中，選擇所需的方案。 然後，按一下&#x200B;**[!UICONTROL 建立]**。

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構之資料夾的中繼資料屬性。
1. 要查看資料夾元資料欄位，請按一下&#x200B;**[!UICONTROL 資料夾元資料]**&#x200B;頁籤。

### 使用資料夾元資料架構{#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。資料夾[!UICONTROL 屬性]頁中顯示&#x200B;**[!UICONTROL 資料夾元資料]**&#x200B;頁籤。 要查看資料夾元資料結構表單，請選擇此頁籤。

在各欄位中輸入中繼資料值，然後按一下「儲存」以儲存值。 ****&#x200B;您指定的值儲存在CRX儲存庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 提示和限制{#best-practices-limitations}

* 若要匯入自訂名稱空間上的中繼資料，請先註冊名稱空間。
* 「屬性選擇器」會顯示用於架構編輯器和搜尋表單的屬性。 屬性選擇器不會從資產中挑選中繼資料屬性。
* 升級至[!DNL Experience Manager] 6.5之前，您可能已有預先存在的中繼資料設定檔。升級後，如果您在[!UICONTROL 中繼資料描述檔]標籤的[!UICONTROL Properties]資料夾中套用此描述檔，則不會顯示中繼資料表單欄位。 不過，如果您套用新建立的中繼資料描述檔，表單欄位會顯示，但無法如預期般使用。 功能不會遺失，但如果您想查看（無法使用）表單欄位，請編輯並儲存現有的中繼資料設定檔。

>[!MORELIKETHIS]
>
>* [中繼資料概念與理解](metadata-concepts.md)。
>* [編輯多個系列的中繼資料屬性](manage-collections.md#editing-collection-metadata-in-bulk)。
>* [中繼資料在Experience Manager資產中匯入和匯出](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)。
>* [處理中繼資料、影像和視訊的設定檔](processing-profiles.md)。
>* [最佳實務：組織您的數位資產，以使用處理設定檔](/help/assets/organize-assets.md)。
>* [XMP回寫](/help/assets/xmp-writeback.md)。

