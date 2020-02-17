---
title: 建立HTML5表格的CSS樣式
seo-title: 建立HTML5表格的CSS樣式
description: 瞭解如何修改與HTML表單元素關聯的CSS類別，以變更HTML5表單的外觀。
seo-description: 瞭解如何修改與HTML表單元素關聯的CSS類別，以變更HTML5表單的外觀。
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# 建立HTML5表格的CSS樣式 {#creating-css-styles-for-html-forms}

以XFA為基礎的表單範本的HTML5轉譯由數個HTML元素組成。 這些元件按順序排列。 每個元素都有定義良好的CSS類別。 您可以使用這些CSS類別來選取和變更元素的外觀。

>[!NOTE]
>
>在CSS類別中，請勿變更寬度、高度、邊框粗細、頂端、左、右、底部、填補空間、邊界和其他位置與大小屬性的值。 位置和大小屬性的任何變更都會對表單的版面配置造成變更。

## 元素的CSS類別 {#css-classes-nbsp-for-elements-nbsp}

每個元素都包含定義良好的CSS類別。 您可以修改這些類以更改元素的外觀。 除了欄位和繪圖元素之外，每個元素都有兩個CSS類別- Type class和Name class。

* Type **類** ，表示XFA欄位的類型。 您可以覆寫類 `type` 別，以修改特定類型的所有元素的樣式。

* Name **類** ，與XFA欄位的名稱相對應。 您可以覆寫類 `name` 別，以修改自訂樣式並套用至元素。

>[!NOTE]
>
>某些XFA元素沒有名稱。 要更改此類元件的樣式，請修改該特定類型的所有元件。

對於未在AEM Forms Designer中命名的頁面，HTML5表單中的頁面會依其數目的遞增順序命名。 例如，對於具有兩頁的HTML5表單，頁面名稱為Page1, Page2。

## 欄位元素 {#field-element}

欄位元素包含兩個巢狀元素：介面工具集和標題。

**介面工具集元素**

介面工具集元素包含與使用者互動的使用者介面元素。 它有三個CSS類別：

* **介面工具集**:每個小部件都有此類。
* **名稱**:AEM隨附的所有Widget都包含Widget名稱類別。 對於自訂介面工具集，介面工具集開發人員會提供介面工具集名稱類別。
* **類型**:每個Widget都有使用者介面元素。 此類定義用戶介面元素的類型。

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

除了type和name類別外，欄位元件也包含另一個名為subtype的CSS **類別**。 子類型可識別其是何種類型的欄位，例如NumericField、DateField、TextField。 您可以覆蓋子類型類以修改所有類型欄位的樣式，子類型。

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
   <td>使用者定義的名稱<br /> 或<br /> Page&lt;pageNumber&gt;（預設值）</td>
  </tr>
  <tr>
   <td>內容區域</td>
   <td>contentarea</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>子表單</td>
   <td>子表單</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>排除群組</td>
   <td>exclgroup</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>繪製</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>欄位</td>
   <td>欄位</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>插圖標題</td>
   <td>caption</td>
   <td>不適用</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>介面工具集</td>
   <td>介面工具集開發人員會定義它（若需使用者定義的介面工具集，請參閱下節中的表格）</td>
  </tr>
 </tbody>
</table>

## 不同欄位的CSS類別 {#css-classes-for-different-fields}

AEM Forms Designer支援不同類型的欄位，例如NumericField、DecimalField和Date Field。 HTML中的這些欄位都包含上述的CSS類別。 它們還包含一些額外類，具體取決於欄位的類型。

每個欄位都有一個代表UI元素的關聯介面工具集。 每個欄位的類和與每個欄位關聯的Widget列在下面。

<table>
 <tbody>
  <tr>
   <td><strong>欄位類型</strong></td>
   <td><strong>子類型</strong></td>
   <td><strong>介面工具集名稱</strong></td>
   <td><strong>介面工具集類型</strong></td>
   <td><strong>HTML UI標籤</strong></td>
  </tr>
  <tr>
   <td>按鈕<br type="_moz" /> </td>
   <td>不適用</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>按鈕域widget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=複選框<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期欄位<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>數字場<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>數字域widget<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>選擇<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>sect</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>選擇<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>數字場<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>數字域widget<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>密碼<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>密碼widget<br type="_moz" /> </td>
   <td>輸入類型=密碼<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>放射場<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>放射場widget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同繪圖元素的CSS類別 {#css-classes-for-different-draw-elements}

您可以使用AEM Forms Designer插入靜態繪圖元素，例如文字和影像。 對於每個繪圖元素，會有個別的CSS類別與該元素相關聯。 繪圖元素的CSS類別清單列於下方。 每個繪圖元素都有一個與之關聯的繪圖類。

| **繪圖類型** | **CSS 類別** |
|---|---|
| 文字 | 文字 |
| 影像 | 影像 |
| 矩形 | 矩形 |
| Line | 折線圖 |

## 為表單的其他部分設定樣式 {#styling-other-parts-of-the-form}

除了HTML表單中的UI元件外觀，您還可以變更元素的樣式，例如「內嵌錯誤」、「內嵌警告」和具有驗證錯誤的欄位。

`Styling Inline Errors`

當欄位驗證導致錯誤時，在作用中的欄位時會顯示內嵌錯誤。 若要變更內嵌錯誤的樣式，請覆寫CSS ID **error-msg**。

`Styling Inline Warnings`

當欄位驗證產生警告時，當欄位處於作用中時，會顯示內嵌警告。 若要變更這些內嵌警告的樣式，請覆寫CSS ID **warning-msg**。

`Styling Fields with Validation Errors`

當欄位驗證失敗時，介面工具集的樣式會變更。 此樣式變更是透過在Widget元件上套用CSS **類別WidgetError** 來完成。 若要修改預設樣式，請覆寫 **widgetError類** 。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
