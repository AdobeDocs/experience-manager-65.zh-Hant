---
title: 中繼資料結構
description: 中繼資料結構定義屬性頁面的版面配置，以及資產所顯示的中繼資料屬性。 瞭解如何建立自訂中繼資料結構、編輯中繼資料結構，以及如何將中繼資料結構套用至資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Metadata schemas {#metadata-schemas}

在Adobe Experience Manager(AEM)Assets中，中繼資料結構定義屬性頁面的版面配置，以及使用特定結構的資產所顯示的中繼資料屬性。 中繼資料屬性包括標題、說明、MIME類型、標籤等。

您可以使用中繼資料結構表單編輯器來修改現有結構或新增自訂中繼資料結構。

1. 若要檢視資產的屬性頁面，請在「卡片檢視」中按一下或點選資產圖格上的「快速動作」 **[!UICONTROL 的「檢視屬性]** 」圖示。

   ![chlimage_1-34](assets/chlimage_1-170.png)

   或者，在UI中選取資產，然後按一下或點選工具列 **[!UICONTROL 中的]** 「屬性」圖示。

   ![chlimage_1-35](assets/chlimage_1-171.png)

1. 在各種標籤下編輯各種中繼資料屬性。 但是，您無法修改屬性頁面中的資產類型。

   ![您不能更改資產屬性的基本標籤中的資產類型](assets/asset-properties-basic-tab.png)

   *圖：資產屬性上的「基本」標籤*


   若要修改資產的MIME類型，請使用自訂中繼資料結構表單或修改現有表單。 如需詳 [細資訊，請參閱編輯中繼資料結構](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) 表單。 如果您修改特定MIME類型的中繼資料架構，則會修改目前MIME類型資產和所有資產子類型的屬性頁面配置。 例如，在下修改jpeg架構時， `default/image` 僅會修改MIME類型資產的中繼資料配置（資產屬性） `image/jpeg`。 不過，如果您編輯預設結構，您的變更會修改所有類型資產的中繼資料配置。

1. 若要檢視表單/範本清單，請按一下 AEM 標誌，然後導覽至&#x200B;**[!UICONTROL 「工具」]**>**[!UICONTROL 「資產」]**>**[!UICONTROL 「中繼資料結構描述」]**。

   ![chlimage_1-37](assets/chlimage_1-173.png)

   AEM提供現成可用的下列範本：
   * **預設**:資產的基本中繼資料結構表單。

      以下子表單繼承預設表單的屬性：

      1. **影像**:MIME類型為&quot;image&quot;的資產的架構表單， `image/jpeg`例如 `image/png`、等。

         「影像」表單包含下列子表單範本：
         * **jpeg**:子類型資產的結構表單 `jpeg`。
         * **tiff**:子類型資產的結構表單 `tiff`。
      1. **應用程式**:具有MIME類型的資產的 `application`架構表單， `application/pdf``application/zip`例如，等等。
         * **pdf**:子類型資產的結構表單 `pdf`。
      1. **視訊**:具有MIME類型的資產的 `video`架構表單， `video/avi`如 `video/mp4`、等等。
   * **系列**:系列的結構表單。
   * **contentfragment:** 內容片段的架構表單。
   * **表單**:此結構表單與 [Adobe Experience Manager Forms相關](/help/forms/home.md)。

>[!NOTE]
>
>要查看方案表單的子表單，請按一下／點選方案表單名稱。

## 新增中繼資料結構表單 {#add-a-metadata-schema-form}

1. 若要將自訂範本新增至清單，請按一下工 **[!UICONTROL 具列中的]** 「建立」。

   >[!NOTE]
   >
   >未編輯的範本前面有鎖定圖示。 如果您自訂任何範本，範本消失前的鎖定圖示。

1. 在對話框中，輸入架構表單的標題，然後按一下 **[!UICONTROL 建立]** ，完成表單建立過程。

   ![chlimage_1-38](assets/chlimage_1-174.png)

## 編輯中繼資料結構表單 {#edit-metadata-schema-forms}

您可以編輯新增或現有的中繼資料結構表單。 中繼資料結構表單包含下列項目：

* 索引標籤
* 標籤內的表單項目。

您可以將這些表單項目映射／配置到CRX儲存庫中元資料節點中的欄位。

您可以將新標籤或表單項目新增至中繼資料結構表單。 衍生自父項的制表符和表單項處於鎖定狀態。 您無法在子級更改它們。

1. 在「方案表單」頁中，選中表單前的複選框，然後按一下工 具欄上的 「編輯」表徵圖。

   ![chlimage_1-39](assets/chlimage_1-175.png)

1. 在「元數 **[!UICONTROL 據結構編輯器]** 」頁中，通過將一個或多個元件從「構建表單」頁籤中的元件類型清單拖到「基本」頁籤，自定義資產的屬性頁 ******** 。

   ![將元件從建立表單新增至中繼資料結構編輯器，以自訂資產屬性](assets/metadata-schema-editor.png)


   *圖：中繼資料結構編輯器的基本索引標籤*

1. 要配置元件，請選擇該元件並在「設定」頁籤中修改 **其屬** 性。

### 「生成表單」頁籤中的元件 {#components-within-the-build-form-tab}

「建 **[!UICONTROL 立表單]** 」標籤會列出您在架構表單中使用的表單項目。 「設 **[!UICONTROL 定]** 」標籤提供您在「建置表單」標籤中選取之每 **[!UICONTROL 個項目的屬性]** 。 下表列出了「生成表單」頁籤中可 **[!UICONTROL 用的表單]** 項：

| 元件名稱 | 說明 |
|---|---|
| [!UICONTROL 區段標題] | 新增共用元件清單的區段標題。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它儲存為字串陣列。 |
| [!UICONTROL 數字] | 添加數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式] | 新增下拉式清單。 |
| [!UICONTROL 標準標記] | 新增標記. |
| [!UICONTROL 智慧標記] | 自動新增中繼資料標籤，以增強搜尋功能。 |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST參數傳送。 |
| [!UICONTROL 資產引用者] | 新增此元件以檢視資產參考的資產清單。 |
| [!UICONTROL 資產引用] | 新增以顯示參考資產的資產清單。 |
| [!UICONTROL 產品參考] | 新增以顯示與資產連結的產品清單。 |
| [!UICONTROL 資產評等] | 新增至顯示選項，以評分資產。 |
| [!UICONTROL 關聯式中繼資料] | 新增以控制資產屬性頁面中其他中繼資料標籤的顯示。 |

#### 編輯中繼資料元件 {#edit-the-metadata-component}

要編輯表單上元資料元件的屬性，請按一下該元件，然後在「設定」頁籤中編輯以下所有或子 **[!UICONTROL 集]** 。

**欄位標籤**:顯示在資產屬性頁面上的中繼資料屬性名稱。

**對應至屬性**:此屬性指定資產節點的相對路徑／名稱，該資產節點保存在CRX儲存庫中。 它以開 `./` 頭，因為它表示路徑位於資產的節點下。

以下是此屬性的有效值：

以下是此屬性的有效值：

* `./jcr:content/metadata/dc:title`:將值儲存在資產的中繼資料節點，做為屬性 `dc:title`。

* `./jcr:created`:在資產的節點顯示JCR屬性。 如果您在檢視屬性上設定這些屬性，建議您將它們標示為「停用編輯」，因為這些屬性受到保護。Otherwise, the error [!UICONTROL Asset(s) failed to modify] results when you save the asset&#39;s properties.

為確保元資料架構表單中的元件正確顯示，屬性路徑不應包含任何空格。

**預留位置**:使用此屬性可指定與中繼資料屬性相關的預留位置文字。
**必要**:使用此屬性可將中繼資料屬性標示為屬性頁面上的必要屬性。
**停用編輯**:使用此屬性可讓中繼資料屬性在屬性頁面上無法編輯。
**在唯讀中顯示空白欄位**:標籤此屬性，即使其沒有值，也可在屬性頁面上顯示中繼資料屬性。 預設情況下，當中繼資料屬性沒有值時，該屬性不會列在屬性頁面上。
**顯示順序清單**:使用此屬性可顯示選擇的有序列&#x200B;**表**:使用此屬性可指定清單說明中的&#x200B;**選項** :使用此屬性可為中繼資料元件新增簡短說明。
**類別**:屬性與關聯的對象類。
**刪除**:按一下此表徵圖可從架構表單中刪除元件。

![chlimage_1-41](assets/chlimage_1-177.png)

>[!NOTE]
>
>隱藏欄位元件不包括這些屬性。 而是包含屬性，例如屬性名稱、值、欄位標籤和說明。 每當儲存資產時，「隱藏欄位」元件的值都會以POST參數傳送。 它不會儲存為資產的中繼資料。

如果您選取「必 **[!UICONTROL 要]** 」選項，可以搜尋遺失必要中繼資料的資產。從「篩 **[!UICONTROL 選器]** 」面板中，展開「中繼資料 **[!UICONTROL 驗證謂語]** 」並選取「 **[!UICONTROL 無效]** 」選項。搜尋結果會顯示遺失您透過結構表單設定之必要中繼資料的資產。

![chlimage_1-42](assets/chlimage_1-178.png)

如果將上下文元資料元件添加到任何方案表單的任何頁籤，則該元件將作為清單顯示在應用特定方案的資產的屬性頁中。 該清單包括除應用上下文元資料元件的頁籤之外的所有其他頁籤。 目前，此功能提供基本功能，可根據內容控制中繼資料的顯示。

![chlimage_1-43](assets/chlimage_1-179.png)

要顯示屬性頁面中除了應用上下文元資料元件的頁籤之外的任何頁籤，請從清單中選擇該頁籤。 該頁籤將添加到屬性頁。

![從上下文中繼資料清單中選取標籤，以顯示在屬性頁面上](assets/contextual-metadata-asset-properties.png)

*圖：資產屬性頁面中的內容相關中繼資料*

### 在JSON檔案中指定屬性 {#specify-properties-in-json-file}

您不必在「設定」標籤中指定選項的屬 **[!UICONTROL 性]** ，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。在「 **[!UICONTROL JSON路徑」欄位中指定JSON檔案的]** 路徑。

#### 在架構表單中添加或刪除頁籤 {#adding-deleting-a-tab-in-the-schema-form}

架構編輯器可讓您新增或刪除標籤。預設模式表單包 **[!UICONTROL 括Basic]**、 **[!UICONTROL Advanced]** 、 **[!UICONTROL IPTC]**&#x200B;和 **** IPTC Extension頁籤，預設情況下。

![chlimage_1-45](assets/chlimage_1-181.png)

單 `+` 擊可在架構表單上添加新頁籤。 依預設，新標籤的名稱為 `Unnamed-1`。 您可以從「設定」索引標籤修 **[!UICONTROL 改名稱]** 。

按一 `X` 下以刪除標籤。

![chlimage_1-46](assets/chlimage_1-182.png)

## 刪除中繼資料結構表單 {#delete-metadata-schema-forms}

AEM可讓您僅刪除自訂結構表單。 它不允許您刪除預設模式表單／模板。 不過，您可以刪除這些表單中的任何自訂變更。

要刪除表單，請選擇一個表單並按一下刪除表徵圖。

![chlimage_1-47](assets/chlimage_1-183.png)
<!--![chlimage_1-47](assets/chlimage_1-177.png) -->
>[!NOTE]
>
>刪除對預設表單的自定義更改後，鎖定表徵圖會重新顯示在元資料架構介面的前面，以指示表單恢復為預設狀態。

>[!NOTE]
>
>您無法刪除AEM Assets中立即可用的中繼資料結構表單。

## MIME類型的架構表單 {#schema-forms-for-mime-types}

AEM Assets提供各種MIME類型的預設現成可用表單。 不過，您可以為各種MIME類型的資產新增自訂表格。

### 為MIME類型添加新表單 {#add-new-forms-for-mime-types}

在適當的表單類型下建立新表單。例如，若要新增影像/png子類型 **的新範本** ，請在「影像」表單下建立表單。方案表單的標題是子類型名稱。在本例中，標題為&quot;png.**&quot;**

#### 對各種MIME類型使用現有的架構模板 {#use-an-existing-schema-template-for-various-mime-types}

您可以針對不同的MIME類型使用現有範本。 例如，使用MIME `image/jpeg` 類型資產的表單 `image/png`。

在這種情況下，請在CRX儲存庫中 `/etc/dam/metadataeditor/mimetypemappings` 建立新節點。 指定節點的名稱並定義以下屬性：

| 名稱 | 說明 | 類型 | 值 |
|---|---|---|---|
| `exposedmimetype` | 要映射的現有表單的名稱 | `String` | `image/jpeg` |
| `mimetypes` | 使用屬性中定義的表單的MIME類型列 `exposedmimetype` 表 | `String` | `image/png` |

AEM Assets會對應下列MIME類型和架構表單：

| 架構表單 | MIME類型 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | 視訊/avi，視訊/msvideo，視訊/x-msvideo |
| video/wmv | video/x-ms-wmv |
| 視訊/flv | video/x-flv |

## 授予對中繼資料結構的存取權 {#grant-access-to-metadata-schemas}

「中繼資料結構」功能僅供管理員使用。 不過，管理員可修改某些權限，以提供非管理員的存取權。 非管理員應具有對資料夾的建立、修改和刪除權 `/conf` 限。

## 套用資料夾特定的中繼資料 {#apply-folder-specific-metadata}

AEM Assets可讓您定義中繼資料結構的變體，並將其套用至特定資料夾。

例如，您可以定義預設中繼資料結構的變體，並將其套用至資料夾。 當您套用已修改的架構時，它會覆寫套用至資料夾內資產的原始預設中繼資料架構。

只有上傳至套用此架構的資料夾的資產，才會符合變型中繼資料架構中定義的已修改中繼資料。

套用原始架構的其他資料夾中的資產會持續符合原始架構中定義的中繼資料。

資產的中繼資料繼承是根據套用至階層中第一層資料夾的架構。 換言之，如果資料夾不包含子檔案夾，資料夾內的資產會繼承套用至資料夾之結構的中繼資料。

如果資料夾具有子資料夾，則子資料夾內的資產將繼承子資料夾級別上應用的方案的元資料（如果子資料夾級別應用了不同的方案）。 但是，如果子資料夾級別未應用方案或相同方案，則子資料夾資產將繼承父資料夾級別所應用方案的元資料。

1. 按一下 AEM 標誌，然後導覽至&#x200B;**[!UICONTROL 「工具」]**>**[!UICONTROL 「資產」]**>**[!UICONTROL 「中繼資料結構描述」]**。此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 選取表單前的核取方塊，例如預設中繼資料表單，然後按一下或點選復製圖示，並將它儲存為自訂表單。 例如，指定表單的自訂名稱 `my_default`。 或者，您也可以建立自訂表格。
   ![chlimage_1-184](assets/chlimage_1-184.png)

1. 在「元數 **[!UICONTROL 據結構表單]** 」頁中，選 `my_default` 擇表單，然後按一下 **[!UICONTROL 編輯表徵圖]** 。

   ![chlimage_1-49](assets/chlimage_1-185.png)

1. 在「元數 **[!UICONTROL 據結構編輯器]** 」頁中，將文本欄位添加到結構表單中。 例如，新增標籤為「類別」的 **[!UICONTROL 欄位]**。

   ![將文本欄位添加到元資料架構表單編輯器](assets/text-field-metadata-schema-editor.png)

   *圖：已新增文字欄位至中繼資料結構表單編輯器*

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。已修改的表單列在「元資料結構表 **[!UICONTROL 單」頁中]** 。
1. 按一下／點 **[!UICONTROL 選工具列中的「套用至資料夾」]** ，將自訂中繼資料套用至資料夾。

   ![chlimage_1-51](assets/chlimage_1-187.png)

1. 選擇要在其上應用已修改方案的資料夾，然後按一下／點選「應 **[!UICONTROL 用」]**。

   ![chlimage_1-52](assets/chlimage_1-188.png)

1. 如果資料夾已套用其他中繼資料結構，會出現警告訊息，指出您即將覆寫現有的中繼資料結構。 按一 **下覆寫**。
1. 按一 **下「確定** 」以關閉成功訊息。
1. 導覽至您套用已修改中繼資料結構的資料夾。

## 定義必備中繼資料 {#define-mandatory-metadata}

您可以在資料夾層級定義必要欄位，並強制執行在上傳至資料夾的資產上。 如果您上傳資產時，先前定義之必填欄位的中繼資料遺失，則「卡片」檢視中的資產上會顯示遺失中繼資料的視覺指示。

>[!NOTE]
>
>中繼資料欄位可根據其他欄位的值，定義為必填欄位。 在「卡片」檢視中，AEM不會顯示有關此類強制中繼資料欄位遺失中繼資料的警告訊息。

1. 按一下 AEM 標誌，然後導覽至&#x200B;**[!UICONTROL 「工具」]**>**[!UICONTROL 「資產」]**>**[!UICONTROL 「中繼資料結構描述」]**。此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 將預設中繼資料表單儲存為自訂表單。 例如，將它另存為 `my_default`。

   ![chlimage_1-53](assets/chlimage_1-189.png)

1. 編輯自訂表格。 新增必填欄位。 例如，新增「類 **[!UICONTROL 別」欄位]** ，並將欄位設為必填。

   ![將欄位新增至中繼資料表單，並選取「規則」索引標籤中的「必要」，將它設為強制](assets/mandatory-field-metadata-schema-editor.png)

   *圖：中繼資料結構表單編輯器中的必填欄位*

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。已修改的表單列在「元資料結構表 **[!UICONTROL 單」頁中]** 。 選取表單，然後按一下或點選 **[!UICONTROL 工具列中的「套用至資料夾」]** ，將自訂中繼資料套用至資料夾。

   ![chlimage_1-55](assets/chlimage_1-191.png)

1. 導覽至資料夾，並上傳您新增至自訂表單之必填欄位中遺失中繼資料的部分資產。 資產的「卡片」檢視中會顯示必要欄位遺失中繼資料的訊息。

   ![chlimage_1-56](assets/chlimage_1-192.png)

1. （可選）存取 `https://[server]:[port]/system/console/components/`。 配置並啟 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 用預設禁用的元件。 設定AEM檢查資產中中繼資料有效性的頻率。

   此設定會將屬性新 `hasValidMetadata` 增至 `jcr:content` 資產。 AEM可使用此屬性來篩選搜尋結果。

   >[!NOTE]
   >
   >如果在排程檢查後新增資產，則資產在下次排程檢查前 `hasValidMetadata` 不會加上標籤。 資產不會出現在中間搜尋結果中。

   >[!CAUTION]
   >
   >中繼資料驗證檢查需要耗費大量資源，而且可能會影響您系統的效能。 相應地安排檢查。 如果伺服器無法處理負載，請嘗試禁用此作業。
