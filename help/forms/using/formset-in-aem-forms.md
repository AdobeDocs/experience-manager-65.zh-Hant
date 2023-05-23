---
title: AEM Forms背景
seo-title: Form set in AEM Forms
description: 介紹了表單集，並說明了如何通過拼合HTML5個表單來建立表單集。 本文還介紹如何將xml資料預填充到表單集，以及如何在流程管理中使用表單集。
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

# AEM Forms背景{#form-set-in-aem-forms}

## 概觀 {#overview}

您的客戶通常需要提交多個表單才能申請服務或福利。 包括尋找一切相關形式，分別填寫、提交和跟蹤。 此外，還需要在表單中多次填寫常用詳細資訊。 如果整個過程涉及大量的形式，則會變得繁瑣和容易出錯。 AEM Forms的表單集功能有助於簡化此類場景中的用戶體驗。

表單集是HTML5表單的集合，這些表單組合在一起，並作為單個表單集呈現給最終用戶。 當最終用戶開始填寫表單集時，他們會從一個表單無縫過渡到另一個表單。 最後，他們只需點擊一下即可提交所有表格。

AEM Forms為表單作者提供了建立、配置和管理表單集的直觀用戶介面。 作為作者，您可以按希望最終用戶遵循的特定順序訂購表單。 此外，您可以在單個表單上應用條件或資格表達式，以基於用戶輸入控制其可見性。 例如，您可以將配偶詳細資訊表單配置為僅在婚姻狀態指定為「已婚」時顯示。

此外，您可以配置不同表單中的公用欄位以共用公用資料綁定。 在適當的資料綁定到位後，最終用戶只需在後續表單中自動填充一次公共資訊。

AEM Forms應用還支援表單集，允許您的現場工作人員離線使用表單集、訪問客戶、輸入資料，以後與AEM Forms伺服器同步，以將表單資料提交到業務流程。

## 建立和管理表單集 {#creating-and-managing-form-set}

可以將使用設計器建立的多個XDP或表單模板關聯到表單集。 然後，可以根據用戶在初始表單中輸入的值及其配置檔案來選擇性地呈現XDP。

使用 [AEM Forms用戶介面](../../forms/using/introduction-managing-forms.md) 管理所有表單、表單集和相關資產。

### 建立表單集 {#create-a-form-set}

要建立表單集，請執行以下操作：

1. 選擇「Forms」>「Forms」和「文檔」。
1. 選擇「建立」>「表單集」。

1. 在「添加屬性」頁中，添加以下詳細資訊，然後按一下「下一步」。

   * 標題：指定文檔的標題。 標題可幫助您識別在AEM Forms用戶介面中設定的表單。
   * 描述：指定有關文檔的詳細資訊。
   * 標籤：指定用於唯一標識表單集的標籤。 標籤幫助搜索表單集。 要建立標籤，請在「標籤」框中鍵入新標籤名稱。
   * 提交URL:指定表單集獨立格式副本(非AEM Forms應用程式使用案例)的提交資料的發佈URL。 資料以多部件/表單資料形式提交到此端點，具有以下請求參數：
   * 資料XML:此參數包含已提交表單集資料的XML表示形式。 如果表單集中的所有表單都使用公共架構，則根據該架構生成XML。 否則，XML根標籤將包含表單集中每個填充表單的子標籤，該表單集包含表單附件的資料。
   * formsetPath:已提交的CRXDE中格式集的路徑。
   * HTML渲染配置檔案：您可以配置某些選項，如浮動欄位、附件和草稿支援（對於單機表單集格式副本），以自定義表單集的外觀、行為和交互。 您可以自定義或擴展現有配置檔案以更改任何HTML表單配置檔案設定。

   ![表單集：添加屬性](assets/createformset1.png)

1. 「選擇表單」螢幕顯示可用的XDP表單或XDP檔案。 搜索並選擇要包括在表單集中的表單，然後按一下「添加到表單集」。 如有必要，請再次搜索要添加的表單。 將所有表單添加到表單集後，按一下「下一步」。

   >[!NOTE]
   >
   >確保XDP表單中的欄位名稱不包含點字元。 否則，任何試圖解析欄位的指令碼都無法解析這些欄位。

1. 在「配置表單」頁中，可以執行以下操作：

   * 窗體順序：拖放表單以重新排序。 表單順序定義在AEM Forms應用和獨立格式副本中向最終用戶顯示表單的順序。
   * 表單標識符：為要在資格表達式中使用的表單指定唯一標識。
   * 資料根：對於表單集中的每個表單，作者可以配置XPATH，在該XPATH中，特定表單的資料以已提交的XML形式放置。 預設情況下，值為/。 如果表單集中的所有表單都綁定了模式並共用了相同的XML模式，則可以更改此值。 建議在XDP中指定格式中的每個欄位都具有適當的資料綁定。 如果兩個不同表單中的兩個欄位共用公共資料綁定，則第二個表單中的欄位顯示第一個表單中的預填充值。 不要將具有相同內部內容的兩個子窗體綁定到同一XML節點。 有關表單集的XML結構的詳細資訊，請參見 [為表單集預填充XML](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p)。
   * 資格表達式：指定一個JavaScript表達式，該表達式計算布爾值並指示表單集中的表單是否適合填充。 如果為false，則不要求用戶填寫，甚至不顯示要填寫的表單。 通常，表達式基於在此表單之前捕獲的欄位的值。 表達式還包含對表單集API fs.valueOf的調用，以提取表單集的欄位中由用戶填充的值：

   *fs.valueOf(&lt;form identifier=&quot;&quot;>。 &lt;fieldsom expression=&quot;&quot;>)> &lt;value>*

   例如，如果表單集中有兩個表單：業務費用和差旅費用，您可以在這兩個表單的「資格表達式」欄位中為這兩個表單添加JavaScript代碼段，以檢查表單中費用類型的用戶輸入。 如果用戶選擇「業務費用」，則「業務費用」表單將呈現給最終用戶。 或者，如果用戶選擇差旅費，則向最終用戶呈現不同的表單。 有關詳細資訊，請參閱資格表達式。

   此外，作者還可以選擇使用每行右角的「刪除」表徵圖從表單集中刪除表單，或使用「 」添加另一組表單&#x200B;**+**&#x200B;表徵圖。 此&#39;**+**「表徵圖將用戶引導回嚮導中的上一步，該步驟用於「選擇表單」。 現有選擇將保持不變，並且必須使用該頁上的「添加到表單集」表徵圖將所做的任何其他選擇添加到表單集。

   ![表單集：配置表單](assets/createformset2.png)

   >[!NOTE]
   >
   >表單集中使用的所有表單都由AEM Forms用戶介面管理。

### 管理表單集 {#managing-a-form-set}

建立表單集後，您可以對該表單集執行以下操作：

* 按一下：建立並列在主資產頁上的表單集時，可以按一下表單集以查看它。 表單集開啟並顯示該表單集中的所有表單模板(XDP)。
* 編輯：在選擇表單集後按一下「編輯」時，將開啟「配置表單」螢幕，該螢幕在建立表單集的步驟中如上所示。 您可以執行此處描述的所有功能。
* 複製+貼上：這允許您從一個位置複製整個表單集，並將其貼上到同一位置或任何其他位置或資料夾。
* 下載：您可以下載包含其所有依賴項的表單集。
* 開始/管理審閱：建立表單集後，可通過按一下「開始審閱」(Start Review)來設定其審閱。 在對表單集啟動審閱後，將向用戶顯示「管理審閱」選項。 在「管理審閱」螢幕上，可以更新/結束審閱。 對於您添加的審閱，如有必要，您可以檢查審閱並添加註釋。
* 刪除：刪除完整的表單集。 已刪除表單集中的表單保留在儲存庫中。
* 發佈/取消發佈：此表單將發佈/取消發佈表單集及其包含的所有表單以及這些表單的相關資產。
* 預覽：預覽提供兩個選項：預覽為HTML（無資料），自定義預覽為示例資料。
* 檢視/編輯屬性：您可以檢視/編輯所選表單集的元資料屬性。

![createformset3](assets/createformset3.png)

### 編輯表單集 {#edit-a-form-set}

要編輯表單集，請執行以下操作：

1. 選擇「Forms」>「Forms」和「文檔」。
1. 找到要編輯的表單集。 將滑鼠懸停在上面並選擇「編輯」( ![編輯](assets/editicon.png))。
1. 在「配置表單」頁中，可以編輯以下內容：

   * 窗體順序
   * 表單識別碼
   * 資料根
   * 資格表達式

   也可以按一下相關的「刪除」表徵圖從表單集中刪除表單。

## 在Oracle Process Management中設定窗體 {#form-set-in-process-management}

使用「AEM Forms管理」用戶介面建立表單集後，您可以使用「起始點」或「使用工作台分配任務」活動中的表單集。

### 在任務或起點中使用表單集 {#using-form-set-in-task-or-start-point}

1. 設計流程時，在「分配任務/起始點」的「演示和資料」部分下，選擇 **使用CRX資產**。 CRX資產瀏覽器出現。

   ![設計流程：使用CRX資產](assets/formsetinprocessmgmt1.png)

1. 選擇表單集以篩選儲存庫(AEMCRX)中的表單集。

   ![設計流程：「選擇表單資產」對話框](assets/formsetinprocessmgmt2.png)

1. 選擇表單集並按一下確定。

## 資格表達式 {#eligibility-expressions}

表單集中的資格表達式用於定義和動態控制顯示給用戶的表單。 例如，僅當用戶屬於特定年齡組時才顯示特定窗體。 使用表單管理器指定和編輯資格表達式。

資格表達式可以是任何返回布爾值的有效JavaScript語句。 JavaScript代碼段中的最後一條語句被視為一個布爾值，該布爾值根據JavaScript代碼段其餘（前幾行）中的處理確定表單的資格。 如果表達式的值為true，則表單有資格顯示給用戶。 此類表格稱為合格表格。

>[!NOTE]
>
>不執行表單集中第一個表單的資格表達式。 無論其資格表達式如何，都始終顯示第一個表單。

除了標準JavaScript函式外，表單集還顯示fs.valueOf API，該API提供對表單集中表單欄位值的訪問。 使用此API訪問表單集中表單域的值。 API語法為fs.valueOf(formUid, fieldSOM)，其中：

* formUid（字串）:表單集中表單的唯一ID。 可以在表單管理器用戶介面中建立表單集時指定它。 預設情況下，它是表單名稱。
* 欄位SOM（字串）:formUid指定格式的欄位的SOM表達式。 SOM表達式或指令碼對象模型表達式用於引用特定文檔對象模型(DOM)中的值、屬性和方法。 在選擇欄位時，可以在「指令碼」頁籤下的「表單設計器」中查看它。

>[!NOTE]
>
>formUid和fieldSOM參數都必須是字串文本。

### 範例 {#examples}

API的有效用法：

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

API的使用無效：

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 為表單集預填充XML {#prefill-xml-for-form-set}

表單集是多個HTML5表單的集合，這些表單具有共同或不同的架構。 表單集支援使用XML檔案預填充表單域。 可以將XML檔案與表單集關聯，這樣，當您在表單集中開啟表單時，表單中的某些欄位就會被預先處理。

預填充XML檔案是使用表單集URL的dataRef參數指定的。 dataRef參數指定與表單集合併的資料XML檔案的絕對路徑。

例如，在具有以下結構的表單集中有三個表單（form1、form2和form3）:

form1

欄位

form2

欄位

form3

欄位

每個表單都有一個公用的命名欄位，名為&quot;field&quot;，並有一個唯一的命名字段，名為&quot;formfield&quot;。

可以使用具有以下結構的XML預填充此表單集：

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
>XML根標籤可以具有任何名稱，但與欄位對應的元素標籤必須具有與欄位相同的名稱。 XML的層次結構必須模仿表單的層次結構，這意味著XML必須具有用於包裝子表單的相應標籤。

上述XML代碼段顯示表單集的預填充XML是各個表單的預填充XML代碼段的聯合。 如果不同表單中的某些欄位具有彼此相似的資料層次/架構，則這些欄位將預填相同的值。 在本示例中，所有三個表單都預填充了公共欄位&quot;field&quot;的相同值。 這是將資料從一種形式轉發到另一種形式的簡單方法。 也可以通過將欄位綁定到同一架構或資料引用來實現這一點。 如果要根據表單的架構分離表單集資料。 這可以通過在建立表單集期間指定表單的「資料根」屬性來實現（預設值為「/」，它映射到表單集根標籤）。

在上例中，如果指定資料根：&quot;/form1&quot;、&quot;/form2&quot;和&quot;/form3&quot;分別用於這三個表單，需要使用以下結構的預填充XML:

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

在表單集中，XML使用以下語法定義了XML架構：

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
>如果存在兩個具有重疊資料根的表單，或者一個表單的元素層次與另一個表單的資料根層次重疊，則在預填充xml中合併重疊元素的值。 提交XML與預填充XML結構相似，但提交XML具有更多的包裝標籤和附加在表單集上下文資料標籤的結尾。

### 預填充XML元素說明 {#prefill-xml-elements-description}

用於建立預填充XML檔案的語法規則：

* 父元素：元素（可以是其父級），其中null表示元素可以位於XML的根。
* 基數：描述了元素在其父元素中可使用的次數。
* submitXML:指示元素在提交XML中是始終存在(P)還是可選(O)。
* prefillXML:指示在預填充XML中是必需(R)還是可選(O)元素。
* 子項：指示哪些元素可以是其子元素。

### 格式集 {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

表單集XML的根元素。 建議不要將此單詞用作表單集中任何表單的rootSubform的名稱。

### FS_DATA {#fs-data}

`parent elements:`

`formset`

基數： [1]

submitXML:P

prefillXML:O

`children: xdp:xdp/rootElement`

子樹指示表單集中表單的資料。 僅當表單集元素不存在時，該元素在預填充XML中是可選的

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

此標籤指示HTML5表單XML的開始。 如果提交XML中存在該XML，或者沒有預填充XML，則會將其添加到提交XML中。 可以從預填充XML中刪除此標籤。

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

### 根 {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

名稱rootElement只是一個佔位符。 實際名稱是從表單集中使用的表單中選取的。 以rootElement開頭的子樹包含表單集中Forms內的欄位和子表單的資料。 有多種因素決定rootElement及其子級的結構。

在預填充XML中，此標籤是可選的，但如果缺少它，則忽略整個XML。

根元素標籤的名稱

如果預填充XML中有根元素，則該元素的名稱也將在提交XML中使用。 如果沒有預填充xml，則rootElement的名稱是表單集中第一個表單的根子表單的名稱，該表單的dataRoot屬性設定為「/」。 如果沒有此形式，則rootElement名稱為 **fs_dummy_root**，是保留關鍵字。

## 在AEM Forms應用中設定的窗體 {#formset-in-workspace-app}

AEM Forms應用允許現場工作人員將他們的移動設備與AEM Forms伺服器同步，並處理他們的任務。 即使在設備離線時，應用程式也會通過將資料本地保存到設備上而工作。 使用注釋功能（如照片），現場工作人員可以提供準確的資訊以整合到業務流程中。

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 已知限制 — 表單集中不完全支援模式 {#known-limitations-patterns-not-fully-supported-in-form-set}

表單集不完全支援以下資料模式：

<table>
 <tbody>
  <tr>
   <td><strong>表單集中未完全支援模式</strong></td>
   <td><strong>範例</strong></td>
  </tr>
  <tr>
   <td>輸入大小和圖案大小不匹配</td>
   <td><p>當pattern= num{z,zzz}時</p> <p>和輸入=</p> <p>12,345或</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>帶括弧"(" ")"的圖片子句模式</td>
   <td>數字{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>多個資料模式</td>
   <td>數字{zz,zzz} |num{z,zzz,zzz</td>
  </tr>
  <tr>
   <td>速記模式 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>數字%{}或</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
