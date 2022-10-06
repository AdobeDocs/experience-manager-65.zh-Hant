---
title: HTML5表單的子句支援
seo-title: Picture clause support for HTML5 forms
description: HTML5表單支援XFA Picture子句，用於顯示值，以及日期、文本和數字元號的格式化值。
seo-description: HTML5 forms supports XFA Picture clause for display value and formatted value for date, text, and numeric symbols.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# HTML5表單的子句支援 {#picture-clause-support-for-html-forms}

HTML5表單支援XFA Picture子句，用於顯示值，以及日期、文本和數字元號的格式化值。 支援以下子句表達式：

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobiles Forms不支援Edit Picture子句。 此外，不支援DateTime和Time Picture子句符號。

## 支援的日期欄位符號 {#supported-date-field-symbols}

支援的Date Picture子句表達式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture子句符號}

>[!NOTE]
>
>圖片子句的預設模式為{MMM D, YYYY}模式。 如果未應用模式，則使用預設模式。

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th>解釋</th>
  </tr>
  <tr>
   <td>D</td>
   <td>當月1天或2位數(1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>月中的零補兩位數(01-31)。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1 — 或2位數(1-12)的月份。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>0補兩位數(01-12)的月份。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>當前地區的縮寫月名<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>當前區域設定的整月名稱<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>當前地區的縮寫工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>當前地區設定的完整工作日名稱<br /> </td>
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

## 數值子句 {#numeric-picture-clause}

HTML5表單支援數字圖片符號。 不過，PDF forms和HTMLForms的支援有所差異。

在 **PDF forms**，則數字的格式與Picture子句中符號數無關

在 **HTMLForms**，只有數字的位數小於Picture子句中符號的數時，數字才會格式化。

**範例**:考慮Picture子句：num{zzz,zzz,zz9}。

數字 **10000** 格式為 **1萬** 在HTML和PDF forms中。

1000000的格式為1,000,000PDF forms。 不過，在HTMLForms中，數字仍未格式化為1000000。

中支援的數值圖片子句表達式 **HTMLForms** 為：

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{數值圖片子句符號}

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th><strong>解釋</strong></th>
   <th>輸入解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>輸出格式</strong>:一位數。 或者，如果輸入資料為空或對應位置有空格，則為零位。<br /> </td>
   <td>單位數</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>輸出格式</strong>:一位數。 或者，如果輸入資料為空，則空格或相應位置的零位。<br /> </td>
   <td>單位數或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>輸出格式</strong>:一位數。 或者，如果輸入資料為空、空格或對應位置的零位，則無用。<br /> </td>
   <td>一位數或無</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>輸出格式</strong>:由指數符號(E)組成的浮點數的指數部分。 後面接可選的加號或減號。 後跟指數值。<br /> </td>
   <td>與輸出格式相同</td>
  </tr>
  <tr>
   <td>CR或CR<br /> </td>
   <td>如果數字為負，則信用符號(CR)。 沒別的。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>輸出格式：如果數字為負，則為減號。 其他空間。<br /> </td>
   <td>如果數字為負，則減號。 如果數字為正數，加號</td>
  </tr>
  <tr>
   <td>V</td>
   <td>當前地區設定的十進位數。 允許在輸入解析時隱含小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>當前地區設定的十進位數。 允許在輸入解析和輸出格式設定時隱含小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>當前地區設定的十進位數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>,(U+FF0C)</td>
   <td>當前地區的分組分隔符</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$(U+FF04)</td>
   <td>當前地區的貨幣符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>%(U+FF05)</td>
   <td>當前地區的百分比符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>(U+FF08)</td>
   <td>如果數字為負，則使用左括弧。 其他空間。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>)(U+FF09)</td>
   <td>如果數字為負數，則用右括弧。 其他空間。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>定位字元</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 文本圖片子句 {#text-picture-clause}

HTML5表單支援以下文本圖片子句表達式：

* text{textPicture子句符號}

| **符號** | **解釋** |
|---|---|
| A | 單字母字元。 |
| X | 單一字元。 |
| O | 單一英數字元。 |
| 0（零） | 單一英數字元。 |
| 9 | 一位數。 |
