---
title: 對HTML5窗體的Picture子句支援
seo-title: Picture clause support for HTML5 forms
description: HTML5表單支援XFA Picture子句，用於顯示日期、文本和數字元號的顯示值和格式化值。
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

# 對HTML5窗體的Picture子句支援 {#picture-clause-support-for-html-forms}

HTML5表單支援XFA Picture子句，用於顯示日期、文本和數字元號的顯示值和格式化值。 支援以下Picture子句表達式：

* 類別（區域設定）{picture-clause} |類別（區域設定）{picture-clause} |類別（區域設定）{picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，MobilesForms不支援編輯圖片子句。 此外，不支援DateTime和Time Picture子句符號。

## 支援的日期欄位符號 {#supported-date-field-symbols}

Date Picture子句支援的表達式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture子句符號}

>[!NOTE]
>
>圖片子句的預設模式是{MMM D,YYYY}模式。 如果未應用陣列，則使用預設陣列。

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th>解釋</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月的1 — 位或2位(1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月的零補兩位數(01-31)。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>一年中的1 — 或2位(1-12)月份。<br /> </td>
  </tr>
  <tr>
   <td>毫米</td>
   <td>每年的零補兩位數(01-12)月份。<br /> </td>
  </tr>
  <tr>
   <td>嗯</td>
   <td>當前區域設定的縮寫月份名稱<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>當前區域設定的完整月名<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>當前區域設定的縮寫工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>當前區域設定的完整工作日名稱<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2位年份，其中00 = 2000, 29 = 2029, 30 = 1930, 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>年</td>
   <td>4位數年份<br /> </td>
  </tr>
 </tbody>
</table>

## 數字圖片子句 {#numeric-picture-clause}

HTML5表單支援數字圖片符號。 但是，PDF forms和HTMLForms在支援上有差異。

在 **PDF forms**，數字將被格式化，而與Picture子句中的符號數無關

在 **HTMLForms**，僅當數字的數字小於Picture子句中的符號數時，才設定數字格式。

**示例**:請考慮Picture子句：num{zz,zzz,zz9}。

數字 **10000** 格式為 **1萬** HTML和PDF forms。

數字1000000的PDF forms格式為1,000,000。 但是，在FormsHTML中，數字仍未格式化為1000000。

中支援的Numeric Picture子句表達式 **HTMLForms** 為：

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{數字圖片子句符號}

<table>
 <tbody>
  <tr>
   <th><strong>符號</strong></th>
   <th><strong>解釋</strong></th>
   <th>輸入分析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>輸出格式</strong>:一個數字。 或者，如果輸入資料為空或相應位置有空格，則對零位。<br /> </td>
   <td>單位</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>輸出格式</strong>:一個數字。 或者，如果輸入資料為空，則對於空格，或者對應位置中的零位。<br /> </td>
   <td>單位數或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>輸出格式</strong>:一個數字。 或者，如果輸入資料為空、空格或相應位置的零位，則不會有任何用處。<br /> </td>
   <td>單位數或無</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>輸出格式</strong>:由指數符號(E)組成的浮點數的指數部分。 後跟可選的加號或減號。 後跟指數值。<br /> </td>
   <td>與輸出格式相同</td>
  </tr>
  <tr>
   <td>CR或CR<br /> </td>
   <td>如果數字為負，則信用符號(CR)。 否則就沒了。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或S<br /> </td>
   <td>輸出格式：如果數字為負，則為減號。 其他空間。<br /> </td>
   <td>如果數字為負數，則減號。 如果數字為正數則加號</td>
  </tr>
  <tr>
   <td>V</td>
   <td>當前區域設定的十進位基數。 允許在輸入分析時隱含小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>當前區域設定的十進位基數。 允許在輸入分析和輸出格式設定時隱含小數基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>當前區域設定的十進位基數。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>,(U+FF0C)</td>
   <td>當前區域設定的分組分隔符</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$(U+FF04)</td>
   <td>當前區域設定的貨幣符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>%(U+FF05)</td>
   <td>當前區域設定的百分比符號。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>(U+FF08)</td>
   <td>如果數字為負，則使用左括弧。 其他空間。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>)(U+FF09)</td>
   <td>如果數字為負數，則右括弧。 其他空間。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>制表符</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 文本圖片子句 {#text-picture-clause}

HTML5表單支援以下文本圖片子句表達式：

* 文本{文本圖片子句符號}

| **符號** | **解釋** |
|---|---|
| A | 單字母字元。 |
| X | 單字元。 |
| O | 單個字母數字字元。 |
| 0（零） | 單個字母數字字元。 |
| 9 | 一位數。 |
