---
title: 批量編輯器
seo-title: The Bulk Editor
description: 瞭解如何使用批量編輯器。
seo-description: Learn how to use the Bulk Editor.
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# 批量編輯器{#the-bulk-editor}

批量編輯器允許在不需要可視頁面上下文時進行非常有效的編輯，因為它允許您：

* 從多個頁面搜索（和顯示）內容；這是使用GQL(Google查詢語言)完成的
* 直接在批量編輯器中編輯此內容
* 保存更改（到原始頁面）
* 將此內容導出到以制表符分隔的(.tsv)電子錶格檔案

>[!NOTE]
>
>您也可以將內容導入儲存庫，但預設情況下，在「批量編輯器」中禁用此功能。 **工具** 控制台。

本節介紹如何使用中的批量編輯器 **工具** 控制台。 通常，管理員使用批量編輯器搜索和編輯多個項目。 通過使用GQL查詢填充表，然後選擇要處理的內容項來完成此操作。 作者通常將批量編輯器用作可通過 [產品清單](/help/sites-authoring/default-components.md#productlist) 元件。

>[!CAUTION]
>
>使用 [經典UI的棄用](/help/release-notes/deprecated-removed-features.md) 在AEM6.4中，批量編輯器也已被棄用，因此Adobe不打算進一步增強批量編輯器。

## 批量編輯器的示例用例 {#example-use-case-for-the-bulk-editor}

例如，如果您需要填寫特定調查的用戶的所有姓名和電子郵件地址，批量編輯器可以提供該資訊，並可以將其導出到電子錶格中。

在Geometrixx網站中包含一個示例來說明此使用案例：

1. 導航到 **支援** 頁面，然後 **客戶服務滿意度** 調查。
1. **編輯** 這樣 **窗體開頭** 段。 在對話框中，按一下 **高級** 的 **操作配置**，然後按一下 **查看資料……**。

   ![](assets/custsatsurvey.png)

1. 批量編輯器是完全可自定義的。雖然在本示例中，批量編輯器不允許用戶編輯內容，但只允許用戶將資訊導出到電子錶格。

   ![](assets/bulkeditor.png)

## 如何使用批量編輯器 {#how-to-use-the-bulk-editor}

批量編輯器允許您：

* [根據查詢參數搜索內容，在列中顯示結果的指定屬性，編輯此內容並保存更改](#searching-and-editing-content)
* [將此內容導出到以制表符分隔的電子錶格](#exporting-content)

* [從以制表符分隔的電子錶格導入內容](#importing-content)

### 搜索和編輯內容 {#searching-and-editing-content}

要使用批量編輯器同時編輯多個項目：

1. 在 **工具** 控制台，按一下 **進口商** 資料夾以展開。
1. 按兩下 **批量編輯器** 開啟它。
1. 輸入您的選擇要求：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>屬性</td>
  </tr>
  <tr>
   <td>根路徑</td>
   <td>指示批量編輯器搜索的根路徑。<br /> 比如說， <code>/content/geometrixx/en</code>。 批量編輯器將搜索所有子節點。</td>
  </tr>
  <tr>
   <td>查詢參數</td>
   <td>使用GQL參數，輸入您希望批量編輯器在儲存庫中查找的搜索字串；比如說， <code>type:Page</code> 查找根路徑中的所有頁面， <code>text:professional</code> 查找所有包含「專業」一詞的頁面， <code>"jcr:title":English</code> 查找以「英語」為標題的所有頁面。 只能搜索字串。</td>
  </tr>
  <tr>
   <td>「內容模式」複選框</td>
   <td>選中此複選框可讀取 <code>jcr:content</code> 搜索結果的子節點（如果存在）。 僅用於頁面。 屬性名稱前置詞為 <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>屬性/欄</td>
   <td>選中希望批量編輯器返回的屬性的複選框。 您選擇的屬性是結果窗格中的列標題。 預設情況下，節點路徑將顯示在結果中。</td>
  </tr>
  <tr>
   <td>自訂屬性/欄</td>
   <td>輸入未列在 <strong>屬性/列</strong> 的子菜單。 這些自定義屬性將出現在結果窗格中。 可以使用逗號分隔屬性，從而添加多個屬性。 <i>注：</i> 如果添加的自定義屬性尚不存在，AEM WCM將顯示一個空單元格。 修改並保存空單元格時，屬性將添加到節點。 新建立的屬性必須考慮節點類型約束和屬性命名空間。</td>
  </tr>
 </tbody>
</table>

例如：

![](assets/searchfilter.png)

1. 按一下 **搜索**。 「批量編輯器」(Bulk Editor)顯示結果。
在上例中，符合搜索條件的所有頁面都將返回並顯示為請求的列。

   ![](assets/chlimage_1-39.png)

1. 通過按兩下單元格進行任何需要的更改。

   ![](assets/srchresultedit.png)

1. 按一下 **保存** 保存更改( **保存** 按鈕)。

   >[!CAUTION]
   >
   >您在此處所做的更改將寫入儲存庫內容；例如，中引用的頁 **路徑**。

#### 其他GQL查詢參數 {#additional-gql-query-parameters}

* **路徑：** 僅搜索此路徑下的節點。 如果指定多個具有路徑前置詞的術語，則只考慮最後一個術語。
* **類型：** 僅返回給定節點類型的節點。 這包括主類型和混合類型。 可以指定多個逗號分隔的節點類型。 GQL將返回屬於任何指定類型的節點。
* **訂單：** 按給定屬性對結果進行排序。 可以指定多個逗號分隔的屬性名稱。 要按降序順序排序結果，只需在屬性名稱前加上減號。 例如：順序：-name。 使用加號將以升序返回結果，這也是預設值。
* **限制：** 使用間隔限制結果數。 例如：limit:10..20請注意，間隔為零，起始為包括，終止為排除。 您還可以指定開啟間隔:limit:10.. 或限制：..20如果省略點並且只指定一個值，則GQL最多將返回此數目的結果。 例如，限制：10（將返回前10個結果）

### 導出內容 {#exporting-content}

您可能需要在Excel電子錶格中導出內容並對其進行更改。 例如，您可能希望導出郵件清單，並直接在Excel中更改所有列出電話號碼的區號，添加其他線路等。

要導出內容：

1. 搜索內容（如所述） [搜索和編輯內容](#searching-and-editing-content)。
1. 按一下 **導出** 將更改導出到以制表符分隔的Excel電子錶格。 AEMWCM詢問您要從何處下載檔案。

   >[!NOTE]
   >
   >預設情況下，更改將編碼為 [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) （也稱為CP-1252）。 您可以檢查UTF-8以導出UTF-8中的更改。

   ![](assets/srchrsesultexport.png)

1. 選擇位置並確認要下載檔案。
1. 下載檔案後，可以從電子錶格程式開啟它，例如，MicrosoftExcel。 電子錶格程式導入檔案並將其轉換為電子錶格格式。

   ![](assets/exportinexcel.png)

### 導入內容 {#importing-content}

預設情況下，開啟「批量編輯器」時，導入功能將隱藏。 只需添加參數 `hib=false` 將顯示 **導入** 按鈕。 可以從任何以制表符分隔的( `.tsv`)。 為了使導入工作正常，列標題（第一行單元格）必須與要導入到的表的列標題匹配。

>[!NOTE]
>
>重新導入內容時，將清除這些節點的任何先前內容。 注意不要覆蓋重要資訊。

要導入內容：

1. 開啟批量編輯器。
1. 添加 `?hib=false` 到URL，例如：
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. 按一下 **導入**。
1. 選擇 `.tsv` 的子菜單。 資料將導入儲存庫。
