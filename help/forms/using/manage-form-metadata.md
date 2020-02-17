---
title: 管理表單中繼資料
seo-title: 管理表單中繼資料
description: 中繼資料可讓資產分類和組織更輕鬆，並協助尋找特定資產的使用者。
seo-description: 中繼資料可讓資產分類和組織更輕鬆，並協助尋找特定資產的使用者。
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# 管理表單中繼資料{#manage-form-metadata}

## 概覽  {#overview-nbsp}

中繼資料可讓資產分類和組織更輕鬆，並協助尋找特定資產的使用者。

依預設，AEM Forms會為每個資產類型提供一組已定義的中繼資料。 除了預設中繼資料，您還可以將自訂中繼資料新增至每個資產類型。 AEM Forms也提供您適當的方式，讓您有效率地建立、管理和交換表單的所有中繼資料。

如果您是開發人員或網站擁有者，您可以自訂Forms Portal（AEM Forms的使用者介面），以反映您在組織中使用的中繼資料。 如需表單入口網站的詳細資訊，請參 [閱在入口網站上發佈表單的簡介](../../forms/using/introduction-publishing-forms.md)。

## AEM Forms中的中繼資料 {#metadata-in-aem-forms}

在AEM Forms中，與資產相關聯的中繼資料屬性清單會視其類型而定。 此外，如果您新增任何自訂中繼資料屬性，則會將其新增至新增自訂中繼資料之類型的所有資產。

### Asset types {#asset-types}

AEM Forms支援下列資產類型：

* 表單範本（XFA表單）
* PDF表格
* 檔案（平面PDF）
* 最適化表單
* 資源
* XFS

#### 中繼資料的詳盡清單 {#extensive-list-of-metadata}

以下是AEM Forms支援的中繼資料屬性詳細清單：

<table>
 <tbody> 
  <tr> 
   <td><strong>屬性名稱</strong></td> 
   <td><strong>資產類型</strong></td> 
   <td><strong>說明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>標題</td> 
   <td>除資源外的所有</td> 
   <td>表單的顯示名稱。<br /> </td> 
  </tr> 
  <tr> 
   <td>說明</td> 
   <td>除資源外的所有</td> 
   <td>表單的說明。 使用者可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>類型</td> 
   <td>全部</td> 
   <td><p>指定資產類型的唯讀值。 它可以具有以下值之一：</p> 
    <ul> 
     <li>表單範本</li> 
     <li>PDF表單、PDF表單(Acroform)或PDF表單（簽名）</li> 
     <li>檔案、檔案（已簽署）</li> 
     <li>調適性表單</li> 
     <li>資源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>建立日期</td> 
   <td>全部</td> 
   <td>指定資產建立時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>全部</td> 
   <td>指定資產上次修改時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>作者</td> 
   <td>除資源外的所有</td> 
   <td><p>根據表單類型自動計算的唯讀值。</p> 
    <ul> 
     <li>PDF/表單範本／檔案——從已上傳的二進位檔案擷取。</li> 
     <li>最適化表單——在建立表單時登入使用者。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>狀態</td> 
   <td>除資源外的所有</td> 
   <td><p> 定義表單下列狀態之一的只讀值：</p> 
    <ul> 
     <li>無值：如果表單從未發佈過。</li> 
     <li>已發佈：發佈表單時。</li> 
     <li>已修改：在發佈表單後修改表單的時間。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次發佈日期</td> 
   <td>除資源外的所有</td> 
   <td>指定表單上次發佈時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>發佈開／關時間</td> 
   <td>除資源外的所有</td> 
   <td><p>排程表單自動發佈／取消發佈的時間。 使用者在編輯中繼資料時設定此值。</p> 
    <ul> 
     <li>「發佈開啟」和「關閉」時間都應超過目前日期。 </li> 
     <li>「發佈關閉」時間應超過「發佈開啟」時間。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表單範本</p> <p>PDF表格</p> </td> 
   <td><p>若要設定使用者指定的URL，以便將表單資料送出至servlet。</p> <p>可使用下列任何方法來設定提交URL，依優先順序列出：</p> 
    <ul> 
     <li>在AEM Forms Designer中建立XFA表單時，使用「HTTP提交」按鈕，直接在「表單範本」中指定提交URL。</li> 
     <li>在AEM Forms UI中，選取表單並指定在編輯中繼資料屬性時的送出URL。</li> 
     <li>在Forms Portal中，編輯Search &amp; Lister元件，並在「Form Link」（表單連結）標籤下指定送出URL。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML演算描述檔</td> 
   <td>表單範本</td> 
   <td>以HTML格式呈現表單範本時使用的HTML呈現描述檔。</td> 
  </tr> 
  <tr> 
   <td>演算格式</td> 
   <td><p>表單範本</p> <p>調適性表單</p> </td> 
   <td><p>此選項允許用戶在發佈表單時指定表單的渲染格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>兩者</li> 
    </ul> <p>此選項僅用於限制表單入口網站（一般使用者可看到表單）的轉譯格式。</p> </td> 
  </tr> 
  <tr> 
   <td>標記</td> 
   <td>除資源外的所有</td> 
   <td>與表單關聯的標籤可協助快速且輕鬆地搜尋。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>調適性表單</p> <p>表單範本</p> <p>資源</p> </td> 
   <td><p>此表單相關的資產（其他表單或資源）清單。 這些資產可分為下列兩類：</p> 
    <ul> 
     <li>參考：目前表單所參照的資產。</li> 
     <li>轉介者：指流動資產之資產。</li> 
    </ul> <p>這些資產會顯示為連結，而且按一下即可直接存取其中繼資料。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表單模型(XDP/XSD)選擇</td> 
   <td>調適性表單</td> 
   <td><p>指定在編寫最適化表單時使用的表單模型。 此屬性可以有下列值：</p> 
    <ul> 
     <li>表單範本：從儲存庫中現有的表單模板中選擇一個表單模板。 此值可以更新。</li> 
     <li>XML架構：XSD檔案已上傳。 此值可以更新。</li> 
     <li>無</li> 
    </ul> 
    <div>
      選取表單模型後，即可更新但無法移除。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 檢視表單中繼資料 {#view-form-metadata}

資產具有現有的屬性值，可在唯讀模式中檢視。 此中繼資料是在表單上傳或表單建立時產生。

1. 導覽至您要檢視中繼資料的資產所在位置。

1. 使用下列其中一種方式開啟屬性頁面：

   1. 按一下「快速操 ![作」(Quick Actions)中的「查看屬性」(View Properties)e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) （View屬性e_reviewmode_properties_n）表徵圖。

      >[!NOTE]
      >
      >「快速動作」是滑鼠暫留時在縮圖上顯示的動作項目。

   1. 選擇該表單，然後按一下工 ![具欄中顯示的「查看屬性」(View Properties)e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) 表徵圖。
   1. 在未處於選擇模式時，按一下表格縮圖，導覽至表格詳細資訊頁面。 現在，按一 ![下右上方的aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) eye圖示，然後按一下其下方清單中的「屬性」。

1. 開啟的屬性頁面會顯示僅包含含有某些值之中繼資料屬性的架構。

   屬性頁面有一個工具列，包含兩個動作圖示：

   * 編輯： ![aem6forms_edit](assets/aem6forms_edit.png) 編輯中繼資料屬性值
   * 檢視： ![aem6forms_eye_viewon導覽至表單詳細資訊頁面](assets/aem6forms_eye_viewon.png) ，此頁面會在預覽模式中開啟表單。
   內容部分分為兩部分：

   * 左側面板包含表格的縮圖
   * 右側面板包含唯讀模式下的中繼資料屬性，散布在各種標籤上。


## 新增／更新表單中繼資料值 {#add-update-form-metadata-values}

您可以編輯現有中繼資料屬性的值，或將新值新增至現有中繼資料屬性欄位（例如，中繼資料欄位空白時）。

### 更新中繼資料屬性值 {#update-metadata-property-values}

1. 請依照上一節中提及的步驟，開啟屬性頁面，供您檢視選取表單的現有中繼資料。

1. 在工具列中，按一下編 ![輯圖示aem6forms_edit](assets/aem6forms_edit.png) ，將頁面模式從唯讀變更為讀／寫。

1. 開啟的屬性頁面會包含混合有可編輯輸入欄位和靜態文字的架構。

1. 靜態文本中顯示的屬性是您無法編輯的屬性。

1. 您可以導覽至其他標籤，以尋找置入其下方之中繼資料屬性的輸入欄位。

   此頁面有一個工具列，包含兩個與檢視模式不同的動作圖示：

   * 取消： ![aem6forms_close](assets/aem6forms_close.svg_w24.png) 取消目前對中繼資料屬性值所做的任何變更
   * 完成： ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values to save
   這兩個動作都會引導使用者返回包含更新值之屬性頁面的唯讀模式。

### 更新表格縮圖 {#update-the-form-thumbnail}

屬性頁面的左側面板會顯示表單的縮圖。 依預設，顯示的縮圖是在建立表單（最適化表單）時或表單上傳時產生的縮圖。

對於所有表單類型，您可以選擇按一下「上傳影像 **** 」並從本機目錄瀏覽影像檔案，以上傳影像。 選取的影像會當做縮圖使用，而非預設影像。

對於最適化表單，提供了附加功能，其允許用戶生成縮略圖作為當前最適化表單預覽的快照。 由於AEM Forms也支援製作最適化表單，因此每當您變更最適化表單時，最適化表單的預覽可能會變更。 產生縮圖的這項功能可協助您根據目前的預覽狀態，取得最適化表單的全新縮圖。 按一 **[!UICONTROL 下「產生預覽]** 」以執行此動作。

>[!NOTE]
>
>* 使用縮圖的正方形影像。 當您使用非正方形影像並在清單檢視中檢視縮圖時，縮圖會出現剪裁。
>* 一旦上傳或產生新影像後，縮圖就會由此影像取代，而且無法重設為上一個影像。
>



## 新增自訂中繼資料 {#add-custom-metadata}

除了現成可用的中繼資料外，AEM Forms還支援新的自訂中繼資料。

提供了一種工具（元資料模式編輯器）來定義元資料佈局的模式；即表單的「屬性」頁面中顯 **[!UICONTROL 示內容]** 的佈局。 中繼資料結構編輯器可讓您新增或修改資產的自訂結構。

AEM Forms會在此工具中公開支援表單類型的中繼資料結構描述。 這樣，您可以訪問這些架構，並使用元資料架構編輯器中提供的功能添加自定義屬性。

### 導覽中繼資料結構編輯器 {#navigate-the-metadata-schema-editor}

1. 導覽至「 **[!UICONTROL 工具>資產>中繼資料結構]**」。

1. 從列 **[!UICONTROL 出的架構]** 表單按一下表單。

1. 從開啟的清單中，按一下您要新增自訂中繼資料的資產類型。

   >[!NOTE]
   >
   >這些結構包含立即提供的中繼資料屬性，且不得變更／編輯（選取核取方塊並從工具列按一下編輯），以避免功能問題。

1. 所點按的任何資產類型都會開啟包含選項的 `extendedmetadata` 清單。 編輯此架構。

1. 選取旁邊的核取 `extendedmetadata` 方塊，然後按一 ![下工具列中顯示的編輯aem6forms_edit](assets/aem6forms_edit.png) 圖示。

1. AEM Forms會開啟選取資產類型的中繼資料架構編輯器／表單產生器（在此例中為最適化表單）。

   ![最適化表單類型的中繼資料架構編輯器](assets/metadata-schema-editor-for-adaptive-form-type.png)

   中繼資料編輯器

   1. 左側面板包含標籤式區段，欄位放置在此區段中，右側面板會顯示所有可用的UI元件，以及從左側面板選取欄位的屬性。

   1. 鎖定的部分不可編輯，並包含框外提供的所有元資料屬性的欄位。

   1. 您可以按一下+符號，以新增其他標籤。

   1. 通過將欄位元件從上的「生成表單」部分拖動到架構頁，可以添加所需類型的自 **[!UICONTROL 定義欄位]** 。
   1. 按一下該欄位後，可在「設定」( **[!UICONTROL Settings]** )部分下提供該欄位的規範。

### 在架構編輯器中新增自訂中繼資料屬性 {#add-custom-metadata-property-in-schema-editor}

1. 導覽至您要新增自訂屬性的標籤（現有或新）。

1. 將所需類型的元件從「建置表 **[!UICONTROL 單]** 」區段拖曳至左側面板，並放置在方便的位置。

   >[!NOTE]
   >
   >您無法移動鎖定的部分，但可以將元件放置在任何空格中。

1. 按一下您剛拖曳的元件。 在右側面板中開啟的「設定」索引標籤中，填入下列欄位的資訊：

   1. 指定欄位標籤，該欄位標籤將用作方案中欄位上方的顯示名稱(例如：部門)
   1. 在「對應至屬性」欄位下，您可以看到預先填入的 **值&#39;。/jcr:content/metadata/default&#39;**。 將「**default**」變更為所要的屬性名稱，用來將屬性儲存在crx儲存庫中(例如：&#39;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >請勿變更首碼「」。/jcr:content/metadata/』，因為它定義了儲存屬性的路徑。
      >
      >此外，屬性名稱必須是唯一的，以避免在儲存庫中同一位置寫入兩個或更多屬性的值。 因此，建議您變更&#39;default&#39;值。

   1. 根據需求填寫其他設定。 例如：如果要將欄位設定為必填欄位，請選擇「必填」選項。
   1. 若要刪除您新增的欄位，請選取欄位，然後按一下刪除 ![刪除-1](assets/delete-1.png) 圖示。

1. 如有必要，請依照步驟1-3新增其他屬性。
1. 進行所 **有變更後** ，按一下「完成」。

   您已成功新增自訂中繼資料屬性。

AEM Forms中的所有最適化表單現在都包含此額外的中繼資料屬性。 您可以從屬性頁面編輯它。
