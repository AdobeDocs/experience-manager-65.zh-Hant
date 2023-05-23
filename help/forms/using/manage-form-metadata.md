---
title: 管理表單元資料
seo-title: Manage form metadata
description: 元資料允許更輕鬆地對資產進行分類和組織，並幫助正在查找特定資產的用戶。
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
role: Admin
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 1%

---

# 管理表單元資料{#manage-form-metadata}

## 概觀  {#overview-nbsp}

元資料允許更輕鬆地對資產進行分類和組織，並幫助正在查找特定資產的用戶。

AEM Forms預設為每種資產類型提供一組定義的元資料。 除預設元資料外，您還可以將自定義元資料添加到每個資產類型。 AEM Forms還為您提供了有效建立、管理和交換所有這些元資料的正確方法。

如果您是開發人員或站點所有者，則可以自定義Forms門戶，這是AEM Forms的最終用戶介面，用於反映您在組織中使用的元資料。 有關Forms門戶的詳細資訊，請參閱 [門戶上發佈表單簡介](../../forms/using/introduction-publishing-forms.md)。

## AEM Forms元資料 {#metadata-in-aem-forms}

在AEM Forms，與資產關聯的元資料屬性清單取決於其類型。 此外，如果添加了任何自定義元資料屬性，則會在添加自定義元資料的類型的所有資產中添加該屬性。

### 資產類型 {#asset-types}

AEM Forms支援以下資產類型：

* 表單模板（XFA表單）
* PDF forms
* 文檔(平面PDF)
* 調適型表單
* 資源
* XFS

#### 元資料的詳細清單 {#extensive-list-of-metadata}

以下是AEM Forms支援的元資料屬性的詳細清單：

<table>
 <tbody> 
  <tr> 
   <td><strong>屬性名稱</strong></td> 
   <td><strong>資產類型</strong></td> 
   <td><strong>說明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>標題</td> 
   <td>資源除外</td> 
   <td>窗體的顯示名稱。<br /> </td> 
  </tr> 
  <tr> 
   <td>說明</td> 
   <td>資源除外</td> 
   <td>窗體的說明。 用戶可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>類型</td> 
   <td>全部</td> 
   <td><p>指定資產類型的只讀值。 它可以具有以下值之一：</p> 
    <ul> 
     <li>表單模板</li> 
     <li>PDF表單、PDF表單（頂框）或PDF表單（簽名）</li> 
     <li>文檔，文檔（簽名）</li> 
     <li>調適性表單</li> 
     <li>資源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>建立日期</td> 
   <td>全部</td> 
   <td>指定資產建立時間的只讀值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>全部</td> 
   <td>指定上次修改資產的時間的只讀值。</td> 
  </tr> 
  <tr> 
   <td>作者</td> 
   <td>資源除外</td> 
   <td><p>根據表單類型自動計算的只讀值。</p> 
    <ul> 
     <li>PDF/表單模板/文檔 — 從上載的二進位檔案中讀取。</li> 
     <li>自適應表單 — 建立表單時登錄的用戶。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>狀態</td> 
   <td>資源除外</td> 
   <td><p> 一個只讀值，它定義表單的以下狀態之一：</p> 
    <ul> 
     <li>無值：如果表單從未發佈。</li> 
     <li>已發佈：發佈窗體時。</li> 
     <li>已修改：在發佈一次後修改窗體的時間。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次發佈日期</td> 
   <td>資源除外</td> 
   <td>指定上次發佈表單的時間的只讀值。</td> 
  </tr> 
  <tr> 
   <td>發佈開/關時間</td> 
   <td>資源除外</td> 
   <td><p>計畫自動發佈/取消發佈表單的時間。 用戶在編輯元資料時設定此值。</p> 
    <ul> 
     <li>「發佈開啟」和「關閉」時間都應超出當前日期。 </li> 
     <li>發佈關閉時間應超出發佈按時間。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表單模板</p> <p>PDF窗體</p> </td> 
   <td><p>配置用戶指定的URL，以將表單資料提交到Servlet。</p> <p>可以使用以下任何方法配置提交URL（按優先順序列出）:</p> 
    <ul> 
     <li>在AEM Forms設計器中建立XFA表單時，使用「HTTP提交」按鈕直接在表單模板中指定提交URL。</li> 
     <li>在AEM FormsUI中，選擇表單並指定編輯元資料屬性時的提交URL。</li> 
     <li>在Forms門戶中，編輯Search &amp; Lister元件，並在「表單連結」頁籤下指定提交URL。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML渲染配置檔案</td> 
   <td>表單模板</td> 
   <td>以HTML格式呈現表單模板時使用的HTML渲染配置檔案。</td> 
  </tr> 
  <tr> 
   <td>呈現格式</td> 
   <td><p>表單模板</p> <p>調適性表單</p> </td> 
   <td><p>此選項允許用戶在發佈表單時指定表單的呈現格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>兩者</li> 
    </ul> <p>此選項僅用於限制表單的呈現格式，在表單門戶中，表單對最終用戶可見。</p> </td> 
  </tr> 
  <tr> 
   <td>標記</td> 
   <td>資源除外</td> 
   <td>與表單關聯的標籤有助於快速、輕鬆地搜索。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>調適性表單</p> <p>表單模板</p> <p>資源</p> </td> 
   <td><p>此表單相關的資產（其他表單或資源）清單。 這些資產可分為以下兩類：</p> 
    <ul> 
     <li>參考：當前表單所指的資產。</li> 
     <li>參考者：指流動資產的資產。</li> 
    </ul> <p>這些資產顯示為連結，通過按一下這些資產可以直接訪問其元資料。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表單模型(XDP/XSD)選擇</td> 
   <td>調適性表單</td> 
   <td><p>指定在創作自適應表單時使用的表單模型。 此屬性可以具有以下值：</p> 
    <ul> 
     <li>表單模板：從儲存庫中現有的表單模板中選擇一個表單模板。 可以更新此值。</li> 
     <li>XML架構：已上載XSD檔案。 可以更新此值。</li> 
     <li>無</li> 
    </ul> 
    <div>
      選定後，可更新但不能刪除表單模型。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 查看表單元資料 {#view-form-metadata}

資產具有現有屬性值，可以在只讀模式下查看。 此元資料在表單上載或表單建立時發生。

1. 導航到要查看其元資料的資產的位置。

1. 使用以下方法之一開啟屬性頁：

   1. 按一下「查看屬性」 ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) 表徵圖。

      >[!NOTE]
      >
      >「快速操作」(Quick Actions)是滑鼠懸停時在縮略圖上顯示的操作項。

   1. 選擇表單，然後按一下「查看屬性」 ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) 表徵圖。
   1. 在不處於選擇模式時，按一下表單縮略圖，導航到表單詳細資訊頁。 現在，按一下 ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) 右上角的「眼睛」表徵圖，然後按一下其下方清單中的「屬性」。

1. 開啟的屬性頁顯示一個僅包含那些包含某些值的元資料屬性的架構。

   「屬性」頁的工具欄包含兩個操作表徵圖：

   * 編輯： ![aem6forms_edit](assets/aem6forms_edit.png) 編輯元資料屬性值
   * 視圖： ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) 導航至表單詳細資訊頁面，該頁面在預覽模式下開啟表單。

   內容部分分為兩部分：

   * 左面板包含窗體的縮覽圖
   * 右面板包含只讀模式下的元資料屬性，這些屬性分佈在各個頁籤中。


## 添加/更新表單元資料值 {#add-update-form-metadata-values}

您可以編輯現有元資料屬性的值或向現有元資料屬性欄位添加新值（例如，元資料欄位為空時）。

### 更新元資料屬性值 {#update-metadata-property-values}

1. 按照上一節中提到的步驟開啟屬性頁，在該頁中可以查看所選表單的現有元資料。

1. 在工具欄中，按一下編輯表徵圖 ![aem6forms_edit](assets/aem6forms_edit.png) 將頁面模式從只讀更改為讀/寫。

1. 開啟的屬性頁包含一個包含可編輯輸入欄位和靜態文本混合的架構。

1. 靜態文本中顯示的屬性是無法編輯的屬性。

1. 您可以導航到其他頁籤，以查找位於這些頁籤下的元資料屬性的輸入欄位。

   此頁面的工具欄包含兩個與視圖模式操作表徵圖不同的操作表徵圖：

   * 取消： ![aem6forms_close](assets/aem6forms_close.svg_w24.png) 取消迄今對元資料屬性值所做的任何更改
   * 完成： ![aem6forms_check](assets/aem6forms_check.png) 保存迄今對元資料屬性值所做的所有更改

   這兩個操作都將用戶引導回包含更新值的屬性頁的只讀模式。

### 更新表單縮略圖 {#update-the-form-thumbnail}

屬性頁中的左面板顯示表單的縮略圖。 預設情況下，顯示的縮略圖是在建立表單（自適應表單）時或在上載表單時生成的縮略圖。

對於所有表單類型，您可以選擇通過按一下 **[!UICONTROL 上載映像]** 並從本地目錄瀏覽影像檔案。 所選影像將用作縮略圖，而不是預設影像。

對於自適應表單，提供了附加功能，其允許用戶生成縮略圖作為當前自適應表單預覽的快照。 由於AEM Forms也支援自適應表單的創作，因此每次更改自適應表單時，自適應表單的預覽可能會發生更改。 生成縮略圖的功能可幫助您根據當前預覽狀態獲取自適應表單的新縮略圖。 按一下 **[!UICONTROL 生成預覽]** 來執行此操作。

>[!NOTE]
>
>* 將方形影像用於縮略圖。 使用非方形影像並在清單視圖中查看縮略圖時，縮略圖會被剪切。
>* 上載或生成新影像後，縮略圖將被此影像替換，無法重置為以前的影像。
>


## 添加自定義元資料 {#add-custom-metadata}

除了現成提供的元資料外，AEM Forms還支援新的定製元資料。

提供了一種工具（元資料模式編輯器）來定義元資料佈局的模式；即，顯示在 **[!UICONTROL 屬性]** 的子菜單。 通過元資料架構編輯器，可以添加或修改資產的自定義架構。

AEM Forms在此工具中顯示受支援表單類型的元資料模式。 這樣，您就可以訪問這些架構並使用元資料架構編輯器中提供的功能來添加自定義屬性。

### 導航元資料架構編輯器 {#navigate-the-metadata-schema-editor}

1. 導航到 **[!UICONTROL 「工具」>「資產」>「元資料架構」]**。

1. 按一下 **[!UICONTROL 表]** 從列出的架構窗體中。

1. 在開啟的清單中，按一下要為其添加自定義元資料的資產類型。

   >[!NOTE]
   >
   >這些架構包含的元資料屬性是現成的，不得更改/編輯（選中複選框，然後按一下工具欄中的編輯），以避免出現功能問題。

1. 按一下的任何資產類型都會開啟包含 `extendedmetadata` 的雙曲餘切值。 編輯此架構。

1. 選中旁邊的複選框 `extendedmetadata` ，然後按一下「編輯」 ![aem6forms_edit](assets/aem6forms_edit.png) 表徵圖。

1. AEM Forms開啟選定資產類型的元資料架構編輯器/表單構建器（在本例中為自適應表單）。

   ![Adaptive Form類型的元資料架構編輯器](assets/metadata-schema-editor-for-adaptive-form-type.png)

   元資料編輯器

   1. 左面板包含頁籤式部分，其中放置了欄位，右面板顯示所有可用的UI元件以及從左面板中選擇的欄位的屬性。

   1. 鎖定的節不可編輯，並且包含框外提供的所有元資料屬性的欄位。

   1. 可通過按一下+符號來添加其它頁籤。

   1. 通過將欄位元件從 **[!UICONTROL 生成窗體]** 的子目錄。
   1. 此欄位的規範可在 **[!UICONTROL 設定]** 的下界。

### 在架構編輯器中添加自定義元資料屬性 {#add-custom-metadata-property-in-schema-editor}

1. 導航到要添加自定義屬性的頁籤（現有或新）。

1. 從 **[!UICONTROL 生成窗體]** 框，並放置在方便的位置。

   >[!NOTE]
   >
   >不能移動鎖定的節，但可以將元件放置在任何空格中。

1. 按一下剛拖動的元件。 在右面板中開啟的「設定」頁籤中，填寫以下欄位的資訊：

   1. 指定將用作方案中放置的欄位上方顯示名稱的欄位標籤(例如：部門)
   1. 在「映射到屬性」(Map to property)欄位下，可以看到預填充值 **「 」。/jcr:content/metadata/default**。 更改「**預設**&#39;到所需的屬性名稱，該名稱用於將屬性儲存在crx儲存庫中(例如：「 」。/jcr:content/metada/department&#39;

      >[!NOTE]
      >
      >不要更改前置詞「。/jcr:content/metadata/&#39;，因為它定義了儲存屬性的路徑。
      >
      >此外，屬性名稱必須唯一，以避免在儲存庫中同一位置寫入兩個或更多屬性的值。 因此，建議您更改值「default」。

   1. 根據要求填寫其他設定。 例如：如果要使欄位成為必填欄位，請選擇「必需」選項。
   1. 要刪除添加的欄位，請選擇該欄位，然後按一下刪除 ![刪除–1](assets/delete-1.png) 表徵圖

1. 如有必要，請執行步驟1-3以添加其他屬性。
1. 按一下 **完成** 做了所有的改變。

   您已成功添加自定義元資料屬性。

AEM Forms的所有自適應表單現在都包含此附加的元資料屬性。 可以從屬性頁編輯它。
