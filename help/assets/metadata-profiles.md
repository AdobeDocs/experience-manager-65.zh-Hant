---
title: 自訂資產中繼資料需求的中繼資料設定檔
description: 瞭解資產的中繼資料設定檔。 瞭解如何建立中繼資料描述檔並將它套用至資料夾資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 17%

---


# 中繼資料設定檔 {#metadata-profiles}

中繼資料設定檔可讓您將預設中繼資料套用至資料夾中的資產。 建立中繼資料描述檔並將它套用至資料夾。 您隨後上傳至資料夾的任何資產都會繼承您在中繼資料描述檔中設定的預設中繼資料。

## 新增中繼資料設定檔 {#adding-a-metadata-profile}

1. 導覽至「工 **[!UICONTROL 具>資產>中繼資料設定檔]** 」，然後按 **[!UICONTROL 一下「建立]**」。
1. 輸入中繼資料描述檔的標題，例如範例中繼資料，然後按一下「建 **[!UICONTROL 立]**」。 此時將顯示 [!UICONTROL 元資料配置檔案的編輯表單] 。

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. 按一下元件，並在「設定」標籤中設 **[!UICONTROL 定其屬]** 性。 例如，按一下「說 **[!UICONTROL 明]** 」元件並編輯其屬性。

   ![chlimage_1-198](assets/chlimage_1-481.png)

   編輯Description元件的以 **[!UICONTROL 下屬性]** :

   * **[!UICONTROL 欄位標籤]**: 中繼資料屬性的顯示名稱。 僅供使用者參考。

   * **[!UICONTROL 對應至屬性]**: 此屬性的值為資產節點提供了相對路徑／名稱，該資產節點保存在儲存庫中。 值應一律以開頭 `./` ，因為它表示路徑位於資產的節點下。
   ![chlimage_1-199](assets/chlimage_1-482.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. 例如，如果您指定。`/jcr:content/metadata/dc:desc` AEM Assets會將值儲 **[!UICONTROL 存在資產的中繼資料節點，作為]**`dc:desc` 「對應至屬性」的名稱。

   * **[!UICONTROL 預設值]**: 使用此屬性可為中繼資料元件新增預設值。 例如，如果您指定「我的說明」，則會將此值指派給資產中繼資 `dc:desc` 料節點的屬性。
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >新增預設值至新的中繼資料屬性(此屬性在中已不存在。 `/jcr:content/metadata` 節點)預設不會在資產的「屬性」頁面上顯示屬性及其值。 要在資產的「屬性」頁上查看新屬 [!UICONTROL 性] ，請修改相應的架構表單。

1. (可選) 從「建置表單」標籤新增更多元件至「 **[!UICONTROL 編輯表單]** 」，並在「設定」標籤中設定 **[!UICONTROL 其屬性]** 。「生成表單」頁籤提供 **[!UICONTROL 以下屬性]** :

| 元件 | 屬性 |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 欄位標籤，說 <br> 明 |
| [!UICONTROL 單行文字] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 多值文字] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 數字] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 日期] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值 |
| [!UICONTROL 標準標記] | 欄位標籤、 <br> 對應至屬性、預 <br> 設值、說 <br> 明 |

![chlimage_1-201](assets/chlimage_1-484.png)

1. 按一 **[!UICONTROL 下完成]**。 中繼資料描述檔會新增至「中繼資料描述檔」頁面中的描 **[!UICONTROL 述檔清單]** 。<br>

   ![「元資料配置檔案」頁中添加的元資料配置檔案](assets/MetadataProfiles-page.png)

## 複製中繼資料描述檔 {#copying-a-metadata-profile}

1. 從「中 **[!UICONTROL 繼資料描述檔]** 」頁面中，選取中繼資料描述檔以製作其副本。

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. 從工 **[!UICONTROL 具列按一下]** 「複製」。
1. 在「復 **[!UICONTROL 制中繼資料設定檔]** 」對話方塊中，輸入中繼資料設定檔新副本的標題。
1. 按一 **[!UICONTROL 下複製]**。 中繼資料描述檔的復本會顯示在「中繼資料描述檔」頁面的描述檔 **[!UICONTROL 清單中]** 。

   ![在「中繼資料描述檔」頁面中新增的中繼資料描述檔復本](assets/copy-metadata-profile.png)

## 刪除中繼資料設定檔 {#deleting-a-metadata-profile}

1. 從「中繼資 **[!UICONTROL 料描述檔]** 」頁面中，選取要刪除的描述檔。

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. 在工[] 具列中刪除中繼資料設定檔 **** 。
1. 在對話方塊中，按一下「 **[!UICONTROL 刪除]** 」以確認刪除作業。 元資料配置檔案將從清單中刪除。

## 將中繼資料描述檔套用至資料夾 {#applying-a-metadata-profile-to-folders}

將元資料配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承該配置檔案。 這表示您只能將一個中繼資料描述檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的檔案夾結構。

如果您指派不同的中繼資料描述檔給資料夾，新的描述檔會覆寫先前的描述檔。 舊有的資料夾資產仍維持不變。 新的描述檔會套用至稍後新增至資料夾的資產。

在用戶介面中，配置有配置檔案的資料夾將通過卡名稱中顯示的配置檔案名稱來指示。

![chlimage_1-206](assets/chlimage_1-489.png)

您可以將中繼資料設定檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理已有現有中繼資料設定檔的資料夾中的資產，而您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](processing-profiles.md#reprocessing-assets)。

### 將中繼資料描述檔套用至特定的資料夾 {#applying-metadata-profiles-to-specific-folders}

您可以從「工具」菜單或者在資料夾內的「屬性」中，將元資料配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將中繼資料描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](processing-profiles.md#reprocessing-assets)。

#### 從Profiles使用者介面將中繼資料描述檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

請依照下列步驟來套用中繼資料描述檔：

1. Click the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 選擇要應用於資料夾或多個資料夾的元資料配置檔案。

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從屬性將中繼資料描述檔套用至資料夾 {#applying-metadata-profiles-to-folders-from-properties}

1. 在左側導軌中，按一下「 **[!UICONTROL 資產]** 」，然後導覽至您要套用中繼資料描述檔的檔案夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下「屬 **[!UICONTROL 性」]**。

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the drop-down menu and click **[!UICONTROL Save]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

### 全域套用中繼資料設定檔 {#applying-a-metadata-profile-globally}

除了將描述檔套用至檔案夾外，您也可以全域套用一個，如此任何檔案夾中上傳至AEM資產的內容都會套用選取的描述檔。

您可以重新處理已有現有中繼資料設定檔的資料夾中的資產，而您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](processing-profiles.md#reprocessing-assets)。

若要全域套用中繼資料設定檔，請遵循下列步驟：

* 導覽至並 `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` 套用適當的描述檔，然後按一下「 **[!UICONTROL 儲存]**」。

   ![chlimage_1-209](assets/chlimage_1-492.png)

* 在CRXDE Lite中，導覽至下列節點： `/content/dam/jcr:content`. 新增屬性， `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` 然後按一下「 **[!UICONTROL 全部儲存」]**。

   ![chlimage_1-210](assets/chlimage_1-493.png)

## 從資料夾移除中繼資料描述檔 {#removing-a-metadata-profile-from-folders}

從資料夾中刪除元資料配置檔案時，任何子資料夾都會自動繼承從其父資料夾中刪除配置檔案。 不過，對檔案夾中發生的檔案處理仍維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「屬性」中移除中繼資料描述檔，或從「工具 **[!UICONTROL 」功能表]** 移除中繼資料描述檔 ****。本節將說明如何以兩種方式從資料夾中移除中繼資料描述檔。

### 透過描述檔使用者介面，從資料夾移除中繼資料描述檔 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 選擇要從資料夾或多個資料夾中刪除的元資料配置檔案。
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   您可以確認中繼資料描述檔不再套用至資料夾，因為該名稱不會再顯示在資料夾名稱下方。

### 透過屬性從資料夾移除中繼資料描述檔 {#removing-metadata-profiles-from-folders-via-properties}

1. 按一下AEM標誌，並導覽 **[!UICONTROL Assets]** ，然後導覽至您要從中移除中繼資料描述檔的檔案夾。
1. 在資料夾上，按一下複選標籤以選擇它，然後按一下「屬 **[!UICONTROL 性」]**。
1. 選擇「元 **[!UICONTROL 資料描述檔]** 」標籤，然後從下拉式選單中選 **[!UICONTROL 擇「無]** 」，然後按一下「 **[!UICONTROL 儲存]**」。已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

## 限制與最佳實務 {#limitations-best-practices-tips}

* 升級至 [!DNL Experience Manager] 6.5之前，您可能已有預先存在的中繼資料設定檔。 升級後，如果您在「中繼資料設定檔」索引標籤的 [!UICONTROL 資料夾] 「屬  性」中套用此類設定檔，則不會顯示中繼資料表格欄位。 不過，如果您套用新建立的中繼資料描述檔，表單欄位會顯示，但無法如預期般使用。 功能不會遺失，但如果您想查看（無法使用）表單欄位，請編輯並儲存現有的中繼資料設定檔。

>[!MORELIKETHIS]
>
>* [處理中繼資料、影像和視訊的設定檔](processing-profiles.md)
>* [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md)

