---
title: 預填最適化表單欄位
seo-title: Prefill adaptive form fields
description: 使用現有資料預填最適化表單的欄位。
seo-description: With adaptive forms, you users can prefill basic information in a form by logging in with their social profiles. This article describes how you can accomplish this.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: Adaptive Forms
exl-id: 29cbc330-7b3d-457e-ba4a-7ce6091f3836
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2169'
ht-degree: 0%

---

# 預填最適化表單欄位{#prefill-adaptive-form-fields}

## 簡介 {#introduction}

您可以使用現有資料預先填寫最適化表單的欄位。 使用者開啟表單時，會預填這些欄位的值。 若要在最適化表單中預填資料，請以符合預填適用性表單資料結構的格式，將使用者資料以預填XML/JSON的形式提供。

## 預填資料的結構 {#the-prefill-structure}

最適化表單可以混合綁定和未綁定欄位。 系結欄位是從「內容尋找器」標籤拖曳而包含非空白的欄位 `bindRef` 屬性值（在「編輯」欄位中）。 未綁定欄位直接從Sidekick的元件瀏覽器拖動，且為空 `bindRef` 值。

您可以預填適用性表單的綁定和未綁定欄位。 預填資料包含afBoundData和afUnBoundData區段，以預填適用性表單的綁定和未綁定欄位。 此 `afBoundData` 小節包含綁定欄位和面板的預填資料。 此資料必須與關聯的表單模型架構相容：

* 針對使用 [XFA表單範本](../../forms/using/prepopulate-adaptive-form-fields.md)，請使用與XFA範本資料結構相容的預填XML。
* 針對適用性表單，使用 [XML架構](#xml-schema-af)，請使用與XML架構結構相容的預填XML。
* 針對適用性表單，使用 [JSON結構](#json-schema-based-adaptive-forms)，請使用符合JSON結構的預填JSON。
* 對於使用FDM結構的適用性表單，請使用與FDM結構相容的預填JSON。
* 適用於具有 [無表單模型](#adaptive-form-with-no-form-model)，則沒有綁定的資料。 每個欄位都是未綁定的欄位，使用未綁定的XML預填。

### 預填XML結構示例 {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 預填JSON結構範例 {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

對於具有相同綁定欄位或具有相同名稱的未綁定欄位，在XML標籤或JSON對象中指定的資料將填充到所有欄位中。 例如，表單中的兩個欄位會對應至名稱 `textbox` 填入資料。 在執行階段中，如果第一個文字方塊欄位包含「A」，則會自動填入第二個文字方塊中的「A」。 此連結稱為適用性表單欄位的即時連結。

### 使用XFA表單範本的最適化表單 {#xfa-based-af}

預填XML和針對XFA適用性表單提交的XML結構如下：

* **預填XML結構**:預填XFA適用性表單的XML必須與XFA表單範本的資料架構相容。 要預填未綁定的欄位，請將預填的XML結構包裝為 `/afData/afBoundData` 標籤。

* **已提交的XML結構**:當未使用預填XML時，提交的XML包含中綁定和未綁定欄位的資料 `afData` 包裝函式標籤。 如果使用預填XML，則提交的XML的結構與預填XML的結構相同。 如果預填XML以 `afData` 根標籤，輸出XML也具有相同的格式。 如果預填XML沒有 `afData/afBoundData`包裝，而是直接從結構根標籤(如 `employeeData`，提交的XML也會以 `employeeData` 標籤。

Prefill-Submit-Data-ContentPackage.zip

[取得檔案](assets/prefill-submit-data-contentpackage.zip)
包含預填資料和已提交資料的範例

### 基於XML架構的最適化表單  {#xml-schema-af}

基於XML架構的最適化表單預填XML和提交XML的結構如下：

* **預填XML結構**:預填XML必須與關聯的XML架構相容。 要預填未綁定的欄位，請將預填的XML結構包裝到/afData/afBoundData標籤中。
* **已提交的XML結構**:如果未使用預填XML，則提交的XML包含中綁定和未綁定欄位的資料 `afData` 包裝函式標籤。 如果使用預填XML，則提交的XML與預填XML的結構相同。 如果預填XML以 `afData` 根標籤，則輸出XML的格式相同。 如果預填XML沒有 `afData/afBoundData` 包裝函式，而是直接從結構根標籤(例如 `employeeData`，提交的XML也會以 `employeeData` 標籤。

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

對於模型為XML架構的欄位，資料會預先填入 `afBoundData` 標籤，如下列範例XML所示。 它可用於使用一個或多個未綁定的文本欄位預先填寫最適化表單。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>建議不要在系結面板中使用未系結的欄位（具有非空白的面板） `bindRef` 是從Sidekick或「資料來源」標籤拖曳元件而建立)。 這可能導致這些未綁定欄位的資料丟失。 此外，建議在表單中，欄位名稱是唯一的，特別是非綁定欄位。

#### 沒有afData和afBoundData包裝函式的範例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON結構型適用性表單 {#json-schema-based-adaptive-forms}

針對以JSON結構為基礎的適用性表單，預填JSON和已提交JSON的結構說明如下。 如需詳細資訊，請參閱 [使用JSON結構建立最適化表單](../../forms/using/adaptive-form-json-schema-form-model.md).

* **預填JSON結構**:預填JSON必須符合相關的JSON結構。 或者，如果您也想預填未綁定的欄位，可以將其包裝到/afData/afBoundData對象中。
* **已提交的JSON結構**:如果未使用預填JSON，則提交的JSON會包含afData包裝函式標籤中已系結和未系結欄位的資料。 如果使用預填JSON，提交的JSON結構會與預填JSON相同。 如果預填JSON的開頭為afData根物件，則輸出JSON的格式會相同。 如果預填JSON沒有afData/afBoundData包裝函式，而是直接從結構根物件（例如使用者）開始，則提交的JSON也會從使用者物件開始。

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

若是使用JSON結構描述模型的欄位，資料會預先填入afBoundData物件，如下方範例JSON所示。 它可用於使用一個或多個未綁定的文本欄位預先填寫最適化表單。 以下是資料的範例，其中 `afData/afBoundData` 包裝器：

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

以下範例不含 `afData/afBoundData` 包裝器：

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>在綁定面板中使用未綁定的欄位（具有非空的bindRef的面板，這些面板是通過從Sidekick或Data Sources頁簽中拖動元件而建立的） **not** 建議使用，因為這可能會造成未綁定欄位的資料遺失。 建議在表單中使用唯一的欄位名稱，尤其是未綁定欄位。

### 沒有表單模型的適用性表單 {#adaptive-form-with-no-form-model}

若為沒有表單模型的適用性表單，所有欄位的資料位於 `<data>` 標籤 `<afUnboundData> tag`.

另外，請注意以下事項：

系統會使用欄位名稱，產生針對針對各種欄位提交之使用者資料的XML標籤。 因此，欄位名稱必須是唯一的。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 使用Configuration Manager配置預填服務 {#configuring-prefill-service-using-configuration-manager}

若要啟用預填服務，請在AEM Web主控台設定中指定預設預填服務設定。 使用下列步驟來設定預填服務：

>[!NOTE]
>
>預填服務設定適用於最適化表單、HTML5表單和HTML5表單集。

1. 開啟 **[!UICONTROL Adobe Experience Manager Web主控台設定]** 使用URL:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. 搜尋並開啟 **[!UICONTROL 預設預填服務配置]**.

   ![預填配置](assets/prefill_config_new.png)

1. 輸入資料位置，或輸入 **資料檔案位置**. 有效資料檔案位置的範例包括：

   * file:///C:/Users/public/Document/Prefill/。&#42;
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >依預設，所有類型的適用性Forms（XSD、XDP、JSON、FDM，且無表單模型）都允許透過crx檔案預填。 僅允許預填JSON和XML檔案。

1. 現在已為您的表單設定預填服務。

   >[!NOTE]
   >
   >crx通訊協定會處理預填的資料安全性，因此預設允許。 使用一般規則運算式預先填入其他通訊協定可能會造成漏洞。 在設定中，指定保護資料的安全URL設定。

## 可重複面板的奇特案例 {#the-curious-case-of-repeatable-panels}

一般而言，系結（表單結構）和未系結欄位是以相同的最適化表單撰寫，但若系結可重複，以下是幾個例外：

* 使用XFA表單範本、XSD、JSON結構或FDM結構的適用性表單不支援未結束的可重複面板。
* 請勿在系結的可重複面板中使用未系結欄位。

>[!NOTE]
>
>根據經驗，如果綁定欄位和未綁定欄位在由最終用戶填寫的未綁定欄位中相交，則不要混合這些欄位。 如果可能，您應修改架構或XFA表單範本，並為未綁定欄位添加一個條目，這樣它就會被綁定，其資料也可以像提交資料中的其他欄位一樣使用。

## 預填使用者資料的支援通訊協定 {#supported-protocols-for-prefilling-user-data}

使用有效的規則運算式設定時，可透過下列通訊協定，以預填資料格式預先填入使用者資料：

### crx://協定 {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的節點必須具有名為的屬性 `jcr:data` 並保存資料。

### file://協定  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

引用的檔案必須位於同一伺服器上。

### https://協定 {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service://協定 {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME表示OSGI預填服務的名稱。 請參閱 [建立並執行預填服務](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER是指OSGI預填服務擷取預填資料所需的任何中繼資料。 登入使用者的識別碼是可使用的中繼資料範例。

>[!NOTE]
>
>不支援傳遞驗證參數。

### 在slingRequest中設定資料屬性 {#setting-data-attribute-in-slingrequest}

您也可以設定 `data` 屬性 `slingRequest`，其中 `data` 屬性是包含XML或JSON的字串，如以下范常式式碼所示（範例為XML）:

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

您可以撰寫包含所有資料的簡單XML或JSON字串，並在slingRequest中加以設定。 您可以在任何元件的轉譯器JSP中輕鬆完成這項作業，您可在其中設定slingRequest資料屬性的頁面中納入這些元件。

例如，您想要以特定類型的標題為頁面進行特定設計。 要達到此目的，您可以自行撰寫 `header.jsp`，您可將其納入頁面元件中，並設定 `data` 屬性。

另一個好的範例是您想要透過Facebook、Twitter或LinkedIn等社交帳戶預先填入登入資料的使用案例。 在這種情況下，可以在 `header.jsp`，會從使用者帳戶擷取資料並設定資料參數。

prefill-page component.zip

[取得檔案](assets/prefill-page-component.zip)
頁面元件中的範例prefill.jsp

## AEM Forms自訂預填服務 {#aem-forms-custom-prefill-service}

在您經常從預先定義的來源讀取資料的情況下，可以使用自訂預填服務。 預填服務會從定義的資料來源讀取資料，並以預填資料檔案的內容預填最適化表單的欄位。 也可協助您將預先填入的資料與最適化表單建立永久關聯。

### 建立並執行預填服務 {#create-and-run-a-prefill-service}

預填服務是OSGi服務，並透過OSGi套件組合封裝。 您可以建立OSGi套件組合、上傳並安裝至AEM Forms套件組合。 開始建立套件組合之前：

* [下載AEM Forms Client SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
* 下載模板套件

* 將資料（預填資料）檔案放入crx-repository。 您可以將檔案放置在crx-repository的\contents資料夾中的任何位置。

[取得檔案](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 建立預填服務 {#create-a-prefill-service}

模板套件（範例預填服務套件）包含AEM Forms預填服務的範例實作。 在程式碼編輯器中開啟模板套件。 例如，在Eclipse中開啟模板專案以進行編輯。 在程式碼編輯器中開啟模板套件後，請執行下列步驟以建立服務。

1. 開啟src\main\java\com\adobe\test\Prefill.java檔案進行編輯。
1. 在程式碼中，設定值：

   * `nodePath:` 指向crx-repository位置的節點路徑變數包含資料（預填）檔案的路徑。 例如， /content/prefilldata.xml
   * `label:` 標籤參數指定服務的顯示名稱。 例如，預設預填服務

1. 儲存並關閉 `Prefill.java` 檔案。
1. 新增 `AEM Forms Client SDK` 封裝至模板專案的建置路徑。
1. 編譯專案並為套件組合建立.jar。

#### 啟動並使用預填服務 {#start-and-use-the-prefill-service}

若要啟動預填服務，請將JAR檔案上傳至AEM Forms Web Console，然後啟用服務。 現在，服務會開始出現在最適化表單編輯器中。 將預填服務與最適化表單關聯：

1. 在Forms編輯器中開啟最適化表單，然後開啟「表單容器」的「屬性」面板。
1. 在「屬性」主控台中，導覽至「AEM Forms容器>基本>預填服務」。
1. 選擇預設預填服務，然後按一下 **[!UICONTROL 儲存]**. 服務與表單相關聯。

## 在用戶端預先填入資料 {#prefill-at-client}

預填最適化表單時，AEM Forms伺服器會合併資料與最適化表單，並將已填入的表單傳送給您。 依預設，資料合併動作會在伺服器上發生。

您可以設定AEM Forms伺服器以在用戶端（而非伺服器）執行資料合併動作。 大幅縮短預填及演算最適化表單的所需時間。 預設情況下，該功能為禁用狀態。 您可以從Configuration Manager或命令行啟用它。

* 要從配置管理器中啟用或禁用，請執行以下操作：
   1. 開啟AEM Configuration Manager。
   1. 找到並開啟最適化表單與互動式通訊Web通道設定
   1. 啟用Configuration.af.clientside.datamerge.enabled.name選項
* 要從命令行啟用或禁用：
   * 若要啟用，請執行下列cURL命令：
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * 若要停用，請執行下列cURL命令：
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   若要充分利用用戶端的預填資料選項，請更新預填服務以傳回 [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) 和 [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)
