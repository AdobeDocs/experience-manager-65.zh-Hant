---
title: 如何使用XML結構描述建立最適化Forms？
description: 瞭解如何在最適化表單中將XML結構描述用作表單模型。 您可以套用現有的XSD範本來建立調適型表單，並從XSD將結構描述元素拖放至您的調適型表單上。 深入瞭解XML結構描述範例，使用XML結構描述將特殊屬性新增至欄位，並限制適用性表單元件的可接受值。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 35d5859f-54c4-4d14-9c64-0d9291ef9029
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 9%

---

# 使用XML結構描述建立調適型表單 {#creating-adaptive-forms-using-xml-schema}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

## 先決條件 {#prerequisites}

使用XML結構描述作為其表單模型來製作調適型表單需要基本瞭解XML結構描述。 此外，建議您先閱讀下列內容，再閱讀本文。

* [建立最適化表單](creating-adaptive-form.md)
* [XML結構描述](https://www.w3.org/TR/xmlschema-2/)

## 使用XML結構描述作為表單模型 {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] 支援使用現有XML結構描述作為表單模型來建立調適型表單。 此XML結構描述代表組織中的後端系統產生或使用資料的結構。

使用XML結構描述的主要功能如下：

* XSD的結構在最適化表單的製作模式中，會以樹狀結構顯示在「內容尋找器」標籤中。 您可以從XSD階層拖曳元素並新增至最適化表單。
* 您可以使用與關聯結構描述相容的XML預先填入表單。
* 提交時，使用者輸入的資料會以符合關聯結構描述的XML格式提交。

XML結構描述包含簡單和複雜的元素型別。 元素具有將規則新增至元素的屬性。 將這些元素和屬性拖曳至最適化表單時，會自動對應至對應的最適化表單元件。

這種具有最適化表單元件的XML元素對應如下：

<table>
 <tbody>
  <tr>
   <th><strong>XML元素或屬性 </strong></th>
   <th><strong>最適化表單元件</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>文字方塊</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>核取方塊</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>所有型別的數值</li>
    </ul> </td>
   <td>數值方塊</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>日期挑選器</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>下拉式清單</td>
  </tr>
  <tr>
   <td>任何複雜型別的元素</td>
   <td>面板</td>
  </tr>
 </tbody>
</table>

## 範例XML結構描述 {#sample-xml-schema}

以下是XML結構描述的範例。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>確定您的XML結構描述只有一個根元素。 不支援具有多個根元素的XML結構描述。

## 使用XML結構描述新增特殊屬性至欄位 {#adding-special-properties-to-fields-using-xml-schema}

您可以將下列屬性新增至「XML結構描述」元素，以將特殊屬性新增至相關聯的最適化表單的欄位。

<table>
 <tbody>
  <tr>
   <th><strong>結構描述屬性</strong></th>
   <th><strong>在最適化表單中使用</strong></th>
   <th><strong>支援 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>標籤欄位為必填<br /> </td>
   <td>屬性</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>新增預設值</td>
   <td>元素和屬性</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>指定最小出現次數</p> <p>(適用於可重複的子表單（複雜型別）)</p> </td>
   <td>元素（複雜型別）</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>指定最大發生次數</p> <p>(適用於可重複的子表單（複雜型別）)</p> </td>
   <td>元素（複雜型別）</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>將結構描述元素拖曳至最適化表單時，會產生預設標題：
>
>* 將元素名稱的第一個字元轉換為大寫
>* 在駝峰式大小寫邊界插入空格。
>
>例如，如果您將 `userFirstName` 結構元素中，在最適化表單中產生的標題為 `User First Name`.

## 限制最適化表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以將下列限制新增至XML結構描述元素，以限制最適化表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 結構描述屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>元件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最大位數。 指定的位數必須大於零。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上限。 預設會包含最大值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器<br /> </li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的下限。 預設會包含最小值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須小於或等於為maximum屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須大於針對minimum屬性指定的數值或日期。</p> <p>若為false，則表單元件中指定的數值或日期必須大於或等於針對minimum屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最小字元數。 最小長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最大字元數。 最大長度必須大於零。</p> </td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許字元的確切數量。 長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的小數位數上限。 fractionDigits必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li> 資料型別為浮點數或小數的數值方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元順序。 如果字元符合指定的模式，元件會接受字元。</p> <p>pattern屬性對應至對應的最適化表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>對應至XSD結構描述的所有調適型表單元件 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 常見問題 {#frequently-asked-questions}

**我如何知道樹狀結構中的哪個元素與哪個XML元素相關聯？**

在「內容尋找器」中按兩下元素時，快顯視窗會顯示欄位名稱和屬性，稱為 `bindRef`. 此屬性會將樹狀元素對應至結構描述中的元素或屬性。

![XML結構描述元素的bindref欄位](assets/dblclick.png)

此 <code>bindRef</code> 欄位顯示樹狀元素與結構描述中元素或屬性之間的關聯。

>[!NOTE]
>
>屬性具有 `@` 符號在其中 `bindRef`值，以便與元素加以區分。 例如，`/config/projectDetails/@duration`。

**我為何無法為可重複的子表單（minOccours或maxOccurs值大於1）拖曳子表單的個別元素（由任何複雜型別產生的結構）？**

在可重複的子表單中，您必須使用「完成」子表單。 如果您只想使用選擇性欄位，請使用整個結構並刪除不需要的結構。

**我在內容尋找器中有個長而複雜的結構。 如何尋找特定元素？**

您有兩個選項：

* 捲動瀏覽樹狀結構
* 使用搜尋方塊來尋找元素

**什麼是bindRef？**

A `bindRef` 最適化表單元件與結構元素或屬性之間的連線。 它會指定 `XPath` 其中從這個元件或欄位擷取的值可在輸出XML中使用。 A `bindRef`從預先填入（預先填入）的XML預先填入欄位值時，也會使用。
