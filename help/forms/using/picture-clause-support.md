---
title: HTML5表單的Picture子句支援
description: HTML5表單支援XFA Picture子句，用於顯示日期、文字和數值符號的值及格式化值。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 6990a68e92885fcf9b94a511e8bf5c729195849f
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# HTML5表單的Picture子句支援 {#picture-clause-support-for-html-forms}

HTML5表單支援XFA Picture子句，用於顯示日期、文字和數值符號的值及格式化值。 支援下列Picture子句運算式：

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobiles Forms不支援Edit Picture子句。 此外，不支援DateTime和Time Picture子句符號。

## 支援的日期欄位符號 {#supported-date-field-symbols}

Date Picture子句支援的運算式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture子句符號}

>[!NOTE]
>
>picture子句的預設模式為{MMM D， YYYY}模式。 如果未套用任何陣列，則會使用預設的陣列。

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th>解譯</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月的1或2位數(1-31)日</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月以零填入兩位數(01-31)的天數。<br /> </td>
  </tr>
  <tr>
   <td>一</td>
   <td>一年中的1或2位數(1-12)月份。<br /> </td>
  </tr>
  <tr>
   <td>公厘</td>
   <td>月份以零填入兩位數(01-12)。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>目前地區設定的月份名稱縮寫<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>目前地區設定的完整月份名稱<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>目前地區設定的簡化工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>目前地區設定的完整工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2位數年份，其中00 = 2000、29 = 2029、30 = 1930、99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4位數年份<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> 根據設計，HTML5 Forms中的「日期」欄位不支援 `MM-YYYY` 編輯格式的圖樣。 不過，顯示格式支援該模式。

## Numeric圖片子句 {#numeric-picture-clause}

HTML5表單支援數字圖片符號。 不過，PDF forms和HTMLForms之間的支援有所不同。

在 **PDF forms**，數字的格式與Picture子句中的符號數目無關

在 **HTMLForms**，只有在數字的位數小於Picture子句中的符號數時，才會格式化數字。

**範例**：以Picture子句為例： num{zzz，zzz，zz9}。

數字 **10000** 格式為 **10,000** 在HTML和PDF forms中。

數字1000000PDF forms格式為1,000,000。 不過，在HTMLForms中，數字仍維持未格式化為1000000。

中支援的Numeric Picture子句運算式 **HTMLForms** 為：

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture子句符號}

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th><strong>解譯</strong></th>
   <th>輸入剖析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>輸出格式</strong>：一位數。 或者，如果輸入資料為空白或對應位置有空格，則為0位數。<br /> </td>
   <td>單一數字</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>輸出格式</strong>：一位數。 或者，如果輸入資料是空的，則為空格，或對應位置中的零位數。<br /> </td>
   <td>單一數字或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>輸出格式</strong>：一位數。 或者，如果輸入資料是空的、空格或對應位置中的零位數，則無意義。<br /> </td>
   <td>一位數或無</td>
  </tr>
  <tr>
   <td>錯誤</td>
   <td><strong>輸出格式</strong>：浮點數的指數部分，由指數符號(E)組成。 後面接著選用的加號或減號。 後面接著指數值。<br /> </td>
   <td>與輸出格式設定相同</td>
  </tr>
  <tr>
   <td>CR或cr<br /> </td>
   <td>數字為負數時為貸方符號(CR)。 否則就什麼也沒有。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>輸出格式：如果數字為負數，則為負號。 其他空格。<br /> </td>
   <td>如果數字為負數，則為減號。 如果數字是正數，則加上符號</td>
  </tr>
  <tr>
   <td>V</td>
   <td>主要地區設定的十進位基數。 允許輸入剖析時隱含十進位基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>主要地區設定的十進位基數。 允許輸入剖析和輸出格式設定時隱含十進位基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>主要地區設定的十進位基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>， (U+FF0C)</td>
   <td>主要地區設定的分組分隔符號</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>主要地區設定的貨幣符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>主要地區設定的百分比符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>數字為負數時加上左括弧。 其他空格。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>數字為負數時加上右括弧。 其他空格。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>定位字元</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 文字圖片子句 {#text-picture-clause}

HTML5表單支援下列Text Picture子句運算式：

* text{text Picture子句符號}

| **符號** | **解譯** |
|---|---|
| A | 單一字母字元。 |
| X | 單一字元。 |
| O | 單一英數字元。 |
| 0 （零） | 單一英數字元。 |
| 9 | 一位數。 |
