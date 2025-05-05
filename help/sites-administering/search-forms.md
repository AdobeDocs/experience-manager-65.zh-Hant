---
title: 設定搜尋表單
description: 瞭解如何使用搜尋Forms來自訂用於搜尋面板的搜尋述詞選擇，這些面板可在製作環境的AEM主控台和面板中使用。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 6%

---


# 設定搜尋表單{#configuring-search-forms}

使用&#x200B;**搜尋Forms**&#x200B;來自訂搜尋面板中所使用的搜尋述詞選擇，這些面板可用於各種AEM主控台及/或製作環境的面板。 自訂這些面板可讓搜尋功能根據您的特定需求而通用。

[範圍的述詞](#predicates-and-their-settings)是現成可用的。 您可以新增多個述詞，包括（其中包括）屬性述詞，以搜尋符合您指定之單一屬性的資產。 或者，使用「選項」述詞來搜尋符合您為特定屬性指定的一或多個值的資產。

您可以[設定用於各種主控台和資產瀏覽器（編輯頁面時）的搜尋表單](#configuring-your-search-forms)。 設定這些表單[&#128279;](#configuring-your-search-forms)的對話方塊可透過下列方式存取：

* **工具**

   * **一般**

      * **搜尋Forms**

第一次存取此主控台時，您可以看到所有組態都有掛鎖符號。 這表示適當的設定是預設（現成）設定，且無法刪除。 自訂組態之後，除非您[刪除自訂的組態](#deleting-a-configuration-to-reinstate-the-default)，否則鎖定會消失。 在這種情況下，會恢復預設值（和掛鎖指示器）。

![搜尋表單視窗](assets/chlimage_1-374.png)

## 設定 {#configurations}

可用的預設設定包括：

* **頁面編輯器（檔案搜尋）：**

  此設定會定義在資產瀏覽器中搜尋檔案時（編輯頁面時）可用的選項。

* **頁面編輯器（影像搜尋）：**

  此設定會定義在資產瀏覽器中搜尋影像時（編輯頁面時）可用的選項。

* **頁面編輯器（手稿搜尋）：**

  此設定會定義在資產瀏覽器中搜尋手稿時（編輯頁面時）可用的選項。

* **頁面編輯器（頁面搜尋）：**

  此設定會定義在資產瀏覽器中搜尋頁面時（編輯頁面時）可用的選項。

* **頁面編輯器（段落搜尋）：**

  此設定會定義在資產瀏覽器中搜尋段落時（編輯頁面時）可用的選項。

* **頁面編輯器（產品搜尋）：**

  此設定會定義在資產瀏覽器中搜尋產品時（編輯頁面時）可用的選項。

* **頁面編輯器(Dynamic Media Classic [先前為Scene7]搜尋)**：

  此設定會定義在資產瀏覽器中搜尋Scene7資源（編輯頁面時）時可用的選項。

* **網站管理搜尋邊欄**：

  此設定會定義使用者在使用Sites主控台的搜尋邊欄時可用的搜尋選項。

* **頁面編輯器（視訊搜尋）：**

  此設定會定義在資產瀏覽器中搜尋視訊時（編輯頁面時）可用的選項。

* **Assets管理搜尋邊欄：**

  此設定會定義使用者在使用Assets主控台時可用的搜尋選項。

* **目錄管理搜尋邊欄：**

  此設定會定義使用者在搜尋商務目錄時可使用的搜尋選項。

* **訂單管理搜尋邊欄：**

  此設定會定義使用者在搜尋商務訂單時可使用的搜尋選項。

* **產品集合管理搜尋邊欄：**

  此設定會定義使用者在搜尋商務產品集合時可用的搜尋選項。

* **產品管理搜尋邊欄：**

  此設定會定義使用者在搜尋商務產品時可使用的搜尋選項。

* **專案管理搜尋邊欄：**

  此設定會定義使用者在搜尋專案時可使用的搜尋選項。

## 述詞及其設定 {#predicates-and-their-settings}

### 述詞 {#predicates}

視設定而定，以下述詞可供使用：

<table>
 <tbody>
  <tr>
   <th>述詞</th>
   <th>用途</th>
   <th>設定</th>
  </tr>
  <tr>
   <td>分析 </td>
   <td>顯示Analytics支援的資料時，提供Sites瀏覽器中的搜尋/篩選功能。 Analytics搜尋篩選器會載入以符合對應的自訂分析欄。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>上次修改的資產 </td>
   <td>上次修改資產的日期。<br /> </td>
   <td>根據日期述詞的自訂述詞。</td>
  </tr>
  <tr>
   <td>元件 </td>
   <td>允許作者搜尋/篩選上面有特定元件的頁面。 例如，影像庫。<br /> </td>
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
   <td>根據日期屬性的資產滑桿式搜尋。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期範圍 </td>
   <td>在指定範圍內為日期屬性搜尋建立的資產。 在「搜尋」面板中，您可以指定「開始」和「結束」日期。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>預留位置</li>
     <li>屬性名稱*</li>
     <li>範圍文字（從）*</li>
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
   <td>根據資產的大小來搜尋資產。</td>
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
   <td><p>選項是使用者建立的內容節點。</p> <p>如需詳細資訊，請參閱<a href="#addinganoptionspredicate">新增選項述詞</a>。</p> </td>
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
     <li>新增搜尋路徑</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>屬性 </td>
   <td>搜尋指定的屬性。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>Publish狀態 </td>
   <td>根據資產的發佈狀態來搜尋資產</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範圍 </td>
   <td>搜尋指定範圍內的資源。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>範圍選項 </td>
   <td>Assets的特定搜尋述詞，與常見的滑桿述詞相同。 由於回溯相容性問題，仍可使用。</td>
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
   <td>根據資產的評等搜尋資產。<br /> </td>
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
   <td>根據資產的建立相對日期搜尋資產<br /> </td>
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
   <td>使用滑桿功能擴充範圍述詞的常見搜尋述詞。 搜尋的屬性值必須介於滑桿限制之間。</td>
   <td>
    <ul>
     <li>欄位標籤</li>
     <li>屬性名稱*</li>
     <li>說明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標記 </td>
   <td>根據標籤搜尋資產。 您可以設定Path屬性以填入Tags清單中的各種標籤。</td>
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
>* 僅與Siteadmin （傳統UI）相關的搜尋述詞位於以下位置：
>  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * 這些功能已過時，僅供回溯相容性使用。
>
>此資訊僅供參考。 請勿變更`/libs`。

### 述詞設定 {#predicate-settings}

視述詞而定，以下是可用於設定的設定選擇：

* **欄位標籤**

  顯示為可摺疊標題或述詞欄位標籤的標籤。

* **說明**

  使用者的描述性詳細資料。

* **預留位置**

  空白文字或述詞的預留位置（若未輸入篩選文字）。

* **屬性名稱**

  要搜尋的屬性。 它使用相對路徑，萬用字元`*/*/*`指定相對於`jcr:content`節點的屬性深度（每個星號代表一個節點層級）。

  如果您只想在`jcr:content`節點上具有`x`屬性的資源之第一層子節點上搜尋，請使用`*/jcr:content/x`

* **屬性深度**

  在資源中搜尋該屬性的最大深度。 因此，可針對資源及遞回子項執行該屬性的搜尋，直到子項的層級等於指定的深度為止。

* **屬性值**

  屬性值做為絕對字串或做為運算式語言；例如，`cq:Page`或

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **範圍文字**

  **日期範圍**&#x200B;述詞中範圍欄位的標籤。

* **選項路徑**

  使用者可以使用述詞設定索引標籤中的路徑瀏覽器來選取路徑。 選取&#x200B;**+**&#x200B;後，圖示會用來將選取專案新增至有效選項清單（如有必要，接著會移除&#x200B;**-**&#x200B;圖示）。

  選項是使用者建立的內容節點，結構如下：

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **選項節點路徑**
實際上與&#x200B;**選項路徑**&#x200B;相同，只有這個在通用述詞欄位中，其他則專用於資產。

* **單選**
如果勾選，選項會呈現為僅允許單一選取的核取方塊。 如果錯誤地選取了，則可取消選取核取方塊。

* **Publish和即時副本屬性名稱**
網站特定述詞的發佈和即時副本核取方塊的標籤。

* **設定**&#x200B;索引標籤中欄位標籤上的&amp;amp；ast；表示欄位為必填，若保留為空白，則會出現錯誤訊息。

## 設定搜尋Forms {#configuring-your-search-forms}

### 建立/開啟自訂組態 {#creating-opening-a-customized-configuration}

1. 導覽至&#x200B;**工具** >> **一般** >> **搜尋Forms**。

1. 選取您要自訂的設定。
1. 使用&#x200B;**編輯**&#x200B;圖示開啟設定以進行更新。
1. 若是新的自訂，您可能要[新增述詞欄位，並視需要定義設定](#add-edit-a-predicate-field-and-define-field-settings)。 如果已有自訂，您可以選取現有欄位並[更新設定](#add-edit-a-predicate-field-and-define-field-settings)。
1. 選取&#x200B;**完成**&#x200B;以儲存組態。

   >[!NOTE]
   >
   >自訂組態會視情況儲存在：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### 新增/編輯述詞欄位和定義欄位設定 {#add-edit-a-predicate-field-and-define-field-settings}

您可以新增或編輯欄位，並定義/更新其設定：

1. [開啟自訂的設定](#creating-opening-a-customized-configuration)以進行更新。
1. 如果您想要新增欄位，請開啟&#x200B;**選取述詞**&#x200B;索引標籤，並將必要的述詞拖曳到必要的位置。 例如，**日期範圍述詞**：

   ![編輯搜尋表單](assets/chlimage_1-375.png)

1. 視以下專案而定：

   * 您正在新增欄位：

     新增述詞之後，**設定**&#x200B;索引標籤會開啟，並顯示可定義的屬性。

   * 您要更新現有的述詞：

     選取述詞欄位（在右側），然後開啟&#x200B;**設定**&#x200B;標籤。

   例如，**日期範圍述詞**&#x200B;的設定：

   日期範圍述詞![&#128279;](assets/chlimage_1-376.png)的屬性

1. 視需要進行變更，並透過&#x200B;**完成**&#x200B;確認。

### 預覽搜尋組態 {#previewing-the-search-configuration}

1. 選取預覽圖示：

   ![預覽搜尋表單](do-not-localize/chlimage_1-31.png)

1. 如此一來，搜尋表單就會顯示在適當主控台的「搜尋」欄中（完全展開）。

   ![預覽搜尋表單](assets/chlimage_1-377.png)

1. **關閉**&#x200B;預覽，讓您能夠返回並完成設定。

### 刪除述詞欄位 {#deleting-a-predicate-field}

1. [開啟自訂的設定](#creating-opening-a-customized-configuration)以進行更新。
1. 選取述詞欄位（在右側），開啟&#x200B;**設定**&#x200B;標籤，然後選取&#x200B;**刪除**&#x200B;圖示（左下方）。

   ![「刪除」圖示](do-not-localize/chlimage_1-32.png)

1. 對話方塊會要求確認刪除動作。

1. 透過&#x200B;**完成**&#x200B;確認此變更及任何其他變更。

### 刪除組態（恢復預設值） {#deleting-a-configuration-to-reinstate-the-default}

自訂組態之後，這會覆寫預設值。 您可以刪除自訂的組態，以恢復預設組態。

>[!NOTE]
>
>您無法刪除任一預設組態。

從主控台刪除自訂設定完成：

1. 選取必要的設定(例如，**頁面編輯器（段落搜尋）**)，然後選取工具列中的&#x200B;**刪除**&#x200B;圖示：

   ![正在刪除表單](assets/chlimage_1-378.png)

1. 自訂的組態會遭到刪除，而預設值會恢復（由主控台中掛鎖符號的重新顯示所指示）。

### 新增選項述詞 {#adding-options-predicates}

選項述詞（選項、選項屬性）可讓您設定要搜尋的專案。 它們可用來搜尋頁面正下方的內容，例如頁面節點上的屬性。

以下範例（根據用來建立頁面的範本進行搜尋）說明了相關步驟：

1. 建立定義要搜尋之屬性的節點。

   您需要一個根節點，其中包含使用者可用的個別選項定義。

   個別選項的節點需要屬性：

   * `jcr:title` — 要在搜尋邊欄中顯示的欄位標籤
   * `value` — 要搜尋的屬性值

   ![在CRXDE中新增選項](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >請&#x200B;***不要***&#x200B;變更`/libs`路徑中的任何專案。
   >
   >這是因為下次升級執行個體時，`/libs`的內容會被覆寫（當您套用Hotfix或Feature Pack時，這些內容很可能會被覆寫）。
   >
   >設定和其他變更的建議方法是：
   >
   >1. 重新建立必要專案，因為它存在於`/libs`中的`/apps`下。 在此案例中，來自：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在`/apps.`中進行任何變更

1. 開啟&#x200B;**搜尋Forms**&#x200B;主控台，並選取您要更新的設定。 例如，**網站管理員搜尋邊欄**。

   然後按一下&#x200B;**編輯搜尋表單**&#x200B;圖示。

1. 視組態而定，將&#x200B;**Options**&#x200B;或&#x200B;**Options屬性**&#x200B;新增至組態。
1. 更新欄位，特別是：

   * **屬性名稱**

     指定要在目標節點上搜尋的節點屬性。 例如：

     `jcr:content/cq:template`

   * **選項節點路徑**

     選取保留選項的路徑。 例如：

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![正在新增屬性路徑](assets/chlimage_1-380.png)

1. 選取&#x200B;**完成**&#x200B;以儲存您的設定。
1. 導覽至適當的主控台（在此範例中為&#x200B;**Sites**）並開啟&#x200B;**搜尋**&#x200B;邊欄。 會顯示新定義的搜尋表單以及各種選項。 選取必要選項，即可檢視搜尋結果：

   ![最終結果](assets/chlimage_1-381.png)

## 使用者權限 {#user-permissions}

下表列出對搜尋表單執行編輯、刪除和預覽動作所需的許可權。

<table>
 <tbody>
  <tr>
   <td><strong>動作</strong></td>
   <td><strong>權限</strong></td>
  </tr>
  <tr>
   <td>編輯 </td>
   <td><code>/apps </code>節點的讀取、寫入許可權。</td>
  </tr>
  <tr>
   <td>刪除</td>
   <td><code>/apps</code>節點的讀取、寫入、刪除許可權</td>
  </tr>
  <tr>
   <td>預覽</td>
   <td><code>/var/dam/content</code>節點的讀取、寫入、刪除許可權。<code>/apps</code>節點上的<br />讀取、寫入許可權。</td>
  </tr>
 </tbody>
</table>
