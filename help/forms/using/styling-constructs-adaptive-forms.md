---
title: 自適應表單的樣式構造
seo-title: Styling constructs for adaptive forms
description: 使用LESS框架定制自適應表單的外觀。
seo-description: Use LESS framework to customize appearance of adaptive forms.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Adaptive Forms
exl-id: 691608a6-be82-4d81-b876-427de997e5be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 3%

---

# 自適應表單的樣式構造{#styling-constructs-for-adaptive-forms}

## 必備條件 {#prerequisites}

瞭解CSS和LESS框架。

## 可定製的內容 {#what-can-be-customized}

文章列出了可公開使用的自適應表單的css類。 您可以利用這些類來設計自適應表單的各種元件的樣式。 創作元件的樣式，如顯示警告的對話框和狀態欄超出了本文的範圍。 僅當無法使用樣式元件時，才使用這些樣式結構建立樣式（使用CSS或更少） [主題編輯器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)。

## 在自適應表單中自定義樣式 {#customizing-styles-in-adaptive-forms}

LESS框架簡化了用例，以自適應形式定制樣式。 該框架允許您使用一組變數和函式（混合）定義樣式。 LESS框架有助於減少捆綁代碼的大小並增加其可重用性。

可以通過以下方式自定義自適應窗體樣式：

* 更改主題
* 更改元件的樣式

## 更改主題 {#changing-theme}

您可以更改自適應表單的主題以確保其外觀與嵌入自適應表單的網頁一致。

使用CSS屬性的自適應表單總體外觀的更改通常是主題更改的一部分。 對「確定和感覺自適應表單」的主要更改，例如對元件佈局和放置位置的更改，不視為主題更改。

根據引導，以下一組CSS屬性定義網頁的主題：

* 背景色彩
* 邊框（類型、顏色、厚度）
* 字型色彩
* 邊距
* 邊距
* 字型大小
* 行高

當前，LESS變數僅針對自適應形式中各元素的這些屬性進行定義。

## 更改元件樣式 {#changing-component-style}

可以更改元素的外觀、佈局、定位和可見性。 要完成此任務，請建立或更新自定義.css檔案，以包括本文中列出的樣式結構。

要將樣式應用於自適應表單，請在中開啟自適應表單進行編輯，開啟自適應表單容器的屬性，在基本頁籤中指定自定義CSS檔案的路徑。 自適應表單的預設樣式構造，並用自定義.css檔案中列出的構造覆蓋。

## 元件 {#components}

本文中討論的元件具有其預定義的CSS類。 可以編輯變數以修改CSS類中的樣式。 或者，可以重寫整個類。 本節介紹可使用變數修改的元件和樣式中的類。

## 容器樣式 {#container-styling}

容器是頂級元件。 其它面板和欄位位於容器元件下。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數說明</strong></p> </td>
   <td><p><strong>變數說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>容器的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>容器的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>容器的邊距</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>容器的字型顏色</p> </td>
  </tr>
 </tbody>
</table>

## 欄位樣式 {#field-styling}

自適應表單包括各種類型的欄位。 每個欄位都有一個唯一的類名，即欄位的名稱。 該欄位還具有公用類名 `guideFieldNode`。

欄位包括標籤、小部件、幫助說明（長說明和短說明）和欄位幫助表徵圖（問號）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>欄位的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>欄位錯誤消息的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>欄位錯誤消息的字型大小</p> </td>
  </tr>
 </tbody>
</table>

## 標籤樣式 {#label-styling}

HTML元素 **標籤** 用於欄位的類包括 **左** 或 **頂** 取決於標籤是位於頂部還是左側。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>欄位標籤的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>欄位標籤的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>欄位標籤的CSS行高屬性 </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>欄位標籤的CSS字型粗細屬性 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>欄位標籤的邊距</p> </td>
  </tr>
 </tbody>
</table>

標籤的CSS規則使用 **guideFieldLabel** 的子菜單。 如果您是作者，請覆蓋此規則以使自定義更改可見。

## 小部件樣式 {#widgets-styling}

小部件還包括類，具體取決於類型。 通常，小部件包括 `guideFieldWidget` 類。 附帶HTML的小部件通常使用標準HTML要素輸入和選擇。 樣式也相應地進行。 不能通過更改變數來設定自定義小部件的樣式。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 <code></code></strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>小部件的背景顏色（複選框和單選按鈕不工作）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>小部件的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>小部件的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>小部件的邊框半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>小部件的邊框類型</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>小部件邊框的焦點類型</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>小部件的合併邊框樣式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>小部件內文本的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>小部件內文本的大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>小部件的CSS行高屬性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>構件的CSS填充屬性</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>小部件處於焦點時的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>強制欄位的小部件的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>強制欄位的小部件的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>禁用欄位時小部件的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>禁用欄位時小部件的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>禁用欄位時小部件的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>小部件的高度（複選框和單選按鈕不工作）</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>複選框和單選按鈕的高度。</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>多選下拉清單的最大高度</p> </td>
  </tr>
 </tbody>
</table>

### 小部件樣式中的限制 {#limitations-in-widget-styling}

聚焦、強制和禁用欄位的樣式使用變數進行限制。 但是，可以通過覆蓋樣式來更改它。 使用變數的限制主要是為了保持變數數的檢查。 如果欄位的出現由於處於前面討論的任何狀態而發生顯著變化，則可以放寬限制。

## 幫助說明 {#help-description}

作者可以使用「短」和「長」說明元件在欄位中指定「幫助」內容。 兩個元件都具有公用類 `.guideHelpDescription` 另一個班 `.long`/ `.short`，具體取決於說明類型。 「幫助」內容包含在段落元素中，以覆蓋說明的樣式。 使用以widgetshelp開頭的變數修改幫助說明（長和短），如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>小部件的背景顏色長幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>小部件的邊框顏色長幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>小部件的左指示器邊框顏色的長幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>小部件的短幫助的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>小部件的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>小部件的短工具提示的背景顏色幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>小部件的短工具提示的字型顏色幫助</p> </td>
  </tr>
 </tbody>
</table>

## 條款和條件 {#terms-and-conditions}

條款和條件(TnC) `` ``)小部件，用於指定條款和條件。 可以使用下表中描述的變數自定義小部件。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>未訪問的tnc連結的字型顏色。</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>訪問的tnc連結的字型顏色。</td>
  </tr>
 </tbody>
</table>

## 按鈕 {#button}

按鈕也是小部件。 然而，它們的造型與小件稍有不同。 在自適應表單中，下列任一項構成按鈕：

* 輸入[類型=文本]
* 按鈕
* 帶有類.butt的元素

HTML代碼按鈕：

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>提供按鈕的表徵圖</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>樣式按鈕標籤/標題</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 <code></code></strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>按鈕的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>邊框類型</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>按鈕的CSS填充屬性</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>填充大按鈕（類為.buttonlarge的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小按鈕的填充（類為.buttonsmall的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>資訊按鈕（具有類.buttoninformity的按鈕）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>資訊按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>資訊按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告樣式按鈕的背景顏色（具有類.buttonwarning的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告樣式按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告樣式按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>警報按鈕的背景顏色（具有類.buttonalert的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>警報按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>警報按鈕的邊框顏色</p> </td>
  </tr>
 </tbody>
</table>

## 問號 {#question-mark}

對於小部件，當作者在「幫助」內容中添加長說明時，將顯示問號。 使用引導中提供的預設表徵圖。 要使用自定義表徵圖，可以自定義引導表徵圖。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>表徵圖的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>滑鼠懸停在表徵圖上方時表徵圖的顏色</p> </td>
  </tr>
 </tbody>
</table>

## 表格 {#table}

可以使用以下變數更改表中標題行和正文行的顏色主題。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>標題行的背景顏色。 預設值為 <code>#333</code>。<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>奇數正文行的背景顏色。 預設值為 <code>rgb(255, 255, 255)</code>。</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>偶數正文行的背景顏色。 預設值為 <code>#eee</code>。</p> </td>
  </tr>
 </tbody>
</table>

## 檔案附件 {#file-attachment}

使用自適應表單的「檔案附件」小部件可以上載檔案。 也可以使用變數自定義小部件。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>小部件中顯示的檔案的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>檔案項的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>上邊框的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>檔案項的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>小部件中預覽表徵圖(Bootstrap表徵圖)的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>檔案項的注釋高度</p> </td>
  </tr>
 </tbody>
</table>

## 導航器樣式 {#navigator-styles}

導航頁籤有四種類型。 這些頁籤包括左側、頂部、嚮導中的頁籤和折疊面板。 每個導航器都有不同的類。

<table>
 <tbody>
  <tr>
   <td><p><strong>導航器</strong></p> </td>
   <td><p><strong>CSS 類別</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion導航器</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab導航器 — 垂直</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab導航器</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.嚮導導航器</p> </td>
  </tr>
 </tbody>
</table>

以下是頁籤導航器元素的HTML代碼（與引導頁籤類似）:

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

可以使用CSS規則更改導航器的樣式，這些規則使用 **後代** 選擇器。 例如，要向錨點標籤添加文本裝飾樣式：

頂部的頁籤導航器：

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

此外，還根據標籤導航器是否具有嵌套/子導航器/子導航器，為樣式標籤導航器（左和上）提供類。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有嵌套/子導航器/子導航器的頁籤導航器（左和上）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>沒有嵌套/子導航器/子導航器的頁籤導航器（左和上）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon類為頁籤導航器（左和上）和嚮導導航器提供預設表徵圖。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>通過在創作表單示例的面板上提供CSS類，可以更改特定導航器的表徵圖 &lt;class_name>。 添加 **&lt;class_name>導航** 的子菜單。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>頁籤導航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>整個頁籤導航器的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>頁籤的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>頁籤的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>懸停時頁籤的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>懸停時頁籤的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>當面板處於焦點時的背景顏色（活動）</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>當面板處於焦點時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成表達式返回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成表達式返回true時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>當面板已聚焦一次但完成表達式返回false時，背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>當面板已聚焦一次但完成表達式返回false時，字型顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>頁籤的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>頁籤的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>頁籤的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>頁籤的邊距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>垂直制表符的邊距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>頁籤的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>制表符的最小高度</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>嵌套頁籤的縮進</p> </td>
  </tr>
  <tr>
   <td><p><strong>嚮導導航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>整個嚮導導航器的背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>嚮導的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>嚮導的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>當面板處於焦點時的背景顏色（活動）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>當面板處於焦點（聚焦）時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成表達式返回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成表達式返回true時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>當面板焦點一次但完成表達式返回false時，背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>當面板已聚焦一次但完成表達式返回false時，字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>嚮導的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>嚮導的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>嚮導的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>嚮導的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>嚮導導航器項目符號的邊框顏色（預定標題/標籤）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>嚮導導航器進度欄的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>進度欄的填充顏色</p> </td>
  </tr>
  <tr>
   <td><p><strong>手風琴導航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>手風琴的填充</p> </td>
  </tr>
 </tbody>
</table>

## 面板樣式 {#panel-styling}

面板包括可選工具欄及其內容。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>面板的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>面板文本的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>面板文本的字型顏色<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>在面板內填充</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>面板說明的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>面板說明的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>面板幫助的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>面板幫助的指示器邊框顏色</p> </td>
  </tr>
 </tbody>
</table>

面板節點被分為導航器和內容。 在那裡 `` `` 不是內容的單獨樣式元件。 所述變數將應用於導航器和內容。

最上面的面板(RootPanel)沒有此類。

## 移動式造型 {#mobile-styling}

## 標題欄 {#header-bar}

這些變數影響移動設備或小螢幕設備上可見的標題欄，這些設備包含面板標題以及下一和後導航器。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>標題欄的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>標題欄中文本的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>標題欄的填充</p> </td>
  </tr>
 </tbody>
</table>

## 滾動指示器 {#scroll-indicator}

這些變數影響滾動指示器，該指示器是顯示在移動設備或小螢幕設備上的橙色箭頭。 「滾動」指示器指示螢幕的可見部分之外有內容。 你可以向下滾動查看它。 當您到達內容結尾時，箭頭將消失。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>陰囊底部固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>陰囊器右側固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>陰囊寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>陰囊高度</p> </td>
  </tr>
 </tbody>
</table>

## 移動固定工具欄佈局特定變數 {#mobile-fixed-toolbar-layout-specific-variables}

下表中的這些變數會影響移動固定工具欄佈局。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別 </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>從底部固定工具欄在移動設備上的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>從頂部固定工具欄在移動設備上的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>固定工具欄的左側位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>工具欄的固定位置，從右到右</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>工具欄按鈕表徵圖的固定位置，從頂部</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>移動設備上工具欄按鈕表徵圖的寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>移動設備上工具欄按鈕表徵圖的高度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>移動設備上工具欄的背景顏色</p> </td>
  </tr>
 </tbody>
</table>

## 主題特定變數 {#theme-specific-variable}

的 **簡單註冊** /etc/clientlibs/fd/af/guidetheme/simpleEnrollment和類別中的主題 `guide.theme.simpleEnrollment` 並引入幾個變數。 如果要建立增強簡單註冊的主題，可以使用以下「附加變數：

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>焦點按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>懸停時按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>按鈕半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>導航按鈕的背景顏色（後/後）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>懸停時導航按鈕（後/後）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>首次呈現嚮導導航器和相應進度欄的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>當前/活動嚮導導航器和相應進度欄的背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>已訪問的嚮導導航器和相應進度欄的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>將容器分成導航器和面板的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左邊的制表符（制表符導航符）的底邊框顏色分隔制表符。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>導航器的嵌套/子/子導航器的背景顏色</p> </td>
  </tr>
 </tbody>
</table>
