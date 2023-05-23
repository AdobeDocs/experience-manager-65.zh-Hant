---
title: 資料字典
seo-title: Data Dictionary
description: Oracle Tergement Management中的資料字典允許您將後端資料整合到信函中作為輸入，以用於客戶信函。
seo-description: Data dictionary in Correspondence Management lets you integrate back-end data to letters as inputs for use in customer correspondence.
uuid: 178a285e-b4a4-4a36-a2aa-b43ecb0871ed
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a1a0ad6b-023a-4822-9cce-0618657c3f9d
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3838'
ht-degree: 1%

---

# 資料字典{#data-dictionary}

## 簡介 {#introduction}

資料字典使業務用戶能夠使用來自後端資料源的資訊，而無需瞭解其基礎資料模型的技術詳細資訊。 資料字典由資料字典元素(DDE)組成。 您可以使用這些資料元素將後端資料整合到信函中作為輸入，以用於客戶信函。

資料字典是描述基礎資料結構及其相關屬性的元資料的獨立表示。 使用商業辭彙建立資料字典。 它可以映射到一個或多個基礎資料模型。

資料字典由三種類型的元素組成：Simple、Composite和Collection元素。 簡單DDE是原始元素，如字串、數字、日期和布爾值，它們包含城市名稱等資訊。 複合DDE包含其它DDE，其類型可以是基元、複合或集合。 例如，地址，它由街道地址、城市、省、國家和郵遞區號組成。 集合是類似的簡單或複合DDE的清單。 例如，具有多個地點或不同開單和發運地址的客戶。

通信管理使用根據資料字典的結構儲存的後端、客戶或收件人特定的資料來建立針對不同客戶的通信。 例如，可以使用友好名稱建立文檔，如「尊敬的{First Name}」，「Mr。 {姓氏}&quot;.

通常，業務用戶不需要對元資料表示(如XSD（XML架構）和Java類)有所瞭解。 但是，它們通常需要訪問這些資料結構和屬性來構建解決方案。

### 資料字典工作流 {#data-dictionary-workflow}

1. 作者 [建立資料字典](#createdatadictionary) 上載模式或從頭開始。
1. 作者根據資料字典建立字母和互動式通信，並根據需要將字母和互動式通信中的資料字典元素關聯起來。
1. 作者可以下載基於資料字典模式的XML檔案示例。 作者可以修改樣本資料XML檔案，該檔案可以與資料字典test資料關聯。 在字母預覽期間使用相同的內容。
1. 同時 [預覽信件](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p)，作者選擇預覽帶資料的字母（自定義預覽）。 此信開啟，並預填作者提供的資料。 這將在建立對應介面中開啟。 預覽此信函的代理可以修改此信函中的內容、資料和附件，並可以提交最終信函。 有關建立字母的詳細資訊，請參閱 [建立對應](../../forms/using/create-letter.md)。

## 必備條件 {#prerequisite}

安裝 [相容性包](compatibility-package.md) 的 **資料字典** 的上界 **Forms** 的子菜單。

## 建立資料字典 {#createdatadictionary}

您可以使用資料字典編輯器建立資料字典，或者可以上載XSD架構檔案以基於此建立資料字典。 然後，可以通過添加更多所需資訊（包括欄位）來擴展資料字典。 無論資料字典的建立方式如何，業務流程所有者都不需要對後端系統的知識。 業務流程所有者只需要知道域對象及其定義，即可完成其流程。

>[!NOTE]
>
>對於需要相似元素的多個字母，可以建立公用資料字典。 然而，具有大量元素的大資料字典在使用資料字典和載入元素（例如字母和文檔片段）時可能會導致效能問題。 如果遇到效能問題，請嘗試為不同的字母建立單獨的資料字典。

1. 選擇 **Forms** > **資料字典**。
1. 點擊 **建立資料字典**。
1. 在「屬性」螢幕中，添加以下內容：

   * **標題：** （可選）輸入資料字典的標題。 標題不必唯一，可以有特殊字元和非英文字元。 字母和其他文檔片段與其標題（如果可用）一起引用，例如在縮略圖和資產屬性中。 資料字典是以其名稱而不是標題引用的。
   * **名稱：** 資料字典的唯一名稱。 在「名稱」欄位中，只能輸入英語字元、數字和連字元。 「名稱」欄位將基於「標題」欄位自動填充，在「標題」欄位中輸入的特殊字元、空格、數字和非英語字元將替換為連字元。 儘管「標題」(Title)欄位中的值會自動複製到「名稱」(Name)中，但您可以編輯該值。

   * **說明**:（可選）資料字典的說明。
   * **標籤：** （可選）要建立自定義標籤，請在文本欄位中輸入值，然後按Enter。 您可以在標籤的文本欄位下看到您的標籤。 保存此文本時，還會建立新添加的標籤。
   * **擴展屬性**:（可選）點擊 **添加欄位** 指定資料字典的元資料屬性。 在「屬性名稱」列中，輸入唯一的屬性名稱。 在「值」列中，輸入要與屬性關聯的值。

   ![德語中指定的資料字典屬性](do-not-localize/1_ddproperties.png)

1. （可選）要上載資料字典的XSD架構定義，請在「資料字典結構」窗格下按一下 **上載XML架構**。 瀏覽到XSD檔案，選擇它，然後點擊 **開啟**。 基於上載的XML架構建立資料字典。 您需要調整資料字典中元素的顯示名稱和說明。 為此，請按一下元素名稱，然後在右窗格中的欄位中編輯其說明、顯示名稱和其他詳細資訊，以選擇這些元素的名稱。

   有關計算DD元素的詳細資訊，請參見 [計算資料字典元素](#computedddelements)。

   >[!NOTE]
   >
   >可以使用用戶介面從頭跳過上載架構檔案和構建資料字典。 要執行此操作，請跳過此步驟，然後繼續下一步。

1. 點擊 **下一個**。
1. 在添加屬性螢幕中，將元素添加到資料字典中。 如果上載了一個架構以獲取資料字典的基本結構，則還可以添加/刪除元素並編輯其詳細資訊。

   您可以點擊元素右側的三個點，然後將元素添加到資料字典結構。

   ![1_2建立元素](assets/1_2_createanelement.png)

   選擇複合元素、集合元素或基元元素。

   * 複合DDE包含其它DDE，其類型可以是基元、複合或集合。 例如，地址，它由街道地址、城市、省、國家和郵遞區號組成。
   * 基元DDE是字串、數字、日期和布爾值等元素，它們包含城市名稱等資訊。
   * 集合是類似的簡單或複合DDE的清單。 例如，具有多個地點或不同開單和發運地址的客戶。

   以下是建立資料字典的一些規則：

   * 在資料字典中，只允許將複合類型作為頂級DDE。
   * 名稱、引用名稱和元素類型是資料字典和DDE的必需欄位。
   * 引用名稱必須唯一。
   * 父DDE（複合）不能有兩個同名的子級。
   * 枚舉僅包含基元字串類型。

   有關複合、集合和基元元素以及使用資料字典元素的詳細資訊，請參見 [將資料字典元素映射到XML架構](#mappingddetoschema)。

   有關資料字典中驗證的資訊，請參閱 [資料字典編輯器驗證](#ddvalidations)。

   ![2_adddproperty基本](assets/2_addddpropertiesbasic.png)

1. （可選）選擇元素後，可在「高級」頁籤中添加屬性（屬性）。 也可以點擊 **添加欄位** 並擴展DD元素的屬性。

   ![3_adddproperties高級](assets/3_addddpropertiesadvanced.png)

1. （可選）通過點擊元素右側的三個點並選取 **刪除**。

   ![4_刪除元素](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >刪除包含子節點的複合/集合元素也會刪除其子節點。

1. （可選）在「資料字典結構」窗格和「欄位和變數清單」面板中選擇元素。 更改或添加與元素關聯的任何必需屬性。
1. 點擊 **保存**。

### 建立一個或多個資料字典的副本 {#create-copies-of-one-or-more-data-dictionary}

要快速建立一個或多個具有類似於現有資料字典的屬性和元素的資料字典，可以複製和貼上它們。

1. 從資料字典清單中，選擇相應的資料字典。 UI顯示「複製」表徵圖。
1. 點選「 複製」。UI顯示「貼上」表徵圖。
1. 按一下「貼上」。 此時將出現「貼上」對話框。 系統自動為新資料字典分配名稱和標題。
1. 如果需要，請編輯要用其保存資料字典副本的標題和名稱。
1. 按一下「貼上」。 建立資料字典的副本。 現在，您可以在新建立的資料字典中進行所需的更改。

## 請參閱引用資料字典元素的文檔片段或文檔 {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

在編輯或查看資料字典時，您可以看到資料字典中引用了哪些元素，其中包含文本、條件、字母和交互通信。

1. 執行下列操作之一以編輯資料字典：

   * 將滑鼠懸停在資料字典上，然後按一下「編輯」。
   * 選擇資料字典，然後點擊標題中的「編輯」。
   * 將滑鼠懸停在資料字典上，然後點擊「Select（選擇）」。 然後按一下標題中的「編輯」。

   或者點擊資料字典查看。

1. 在資料字典中，按一下一個簡單元素以選擇它。 複合元素和集合元素沒有引用。

   除元素的「基本」和「高級」屬性外，還會顯示「借出內容」。

1. 按一下「借出內容」。

   此時將顯示「借出內容」頁籤，其中包含以下內容：文本、條件、字母和交互通信。 每個標題還顯示對選定元素的引用數。

1. 按一下標題可查看引用元素的資產名稱。

   ![鏡頭內容](assets/lentcontent.png)

1. 要查看其他元素的借出內容，請點擊該元素。
1. 要顯示引用元素的資產，請點擊其名稱。 瀏覽器顯示資產、字母或互動式通信。

## 使用test資料 {#working-with-test-data}

1. 在「資料字典」頁上，按一下 **選擇**。
1. 點擊要下載test資料的資料字典，然後點擊 **下載示例XML資料**。
1. 點擊 **確定** 的子菜單。 將下載XML檔案。
1. 使用記事本或其他XML編輯器開啟XML檔案。 XML檔案與元素中的資料字典和佔位符字串具有相同的結構。 將佔位符字串替換為要test字母的資料。

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >在本示例中，XML為集合元素的三個值建立空間，但可根據要求增加/減少值的數量。

1. 生成資料條目後，在預覽帶有test資料的字母時，可以使用此XML檔案。

   您可以使用DD添加此test資料(選擇DD並點擊「上載Test資料」並上載此xml檔案)。因此，在此之後，當您正常預覽字母（而非自定義）時，此XML資料將用於字母。 您也可以點擊「自定義」，然後上載此XML。

## 示例 {#samples}

以下代碼示例顯示資料字典的實現詳細資訊。

### 可上載到資料字典的示例方案 {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## 與DDE關聯的公用屬性 {#common-attributes-associated-with-a-dde}

下表詳細說明了與DDE關聯的公用屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>字串</td>
   <td>必要.<br /> DDE的名稱。 它一定是獨一無二的。</td>
  </tr>
  <tr>
   <td>引用<br /> 名稱</td>
   <td>字串</td>
   <td>必要. DDE的唯一引用名稱，允許對DDE的引用與對資料字典的層次結構或結構的更改無關。 使用此名稱映射文本模組</td>
  </tr>
  <tr>
   <td>顯示名稱</td>
   <td>字串</td>
   <td>DDE的可選用戶友好名稱。</td>
  </tr>
  <tr>
   <td>說明</td>
   <td>字串</td>
   <td>DDE的說明。</td>
  </tr>
  <tr>
   <td>元素類型</td>
   <td>字串</td>
   <td>必要. DDE的類型：STRING、NUMBER、DATE、Boolean、COMPOSITE、COLLECTION。</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>字串</td>
   <td>DDE的子類型：枚舉。 僅允許STRING和NUMBER elementType。</td>
  </tr>
  <tr>
   <td>金鑰</td>
   <td>布林值</td>
   <td>指示DDE是否為鍵元素的布爾欄位。</td>
  </tr>
  <tr>
   <td>運算結果</td>
   <td>布林值</td>
   <td>指示是否計算DDE的布爾欄位。 計算的DDE值是其它DDE值的函式。 預設情況下，支援jsp表達式。</td>
  </tr>
  <tr>
   <td>運算式</td>
   <td>字串</td>
   <td>「已計算」DDE的表達式。 預設情況下提供的表達式評估服務支援JSP EL表達式。 可以用自定義實現替換表達式服務。</td>
  </tr>
  <tr>
   <td>值集</td>
   <td>清單</td>
   <td>枚舉類型DDE的允許值集。 例如，帳戶類型只能具有（保存，當前）值。</td>
  </tr>
  <tr>
   <td>擴展屬性</td>
   <td>物件</td>
   <td>添加到DDE（用戶介面特定或任何其他資訊）的自定義屬性的映射。</td>
  </tr>
  <tr>
   <td>必要</td>
   <td>布林值</td>
   <td>該標誌表示與資料字典對應的實例資料源必須包含此特定DDE的值。</td>
  </tr>
  <tr>
   <td>繫結</td>
   <td>綁定元素</td>
   <td>元素的XML或Java綁定。</td>
  </tr>
 </tbody>
</table>

### 計算資料字典元素 {#computedddelements}

資料字典還可以包括計算元素。 計算資料字典元素始終與表達式相關聯。 計算此表達式以在運行時獲取資料字典元素的值。 計算的DDE值是其它DDE值或文本的函式。 預設情況下，支援JSP表達式語言(EL)表達式。 EL表達式使用${ }字元，有效表達式可包括文本、運算子、變數（資料字典元素引用）和函式調用。 在引用表達式中的資料字典元素時，將使用DDE的引用名稱。 引用名稱對於資料字典中的每個資料字典元素是唯一的。

計算的DDE PersonFullName可以與EL級聯表達式關聯，如${PersonFirstName} ${PersonLastName}。

## XSD與資料字典之間的資料類型映射 {#data-type-mapping-between-xsd-and-data-dictionary-br}

導出XSD需要特定的資料映射，下表對此進行了詳細說明。 DDI列指示DDI中可用的DDE值的類型。

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>資料字典 <br /> </p> </td>
   <td>DDI（實例值資料類型）<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs：類型的元素 — 複合類型<br /> </p> </td>
   <td>DDE類型 — 複合<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:maxOccurs的元素&gt; 1<br /> </p> </td>
   <td>DDE類型 — COLLECTION-<br /> 在COLLECTION DDE旁邊建立DDE節點，該節點從父COLLECTION節點捕獲資訊。 為簡單/複合資料類型的兩個集合建立相同的集合。 每當您有類型複合的COLLECTION時，「資料字典」樹將捕獲為捕獲類型資訊而建立的DDE子代中的組成欄位。<br /> - DDE（集合）<br /> - DDE（類型資訊的複合）<br /> - DDE(STRING)欄位1<br /> - DDE(STRING)欄位2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>類型屬性 — xs:id <br /> </p> </td>
   <td>類型DDE — 字串 <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs：屬性/xs：類型的元素 — xs：字串</p> </td>
   <td>類型DDE — 字串<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:type - xs:布爾 <br /> </td>
   <td>類型DDE — 布爾型 <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs：屬性/xs：類型的元素 — xs:date </td>
   <td>類型DDE - DATE </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs：屬性/xs：類型的元素 — xs：整數 </td>
   <td>類型DDE - NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:type - xs:long</td>
   <td>類型DDE - NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs：屬性/xs：類型的元素 — xs：雙：</td>
   <td>類型DDE - NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>枚舉類型和baseType的元素 — xs:string</td>
   <td>DDE<br /> 類型 — 字串<br /> 子類型 — 枚舉<br /> valueSet - ENUM允許的值<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## 從資料字典下載示例資料檔案 {#download-a-sample-data-file-from-a-data-dictionary}

建立資料字典後，可以將其作為XML示例資料檔案下載，以在其中輸入文本。

1. 在「資料字典」頁中，按一下 **選擇** 然後點擊資料字典以選擇它。
1. 選擇 **下載示例XML資料**。
1. 點擊 **確定** 的子菜單。

   Oracle Tergement Management根據所選資料字典的結構建立XML檔案，並將其以名稱下載到您的電腦 &lt;data-dictionary-name>-SampleData。 現在，您可以在XML或文本編輯器中編輯此檔案以在 [建立字母](../../forms/using/create-letter.md)。

## 元資料的國際化 {#internationalization-of-meta-data}

當您希望以不同語言向客戶發送相同的字母時，您可以本地化資料字典和資料字典元素的顯示名稱、說明和枚舉值集。

### 本地化資料字典 {#localize-data-dictionary}

1. 在「資料字典」頁上，按一下 **選擇** 然後點擊資料字典以選擇它。
1. 點擊 **下載本地化資料**。
1. 點擊 **確定** 在警報中。 Tergement Management將一個zip檔案下載到您的電腦，其名稱為DataDictionary-&lt;ddname>.zip。
1. Zip檔案包含一個.properties檔案。 此檔案定義下載的資料字典。 屬性檔案的內容與以下內容類似：

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   屬性檔案的結構為資料字典的說明和顯示名稱以及資料字典中的每個資料字典元素定義一行。 此外，屬性檔案為每個資料字典元素的枚舉值集定義一行。 與資料字典一樣，相應的屬性檔案可以具有多個資料字典元素定義。 此外，檔案可以包含一個或多個枚舉值集的定義。

1. 要在不同的區域設定中更新.properties檔案，請更新檔案中的顯示名稱和說明值。 為要本地化的每種語言建立更多檔案實例。 只支援法語、德語、日語和英語。

1. 使用以下名稱保存不同的已更新屬性檔案：

   _fr_FR.properties法文

   _de_DE.properties德語

   _ja_JA.properties日文

   _en_EN.properties英語

1. 將.properties檔案（或多個區域設定的檔案）存檔到單個.zip檔案中。

1. 在「資料字典」頁中，選擇 **更多** > **上載本地化資料** 並選擇包含本地化屬性檔案的zip檔案。
1. 要查看本地化更改，請更改瀏覽器區域設定。

## 資料字典驗證 {#ddvalidations}

資料字典編輯器在建立或更新資料字典時強制執行以下驗證。

* 在資料字典中，只允許將複合類型作為頂級元素。
* 在葉級別不允許使用複合元素和集合元素。 葉級別只允許使用基元(String、Date、Number、Boolean)元素。 此驗證確保沒有沒有子DDE的複合和集合元素。
* 上載XSD檔案以建立資料字典時，資料字典編輯器會提示輸入頂級元素（如果存在多個元素）以建立資料字典。
* 名稱是資料字典的唯一必需參數。
* 父DDE（複合）不能有兩個同名的子代
* 確保僅當DDE不是必需參數時，才標籤DDE。 無法計算所需元素，也不能需要計算元素。 此外，「集合」和「複合元素」不能是計算元素。
* 確保DDE是必需的，僅當DDE未計算時。 它還確保它不是表示集合類型的「collectionElement」（即集合元素的唯一子代）。
* 資料字典或DDE的extendedProperties中不允許空鍵或重複鍵。
* 請勿在擴展屬性的鍵或值中使用冒號(:)或垂直條(|)字元。 沒有驗證這些禁止字元的使用。

在資料字典級別應用的驗證

* 資料字典名稱不能為空。
* 資料字典名稱只能包含字母數字字元。
* 資料字典中的子元素清單不得為空。
* 資料字典不能包含多個頂級資料字典元素。
* 在資料字典中，只允許將複合類型作為頂級元素。

在資料字典元素級別應用的驗證。

* 所有DDE名稱不能為Null且不能包含空格。
* 所有DDE必須具有「not null/non null」元素類型。
* 所有DDE引用名稱不能為Null。
* 所有DDE引用名稱必須唯一。
* 所有DDE引用只能包含字母數字字元和「_」。
* 所有DDE顯示名稱只能包含字母數字字元和「_」。
* 在葉級別不允許使用複合元素和集合元素。 葉級別只允許使用基元(String、Date、Number、Boolean)元素。 此驗證確保沒有沒有子DDE的複合和集合元素。
* 複合父DDE不能有兩個同名的子元素。
* ENUM子類型僅用於String和Number元素。
* 無法計算集合和複合元素。
* DDE不能同時計算和必需。
* 計算的DDE必須包含有效的表達式。
* 計算的DDE不能具有XML綁定。
* 不能計算或要求表示集合DDE類型的DDE。
* 子類型ENUM的DDE不能包含null或空值集。
* 集合DDE的XML綁定不能映射到屬性。
* XML綁定語法必須有效，例如，只顯示一個@，只有在跟著屬性名稱時才允許使用@。

## 將資料字典元素映射到XML架構 {#mappingddetoschema}

您可以從XML架構建立資料字典，或使用「資料字典」用戶介面生成資料字典。 資料字典中的所有資料字典元素(DDE)都具有XML綁定欄位，用於將DDE綁定儲存到XML架構中的元素。 每個DDE中的綁定相對於父DDE。

以下詳細資訊示例模型和代碼示例，它們顯示資料字典的實現詳細資訊。

## 映射簡單（基元）元素 {#mapping-simple-primitive-elements}

基元DDE表示在本質上是原子的欄位或屬性。 在複雜類型（複合DDE）或重複元素（集合DDE）的範圍之外定義的基元DDE可以儲存在XML架構中的任何位置。 與基元DDE對應的資料的位置不依賴於其父DDE的映射。 基元DDE使用XML綁定欄位中的映射資訊來確定其值，並且映射轉換為以下值之一：

* 屬性
* 元素
* 文本上下文
* 無（忽略的DDE）

以下示例顯示了一個簡單模式。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **資料字典元素** | **預設XML綁定** |
|---|---|
| 年齡 | /年齡 |
| 價格 | /價格 |

### 映射複合元素 {#mapping-composite-elements}

組合元素不支援綁定，如果提供綁定，則忽略它。 所有原始類型的組成子DDE的綁定必須是絕對的。 允許對複合DDE的子元素進行絕對映射在XPath綁定方面提供了更大的靈活性。 將複合DDE映射到XML架構中的複雜類型元素，會限制其子元素的綁定範圍。

以下示例顯示注釋的架構。

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>資料字典元素</strong></td>
   <td><strong>預設XML綁定</strong></td>
  </tr>
  <tr>
   <td>附註</td>
   <td>空(null)<br /> </td>
  </tr>
  <tr>
   <td>至</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>從</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>/note/標題</td>
  </tr>
  <tr>
   <td>體</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### 映射集合元素 {#mapping-collection-elements}

收集元素僅映射到基數> 1的另一個收集元素。 集合DDE的子DDE具有與其父XML綁定相關的（本地）XML綁定。 由於集合元素的子DDE必須與父代的基數相同，因此相對綁定必須確保基數約束，以便子DDE不指向非重複的XML架構元素。 在以下示例中，「TokenID」的基數必須與其父集合DDE的「Tokens」相同。

將集合DDE映射到XML架構元素時：

* 與集合元素對應的DDE綁定必須是絕對XPath

* 不為表示集合元素類型的DDE提供綁定。 如果提供，則將忽略綁定。

* 集合元素的所有子DDE的綁定必須相對於父集合元素。

下面的XML架構聲明了名為Tokens的元素和「unbounded」的maxOccurs屬性。 因此，Tokens是集合元素。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

與此示例關聯的Token.xsd為：

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **資料字典元素** | **預設XML綁定** |
|---|---|
| 根 | 空(null) |
| 令牌 | /根/令牌 |
| 構成 | 空(null) |
| 令牌ID | 令牌ID |
| 標籤文本 | 空(null) |
| 標籤標題 | TokenText/TextHeading |
| 令牌正文 | TokenText/TextBody |
