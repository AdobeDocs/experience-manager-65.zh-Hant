---
title: 管理表單中繼資料
description: 中繼資料可讓您更輕鬆地分類及組織資產，並幫助尋找特定資產的使用者。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 2%

---

# 管理表單中繼資料{#manage-form-metadata}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/manage-form-metadata.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

## 概觀  {#overview-nbsp}

中繼資料可讓您更輕鬆地分類及組織資產，並幫助尋找特定資產的使用者。

依預設，AEM Forms會為每種資產型別提供一組已定義的中繼資料。 除了預設中繼資料外，您還可以新增自訂中繼資料至每個資產型別。 AEM Forms也提供正確的方法，讓您有效率地建立、管理和交換表單的所有這些中繼資料。

如果您是開發人員或網站擁有者，您可以自訂AEM Forms的一般使用者介面 — Forms Portal，以反映您在組織中使用的中繼資料。 如需Forms入口網站的詳細資訊，請參閱[在入口網站上發佈表單的簡介](../../forms/using/introduction-publishing-forms.md)。

## AEM Forms中的中繼資料 {#metadata-in-aem-forms}

在AEM Forms中，與資產相關聯的中繼資料屬性清單會依其型別而定。 此外，如果您新增任何自訂中繼資料屬性，則會將該屬性新增至新增自訂中繼資料所在型別的所有資產。

### 資產型別 {#asset-types}

AEM Forms支援下列資產型別：

* 表單範本（XFA表單）
* PDF forms
* 檔案(平面PDF)
* 調適型表單
* 資源
* XFS

#### 廣泛的中繼資料清單 {#extensive-list-of-metadata}

以下是AEM Forms支援的中繼資料屬性詳盡清單：

<table>
 <tbody> 
  <tr> 
   <td><strong>屬性名稱</strong></td> 
   <td><strong>資產類型</strong></td> 
   <td><strong>說明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>標題</td> 
   <td>除了資源以外的所有專案</td> 
   <td>表單的顯示名稱。<br /> </td> 
  </tr> 
  <tr> 
   <td>說明</td> 
   <td>除了資源以外的所有專案</td> 
   <td>表單說明。 使用者可以指定這個值。<br /> </td> 
  </tr> 
  <tr> 
   <td>類型</td> 
   <td>全部</td> 
   <td><p>指定資產型別的唯讀值。 它可以有下列其中一個值：</p> 
    <ul> 
     <li>表單範本</li> 
     <li>PDF表單、PDF表單(Acroform)或PDF表單（已簽署）</li> 
     <li>檔案，檔案（已簽署）</li> 
     <li>調適性表單</li> 
     <li>資源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>已建立</td> 
   <td>全部</td> 
   <td>指定資產建立時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>全部</td> 
   <td>指定上次修改資產時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>作者</td> 
   <td>除了資源以外的所有專案</td> 
   <td><p>根據表單型別自動計算的唯讀值。</p> 
    <ul> 
     <li>PDF/表單範本/檔案 — 從上傳的二進位檔案中擷取。</li> 
     <li>最適化表單 — 建立表單時登入的使用者。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>狀態</td> 
   <td>除了資源以外的所有專案</td> 
   <td><p> 唯讀值，定義表單的下列其中一種狀態：</p> 
    <ul> 
     <li>無值：如果表單未曾發佈。</li> 
     <li>已發佈：表單發佈時。</li> 
     <li>已修改：表單發佈一次後修改的時間。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次發佈日期</td> 
   <td>除了資源以外的所有專案</td> 
   <td>指定上次發佈表單時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>Publish開啟/關閉時間</td> 
   <td>除了資源以外的所有專案</td> 
   <td><p>排定自動發佈/取消發佈表單的時間。 使用者在編輯中繼資料時設定此值。</p> 
    <ul> 
     <li>Publish的開啟和關閉時間都應在目前日期以後。 </li> 
     <li>Publish關閉時間應在發佈開啟時間之後。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表單範本</p> <p>PDF表單</p> </td> 
   <td><p>設定使用者指定的URL以將表單資料提交至servlet。</p> <p>您可以使用下列任一方法來設定提交URL （依優先順序排列）：</p> 
    <ul> 
     <li>在AEM Forms Designer中建立XFA表單時，使用HTTP提交按鈕直接在表單範本中指定提交URL。</li> 
     <li>在AEM Forms UI中，選取表單並指定編輯中繼資料屬性時的提交URL。</li> 
     <li>在Forms入口網站中，編輯「搜尋並製表器」元件，並在「表單連結」索引標籤下指定提交URL。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML演算設定檔</td> 
   <td>表單範本</td> 
   <td>以HTML格式轉譯表單範本時使用的HTML轉譯器設定檔。</td> 
  </tr> 
  <tr> 
   <td>演算格式</td> 
   <td><p>表單範本</p> <p>調適性表單</p> </td> 
   <td><p>此選項可讓使用者在發佈表單時指定表單的轉譯格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>兩者</li> 
    </ul> <p>此選項僅用來限制一般使用者可在表單入口網站上看到的表單轉譯格式。</p> </td> 
  </tr> 
  <tr> 
   <td>標記</td> 
   <td>除了資源以外的所有專案</td> 
   <td>與表單關聯的標籤有助於快速輕鬆的搜尋。</td> 
  </tr> 
  <tr> 
   <td>參考</td> 
   <td><p>調適性表單</p> <p>表單範本</p> <p>資源</p> </td> 
   <td><p>與此表單相關的資產（其他表單或資源）清單。 這些資產可能分為以下兩個類別：</p> 
    <ul> 
     <li>參照：目前表單參照的Assets。</li> 
     <li>反向連結為：參考目前資產的Assets。</li> 
    </ul> <p>這些資產會顯示為連結，按一下這些連結即可直接存取其中繼資料。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表單模型(XDP/XSD)選擇</td> 
   <td>調適性表單</td> 
   <td><p>指定在製作最適化表單時使用的表單模型。 此屬性可以有下列值：</p> 
    <ul> 
     <li>表單範本：從存放庫中的現有表單範本中選取表單範本。 此值可更新。</li> 
     <li>XML結構描述：已上傳XSD檔案。 此值可更新。</li> 
     <li>無</li> 
    </ul> 
    <div>
      表單模型一旦選取便可以更新，但不能移除。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 檢視表單中繼資料 {#view-form-metadata}

Assets有現有的屬性值，可以在唯讀模式下檢視。 此中繼資料源自表單上傳或表單建立時。

1. 導覽至您要檢視中繼資料的資產位置。

1. 使用下列其中一種方式開啟屬性頁面：

   1. 按一下「快速動作」中的「檢視屬性」 ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png)。

      >[!NOTE]
      >
      >快速動作是指滑鼠懸停時縮圖上顯示的動作專案。

   1. 選取表單，然後按一下出現在工具列中的檢視屬性![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png)圖示。
   1. 不在選擇模式中時，按一下表單縮圖，導覽至表單詳細資訊頁面。 現在，請按一下右上角的![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png)眼睛圖示，然後按一下下方清單中的「屬性」。

1. 開啟的屬性頁面會顯示一個綱要，其中只包含那些儲存某些值的中繼資料屬性。

   屬性頁面有一個包含兩個動作圖示的工具列：

   * 編輯： ![aem6forms_edit](assets/aem6forms_edit.png)編輯中繼資料屬性值
   * 檢視： ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png)瀏覽至表單詳細資訊頁面，該頁面會在預覽模式下開啟表單。

   內容部分分為兩個部分：

   * 左側面板包含表單的縮圖
   * 右側面板包含唯讀模式的中繼資料屬性，並分佈於各種索引標籤中。

## 新增/更新表單中繼資料值 {#add-update-form-metadata-values}

您可以編輯現有中繼資料屬性的值，或將新值新增至現有中繼資料屬性欄位（例如，當中繼資料欄位空白時）。

### 更新中繼資料屬性值 {#update-metadata-property-values}

1. 依照上一節所述的步驟，開啟屬性頁面，您可在此檢視所選表單的現有中繼資料。

1. 在工具列中按一下編輯圖示![aem6forms_edit](assets/aem6forms_edit.png)，將頁面模式從唯讀變更為讀取/寫入。

1. 開啟的屬性頁面包含混合了可編輯輸入欄位和靜態文字的架構。

1. 靜態文字中顯示的屬性是您無法編輯的屬性。

1. 您可以導覽至其他標籤，以尋找置於其下的中繼資料屬性輸入欄位。

   此頁面有一個工具列，其中包含兩個與檢視模式不同的動作圖示：

   * 取消： ![aem6forms_close](assets/aem6forms_close.svg_w24.png)取消目前對中繼資料屬性值所做的任何變更
   * 完成： ![aem6forms_check](assets/aem6forms_check.png)儲存目前對中繼資料屬性值所做的所有變更

   這兩個動作都會將使用者引導回包含更新值之屬性頁面的唯讀模式。

### 更新表單縮圖 {#update-the-form-thumbnail}

屬性頁面中的左側面板會顯示表單的縮圖。 依預設，顯示的縮圖是建立表單（最適化表單）時或上傳表單時產生的縮圖。

對於所有表單型別，您可以選擇按一下&#x200B;**[!UICONTROL 上傳影像]**&#x200B;並從本機目錄瀏覽影像檔案，以上傳影像。 選取的影像會用作縮圖，而非預設的縮圖。

針對調適型表單，提供其他功能，可讓使用者產生縮圖，作為目前調適型表單預覽的快照。 由於AEM Forms也支援撰寫調適型表單，因此每次您變更調適型表單時，調適型表單的預覽可能會變更。 此功能可產生縮圖，協助您根據目前預覽狀態，為最適化表單取得新的縮圖。 按一下&#x200B;**[!UICONTROL 產生預覽]**&#x200B;以執行此動作。

>[!NOTE]
>
>* 縮圖使用正方形影像。 當您使用非正方形影像並在清單檢視中檢視縮圖時，縮圖會以裁剪方式顯示。
>* 上傳或產生新影像後，此影像會取代縮圖，且無法重設為上一個影像。
>

## 新增自訂中繼資料 {#add-custom-metadata}

除了現成可用的中繼資料外，AEM Forms也支援新的自訂中繼資料。

提供的工具（中繼資料結構編輯器）可定義中繼資料配置的結構描述；也就是顯示在表單的&#x200B;**[!UICONTROL 屬性]**&#x200B;頁面中的配置描述。 中繼資料結構編輯器可讓您新增或修改資產的自訂結構。

AEM Forms會公開此工具中支援之表單型別的中繼資料結構。 如此一來，您就可以存取這些結構描述，並使用中繼資料結構編輯器提供的功能來新增自訂屬性。

### 瀏覽中繼資料結構編輯器 {#navigate-the-metadata-schema-editor}

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets >中繼資料結構]**。

1. 從列出的結構表單中按一下&#x200B;**[!UICONTROL 表單]**。

1. 在開啟的清單中，按一下您要新增自訂中繼資料的資產型別。

   >[!NOTE]
   >
   >這些結構描述包含現成可用的中繼資料屬性，且不可變更/編輯（選取核取方塊並從工具列按一下「編輯」）以避免功能問題。

1. 任何按下的資產型別都會開啟包含`extendedmetadata`選項的清單。 編輯此結構描述。

1. 選取`extendedmetadata`旁的核取方塊，然後按一下工具列中顯示的編輯![aem6forms_edit](assets/aem6forms_edit.png)圖示。

1. AEM Forms會開啟所選資產型別的中繼資料結構編輯器/表單產生器（在此案例中為調適型表單）。

   最適化表單型別![&#128279;](assets/metadata-schema-editor-for-adaptive-form-type.png)的中繼資料結構描述編輯器

   中繼資料編輯器

   1. 左側面板包含放置欄位的標籤區段，右側面板顯示所有可用的UI元件和從左側面板中選取的欄位屬性。

   1. 鎖定的區段無法編輯，且包含現成提供的所有中繼資料屬性的欄位。

   1. 您可以按一下+符號來新增其他標籤。

   1. 您可以將欄位元件從&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖曳到結構描述頁面，以新增所需型別的自訂欄位。
   1. 按一下此欄位後，可在&#x200B;**[!UICONTROL 設定]**&#x200B;區段下提供此欄位的規格。

### 在結構描述編輯器中新增自訂中繼資料屬性 {#add-custom-metadata-property-in-schema-editor}

1. 導覽至您要新增自訂屬性的標籤（現有或新的）。

1. 將所需型別的元件從&#x200B;**[!UICONTROL 建置表單]**&#x200B;區段拖曳至左側面板，並放置在方便的位置。

   >[!NOTE]
   >
   >您無法移動鎖定的區段，但可以將元件置於任何空白處。

1. 按一下您剛才拖曳的元件。 在右側面板中開啟的「設定」標籤中，填寫下列欄位的資訊：

   1. 指定欄位標籤，在結構描述中的欄位上方做為顯示名稱（例如：Department）
   1. 在[對應至屬性]欄位下，您可以看到預填值&#x200B;**&#39;。/jcr：content/metadata/default&#39;**。 將&#39;**default**&#39;變更為所需的屬性名稱，用來儲存crx存放庫中的屬性(例如： &#39;。/jcr：content/metadata/department&#39;)

      >[!NOTE]
      >
      >請勿變更前置詞&#39;。/jcr：content/metadata/&#39;，定義儲存屬性的路徑。
      >
      >此外，屬性名稱必須是唯一的，以避免在存放庫的同一位置寫入兩個或更多屬性的值。 因此，建議您變更「預設」值。

   1. 根據需求填寫其他設定。 例如：如果您要將欄位設為必要欄位，請選取必要選項。
   1. 若要刪除您新增的欄位，請選取該欄位，然後按一下刪除![delete-1](assets/delete-1.png)圖示。

1. 如有必要，請依照步驟1至3新增其他屬性。
1. 完成所有變更後，按一下&#x200B;**完成**。

   您已成功新增自訂中繼資料屬性。

AEM Forms中的所有調適型表單現在包含此額外的中繼資料屬性。 您可以從屬性頁面進行編輯。
