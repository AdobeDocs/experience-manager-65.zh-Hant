---
title: 建立HTML5表單的CSS樣式
seo-title: Creating CSS styles for HTML5 forms
description: 了解如何修改與HTML表單元素相關聯的CSS類別，以變更HTML5表單的外觀。
seo-description: Learn how to change the appearance of HTML5 forms by modifying the CSS class associated with the HTML form element.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 3%

---

# 建立HTML5表單的CSS樣式 {#creating-css-styles-for-html-forms}

HTML5型XFA表單範本的轉譯包含數個HTML元素。 這些元素按順序排列。 每個元素都有定義良好的CSS類別。 您可以使用這些CSS類別來選取和變更元素的外觀。

>[!NOTE]
>
>在CSS類別中，請勿變更寬度、高度、邊框粗細、上、左、右、下、邊框間距、邊界以及其他位置和大小屬性的值。 位置和大小屬性中的任何變更都會對表單的版面配置造成變更。

## 元素的CSS類  {#css-classes-nbsp-for-elements-nbsp}

每個元素都包含定義良好的CSS類別。 您可以修改這些類以更改元素的外觀。 除欄位和繪製元素外，每個元素都有兩個CSS類 — Type類和Name類。

* 此 **類型類** 代表XFA欄位的類型。 您可以覆寫 `type` 類，修改特定類型的所有元素的樣式。

* 此 **名稱類** 與XFA欄位的名稱對應。 您可以覆寫 `name` 類，以修改自定義樣式並將其應用於元素。

>[!NOTE]
>
>某些XFA元素沒有名稱。 要更改此類元件的樣式，請修改該特定類型的所有元件。

對於在AEM Forms設計工具中未命名的頁面，HTML5表單中的頁面會以其數量的遞增順序命名。 例如，對於含有兩頁的HTML5表單，頁面名為Page1、Page2。

## 欄位元素 {#field-element}

欄位元素包含兩個巢狀元素：介面工具集和註解。

**介面工具集元素**

介面工具集元素包含與使用者互動的使用者介面元素。 它有三個CSS類：

* **介面工具集**:每個小部件都有這個類。
* **名稱**:隨AEM提供的所有Widget都包含Widget名稱類。 對於自訂介面工具集，介面工具集開發人員提供介面工具集名稱類。
* **type**:每個Widget都有一個使用者介面元素。 此類定義用戶介面元素的類型。

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

除了type和name類別，欄位元件也包含另一個名為的CSS類別 **子類型**. 子類型標識其是哪種類型的欄位，例如NumericField、DateField、TextField。 您可以改寫子類型類，以修改所有類型、子類型欄位的樣式。

## 不同元件的CSS類 {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>名稱</strong></td>
  </tr>
  <tr>
   <td>Page</td>
   <td>頁面</td>
   <td>用戶定義的名稱<br /> 或<br /> 頁面&lt;pagenumber&gt; （預設）</td>
  </tr>
  <tr>
   <td>內容區域</td>
   <td>contentrea</td>
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
   <td>繪圖</td>
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
   <td>介面</td>
   <td>介面工具集開發人員會加以定義（針對使用者定義的介面工具集，請參閱下節中的表格）</td>
  </tr>
 </tbody>
</table>

## 不同欄位的CSS類 {#css-classes-for-different-fields}

AEM Forms設計工具支援不同類型的欄位，如數值欄位、小數欄位和日期欄位。 HTML中的所有這些欄位都包含上述的CSS類別。 視欄位類型而定，它們也包含一些額外類別。

每個欄位都有一個代表UI元素的關聯Widget。 下面列出了每個欄位的類和與每個欄位關聯的小部件。

<table>
 <tbody>
  <tr>
   <td><strong>欄位類型</strong></td>
   <td><strong>子類型</strong></td>
   <td><strong>介面工具集名稱</strong></td>
   <td><strong>介面工具集類型</strong></td>
   <td><strong>HTMLUI標籤</strong></td>
  </tr>
  <tr>
   <td>按鈕<br type="_moz" /> </td>
   <td>不適用</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=按鈕<br type="_moz" /> </td>
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
   <td>輸入類型=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>輸入類型=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>小數欄位<br type="_moz" /> </td>
   <td>數場<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>下拉式清單<br type="_moz" /> </td>
   <td>選擇者<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>選擇介面工具集<br type="_moz" /> </td>
   <td>選取</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>選擇者<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>選擇介面工具集<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>數值欄位<br type="_moz" /> </td>
   <td>數場<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=密碼<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>放射場<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radifieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>時間欄位<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>輸入類型=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同繪製元素的CSS類 {#css-classes-for-different-draw-elements}

您可以使用AEM Forms設計工具插入靜態繪圖元素，如文字和影像。 對於每個繪圖元素，單獨的CSS類與該元素相關聯。 下面列出了用於繪製元素的CSS類清單。 每個繪製元素都有一個與其關聯的繪製類。

| **繪圖類型** | **CSS 類別** |
|---|---|
| 文字 | text |
| 影像 | 影像 |
| 矩形 | 矩形 |
| Line | 折線圖 |

## 為表單的其他部分設定樣式 {#styling-other-parts-of-the-form}

除了HTML表單中的UI元件外觀之外，您還可以更改元素的樣式，如「內嵌錯誤」、「內嵌警告」和包含驗證錯誤的欄位。

`Styling Inline Errors`

驗證欄位時產生錯誤時，當使用中的欄位時，會顯示內嵌錯誤。 若要變更內嵌錯誤的樣式，請覆寫CSS ID **error-msg**.

`Styling Inline Warnings`

驗證欄位時產生警告時，當欄位處於作用中狀態時，會顯示內嵌警告。 若要變更這些內嵌警告的樣式，請覆寫CSS ID **warning-msg**.

`Styling Fields with Validation Errors`

欄位驗證失敗時，介面工具集的樣式會變更。 此樣式變更是透過套用CSS類別來完成 **widgetError** 在widget元件上。 要修改預設樣式，請覆蓋 **widgetError** 類別。
