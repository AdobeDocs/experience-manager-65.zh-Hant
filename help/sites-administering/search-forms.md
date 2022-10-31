---
title: 設定搜尋表單
description: 了解如何設定搜尋Forms。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 11%

---

# 設定搜尋表單{#configuring-search-forms}

使用 **搜尋Forms** 自訂在各種AEM主控台和/或製作環境面板中可用的搜尋面板中所使用的搜尋述詞選擇。 自訂這些面板，可讓搜尋功能根據您的特定需求而多用。

A [謂語範圍](#predicates-and-their-settings)可立即使用。 您可以新增多個述詞，其中包括（其中包括）「屬性述詞」以搜尋符合您所指定之單一屬性的資產，或「選項述詞」以搜尋符合您為特定屬性所指定之一或多個值的資產。

您可以 [配置搜索表單](#configuring-your-search-forms) 用於各種主控台和資產瀏覽器（編輯頁面時）。 此 [配置這些表單的對話框](#configuring-your-search-forms) 可透過下列方式存取：

* **工具**

   * **一般**

      * **搜尋表單**

首次訪問此控制台時，您會看到所有配置都帶有掛鎖符號。 這表示適當的設定是預設（現成）設定，且無法刪除。 自訂設定後，鎖就會消失 — 除非您 [刪除自訂配置](#deleting-a-configuration-to-reinstate-the-default)，則會恢復預設值（和掛鎖指示器）。

![chlimage_1-374](assets/chlimage_1-374.png)

## 設定 {#configurations}

可用的預設配置有：

* **頁面編輯器 (文件搜尋):**

   此設定會定義在資產瀏覽器中搜尋檔案時（編輯頁面時）可用的選項。

* **頁面編輯器 (影像搜尋):**

   此設定會定義在資產瀏覽器中搜尋影像時（編輯頁面時）可用的選項。

* **頁面編輯器 (手稿搜尋):**

   此設定會定義在資產瀏覽器中搜尋手稿時（編輯頁面時）可用的選項。

* **頁面編輯器 (頁面搜尋):**

   此設定會定義在資產瀏覽器中搜尋頁面時（編輯頁面時）可用的選項。

* **頁面編輯器 (段落搜尋):**

   此設定會定義在資產瀏覽器中搜尋段落時（編輯頁面時）可用的選項。

* **頁面編輯器 (產品搜尋):**

   此設定會定義在資產瀏覽器中搜尋產品時（編輯頁面時）可用的選項。

* **頁面編輯器(Dynamic Media Classic [原稱Scene7] 搜尋)**:

   此設定會定義在資產瀏覽器中搜尋Scene7資源時（編輯頁面時）可用的選項。

* **網站管理搜尋邊欄**:

   此設定會定義使用者在使用Sites主控台的搜尋邊欄時可用的搜尋選項。

* **頁面編輯器 (視訊搜尋):**

   此設定會定義在資產瀏覽器中搜尋視訊時（編輯頁面時）可用的選項。

* **資產管理搜尋邊欄:**

   此設定會定義使用者使用Assets控制台時可用的搜尋選項。

* **目錄管理搜尋邊欄:**

   此設定定義搜尋商務目錄時，使用者可用的搜尋選項。

* **訂單管理搜尋邊欄:**

   此設定定義搜尋商務訂單時，使用者可用的搜尋選項。

* **產品集合管理搜尋邊攔:**

   此設定定義搜尋商務產品集合時，使用者可用的搜尋選項。

* **產品管理搜尋邊欄:**

   此設定定義搜尋商務產品時，使用者可用的搜尋選項。

* **專案管理搜尋邊欄:**

   此設定會定義搜尋專案時使用者可用的搜尋選項。

## 謂語及其設定 {#predicates-and-their-settings}

### 謂語 {#predicates}

下列謂語可用，視設定而定：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>用途</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析 </td>
   <td>顯示分析支援的資料時，在Sites瀏覽器中執行搜尋/篩選功能。 載入Analytics搜尋篩選器，以符合對應的自訂分析欄。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>上次修改的資產 </td>
   <td>上次修改資產的日期。<br /> </td>
   <td>根據「日期述詞」的自訂述詞。</td>
  </tr>
  <tr>
   <td>元件 </td>
   <td>可讓作者搜尋/篩選含有特定元件的頁面。 例如影像庫。<br /> </td>
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
   <td>根據日期屬性，以滑桿式方式搜尋資產。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期範圍 </td>
   <td>搜尋日期屬性在指定範圍內建立的資產。 在「搜尋」面板中，您可以指定「開始」和「結束」日期。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>範圍文本（從）*</li>
     <li>範圍文本（至）*</li>
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
   <td>隱藏的篩選器</td>
   <td>屬性和值的篩選器，使用者看不到。</td>
   <td>
    <ul>
     <li>屬性名稱</li>
     <li>屬性值</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>選項 </td>
   <td><p>選項是使用者建立的內容節點。</p> <p>請參閱 <a href="#addinganoptionspredicate">新增選項述詞</a> 以取得更多資訊。</p> </td>
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
   <td>根據頁面的狀態來搜尋頁面。</td>
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
     <li>添加搜索路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>屬性 </td>
   <td>在指定的屬性上搜索。</td>
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
   <td>資產的特定搜尋述詞，與常見的滑桿述詞相同。 因為回溯相容問題，仍可供使用。</td>
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
   <td>根據資產的評等來搜尋資產。<br /> </td>
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
   <td>使用滑桿功能擴充範圍述詞的通用搜尋述詞。 所搜尋屬性的值必須介於滑桿限制之間。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標記 </td>
   <td>根據標籤搜尋資產。 您可以設定「路徑」屬性，以填入「標籤」清單中的各種標籤。</td>
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
>* 常見的搜尋述詞定義於：
   >  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>* 僅與網站管理員（傳統UI）相關的搜尋述詞位於：
   >  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
   >   * 這些規則已過時，且僅適用於回溯相容性。
>
>此資訊僅供參考，您不得變更 `/libs`.

### 謂詞設定 {#predicate-settings}

根據謂語，選擇的設定可用於配置：

* **欄位標籤**

   將顯示為可折疊標題或謂語欄位標籤的標籤。

* **說明**

   使用者的描述性詳細資訊。

* **預留位置**

   空文本或謂語的位置保持符，以防未輸入篩選文本。

* **屬性名稱**

   要搜尋的屬性。 它會使用相對路徑和萬用字元 `*/*/*` 指定相對於 `jcr:content` 節點（每個星號代表一個節點級別）。

   如果您只想在具有 `x` 屬性 `jcr:content` 節點使用 `*/jcr:content/x`

* **屬性深度**

   在資源內搜尋該屬性的最大深度。 因此，可以對資源和遞歸子項執行對該屬性的搜索，直到子項的級別等於指定深度為止。

* **屬性值**

   屬性值作為絕對字串或作為表達式語言；例如， `cq:Page` 或

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **範圍文字**

   範圍欄位在 **日期範圍** 謂語。

* **選項路徑**

   用戶可以使用謂詞設定頁簽中的路徑瀏覽器選擇路徑。 選取 **+** 表徵圖用於將所選內容添加到有效選項清單(然後 **-** 圖示以移除（如果需要）。

   這些選項是用戶建立的內容節點，具有以下結構：

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **選項節點路徑**
實際上與 
**選項路徑**，只有此欄位在通用述詞欄位中，而另一個欄位是資產專屬欄位。

* **單選**
如果選中，則選項將呈現為僅允許單個選擇的複選框。 如果錯誤選取，則可取消選取核取方塊。

* **發佈和即時副本屬性名稱**
Sites特定述詞的發佈和即時副本核取方塊標籤。

* &amp;ast;在 **設定** 標籤表示欄位為必填欄位，若保留為空白，則會顯示錯誤訊息

## 設定您的搜尋Forms {#configuring-your-search-forms}

### 建立/開啟自訂設定 {#creating-opening-a-customized-configuration}

1. 導覽至 **工具**, **一般**, **搜尋Forms**.

1. 選取您要自訂的設定。
1. 使用 **編輯** 圖示以開啟要更新的設定。
1. 如果您想要新自訂 [新增謂語欄位並定義設定](#add-edit-a-predicate-field-and-define-field-settings) 視需要。 如果現有自訂，您可以選取現有欄位，並 [更新設定](#add-edit-a-predicate-field-and-define-field-settings).
1. 選擇 **完成** 以儲存設定。

   >[!NOTE]
   >
   >自訂設定會（視情況）儲存在：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### 新增/編輯述詞欄位和定義欄位設定 {#add-edit-a-predicate-field-and-define-field-settings}

您可以新增或編輯欄位，並定義/更新其設定：

1. [開啟自訂的設定](#creating-opening-a-customized-configuration) 以更新。
1. 如果要新增欄位，請開啟 **選擇謂詞** 標籤，並將所需謂語拖曳至所需位置。 例如， **日期範圍述詞**:

   ![chlimage_1-375](assets/chlimage_1-375.png)

1. 取決於：

   * 正在添加新欄位：

      新增述詞後， **設定** 標籤，並顯示可定義的屬性。

   * 要更新現有謂詞：

      選取謂語欄位（位於右側），然後開啟 **設定** 標籤。
   例如， **日期範圍述詞**:

   ![chlimage_1-376](assets/chlimage_1-376.png)

1. 視需要進行變更，並使用確認 **完成**.

### 預覽搜尋設定 {#previewing-the-search-configuration}

1. 選取「預覽」圖示：

   ![](do-not-localize/chlimage_1-31.png)

1. 這樣，在適當控制台的「搜尋」欄中，搜尋表單就會顯示為（完全展開）。

   ![chlimage_1-377](assets/chlimage_1-377.png)

1. **關閉** 預覽，返回並完成配置。

### 刪除謂詞欄位 {#deleting-a-predicate-field}

1. [開啟自訂的設定](#creating-opening-a-customized-configuration) 以更新。
1. 選取謂語欄位（位於右側），開啟 **設定** 標籤，然後選取 **刪除** 圖示（左下）。

   ![](do-not-localize/chlimage_1-32.png)

1. 對話方塊會要求確認刪除動作。

1. 確認此項目，以及使用 **完成**.

### 刪除配置（恢復預設值） {#deleting-a-configuration-to-reinstate-the-default}

自訂設定後，這將覆寫預設值。 您可以刪除自訂設定，以重新設定預設設定。

>[!NOTE]
>
>您無法刪除任一預設配置。

從主控台刪除自訂設定：

1. 選取所需的設定(例如 **頁面編輯器（段落搜尋）**)，然後 **刪除** 圖示：

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 將刪除自定義配置並恢復預設配置（這由控制台中的掛鎖符號的再現指示）。

### 添加選項謂語 {#adding-options-predicates}

選項謂語（選項、選項屬性）可讓您設定要搜尋的項目。 它們通常用於直接在頁面下方搜尋內容；例如，頁面節點上的屬性。

以下範例（根據用來建立頁面的範本進行搜尋）說明了相關步驟：

1. 建立定義要搜索的屬性的節點。

   您需要一個根節點，其中包含使用者可使用的個別選項定義。

   個別選項的節點需要屬性：

   * `jcr:title`  — 要在搜尋邊欄中顯示的欄位標籤
   * `value`  — 要搜尋的屬性值

   ![chlimage_1-379](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >您 ***必須*** 不會變更 `/libs` 路徑。
   >
   >這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
   >
   >設定和其他變更的建議方法為：
   >
   >1. 重新建立所需項目，因為它存在於 `/libs`，在 `/apps`. 在此案例中，來源為：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在內進行任何變更 `/apps.`


1. 開啟 **搜尋Forms** 主控台，然後選取您要更新的設定。 例如， **網站管理員搜尋邊欄**.

   然後按一下/點選 **編輯搜索表單** 表徵圖。

1. 視設定而定，新增 **選項** 或 **選項屬性** 至設定。
1. 更新欄位，尤其是：

   * **屬性名稱**

      在目標節點上指定要搜索的節點屬性。 例如：

      `jcr:content/cq:template`

   * **選項節點路徑**

      選取保留選項的路徑。 例如：

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![chlimage_1-380](assets/chlimage_1-380.png)

1. 選擇 **完成** 以儲存您的設定。
1. 導覽至適當的主控台(在此範例中， **網站**)並開啟 **搜尋** 欄。 新定義的搜尋表單以及各種選項將會顯示。 選擇查看搜索結果所需的選項：

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
   <td>讀取、寫入 <code>/apps </code>節點。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td>讀取、寫入、刪除 <code>/apps</code> 節點</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td>讀取、寫入、刪除 <code>/var/dam/content</code> 節點。<br /> 讀取、寫入 <code>/apps</code> 節點。</td>
  </tr>
 </tbody>
</table>
