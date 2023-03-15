---
title: 表單集於AEM Forms
seo-title: Form set in AEM Forms
description: 本文介紹表單集，並說明如何透過將表單HTML5來建立表單集。 本文還說明如何將xml資料預填到表單集，以及如何在流程管理中使用表單集。
seo-description: This article introduces form set and explains how to create form sets by stitching together HTML5 forms. This article also explains how you can prefill xml data to a form set and how you can use form sets in process management.
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
feature: Mobile Forms
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2814'
ht-degree: 0%

---

# 表單集於AEM Forms{#form-set-in-aem-forms}

## 概觀 {#overview}

客戶通常需要提交多份表單才能申請服務或福利。 它涉及尋找所有相關表格；分別填寫、提交和追蹤。 此外，他們必須在各個表單中多次填寫常見詳細資訊。 若整個程式涉及大量表單，則會變得繁瑣且容易出錯。 AEM Forms的表單集功能有助於簡化這類案例的使用者體驗。

表單集是HTML5份表單的集合，這些表單分組在一起，並以單一表單集的形式向使用者呈現。 當最終用戶開始填寫表單集時，他們將從一個表單無縫轉換到另一個表單。 最後，只需按一下即可提交所有表單。

AEM Forms為表單作者提供直覺式的使用者介面，以建立、設定和管理表單集。 身為作者，您可以依照您希望使用者遵循的特定順序來排序表單。 此外，您也可以對個別表單套用條件或資格運算式，以根據使用者輸入控制其可見度。 例如，您可以將配偶詳細資訊表設定為只有在婚姻狀態指定為「已婚」時才顯示。

此外，您可以配置不同表單中的公用欄位，以共用通用資料綁定。 在適當的資料綁定到位後，最終用戶只需在後續表單中自動填寫公共資訊時填寫。

AEM Forms應用程式也支援表單集，讓您的現場員工能夠離線建立表單集、造訪客戶、輸入資料，並稍後與AEM Forms伺服器同步，以便將表單資料提交至業務流程。

## 建立和管理表單集 {#creating-and-managing-form-set}

您可以將使用設計工具建立的多個XDP或表單範本關聯至表單集。 然後，可以使用表單集根據用戶在初始表單中輸入的值及其配置檔案有選擇地呈現XDP。

使用 [AEM Forms使用者介面](../../forms/using/introduction-managing-forms.md) 管理所有表單、表單集和相關資產。

### 建立表單集 {#create-a-form-set}

要建立表單集，請執行以下操作：

1. 選取「Forms > Forms和檔案」。
1. 選擇「建立」>「表單集」。

1. 在「添加屬性」頁中，添加以下詳細資訊並按一下「下一步」。

   * 標題：指定文檔的標題。 標題可協助您識別AEM Forms使用者介面中設定的表單。
   * 說明：指定有關文檔的詳細資訊。
   * 標籤：指定用以唯一識別表單集的標籤。 標籤有助於搜尋表單集。 若要建立標籤，請在「標籤」方塊中輸入新的標籤名稱。
   * 提交URL:指定針對表單集的獨立轉譯(非AEM Forms應用程式使用案例)，張貼已提交資料的URL。 資料會以多部分/表單資料的形式提交至此端點，並包含下列請求參數：
   * dataXML:此參數包含已提交表單集資料的XML表示法。 如果表單集中的所有表單都使用通用架構，則會根據該架構生成XML。 否則，XML根標籤將包含表單集中每個已填寫表單的子標籤，該表單集包含表單附件的資料。
   * formsetPath:已提交的CRXDE中表單集的路徑。
   * HTML呈現配置檔案：您可以配置某些選項，如浮動欄位、附件和草稿支援（適用於獨立表單集轉譯），以自訂表單集的外觀、行為和互動。 您可以自訂或擴充現有的設定檔，以變更任何HTML表單設定檔設定。

   ![表單集：新增屬性](assets/createformset1.png)

1. 「選取表單」畫面會顯示可用的XDP表單或XDP檔案。 搜尋並選取要納入表單集的表單，然後按一下「新增至表單集」 。 如有必要，請再次搜尋要新增的表單。 將所有表單添加到表單集後，按一下「下一步」。

   >[!NOTE]
   >
   >請確定XDP表單中的欄位名稱不包含點字元。 否則，任何嘗試解析具有點字元的欄位的指令碼都無法解析這些欄位。

1. 在「配置表單」頁中，您可以執行以下操作：

   * 表單順序：拖放表單以重新排序。 表單順序會定義在AEM Forms應用程式中向使用者顯示表單的順序，以及獨立轉譯。
   * 表單識別碼：為要在適用性運算式中使用的表單指定唯一的標識。
   * 資料根：對於表單集中的每個表單，作者可以設定XPATH，將特定表單的資料放在已提交XML中。 依預設，值為/。 如果表單集中的所有表單都是架構綁定，並且共用相同的XML架構，則可以更改此值。 建議表單中的每個欄位在XDP中指定適當的資料系結。 如果兩個不同表單中的兩個欄位共用共同的資料系結，則第二個表單中的欄位會顯示第一個表單的預先填入值。 請勿將具有相同內部內容的兩個子表單綁定到相同的XML節點。 有關表單集的XML結構的詳細資訊，請參見 [為表單集預填XML](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * 適用性運算式：指定會評估布林值的JavaScript運算式，並指出表單集中的表單是否符合填寫條件。 若為false，系統不會要求使用者，甚至會顯示要填入的表單。 運算式通常以此表單之前擷取之欄位的值為基礎。 運算式也包含對表單集API fs.valueOf的呼叫，以擷取使用者在表單集欄位中填入的值：

   *fs.valueOf(&lt;form identifier=&quot;&quot;>, &lt;fieldsom expression=&quot;&quot;>)> &lt;value>*

   例如，如果表單集中有兩個表單：業務費用和差旅費用，您可以在「適用性表達式」欄位中為這兩種表單添加JavaScript代碼段，以檢查用戶在表單中的費用類型輸入。 如果用戶選擇「業務費用」，則「業務費用」表單將呈現給最終用戶。 或者，如果用戶選擇差旅費，則會向最終用戶呈現不同的表單。 如需詳細資訊，請參閱適用性運算式。

   此外，作者也可以選擇使用每列右角出現的「刪除」圖示，從表單集中移除表單，或使用「**+**「 」表徵圖。 此「**+**「 」表徵圖將用戶引導回嚮導中用於「選擇表單」的上一步。 現有選擇將保持不變，並且必須使用該頁上的「添加到表單集」表徵圖將進行的任何其他選擇添加到表單集中。

   ![表單集：配置表單](assets/createformset2.png)

   >[!NOTE]
   >
   >表單集中使用的所有表單均由AEM Forms使用者介面管理。

### 管理表單集 {#managing-a-form-set}

建立表單集後，您可以對該表單集執行下列動作：

* 按一下：當表單集建立並列在主要資產頁面上時，您可以按一下單一按一下表單集以加以檢視。 表單集隨即開啟，並顯示該表單集中的所有表單範本(XDP)。
* 編輯：在選取表單集後按一下「編輯」時，會開啟上方「建立表單集的步驟」中所示的「設定表單」畫面。 您可以執行此處說明的所有功能。
* 複製+貼上：這可讓您從一個位置複製整個表單集，並貼到相同或任何其他位置或資料夾。
* 下載：您可以下載表單集及其所有相依性。
* 開始/管理審閱：建立表單集後，按一下「開始審閱」即可設定其審閱。 表單集審核開始後，將向用戶顯示「管理審核」選項。 在「管理審閱」螢幕上，您可以更新/結束審閱。 對於您新增的審核，您可以檢查審核並添加註釋（如有必要）。
* 刪除：刪除完整的表單集。 已刪除表單集中的表單會保留在存放庫中。
* 發佈/取消發佈：這會發佈/取消發佈表單集，以及其包含的所有表單和這些表單的相關資產。
* 預覽：預覽提供兩個選項：預覽為HTML（無資料），並使用範例資料自訂預覽。
* 檢視/編輯屬性：您可以檢視/編輯所選表單集的中繼資料屬性。

![createformset3](assets/createformset3.png)

### 編輯表單集 {#edit-a-form-set}

要編輯表單集，請執行以下操作：

1. 選取「Forms > Forms和檔案」。
1. 找出您要編輯的表單集。 將滑鼠指標暫留在滑鼠指標上，然後選取「編輯」( ![編輯](assets/editicon.png))。
1. 在「配置表單」頁中，可以編輯以下內容：

   * 表單順序
   * 表單識別碼
   * 資料根
   * 適用性運算式

   您也可以按一下相關的「刪除」圖示，從表單集中刪除表單。

## 流程管理中的表單集 {#form-set-in-process-management}

使用AEM Forms管理使用者介面建立表單集後，您就可以使用Workbench在起始點或指派任務活動中使用表單集。

### 在任務或起始點中使用表單集 {#using-form-set-in-task-or-start-point}

1. 設計流程時，在「分配任務/起始點」的「演示和資料」部分下，選擇 **使用CRX資產**. CRX資產瀏覽器隨即顯示。

   ![設計流程：使用CRX資產](assets/formsetinprocessmgmt1.png)

1. 選取表單集以篩選AEM存放庫(CRX)中的表單集。

   ![設計流程：選取表單資產對話方塊](assets/formsetinprocessmgmt2.png)

1. 選擇表單集並按一下「確定」。

## 適用性運算式 {#eligibility-expressions}

表單集中的適用性運算式可用來定義並動態控制顯示給使用者的表單。 例如，只有在使用者屬於特定年齡群組時，才顯示特定表單。 使用Forms Manager指定和編輯適用性運算式。

適用性運算式可以是任何傳回布林值的有效JavaScript陳述式。 JavaScript程式碼片段中的最後一個陳述式會視為布林值，根據JavaScript程式碼片段其餘（前幾行）的處理，決定表單的適用性。 如果運算式的值為true，則表單符合向用戶顯示的條件。 這類表單稱為合格表單。

>[!NOTE]
>
>不會執行表單集中第一個表單的適用性運算式。 無論第一個表單的適用性表達式為何，都會一律顯示第一個表單。

除了標準JavaScript函式外，表單集還會公開fs.valueOf API，該API提供對表單集中表單欄位值的存取。 使用此API存取表單集中表單欄位的值。 API語法為fs.valueOf(formUid, fieldSOM)，其中：

* formUid（字串）:表單集中表單的唯一ID。 您可以在表單管理員使用者介面中建立表單集時指定。 依預設，這是表單名稱。
* fieldSOM（字串）:formUid所指定格式的欄位SOM運算式。 SOM表達式或指令碼對象模型表達式用於引用特定文檔對象模型(DOM)中的值、屬性和方法。 選取欄位時，您可以在「指令碼」標籤下的「表單設計器」中檢視它。

>[!NOTE]
>
>formUid和fieldSOM參數都必須是字串常值。

### 範例 {#examples}

API的有效用法：

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

API的使用無效：

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 為表單集預填XML {#prefill-xml-for-form-set}

表單集是多個HTML5個表單的集合，這些表單具有共同或不同的結構。 表單集支援使用XML檔案預填表單欄位。 您可以將XML檔案與表單集關聯，這樣，當您在表單集中開啟表單時，表單中的某些欄位就會被預先計算。

預填XML檔案是使用表單集URL的dataRef參數指定的。 dataRef參數指定與表單集合併的資料XML檔案的絕對路徑。

例如，您在表單集中有三個表單（form1、form2和form3），其結構如下：

form1

欄位

form2

欄位表單2欄位

form3

欄位表單3欄位

每個表單都有一個通用的命名欄位（名為「field」）和一個唯一命名的欄位(名為「formfield」)。

您可以使用具有以下結構的XML預填此表單集：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <field>common field value</field>
 <form1field>value1</form1field>
 <form2field>value2</form2field>
 <form3field>value3</form3field>
</formSetRootTag>
```

>[!NOTE]
>
>XML根標籤可以有任何名稱，但與欄位對應的元素標籤必須與欄位具有相同名稱。 XML的階層必須模擬表單的階層，這表示XML必須具有用於包裝子表單的對應標籤。

上述XML片段顯示為表單集預填的XML是個別表單預填的XML片段的聯合。 如果不同表單中的某些欄位資料階層/結構彼此類似，則欄位會預先填入相同的值。 在此範例中，所有三個表單都預先填入通用欄位&quot;field&quot;的相同值。 這是將資料從一種形式傳輸到另一種形式的簡單方式。 這也可透過將欄位系結至相同的架構或資料參考來達成。 如果您想要根據表單的結構來隔離表單集資料。 在建立表單集期間，您可以指定表單的「資料根」屬性（預設值為「/」，會對應至表單集根標籤），來達成此目的。

在上一個範例中，如果您指定資料根：&quot;/form1&quot;、&quot;/form2&quot;和&quot;/form3&quot;分別適用於三種表單，您需要使用以下結構的預填XML:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <form1>
  <field>field value1</field>
  <form1field>value1</form1field>
 </form1>
 <form2>
  <field>field value2</field>
  <form2field>value2</form2field>
 </form2>
 <form3>
  <field>field value3</field>
  <form3field>value3</form3field>
 </form3>
</formSetRootTag>
```

在表單集中，XML使用以下語法定義XML架構：

```xml
<formset>
 <fs_data>
  <xdp:xdp xmlns:xdp="https://ns.adobe.com/xdp/">
  <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
   <xfa:data>
   <rootElement>
    ... data ....
   </rootElement>
   </xfa:data>
  </xfa:datasets>
  </xdp:xdp>
 </fs_data>
 <fs_draft>
  ... private data...
 </fs_draft>
</formset>
```

>[!NOTE]
>
>如果有兩個表單具有重疊的資料根，或者一個表單的元素層次結構與另一個表單的資料根層次結構重疊，則在預填xml中，會合併重疊元素的值。 提交XML的結構與預填XML類似，但提交XML的包裝標籤較多，結尾附加了一些表單集上下文資料標籤。

### 預填XML元素說明 {#prefill-xml-elements-description}

建立預填XML檔案的語法規則：

* 父元素：元素，可以是其父項，其中null表示元素可以位於XML的根。
* 基數：說明元素可在其父元素內使用的次數。
* submitXML:指示元素在提交XML中是始終存在(P)還是可選(O)。
* prefillXML:指示預填XML中是必需(R)還是可選(O)。
* 孩子：指示哪些元素可以是其子項。

### 表單集 {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

表單集XML的根元素。 建議不要將此詞用作表單集中任何表單的rootSubform的名稱。

### FS_DATA {#fs-data}

`parent elements:`

`formset`

基數： [1]

submitXML:P

prefillXML:O

`children: xdp:xdp/rootElement`

子樹表示表單集中的表單資料。 只有在表單集元素不存在時，預填XML中的元素才是選用元素

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

此標籤表示HTML5表單XML的開始。 如果預填XML中存在或沒有預填XML，則會在提交XML中添加該XML。 可從預填XML中移除此標籤。

### XFA：資料集 {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA：資料 {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### 房屋 {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

名稱rootElement只是預留位置。 實際名稱是從表單集中使用的表單中挑選的。 以rootElement開頭的子樹狀結構包含表單集中Forms內欄位和子表單的資料。 有多種因素可決定rootElement及其子項的結構。

在預填XML中，此標籤是可選的，但如果缺少，則會忽略整個XML。

根元素標籤的名稱

如果預填XML中有根元素，該元素的名稱也會取用於提交XML。 如果沒有預填xml，則rootElement的名稱是表單集中第一個表單的根子表單的名稱，該表單集的dataRoot屬性設定為「/」。 如果沒有此類形式，則rootElement名稱為 **fs_dummy_root**，即保留關鍵字。

## AEM Forms應用程式中設定的表單 {#formset-in-workspace-app}

AEM Forms應用程式可讓現場工作人員將其行動裝置與AEM Forms伺服器同步，並處理其工作。 即使裝置離線，應用程式仍會透過將資料儲存在裝置本機而運作。 使用注釋功能（如照片），現場工作人員可以提供準確的資訊以整合到業務流程中。

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 已知限制 — 表單集中未完全支援模式 {#known-limitations-patterns-not-fully-supported-in-form-set}

表單集未完全支援以下資料模式：

<table>
 <tbody>
  <tr>
   <td><strong>表單集中未完全支援模式</strong></td>
   <td><strong>範例</strong></td>
  </tr>
  <tr>
   <td>輸入大小和模式大小不匹配</td>
   <td><p>當模式= num{z,zzz}</p> <p>和輸入=</p> <p>12,345或</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>帶括弧"(" ")"的子句模式</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>多資料模式</td>
   <td>num{zz,zzz) | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>速記模式 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num. %{}或</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
