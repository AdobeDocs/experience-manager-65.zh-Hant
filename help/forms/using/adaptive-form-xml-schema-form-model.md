---
title: 如何使用XML架構建立自適應Forms?
description: 瞭解如何將XML架構用作自適應表單中的表單模型。 您可以應用現有XSD模板來建立自適應表單，並將架構元素從XSD拖放到自適應表單上。 使用XML架構的示例進行更深入的挖掘，使用XML架構向欄位添加特殊屬性，並限制自適應表單元件的可接受值。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 35d5859f-54c4-4d14-9c64-0d9291ef9029
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 3%

---

# 使用XML架構建立自適應表單 {#creating-adaptive-forms-using-xml-schema}

## 必備條件 {#prerequisites}

使用XML架構作為其表單模型來創作自適應表單需要對XML架構有基本的瞭解。 此外，建議在本文之前閱讀以下內容。

* [建立自適應窗體](creating-adaptive-form.md)
* [XML架構](https://www.w3.org/TR/xmlschema-2/)

## 將XML架構用作表單模型 {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] 支援使用現有XML架構作為表單模型建立自適應表單。 此XML架構表示組織中後端系統生成或使用資料的結構。

使用XML架構的主要功能是：

* XSD的結構在自適應表單的創作模式下的「內容查找器」頁籤中顯示為樹。 您可以將元素從XSD層次結構拖放到自適應表單中。
* 可以使用與關聯方案相容的XML預填充表單。
* 在提交時，用戶輸入的資料將作為與關聯架構對齊的XML提交。

XML架構由簡單和複雜的元素類型組成。 元素具有向元素添加規則的屬性。 當這些元素和屬性被拖到自適應表單上時，它們將自動映射到相應的自適應表單元件。

XML元素與自適應表單元件的映射如下：

<table>
 <tbody>
  <tr>
   <th><strong>XML元素或屬性 </strong></th>
   <th><strong>自適應表單元件</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>文本框</td>
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
   <td>數字框</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>日期選取器</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>下拉</td>
  </tr>
  <tr>
   <td>任何複雜類型元素</td>
   <td>面板</td>
  </tr>
 </tbody>
</table>

## 示例XML架構 {#sample-xml-schema}

這是XML架構的示例。

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
>確保XML架構只有一個根元素。 不支援具有多個根元素的XML架構。

## 使用XML架構向欄位添加特殊屬性 {#adding-special-properties-to-fields-using-xml-schema}

可以將以下屬性添加到XML架構元素中，以將特殊屬性添加到關聯自適應表單的欄位中。

<table>
 <tbody>
  <tr>
   <th><strong>架構屬性</strong></th>
   <th><strong>在自適應窗體中使用</strong></th>
   <th><strong>支援 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>將欄位標籤為必填<br /> </td>
   <td>屬性</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>添加預設值</td>
   <td>元素和屬性</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>指定最小發生次數</p> <p>(對於可重複子表單（複雜類型）)</p> </td>
   <td>元素（複雜類型）</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>指定最大發生次數</p> <p>(對於可重複子表單（複雜類型）)</p> </td>
   <td>元素（複雜類型）</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>將架構元素拖動到自適應窗體時，將生成預設標題：
>
>* 正在大寫元素名稱的第一個字元
>* 在駱駝大小寫邊界處插入空白。
>
>例如，如果 `userFirstName` 模式元素，在自適應窗體中生成的標題為 `User First Name`。

## 限制自適應表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

可以將以下限制添加到XML架構元素中，以限制自適應表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 架構屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>Component</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最大位數。 指定的位數必須大於零。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上限。 預設情況下，包括最大值。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器<br /> </li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的下界。 預設情況下，包括最小值。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則在窗體元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，則在表單元件中指定的數值或日期必須小於或等於為maximum屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則在窗體元件中指定的數值或日期必須大於為minimum屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須大於或等於為最小值屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數字框</li>
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
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最大字元數。 最大長度必須大於零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的字元數。 長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最大小數位數。 fractionDigits必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li> 具有資料類型浮點或小數的數字框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元的順序。 如果字元符合指定的模式，則元件將接受字元。</p> <p>該模式屬性映射到相應自適應表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD架構的所有自適應表單元件 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 常見問題 {#frequently-asked-questions}

**如何知道樹中的哪個元素與哪個XML元素關聯？**

按兩下Content Finder中的元素時，彈出窗口將顯示欄位名和名為 `bindRef`。 此屬性將樹元素映射到架構中的元素或屬性。

![XML架構元素的bindref欄位](assets/dblclick.png)

bindRef</code> 欄位顯示樹元素與架構中的元素或屬性之間的關聯。

>[!NOTE]
>
>屬性具有 `@` 符號 `bindRef`值以將它們與元素區分開。 比如說， `/config/projectDetails/@duration`。

**為什麼無法為可重複子表單拖動子表單（從任何複雜類型生成的結構）的單個元素（minOccours或maxOccurs值大於1）?**

在可重複子窗體中，必須使用「完成」子窗體。 如果只需要選擇欄位，請使用整個結構並刪除不需要的欄位。

**我在Content Finder中有一個很長的複雜結構。 如何找到特定元素？**

您有兩個選擇：

* 滾動瀏覽樹結構
* 使用「搜索」框查找元素

**什麼是bindRef?**

A `bindRef` 是自適應表單元件與模式元素或屬性之間的連接。 它決定了 `XPath` 其中，從此元件或欄位捕獲的值在輸出XML中可用。 A `bindRef`在從預填充（預填充）XML中預填充欄位值時也使用。
