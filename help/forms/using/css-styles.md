---
title: 建立HTML5表單的CSS樣式
description: 瞭解如何修改與HTML表單元素相關的CSS類別，以變更HTML5表單的外觀。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 2%

---

# 建立HTML5表單的CSS樣式 {#creating-css-styles-for-html-forms}

XFA型表單範本的HTML5轉譯包含數個HTML元素。 這些元素會依順序排列。 每個元素都有已妥善定義的CSS類別。 您可以使用這些CSS類別來選取和變更元素的外觀。

>[!NOTE]
>
>在CSS類別中，請勿變更width、height、border-thickness、top、left、right、bottom、padding、margin及其他位置與大小屬性的值。 位置和大小屬性的任何變更都會對表單的版面配置造成變更。

## 元素的CSS類別  {#css-classes-nbsp-for-elements-nbsp}

每個元素都包含定義良好的CSS類別。 您可以修改這些類別來變更元素的外觀。 每個元素（欄位和繪圖元素除外）都有兩個CSS類別 — Type類別和Name類別。

* 此 **型別類別** 代表XFA欄位的型別。 您可以覆寫 `type` 類別修改特定型別之所有元素的樣式。

* 此 **名稱類別** 對應至XFA欄位的名稱。 您可以覆寫 `name` 類別來修改自訂樣式並套用至元素。

>[!NOTE]
>
>有些XFA元素沒有名稱。 若要變更這類元件的樣式，請修改該特定型別的所有元件。

對於AEM Forms Designer中未命名的頁面，HTML5表單中的頁面會依其編號的遞增順序命名。 例如，如果是具有兩個頁面的HTML5表單，這些頁面的名稱為Page1， Page2。

## 欄位元素 {#field-element}

欄位元素包含兩個巢狀元素：Widget和標題。

**Widget元素**

widget元素包含用於與使用者互動的使用者介面元素。 它有三個CSS類別：

* **Widget**：每個Widget都有這個類別。
* **名稱**：AEM隨附的所有Widget都包含Widget Name類別。 對於自訂Widget，Widget開發人員會提供Widget name類別。
* **type**：每個Widget都有使用者介面元素。 此類別會定義使用者介面元素的型別。

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

除了型別和名稱類別外，欄位元件也包含其他名為的CSS類別 **子型別**. 子型別會識別其欄位型別，例如NumericField、DateField、TextField。 您可以覆寫子型別類別，以修改型別、子型別的所有欄位的樣式。

## 不同元件的CSS類別 {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>元件</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>名稱</strong></td>
  </tr>
  <tr>
   <td>頁面</td>
   <td>頁面</td>
   <td>使用者定義的名稱<br /> 或<br /> 頁面&lt;pagenumber&gt; （預設）</td>
  </tr>
  <tr>
   <td>內容區域</td>
   <td>contentarea</td>
   <td>使用者定義的名稱</td>
  </tr>
  <tr>
   <td>子表單</td>
   <td>子表單</td>
   <td>使用者定義的名稱</td>
  </tr>
  <tr>
   <td>排除群組</td>
   <td>exclgroup</td>
   <td>使用者定義的名稱</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>使用者定義的名稱</td>
  </tr>
  <tr>
   <td>欄位</td>
   <td>欄位</td>
   <td>使用者定義的名稱</td>
  </tr>
  <tr>
   <td>輔助字幕</td>
   <td>註解</td>
   <td>不適用</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>Widget</td>
   <td>Widget開發人員會加以定義（若是使用者定義的Widget，請參閱下節中的表格）</td>
  </tr>
 </tbody>
</table>

## 不同欄位的CSS類別 {#css-classes-for-different-fields}

AEM Forms Designer支援表單中不同型別的欄位，例如「數值欄位」、「十進位欄位」和「日期欄位」。 HTML中的所有欄位都包含上述CSS類別。 它們也包含一些額外的類別，視欄位型別而定。

每個欄位都有一個代表UI元素的關聯Widget。 以下列出每個欄位的類別以及與每個欄位相關聯的Widget。

<table>
 <tbody>
  <tr>
   <td><strong>欄位型別</strong></td>
   <td><strong>子類型</strong></td>
   <td><strong>Widget名稱</strong></td>
   <td><strong>Widget 類型</strong></td>
   <td><strong>HTMLUI標籤</strong></td>
  </tr>
  <tr>
   <td>按鈕<br type="_moz" /> </td>
   <td>不適用</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>輸入型別=按鈕<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>核取按鈕<br type="_moz" /> </td>
   <td>核取方塊欄位<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期欄位<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>輸入型別=文字<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期時間欄位<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>輸入型別=文字<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>數值輸入<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>輸入型別=文字<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>下拉式清單<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>選取</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>數值欄位<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>數值輸入<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>輸入型別=文字<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>密碼欄位Widget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>無線電場<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>Radiofieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>文字欄位<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>輸入型別=文字<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>時間欄位<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>輸入型別=文字<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同繪圖元素的CSS類別 {#css-classes-for-different-draw-elements}

您可以使用AEM Forms Designer插入靜態繪圖元素，例如文字和影像。 對於每個繪圖元素，個別的CSS類別會與該元素相關聯。 以下列出用於繪製元素的CSS類別清單。 每個繪圖元素都有與其關聯的繪圖類別。

| **Draw Type** | **CSS類別** |
|---|---|
| 文字 | text |
| 影像 | 影像 |
| 矩形 | 矩形 |
| 線條 | 折線圖 |

## 設定表單其他部分的樣式 {#styling-other-parts-of-the-form}

除了HTML表單中UI元件的外觀外，您還可以變更元素的樣式，例如內嵌錯誤、內嵌警告和有驗證錯誤的欄位。

`Styling Inline Errors`

當欄位驗證導致錯誤時，當欄位處於活動狀態時會顯示內嵌錯誤。 若要變更內嵌錯誤的樣式，請覆寫CSS ID **error-msg**.

`Styling Inline Warnings`

當欄位驗證導致警告時，當欄位處於活動狀態時會顯示內嵌警告。 若要變更這些內嵌警告的樣式，請覆寫CSS ID **warning-msg**.

`Styling Fields with Validation Errors`

當欄位驗證失敗時，Widget的樣式會變更。 此樣式變更是透過套用CSS類別來完成 **widgetError** 在widget元件上。 若要修改預設樣式，請覆寫 **widgetError** 類別。
