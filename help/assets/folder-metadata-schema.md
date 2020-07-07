---
title: 資料夾中繼資料結構
description: 瞭解如何在Adobe Experience Manager Assets中為資產資料夾建立中繼資料結構
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 4%

---


# 資料夾中繼資料結構 {#folder-metadata-schema}

Adobe Experience Manager Assets lets you create metadata schemas for asset folders, which define the layout and metadata displayed in folder properties pages.

## Add a folder metadata schema form {#add-a-folder-metadata-schema-form}

使用資料夾元資料結構表單編輯器可建立和編輯資料夾的元資料結構。

1. 在Experience Manager介面中，前往「工 **[!UICONTROL 具]** >資 **[!UICONTROL 產]** >資 **[!UICONTROL 料夾中繼資料結構]**」。
1. 在「檔案 [!UICONTROL 夾元資料結構表單」頁] ，按一下 **[!UICONTROL 建立]**。
1. 指定表單的名稱，然後按一下「建 **[!UICONTROL 立」]**。 新的架構表單列在「架構表 [!UICONTROL 單」頁中] 。

## Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

您可以編輯新增或現有的中繼資料結構表單，其中包含：

* 索引標籤
* 標籤內的表單項目。

您可以將這些表單項目映射／配置到CRX儲存庫中元資料節點中的欄位。 您可以將新標籤或表單項目新增至中繼資料結構表單。

1. In the Schema Forms page, select the form you created, and then select the **[!UICONTROL Edit]** option from the toolbar.
1. In the Folder Metadata Schema Editor page, click `+` to add a tab to the form. To rename the tab, click the default name and specify the new name under **[!UICONTROL Settings]**.

   ![custom_tab](assets/custom_tab.png)

   To add more tabs, click `+`. Click `X` on a tab to delete it.

1. 在作用中標籤中，從「建置表單」標籤中新增一 **[!UICONTROL 或多個元件]** 。

   ![adding_components](assets/adding_components.png)

   如果您建立多個標籤，請按一下特定標籤以新增元件。

1. 要配置元件，請選擇該元件並在「設定」頁籤中修改 **[!UICONTROL 其屬]** 性。

   If required, delete a component from the **[!UICONTROL Settings]** tab.

   ![configure_properties](assets/configure_properties.png)

1. 按一 **[!UICONTROL 下工具]** 列中的「儲存」以儲存變更。

### Components to build forms {#components-to-build-forms}

「構 **[!UICONTROL 建表單]** 」頁籤列出了資料夾元資料結構表單中使用的表單項。 「設 **[!UICONTROL 定]** 」標籤會顯示您在「建立表單」標籤中選取之每個項 **[!UICONTROL 目的屬性]** 。 以下是「建立表單」標籤中可用的表 **[!UICONTROL 單項目]** :

| 元件名稱 | 說明 |
|---|---|
| [!UICONTROL 區段標題] | 新增共用元件清單的區段標題。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它儲存為字串陣列。 |
| [!UICONTROL 數字] | 添加數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式] | 新增下拉式清單。 |
| [!UICONTROL 標準標記] | 新增標記. |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST參數傳送。 |

### 編輯表單項目 {#editing-form-items}

要編輯表單項的屬性，請按一下該元件，然後在「設定」頁籤中編輯以下所有屬性或 **[!UICONTROL 子集]** 。

**[!UICONTROL 欄位標籤]**: 顯示在資料夾屬性頁面上的元資料屬性的名稱。

**[!UICONTROL 對應至屬性]**: 此屬性指定保存資料夾節點的CRX儲存庫中資料夾節點的相對路徑。 它開頭是&quot;**./**&quot;，表示路徑位於資料夾節點下。

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`: 將值儲存在資料夾的元資料節點中作為屬性 `dc:title`。

* `./jcr:created`: 在資料夾的節點顯示JCR屬性。 如果您在CRXDE中設定這些屬性，Adobe建議您將它們標示為「停用編輯」，因為這些屬性受到保護。 否則，當您儲 `Asset(s) failed to modify`存資產的屬性時，會發生錯誤「」。

要確保元資料架構表單中元件正確顯示，請勿在屬性路徑中包含空格。

**[!UICONTROL JSON路徑]**: 使用它來指定JSON檔案的路徑，您可在此指定選項的索引鍵值配對。

**[!UICONTROL 預留位置]**: 使用此屬性可指定與中繼資料屬性相關的預留位置文字。

**[!UICONTROL 選擇]**: 使用此屬性可指定清單中的選擇。

**[!UICONTROL 說明]**: 使用此屬性可為中繼資料元件新增簡短說明。

**[!UICONTROL 類別]**: 屬性與關聯的對象類。

## Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

可以從「資料夾元資料結構表單」頁刪除資料夾元資料結構表單。 要刪除表單，請選擇表單，然後從工具欄中按一下刪除選項。

![delete_form](assets/delete_form.png)

## 指派資料夾中繼資料結構 {#assign-a-folder-metadata-schema}

您可以從「資料夾元資料結構表單」頁或在建立資料夾時將資料夾元資料結構表單分配給資料夾。

如果為資料夾配置元資料模式，則模式表單的路徑將儲存在資料夾節 `folderMetadataSchema` 點的屬性中。*/jcr:content*.

### 從「資料夾元資料方案」頁指定給方案 {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. 在Experience Manager介面中，前往「工 **[!UICONTROL 具]** >資 **[!UICONTROL 產]** >資 **[!UICONTROL 料夾中繼資料結構]**」。
1. 從「資料夾元資料結構表單」頁中，選擇要應用於資料夾的結構結構表單。
1. 在工具列中，按一 **[!UICONTROL 下套用至資料夾]**。

1. 選擇要應用方案的資料夾，然後按一下應 **[!UICONTROL 用]**。 如果資料夾上已套用中繼資料結構，會出現警告訊息通知您即將覆寫現有的中繼資料結構。 按一 **[!UICONTROL 下覆寫]**。
1. 開啟您套用中繼資料結構之資料夾的中繼資料屬性。

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### 在建立資料夾時分配方案 {#assign-a-schema-when-creating-a-folder}

建立資料夾時，可以指定資料夾元資料方案。 如果系統中至少存在一個資料夾元資料模式，則「建立資料夾」對話框中會顯 **[!UICONTROL 示一個額外清單]** 。 您可以選擇所需的架構。 預設情況下，未選擇任何模式。

1. 在使用 [!DNL Experience Manager Assets] 者介面中，按一下工 **[!UICONTROL 具列中的]** 「建立」。
1. 指定資料夾的標題和名稱。
1. 從「資料夾元資料方案」清單中，選擇所需的方案。 然後，按一下「 **[!UICONTROL 建立]**」。

   ![select_schema](assets/select_schema.png)

1. 開啟您套用中繼資料結構之資料夾的中繼資料屬性。
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

## 使用資料夾中繼資料結構 {#use-the-folder-metadata-schema}

開啟配置了資料夾元資料架構的資料夾的屬性。A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. 要查看資料夾元資料結構表單，請選擇此頁籤。

在各欄位中輸入中繼資料值，然後按一 **[!UICONTROL 下「儲存]** 」以儲存值。 您指定的值儲存在CRX儲存庫的資料夾節點中。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
