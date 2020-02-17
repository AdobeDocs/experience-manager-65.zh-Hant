---
title: 最適化表單的樣式構造
seo-title: 最適化表單的樣式構造
description: 使用LESS架構自訂最適化表單的外觀。
seo-description: 使用LESS架構自訂最適化表單的外觀。
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619

---


# 最適化表單的樣式構造{#styling-constructs-for-adaptive-forms}

## 必備條件 {#prerequisites}

瞭解CSS和LESS架構。

## 可自訂的內容 {#what-can-be-customized}

文章會列出可公開使用的最適化表單css類別。 您可以利用這些類別來設定最適化表單的各種元件樣式。 撰寫元件的樣式，例如顯示警告的對話方塊和狀態列，超出本文的範圍。 只有當您無法使用主題編輯器來設定元件的樣式時，才可使用這些樣式結構來建立樣 [式（使用CSS或Less）](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)。

## 自訂最適化表單中的樣式 {#customizing-styles-in-adaptive-forms}

LESS架構可簡化使用案例，以自訂最適化表單的樣式。 此架構可讓您使用一組變數和函式（混合）來定義樣式。 LESS框架有助於減少捆綁代碼的大小並增加其可重用性。

您可以以下列方式自訂最適化的表單樣式：

* 變更主題
* 更改元件的樣式

## 變更主題 {#changing-theme}

您可以變更最適化表單的主題，以確保其外觀與嵌入最適化表單的網頁一致。

使用CSS屬性變更最適化表單的整體外觀通常是主題變更的一部分。 對「最適化表單的確定與感覺」的重大變更（例如元件版面配置和位置的變更）不會視為主題變更。

以引導為基礎，下列CSS屬性集會定義網頁的主題：

* 背景色彩
* 邊框（文字、顏色、粗細）
* 字型色彩
* 邊距
* 邊距
* 字型大小
* LineHeight

目前，LESS變數僅針對自適應形式中各種元素的這些屬性進行定義。

## 變更元件樣式 {#changing-component-style}

您可以變更元素的外觀、版面、位置和可見度。 若要完成此工作，請建立或更新您的自訂。css檔案，以包含本文中所列的樣式結構。

若要將樣式套用至最適化表單，請在中開啟最適化表單以進行編輯，開啟最適化表單容器的屬性，然後在基本索引標籤中指定自訂CSS檔案的路徑。 預設最適化表單的樣式建構，並以自訂。css檔案中所列的建構值覆寫。

## 元件 {#components}

本文討論的元件有其預先定義的CSS類別。 您可以編輯變數以修改CSS類別中的樣式。 或者，您也可以重寫整個類。 本節介紹可使用變數修改的元件和樣式中的類。

## 容器樣式 {#container-styling}

容器是頂層元件。 其他面板和欄位位於容器元件下方。

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
   <td><p>容器的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>容器的字型顏色</p> </td>
  </tr>
 </tbody>
</table>

## 欄位樣式 {#field-styling}

最適化表單包括各種欄位類型。 每個欄位都有一個唯一的類名，即欄位的名稱。 該欄位還具有公用類名 `guideFieldNode`。

欄位包括標籤、Widget、說明說明（包括長篇和短篇說明）和欄位說明圖示（問號）。

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
   <td><p>欄位錯誤消息的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>欄位錯誤訊息的字型大小</p> </td>
  </tr>
 </tbody>
</table>

## 標籤樣式 {#label-styling}

用於欄 **位的** HTML元素標籤包 **含左側****** 或上側的類，視標籤位於上側或左側而定。

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
   <td><p>欄位標籤的邊界</p> </td>
  </tr>
 </tbody>
</table>

標籤的CSS規則會使用guideFieldLabel標 **簽套用** 。 如果您是作者，請覆寫此規則，讓您的自訂變更可見。

## Widget樣式 {#widgets-styling}

Widget也會依其類型而包含類別。 通常，Widget會包含 `guideFieldWidget` 類別。 隨HTML提供的Widget通常使用標準HTML元素輸入並選取。 樣式會據此進行。 您無法變更變數，以自訂介面工具集的樣式設定。

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
   <td>Widget的背景顏色（不適用於核取方塊和選項按鈕）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Widget的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Widget的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Widget的邊框半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Widget的邊框類型</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>介面工具集邊框的焦點類型</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Widget的合併邊框樣式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>介面工具集內文字的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>介面工具集內的文字大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>介面工具集的CSS線條高度屬性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>介面工具集的CSS填補屬性</p> </td>
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
   <td><p>強制欄位的介面工具集背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>停用欄位時介面工具集的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>停用欄位時介面工具集的字型顏色</p> </td>
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
   <td><p>核取方塊和選項按鈕的高度。</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>多選下拉式清單的最高高度</p> </td>
  </tr>
 </tbody>
</table>

### 介面工具集樣式限制 {#limitations-in-widget-styling}

焦點、強制和停用欄位的樣式會使用變數加以限制。 不過，您可以覆寫樣式來變更樣式。 使用變數的限制主要是為了保持變數數目的檢查。 如果場的外觀發生顯著變化，則可以放鬆限制，因為它位於前面討論的任何狀態中。

## 說明說明 {#help-description}

作者可以使用簡短和詳細說明元件，在欄位中指定說明內容。 這兩個元件都有一 `.guideHelpDescription` 個公用類 `.long`/ `.short`，具體取決於說明類型。 「說明」內容會隨附在段落元素中，以覆寫說明的樣式。 說明說明（包括長篇和短篇）會使用以widgetshelp開頭的變數來修改，如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>Widget的背景顏色長篇說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>Widget的邊框顏色長篇說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Widget的左指示符邊框顏色長說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Widget的背景顏色簡短說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Widget的字型顏色說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Widget的背景顏色簡短工具提示說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Widget的字型顏色簡短工具提示說明</p> </td>
  </tr>
 </tbody>
</table>

## Terms and Conditions {#terms-and-conditions}

「條款與條件」(TnC `` ``)介面工具集可讓您指定條款與條件。 您可以使用下表所述的變數來自訂介面工具集。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>未瀏覽的tnc連結的字型顏色。</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>已造訪的tnc連結的字型顏色。</td>
  </tr>
 </tbody>
</table>

## 按鈕 {#button}

按鈕也是Widget。 不過，其樣式與Widget略有不同。 在最適化表單中，下列任一項皆構成按鈕：

* 輸[入類型=文本]
* 按鈕
* 元素與類別。button

按鈕的HTML程式碼：

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
   <td><p>提供按鈕的圖示</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>樣式按鈕標籤／標題</p> </td>
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
   <td><p>按鈕的CSS填補屬性</p> </td>
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
   <td><p>大按鈕的間距（類別為。buttonlarge的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大型按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小按鈕的間距（類別為。buttonsmall的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>資訊按鈕的背景顏色（具有類別。buttoninforment的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>提供資訊的按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>資訊按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告樣式的按鈕的背景顏色（類別為。buttonwarning的按鈕）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告樣式化按鈕的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告樣式化按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>警報按鈕的背景顏色（具有類。buttonalert的按鈕）</p> </td>
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

## Question mark {#question-mark}

對於介面工具集，當作者在「說明」內容中新增詳細說明時，就會顯示問號。 使用引導中提供的預設表徵圖。 若要使用自訂圖示，您可以自訂引導圖示。

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
   <td><p>表徵圖顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>滑鼠停留在圖示上方時的圖示顏色</p> </td>
  </tr>
 </tbody>
</table>

## 表格 {#table}

您可以使用下列變數，變更表格標題列和內文列的色彩主題。

<table>
 <tbody>
  <tr>
   <td><p><strong>變數 </strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>標題列的背景顏色。 預設值為 <code>#333</code>。<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>奇數內文行的背景顏色。 預設值為 <code>rgb(255, 255, 255)</code>。</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>偶數內文行的背景顏色。 預設值為 <code>#eee</code>。</p> </td>
  </tr>
 </tbody>
</table>

## 檔案附件 {#file-attachment}

最適化表單的檔案附件Widget可讓您上傳檔案。 您也可以使用變數自訂介面工具集。

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
   <td><p>檔案項目的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>上邊框的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>檔案項目的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>介面工具集中「預覽」圖示（引導表徵圖）的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>檔案項目的註解高度</p> </td>
  </tr>
 </tbody>
</table>

## 導覽樣式 {#navigator-styles}

導覽標籤有四種類型。 這些頁籤包括嚮導和accordion中左側、頂部的頁籤。 每個導航器都有不同的類。

<table>
 <tbody>
  <tr>
   <td><p><strong>導覽器</strong></p> </td>
   <td><p><strong>CSS 類別</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab導覽器</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

以下是Tab導覽器元素的HTML程式碼（類似於引導標籤）:

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

您可以使用CSS規則來變更導覽器的樣式，這些規則會使用子系選擇器來選 **擇元** 素。 例如，若要新增文字裝飾樣式至錨記：

上方的標籤導覽器：

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

此外，還有類可根據索引標籤導覽器是否具有巢狀／子/子導覽器，來設定索引標籤導覽器的樣式（左側和上側）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 類別</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有巢狀／子/子導覽器的標籤導覽器（左側和上側）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>沒有巢狀／子/子導覽器的標籤導覽器（左側和上方）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon類別提供標籤導覽器（包括左側和上方）和精靈導覽器的預設圖示。

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
>您可以在製作時在面板上提供CSS類別，以&lt;CLASS_NAME>格式，來變更特定導覽器的圖示。 您可以 **為導航器的表徵圖添加&lt;CLASS_NAME>** _nav。

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
   <td><p>整個標籤導覽器的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>標籤的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>標籤的字型顏色</p> </td>
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
   <td><p>當面板處於焦點時的背景顏色（活動）</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>面板焦點時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>當面板的完成運算式傳回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>當面板的完成運算式傳回true時，字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>當面板已聚焦一次但完成運算式傳回false時的背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>當面板已聚焦一次但完成運算式傳回false時，字型顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>頁籤的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>標籤的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>頁籤的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>標籤的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>垂直標籤的邊界</p> </td>
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
   <td><p>嵌套標籤的縮排</p> </td>
  </tr>
  <tr>
   <td><p><strong>精靈導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>整個精靈導覽器的背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>精靈的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>精靈的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>當面板處於焦點時的背景顏色（活動）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>當面板處於焦點時的字型顏色（聚焦）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>當面板的完成運算式傳回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>當面板的完成運算式傳回true時，字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>當面板已聚焦一次但完成運算式傳回false時，背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>當面板已聚焦一次但完成運算式傳回false時，字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>精靈的色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>精靈的字型大小</p> </td>
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
   <td><p>精靈導覽器項目符號的邊框顏色（在標題／標籤前面加上預設）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>嚮導導航器進度欄的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>為進度列填色顏色</p> </td>
  </tr>
  <tr>
   <td><p><strong>收合式導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>accordion的填充</p> </td>
  </tr>
 </tbody>
</table>

## 面板樣式 {#panel-styling}

「面板」包含選用工具列及其內容。

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
   <td><p>面板文字的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>面板文字的字型顏色<br /> </p> </td>
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
   <td><p>面板說明的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>面板說明的指示符邊框顏色</p> </td>
  </tr>
 </tbody>
</table>

面板節點被分為導覽器和內容。 內 `` `` 容沒有單獨的樣式元件。 描述的變數會套用在導覽器和內容上。

最上方的面板(RootPanel)沒有此類。

## 行動樣式 {#mobile-styling}

## Header bar {#header-bar}

這些變數會影響行動裝置或小型螢幕裝置上可見的標題列，這些裝置包含面板標題以及下一個和後一個導覽器。

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
   <td><p>標題列的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>標題列內文字的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>標題欄的間距</p> </td>
  </tr>
 </tbody>
</table>

## 捲動指示器 {#scroll-indicator}

這些變數會影響「捲動」指示器，此指示器是顯示在行動裝置或小型螢幕裝置上的橙色箭頭。 「捲動」指示符指示螢幕的可見部分以外有內容。 您可以向下捲動以檢視。 當您按下內容結尾時，箭頭會消失。

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
   <td><p>從下到下的捲軸器固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>捲軸器右側固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>捲動器寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>捲軸器高度</p> </td>
  </tr>
 </tbody>
</table>

## 行動固定工具列版面特定變數 {#mobile-fixed-toolbar-layout-specific-variables}

下表中的這些變數會影響行動固定工具列的版面配置。

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
   <td><p>固定工具列在行動裝置上的下方位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>固定工具列在行動裝置上的位置，從上方</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>固定工具列在行動裝置上的左側位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>固定工具列在行動裝置上的右側位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>修正工具列按鈕圖示的上方位置</p> </td>
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

位於 **/etc/clientlibs/fd/af/guidetheme/simpleEnrollment的Simple enrollment** 主題和類別 `guide.theme.simpleEnrollment` 也引入了一些變數。 如果您想要建立增強簡單註冊的主題，可以使用下列「額外變數」:

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
   <td><p>導覽按鈕的背景顏色（上／下一頁）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>暫留時的導覽按鈕（上／下一頁）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>首次呈現時，精靈導覽器和對應進度列的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>當前／活動嚮導導航器和相應進度條的背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>已瀏覽的精靈導覽器和對應進度列的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>將邊框顏色分叉的容器分成導覽器和面板</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左側標籤的底部邊框顏色分隔標籤（標籤導覽器）。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>導覽器巢狀／子/子導覽器的背景顏色</p> </td>
  </tr>
 </tbody>
</table>

