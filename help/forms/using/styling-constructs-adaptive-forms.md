---
title: 最適化表單的樣式結構
seo-title: Styling constructs for adaptive forms
description: 使用LESS架構自訂最適化表單的外觀。
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

# 最適化表單的樣式結構{#styling-constructs-for-adaptive-forms}

## 必備條件 {#prerequisites}

了解CSS和LESS架構。

## 可自訂的內容 {#what-can-be-customized}

文章列出可公開使用的適用性表單CSS類別。 您可以利用這些類別來設定最適化表單中各種元件的樣式。 製作元件的樣式（例如顯示警告的對話方塊和狀態列）不在本文的討論範圍內。 只有在您無法使用 [主題編輯器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## 在最適化表單中自訂樣式 {#customizing-styles-in-adaptive-forms}

LESS架構可簡化使用案例，以自訂最適化表單中的樣式。 架構可讓您使用一組變數和函式(mixin)來定義樣式。 LESS框架有助於減小捆綁代碼的大小並增加其可重用性。

您可以透過下列方式自訂最適化表單樣式：

* 變更主題
* 更改元件的樣式

## 變更主題 {#changing-theme}

您可以變更最適化表單的主題，確保其外觀與內嵌最適化表單的網頁一致。

使用CSS屬性而變更適用性表單的整體外觀通常是主題變更的一部分。 對「最適化表單的確定和感覺」原則的重大變更（例如元件的版面配置和位置變更），不視為主題變更。

以下一組CSS屬性會根據引導來定義網頁的主題：

* 背景色彩
* 邊框（類型、顏色、厚度）
* 字型色彩
* 邊距
* 邊距
* 字型大小
* LineHeight

目前，LESS變數僅針對適用性表單中各元素的這些屬性定義。

## 變更元件樣式 {#changing-component-style}

您可以對元素的外觀、版面、定位和可見性進行更改。 若要完成此工作，請建立或更新您的自訂.css檔案，以包含本文所列的樣式結構。

若要將樣式套用至最適化表單，請開啟中的最適化表單以進行編輯，開啟最適化表單容器的屬性，在基本索引標籤中指定自訂CSS檔案的路徑。 適用性表單的預設樣式建構，並以自訂.css檔案中所列的建構加以覆寫。

## 元件 {#components}

本文討論的元件有其預先定義的CSS類別。 您可以編輯變數以修改CSS類別中的樣式。 或者，您也可以重寫整個類。 本節介紹可使用變數修改的元件和樣式中的類。

## 容器樣式 {#container-styling}

容器是頂層元件。 其他面板和欄位位於容器元件下。

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
   <td><p>容器的邊框間距</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>容器的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>容器的字型顏色</p> </td>
  </tr>
 </tbody>
</table>

## 欄位樣式 {#field-styling}

適用性表單包含各種欄位類型。 每個欄位都有唯一的類名，即欄位的名稱。 該欄位還具有通用類名 `guideFieldNode`.

欄位包括標籤、小部件、幫助說明（包括長說明和短說明）和「域幫助」表徵圖（問號）。

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
   <td><p>欄位填補</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>欄位錯誤訊息的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>欄位錯誤消息的字型大小</p> </td>
  </tr>
 </tbody>
</table>

## 標籤樣式 {#label-styling}

HTML元素 **標籤** 用於欄位的包括類 **lef** 或 **top** 視標籤在上方還是左側而定。

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
   <td>欄位標籤的CSS字型寬度屬性 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>欄位標籤的邊界</p> </td>
  </tr>
 </tbody>
</table>

標籤的CSS規則會使用 **guideFieldLabel** 標籤。 如果您是作者，請覆寫此規則，讓您的自訂變更可見。

## 介面工具集樣式 {#widgets-styling}

視其類型而定，Widget也包含類別。 通常，介面工具集包括 `guideFieldWidget` 類別。 隨HTML提供的小部件通常使用標準HTML要素輸入並選擇。 樣式將相應地進行。 您無法變更自訂Widget的樣式。

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
   <td>小工具的背景顏色（複選框和單選按鈕無效）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>小工具的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>小工具的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>小工具的邊框半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>小工具的邊框類型</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>介面工具集邊框的焦點類型</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>小部件的合併邊框樣式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>介面工具集內的文字顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>介面工具集內的文字大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>介面工具集的CSS行高屬性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>介面工具集的CSS填充屬性</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>介面工具集聚焦時的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>強制欄位的介面工具集邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>必填欄位的介面工具集背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>禁用欄位時介面工具集的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>禁用欄位時介面工具集的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>停用欄位時介面工具集的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>介面工具集的高度（無法用於核取方塊和選項按鈕）</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>複選框和單選按鈕的高度。</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>多選下拉式清單的最大高度</p> </td>
  </tr>
 </tbody>
</table>

### 介面工具集樣式的限制 {#limitations-in-widget-styling}

焦點、必填和停用欄位的樣式會使用變數進行限制。 不過，您可以覆寫樣式來變更。 提供使用變數的限制主要是為了控制變數的數量。 如果欄位的外觀發生顯著變化，則可以放鬆限制，因為它位於先前討論的任何狀態中。

## 說明說明 {#help-description}

作者可使用簡短和長篇說明元件，在欄位中指定說明內容。 這兩個元件都有共同類別 `.guideHelpDescription` 另一類 `.long`/ `.short`，視說明類型而定。 「幫助」內容括在段落元素中，以覆蓋說明的樣式。 說明說明（長和短）是使用以widgetshelp開頭的變數來修改，如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>小部件的背景顏色的長幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>小工具的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>小工具的左指示器邊框顏色的長幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>小工具的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>小工具的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>小工具的背景顏色簡短工具提示幫助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>小工具的字型顏色簡短工具提示幫助</p> </td>
  </tr>
 </tbody>
</table>

## 條款和條件 {#terms-and-conditions}

條款與條件(TnC) `` ``)介面工具集可讓您指定條款與條件。 您可以使用下表所述的變數來自訂介面工具集。

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

按鈕也是小工具。 不過，其樣式與介面工具集稍有不同。 在最適化表單中，下列任一項皆構成按鈕：

* 輸入[類型=文字]
* 按鈕
* 元素，類別為button

按鈕的HTML代碼：

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
   <td><p>樣式按鈕標籤/註解</p> </td>
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
   <td><p>填充大按鈕（具有類.buttonlarge的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小按鈕的邊框間距（類為.buttonsmall的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>提供資訊的按鈕的背景顏色（具有類.buttoninformity的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>資訊性按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>資訊按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告樣式的按鈕（具有類.buttonwarning的按鈕）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告樣式的按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告樣式的按鈕的邊框顏色</p> </td>
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

對於介面工具集，當作者在說明內容中新增長說明時，會顯示問號。 會使用引導中提供的預設圖示。 若要使用自訂圖示，您可以自訂引導圖圖示。

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
   <td><p>圖示的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>滑鼠滑鼠暫留在表徵圖上時的顏色</p> </td>
  </tr>
 </tbody>
</table>

## 表格 {#table}

您可以使用下列變數來變更表格中標題和內文列的顏色主題。

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
   <td><p>偶體行的背景顏色。 預設值為 <code>#eee</code>。</p> </td>
  </tr>
 </tbody>
</table>

## 檔案附件 {#file-attachment}

適用性表單的「檔案附件」Widget可讓您上傳檔案。 您也可以使用變數來自訂介面工具集。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>填充介面工具集中顯示的檔案</p> </td>
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
   <td><p>介面工具集中「預覽」圖示(Bootstrap圖示)的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>檔案項的注釋高度</p> </td>
  </tr>
 </tbody>
</table>

## 導航樣式 {#navigator-styles}

有四種類型的導航標籤。 這些功能包括左側、頂端、精靈和折疊式功能表的標籤。 每個導航器都有不同的類。

<table>
 <tbody>
  <tr>
   <td><p><strong>導覽器</strong></p> </td>
   <td><p><strong>CSS 類別</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigator</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigator-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab導覽器</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigator</p> </td>
  </tr>
 </tbody>
</table>

以下是標籤導航器元素的HTML代碼（類似於引導頁簽）:

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

您可以使用CSS規則來變更導覽器的樣式，此規則會使用 **後代** 選取器。 例如，若要將文字裝飾樣式新增至錨點標籤：

頂部的頁簽導航器：

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

此外，還有可根據頁簽導航器是否嵌套/子/子導航器來設定頁簽導航器樣式的類（包括左側和頂部）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有巢狀/子/子導覽器的標籤導覽器（左側和頂部）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>沒有巢狀/子/子導覽器的標籤導覽器（左側和頂部）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon類別提供索引標籤導覽器（包括左側和頂部）和精靈導覽器的預設圖示。

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
>表單範例中，您可以在面板上提供CSS類別，以變更特定導覽器的圖示 &lt;class_name>. 您新增 **&lt;class_name>_nav** 框中。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>標籤導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>整個頁簽導航器的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>頁簽的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>頁簽的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>暫留時標籤的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>暫留時標籤的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>面板聚焦時的背景顏色（活動）</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>面板聚焦時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成運算式傳回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成運算式返回true時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>面板聚焦一次但完成運算式傳回false時的背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>面板聚焦一次但完成運算式傳回false時的字型顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>標籤的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>頁簽的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>頁簽的邊框間距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>索引標籤的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>垂直標籤的邊距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>標籤的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>制表符的最小高度</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>嵌套頁簽的縮進</p> </td>
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
   <td><p>精靈的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>嚮導的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>面板聚焦時的背景顏色（活動）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>面板聚焦時的字型顏色（聚焦）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成運算式傳回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成運算式返回true時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>面板聚焦一次但完成運算式傳回false時的背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>面板聚焦一次但完成表達式返回false時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>精靈的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>嚮導的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>嚮導的邊框間距</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>嚮導的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>嚮導導航器項目符號的邊框顏色（前置詞為註解/標籤）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>嚮導導航器進度欄的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>填充進度條的顏色</p> </td>
  </tr>
  <tr>
   <td><p><strong>折疊式面板導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>折疊式面板的邊框間距</p> </td>
  </tr>
 </tbody>
</table>

## 面板樣式 {#panel-styling}

面板包含可選工具列及其內容。

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
   <td><p>面板內填充</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>面板說明的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>面板說明的邊框間距</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>面板說明的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>面板說明的指示器邊框顏色</p> </td>
  </tr>
 </tbody>
</table>

面板節點分為導覽器和內容。 那裡 `` `` 不是內容的個別樣式元件。 描述的變數會套用在導覽器上以及內容上。

最頂端的面板(RootPanel)沒有此類。

## 行動樣式 {#mobile-styling}

## 標題列 {#header-bar}

這些變數會影響行動裝置或小型螢幕裝置上可見的標題列，這些裝置包含面板標題以及下一個和後面的導覽器。

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
   <td><p>標題欄內文本的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>標題欄的邊框間距</p> </td>
  </tr>
 </tbody>
</table>

## 捲動指示器 {#scroll-indicator}

這些變數會影響「捲動」指示器，此為顯示在行動裝置或小型螢幕裝置上的橘色箭頭。 「捲動」指標表示畫面的可見部分以外有內容。 您可以向下捲動以查看。 當您點擊內容結尾時，箭頭會消失。

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
   <td><p>從底部固定陰旋器位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>從右到右的陰旋器的固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>捲軸寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>陰囊高度</p> </td>
  </tr>
 </tbody>
</table>

## 行動版修正工具列版面專屬變數 {#mobile-fixed-toolbar-layout-specific-variables}

下表中的這些變數會影響行動固定工具列配置。

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
   <td><p>從底部固定行動裝置上的工具列位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>從上方固定行動裝置上的工具列位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>修正行動裝置上左側工具列的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>在行動裝置上，從右方固定工具列的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>從頂部固定工具欄按鈕表徵圖的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>行動裝置上工具列按鈕圖示的寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>行動裝置上工具列按鈕圖示的高度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>行動裝置上工具列的背景顏色</p> </td>
  </tr>
 </tbody>
</table>

## 主題特定變數 {#theme-specific-variable}

此 **簡單註冊** 主題（位於/etc/clientlibs/fd/af/guidetheme/simpleEnrollment和類別） `guide.theme.simpleEnrollment` 也會引入一些變數。 如果要建立增強簡單註冊的主題，可以使用以下「額外變數」：

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
   <td><p>暫留時按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>按鈕半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>導覽按鈕的背景顏色（上/下一個）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>暫留時導覽按鈕（上/下一頁）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>首次呈現時，嚮導導航器和相應進度欄的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>當前/活動嚮導導航器和相應進度欄的背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>已瀏覽的嚮導導航器和相應進度欄的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>邊框顏色分叉容器分成導航器和面板</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左側標籤的下邊框顏色分隔標籤（標籤導航器）。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>導航器的嵌套/子/子導航器的背景顏色</p> </td>
  </tr>
 </tbody>
</table>
