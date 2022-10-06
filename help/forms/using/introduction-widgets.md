---
title: 最適化和HTML5表單的外觀架構
seo-title: Appearance framework for adaptive and HTML5 forms
description: 行動Forms會將表單範本轉譯為HTML5表單。 這些表單使用jQuery、Backbone.js和Underscore.js檔案來顯示外觀並啟用指令碼。
seo-description: Mobile Forms render Form Templates as HTML5 forms. These forms use jQuery, Backbone.js and Underscore.js files for the appearance and to enable scripting.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 2%

---

# 最適化和HTML5表單的外觀架構 {#appearance-framework-for-adaptive-and-html-forms}

Forms(適用性表單和HTML5表單)使用 [jQuery](https://jquery.com/), [骨幹.js](https://backbonejs.org/) 和 [Underscore.js](https://underscorejs.org/) 用於外觀和指令碼的庫。 表單也使用 [jQuery UI](https://jqueryui.com/) **介面工具集** 表單中所有互動式元素（例如欄位和按鈕）的架構。 此架構可讓表單開發人員在Forms中使用一組豐富的可用jQuery Widget和外掛程式。 您也可以實作表單特定邏輯，同時從使用者（例如leadDigits/trailDigits限制）擷取資料或實作圖片子句。 表單開發人員可建立並使用自訂的特色，以改善資料擷取體驗，並讓其更方便使用。

本文適用於對jQuery和jQuery Widget有充分了解的開發人員。 它提供外觀架構的洞察力，並可讓開發人員為表單欄位建立替代外觀。

外觀框架依賴各種選項、事件（觸發器）和函式來捕獲用戶與表單的交互，並響應模型更改以通知最終用戶。 此外：

* 框架提供一組用於欄位外觀的選項。 這些選項為機碼值組，分為兩個類別：常用選項和欄位類型特定選項。
* 在合約中，外觀會觸發一組事件，例如進入和退出。
* 實施一組函式時需要外觀。 有些函式是常見的，有些則是欄位類型函式專用的。

## 常見選項 {#common-options}

以下是設定的全域選項。 這些選項適用於每個欄位。

<table>
 <tbody>
  <tr>
   <th>屬性 </th>
   <th>說明</th>
  </tr>
  <tr>
   <td>名稱</td>
   <td>用於在指令碼表達式中指定此對象或事件的標識符。 例如，此屬性指定主機應用程式的名稱。</td>
  </tr>
  <tr>
   <td>值</td>
   <td>欄位的實際值。 </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>隨即顯示欄位的此值。 </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>螢幕Reader使用此值提供欄位的相關資訊旁白。 表單會提供值，您可以覆寫值。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>欄位在表單的索引標籤序列中的位置。 僅當要更改表單的預設頁簽順序時，才覆蓋tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如標題或表。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>介面工具集的高度。 以像素指定。 </td>
  </tr>
  <tr>
   <td>寬度</td>
   <td>介面工具集的寬度。 以像素指定。</td>
  </tr>
  <tr>
   <td>存取</td>
   <td>用於訪問容器對象（如子表單）的內容的控制項。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>Widget的XFA元素的para屬性。</td>
  </tr>
  <tr>
   <td>dr</td>
   <td>文字的方向。 可能的值為ltr（從左到右）和rtl（從右到左）。</td>
  </tr>
 </tbody>
</table>

除了這些選項外，框架還提供了一些其他選項，這些選項會根據欄位類型而有所不同。 欄位特定選項的詳細資訊列於下方。

### 與表單架構互動 {#interaction-with-forms-framework}

若要與表單架構互動，Widget會觸發某些事件，讓表單指令碼可運作。 如果介面工具集未擲回這些事件，則在該欄位表單中撰寫的某些指令碼將無法運作。

#### 由介面工具集觸發的事件 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Event </th>
   <th>說明</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>每當欄位聚焦時，就會觸發此事件。 它可讓「enter」指令碼在欄位上執行。 觸發事件的語法為<br /> （介面工具集）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>每當使用者離開欄位時，就會觸發此事件。 它可讓引擎設定欄位的值，並執行其「退出」指令碼。 觸發事件的語法為<br /> （介面工具集）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>觸發此事件是為了讓引擎執行寫入欄位的「變更」指令碼。 觸發事件的語法為<br /> （介面工具集）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>只要按一下欄位，就會觸發此事件。 它可讓引擎執行寫入欄位的「點按」指令碼。 觸發事件的語法為<br /> （介面工具集）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由介面工具集實作的API {#apis-implemented-by-widget}

外觀框架調用了在自定義Widget中實現的Widget的一些功能。 介面工具集必須實作下列函式：

<table>
 <tbody>
  <tr>
   <th>函數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>重點：function()</td>
   <td>專注於現場。</td>
  </tr>
  <tr>
   <td>按一下：function()</td>
   <td>將焦點放在欄位上，並呼叫XFA_CLICK_EVENT。</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>錯誤消息：字串 </em>代表錯誤<br /> <em>errorType:字串("warning"/"error")</em></p> <p><strong>附註</strong>:僅適用於HTML5表單。</p> </td>
   <td>傳送錯誤訊息和錯誤類型至介面工具集。 介面工具集會顯示錯誤。</td>
  </tr>
  <tr>
   <td><p>clearError:function()</p> <p><strong>附註</strong>:僅適用於HTML5表單。</p> </td>
   <td>若欄位中的錯誤已修正，則呼叫。 介面工具集會隱藏錯誤。</td>
  </tr>
 </tbody>
</table>

## 欄位類型的特定選項 {#options-specific-to-type-of-field}

所有自訂Widget都應符合上述規格。 若要使用不同欄位的功能，介面工具集必須符合該特定欄位的准則。

### 文本編輯：文字欄位 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>多線</td>
   <td>如果欄位支援輸入新行字元，則為true，否則為false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>可在欄位中輸入的字元數上限。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>附註</strong>:僅適用於HTML5表單</p> </td>
   <td>指定當文本寬度超過介面工具集的寬度時的文本欄位行為。</td>
  </tr>
 </tbody>
</table>

### ChoiceList:DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>值<br /> </td>
   <td>所選值的陣列。<br /> </td>
  </tr>
  <tr>
   <td>項目<br /> </td>
   <td>要顯示為選項的對象陣列。 每個物件都包含兩個屬性 — <br /> 儲存：要保存的值，顯示：值。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>可編輯</p> <p><strong>附註</strong>:僅適用於HTML5表單。<br /> </p> </td>
   <td>如果值為true，則會在介面工具集中啟用自訂文字輸入。<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>要顯示的值陣列。<br /> </td>
  </tr>
  <tr>
   <td>多選<br /> </td>
   <td>如果允許多個選取，則為true，否則為false。<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>函數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues:包含顯示和儲存值的物件 <br /> {sDisplayVal: &lt;displayvalue&gt;, sSaveVal: &lt;save value=""&gt;}</em></p> </td>
   <td>將項目新增至清單。</td>
  </tr>
  <tr>
   <td>deleteItem<em>:函式(nIndex)<br /> 索引：要從清單中刪除的項的索引<br /> </em><br /> <br /> </td>
   <td>從清單中刪除選項。</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>清除清單中的所有選項。</td>
  </tr>
 </tbody>
</table>

### 數值編輯：數值欄位，小數欄位 {#numericedit-numericfield-decimalfield}

| 選項 | 說明 |
|---|---|
| dataType | 代表欄位資料類型的字串（整數/小數）。 |
| leadDigits | 小數位數中允許的最大前導位數。 |
| fracDigits | 小數位數中允許的最大小數位數。 |
| 零 | 字串表示在欄位的地區中為零。 |
| 小數 | 字串表示欄位地區中小數的字串。 |

### CheckButton:RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>值陣列（開/關/中性）。</p> <p>它是checkButton不同狀態的值陣列。 值[0]是狀態為ON時的值，值[1]是狀態為OFF時的值，<br /> values[2]是狀態為NEUTRAL時的值。 值陣列的長度等於state選項的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>國家</td>
   <td><p>允許的狀態數。 </p> <p>兩個適用於最適化表單（開啟、關閉），三個適用於HTML5個表單（開啟、關閉、中性）。</p> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td><p>元素的目前狀態。</p> <p>兩個適用於最適化表單（開啟、關閉），三個適用於HTML5個表單（開啟、關閉、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit:（日期欄位） {#datetimeedit-datefield}

| 選項 | 說明 |
|---|---|
| 天 | 該欄位本地化的天數名稱。 |
| 個月 | 該欄位的本地化月份名稱。 |
| 零 | 數字0的本地化文本。 |
| clearText | 清除按鈕的本地化文字。 |
