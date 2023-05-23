---
title: 元資料架構定義元資料屬性頁的佈局
description: 元資料架構定義屬性頁的佈局和為資產顯示的元資料屬性。 瞭解如何建立自定義元資料架構、編輯元資料架構以及如何將元資料架構應用於資產。
contentOwner: AG
mini-toc-levels: 1
role: User,Admin
feature: Metadata
exl-id: 0dd322cd-ce97-4335-825d-71f72a5e438c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 8%

---

# 中繼資料結構描述 {#metadata-schemas}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-schemas.html?lang=en) |
| AEM 6.5 | 本文 |

組織提出了一種元資料模型，可增強資產發現、使用、互操作性等。 正確的元資料應用程式是維護元資料驅動的工作流和進程的神聖不可侵犯的。 要遵守組織範圍的元資料策略和標準，可以使用元資料架構來幫助DAM用戶協調。 [!DNL Adobe Experience Manager] 允許建立、維護和應用元資料架構的簡單而靈活的方法。

在 [!DNL Adobe Experience Manager Assets]，架構包含要填寫的特定資訊的特定欄位。 它還包含佈局資訊，以用戶友好的方式顯示元資料欄位。 元資料屬性包括標題、說明、MIME類型、標籤等。 您可以使用 [!UICONTROL 元資料架構Forms] 編輯器以修改現有架構或添加自定義元資料架構。

要查看和編輯資產的屬性頁，請執行以下步驟：

1. 按一下 **[!UICONTROL 查看屬性]** 選項。 或者，選擇一個資產，然後按一下 **[!UICONTROL 屬性]** ![查看屬性](assets/do-not-localize/info-circle-icon.png) 的子菜單。

1. 可以編輯可用頁籤下的各種可編輯元資料屬性。 但是，您不能修改資產 [!UICONTROL 類型] 的 [!UICONTROL 基本] 頁籤。

   ![資產屬性的基本標籤，其中不能更改資產類型](assets/asset-properties-basic-tab.png)

   *圖：資產的「基本」頁籤 [!UICONTROL 屬性]。*

   在建立或編輯元資料架構時，請確保只將一個屬性映射到欄位。

   要修改資產的MIME類型，請使用自定義元資料架構表單或修改現有表單。 請參閱 [編輯元資料架構Forms](#edit-metadata-schema-forms) 的子菜單。 如果修改MIME類型的元資料架構，則會修改資產和所有子類型的屬性頁佈局。 例如，修改jpeg架構 `default/image` 僅修改MIME類型資產的元資料佈局（資產屬性） `image/jpeg`。 但是，如果編輯預設架構，則所做的更改將修改所有類型資產的元資料佈局。

## 元資料架構表單 {#default-metadata-schema-forms}

要查看表單或模板清單，請在 [!DNL Experience Manager] 介面導航 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。

[!DNL Experience Manager] 提供了以下元資料架構表單模板。

| 範本 |  | 說明 |
|---|---|---|
| [!UICONTROL 預設] |  | 資產的基元資料架構窗體。 |
|  | 以下子窗體繼承 [!UICONTROL 預設] 表格： |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media視頻的架構窗體。 |
|  | <ul><li>[!UICONTROL 影像]</li></ul> | 具有MIME類型的映像的架構窗體，如 `image/jpeg` 和 `image/png`。 <br> 的 [!UICONTROL 影像] 表單具有以下子表單模板： <ul><li> [!UICONTROL jpeg]:子類型資產的架構窗體 [!UICONTROL jpeg]。</li> <li>[!UICONTROL 原告]:具有子類型TIFF的資產的架構窗體。</li></ul> |
|  | <ul><li>[!UICONTROL 應用]</li></ul> | 具有MIME類型的資產的架構表單，如 `application/pdf` 和 `application/zip`。 <br>[!UICONTROL pdf]:具有子類型PDF的資產的架構窗體。 |
|  | <ul><li>[!UICONTROL 視訊]</li></ul> | MIME類型的視頻資產的架構表單，如 `video/avi` 和 `video/mp4`。 |
| [!UICONTROL 集合] |  | 集合的架構窗體。 |
| [!UICONTROL 內容片段] |  | [內容片段的架構窗體](/help/sites-developing/customizing-content-fragments.md)。 |
| [!UICONTROL 表] |  | 此架構窗體與 [Adobe Experience Manager Forms](/help/forms/home.md)。 |
| [!UICONTROL ugc_contentfragment] |  | 用於用戶生成的內容片段和資產的模式表單，這些內容和資產整合到從社交媒體Experience Manager中。 |

>[!NOTE]
>
>要查看架構表單的子窗體，請按一下架構表單名稱。

## 添加元資料架構窗體 {#add-a-metadata-schema-form}

要添加元資料架構表單，請執行以下步驟：

1. 要將自定義模板添加到清單，請按一下 **[!UICONTROL 建立]** 的子菜單。

   >[!NOTE]
   >
   >鎖定符號隨未編輯的模板一起顯示。 如果自定義模板，則不會鎖定 ![鎖定](assets/do-not-localize/lock_closed_icon.svg)。

1. 在對話框中，提供架構表單的標題，然後按一下 **[!UICONTROL 建立]** 的子菜單。

## 編輯元資料架構表單 {#edit-metadata-schema-forms}

可以編輯新添加的或現有的元資料架構表單。 元資料架構表單包含頁籤和制表符內的表單項。 您可以將這些表單項映射到/配置到CRX儲存庫的元資料節點中的欄位。 可以將頁籤或表單項添加到元資料架構表單中。 從父級派生的制表符和表單項處於鎖定狀態。 不能在子級更改它們。

1. 在 [!UICONTROL 元資料架構Forms] 的子菜單。 **[!UICONTROL 編輯]** 的子菜單。

1. 在 **[!UICONTROL 元資料架構窗體編輯器]** 的子菜單。 從 **[!UICONTROL 生成窗體]** 的子菜單。

1. 要配置元件，請選擇它並在 **[!UICONTROL 設定]** 頁籤。

### 元件 [!UICONTROL 生成窗體] 頁籤 {#components-within-the-build-form-tab}

的 **[!UICONTROL 生成窗體]** 頁籤列出在架構窗體中使用的窗體項。 的 **[!UICONTROL 設定]** 頁籤提供您在 **[!UICONTROL 生成窗體]** 頁籤。 下表列出了 **[!UICONTROL 生成窗體]** 頁籤：

| 元件名稱 | 說明 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 為公用元件清單添加節標題。 |
| [!UICONTROL 單行文字] | 添加單行文本屬性。 它儲存為字串。 |
| [!UICONTROL 多值文字] | 添加多值文本屬性。 它儲存為字串陣列。 |
| [!UICONTROL 數字] | 添加數字元件。 |
| [!UICONTROL 日期] | 添加日期元件。 |
| [!UICONTROL 下拉式] | 添加下拉清單。 |
| [!UICONTROL 標準標記] | 新增標記. |
| [!UICONTROL 智慧標記] | 通過自動添加元資料標籤添加以增強搜索功能。 |
| [!UICONTROL 隱藏欄位] | 添加隱藏欄位。 保存資產時，它將作為POST參數發送。 |
| [!UICONTROL 資產引用者] | 添加此元件以查看資產引用的資產清單。 |
| [!UICONTROL 資產引用] | 添加以顯示引用資產的資產清單。 |
| [!UICONTROL 產品參考] | 添加以顯示與資產連結的產品清單。 |
| [!UICONTROL 資產評等] | 添加以顯示資產評級選項。 |
| [!UICONTROL 關聯式中繼資料] | 添加以控制資產屬性頁中其他元資料頁籤的顯示。 |

#### 編輯元資料元件 {#edit-the-metadata-component}

要編輯表單上元資料元件的屬性，請按一下該元件以編輯表單中以下屬性的全部或子集 **[!UICONTROL 設定]** 頁籤。 建議只將一個欄位映射到元資料架構中的給定屬性。 否則，系統將選取映射到該屬性的最新添加欄位。

**欄位標籤**:顯示在資產屬性頁上的元資料屬性的名稱。

**映射到屬性**:此屬性指定保存在CRX儲存庫中的資產節點的相對路徑或名稱。 開始於 `./` 以指示路徑位於資產的節點下。

以下是屬性有效值的示例：

* `./jcr:content/metadata/dc:title`:將值儲存在資產的中繼資料節點，做為屬性 `dc:title`。

* `./jcr:created`:儲存資產的建立日期和時間。 它是受保護的屬性。 如果配置這些屬性，Adobe建議將其標籤為「禁用編輯」。 否則，當您儲存資產的屬性時，會出現「資產無法修改」錯誤。

為了確保元件在元資料架構表單中正確顯示，屬性路徑不應包含任何空格。

* **佔位符**:使用此屬性可指定與元資料屬性相關的佔位符文本。
* **必需**:使用此屬性可在屬性頁上將元資料屬性標籤為必需屬性。
* **禁用編輯**:使用此屬性可禁止對屬性頁面上的屬性進行任何編輯。
* **以只讀方式顯示空欄位**:將此屬性標籤為在屬性頁上顯示元資料屬性，即使它沒有值。 預設情況下，當元資料屬性沒有值時，該屬性不會列在屬性頁上。
* **按順序顯示清單**:使用此屬性可顯示有序的選項清單。
* **選擇**:使用此屬性可指定清單中的選項。
* **說明** :使用此屬性可為元資料元件添加簡短說明。
* **類**:屬性與關聯的對象類。
* **刪除**:按一下 [!UICONTROL 刪除] 從架構窗體中刪除元件。

>[!NOTE]
>
>的 [!UICONTROL 隱藏欄位] 元件不包括這些屬性。 而是包括屬性，如屬性名稱、值、欄位標籤和說明。 每次保存資產時，「隱藏欄位」元件的值都作為POST參數發送。 它不會保存為資產的元資料。

如果您選取「必 **[!UICONTROL 要]** 」選項，可以搜尋遺失必要中繼資料的資產。從「篩 **[!UICONTROL 選器]** 」面板中，展開「中繼資料 **[!UICONTROL 驗證謂語]** 」並選取「 **[!UICONTROL 無效]** 」選項。搜尋結果會顯示遺失您透過結構表單設定之必要中繼資料的資產。

![在「篩選器」面板的元資料驗證謂語中選擇的選項](assets/invalid-metadata-predicate.png)

如果將上下文元資料元件添加到任何架構表單的任何頁籤，則該元件將作為清單出現在應用特定架構的資產的屬性頁中。 該清單包括除您應用上下文元資料元件的頁籤之外的所有其它頁籤。 當前，此功能提供了基本功能，用於根據上下文控制元資料的顯示。

![上下文元資料元件清單資產屬性頁籤](assets/metadata-contextual-component-list.png)

要在屬性頁中顯示除應用上下文元資料元件的頁籤之外的任何頁籤，請從清單中選擇該頁籤。 該頁籤將添加到屬性頁。

![上下文元資料清單上選擇的頁籤顯示在資產屬性頁上](assets/contextual-metadata-asset-properties.png)

*圖：資產屬性頁中的上下文元資料。*

### 在JSON檔案中指定屬性 {#specify-properties-in-json-file}

您不必在「設定」標籤中指定選項的屬 **[!UICONTROL 性]** ，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。在「 **[!UICONTROL JSON路徑」欄位中指定JSON檔案的]** 路徑。

#### 在架構表單中添加或刪除頁籤 {#adding-deleting-a-tab-in-the-schema-form}

架構編輯器可讓您新增或刪除標籤。預設架構窗體包括 **[!UICONTROL 基本]**。 **[!UICONTROL 高級]** 。 **[!UICONTROL IPTC]**, **[!UICONTROL IPTC擴展]** 頁籤。

按一下 `+` 在架構窗體上添加頁籤。 預設情況下，新頁籤具有 `Unnamed-1`。 可以從 **[!UICONTROL 設定]** 頁籤。 按一下 `X` 按鈕

![使用元資料架構編輯器添加或刪除頁籤](assets/metadata-schema-form-new-tab.png)

## 階層式中繼資料 {#cascading-metadata}

當捕獲資產的元資料資訊時，用戶在各種可用欄位中提供資訊。 您可以顯示特定元資料欄位或欄位值，這些欄位值取決於在其它欄位中選擇的選項。 這種元資料的條件顯示稱為級聯元資料。 換句話說，您可以在特定元資料欄位/值和一個或多個欄位和/或其值之間建立依賴關係。

使用元資料架構定義用於顯示級聯元資料的規則。 例如，如果元資料方案包括資產類型欄位，則可以根據用戶選擇的資產類型定義要顯示的相關欄位集。

>[!CAUTION]
>
>內容片段不支援級聯元資料。

以下是一些可以定義級聯元資料的使用案例：

* 如果需要用戶位置，則根據用戶對國家和州的選擇顯示相關城市名稱。
* 根據用戶對產品類別的選擇，將相關品牌名稱載入到清單中。
* 根據在另一個欄位中指定的值切換特定欄位的可見性。 例如，如果用戶希望以不同地址交付發運，則顯示單獨的發運地址欄位。
* 根據在另一個欄位中指定的值將欄位指定為必需欄位。
* 根據在另一個欄位中指定的值更改特定欄位顯示的選項。
* 根據在另一個欄位中指定的值，在特定欄位中設定預設元資料值。

### 在中配置級聯元資料 [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

考慮要根據所選資產類型顯示級聯元資料的方案。 一些示例

* 對於視頻，顯示適用的欄位，如格式、編解碼器、持續時間等。
* 對於Word或PDF文檔，顯示欄位，如頁數、作者等。

無論選擇的資產類型如何，都將版權資訊顯示為必填欄位。

1. 在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。
1. 在 **[!UICONTROL 架構Forms]** 頁，選擇架構表單，然後按一下 **[!UICONTROL 編輯]** 的子菜單。

   ![選擇窗體](assets/select_form.png)

1. （可選）在元資料架構編輯器中，建立要條件化的新欄位。 在中指定名稱和屬性路徑 **[!UICONTROL 設定]** 頁籤。

   要建立新頁籤，請按一下 `+` 添加頁籤，然後添加元資料欄位。

   ![添加頁籤](assets/add_tab.png)

1. 為資產類型添加下拉欄位。 在中指定名稱和屬性路徑 **[!UICONTROL 設定]** 頁籤。 添加可選說明。

   ![asset_type_field](assets/asset_type_field.png)

1. 鍵值對是提供給表單用戶的選項。 您可以手動或從JSON檔案提供鍵值對。

   * 要手動指定值，請選擇 **[!UICONTROL 手動添加]**，然後按一下 **[!UICONTROL 添加選項]** 並指定選項文本和值。 例如，指定「視頻」、「PDF」、「Word」和「影像」資產類型。

   * 要動態從JSON檔案中提取值，請選擇 **[!UICONTROL 通過JSON路徑添加]** 並提供JSON檔案的路徑。 [!DNL Experience Manager] 在向用戶顯示表單時即時讀取鍵值對。

   兩個選項互斥。 無法從JSON檔案導入選項並手動編輯。

   ![添加選項](assets/add_choice.png)

   >[!NOTE]
   >
   >添加JSON檔案時，鍵值對不會顯示在元資料架構編輯器中，但在發佈的表單中可用。

   >[!NOTE]
   >
   >添加選項時，如果按一下「下拉」欄位，則介面會失真，並且選項的刪除選項將停止工作。 保存更改之前，請勿按滑鼠下拉清單。 如果遇到此問題，請保存架構並再次開啟以繼續編輯。

1. （可選）添加其他必填欄位。 例如，資產類型視頻的格式、編解碼器和持續時間。

   同樣，為其他資產類型添加從屬欄位。 例如，為文檔資產(如PDF和Word檔案)添加欄位頁數和作者。

   ![視頻_dependent_fields](assets/video_dependent_fields.png)

1. 要在資產類型欄位和其它欄位之間建立相關性，請選擇相關欄位並開啟 **[!UICONTROL 規則]** 頁籤。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 下 **[!UICONTROL 要求]**&#x200B;的子菜單。 **[!UICONTROL 必需，基於新規則]** 的雙曲餘切值。
1. 按一下 **[!UICONTROL 添加規則]** 選擇 **[!UICONTROL 資產類型]** 的子菜單。 也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。按一下「**[!UICONTROL 完成]**」以儲存變更。

   ![定義規則](assets/define_rule.png)

   >[!NOTE]
   >
   >帶有手動預定義值的下拉清單可與規則一起使用。 配置了JSON路徑的下拉菜單不能與使用預定義值應用條件的規則一起使用。 如果在運行時從JSON載入值，則不能應用預定義規則。

1. 在「可 **[!UICONTROL 見性]**」下，選擇「可 **[!UICONTROL 見」，根據新規則選項]** 。

1. 按一下 **[!UICONTROL 添加規則]** 選擇 **[!UICONTROL 資產類型]** 的子菜單。 也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。按一下「**[!UICONTROL 完成]**」以儲存變更。

   ![define_visibility規則](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >按一下空白（或值以外的任何位置）將重置值。 如果發生這種情況，請重新選擇值。

   >[!NOTE]
   >
   >您可以套用 **[!UICONTROL 「需求]** 」條件 **[!UICONTROL 和「可見性]** 」條件，它們彼此獨立。

1. 同樣，在「資產類型」欄位中的值「視頻」和其它欄位（如「編解碼器」和「持續時間」）之間建立相關性。
1. 重複步驟，在中建立文檔資產(PDF和Word)之間的依賴關係 [!UICONTROL 資產類型] 欄位和欄位 [!UICONTROL 頁數] 和 [!UICONTROL 作者]。
1. 按一下「**[!UICONTROL 儲存]**」。將元資料架構應用於資料夾。

1. 導航到應用元資料架構的資料夾並開啟資產的屬性頁。 根據您在「資產類型」欄位中的選擇，將顯示相關的級聯元資料欄位。

   ![視頻資產的級聯元資料](assets/video_asset.png)

   *圖：級聯視頻的元資料。*

   ![為文檔資產級聯元資料](assets/doc_type_fields.png)

   *圖：為文檔級聯元資料。*

## 刪除元資料架構表單 {#delete-metadata-schema-forms}

[!DNL Experience Manager] 允許您僅刪除自定義架構表單。 它不允許您刪除預設架構表單/模板。 但是，您可以刪除這些表單中的任何自定義更改。

要刪除表單，請選擇一個表單並按一下刪除。

>[!NOTE]
>
>* 刪除對預設表單的自定義更改後，鎖 ![鎖定](assets/do-not-localize/lock_closed_icon.svg) 重新出現在窗體之前。 它表示表單已恢復為預設狀態。
>* 無法刪除中的預設元資料架構表單 [!DNL Assets]。


## MIME類型的架構表單 {#schema-forms-for-mime-types}

[!DNL Experience Manager] 為各種MIME類型提供了預設表單。 但是，您可以為各種MIME類型的資產添加自定義表單。

### 為MIME類型添加新表單 {#add-new-forms-for-mime-types}

在相應的窗體類型下建立窗體。 例如，要為 `image/png` 子類型，在「image」窗體下建立窗體。 方案表單的標題是子類型名稱。在本例中，標題是 `png`。

#### 將現有架構模板用於各種MIME類型 {#use-an-existing-schema-template-for-various-mime-types}

您可以將現有模板用於其他MIME類型。 例如，使用 `image/jpeg` MIME類型資產的窗體 `image/png`。

在這種情況下，在 `/etc/dam/metadataeditor/mimetypemappings` 的下界。 指定節點的名稱並定義以下屬性：

| 名稱 | 說明 | 類型 | 值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要映射的現有窗體的名稱 | `String` | `image/jpeg` |
| `mimetypes` | 使用中定義的表單的MIME類型清單 `exposedmimetype` 屬性 | `String` | `image/png` |

[!DNL Assets] 映射以下MIME類型和架構表單：

| 架構窗體 | MIME類型 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | 影像/x-tiff |
| application/pdf | application/postscript |
| 應用程式/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| 應用程式/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | 視頻/x快速時間 |
| 視頻/mpeg4 | video/mp4 |
| 視頻/avi | 視頻/avi、視頻/msvideo、視頻/xmsvideo |
| 視頻/wmv | video/x-ms-wmv |
| 視頻/flv | video/x-flv |

## 授予對元資料架構的訪問權 {#grant-access-to-metadata-schemas}

元資料架構功能僅供管理員使用。 但是，管理員可以通過修改某些權限來提供對非管理員的訪問權限。 提供非管理員用戶對 `/conf` 的子菜單。

## 應用特定於資料夾的元資料 {#apply-folder-specific-metadata}

[!DNL Assets] 用於定義元資料架構的變型並將其應用於特定資料夾。

例如，可以定義預設元資料架構的變型並將其應用於資料夾。 應用修改的架構時，它將覆蓋應用於資料夾內資產的原始預設元資料架構。

只有上載到應用此架構的資料夾的資產才符合變數元資料架構中定義的修改元資料。 [!DNL Assets] 在應用原始架構的其他資料夾中，繼續遵循原始架構中定義的元資料。

按資產列出的元資料繼承基於應用於層次結構中頂層資料夾的架構。 同一架構將應用於子資料夾或由子資料夾繼承。 如果在子資料夾級別應用了其他模式，則繼承將停止。

1. 在 [!DNL Experience Manager] 介面，導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 選中表單前的複選框，然後按一下 **[!UICONTROL 複製]** 並將其保存為自定義窗體。 指定表單的自定義名稱，例如 `my_default`。 或者，可以建立自定義表單。

1. 在 **[!UICONTROL 元資料架構Forms]** ，選擇 `my_default` ，然後按一下 **[!UICONTROL 編輯]**。

1. 在 **[!UICONTROL 元資料架構編輯器]** 的子菜單。 例如，添加帶標籤的欄位 **[!UICONTROL 類別]**。

   ![添加到元資料架構表單編輯器的文本欄位](assets/text-field-metadata-schema-editor.png)

   *圖：文本欄位已添加到元資料架構表單編輯器中。*

1. 按一下「**[!UICONTROL 儲存]**」。已修改的表單列在 **[!UICONTROL 元資料架構Forms]** 的子菜單。
1. 按一下 **[!UICONTROL 應用於資料夾]** 的子菜單。

1. 選擇要應用修改的架構的資料夾，然後按一下 **[!UICONTROL 應用]**。

   ![選擇要應用元資料架構的資料夾](assets/metadata-schema-select-folder.png)

1. 如果資料夾應用了其他元資料架構，則會顯示一條警告消息，指出您將覆蓋現有元資料架構。 按一下 **覆蓋**。
1. 按一下 **確定** 關閉成功消息。
1. 導航到應用已修改元資料架構的資料夾。

## 定義強制元資料 {#define-mandatory-metadata}

您可以在資料夾級別定義強制欄位，該欄位對上載到資料夾的資產強制執行。 如果上載具有先前定義的必需欄位的缺失元資料的資產，則卡視圖中的資產上會顯示缺失元資料的直觀指示。

>[!NOTE]
>
>元資料欄位可以基於另一個欄位的值被定義為強制欄位。 在卡片視圖中， [!DNL Experience Manager] 不顯示有關此類強制元資料欄位缺少元資料的警告消息。

1. 在 [!DNL Experience Manager] 介面，導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 將預設元資料表單另存為自定義表單。 例如，將其另存為 `my_default`。

1. 編輯自定義窗體。 添加必填欄位。 例如，添加 **[!UICONTROL 類別]** 欄位，並使欄位成為必填項。

   ![通過在元資料架構表單編輯器中選擇規則頁籤中的「必需」頁籤，將必需欄位添加到元資料表單](assets/mandatory-field-metadata-schema-editor.png)

   *圖：元資料架構窗體編輯器中的必需欄位。*

1. 按一下「**[!UICONTROL 儲存]**」。已修改的表單列在 **[!UICONTROL 元資料架構Forms]** 的子菜單。 選擇表單，然後按一下 **[!UICONTROL 應用於資料夾]** 的子菜單。

1. 導航到資料夾並上載一些資產，其中缺少添加到自定義表單的必需欄位的元資料。 在資產的卡視圖上顯示該必需欄位缺少的元資料的消息。

   ![在資料夾中上載資產時，資產卡視圖上缺少必需元資料的消息](assets/metadata-missing-info-card-view.png)

1. （可選）訪問 `https://[aem_server]:[port]/system/console/components/`。 配置和啟用 `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` 預設禁用的元件。 設定頻率 [!DNL Experience Manager] 檢查資產上元資料的有效性。 此配置添加屬性 `hasValidMetadata` 至 `jcr:content` 資產。 [!DNL Experience Manager] 使用此屬性篩選搜索結果中的無效資產。 如果在選中後添加資產，則資產不會標籤為 `hasValidMetadata` 直到下次計畫檢查。 因此，在下次計畫檢查之後，搜索篩選器中不會顯示無效元資料。

   >[!CAUTION]
   >
   >元資料驗證檢查是資源密集型的，可能會影響系統的效能。 相應地安排檢查。 如果伺服器無法處理負載，請嘗試禁用此作業。

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
