---
title: AEM Forms中的表單集
description: 本文介紹表單集，並說明如何將HTML5表單彙整在一起，以建立表單集。 本文也說明如何將xml資料預填至表單集，以及如何在程式管理中使用表單集。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2804'
ht-degree: 0%

---

# AEM Forms中的表單集{#form-set-in-aem-forms}

## 概觀 {#overview}

您的客戶通常需要提交多個表單才能申請服務或權益。 它需要尋找所有相關表單；以及個別填寫、提交和追蹤表單。 此外，他們還需要在表格中多次填寫常見詳細資訊。 如果涉及大量表單，則整個流程會變得繁瑣且容易出錯。 AEM Forms的表單集功能可協助簡化在這類情況下的使用者體驗。

表單集是分組在一起的HTML5表單的集合，並以單一表單集呈現給一般使用者。 使用者開始填寫表單集時，就能順暢地從一個表單轉換為另一個表單。 最後，使用者只要按一下即可提交所有表單。

AEM Forms為表單作者提供直覺式使用者介面，以便建立、設定和管理表單集。 身為作者，您可以按照您希望一般使用者遵循的特定順序來排序表格。 此外，您也可以在個別表單上套用條件或適用性運算式，以根據使用者輸入控制其可見性。 例如，您可以將配偶詳細資料表單設定為僅在婚姻狀況指定為「已婚」時顯示。

此外，您可以設定不同表單中的通用欄位，以共用通用資料繫結。 設定好適當的資料繫結後，一般使用者只需在後續表單中自動填入一般資訊一次。

AEM Forms應用程式也支援表單集，可讓您的欄位員工離線建立表單集、造訪客戶、輸入資料，以及稍後與AEM Forms伺服器同步，以將表單資料提交至業務流程。

## 建立和管理表單集 {#creating-and-managing-form-set}

您可以使用設計工具將多個XDP或表單範本關聯到表單集中。 接著，即可使用表單集，根據使用者在初始表單及其設定檔中輸入的值，選擇性地轉譯XDP。

使用 [AEM Forms使用者介面](../../forms/using/introduction-managing-forms.md) 以管理所有表單、表單集和相關資產。

### 建立表單集 {#create-a-form-set}

若要建立表單集，請執行下列動作：

1. 選取「Forms > Forms和檔案」。
1. 選取「建立>表單集」。

1. 在新增特性頁面中，新增下列詳細資訊，然後按下一步。

   * Title：指定檔案的標題。 標題可協助您識別AEM Forms使用者介面中設定的表單。
   * 說明：指定檔案的詳細資訊。
   * 標籤：指定可唯一識別表單集的標籤。 標籤有助於搜尋表單集。 若要建立標籤，請在「標籤」方塊中鍵入新標簽名稱。
   * 提交URL：指定針對表單集的獨立轉譯(非AEM Forms應用程式使用案例)發佈已提交資料的URL。 資料會透過下列請求引數，以multipart/formdata形式提交至此端點：
   * dataXML：此引數包含已提交表單集資料的XML表示法。 如果表單集中的所有表單都使用共同綱要，則會根據該綱要產生XML。 否則，XML根標籤會針對表單集中每個已填入的表單，包含一個子標籤，其中包含表單附件的資料。
   * formsetPath： CRXDE中已提交之表單集的路徑。
   * HTML演算設定檔：您可以設定某些選項，例如浮動欄位、附件和草稿支援（適用於獨立表單集轉譯），以自訂表單集的外觀、行為和互動。 您可以自訂或擴充現有的設定檔，以變更任何HTML表單設定檔設定。

   ![表單集：新增屬性](assets/createformset1.png)

1. 「選取表單」畫面會顯示可用的XDP表單或XDP檔案。 搜尋並選取要納入表單集的表單，然後按一下「新增至表單集」。 如有必要，請再次搜尋要新增的表單。 將所有表單新增至表單集後，按一下「下一步」。

   >[!NOTE]
   >
   >請確定XDP表單中的欄位名稱不包含點字元。 否則，任何嘗試解析包含點字元的欄位的指令碼無法解析它們。

1. 在「設定表單」頁面中，您可以執行下列作業：

   * 表單順序：拖放表單以重新排序。 表單順序會定義在AEM Forms應用程式和獨立轉譯中向一般使用者顯示表單的順序。
   * 表單識別碼：指定要用於適用性運算式之表單的唯一身分。
   * 資料根：針對表單集中的每個表單，作者可以設定XPATH，該特定表單的資料會放置於提交的XML中。 預設值為/。 如果表單集中的所有表單都是結構描述繫結並共用相同的XML結構描述，您可以變更此值。 建議表單中的每個欄位都有XDP中指定的適當資料繫結。 如果兩個不同表單中的兩個欄位共用相同的資料繫結，則第二個表單中的欄位會顯示第一個表單中的預填值。 請勿將內部內容相同的兩個子表單繫結至相同的XML節點。 如需表單集的XML結構的詳細資訊，請參閱 [預填表單集的XML](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * 適用性運算式：指定評估布林值的JavaScript運算式，並指示表單集中的表單是否符合填寫條件。 如果為false，則不會要求使用者填寫表單，甚至不會向其顯示要填寫的表單。 通常，運算式會根據此表單前擷取的欄位值。 運算式也包含對表單集API fs.valueOf的呼叫，以擷取使用者在表單集表單的欄位中填入的值：

   *fs.valueOf(&lt;form identifier=&quot;&quot;>， &lt;fieldsom expression=&quot;&quot;>) > &lt;value>*

   例如，如果表單集內有兩個表單：商務費用與差旅費，則您可以在資格運算式欄位中為這兩個表單新增JavaScript程式碼片段，以檢查使用者輸入表單中的費用型別。 如果使用者選擇「業務費用」，則「業務費用」表單會呈現給一般使用者。 或者，如果使用者選擇差旅費，則會將不同的表單呈現給一般使用者。 如需詳細資訊，請參閱適用性運算式。

   此外，作者也可以選擇使用每列右角的「刪除」圖示，從表單集移除表單，或使用「**+**」圖示。 這個&#39;**+**&#39;圖示會將使用者導回精靈中的上一個步驟，即「選取表單」。 現有選擇會得到維護，而且任何額外的選擇都必須使用頁面上的「新增至表單集」圖示新增至表單集。

   ![表單集：設定表單](assets/createformset2.png)

   >[!NOTE]
   >
   >表單集中使用的所有表單皆由AEM Forms使用者介面管理。

### 管理表單集 {#managing-a-form-set}

建立表單集後，您可以對該表單集執行下列動作：

* 按一下：建立表單集並列在主資產頁面時，您可以按一下表單集進行檢視。 表單集隨即開啟並顯示該表單集中的所有表單範本(XDP)。
* 編輯：選取表單集後按一下「編輯」時，會開啟設定表單（如上方「建立表單集的步驟」中所顯示）畫面。 您可以執行此處所述的所有功能。
* 複製+貼上：這可讓您從一個位置複製整個表單集，並將其貼到相同位置或任何其他位置或資料夾。
* 下載：您可以下載包含所有相依性的表單集。
* 開始/管理檢閱：建立表單集後，您可以按一下「開始檢閱」來設定其檢閱。 開始表單集的稽核後，管理稽核選項就會向使用者顯示。 在「管理稽核」畫面上，您可以更新/結束稽核。 對於您新增的稽核，您可以檢查稽核並在必要時新增註釋。
* 刪除：刪除完整的表單集。 已刪除表單集中的表單會保留在存放庫中。
* 發佈/取消發佈：這會發佈/取消發佈表單集，以及其包含的所有表單以及這些表單的相關資產。
* 預覽：預覽提供兩個選項：以HTML預覽（不含資料）和自訂預覽（含範例資料）。
* 檢視/編輯屬性：您可以檢視/編輯所選表單集的中繼資料屬性。

![createformatset3](assets/createformset3.png)

### 編輯表單集 {#edit-a-form-set}

若要編輯表單集，請執行下列動作：

1. 選取「Forms > Forms和檔案」。
1. 找到您要編輯的表單集。 將滑鼠停留在滑鼠上並選取編輯( ![編輯](assets/editicon.png))。
1. 在「設定表單」頁面中，您可以編輯下列專案：

   * 表單順序
   * 表單識別碼
   * 資料根
   * 適用度運算式

   您也可以按一下相關的「刪除」圖示，將表單從「表單集」中刪除。

## 處理序管理中的表單集 {#form-set-in-process-management}

使用「AEM Forms管理」使用者介面建立表單集後，您就可以在「起點」中使用表單集，或使用「工作台」使用「指派工作」活動。

### 在任務或起點中使用表單集 {#using-form-set-in-task-or-start-point}

1. 設計流&#39;b5&#39;7b時，在「指派任務/起點」的「簡報與資料」區段下，選取 **使用CRX資產**. CRX資產瀏覽器隨即顯示。

   ![設計程式：使用CRX資產](assets/formsetinprocessmgmt1.png)

1. 選取表單集以篩選AEM存放庫(CRX)中的表單集。

   ![設計程式：選取表單資產對話方塊](assets/formsetinprocessmgmt2.png)

1. 選取表單集，然後按一下「確定」。

## 適用性運算式 {#eligibility-expressions}

表單集中的適用性運算式可用來定義及動態控制向使用者顯示的表單。 例如，僅當使用者屬於特定年齡群組時才顯示特定表單。 使用表單管理員來指定及編輯適用性運算式。

適用性運算式可以是傳回布林值的任何有效JavaScript陳述式。 JavaScript程式碼片段中的最後一個陳述式會被視為布林值，而布林值會根據JavaScript程式碼片段的其他（前幾行）處理來決定表單的適用性。 如果運算式的值為true，則表單符合向使用者顯示的條件。 這類表單稱為合格表單。

>[!NOTE]
>
>表單集中第一個表單的適用性運算式不會執行。 無論適用性運算式為何，都會一律顯示第一個表單。

除了標準JavaScript函式外，表單集也會公開fs.valueOf API，此API提供表單集中表單欄位值的存取權。 使用此API來存取表單集中表單欄位的值。 API語法為fs.valueOf (formUid， fieldSOM)，其中：

* formUid （字串）：表單集中的表單唯一ID。 您可以在表單管理員使用者介面中建立表單集時指定它。 預設為表單名稱。
* fieldSOM （字串）：formUid所指定表單中的欄位SOM運算式。 SOM運算式或Scripting Object Model運算式是用來參照特定檔案物件模型(DOM)中的值、屬性和方法。 選取欄位時，您可以在「指令碼」標籤下的「表單設計工具」中檢視它。

>[!NOTE]
>
>formUid和fieldSOM引數都必須是字串常值。

### 範例 {#examples}

API的有效用法：

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

API的無效用法：

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 預填表單集的XML {#prefill-xml-for-form-set}

表單集是包含相同或不同結構描述的多個HTML5表單的集合。 表單集支援使用XML檔案預先填入表單欄位。 您可以將XML檔案與表單集建立關聯，這樣當您開啟表單集中的表單時，表單中的某些欄位會預先排版。

使用表單集URL的dataRef引數指定預填XML檔案。 dataRef引數會指定與表單集合併的資料XML檔案的絕對路徑。

例如，您有三個表單（form1、form2和form3），表單集具有下列結構：

form1

欄位表單1欄位

form2

欄位form2field

form3

欄位form3field

每個表單都有一個名為「field」的共同欄位以及一個名為「formfield」的唯一命名欄位。

您可以使用具有以下結構的XML預先填寫此表單集：

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
>XML根標籤可以有任何名稱，但是與欄位對應的元素標籤必須具有與該欄位相同的名稱。 XML的階層必須模擬表單的階層，這表示XML必須有對應的標籤來封裝子表單。

上述XML片段顯示表單集的預填XML是個別表單的預填XML片段的聯合。 如果不同表單中的某些欄位具有相似的資料階層/結構描述，則該欄位會預先填入相同的值。 在此範例中，所有三個表單都預先填入了通用欄位「field」的相同值。 這是一種將資料從一個表單轉送至下一個表單的簡單方式。 這也可以透過繫結欄位到相同的結構描述或資料參考來達成。 如果您想要根據表單的結構描述來分隔表單集資料。 這可在表單集建立期間透過指定表單的「資料根」屬性來達成（預設值為「/」，對映至表單集根標籤）。

在上一個範例中，如果您為三個表單分別指定資料根：「/form1」、「/form2」和「/form3」，則需使用下列結構的預填XML：

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

在表單集中，XML會使用下列語法定義XML綱要：

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
>如果有兩個表單具有重疊的資料根，或一個表單的元素階層與另一個表單的資料根階層重疊，則在預填xml中，會合併重疊的元素值。 提交XML的結構與預填XML類似，但提交XML的包裝函式標籤更多，而且最後會附加一些表單集內容資料標籤。

### 預填XML元素說明 {#prefill-xml-elements-description}

建立預填XML檔案的語法規則：

* parent elements：可以是其父系的元素，其中null表示元素可以位於XML的根目錄。
* 基數：描述在其上層元素內可以使用元素的次數。
* submitXML：指示元素在提交XML中是否永遠存在(P)或選擇性(O)。
* prefillXML：指示元素在預填XML中是必要(R)或選用(O)。
* 子項：指出哪些元素可以是其子項。

### 表單集 {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

表單集XML的根元素。 建議不要將此字作為表單集中任何表單的rootSubform的名稱。

### FS_DATA {#fs-data}

`parent elements:`

`formset`

基數： [1]

submitXML： P

prefillXML： O

`children: xdp:xdp/rootElement`

子樹狀結構會指出表單集中表單的資料。 只有在表單集元素不存在時，預填XML中的元素才為選用

### XDP：XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

此標籤表示HTML5表單XML的開頭。 如果預填XML中存在或沒有預填XML，則會將此內容新增到提交XML中。 此標籤可從預填XML中移除。

### XFA：資料集 {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA：DATA {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### ROOTELEMENT {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

名稱rootElement只是預留位置。 實際名稱是從表單集中使用的表單中挑選的。 以rootElement開頭的子樹狀結構包含表單集Forms中欄位和子表單的資料。 有多個因素可決定rootElement及其子系的結構。

在預填XML中，此標籤是選擇性的，但如果遺失此標籤，則會忽略整個XML。

根元素標籤的名稱

如果預填XML中有根元素，該元素的名稱也會出現在提交XML中。 若沒有預填xml，則rootElement的名稱為表單集中第一個表單的Root子表單的名稱，該表單具有設定為「/」的dataRoot屬性。 如果沒有這樣的表單，則rootElement名稱為 **fs_dummy_root**，這是保留關鍵字。

## AEM Forms應用程式中的表單集 {#formset-in-workspace-app}

AEM Forms應用程式可讓現場工作者將其行動裝置與AEM Forms伺服器同步化，並處理其工作。 即使裝置因將資料儲存在裝置本機而離線，應用程式仍可運作。 使用註釋功能（例如像片），現場工作者可以提供精確資訊以整合到業務流程中。

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 已知限制 — 表單集中不完全支援的模式 {#known-limitations-patterns-not-fully-supported-in-form-set}

表單集中不完全支援下列資料模式：

<table>
 <tbody>
  <tr>
   <td><strong>表單集中不完全支援的模式</strong></td>
   <td><strong>範例</strong></td>
  </tr>
  <tr>
   <td>輸入大小和圖樣大小不相符</td>
   <td><p>當pattern= num{z，zzz}</p> <p>而且輸入=</p> <p>12,345或</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>括弧「(」「)」的Picture子句模式</td>
   <td>數字{(zz，zzz)}</td>
  </tr>
  <tr>
   <td>多個資料模式</td>
   <td>num{zz，zzz} | num{z，zzz，zzz}</td>
  </tr>
  <tr>
   <td>速記模式 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>數字。%{}，或</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
