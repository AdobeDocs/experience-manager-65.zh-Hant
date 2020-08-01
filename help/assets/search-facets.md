---
title: 搜尋 Facet.
description: 如何在中建立、修改和使用搜索小面 [!DNL Adobe Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '2488'
ht-degree: 16%

---


# 搜尋 Facet {#search-facets}

整個企業的部署可 [!DNL Adobe Experience Manager Assets] 以儲存許多資產。 有時，如果您只使用的一般搜尋功能，尋找正確的資產不但麻煩而且耗時 [!DNL Experience Manager]。

使用「篩選」面板中的搜尋Facet，為您的搜尋體驗增加更精細的度，並讓搜尋功能更有效率且更多功能。 搜尋刻面新增多個維度（謂語），可讓您執行更精細的搜尋。 「濾鏡」面板包含一些標準刻面。 您也可以新增自訂搜尋Facet。

總之，搜尋Facet可讓您以多種方式來搜尋資產，而非以單一、預先決定的分類順序來搜尋。 您可以輕鬆深入瞭解所需的詳細程度，以便進行更專注的搜尋。

例如，如果您要尋找影像，可以選擇要點陣圖還是向量影像。 您可以指定影像的MIME類型，進一步縮小搜尋範圍。 同樣地，在搜尋檔案時，您可以指定格式，例如PDF或MS Word。

## 添加謂詞 {#adding-a-predicate}

顯示在「篩選器」面板中的搜尋刻面是使用謂語在基礎搜尋表單中定義的。 若要顯示更多或不同的刻面，請新增謂語至預設表單，或使用包含您選擇刻面的自訂表單。

若為全文搜尋，請將  Fulltext謂語新增至表單。 使用Property predicate搜尋符合您指定之單一屬性的資產。 使用「選項」述詞可搜尋符合特定屬性之一或多個值的資產。 新增「日期範圍」述詞，以搜尋在指定日期範圍內建立的資產。

1. Click the [!DNL Experience Manager] logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]**, then click **[!UICONTROL Edit]** ![edit icon](assets/do-not-localize/aemassets_edit.png).

   ![尋找並選取資產或管理搜尋邊欄](assets/assets_admin_searchrail.png)

   >[!NOTE]
   >
   >若要使用舊版「資產管理搜尋邊欄」中預先設定的 **資料夾搜尋功能** ，請執行下列步驟：
   >
   >1. 導覽至 `/conf/global/settings/dam/search/facets/assets/jcr:content/items` CRXDE。
   >1. 刪除 **type節點** 。
   >1. 從路徑 */libs/settings/dam/search/facets/assets/jcr:content/items*，將節點資產、目錄、類型、排除路徑和 **searchtype****** ，複製到步驟1提及的路徑。
   >1. 儲存變更。


1. In the Edit Search Forms page, drag a predicate from the **[!UICONTROL Select Predicate]** tab to the main pane. 例如，拖曳 **[!UICONTROL Property Predicate]**。

   ![按並移動謂詞以自訂搜尋篩選器](assets/drag_predicate.png)

   *圖： 按並移動謂語以自訂搜尋篩選。*

1. 在「設定」標籤中，輸入謂語的欄位標籤、預留位置文字和說明。 為要與謂詞關聯的元資料屬性指定有效名稱。

   「設定」頁籤中的標題標籤標識所選謂詞的類型。

   ![使用「設定」頁籤提供謂語的必需選項](assets/settings.png)

   使用「設定」頁籤提供謂語的必需選項

1. 在「屬 **[!UICONTROL 性名稱]** 」欄位中，指定您要與謂語關聯的中繼資料屬性的有效名稱。它是根據其執行搜索的名稱。例如，輸入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。

   也可以從選擇對話框中選擇一個現有節點。

   ![將中繼資料屬性與屬性名稱欄位中的謂詞關聯](assets/property_settings.png)

   將中繼資料屬性與屬性名稱欄位中的謂詞關聯

1. 按一下「 **[!UICONTROL 預覽]**![」預覽](assets/do-not-localize/preview_icon.png) ，產生「篩選器」面板的預覽，如您新增述詞後所顯示。
1. 在「預覽」模式中查看謂語的佈局。

   ![在提交變更前預覽搜尋表格](assets/preview-1.png)

   在提交變更前預覽搜尋表格

1. 若要關閉預覽，請按 **[!UICONTROL 一下預]** 覽右 ![上角的「關閉](assets/do-not-localize/close.png) 」(Close close)。
1. 按一 **[!UICONTROL 下「完成]** 」以儲存設定。
1. Navigate to the Search panel in the [!DNL Assets] user interface. The Property predicate is added to the panel.
1. 在文本框中輸入要搜索的資產的說明。 For example, enter `Adobe`. 當您執行搜尋時，具有描述符合的資 `Adobe` 產會列在搜尋結果中。

## 新增選項述詞 {#adding-an-options-predicate}

「選項」謂語可讓您在「篩選」面板中新增多個搜尋選項。 您可以在「篩選」面板中選取一或多個這些選項，以搜尋資產。 例如，若要根據檔案類型來搜尋資產，請設定選項，例如搜尋表單中的影像、多媒體、檔案和封存。 設定這些選項後，當您在「濾鏡」面板中選取「影像」選項時，會對GIF、JPEG、PNG等類型的資產執行搜尋。

要將選項映射到相應屬性，請為選項建立節點結構，並在Options謂語的Property Name屬性中提供父節點的路徑。 父節點應為以下類型 `sling`: `OrderedFolder`. 選項應為類型 `nt:unstructured`。 選項節點應具有屬性並 `jcr:title` 進行 `value` 配置。

屬 `jcr:title` 性是顯示在「濾鏡」面板上的選項的用戶友好名稱。 該 `value` 欄位用於查詢以匹配指定的屬性。

選擇選項時，將根據選項節點及其子節點(如 `value` 果有)的屬性執行搜索。 會遍歷選項節點下的整個樹，並使 `value` 用OR操作組合每個子節點的屬性以形成搜索查詢。

例如，如果您為檔案類型選取「影像」，則會使用OR運算結合屬性來建立資 `value` 產的搜尋查詢。例如，通過組合影像/jpeg *、* image/gif *、* png影像、影像 */jpeg影像、以及使用OR操作對Tiff屬性進行搜索的Joff影像*****`jcr:content/metadata/dc:format` /Tiff影像的匹配結果來構建影像搜索查詢。

![CRXDE中所示的檔案類型的Value屬性用於搜索查詢](assets/filetype-value-property.png)

CRXDE中所示的檔案類型的Value屬性用於搜索查詢

您不必手動為CRXDE儲存庫中的選項建立節點結構，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。 在「屬性名稱」欄位中指定JSON檔 **[!UICONTROL 案的路徑]** 。例如，您可以定義鍵值配對、 `image/bmp`、 `image/gif``image/jpeg`、和 `image/png` 並指定其值，如下列範例JSON檔案中所示。In the **[!UICONTROL Property Name]** field, you can specify the CRXDE path for this file.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

如果要使用現有節點，請使用選擇對話框指定該節點。

>[!NOTE]
>
>Options謂語是包含屬性謂語的自訂包裝函式，用來展示描述的行為。 目前，沒有REST端點可用來支援本機功能。

1. Click the [!DNL Experience Manager] logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the **[!UICONTROL Search Forms]** page, select **[!UICONTROL Assets Admin Search Rail]**, then click **[!UICONTROL Edit]**.
1. 在「編 **[!UICONTROL 輯搜索表單]** 」頁中，將「選 **[!UICONTROL 項謂詞」從]** 「選擇謂詞 **** 」頁籤拖到主窗格。
1. 在「設 **[!UICONTROL 定]** 」標籤中，輸入屬性的標籤和名稱。例如，若要根據資產的格式來搜尋資產，請為標籤指定好記的名稱，例如「檔案類 **[!UICONTROL 型」]**。指定在屬性欄位中根據其執行搜索的屬性，例如 `jcr:content/metadata/dc:format.`
1. 執行下列任一項作業：

   * In the **[!UICONTROL Property Name]** field, mention the path of the JSON file where you define the nodes for the options and specify corresponding key-value pairs.
   * 按一下「 `+` 選項」欄位旁的符號，以指定您要在「篩選」面板中提供之選項的顯示文字和值。 要添加另一個選項，請單 `+` 擊符號並重複該步驟。

1. 確保清 **[!UICONTROL 除「單選]** 」，讓使用者一次為檔案類型選取多個選項 (例如影像、檔案、多媒體和封存)。如果您選 **[!UICONTROL 取「單選]**」，使用者一次只能為檔案類型選取一個選項。

   ![Options謂語中的可用欄位](assets/options_predicate.png)

   Options謂語中的可用欄位

1. 在「說 **[!UICONTROL 明]** 」欄位中，輸入選用的說明，然後按一下「 **[!UICONTROL 完成」]**。
1. 導覽至「搜尋」面板。 The Options predicate is added to **Search** panel. 「檔案類型」( **[!UICONTROL File Type]** )選項顯示為複選框。

## 添加多值屬性謂語 {#adding-a-multi-value-property-predicate}

「多值屬性」述詞可讓您搜尋資產以尋找多個值。 假設您在多個產品中有影像，而每個影 [!DNL Assets] 像的中繼資料包含與產品相關的SKU編號。 您可以使用此謂語，根據多個SKU編號搜尋產品影像。

1. Click the [!DNL Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. 在「搜尋表單」頁面上，選取「 **[!UICONTROL 資產管理搜尋邊欄]**」，按一下「編 **[!UICONTROL 輯]**![編輯」圖示](assets/do-not-localize/aemassets_edit.png)。
1. 在「編輯搜索表單」頁中，將「 **[!UICONTROL Multi Value Property Predicate]** 」從「 **[!UICONTROL Select Predicate]** 」頁籤拖動到主窗格。
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. 也可以使用選擇對話框選擇節點。
1. 請確定已 **[!UICONTROL 選取「分隔字元]** 」支援。在「輸入 **[!UICONTROL 分隔字元]** 」欄位中，指定分隔字元以分隔個別值。依預設，逗號會指定為分隔字元。您可以指定不同的分隔字元。
1. 在「說 **明** 」欄位中，輸入選用的說明，然後按一下「 **[!UICONTROL 完成」]**。
1. Navigate to the Filters panel in the [!DNL Assets] user interface. The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 在「多值」欄位中指定多個值，由分隔字元分隔，並執行搜尋。 謂語會為您指定的值提取完全符合的文字。

## 新增標籤述詞 {#adding-a-tags-predicate}

「標籤謂語」可讓您執行資產的標籤搜尋。 依預設， [!DNL Assets] 會根據您指定的標籤，搜尋一或多個標籤符合的資產。 換句話說，搜索查詢使用指定的標籤執行OR操作。 不過，您可以使用「符合所有標籤」選項來搜尋包含您所指定之所有標籤的資產。

1. Click the [!DNL Experience Manager] logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]** and then click **[!UICONTROL Edit]** ![edit icon](assets/do-not-localize/aemassets_edit.png).
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. 在「設定」標籤中，輸入謂語的預留位置文字。 Specify the property name based on which the search is to be performed in the property field, for example *jcr:content/metadata/cq:tags*. 或者，也可以從選擇對話框中選擇CRXDE中的節點。
1. 配置此謂語的Root標籤路徑屬性，以在「標籤」清單中填充各種標籤。
1. 選取 **[!UICONTROL 「顯示符合所有標籤」選項]** ，以搜尋包含您所指定之所有標籤的資產。

   ![Typical settings of Tags predicate](assets/tags_predicate.png)

   Typical settings of Tags predicate

1. 在「說 **[!UICONTROL 明]** 」欄位中，輸入選用的說明，然後按一下「 **[!UICONTROL 完成」]**。
1. 導覽至「搜尋」面板。 The **[!UICONTROL Tags]** predicate is added to the Search panel.
1. 指定您要依據其搜尋資產或從建議清單中選取的標籤。

   ![在輸入標籤名稱時，Experience Manager提供的建議](assets/tag-suggestion.png)

   *圖： 在輸入標籤名稱時，Experience Manager提供的建議。*

1. Select **[!UICONTROL Match all]** to search for matches that include all tags that you specify.

## 添加其他謂語 {#adding-other-predicates}

與添加Property predicate或Options predicate的方式類似，您可以將以下附加謂語添加到「搜索」面板：

| 謂詞名稱 | 說明 | 屬性 |
|---|---|---|
| [!UICONTROL 全文] | 搜索謂詞，以在整個資產節點上執行全文搜索。 它會與jcr:contains運算子映射。 如果要對資產節點的特定部分執行全文搜索，可以指定相對路徑。 | <ul><li>標籤</li><li>預留位置</li><li>屬性名稱</li><li>說明</li></ul> |
| [!UICONTROL 路徑瀏覽器] | 搜尋謂詞，以搜尋預先設定之根路徑之資料夾和子檔案夾中的資產 | <ul><li>預留位置</li><li>根路徑</li><li>說明</li></ul> |
| [!UICONTROL 路徑] | 使用它來篩選位置的結果。 您可以指定不同的路徑作為選項。 | <ul><li>標籤</li><li>路徑</li><li>說明</li></ul> |
| [!UICONTROL 發佈狀態] | 根據資產的發佈狀態搜尋謂詞以搜尋資產 | <ul><li>標籤</li><li>屬性名稱</li><li>說明</li></ul> |
| [!UICONTROL 相對日期] | 搜尋謂詞以根據資產建立的相對日期來搜尋資產。 例如，您可以設定選項，例如2個月前、3週前等。 | <ul><li>標籤</li><li>屬性名稱</li><li>相對日期</li></ul> |
| [!UICONTROL 範圍] | 搜尋謂詞以搜尋位於指定範圍內的資產。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。 | <ul><li>標籤</li><li>屬性名稱</li><li>說明</li></ul> |
| [!UICONTROL 日期範圍] | 搜尋謂詞，以搜尋在指定範圍內建立的日期屬性資產。 在「搜尋」面板中，您可以使用日期選擇器指定「開始和結束日期」。 | <ul><li>標籤</li><li>預留位置</li><li>屬性名稱</li><li>範圍文字（自）</li><li>範圍文字（至）</li><li>說明</li></ul> |
| [!UICONTROL 日期] | 根據日期屬性搜尋資產的滑桿式搜尋謂詞。 | <ul><li>標籤</li><li>屬性名稱</li><li>說明</li></ul> |
| [!UICONTROL 檔案大小] | 搜尋謂詞以根據資產大小搜尋資產。 它是基於Silder的謂語，您可在其中從可配置節點中選擇Slider選項。 預設選項在CRXDE儲存庫的/libs/dam/options/predicates/filesize中定義。 檔案大小以位元組為單位。 | <ul><li>標籤</li><li>屬性名稱</li><li>路徑</li><li>說明</li></ul> |
| [!UICONTROL 上次修改的資產] | 搜尋謂詞以搜尋最近修改的資產 | <ul><li>屬性名稱</li><li>屬性值</li><li>說明</li></ul> |
| [!UICONTROL 發佈狀態] | 搜尋謂詞以根據資產的發佈狀態搜尋資產 | <ul><li>標籤</li><li>屬性名稱</li><li>說明</li></ul> |
| [!UICONTROL 評等] | 根據資產的平均分級來搜尋資產的搜尋謂語 | <ul><li>標籤</li><li>屬性名稱</li><li>選項路徑</li><li>說明</li></ul> |
| [!UICONTROL 到期狀態] | 搜尋謂詞以根據資產的到期狀態搜尋資產 | <ul><li>標籤</li><li>屬性名稱</li><li>說明</li></ul> |
| [!UICONTROL 隱藏] | 定義隱藏欄位屬性以搜尋資產的搜尋謂詞 | <ul><li>屬性名稱</li><li>屬性值</li><li>說明</li></ul> |

## 還原預設搜尋刻面 {#restoring-default-search-facets}

依預設，「搜尋表單」頁 ![面中的「資產管理搜尋邊欄](assets/do-not-localize/lock_closed_icon.svg) 」前，會顯示鎖定圖示「鎖定 **[!UICONTROL 關閉」圖示]****** 。 「搜尋表單」頁面上的選項鎖定圖示表示預設設定保持不變且未自訂。 如果將搜 ![尋Facet新增至表單](assets/do-not-localize/lock_closed_icon.svg) ，表示已修改預設表單，圖示會消失鎖定關閉的圖示。

![「搜尋表單」頁面上的選項鎖定圖示表示預設設定保持不變且未自訂。](assets/locked_admin_rail.png)

若要還原預設搜尋Facet，請執行下列步驟：

1. 在「搜 **[!UICONTROL 尋表單」頁面中]** ，選取「資 **[!UICONTROL 產管理搜尋邊欄]** 」。
1. 按一下 **[!UICONTROL 工具欄]**![中的「刪除刪除大綱](assets/do-not-localize/deleteoutline.png) 」。
1. 在確認對話方塊中，按一下 **[!UICONTROL 刪除]** ，移除自訂變更。

   After you delete the custom changes to search facets, the lock icon ![lock closed icon](assets/do-not-localize/lock_closed_icon.svg) reappears before **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page.

## User permissions {#user-permissions}

如果您未獲指派管理員角色，請列出您執行編輯、刪除和預覽與搜尋Facet有關之動作時所需的權限。

| 動作 | 權限 |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL 編輯] | CRXDE中節點的讀 `/apps` 寫權限 |
| [!UICONTROL 刪除] | 在CRXDE中讀取、寫入和刪除節 `/apps` 點的權限 |
| [!UICONTROL 預覽] | 在CRXDE中讀取、寫入和刪 `/var/dam/content` 除節點權限。 此外，節點上的「讀取」和「寫入」 `/apps` 權限。 |

>[!MORELIKETHIS]
>
>* [擴充資產搜尋功能](searchx.md)
>* [搜尋資產](search-assets.md)

