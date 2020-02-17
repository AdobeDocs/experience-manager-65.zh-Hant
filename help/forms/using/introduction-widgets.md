---
title: 最適化和HTML5表單的外觀架構
seo-title: 最適化和HTML5表單的外觀架構
description: Mobile Forms會將表單範本轉換為HTML5表單。 這些表單使用jQuery、Backbone.js和Undershore.js檔案進行外觀並啟用指令碼。
seo-description: Mobile Forms會將表單範本轉換為HTML5表單。 這些表單使用jQuery、Backbone.js和Undershore.js檔案進行外觀並啟用指令碼。
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 最適化和HTML5表單的外觀架構 {#appearance-framework-for-adaptive-and-html-forms}

表單（最適化表單和HTML5表單）使 [用jQuery](https://jquery.com/)、 [Backbone.js](https://backbonejs.org/) 和 [](https://underscorejs.org/) Undershore.js庫進行外觀和指令碼編寫。 表單也會針對表單中 [的所有互動元素（例如欄位和按鈕）使用jQuery UI](https://jqueryui.com/) **** Widgets架構。 此架構可讓表單開發人員在表單中使用一組豐富的可用jQuery Widget和外掛程式。 您也可以在擷取來自使用者（例如leadDigits/trailDigits限制或實作圖片子句）的資料時，實作表格特定邏輯。 表單開發人員可建立並使用自訂的附加功能，以改善資料擷取體驗，並讓它更方便使用。

本文是為對jQuery和jQuery Widget有充分認識的開發人員而設計。 它提供外觀架構的洞察力，讓開發人員可為表單欄位建立替代外觀。

外觀框架依賴各種選項、事件（觸發器）和函式來擷取使用者與表單的互動，並回應模型變更以通知使用者。 此外：

* 框架提供一組欄位外觀的選項。 這些選項是鍵值配對，並分為兩類：常用選項和欄位類型特定選項。
* 外觀是合約的一部分，會觸發一組事件，例如進入和退出。
* 實施一組函式時需要外觀。 有些函式是常用的，而有些函式是特定於欄位類型函式。

## 常用選項 {#common-options}

以下是設定全局選項。 這些選項適用於每個欄位。

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
   <td>此時會顯示欄位的此值。 </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>螢幕閱讀程式會使用此值來說明欄位的相關資訊。 表單提供值，您可以覆寫值。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>欄位在表單的制表符序列中的位置。 僅當要更改表單的預設頁籤順序時，才覆蓋tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如標題或表格。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>介面工具集的高度。 它以像素指定。 </td>
  </tr>
  <tr>
   <td>寬度</td>
   <td>介面工具集的寬度。 它以像素指定。</td>
  </tr>
  <tr>
   <td>存取</td>
   <td>用於訪問容器對象（如子表單）內容的控制項。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>XFA元素對介面工具集的para屬性。</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>文字的方向。 可能的值為ltr（從左到右）和rtl（從右到左）。</td>
  </tr>
 </tbody>
</table>

除了這些選項外，框架還提供了一些其他選項，這些選項會因欄位類型而異。 欄位特定選項的詳細資訊列於下方。

### 與表單架構互動 {#interaction-with-forms-framework}

若要與表單架構互動，Widget會觸發一些事件，讓表單指令碼運作。 如果介面工具集未擲出這些事件，則在該欄位表單中編寫的某些指令碼將無法運作。

#### 由介面工具集觸發的事件 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>事件 </th>
   <th>說明</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>每當欄位處於焦點時，就會觸發此事件。 它允許在欄位上運行"enter"指令碼。 觸發事件的語法為<br /> (widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>每當使用者離開欄位時，就會觸發此事件。 它可讓引擎設定欄位的值，並執行其「退出」指令碼。 觸發事件的語法為<br /> (widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>觸發此事件可讓引擎執行寫入欄位的「變更」指令碼。 觸發事件的語法為<br /> (widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>只要按一下欄位，就會觸發此事件。 它可讓引擎執行寫入欄位的「點按」指令碼。 觸發事件的語法為<br /> (widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由介面工具集實作的API {#apis-implemented-by-widget}

外觀框架調用在自定義Widget中實現的Widget的一些功能。 介面工具集必須實作下列功能：

<table>
 <tbody>
  <tr>
   <th>函數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>焦點：函式()</td>
   <td>專注於現場。</td>
  </tr>
  <tr>
   <td>按一下：函式()</td>
   <td>將焦點放在欄位上，並呼叫XFA_CLICK_EVENT。</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> err <br /><em>orMessage:代表 </em>error<br /> <em>errorType的字串：字串("warning"/"error")</em></p> <p><strong>注意</strong>:僅適用於HTML5表單。</p> </td>
   <td>傳送錯誤訊息和錯誤類型至介面工具集。 介面工具集會顯示錯誤。</td>
  </tr>
  <tr>
   <td><p>clearError:函式()</p> <p><strong>注意</strong>:僅適用於HTML5表單。</p> </td>
   <td>如果欄位中的錯誤已修正，則呼叫。 介面工具集會隱藏錯誤。</td>
  </tr>
 </tbody>
</table>

## 欄位類型的特定選項 {#options-specific-to-type-of-field}

所有自訂Widget都應符合上述規格。 若要使用不同欄位的功能，介面工具集必須符合該特定欄位的准則。

### 文字編輯：文字欄位 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>多行</td>
   <td>如果欄位支援輸入新行字元，則返回true；否則返回false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>可在欄位中輸入的字元數上限。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注意</strong>:僅適用於HTML5表單</p> </td>
   <td>指定當文字寬度超過介面工具集寬度時，文字欄位的行為。</td>
  </tr>
 </tbody>
</table>

### ChoiceList:下拉式清單、ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>值<br /> </td>
   <td>選取值的陣列。<br /> </td>
  </tr>
  <tr>
   <td>項目<br /> </td>
   <td>要顯示為選項的對象陣列。 <br /> 每個對象包含兩個屬性-<br /> save:要保存的值，顯示：值。 <br /> </td>
  </tr>
  <tr>
   <td><p>可編輯</p> <p><strong>注意</strong>:僅適用於HTML5表單。<br /> </p> </td>
   <td>如果值為true，則會在介面工具集中啟用自訂文字輸入。<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>要顯示的值陣列。<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>如果允許多個選擇，則返回true，否則返回false。<br /> </td>
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
   <td><p><em> addItem:function(itemValues)<br /> itemValues:包含顯示的物件並儲存值 <br /> {sDisplayVal:&lt;displayValue&gt;, sSaveVal:&lt;保存值&gt;}</em></p> </td>
   <td>新增項目至清單。</td>
  </tr>
  <tr>
   <td>deleteItem<em>:函式(nIndex)<br /> nIndex:要從清單中刪除的項的索引<br /></em><br /><br /> </td>
   <td>從清單中刪除選項。</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>清除清單中的所有選項。</td>
  </tr>
 </tbody>
</table>

### 數值編輯：NumericField、DecimalField {#numericedit-numericfield-decimalfield}

| 選項 | 說明 |
|---|---|
| dataType | 代表欄位資料類型的字串（整數／小數）。 |
| leadDigits | 小數數字中允許的最大前導位數。 |
| fracDigits | 小數數字中允許的最大小數位數。 |
| 零 | 欄位區域設定中零的字串表示。 |
| 小數點 | 欄位區域設定中小數的字串表示。 |

### CheckButton:RadioButton、CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>值陣列（開／關/中性）。</p> <p>它是checkButton不同狀態的值陣列。 值[0]是狀態為ON時的值，值[1]是狀態為OFF時的值，<br /> 值[2]是狀態為NEUTRAL時的值。 值陣列的長度等於狀態選項的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>州</td>
   <td><p>允許的狀態數。 </p> <p>兩個用於最適化表單（開啟、關閉），三個用於HTML5表單（開啟、關閉、中性）。</p> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td><p>元素的當前狀態。</p> <p>兩個用於最適化表單（開啟、關閉），三個用於HTML5表單（開啟、關閉、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit:（日期欄位） {#datetimeedit-datefield}

| 選項 | 說明 |
|---|---|
| 天 | 該欄位的本地化天數名稱。 |
| 個月 | 該欄位的本地化月份名稱。 |
| 零 | 數字0的本地化文本。 |
| clearText | 清除按鈕的本地化文字。 |

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
