---
title: 為HTML5窗體建立CSS樣式
seo-title: Creating CSS styles for HTML5 forms
description: 瞭解如何通過修改與HTML表單元素關聯的CSS類來更改HTML表單的外觀。
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

# 為HTML5窗體建立CSS樣式 {#creating-css-styles-for-html-forms}

基於XFA的表單模板的HTML5格式副本由若干HTML元素組成。 這些元件按順序排列。 每個元素都有定義良好的CSS類。 可以使用這些CSS類來選擇和更改元素的外觀。

>[!NOTE]
>
>在CSS類中，不要更改寬度、高度、邊框厚度、頂部、左側、右側、底部、填充、邊距以及其他位置和大小屬性的值。 位置和大小屬性的任何更改都會對表單的佈局進行更改。

## 元素的CSS類  {#css-classes-nbsp-for-elements-nbsp}

每個元素都包含定義良好的CSS類。 可以修改這些類以更改元素的外觀。 除欄位和繪圖元素外，每個元素都有兩個CSS類 — Type類和Name類。

* 的 **類型類** 表示XFA欄位的類型。 您可以覆蓋 `type` 類以修改特定類型的所有元素的樣式。

* 的 **名稱類** 與XFA欄位的名稱相對應。 您可以覆蓋 `name` 類，以修改元素並將自定義樣式應用於元素。

>[!NOTE]
>
>某些XFA元素沒有名稱。 要更改此類元件的樣式，請修改該特定類型的所有元件。

對於在AEM Forms設計器中未命名的頁面，以HTML5窗體中的頁面按其編號的遞增順序命名。 例如，對於具有兩頁的HTML5表單，頁名為Page1、Page2。

## 欄位元素 {#field-element}

欄位元素包含兩個嵌套元素：小部件和標題。

**構件元素**

構件元素包含用於與用戶交互的用戶介面元素。 它有三個CSS類：

* **小部件**:每個小部件都有這個類。
* **名稱**:隨附的所有小部件AEM都包含小部件名稱類。 對於自定義小部件，小部件開發人員提供小部件名稱類。
* **類型**:每個小部件都有一個用戶介面元素。 此類定義用戶介面元素的類型。

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

除類型和名稱類外，欄位元件還包含另外一個名為 **子**。 子類型標識它是哪種類型的欄位，例如NumericField、DateField和TextField。 您可以覆蓋子類型類以修改類型、子類型的所有欄位的樣式。

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
   <td>孔雀屬</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>子窗體</td>
   <td>子窗體</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>排除組</td>
   <td>excl群</td>
   <td>用戶定義的名稱</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>畫</td>
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
   <td>構件</td>
   <td>小部件開發人員定義它（對於用戶定義的小部件，請參閱下節中的表）</td>
  </tr>
 </tbody>
</table>

## 不同欄位的CSS類 {#css-classes-for-different-fields}

AEM Forms設計器支援NumericField、DecimalField和Date Field等表單中的不同類型的欄位。 HTML中的所有這些欄位都包含上述CSS類。 它們還包含一些附加類，具體取決於欄位類型。

每個欄位都有一個代表UI元素的關聯小部件。 下面列出了每個欄位的類和與每個欄位關聯的小部件。

<table>
 <tbody>
  <tr>
   <td><strong>欄位類型</strong></td>
   <td><strong>子類型</strong></td>
   <td><strong>小部件名稱</strong></td>
   <td><strong>構件類型</strong></td>
   <td><strong>HTMLUI標籤</strong></td>
  </tr>
  <tr>
   <td>按鈕<br type="_moz" /> </td>
   <td>不適用</td>
   <td>xfa按鈕<br type="_moz" /> </td>
   <td>按鈕欄位小部件<br type="_moz" /> </td>
   <td>輸入類型=按鈕<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>檢查按鈕<br type="_moz" /> </td>
   <td>檢查框欄位<br /> </td>
   <td>Xfa複選框<br type="_moz" /> </td>
   <td>檢查框域構件<br type="_moz" /> </td>
   <td>輸入類型=複選框<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期欄位<br type="_moz" /> </td>
   <td>datefield（日期欄位）<br type="_moz" /> </td>
   <td>日期欄位<br type="_moz" /> </td>
   <td>日期域構件<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期時間欄位<br type="_moz" /> </td>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本域構件</td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>十進位欄位<br type="_moz" /> </td>
   <td>數域<br type="_moz" /> </td>
   <td>數字輸入<br type="_moz" /> </td>
   <td>數字域構件<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>下拉<br type="_moz" /> </td>
   <td>膽小鬼<br type="_moz" /> </td>
   <td>下拉清單小部件<br type="_moz" /> </td>
   <td>膽小器<br type="_moz" /> </td>
   <td>選擇</td>
  </tr>
  <tr>
   <td>清單框<br type="_moz" /> </td>
   <td>膽小鬼<br type="_moz" /> </td>
   <td>清單框小部件<br type="_moz" /> </td>
   <td>膽小器<br type="_moz" /> </td>
   <td>醇</td>
  </tr>
  <tr>
   <td>數字欄位<br type="_moz" /> </td>
   <td>數域<br type="_moz" /> </td>
   <td>數字輸入<br type="_moz" /> </td>
   <td>數字域構件<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>密碼欄位<br type="_moz" /> </td>
   <td>預設小部件<br type="_moz" /> </td>
   <td>密碼域構件<br type="_moz" /> </td>
   <td>輸入類型=密碼<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>放射場<br type="_moz" /> </td>
   <td>Xfa複選框<br type="_moz" /> </td>
   <td>放射域小組<br type="_moz" /> </td>
   <td>輸入類型=無線<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本域構件<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>時間欄位<br type="_moz" /> </td>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本欄位<br type="_moz" /> </td>
   <td>文本域構件<br type="_moz" /> </td>
   <td>輸入類型=文本<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同繪圖元素的CSS類 {#css-classes-for-different-draw-elements}

可以使用AEM Forms設計器插入靜態繪圖元素，如文本和影像。 對於每個繪製元素，一個單獨的CSS類與該元素相關聯。 下面列出了繪圖元素的CSS類清單。 每個繪圖元素都有與其關聯的繪圖類。

| **繪圖類型** | **CSS 類別** |
|---|---|
| 文字 | text |
| 影像 | 影像 |
| 矩形 | 矩形 |
| Line | 折線圖 |

## 為窗體的其它部分設定樣式 {#styling-other-parts-of-the-form}

除了HTML窗體中UI元件的外觀外，您還可以更改元素的樣式，如「內聯錯誤」、「內聯警告」和具有驗證錯誤的欄位。

`Styling Inline Errors`

當欄位的驗證導致錯誤時，當該欄位處於活動狀態時，將顯示內聯錯誤。 要更改內聯錯誤的樣式，請覆蓋CSS ID **錯誤消息**。

`Styling Inline Warnings`

當欄位的驗證導致警告時，當欄位處於活動狀態時，將顯示內聯警告。 要更改這些內聯警告的樣式，請覆蓋CSS ID **警告消息**。

`Styling Fields with Validation Errors`

當域驗證失敗時，構件的樣式將更改。 此樣式更改是通過應用CSS類來完成的 **小部件錯誤** 在構件元件上。 要修改預設樣式，請覆蓋 **小部件錯誤** 類。
