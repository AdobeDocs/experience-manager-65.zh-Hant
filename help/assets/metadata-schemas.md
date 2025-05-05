---
title: 中繼資料結構描述會定義中繼資料屬性頁面的配置
description: 中繼資料結構會定義屬性頁面的配置，以及為資產顯示的中繼資料屬性。 瞭解如何建立自訂中繼資料結構、編輯中繼資料結構，以及如何將中繼資料結構套用至資產。
contentOwner: AG
mini-toc-levels: 1
role: User,Admin
feature: Metadata
exl-id: 0dd322cd-ce97-4335-825d-71f72a5e438c
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3595'
ht-degree: 8%

---

# 中繼資料結構描述 {#metadata-schemas}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-schemas.html?lang=en) |
| AEM 6.5 | 本文章 |

組織會提出中繼資料模型，藉以強化資產探索、使用、互通性等。 正確的中繼資料應用程式對於維護中繼資料驅動的工作流程和流程至關重要。 若要遵循組織範圍的中繼資料策略和標準，您可以使用可協助DAM使用者調整的中繼資料結構。 [!DNL Adobe Experience Manager]可讓您以簡單靈活的方法建立、維護和套用中繼資料結構。

在[!DNL Adobe Experience Manager Assets]中，結構描述包含要填入之特定資訊的特定欄位。 它也包含版面資訊，以便以方便使用的方式顯示中繼資料欄位。 中繼資料屬性包括標題、說明、MIME型別、標籤等。 您可以使用[!UICONTROL 中繼資料結構Forms]編輯器來修改現有結構描述或新增自訂中繼資料結構。

若要檢視及編輯資產的屬性頁面，請遵循下列步驟：

1. 從卡片檢視中資產圖磚上的快速動作，按一下&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;選項。 或者，選取資產，然後從工具列按一下&#x200B;**[!UICONTROL 屬性]** ![檢視屬性](assets/do-not-localize/info-circle-icon.png)。

1. 您可以在可用的標籤下編輯各種可編輯的中繼資料屬性。 不過，您無法在屬性頁面的[!UICONTROL 基本]索引標籤中修改資產[!UICONTROL 型別]。

   ![資產屬性的基本索引標籤，無法變更資產型別](assets/asset-properties-basic-tab.png)

   *圖：資產[!UICONTROL 屬性]上的基本索引標籤。*

   在建立或編輯中繼資料結構時，請確定只有一個屬性對應至欄位。

   若要修改資產的MIME型別，請使用自訂中繼資料結構表單或修改現有表單。 如需詳細資訊，請參閱[編輯中繼資料結構描述Forms](#edit-metadata-schema-forms)。 如果您修改MIME型別的中繼資料結構，資產和所有子型別的屬性頁面配置都會被修改。 例如，修改`default/image`下的jpeg結構描述只會修改MIME型別為`image/jpeg`之資產的中繼資料配置（資產屬性）。 不過，如果您編輯預設架構，您所做的變更會修改所有資產型別的中繼資料配置。

## 中繼資料結構表單 {#default-metadata-schema-forms}

若要檢視表單或範本清單，請在[!DNL Experience Manager]介面中導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。

[!DNL Experience Manager]提供下列中繼資料結構表單範本。

| 範本 | | 說明 |
|---|---|---|
| [!UICONTROL 預設] | | 資產的基本中繼資料結構表單。 |
| | 下列子表單繼承[!UICONTROL 預設]表單的屬性： | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Dynamic Media影片的結構描述表單。 |
| | <ul><li>[!UICONTROL 影像]</li></ul> | 具有MIME型別（例如`image/jpeg`和`image/png`）之影像的結構描述表單。 <br> [!UICONTROL 影像]表單有下列子表單範本： <ul><li> [!UICONTROL jpeg]：子型別為[!UICONTROL jpeg]之資產的結構描述表單。</li> <li>[!UICONTROL tiff]：具有子型別TIFF之資產的結構描述表單。</li></ul> |
| | <ul><li>[!UICONTROL 應用程式]</li></ul> | 具有MIME型別（例如`application/pdf`和`application/zip`）之資產的結構描述表單。 <br>[!UICONTROL pdf]：具有子型別PDF之資產的結構描述表單。 |
| | <ul><li>[!UICONTROL 影片]</li></ul> | 具有MIME型別（例如`video/avi`和`video/mp4`）之視訊資產的結構描述表單。 |
| [!UICONTROL 集合] | | 集合的結構表單。 |
| [!UICONTROL contentfragment] | | [內容片段的結構描述表單](/help/sites-developing/customizing-content-fragments.md)。 |
| [!UICONTROL 表單] | | 此結構描述表單與[Adobe Experience Manager Forms](/help/forms/using/introduction-aem-forms.md)有關。 |
| [!UICONTROL ugc_contentfragment] | | 使用者產生的內容片段和資產的結構描述表單，可從社群媒體整合至Experience Manager。 |

>[!NOTE]
>
>若要檢視方案表單的子表單，請按一下方案表單名稱。

## 新增中繼資料結構表單 {#add-a-metadata-schema-form}

若要新增中繼資料結構表單，請執行下列步驟：

1. 若要新增自訂範本至清單，請按一下工具列中的[建立]。**&#x200B;**

   >[!NOTE]
   >
   >鎖定符號會與未編輯的範本一起顯示。 如果您自訂範本，則範本未鎖定![鎖定關閉](assets/do-not-localize/lock_closed_icon.svg)。

1. 在對話方塊中，提供結構表單的標題，然後按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以完成表單建立程式。

## 編輯中繼資料結構表單 {#edit-metadata-schema-forms}

您可以編輯新新增或現有的中繼資料結構表單。 中繼資料結構表單包含索引標籤以及索引標籤內的表單專案。 您可以將這些表單專案對應/設定至CRX存放庫中繼資料節點內的欄位。 您可以將索引標籤或表單專案新增到中繼資料結構表單。 從父項衍生的標籤和表單專案處於鎖定狀態。 您無法在子層級變更它們。

1. 在[!UICONTROL 中繼資料結構Forms]頁面上，選取表單並按一下工具列中的&#x200B;**[!UICONTROL 編輯]**。

1. 在&#x200B;**[!UICONTROL 中繼資料結構表單編輯器]**&#x200B;頁面上，自訂中繼資料表單。 從&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤將所需的元件拖曳到其中一個索引標籤。

1. 若要設定元件，請選取該元件，並在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中修改其屬性。

### [!UICONTROL 建置表單]標籤中的元件 {#components-within-the-build-form-tab}

**[!UICONTROL 建置表單]**&#x200B;索引標籤會列出您在結構描述表單中使用的表單專案。 **[!UICONTROL 設定]**&#x200B;索引標籤提供您在&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中選取之每個專案的屬性。 下表列出&#x200B;**[!UICONTROL 建置表單]**&#x200B;索引標籤中可用的表單專案：

| 元件名稱 | 說明 |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL 區段標題] | 新增區段標題以取得常用元件清單。 |
| [!UICONTROL 單行文字] | 新增單行文字屬性。 它會儲存為字串。 |
| [!UICONTROL 多值文字] | 新增多值文字屬性。 它會儲存為字串陣列。 |
| [!UICONTROL 數字] | 新增數字元件。 |
| [!UICONTROL 日期] | 新增日期元件。 |
| [!UICONTROL 下拉式清單] | 新增下拉式清單。 |
| [!UICONTROL 標準標籤] | 新增標籤。 |
| [!UICONTROL 智慧標記] | 透過自動新增中繼資料標記增強搜尋功能。 |
| [!UICONTROL 隱藏欄位] | 新增隱藏欄位。 儲存資產時，會以POST引數的形式傳送。 |
| [!UICONTROL 資產參考者] | 新增此元件以檢視資產所參考的資產清單。 |
| [!UICONTROL 資產引用] | 新增以顯示參照資產的資產清單。 |
| [!UICONTROL 產品參考] | 新增以顯示與資產連結的產品清單。 |
| [!UICONTROL 資產評等] | 新增以顯示資產評等選項。 |
| [!UICONTROL 內容中繼資料] | 新增以控制其他中繼資料索引標籤在資產屬性頁面中的顯示。 |

#### 編輯中繼資料元件 {#edit-the-metadata-component}

若要編輯表單上中繼資料元件的屬性，請按一下該元件，以在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中編輯下列所有屬性或屬性子集。 建議僅將一個欄位對應到中繼資料結構描述中的指定屬性。 否則，系統會挑選對應至屬性的最新新增欄位。

**欄位標籤**：在資產的屬性頁面上顯示的中繼資料屬性名稱。

**對應至屬性**：此屬性會指定資產節點的相對路徑或名稱，此資產節點會儲存在CRX存放庫中。 它以`./`開頭，表示路徑在資產的節點下。

以下是屬性的有效值範例：

* `./jcr:content/metadata/dc:title`:將值儲存在資產的中繼資料節點，做為屬性 `dc:title`。

* `./jcr:created`：儲存資產的建立日期和時間。 這是受保護的屬性。 如果您設定這些屬性，Adobe建議您將其標示為「停用編輯」。 否則，當您儲存資產的屬性時，會出現「資產無法修改」錯誤。

為確保元件在中繼資料結構表單中正確顯示，屬性路徑不應包含任何空格。

* **預留位置**：使用此屬性來指定與中繼資料屬性相關的預留位置文字。
* **必要**：使用此屬性，在屬性頁面上將中繼資料屬性標示為必要。
* **停用編輯**：使用此屬性可禁止對屬性頁面上的屬性進行任何編輯。
* **以唯讀方式顯示空白欄位**：標示此屬性，以在屬性頁面上顯示中繼資料屬性（即使它沒有值）。 根據預設，當中繼資料屬性沒有值時，它不會列在屬性頁面上。
* **顯示排序清單**：使用此屬性顯示排序的選項清單。
* **選擇**：使用此屬性指定清單中的選擇。
* **描述** ：使用此屬性為中繼資料元件新增簡短描述。
* **類別**：與屬性關聯的物件類別。
* **刪除**：按一下[!UICONTROL 刪除]，從結構表單中刪除元件。

>[!NOTE]
>
>[!UICONTROL 隱藏欄位]元件不包含這些屬性。 而是包含屬性，例如「名稱」、「值」、「欄位標籤」和「說明」。 每當儲存資產時，「隱藏欄位」元件的值都會以POST引數的形式傳送。 它不會儲存為資產的中繼資料。

如果您選取「必 **[!UICONTROL 要]** 」選項，可以搜尋遺失必要中繼資料的資產。從「篩 **[!UICONTROL 選器]** 」面板中，展開「中繼資料 **[!UICONTROL 驗證謂語]** 」並選取「 **[!UICONTROL 無效]** 」選項。搜尋結果會顯示遺失您透過結構表單設定之必要中繼資料的資產。

在篩選器面板的中繼資料驗證述詞中選取![選項](assets/invalid-metadata-predicate.png)

如果您將「關聯式中繼資料」元件新增至任何結構描述表單的任何索引標籤中，該元件會在套用特定結構描述的資產屬性頁面中顯示為清單。 此清單包含所有其他標籤，除了您套用內容中繼資料元件的標籤以外。 目前，此功能提供基本功能，可根據內容控制中繼資料的顯示。

![內容中繼資料元件列出資產屬性的索引標籤](assets/metadata-contextual-component-list.png)

除了顯示套用內容中繼資料元件的索引標籤之外，若要在屬性頁面中顯示任何索引標籤，請從清單中選取索引標籤。 標籤會新增至屬性頁面。

![在內容中繼資料清單上選取的索引標籤會顯示在資產屬性頁面](assets/contextual-metadata-asset-properties.png)上

*圖：資產屬性頁面中的內容中繼資料。*

### 指定JSON檔案中的屬性 {#specify-properties-in-json-file}

您不必在「設定」標籤中指定選項的屬 **[!UICONTROL 性]** ，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。在「 **[!UICONTROL JSON路徑」欄位中指定JSON檔案的]** 路徑。

#### 在結構表單中新增或刪除索引標籤 {#adding-deleting-a-tab-in-the-schema-form}

架構編輯器可讓您新增或刪除標籤。預設結構描述表單包含&#x200B;**[!UICONTROL Basic]**、**[!UICONTROL Advanced]**、**[!UICONTROL IPTC]**&#x200B;和&#x200B;**[!UICONTROL IPTC延伸]**&#x200B;標籤。

按一下`+`在結構表單上新增索引標籤。 依預設，新索引標籤的名稱為`Unnamed-1`。 您可以從&#x200B;**[!UICONTROL 設定]**&#x200B;標籤修改名稱。 按一下`X`以刪除索引標籤。

![使用中繼資料結構編輯器新增或刪除索引標籤](assets/metadata-schema-form-new-tab.png)

## 階層式中繼資料 {#cascading-metadata}

擷取資產的中繼資料資訊時，使用者會在各種可用欄位中提供資訊。 您可以根據在其他欄位中選取的選項，顯示特定的中繼資料欄位或欄位值。 這類條件式顯示中繼資料稱為階層式中繼資料。 換言之，您可以在特定中繼資料欄位/值與一或多個欄位及/或其值之間建立相依性。

使用中繼資料結構描述來定義顯示階層式中繼資料的規則。 例如，如果您的中繼資料結構描述包含資產型別欄位，您可以根據使用者選取的資產型別定義要顯示的相關欄位集。

>[!CAUTION]
>
>內容片段不支援階層式中繼資料。

以下是您可以定義階層式中繼資料的一些使用案例：

* 需要使用者位置時，根據使用者對國家/地區和州的選擇顯示相關城市名稱。
* 根據使用者選擇的產品類別，在清單中載入相關品牌名稱。
* 根據在另一個欄位中指定的值切換特定欄位的可見度。 例如，如果使用者希望以不同的地址運送出貨，則顯示個別的出貨位址列位。
* 根據在其他欄位中指定的值，將欄位指定為必填欄位。
* 根據在其他欄位中指定的值變更針對特定欄位顯示的選項。
* 根據在其他欄位中指定的值，在特定欄位中設定預設中繼資料值。

### 在[!DNL Experience Manager]中設定階層式中繼資料 {#configure-cascading-metadata-in-aem}

假設您想根據選取的資產型別顯示階層式中繼資料。 部分範例

* 對於視訊，會顯示適用的欄位，例如格式、轉碼器、持續時間等。
* 對於Word或PDF檔案，顯示欄位，例如頁數、作者等。

無論選擇的資產型別為何，都會將版權資訊顯示為必填欄位。

1. 在[!DNL Experience Manager]介面中，移至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
1. 在&#x200B;**[!UICONTROL 結構描述Forms]**&#x200B;頁面中，選取結構描述表單，然後從工具列按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以編輯結構描述。

   ![select_form](assets/select_form.png)

1. （選用）在中繼資料結構編輯器中，建立欄位以進行條件化。 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中指定名稱和屬性路徑。

   若要建立索引標籤，請按一下`+`以新增索引標籤，然後新增中繼資料欄位。

   ![add_tab](assets/add_tab.png)

1. 新增下拉欄位以取得資產型別。 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中指定名稱和屬性路徑。 新增選擇性說明。

   ![asset_type_field](assets/asset_type_field.png)

1. 機碼值組是提供給表單使用者的選項。 您可以手動或從JSON檔案提供索引鍵/值組。

   * 若要手動指定值，請選取&#x200B;**[!UICONTROL 手動新增]**，然後按一下&#x200B;**[!UICONTROL 新增選項]**&#x200B;並指定選項文字和值。 例如，指定「視訊」、「PDF」、「Word」和「影像」資產型別。

   * 若要從JSON檔案動態擷取值，請選取&#x200B;**[!UICONTROL 透過JSON路徑新增]**&#x200B;並提供JSON檔案的路徑。 當表單呈現給使用者時，[!DNL Experience Manager]會即時擷取機碼值組。

   這兩個選項是互斥的。 您無法從JSON檔案匯入選項並手動編輯。

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >新增JSON檔案時，索引鍵/值組不會顯示在中繼資料結構編輯器中，但會顯示在已發佈的表單中。

   >[!NOTE]
   >
   >新增選項時，如果按一下「下拉式」欄位，介面會扭曲，且選項的刪除選項會停止運作。 在儲存變更之前，請勿按下拉式清單。 如果您遇到此問題，請儲存結構並再次開啟以繼續編輯。

1. （選用）新增其他必要欄位。 例如，資產型別視訊的格式、轉碼器和持續時間。

   同樣地，為其他資產型別新增相依欄位。 例如，為檔案資產(如PDF和Word檔案)新增欄位頁數與作者。

   ![視訊相依欄位](assets/video_dependent_fields.png)

1. 若要在資產型別欄位與其他欄位之間建立相依性，請選擇相依欄位並開啟&#x200B;**[!UICONTROL 規則]**&#x200B;標籤。

   ![select_dependentfield](assets/select_dependentfield.png)

1. 在&#x200B;**[!UICONTROL 需求]**&#x200B;底下，根據新規則&#x200B;**選項選擇**&#x200B;必要。
1. 按一下&#x200B;**[!UICONTROL 新增規則]**&#x200B;並選擇&#x200B;**[!UICONTROL 資產型別]**&#x200B;欄位以建立相依性。 也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。按一下「**[!UICONTROL 完成]**」以儲存變更。

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >具有手動預先定義值的下拉式清單可與規則搭配使用。 已設定JSON路徑的下拉式功能表，無法搭配使用預先定義值來套用條件的規則使用。 如果值是在執行階段從JSON載入，則無法套用預先定義的規則。

1. 在「可 **[!UICONTROL 見性]**」下，選擇「可 **[!UICONTROL 見」，根據新規則選項]** 。

1. 按一下&#x200B;**[!UICONTROL 新增規則]**&#x200B;並選擇&#x200B;**[!UICONTROL 資產型別]**&#x200B;欄位以建立相依性。 也選擇要在其上建立相關性的欄位值。在這種情況下，請選擇「 **[!UICONTROL 視訊」]**。按一下「**[!UICONTROL 完成]**」以儲存變更。

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >按一下空格（或值以外的任何位置）會重設值。 如果發生此情況，請重新選取值。

   >[!NOTE]
   >
   >您可以套用 **[!UICONTROL 「需求]** 」條件 **[!UICONTROL 和「可見性]** 」條件，它們彼此獨立。

1. 同樣地，在「資產型別」欄位中的「視訊」值與其他欄位（例如「轉碼器」和「持續時間」）之間建立相依性。
1. 重複這些步驟，在[!UICONTROL Asset Type]欄位和[!UICONTROL Page Count]和[!UICONTROL Author]等欄位中，建立檔案資產(PDF和Word)之間的相依性。
1. 按一下「**[!UICONTROL 儲存]**」。將中繼資料結構套用至資料夾。

1. 導覽至您套用中繼資料結構的資料夾，並開啟資產的屬性頁面。 視您在「資產型別」欄位中的選擇而定，會顯示相關的階層式中繼資料欄位。

   ![視訊資產的階層式中繼資料](assets/video_asset.png)

   *圖：視訊的階層式中繼資料。*

   ![檔案資產](assets/doc_type_fields.png)的階層式中繼資料

   *圖：檔案的階層式中繼資料。*

## 刪除中繼資料結構表單 {#delete-metadata-schema-forms}

[!DNL Experience Manager]僅可讓您刪除自訂結構描述表單。 它不允許您刪除預設的結構表單/範本。 不過，您可以刪除這些表單中的任何自訂變更。

若要刪除表單，請選取表單並按一下刪除。

>[!NOTE]
>
>* 刪除預設表單的自訂變更後，鎖定![已關閉](assets/do-not-localize/lock_closed_icon.svg)會重新出現在表單前。 這表示表單已恢復為預設狀態。
>* 您無法刪除[!DNL Assets]中的預設中繼資料結構表單。

## MIME型別的結構表單 {#schema-forms-for-mime-types}

[!DNL Experience Manager]為各種現成的MIME型別提供預設表單。 不過，您可以為各種MIME型別的資產新增自訂表單。

### 為MIME型別新增表單 {#add-new-forms-for-mime-types}

在適當的表單型別下建立表單。 例如，若要為`image/png`子型別新增範本，請在「影像」表單下建立表單。 方案表單的標題是子類型名稱。在此案例中，標題為`png`。

#### 針對各種MIME型別使用現有結構描述範本 {#use-an-existing-schema-template-for-various-mime-types}

您可以將現有的範本用於不同的MIME型別。 例如，使用MIME型別`image/png`之資產的`image/jpeg`表單。

在這種情況下，請在CRX存放庫中的`/etc/dam/metadataeditor/mimetypemappings`建立節點。 指定節點名稱並定義下列屬性：

| 名稱 | 說明 | 類型 | 值 |
|------|-------------|------|-------|
| `exposedmimetype` | 要對應的現有表單名稱 | `String` | `image/jpeg` |
| `mimetypes` | 使用`exposedmimetype`屬性中定義之表單的MIME型別清單 | `String` | `image/png` |

[!DNL Assets]對應下列MIME型別和結構描述表單：

| 結構表單 | MIME型別 |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi， video/msvideo， video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## 授予存取中繼資料結構的許可權 {#grant-access-to-metadata-schemas}

「中繼資料結構」功能僅供管理員使用。 但是，管理員可以修改部分許可權，以向非管理員提供存取權。 提供非管理員使用者對`/conf`資料夾的建立、修改和刪除許可權。

## 套用資料夾特定的中繼資料 {#apply-folder-specific-metadata}

[!DNL Assets]可讓您定義中繼資料結構的變體，並將其套用至特定資料夾。

例如，您可以定義預設中繼資料結構的變體，並將其套用至資料夾。 當您套用修改後的結構描述時，它會覆寫套用至資料夾內資產的原始預設中繼資料結構描述。

只有上傳到套用此結構的資料夾的資產才符合變體中繼資料結構中定義的修改後中繼資料。 套用原始結構描述的其他資料夾中的[!DNL Assets]會繼續符合原始結構描述中定義的中繼資料。

資產的中繼資料繼承是根據套用至階層中頂層資料夾的結構描述。 子資料夾會套用或繼承相同的結構描述。 如果在子資料夾層級套用不同的結構描述，繼承就會停止。

1. 在[!DNL Experience Manager]介面中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 選取表單前面的核取方塊（例如，預設中繼資料表單），然後按一下&#x200B;**[!UICONTROL 複製]**&#x200B;並儲存為自訂表單。 指定表單的自訂名稱，例如`my_default`。 或者，您也可以建立自訂表格。

1. 在&#x200B;**[!UICONTROL 中繼資料結構Forms]**&#x200B;頁面中，選取`my_default`表單，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 在&#x200B;**[!UICONTROL 中繼資料結構描述編輯器]**&#x200B;頁面中，新增文字欄位至結構描述表單。 例如，新增標籤為&#x200B;**[!UICONTROL Category]**&#x200B;的欄位。

   ![文字欄位已新增至中繼資料結構表單編輯器](assets/text-field-metadata-schema-editor.png)

   *圖：文字欄位已新增至中繼資料結構描述表單編輯器。*

1. 按一下「**[!UICONTROL 儲存]**」。修改後的表單會列在&#x200B;**[!UICONTROL 中繼資料結構Forms]**&#x200B;頁面中。
1. 按一下工具列中的「套用至資料夾」**&#x200B;**，將自訂中繼資料套用至資料夾。

1. 選取要套用修改的結構描述的資料夾，然後按一下[套用]。**&#x200B;**

   ![選取要套用中繼資料結構描述的資料夾](assets/metadata-schema-select-folder.png)

1. 如果資料夾套用了其他中繼資料結構，系統會顯示一則訊息，警告您即將覆寫現有的中繼資料結構。 按一下&#x200B;**覆寫**。
1. 按一下&#x200B;**確定**&#x200B;關閉成功訊息。
1. 導覽至您套用修改後中繼資料結構的資料夾。

## 定義必要的中繼資料 {#define-mandatory-metadata}

您可以在檔案夾層級定義強制欄位，這會強制上傳至檔案夾的資產執行。 如果您上傳缺少先前定義之必要欄位中繼資料的資產，卡片檢視的資產會顯示缺少中繼資料的視覺指示。

>[!NOTE]
>
>中繼資料欄位可以根據其他欄位的值定義為必填欄位。 在卡片檢視中，[!DNL Experience Manager]不會顯示有關此類必要中繼資料欄位遺失中繼資料的警告訊息。

1. 在[!DNL Experience Manager]介面中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。 此時會顯示&#x200B;**[!UICONTROL 「中繼資料結構描述表單」]**&#x200B;頁面。
1. 將預設中繼資料表單儲存為自訂表單。 例如，將其儲存為`my_default`。

1. 編輯自訂表格。 新增必要欄位。 例如，新增&#x200B;**[!UICONTROL 類別]**&#x200B;欄位，並讓該欄位成為必要欄位。

   ![在中繼資料結構表單編輯器的[規則]索引標籤中選取[必要]，將必要欄位新增至中繼資料表單](assets/mandatory-field-metadata-schema-editor.png)

   *圖：中繼資料結構描述表單編輯器中的必要欄位。*

1. 按一下「**[!UICONTROL 儲存]**」。修改後的表單會列在&#x200B;**[!UICONTROL 中繼資料結構Forms]**&#x200B;頁面中。 選取表單，然後從工具列按一下&#x200B;**[!UICONTROL 套用至資料夾]**，將自訂中繼資料套用至資料夾。

1. 導覽至資料夾，然後上傳部分資產，其中遺失您新增至自訂表單之必要欄位的中繼資料。 資產卡片檢視中會顯示訊息，指出必填欄位缺少中繼資料。

   ![上傳資料夾中的資產時，資產卡檢視中缺少必要中繼資料的訊息](assets/metadata-missing-info-card-view.png)

1. （選擇性）存取`https://[aem_server]:[port]/system/console/components/`。 設定並啟用預設為停用的`com.day.cq.dam.core.impl.MissingMetadataNotificationJob`元件。 設定[!DNL Experience Manager]檢查資產中繼資料有效性的頻率。 此設定會將屬性`hasValidMetadata`新增至資產的`jcr:content`。 [!DNL Experience Manager]使用此屬性來篩選搜尋結果中的無效資產。 如果您在檢查後新增資產，則在下次排程檢查前，資產不會以`hasValidMetadata`標籤。 因此，直到下一次排程檢查後，資產才會出現在無效中繼資料的搜尋篩選條件中。

   >[!CAUTION]
   >
   >中繼資料驗證檢查需要大量資源，可能會影響系統效能。 相應地排程檢查。 如果伺服器無法應付負載，請嘗試停用此工作。

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
