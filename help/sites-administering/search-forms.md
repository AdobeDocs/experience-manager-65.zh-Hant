---
title: 配置搜索表單
seo-title: 配置搜索表單
description: 瞭解如何設定搜尋表單。
seo-description: 瞭解如何設定搜尋表單。
uuid: 0d30921c-0d4d-4ab6-b796-7833cd321e5d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: abc27987-960e-48da-9580-1008a2bdc94c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置搜索表單{#configuring-search-forms}

使用 **Search Forms** ，自訂在各種AEM控制台和／或作者環境面板中可用的搜尋面板中使用的搜尋謂語選擇。 自訂這些面板可讓搜尋功能根據您的特定需求而變得多功能。

預 [測語](#predicates-and-their-settings)的範圍是現成可用的。 您可以新增多個謂語，包括（其中包括）全文搜尋的Fulltext謂語、搜尋符合您所指定單一屬性的資產的Property謂語，或搜尋符合您為特定屬性指定之一或多個值的資產的Options謂語。

您可以 [設定各種控制台和資產瀏覽器](#configuring-your-search-forms) （編輯頁面時）中使用的搜尋表單。 可 [以通過以下方式訪問用於配置這些表單](#configuring-your-search-forms) 的對話框：

* **工具**

   * **一般**

      * **搜尋表單**

首次訪問此控制台時，您可以看到所有配置都有掛鎖符號。 這表示適當的組態是預設（現成可用）組態——且無法刪除。 在您自訂配置後，鎖定將消失——除非您刪 [除自訂配置](#deleting-a-configuration-to-reinstate-the-default)，否則將恢復預設（和掛鎖指示器）。

![chlimage_1-374](assets/chlimage_1-374.png)

## 設定 {#configurations}

可用的預設配置包括：

* **頁面編輯器 (文件搜尋):**

   此設定會定義在資產瀏覽器中搜尋檔案時（在編輯頁面時）可用的選項。

* **頁面編輯器 (影像搜尋):**

   此設定會定義在資產瀏覽器中搜尋影像時（在編輯頁面時）可用的選項。

* **頁面編輯器 (手稿搜尋):**

   此設定會定義在資產瀏覽器中搜尋手稿時（在編輯頁面時）可用的選項。

* **頁面編輯器 (頁面搜尋):**

   此設定會定義在資產瀏覽器中搜尋頁面時（在編輯頁面時）可用的選項。

* **頁面編輯器 (段落搜尋):**

   此設定會定義在資產瀏覽器中搜尋段落時（在編輯頁面時）可用的選項。

* **頁面編輯器 (產品搜尋):**

   此設定會定義在資產瀏覽器中搜尋產品時（在編輯頁面時）可用的選項。

* **頁面編輯器 (Scene7 搜尋)**:

   此設定會定義在資產瀏覽器中搜尋Scene7資源時（在編輯頁面時）可用的選項。

* **網站管理搜尋邊欄**:

   此配置定義了當使用站點控制台的搜索邊欄時用戶可用的搜索選項。

* **頁面編輯器 (視訊搜尋):**

   此設定會定義在資產瀏覽器中搜尋影片（在編輯頁面時）時可用的選項。

* **資產管理搜尋邊欄:**

   此設定定義使用「資產」控制台時，使用者可使用的搜尋選項。

* **目錄管理搜尋邊欄:**

   此配置定義了搜索商務目錄時用戶可用的搜索選項。

* **訂單管理搜尋邊欄:**

   此配置定義了在搜索商務訂單時用戶可用的搜索選項。

* **產品集合管理搜尋邊攔:**

   此設定會定義搜尋商務產品集合時使用者可用的搜尋選項。

* **產品管理搜尋邊欄:**

   此配置定義了搜索商務產品時用戶可用的搜索選項。

* **專案管理搜尋邊欄:**

   此配置定義了用戶在搜索項目時可用的搜索選項。

## 謂語及其設定 {#predicates-and-their-settings}

### 謂語 {#predicates}

以下謂語可用，取決於配置：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>目的</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析 </td>
   <td>顯示分析支援的資料時，在「網站」瀏覽器中執行搜尋／篩選功能。 載入Analytics搜尋篩選器以符合已映射的自訂分析欄。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>上次修改的資產 </td>
   <td>上次修改資產的日期。<br /> </td>
   <td>A customized predicate, based on the Date Predicate.</td>
  </tr>
  <tr>
   <td>元件 </td>
   <td>允許作者搜尋／篩選含有特定元件的頁面。 例如影像收藏館。<br /> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>屬性深度</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期 </td>
   <td>根據日期屬性，以滑桿為基礎搜尋資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期範圍 </td>
   <td>搜尋在指定範圍內建立的日期屬性資產。 在「搜尋」面板中，您可以指定開始和結束日期。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>範圍文字（自）*</li>
     <li>範圍文字（至）*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期狀態 </td>
   <td>根據到期狀態搜尋資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>檔案大小 </td>
   <td>根據資產大小搜尋資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>全文 </td>
   <td>Search predicate for full-text searches.</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隱藏的篩選器</td>
   <td>屬性和值的篩選器，不對使用者顯示。</td>
   <td>
    <ul>
     <li>屬性名稱</li>
     <li>屬性值</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>選項 </td>
   <td><p>這些選項是用戶建立的內容節點。</p> <p>如需詳 <a href="#addinganoptionspredicate">細資訊，請參閱新增選項</a> 「謂詞」。</p> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>JSON 路徑</li>
     <li>屬性名稱*</li>
     <li>單選</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>選項屬性 </td>
   <td>搜尋選項的屬性。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項節點路徑<br /> </li>
     <li>單選</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>頁面狀態 </td>
   <td>根據頁面狀態搜尋頁面。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>發佈屬性名稱</li>
     <li>LiveCopy 屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路徑 </td>
   <td>搜尋位於特定路徑下的資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>新增搜尋路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>屬性 </td>
   <td>在指定的屬性上搜尋。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>發佈狀態 </td>
   <td>根據資產的發佈狀態搜尋資產</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範圍 </td>
   <td>搜尋位於指定範圍內的資源。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範圍選項 </td>
   <td>A specific search predicate for Assets and the as as common Slider Predicate. 由於向後相容性問題，仍可使用。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>評等 </td>
   <td>根據資產的評分搜尋資產。<br /> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>相對日期 </td>
   <td>根據資產建立的相對日期來搜尋資產<br /> </td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>相對日期</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>滑桿範圍 </td>
   <td>使用slider功能擴展範圍謂語的通用搜索謂語。 所搜尋的屬性值必須介於滑桿限制之間。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標記 </td>
   <td>根據標籤搜尋資產。 您可以設定Path屬性，以填入「標籤」清單中的各種標籤。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>選項路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標記 </td>
   <td>根據標籤進行搜尋。</td>
   <td>
    <ul>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 常見搜索謂語定義於：
   >  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
   >
   >
   >

* 僅與網站管理員（傳統UI）相關的搜尋謂語位於：
   > `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
   >   * 這些版本已過時，僅適用於向後相容性。
>
>
此資訊僅供參考，您不得變更 `/libs`。

### 謂詞設定 {#predicate-settings}

Dependent on the predicate a selection of settings are available for configuration:

* **欄位標籤**

   將顯示為可折疊標題或謂語欄位標籤的標籤。

* **說明**

   使用者的說明性詳細資訊。

* **預留位置**

   空文本或謂語的佔位符，以備未輸入篩選文本時使用。

* **屬性名稱**

   要搜索的屬性。 它使用相對路徑，而萬用字元 `*/*/*` 指定屬性相對於節點的深度(每個星 `jcr:content` 號代表一個節點層級)。

   如果只想搜索在節點上具有該屬性的資源的第一級子 `x` 節點上 `jcr:content` 使用 `*/jcr:content/x`

* **屬性深度**

   在資源中搜索該屬性的最大深度。 因此，可對資源和遞歸子項執行對該屬性的搜索，直到子項的級別等於指定深度。

* **屬性值**

   屬性值是絕對字串或運算式語言；例如， `cq:Page` 或

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **範圍文字**

   日期範圍謂語中的範圍欄 **位標籤** 。

* **選項路徑**

   用戶可以使用謂詞設定頁籤中的路徑瀏覽器來選擇路徑。 選取+圖 **示後** ，會將選取範圍新增至有效選項清單(如有需要， **** 則會移除——圖示)。

   這些選項是由用戶建立的內容節點，具有以下結構：

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Options node path**（選項節點路徑）與 **** Options Path（選項路徑）有效相同，僅此欄位位於公用謂語欄位中，而另一個欄位則特定於資產。

* **單選選**&#x200B;項如果選中，選項將顯示為僅允許單選項的複選框。 如果錯誤選取，則可取消選取核取方塊。

* **Publish和Live copy屬性名稱Sites**&#x200B;特定述詞的publish和live copy核取方塊標籤。

* &amp;ast;在「設定」標籤的欄 **位標籤上** ，表示欄位為必填，若留空，則會顯示錯誤訊息

## 設定搜尋表單 {#configuring-your-search-forms}

### 建立／開啟自定義配置 {#creating-opening-a-customized-configuration}

1. 導覽至「 **工具**」、「 **作業**」、「 **搜尋表格**」。

1. 選擇要定製的配置。
1. 使用「編 **輯** 」表徵圖開啟要更新的配置。
1. 如果有新的自訂，您可能想要新 [增謂詞欄位，並視需要定義](#add-edit-a-predicate-field-and-define-field-settings) 設定。 如果現有自訂，您可以選取現有欄位並 [更新設定](#add-edit-a-predicate-field-and-define-field-settings)。
1. 選擇「 **完成** 」以保存配置。

   >[!NOTE]
   >
   >自定義的配置儲存在（如果適用）以下位置：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### 添加／編輯謂詞欄位和定義欄位設定 {#add-edit-a-predicate-field-and-define-field-settings}

您可以新增或編輯欄位，並定義／更新其設定：

1. [開啟自訂的設定](#creating-opening-a-customized-configuration) ，以進行更新。
1. 如果要添加新欄位，請開啟「選 **擇謂詞** 」頁籤，並將所需的謂詞拖動到所需位置。 例如，日 **期範圍謂語**:

   ![chlimage_1-375](assets/chlimage_1-375.png)

1. 取決於：

   * 您正在添加新欄位：

      添加謂詞後，「 **設定** 」頁籤將開啟並顯示可定義的屬性。

   * 要更新現有謂詞：

      選擇謂詞欄位（在右側），然後開啟「設 **置** 」頁籤。
   例如，「日期範圍謂詞」 **的設定**:

   ![chlimage_1-376](assets/chlimage_1-376.png)

1. 視需要進行變更，然後使用「完成」 **確認**。

### 預覽搜尋設定 {#previewing-the-search-configuration}

1. 選取「預覽」圖示：

   ![](do-not-localize/chlimage_1-31.png)

1. 這會顯示搜尋表單，如同在適當主控台的「搜尋」欄中顯示（完全展開）。

   ![chlimage_1-377](assets/chlimage_1-377.png)

1. **關閉** 「預覽」以返回並完成配置。

### 刪除謂詞欄位 {#deleting-a-predicate-field}

1. [開啟自訂的設定](#creating-opening-a-customized-configuration) ，以進行更新。
1. 選擇謂詞欄位（在右側），開啟「 **Settings** （設定）」頁籤，然後選擇「 **Delete** （刪除）」表徵圖（左下）。

   ![](do-not-localize/chlimage_1-32.png)

1. 對話方塊會要求確認刪除動作。

1. 使用「完成」確認此變更和任何其 **他變更**。

### 刪除配置（以恢復預設值） {#deleting-a-configuration-to-reinstate-the-default}

在您自訂設定後，這將覆寫預設值。 您可以刪除自訂的設定，重新設定預設的設定。

>[!NOTE]
>
>不能刪除任一預設配置。

從控制台刪除自定義配置：

1. 選擇所需的配置(例如，頁 **面編輯器（段落搜尋）**)，然後在工具列中選 **** 擇刪除圖示：

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 將刪除自定義配置並恢復預設配置（這由控制台中重新出現掛鎖符號表示）。

### 添加選項謂語 {#adding-options-predicates}

選項謂語（選項、選項屬性）可讓您設定要搜尋的項目。 通常用來搜尋頁面下方的內容；例如，頁面節點上的屬性。

下列範例（根據用於建立頁面的範本進行搜尋）說明相關步驟：

1. 建立定義要搜索的屬性的節點。

   您需要一個根節點，其中包含用戶可以使用的各個選項的定義。

   各個選項的節點需要以下屬性：

   * `jcr:title` -要在搜索邊欄中顯示的欄位標籤
   * `value` -要搜索的屬性值
   ![chlimage_1-379](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >您 ***不得*** 更改路徑中的任 `/libs` 何內容。
   >
   >這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
   >
   >配置和其他更改的建議方法為：
   >
   >1. 重新建立所需項目，如其中 `/libs`所存在 `/apps`。 在本例中，來源為：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在 `/apps.`


1. 開啟「 **搜尋表單** 」主控台，並選取您要更新的組態。 例如，「網 **站管理搜尋邊欄」**。

   然後按一下／點選「編 **輯搜尋表單** 」圖示。

1. 視配置而定，將「選 **項** 」 **或「選項屬性** 」添加到配置。
1. 更新欄位，尤其是：

   * **屬性名稱**

      在目標節點上指定要搜索的節點屬性。 例如：

      `jcr:content/cq:template`

   * **選項節點路徑**

      選取您的選項所在的路徑。 例如：

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![chlimage_1-380](assets/chlimage_1-380.png)

1. 選擇 **完成** ，保存配置。
1. 導覽至適當的主控台(在此範例中 **為Sites**)，並開啟 **Search邊欄** 。 新定義的搜尋表單以及各種選項將會顯示。 選擇所需選項以查看搜索結果：

   ![chlimage_1-381](assets/chlimage_1-381.png)

## 使用者權限 {#user-permissions}

下表列出在搜尋表單上執行編輯、刪除和預覽動作所需的權限。

<table>
 <tbody>
  <tr>
   <td><strong>動作</strong></td>
   <td><strong>權限</strong></td>
  </tr>
  <tr>
   <td>編輯 </td>
   <td>讀取、寫入節點 <code>/apps </code>權限。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td>節點上的讀取、寫入、刪除權 <code>/apps</code> 限</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td>讀取、寫入、刪除節點上的權 <code>/var/dam/content</code> 限。<br /> 讀取、寫入節點的 <code>/apps</code> 權限。</td>
  </tr>
 </tbody>
</table>

