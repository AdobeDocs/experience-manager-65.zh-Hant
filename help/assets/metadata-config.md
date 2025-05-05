---
title: 中繼資料功能的設定和管理。
description: 與中繼資料新增和管理相關的 [!DNL Experience Manager Assets] 功能的設定和管理。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 3%

---

# 在[!DNL Assets]中設定和管理中繼資料功能 {#config-metadata}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets]保留每個資產的中繼資料。 它可讓您更輕鬆地分類及組織資產，並協助尋找特定資產的人。 有了使用資產保留和管理中繼資料的功能，您可以根據資產的中繼資料自動組織和處理資產。 [!DNL Adobe Experience Manager Assets]可讓管理員設定和自訂中繼資料功能，以修改預設Adobe方案。

## 編輯中繼資料結構 {#metadata-schema}

如需詳細資訊，請參閱[編輯中繼資料結構表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在[!DNL Experience Manager]中註冊自訂名稱空間 {#registering-a-custom-namespace-within-aem}

您可以在[!DNL Experience Manager]中新增您自己的名稱空間。 如同預先定義的名稱空間（例如`cq`、`jcr`和`sling`），您可以擁有儲存庫中繼資料和XML處理的名稱空間。

1. 存取節點型別管理頁面`https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`。
1. 若要存取名稱空間管理頁面，請按一下頁面頂端的&#x200B;**[!UICONTROL 名稱空間]**。
1. 若要新增名稱空間，請按一下頁面底部的&#x200B;**[!UICONTROL 新增]**。
1. 以XML名稱空間慣例指定自訂名稱空間。 以URI的形式指定ID，並為該ID指定關聯的前置詞。 按一下「**[!UICONTROL 儲存]**」。

## 設定大量中繼資料更新的限制 {#bulk-metadata-update-limit}

為避免發生拒絕服務(DOS)情況，[!DNL Enterprise Manager]會限制Sling要求中支援的引數數量。 一次更新許多資產的中繼資料時，您可能會達到限制，而且中繼資料不會更新以取得更多資產。 Enterprise Manager會在記錄檔中產生下列警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

若要變更限制，請存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**，並變更&#x200B;**[!UICONTROL Apache Sling要求引數處理]** OSGi設定中&#x200B;**[!UICONTROL 最大POST引數]**&#x200B;的值。

## 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料設定檔，並將其套用至資料夾。 您稍後上傳至資料夾的任何資產都會繼承您在中繼資料設定檔中設定的預設中繼資料。

### 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料設定檔]**，然後按一下&#x200B;**[!UICONTROL 建立]**。
1. 輸入設定檔的標題，例如`Sample Metadata`，然後按一下&#x200B;**[!UICONTROL 建立]**。 此時會顯示中繼資料設定檔的[!UICONTROL 編輯表單]。

   ![編輯中繼資料表單](assets/metadata-edit-form.png)

1. 按一下元件，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中設定其屬性。 例如，按一下&#x200B;**[!UICONTROL Description]**&#x200B;元件並編輯其屬性。

   ![在中繼資料設定檔中設定元件](assets/metadata-profile-component-setting.png)

   編輯&#x200B;**[!UICONTROL Description]**&#x200B;元件的下列屬性：

   * **[!UICONTROL 欄位標籤]**：中繼資料屬性的顯示名稱。 僅供使用者參考。

   * **[!UICONTROL 對應到屬性]**：此屬性的值提供儲存於存放庫中的資產節點相對路徑或名稱。 此值應一律以`./`開頭，因為它表示路徑在資產的節點下。

   ![對應到中繼資料設定檔中的屬性設定](assets/metadata-profile-setting-map-property.png)

   您為&#x200B;**[!UICONTROL 對應至屬性]**&#x200B;指定的值會儲存為資產中繼資料節點下的屬性。 例如，如果您指定`./jcr:content/metadata/dc:desc`作為&#x200B;**[!UICONTROL Map to property]**&#x200B;的名稱，[!DNL Assets]會將值`dc:desc`儲存在資產的中繼資料節點。 Adobe建議您只將一個欄位對應到中繼資料結構描述中的指定屬性。 否則，系統會挑選對應至屬性的最新新增欄位。

   * **[!UICONTROL 預設值]**：使用此屬性為中繼資料元件新增預設值。 例如，如果您指定「我的說明」，此值就會指派給資產中繼資料節點上的屬性`dc:desc`。

   ![在中繼資料設定檔中設定預設描述](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >將預設值新增至新的中繼資料屬性（不存在於`/jcr:content/metadata`節點）預設不會在資產的[!UICONTROL 屬性]頁面上顯示屬性及其值。 若要檢視資產[!UICONTROL 屬性]頁面上的新屬性，請修改對應的結構描述表單。

1. （選擇性）在&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中，新增更多元件至[!UICONTROL 編輯表單]，並在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中設定其屬性。 **[!UICONTROL 建置表單]**&#x200B;索引標籤中有以下屬性：

| 元件 | 屬性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 欄位標籤，<br>描述 |
| [!UICONTROL 單行文字] | 欄位標籤，<br>對應到屬性，<br>預設值 |
| [!UICONTROL 多值文字] | 欄位標籤，<br>對應到屬性，<br>預設值 |
| [!UICONTROL 數字] | 欄位標籤，<br>對應到屬性，<br>預設值 |
| [!UICONTROL 日期] | 欄位標籤，<br>對應到屬性，<br>預設值 |
| [!UICONTROL 標準標籤] | 欄位標籤，<br>對應到屬性，<br>預設值，<br>描述 |

1. 按一下&#x200B;**[!UICONTROL 完成]**。 已將中繼資料設定檔新增至&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面的設定檔清單。<br>

   ![中繼資料設定檔已新增至中繼資料設定檔頁面](assets/MetadataProfiles-page.png)

### 複製中繼資料設定檔 {#copying-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面，選取一個中繼資料設定檔以製作其副本。

   ![複製中繼資料設定檔](assets/metadata-profile-edit-copy-option.png)

1. 按一下工具列中的&#x200B;**[!UICONTROL 複製]**。
1. 在&#x200B;**[!UICONTROL 複製中繼資料設定檔]**&#x200B;對話方塊中，輸入新中繼資料設定檔副本的標題。
1. 按一下&#x200B;**[!UICONTROL 複製]**。 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

   ![在中繼資料設定檔頁面中新增了中繼資料設定檔的復本](assets/copy-metadata-profile.png)

### 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從&#x200B;**[!UICONTROL 中繼資料設定檔]**&#x200B;頁面，選取要刪除的設定檔。

1. 按一下工具列中的&#x200B;**[!UICONTROL 刪除中繼資料設定檔]**。
1. 在對話方塊中，按一下&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認刪除作業。 中繼資料設定檔會從清單中刪除。

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/tw/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

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

[!DNL Adobe Experience Manager Assets]可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的版面和中繼資料。

### 新增資料夾中繼資料結構表單 {#add-a-folder-metadata-schema-form}

使用資料夾中繼資料結構Forms編輯器可建立和編輯資料夾的中繼資料結構。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 資料夾中繼資料結構描述]**。
1. 在[!UICONTROL 資料夾中繼資料結構Forms]頁面上，按一下&#x200B;**[!UICONTROL 建立]**。
1. 指定表單的名稱，然後按一下&#x200B;**[!UICONTROL 建立]**。 新的結構描述表單列在[!UICONTROL 結構描述Forms]頁面中。

### 編輯資料夾中繼資料結構表單 {#edit-folder-metadata-schema-forms}

您可以編輯新新增或現有的中繼資料結構表單，其中包括：

* 標籤
* 索引標籤中的表單專案。

您可以將這些表單專案對應/設定至CRX存放庫中繼資料節點內的欄位。 您可以將新的索引標籤或表單專案新增到中繼資料結構表單。

1. 在「結構描述Forms」頁面中，選取您建立的表單，然後從工具列選取&#x200B;**[!UICONTROL 編輯]**&#x200B;選項。
1. 在「資料夾中繼資料結構編輯器」頁面中，按一下`+`以新增索引標籤至表單。 若要重新命名標籤，請按一下預設名稱，並在&#x200B;**[!UICONTROL 設定]**&#x200B;下指定新名稱。

   ![自訂標籤](assets/custom_tab.png)

   若要新增更多標籤，請按一下`+`。 若要刪除，請按一下索引標籤上的`X`。

1. 在使用中的索引標籤中，從&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤新增一或多個元件。

   ![正在新增_元件](assets/adding_components.png)

   如果您建立多個標籤，請按一下特定標籤以新增元件。

1. 若要設定元件，請選取該元件，並在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中修改其屬性。

   如有需要，請從&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中刪除元件。

   ![configure_properties](assets/configure_properties.png)

1. 若要儲存變更，請從工具列選取&#x200B;**[!UICONTROL 儲存]**。

#### 建立表單的元件 {#components-to-build-forms}

**[!UICONTROL 建置表單]**&#x200B;索引標籤會列出您在資料夾中繼資料結構描述表單中使用的表單專案。 **[!UICONTROL 設定]**&#x200B;索引標籤顯示您在&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中選取的每個專案的屬性。 以下是&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中可用的表單專案清單：

| 元件名稱 | 說明 |
|---|---|
| [!UICONTROL 區段標題] | 新增區段標題以取得常用元件清單。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它會儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它會儲存為字串陣列。 |
| [!UICONTROL 數字] | 新增數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式清單] | 新增下拉式清單。 |
| [!UICONTROL 標準標籤] | 新增標籤。 |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST引數的形式傳送。 |

#### 編輯表單專案 {#editing-form-items}

若要編輯表單專案的屬性，請按一下元件，然後在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中編輯下列所有屬性或屬性子集。

**[!UICONTROL 欄位標籤]**：資料夾屬性頁面上顯示的中繼資料屬性名稱。

**[!UICONTROL 對應至屬性]**：此屬性會指定資料夾節點在CRX存放庫中儲存位置的相對路徑。 它以「**」開頭。/**」，表示路徑在資料夾的節點下。

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`：將值儲存在資料夾的中繼資料節點，做為屬性`dc:title`。

* `./jcr:created`：在資料夾的節點顯示JCR屬性。 如果您在CRXDE中設定這些屬性，Adobe建議您將其標示為「停用編輯」，因為這些屬性受到保護。 否則，當您儲存資產的屬性時，就會發生錯誤&#39; `Asset(s) failed to modify`&#39;。

為確保元件在中繼資料結構表單中正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**：使用它來指定JSON檔案的路徑，您可在其中指定選項的索引鍵值配對。

**[!UICONTROL 預留位置]**：使用此屬性來指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**：使用此屬性指定清單中的選擇。

**[!UICONTROL 描述]**：使用此屬性為中繼資料元件新增簡短描述。

**[!UICONTROL 類別]**：與屬性關聯的物件類別。

### 刪除資料夾中繼資料結構表單 {#delete-folder-metadata-schema-forms}

您可以從「資料夾中繼資料結構Forms」頁面中刪除資料夾中繼資料結構表單。 若要刪除表單，請選取該表單，然後按一下工具列中的刪除選項。

![delete_form](assets/delete_form.png)

### 指派資料夾中繼資料結構 {#assign-a-folder-metadata-schema}

您可以從「資料夾中繼資料結構Forms」頁面或在建立資料夾時，將資料夾中繼資料結構指派給資料夾。

如果您設定資料夾的中繼資料結構，結構表單的路徑會儲存在`./jcr:content`下資料夾節點的`folderMetadataSchema`屬性中。

#### 從「資料夾中繼資料結構」頁面指派至結構 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 資料夾中繼資料結構描述]**。
1. 在「資料夾中繼資料結構Forms」頁面中，選取您要套用至資料夾的結構表單。
1. 在工具列中按一下&#x200B;**[!UICONTROL 套用至資料夾]**。

1. 選取要套用結構描述的資料夾，然後按一下[套用]。**&#x200B;** 如果資料夾已套用中繼資料結構，則會出現警告訊息，告知您即將覆寫現有的中繼資料結構。 按一下&#x200B;**[!UICONTROL 覆寫]**。
1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   若要檢視資料夾中繼資料欄位，請按一下&#x200B;**[!UICONTROL 資料夾中繼資料]**&#x200B;索引標籤。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### 建立資料夾時指派結構 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，您可以指派資料夾中繼資料結構。 如果系統中至少存在一個資料夾中繼資料結構描述，則&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話方塊中會顯示額外的清單。 您可以選取所需的結構描述。 依預設，不會選取結構描述。

1. 從[!DNL Experience Manager Assets]使用者介面，按一下工具列中的&#x200B;**[!UICONTROL 建立]**。
1. 指定資料夾的標題和名稱。
1. 從「資料夾中繼資料結構」清單中，選取所需的結構。 然後，按一下&#x200B;**[!UICONTROL 建立]**。

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構的資料夾的中繼資料屬性。
1. 若要檢視資料夾中繼資料欄位，請按一下&#x200B;**[!UICONTROL 資料夾中繼資料]**&#x200B;索引標籤。

### 使用資料夾中繼資料結構 {#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。**[!UICONTROL 資料夾中繼資料]**&#x200B;索引標籤會顯示在資料夾[!UICONTROL 內容]頁面中。 要查看資料夾元資料結構表單，請選擇此頁籤。

在各個欄位中輸入中繼資料值，然後按一下[儲存]儲存這些值。 **&#x200B;**&#x200B;您指定的值會儲存在CRX存放庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## 提示和限制 {#best-practices-limitations}

* 若要在自訂名稱空間上匯入中繼資料，請先註冊名稱空間。
* 屬性選取器會顯示用於結構描述編輯器和搜尋表單的屬性。 屬性選擇器不會從資產中挑選中繼資料屬性。
* 在升級至[!DNL Experience Manager] 6.5之前，您可能已有既存的中繼資料設定檔。升級之後，如果您在[!UICONTROL 中繼資料設定檔]索引標籤中的資料夾[!UICONTROL 屬性]中套用此類設定檔，則不會顯示中繼資料表單欄位。 不過，如果您套用新建立的中繼資料設定檔，表單欄位會顯示但如預期般無法使用。 功能不會遺失，但如果您想檢視（無法使用）表單欄位，則編輯並儲存現有的中繼資料設定檔。

>[!MORELIKETHIS]
>
>* [中繼資料概念與瞭解](metadata-concepts.md)。
>* [編輯多個集合的中繼資料屬性](manage-collections.md#editing-collection-metadata-in-bulk)。
>* [在Experience Manager Assets中匯入和匯出中繼資料](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html?lang=zh-Hant)。
>* [處理中繼資料、影像和影片的設定檔](processing-profiles.md)。
>* [組織您的數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md)。
>* [XMP回寫](/help/assets/xmp-writeback.md)。
