---
title: 搜尋Facet以篩選搜尋結果
description: 如何在 [!DNL Adobe Experience Manager]中建立、修改和使用搜尋刻面。
contentOwner: AG
role: Administrator, Developer
feature: Search
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '2427'
ht-degree: 15%

---


# 搜尋 Facet {#search-facets}

[!DNL Adobe Experience Manager Assets]的整個企業部署可儲存許多資產。 有時，如果您只使用[!DNL Experience Manager]的一般搜尋功能，尋找正確的資產不但麻煩而且耗時。

使用「篩選」面板中的搜尋Facet，為您的搜尋體驗增加更精細的度，並讓搜尋功能更有效率且更多功能。 搜尋刻面新增多個維度（謂語），可讓您執行更精細的搜尋。 「濾鏡」面板包含一些標準刻面。 您也可以新增自訂搜尋Facet。

總之，搜尋Facet可讓您以多種方式來搜尋資產，而非以單一、預先決定的分類順序來搜尋。 您可以輕鬆深入瞭解所需的詳細程度，以便進行更專注的搜尋。

例如，如果您要尋找影像，可以選擇要點陣圖還是向量影像。 您可以指定影像的MIME類型，進一步縮小搜尋範圍。 同樣地，在搜尋檔案時，您可以指定格式，例如PDF或MS Word。

## 添加謂詞{#adding-a-predicate}

顯示在「篩選器」面板中的搜尋刻面是使用謂語在基礎搜尋表單中定義的。 若要顯示更多或不同的刻面，請新增謂語至預設表單，或使用包含您選擇刻面的自訂表單。

對於全文搜索，請將[!UICONTROL Fulltext]謂語添加到表單中。 使用Property predicate搜尋符合您指定之單一屬性的資產。 使用「選項」述詞可搜尋符合特定屬性之一或多個值的資產。 新增「日期範圍」述詞，以搜尋在指定日期範圍內建立的資產。

1. 按一下[!DNL Experience Manager]標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 從「搜尋Forms」頁面，選擇&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**，然後按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;編輯圖示](assets/do-not-localize/aemassets_edit.png)。![

   ![尋找並選取「資產」或「管理搜尋邊欄」](assets/assets_admin_searchrail.png)

   >[!NOTE]
   >
   >若要使用舊版中預先設定的&#x200B;**資產管理搜尋邊欄**&#x200B;的資料夾搜尋功能，請執行下列步驟：
   >
   >1. 導覽至CRXDE中的`/conf/global/settings/dam/search/facets/assets/jcr:content/items`。
   >1. 刪除&#x200B;**type**&#x200B;節點。
   >1. 從路徑`/libs/settings/dam/search/facets/assets/jcr:content/items`將節點`asset`、`directory`、`typeor`、`excludepaths`和`searchtype`複製到步驟1中提及的路徑。
   >1. 儲存變更。


1. 在[!UICONTROL 編輯搜索Forms]頁中，將&#x200B;**[!UICONTROL 選擇謂詞]**&#x200B;頁籤中的謂詞拖動到主窗格。 例如，拖曳&#x200B;**[!UICONTROL Property Predicate]**。

   ![選擇並移動謂詞以自定義搜索篩選器](assets/drag_predicate.png)

   *圖：選擇並移動謂語以自訂搜尋篩選器。*

1. 在[!UICONTROL Settings]標籤中，輸入謂語的欄位標籤、預留位置文字和說明。 為要與謂詞關聯的元資料屬性指定有效名稱。 [!UICONTROL Settings]標籤中的標題標籤標識所選謂語的類型。

1. 在「屬 **[!UICONTROL 性名稱]** 」欄位中，指定您要與謂語關聯的中繼資料屬性的有效名稱。它是根據其執行搜索的名稱。例如，輸入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。

   也可以從選擇對話框中選擇一個現有節點。

   ![將中繼資料屬性與屬性名稱欄位中的謂詞關聯](assets/property_settings.png)

   將中繼資料屬性與屬性名稱欄位中的謂詞關聯

1. 按一下&#x200B;**[!UICONTROL Preview]** ![preview](assets/do-not-localize/preview_icon.png)，產生在新增謂語後所顯示的「篩選器」面板預覽。
1. 在「預覽」模式中查看謂語的佈局。

   ![在提交變更前預覽搜尋表格](assets/preview-1.png)

   在提交變更前預覽搜尋表格

1. 要關閉預覽，請按一下預覽右上角的&#x200B;**[!UICONTROL Close]** ![close](assets/do-not-localize/close.png)。
1. 按一下&#x200B;**[!UICONTROL Done]**&#x200B;保存設定。
1. 導覽至[!DNL Assets]使用者介面中的「搜尋」面板。 The Property predicate is added to the panel.
1. 在文本框中輸入要搜索的資產的說明。 例如，輸入`Adobe`。 當您執行搜尋時，描述符合`Adobe`的資產會列在搜尋結果中。

## 添加選項謂詞{#adding-an-options-predicate}

「選項」謂語可讓您在「篩選」面板中新增多個搜尋選項。 您可以在「篩選」面板中選取一或多個這些選項，以搜尋資產。 例如，若要根據檔案類型來搜尋資產，請設定選項，例如搜尋表單中的影像、多媒體、檔案和封存。 設定這些選項後，當您在「濾鏡」面板中選取「影像」選項時，會對GIF、JPEG、PNG等類型的資產執行搜尋。

要將選項映射到相應屬性，請為選項建立節點結構，並在Options謂語的Property Name屬性中提供父節點的路徑。 父節點應為`sling`類型：`OrderedFolder`。 選項的類型應為`nt:unstructured`。 選項節點應配置`jcr:title`和`value`屬性。

`jcr:title`屬性是顯示在「篩選器」面板上的選項的用戶友好名稱。 `value`欄位用於查詢中，以符合指定的屬性。

選擇選項時，將根據選項節點及其子節點的`value`屬性（如果有）執行搜索。 會遍歷選項節點下的整個樹，並使用OR操作組合每個子節點的`value`屬性以形成搜索查詢。

例如，如果您為檔案類型選取「影像」，則會使用OR運算結合屬性來建立資 `value` 產的搜尋查詢。例如，通過組合影像/jpeg *、* image/gif *、* png影像、影像 */jpeg影像、以及使用OR操作對Tiff屬性進行搜索的Joff影像*****`jcr:content/metadata/dc:format` /Tiff影像的匹配結果來構建影像搜索查詢。

![CRXDE中所示的檔案類型的Value屬性用於搜索查詢](assets/filetype-value-property.png)

CRXDE中所示的檔案類型的Value屬性用於搜索查詢

您不必手動為CRXDE儲存庫中的選項建立節點結構，而是可以透過指定對應的索引鍵值配對，來定義JSON檔案中的選項。 在「屬性名稱」欄位中指定JSON檔 **[!UICONTROL 案的路徑]** 。例如，您可以定義鍵值配對、 `image/bmp`、 `image/gif``image/jpeg`、和 `image/png` 並指定其值，如下列範例JSON檔案中所示。在&#x200B;**[!UICONTROL 屬性名稱]**&#x200B;欄位中，您可以指定此檔案的CRXDE路徑。

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

1. 按一下[!DNL Experience Manager]標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 從&#x200B;**[!UICONTROL 搜尋Forms]**&#x200B;頁面，選擇&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**，然後按一下&#x200B;**[!UICONTROL 編輯]**。
1. 在「編 **[!UICONTROL 輯搜索表單]** 」頁中，將「選 **[!UICONTROL 項謂詞」從]** 「選擇謂詞 **** 」頁籤拖到主窗格。
1. 在「設 **[!UICONTROL 定]** 」標籤中，輸入屬性的標籤和名稱。例如，若要根據資產的格式來搜尋資產，請為標籤指定好記的名稱，例如「檔案類 **[!UICONTROL 型」]**。指定在屬性欄位中根據其執行搜索的屬性，例如 `jcr:content/metadata/dc:format.`
1. 執行下列任一項作業：

   * 在&#x200B;**[!UICONTROL 屬性名稱]**&#x200B;欄位中，提及您在其中定義選項節點並指定對應索引鍵值配對的JSON檔案路徑。
   * 按一下「選項」欄位旁的`+`符號，以指定您要在「篩選」面板中提供之選項的顯示文字和值。 要添加另一個選項，請按一下`+`符號並重複該步驟。

1. 確保清 **[!UICONTROL 除「單選]** 」，讓使用者一次為檔案類型選取多個選項 (例如影像、檔案、多媒體和封存)。如果您選 **[!UICONTROL 取「單選]**」，使用者一次只能為檔案類型選取一個選項。

   ![Options謂語中的可用欄位](assets/options_predicate.png)

   Options謂語中的可用欄位

1. 在&#x200B;**[!UICONTROL Description]**&#x200B;欄位中，輸入選用的說明，然後按一下&#x200B;**[!UICONTROL Done]**。
1. 導覽至「搜尋」面板。 Options predicate is added to the **Search** panel. **[!UICONTROL File Type]**&#x200B;的選項顯示為複選框。

## 添加多值屬性謂語{#adding-a-multi-value-property-predicate}

「多值屬性」述詞可讓您搜尋資產以尋找多個值。 假設您[!DNL Assets]中有多個產品的影像，且每個影像的中繼資料包含與產品相關聯的SKU編號。 您可以使用此謂語，根據多個SKU編號搜尋產品影像。

1. 按一下[!DNL Experience Manager]標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 在「搜尋Forms」頁面上，選擇&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**，按一下「編輯」****![編輯圖示](assets/do-not-localize/aemassets_edit.png)。
1. 在「編輯搜索表單」頁中，將「 **[!UICONTROL Multi Value Property Predicate]** 」從「 **[!UICONTROL Select Predicate]** 」頁籤拖動到主窗格。
1. 在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤中，輸入謂語的標籤和佔位符文本。 指定屬性名稱，如`jcr:content/metadata/dc:value`，根據該名稱在屬性欄位中執行搜索。 也可以使用選擇對話框選擇節點。
1. 請確定已 **[!UICONTROL 選取「分隔字元]** 」支援。在「輸入 **[!UICONTROL 分隔字元]** 」欄位中，指定分隔字元以分隔個別值。依預設，逗號會指定為分隔字元。您可以指定不同的分隔字元。
1. 在&#x200B;**Description**&#x200B;欄位中，輸入選用的說明，然後按一下&#x200B;**[!UICONTROL Done]**。
1. 導覽至[!DNL Assets]使用者介面中的「篩選」面板。 The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 在「多值」欄位中指定多個值，由分隔字元分隔，並執行搜尋。 謂語會為您指定的值提取完全符合的文字。

## 添加標籤謂詞{#adding-a-tags-predicate}

「標籤謂語」可讓您執行資產的標籤搜尋。 依預設，[!DNL Assets]會根據您指定的標籤搜尋資產，以尋找一或多個符合的標籤。 換句話說，搜索查詢使用指定的標籤執行OR操作。 不過，您可以使用「符合所有標籤」選項來搜尋包含您所指定之所有標籤的資產。

1. 按一下[!DNL Experience Manager]標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**。
1. 從「搜尋Forms」頁面，選擇&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**，然後按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;編輯圖示](assets/do-not-localize/aemassets_edit.png)。![
1. 在「編輯搜索表單」頁中，將&#x200B;**[!UICONTROL Tags Predicate]**&#x200B;從「選擇謂詞」頁籤拖動到主窗格。
1. 在「設定」標籤中，輸入謂語的預留位置文字。 指定屬性名稱，依據該名稱在屬性欄位中執行搜尋，例如&#x200B;*jcr:content/metadata/cq:tags*。 或者，也可以從選擇對話框中選擇CRXDE中的節點。
1. 配置此謂語的Root標籤路徑屬性，以在「標籤」清單中填充各種標籤。
1. 選取 **[!UICONTROL 「顯示符合所有標籤」選項]** ，以搜尋包含您所指定之所有標籤的資產。

1. 在&#x200B;**[!UICONTROL Description]**&#x200B;欄位中，輸入選用的說明，然後按一下&#x200B;**[!UICONTROL Done]**。
1. 導覽至「搜尋」面板。 **[!UICONTROL Tags]**&#x200B;謂語已新增至「搜尋」面板。
1. 指定您要依據其搜尋資產或從建議清單中選取的標籤。

1. 選擇&#x200B;**[!UICONTROL Match all]**&#x200B;以搜尋包含您所指定之所有標籤的相符項目。

## 添加其他謂語{#adding-other-predicates}

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

## 恢復預設搜索刻面{#restoring-default-search-facets}

依預設，在&#x200B;**[!UICONTROL 搜尋Forms]**&#x200B;頁面的&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**&#x200B;前會出現鎖定圖示![鎖定關閉圖示](assets/do-not-localize/lock_closed_icon.svg)。 「搜尋Forms」頁面上的選項鎖定圖示表示預設設定保持不變，且未自訂。 如果向表單添加搜索Facet，表示預設表單已修改，則表徵圖![鎖定關閉表徵圖](assets/do-not-localize/lock_closed_icon.svg)將消失。

![「搜尋Forms」頁面上的選項鎖定圖示表示預設設定保持不變，且未自訂。](assets/locked_admin_rail.png)

若要還原預設搜尋Facet，請執行下列步驟：

1. 在&#x200B;**[!UICONTROL 搜尋Forms]**&#x200B;頁面中，選取&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**。
1. 按一下工具欄中的&#x200B;**[!UICONTROL Delete]** ![deleteoutline](assets/do-not-localize/deleteoutline.png)。
1. 在確認對話框中，按一下&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除自定義更改。

   刪除搜尋Facet的自訂變更後，在&#x200B;**[!UICONTROL 搜尋Forms]**&#x200B;頁面的&#x200B;**[!UICONTROL 資產管理搜尋邊欄]**&#x200B;前會重新顯示鎖定圖示![已關閉圖示](assets/do-not-localize/lock_closed_icon.svg)。

## 用戶權限{#user-permissions}

如果您未獲指派管理員角色，請列出您執行編輯、刪除和預覽與搜尋Facet有關之動作時所需的權限。

| 動作 | 權限 |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL 編輯] | CRXDE中`/apps`節點的讀寫權限 |
| [!UICONTROL 刪除] | CRXDE中`/apps`節點的讀、寫和刪除權限 |
| [!UICONTROL 預覽] | 對CRXDE中`/var/dam/content`節點的讀取、寫入和刪除權限。 此外，`/apps`節點的「讀取」和「寫入」權限。 |

>[!MORELIKETHIS]
>
>* [擴充資產搜尋功能](searchx.md)
>* [搜尋資產](search-assets.md)

