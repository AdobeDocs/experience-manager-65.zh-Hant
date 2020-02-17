---
title: 使用XML架構建立最適化表單
seo-title: 使用XML架構建立最適化表單
description: 最適化表單可以使用XML架構做為表單模型，讓您運用現有的XSD範本來建立最適化表單。 您可以從XSD拖放架構元素至最適化表單。
seo-description: 最適化表單可以使用XML架構做為表單模型，讓您運用現有的XSD範本來建立最適化表單。 您可以從XSD拖放架構元素至最適化表單。
uuid: 84c35728-1b6c-4286-854b-51c03bfd0eac
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d6c12b3-3a70-48e9-a83b-974360a8b0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# 使用XML架構建立最適化表單{#creating-adaptive-forms-using-xml-schema}

## 必備條件 {#prerequisites}

使用XML架構製作最適化表單作為其表單模型，需要基本瞭解XML架構。 此外，建議在本文之前閱讀下列內容。

* [建立最適化表單](../../forms/using/creating-adaptive-form.md)
* [XML架構](https://www.w3.org/TR/xmlschema-2/)

## 使用XML架構作為表單模型 {#using-an-xml-schema-as-form-model}

AEM Forms支援使用現有的XML架構做為表單模型來建立最適化表單。 此XML架構代表組織中後端系統產生或使用資料的結構。

使用XML架構的主要功能包括：

* XSD的結構會在最適化表單的製作模式中，在「內容搜尋器」索引標籤中顯示為樹狀結構。 您可以從XSD階層將元素拖放並新增至最適化表單。
* 您可以使用與相關架構相容的XML預先填入表單。
* 提交時，用戶輸入的資料將作為與相關方案一致的XML提交。

XML架構由簡單而複雜的元素類型組成。 這些元素具有向元素添加規則的屬性。 當這些元素和屬性拖曳至最適化表單時，它們會自動映射至對應的最適化表單元件。

此XML元素與自適應表單元件的映射如下：

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
   <td>複選框</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>所有類型的數值</li>
    </ul> </td>
   <td>數值方塊</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>日期選擇器</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>下拉式清單</td>
  </tr>
  <tr>
   <td>任何複雜類型元素</td>
   <td>面板</td>
  </tr>
 </tbody>
</table>

## 範例XML架構 {#sample-xml-schema}

這是XML架構的範例。

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
>請確定您的XML架構只有一個根元素。 不支援具有多個根元素的XML架構。

## 使用XML架構將特殊屬性新增至欄位 {#adding-special-properties-to-fields-using-xml-schema}

您可以將以下屬性添加到XML架構元素中，以向相關自適應表單的欄位添加特殊屬性。

<table>
 <tbody>
  <tr>
   <th><strong>架構屬性</strong></th>
   <th><strong>以最適化形式使用</strong></th>
   <th><strong>支援 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>將欄位標示為必填<br /> </td>
   <td>屬性</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>新增預設值</td>
   <td>元素和屬性</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>指定最小發生次數</p> <p>(適用於可重複的子表單（複雜類型）)</p> </td>
   <td>元素（複雜類型）</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>指定最大發生次數</p> <p>(適用於可重複的子表單（複雜類型）)</p> </td>
   <td>元素（複雜類型）</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>將架構元素拖曳至最適化表單時，預設標題會由下列項目產生：
>
>* 將元素名稱的第一個字元大寫
>* 在駝峰大小寫邊界插入空格。
>
>
例如，如果您新增模式元 `userFirstName` 素，則在最適化表單中產生的標題為 `User First Name`。

## 限制最適化表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以將下列限制新增至XML架構元素，以限制最適化表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 架構屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>元件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的位數上限。 指定的位數必須大於零。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上界。 預設會包含最大值。</p> </td>
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
   <td><p>指定數值和日期的下界。 預設會包含最小值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值 (Boolean)</p> </td>
   <td><p>如果為true，則在表單元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，表單元件中指定的數字值或日期必須小於或等於為maximum屬性指定的數字值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值 (Boolean)</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須大於最小屬性指定的數值或日期。</p> <p>如果為false，表單元件中指定的數值或日期必須大於或等於為最小屬性指定的數值或日期。</p> </td>
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
   <td><p>指定元件中允許的字元數目下限。 最小長度必須等於或大於零。</p> </td>
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
   <td><p>指定元件中允許的字元數。 長度必須等於或大於零。</p> </td>
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
     <li> 具有資料類型浮點或小數的數值框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元的順序。 如果字元符合指定的模式，則元件接受字元。</p> <p>該模式屬性映射到相應自適應表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>映射至XSD架構的所有最適化表單元件 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Frequently asked questions {#frequently-asked-questions}

**我要如何知道樹中的哪個元素與哪個XML元素相關聯？**

當您連按兩下「內容搜尋器」中的元素時，快顯視窗會顯示欄位名稱和名為的屬性 `bindRef`。 此屬性將樹元素映射到方案中的元素或屬性。

![XML架構元素的bindref欄位](assets/dblclick.png)

bindRef</code> 欄位顯示樹元素與模式中的元素或屬性之間的關聯。

>[!NOTE]
>
>屬性的值 `@` 中有一個符 `bindRef`號，可以與元素區分。 例如， `/config/projectDetails/@duration`。

**為什麼我無法將子表單的個別元素（從任何複雜類型產生的結構）拖曳至可重複的子表單（minOccours或maxOccuns值大於1）?**

在可重複的子表單中，您必須使用完整的子表單。 如果您只想要選擇欄位，請使用整個結構並刪除不要的欄位。

**我在Content Finder中有很長的複雜結構。 如何尋找特定元素？**

您有兩個選項：

* 捲動樹狀結構
* 使用「搜尋」方塊尋找元素

**什麼是bindRef?**

A `bindRef` 是自適應表單元件與模式元素或屬性之間的連接。 它指定從 `XPath` 此元件或欄位捕獲的值在輸出XML中可用的位置。 從 `bindRef`預先填入（預先填入）的XML中預先填入欄位值時，也會使用。
