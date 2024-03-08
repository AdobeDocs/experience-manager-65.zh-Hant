---
title: 大量編輯器
description: 瞭解如何在不需要視覺化頁面內容時，使用大量編輯器來有效編輯。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# 大量編輯器{#the-bulk-editor}

當不需要視覺化頁面內容時，大量編輯器可提供有效的編輯，因為它可讓您：

* 從多個頁面搜尋（和顯示）內容；這是使用GQL (Google查詢語言)完成的
* 直接在大量編輯器中編輯此內容
* 儲存變更（至原始頁面）
* 將此內容匯出至以定位點分隔的(.tsv)試算表檔案

>[!NOTE]
>
>您也可以將內容匯入存放庫，但根據預設，這在「大量編輯器」中是停用的，因為 **工具** 主控台。

本節說明如何使用中的大量編輯器 **工具** 主控台。 通常，管理員會使用大量編輯器來搜尋和編輯多個專案。 這是透過使用GQL查詢填入表格，然後選取要處理的內容專案來完成的。 作者通常使用大量編輯器作為自訂大量編輯器應用程式的一部分，可透過以下方式存取： [產品清單](/help/sites-authoring/default-components.md#productlist) 元件。

>[!CAUTION]
>
>使用 [汰除傳統UI](/help/release-notes/deprecated-removed-features.md) 在AEM 6.4中，大量編輯器也已被取代，因此Adobe不打算進一步增強大量編輯器。

## 大量編輯器的範例使用案例 {#example-use-case-for-the-bulk-editor}

例如，如果您需要填寫特定調查的使用者的所有名稱和電子郵件地址，大量編輯器可以提供該資訊，並且您可以將它匯出到試算表中。

Geometrixx網站中提供了此使用案例的說明範例：

1. 導覽至 **支援** 頁面，然後移至 **客戶服務滿意度** 意見調查。
1. **編輯** 此 **表單的開頭** 段落。 在對話方塊中，按一下 **進階** 標籤，展開 **動作設定**，然後按一下 **檢視資料……**.

   ![客戶滿意度調查範例](assets/custsatsurvey.png)

1. 大量編輯器是完全可自訂的，不過在此範例中，大量編輯器不允許使用者編輯內容，但僅允許他們匯出資訊到試算表。

   ![大量編輯器主控台](assets/bulkeditor.png)

## 如何使用大量編輯器 {#how-to-use-the-bulk-editor}

大量編輯器可讓您：

* [根據查詢引數搜尋內容、在欄中顯示結果的指定屬性、編輯此內容並儲存變更](#searching-and-editing-content)
* [以將此內容匯出至以定位點分隔的試算表](#exporting-content)

* [以從定位字元分隔的試算表匯入內容](#importing-content)

### 搜尋和編輯內容 {#searching-and-editing-content}

若要使用「大量編輯器」同時編輯多個專案：

1. 在 **工具** 主控台，按一下 **匯入工具** 資料夾以展開它。
1. 按兩下 **大量編輯器**.
1. 輸入您的選取需求：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>屬性</td>
  </tr>
  <tr>
   <td>根路徑</td>
   <td>表示大量編輯器搜尋的根路徑。<br /> 例如， <code>/content/geometrixx/en</code>. 「大量編輯器」會搜尋所有子節點。</td>
  </tr>
  <tr>
   <td>查詢參數</td>
   <td>使用GQL引數，輸入您希望「大量編輯器」在存放庫中尋找的搜尋字串。 例如， <code>type:Page</code> 會尋找根路徑中的所有頁面， <code>text:professional</code> 會尋找所有含有「專業」字樣的頁面，並且 <code>"jcr:title":English</code> 會尋找所有以「英文」為標題的頁面。 您只能搜尋字串。</td>
  </tr>
  <tr>
   <td>內容模式核取方塊</td>
   <td>選取此核取方塊，即可讀取 <code>jcr:content</code> 搜尋結果的子節點（如果存在）。 僅用於頁面。 屬性名稱的前置詞為 <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>屬性/欄</td>
   <td>選取您希望「大量編輯器」傳回之屬性的核取方塊。 您選取的屬性是結果窗格中的欄標題。 依預設，節點路徑會顯示在結果中。</td>
  </tr>
  <tr>
   <td>自訂屬性/欄</td>
   <td>輸入未列在 <strong>屬性/欄</strong> 欄位。 這些自訂屬性會出現在結果窗格中。 您可以使用逗號來分隔屬性，以新增多個屬性。 <i>注意：</i> 如果您新增尚不存在的自訂屬性，AEM WCM會顯示空白儲存格。 修改空白儲存格並儲存後，屬性會新增至節點。 新建立的屬性必須符合節點型別限制和屬性名稱空間。</td>
  </tr>
 </tbody>
</table>

例如：

![大量編輯器篩選器選項](assets/searchfilter.png)

1. 按一下 **搜尋**. 大量編輯器會顯示結果。
以上例為例，系統會傳回符合搜尋條件的所有頁面，並顯示要求的欄。

   ![大量編輯器結果](assets/chlimage_1-39.png)

1. 按兩下儲存格，以便進行任何變更。

   ![大量編輯](assets/srchresultedit.png)

1. 按一下 **儲存** 以儲存變更( **儲存** 按鈕會在您編輯儲存格後啟動)。

   >[!CAUTION]
   >
   >您在此進行的變更會寫入存放庫內容；例如，中參照的頁面 **路徑**.

#### 其他GQL查詢引數 {#additional-gql-query-parameters}

* **路徑：** 僅搜尋此路徑下的節點。 如果您指定多個具有路徑首碼的字詞，則只會考慮最後一個字詞。
* **型別：** 僅傳回給定節點型別的節點。 這包括主要和mixin型別。 您可以指定多個逗號分隔的節點型別。 GQL會傳回任何指定型別的節點。
* **訂購：** 依指定的屬性排序結果。 您可以指定多個以逗號分隔的屬性名稱。 若要以遞減順序排序結果，只需在屬性名稱前面加上減號即可。 例如，order：-name。 使用加號會以遞增順序傳回結果，這也是預設值。
* **限制：** 使用間隔來限制結果的數量。 例如，limit：10..20間隔以零為基準，開始為包含範圍，結束為排除範圍。 您也可以指定開啟 `interval:limit:10..` 或 `limit:..20`
如果省略點且只指定了一個值，GQL最多會傳回此數量的結果。 例如， `limit:10` （傳回前十個結果）。

### 匯出內容 {#exporting-content}

如有必要，請將內容匯出至Excel試算表以進行任何變更。 例如，您可能想要匯出郵寄清單，並直接在Excel中變更所有列出電話號碼的區號，或新增其他行。

若要匯出內容：

1. 依照中的說明搜尋內容 [搜尋和編輯內容](#searching-and-editing-content).
1. 按一下 **匯出** 以便您將變更匯出至以定位點分隔的Excel試算表。 AEM WCM會詢問您要下載檔案的位置。

   >[!NOTE]
   >
   >依預設，變更的編碼方式為 [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) （也稱為CP-1252）。 您可以勾選UTF-8以匯出UTF-8中的變更。

   ![匯出結果](assets/srchrsesultexport.png)

1. 選取位置並確認您要下載檔案。
1. 下載檔案後，您可以從試算表程式(例如Microsoft® Excel)開啟該檔案。 試算表程式會匯入檔案，並將其轉換為試算表格式。

   ![在試算表中匯出的結果](assets/exportinexcel.png)

### 匯入內容 {#importing-content}

依預設，當您開啟「大量編輯器」時，匯入功能會隱藏。 只需新增引數 `hib=false` 至URL會顯示 **匯入** 按鈕。 您可以從任何以定位字元分隔的內容匯入( `.tsv`)檔案時每小時精細度無法運作的問題。 為了讓匯入正確運作，欄標題（儲存格的第一列）必須與要匯入至的表格欄標題相符。

>[!NOTE]
>
>當您重新匯入內容時，會清除這些節點之前的任何內容。 請注意不要覆寫重要資訊。

若要匯入內容：

1. 開啟大量編輯器。
1. 新增 `?hib=false` 至URL，例如：
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. 按一下 **匯入**.
1. 選取 `.tsv` 檔案。 資料會匯入存放庫。
