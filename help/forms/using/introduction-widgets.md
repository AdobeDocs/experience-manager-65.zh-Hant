---
title: 用於自適應和HTML5形式的外觀框架
seo-title: Appearance framework for adaptive and HTML5 forms
description: 移動Forms將表單模板渲染為HTML5表單。 這些表單使用jQuery、Backbone.js和Underwork.js檔案進行外觀和啟用指令碼。
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

# 用於自適應和HTML5形式的外觀框架 {#appearance-framework-for-adaptive-and-html-forms}

Forms(適應形式和HTML5形式)使用 [j查詢](https://jquery.com/)。 [骨幹.js](https://backbonejs.org/) 和 [下划線.js](https://underscorejs.org/) 用於外觀和指令碼編寫的庫。 表單還使用 [j查詢UI](https://jqueryui.com/) **小部件** 窗體中所有交互元素（如欄位和按鈕）的體系結構。 此體系結構使窗體開發人員能夠在Forms使用一組豐富的可用jQuery小部件和插件。 您還可以實現特定於表單的邏輯，同時從用戶（如leadDigits/trailDigits限制）或實現圖片子句中捕獲資料。 表單開發人員可以建立和使用自定義附件來改進資料捕獲體驗，並使其更易於用戶使用。

本文是為對jQuery和jQuery小部件有充分認識的開發人員而設計的。 它提供了對外觀框架的洞察，並使開發人員能夠為表單域建立替代外觀。

該外觀框架依賴於各種選項、事件（觸發器）和函式來捕獲用戶與表單的交互，並響應模型更改以通知最終用戶。 此外：

* 框架提供一組用於欄位外觀的選項。 這些選項是鍵值對，並分為兩類：常用選項和欄位類型特定選項。
* 外觀作為合同的一部分，會觸發一組事件，如進入和退出。
* 實現一組功能需要外觀。 有些函式是常用的，而有些函式是特定於欄位類型函式的。

## 常用選項 {#common-options}

以下是設定全局選項。 這些選項可用於每個欄位。

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
   <td>將顯示該欄位的值。 </td>
  </tr>
  <tr>
   <td>螢幕閱讀器文本</td>
   <td>螢幕Reader使用此值來說明有關欄位的資訊。 表單提供值，您可以覆蓋該值。<br /> </td>
  </tr>
  <tr>
   <td>頁籤索引</td>
   <td>欄位在表單的制表符序列中的位置。 僅當要更改表單的預設制表符順序時，才覆蓋tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如標題或表。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>小部件的高度。 它以像素指定。 </td>
  </tr>
  <tr>
   <td>寬度</td>
   <td>小部件的寬度。 它以像素指定。</td>
  </tr>
  <tr>
   <td>訪問</td>
   <td>用於訪問容器對象（如子窗體）的內容的控制項。</td>
  </tr>
  <tr>
   <td>para樣式</td>
   <td>構件的XFA元素的para屬性。</td>
  </tr>
  <tr>
   <td>目錄</td>
   <td>文本的方向。 可能的值為ltr（從左到右）和rtl（從右到左）。</td>
  </tr>
 </tbody>
</table>

除了這些選項外，框架還提供了一些其他選項，這些選項因欄位類型而異。 下面列出了特定於欄位的選項的詳細資訊。

### 與表單框架的交互 {#interaction-with-forms-framework}

要與表單框架交互，小部件會觸發一些事件以使表單指令碼能夠工作。 如果小部件未引發這些事件，則在該欄位的窗體中編寫的某些指令碼將不起作用。

#### 由小部件觸發的事件 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Event </th>
   <th>說明</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>只要欄位處於焦點，就會觸發此事件。 它允許在欄位上運行「enter」指令碼。 觸發事件的語法為<br /> （小部件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>每當用戶離開該欄位時，都會觸發此事件。 它允許引擎設定欄位的值並運行其「exit」指令碼。 觸發事件的語法為<br /> （小部件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>觸發此事件，以允許引擎運行寫入該欄位的「更改」指令碼。 觸發事件的語法為<br /> （小部件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>只要按一下該欄位，就會觸發此事件。 它允許引擎運行寫在欄位上的「click」指令碼。 觸發事件的語法為<br /> （小部件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由小部件實現的API {#apis-implemented-by-widget}

外觀框架調用了在自定義小部件中實現的小部件的某些功能。 小部件必須實現以下功能：

<table>
 <tbody>
  <tr>
   <th>函數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>焦點：函式()</td>
   <td>集中精力在現場。</td>
  </tr>
  <tr>
   <td>按一下：函式()</td>
   <td>將焦點放在欄位上並調用XFA_CLICK_EVENT。</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>錯誤消息：字串 </em>表示錯誤<br /> <em>錯誤類型：字串("warning"/"error")</em></p> <p><strong>注釋</strong>:僅適用於HTML5窗體。</p> </td>
   <td>將錯誤消息和錯誤類型發送到小部件。 小部件顯示錯誤。</td>
  </tr>
  <tr>
   <td><p>clearError:函式()</p> <p><strong>注釋</strong>:僅適用於HTML5窗體。</p> </td>
   <td>如果欄位中的錯誤已修復，則調用。 小部件隱藏錯誤。</td>
  </tr>
 </tbody>
</table>

## 特定於欄位類型的選項 {#options-specific-to-type-of-field}

所有自定義小部件都應符合上述規範。 要使用不同欄位的功能，小部件必須符合該特定欄位的准則。

### 文本編輯：文本欄位 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>多線</td>
   <td>如果欄位支援輸入換行符，則返回true；否則返回false。</td>
  </tr>
  <tr>
   <td>最大字元數</td>
   <td>可在欄位中輸入的最大字元數。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注釋</strong>:僅適用於HTML5窗體</p> </td>
   <td>指定當文本寬度超過構件寬度時文本欄位的行為。</td>
  </tr>
 </tbody>
</table>

### 選擇清單：下拉清單，清單框 {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>值<br /> </td>
   <td>選定值的陣列。<br /> </td>
  </tr>
  <tr>
   <td>項目<br /> </td>
   <td>要作為選項顯示的對象陣列。 每個對象包含兩個屬性 — <br /> 保存：要保存的值，顯示：值。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>可編輯</p> <p><strong>注釋</strong>:僅適用於HTML5窗體。<br /> </p> </td>
   <td>如果值為true，則在小部件中啟用自定義文本條目。<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>要顯示的值陣列。<br /> </td>
  </tr>
  <tr>
   <td>多選<br /> </td>
   <td>如果允許多個選擇，則返回true；否則返回false。<br /> </td>
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
   <td><p>addItem:<em> 函式(itemValues)<br /> itemValues:包含顯示和保存值的對象 <br /> {sDisplayVal: &lt;displayvalue&gt;, sSaveVal: &lt;save value=""&gt;}</em></p> </td>
   <td>將項添加到清單。</td>
  </tr>
  <tr>
   <td>刪除項<em>:函式(nIndex)<br /> 索引：要從清單中刪除的項的索引<br /> </em><br /> <br /> </td>
   <td>從清單中刪除選項。</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>從清單中清除所有選項。</td>
  </tr>
 </tbody>
</table>

### 數字編輯：NumericField、DecimalField {#numericedit-numericfield-decimalfield}

| 選項 | 說明 |
|---|---|
| 資料類型 | 表示欄位的資料類型（整數/小數）的字串。 |
| leadDigits | 十進位數中允許的最大前導位數。 |
| frac數字 | 十進位數中允許的最大小數位數。 |
| 零 | 欄位區域設定中零的字串表示法。 |
| 小數 | 欄位區域設定中小數的字串表示。 |

### CheckButton:單選按鈕，複選框 {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>選項</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>值陣列（開/關/中性）。</p> <p>它是checkButton不同狀態的值陣列。 值[0]是狀態為ON時的值，值[1]是狀態為OFF時的值，<br /> 值[2]是狀態為NETRAL時的值。 值陣列的長度等於state選項的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>州</td>
   <td><p>允許的狀態數。 </p> <p>兩個用於自適應表單（開啟、關閉），三個用於HTML5表單（開啟、關閉、中性）。</p> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td><p>元素的當前狀態。</p> <p>兩個用於自適應表單（開啟、關閉），三個用於HTML5表單（開啟、關閉、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### 日期時間編輯：（日期欄位） {#datetimeedit-datefield}

| 選項 | 說明 |
|---|---|
| 天 | 該欄位的本地化天數。 |
| 個月 | 該欄位的本地化月名。 |
| 零 | 數字0的本地化文本。 |
| 純文字檔案 | 用於清除按鈕的本地化文本。 |
