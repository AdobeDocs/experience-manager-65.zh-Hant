---
title: HTML5表單的Picture子句支援
seo-title: HTML5表單的Picture子句支援
description: HTML5表單支援XFA Picture子句，用於日期、文字和數值符號的顯示值和格式化值。
seo-description: HTML5表單支援XFA Picture子句，用於日期、文字和數值符號的顯示值和格式化值。
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# HTML5表單的Picture子句支援 {#picture-clause-support-for-html-forms}

HTML5表單支援XFA Picture子句，用於日期、文字和數值符號的顯示值和格式化值。 支援以下Picture子句表達式：

* category(locale){picture-clause}| category(locale){picture-clause}| category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobile Forms不支援Edit Picture子句。 此外，DateTime和Time Picture子句符號也不受支援。

## 支援的日期欄位符號 {#supported-date-field-symbols}

支援的Date Picture子句表達式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause符號}

>[!NOTE]
>
>picture子句的預設模式是{MMM D, YYYY}模式。 如果未應用陣列，則使用預設陣列。

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th>解釋</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月1-或2位數(1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月01-31個零填充兩位數。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1或2位數(1-12)的月份。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>每年0.01至12個月，填補零位。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>目前地區設定的縮寫月份名稱<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>目前地區設定的完整月份名稱<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>目前地區設定的縮寫工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>目前地區設定的完整工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2位數的年份，其中00 = 2000, 29 = 2029, 30 = 1930, 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4位數年份<br /> </td>
  </tr>
 </tbody>
</table>

## Numeric Picture子句 {#numeric-picture-clause}

HTML5表格支援數值圖片符號。 不過，PDF表單和HTML表單的支援有所不同。

在 **PDF Forms**&#x200B;中，數字的格式化與Picture子句中符號的數目無關

在 **HTML Forms**&#x200B;中，只有當數字小於Picture子句中符號數時，才會格式化數字。

**範例**:請考慮Picture子句：num{zzz,zzz,zz9}。

編號 **10000** ，在HTML和PDF表 **單中都格式化為10,000** 。

編號1000000的PDF格式為1,000,000。 但是，在HTML Forms中，數字仍未格式化為100000。

**HTML Forms中Numeric Picture子句的支援運算式** :

* num.integer{}
* num.decimal{}
* num.currency{}
* num.%{}
* num{Numeric Picture子句符號}

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th><strong>解釋</strong></th>
   <th>輸入剖析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>輸出格式</strong>:一位數。 或者，若輸入資料空白或位於對應位置的空格，則為零位。<br /> </td>
   <td>單位數</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>輸出格式</strong>:一位數。 或者，如果輸入資料為空，則對應位置中的空格、空格或零位。<br /> </td>
   <td>單位或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>輸出格式</strong>:一位數。 或者，如果輸入資料是空的、空的或者對應位置的零位，則不用考慮。<br /> </td>
   <td>一位數或零</td>
  </tr>
  <tr>
   <td>錯誤</td>
   <td><strong>輸出格式</strong>:由指數符號(E)組成的浮點數的指數部分。 後面接著可選的加號或減號。 後跟指數值。<br /> </td>
   <td>與輸出格式相同</td>
  </tr>
  <tr>
   <td>CR或CR<br /> </td>
   <td>信用符號(CR)（若數字為負數）。 否則就沒有。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>輸出格式：如果數字為負數，則為減號。 其他空間。<br /> </td>
   <td>如果數字為負數，則減號。 加號（如果數字為正數）</td>
  </tr>
  <tr>
   <td>V</td>
   <td>當前地區設定的小數基數。 允許在輸入剖析時隱含小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>當前地區設定的小數基數。 允許在輸入解析和輸出格式時隱含小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>當前地區設定的小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>,(U+FF0C)</td>
   <td>通用地區設定的分組分隔符號</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$(U+FF04)</td>
   <td>主要地區的貨幣符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>%(U+FF05)</td>
   <td>當前地區設定的百分比符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>((U+FF08)</td>
   <td>如果數字為負數，則使用左括弧。 其他空間。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>)(U+FF09)</td>
   <td>如果數字為負數，則右括弧。 其他空間。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Tab字元</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 文本圖片子句 {#text-picture-clause}

HTML5表單支援下列Text Picture子句運算式：

* text{text Picture子句符號}

| **符號** | **解釋** |
|---|---|
| A | 單字母字元。 |
| X | 單一字元。 |
| O | 單一英數字元。 |
| 0（零） | 單一英數字元。 |
| 9 | 一位數。 |

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
