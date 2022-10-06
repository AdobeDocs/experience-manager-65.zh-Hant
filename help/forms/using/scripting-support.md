---
title: 支援HTML5表單的指令碼
seo-title: Scripting support for HTML5 forms
description: HTML5 Forms支援的JavaScript、FormCalc屬性和其他方法。
seo-description: JavaScript, FormCalc properties, and other methods that are supported in HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
feature: Mobile Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3892'
ht-degree: 6%

---

# 支援HTML5表單的指令碼 {#scripting-support-for-html-forms}

HTML5表單支援的JavaScript、FormCalc屬性和方法如下：

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>屬性 </th>
   <th>說明<br /> </th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>指定欄位內容，之後欄位會隨使用者的動作而變更。 可以回調此值，類似於還原功能。</td>
   <td><p>下拉式清單和清單方塊無法運作。 <code>PrevText </code>無法正確運作的問題：</p>
    <ul>
     <li>在iPad的數值欄位中輸入一些特殊字元索引鍵(例如$、(、)、&amp;、@等)時，以及 </li>
     <li>用於「日期」欄位（通過日曆輸入日期時）。<br /> </li>
    </ul> <p>不支援通過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>指定事件在其上執行的對象。</td>
   <td>不支援通過指令碼設定值。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>指定欄位在隨使用者動作而變更後的內容。</td>
   <td><p>此 <code>newText</code> 屬性在下列情況下無法正常運作：</p>
    <ul>
     <li>論文本的選換</li>
     <li>在刪除、複製和貼上文本時。</li>
     <li>在數值欄位中輸入一些特殊字元索引鍵時(例如$、(、)、&amp;、@等)<br /> </li>
     <li>使用Shift+英數字元組合時。 </li>
     <li>使用日期/時間欄位時。</li>
    </ul>
    <div>
      不支援通過指令碼設定值。
    </div> </td>
  </tr>
  <tr>
   <td>變更</td>
   <td>指定使用者執行動作後，立即鍵入或貼入欄位的值。 </td>
   <td><p>變更屬性在下列情況下無法正常運作：</p>
    <ul>
     <li>論文本的選換</li>
     <li>在刪除、複製和貼上文本時。</li>
     <li>在數值欄位中輸入一些特殊字元索引鍵時(例如$、(、)、&amp;、@等)<br /> </li>
     <li>使用Shift+英數字元組合時。 </li>
     <li>使用日期/時間欄位時。</li>
    </ul> <p>不支援通過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td>鍵</td>
   <td>確定用戶是否按箭頭鍵進行選擇。 此屬性僅適用於清單框和下拉清單。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>修飾詞</td>
   <td>決定在執行特定事件時是否按住修飾鍵(例如，Microsoft® Windows®上的Ctrl)。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>返回主機的應用程式類型。 僅適用於客戶端應用程式。</td>
   <td>傳回 <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>返回當前應用程式的名稱。</td>
   <td>傳回瀏覽器名稱及其版本。 例如，在Chrome瀏覽器中，傳回的值為 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>返回文檔中的頁數。</td>
   <td>HTML5表單的分頁原則與PDF forms分頁原則不相同。 因此，numPages API在這兩種情況下都可傳回不同的值。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>傳回代表執行指令碼之電腦平台的字串。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>指定文檔的標題。 它僅適用於客戶端應用程式。</td>
   <td>它會以表單傳回HTML檔案的標題，而非如PDF forms情況般傳回表單中繼資料標題。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>傳回代表目前應用程式版本號碼的字串。</td>
   <td>它會傳回表單的版本。</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>指定是否執行計算指令碼。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>指定是否執行驗證指令碼。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>前往上一頁。</td>
   <td>HTML5表單不遵循與PDF表單相同的分頁原則，因此HTML5表單的上一頁與PDF表單的上一頁不同。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>移至表單的下一頁。 在執行階段使用pageDown方法。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>將鍵盤焦點設定為指定的欄位。 該欄位被指定為對象，或由欄位的SOM表達式指定。 它僅適用於客戶端應用程式。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>將檔案中的欄位重設為其預設值。</td>
   <td>清除表單中含有合併資料的所有資料，而非將其還原為預設值。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>在螢幕上顯示對話框。 它僅適用於客戶端應用程式</td>
   <td>「是/否」類型的消息框將轉換為「確定/取消」。 不支援包含三個按鈕的消息框。</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>在運行時設定文檔的當前活動頁。</p> <p>頁面值基於0，因此文檔的第一頁返回0的值。</p> <p>在用戶端上執行layout:ready時，currentPage屬性可供使用。 但是，當layout:ready在伺服器上執行時，它無法使用，因為該屬性要等到表單配置執行後才會執行。</p> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

### 欄位 {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>屬性</span></strong></th>
   <th><strong><span>說明<br /> </span></strong></th>
   <th><strong><span>例外</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>控制關聯對象在不同處理階段的參與率。 如果物件是容器，則容器的內容會繼承此控制項適用的任何限制。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>控制用戶對內容的訪問。</td>
   <td>無法用於排除群組。 此外，HTML5表單給非互動和受保護的物體同樣的處理。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>HTML5表單不允許設定對象的名稱屬性。 這是HTML5表單的唯讀屬性。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>封閉單一資料內容的內容元素。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>指定此欄位的未格式化值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>指定此欄位的格式化值。</td>
   <td>設定 <code>formattedValue</code> 不支援通過指令碼。</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>指定此欄位的編輯值。</td>
   <td>設定 <code>editValue </code>不支援通過指令碼。</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>指定此欄位的格式驗證消息字串。</td>
   <td>設定 <code>formatMessage </code>不支援通過指令碼。</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>指定此欄位的背景顏色值。 您必須將border.fill.presence屬性設為個別顯示。</td>
   <td>它無法正確傳回欄位的預設顏色。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>邊框對象描述了對象周圍的邊框。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui對象封裝了表單對象的用戶介面說明。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>指定欄位的nullTest值。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>指定此欄位的邊框顏色值。 您必須將border.edge.presence屬性設為個別顯示。</td>
   <td>無法正確傳回欄位的預設邊框顏色。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>清單中的項目數。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>將新項目新增至目前欄位。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>從欄位中移除所有項目。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>獲取下拉清單或清單框的特定顯示項的綁定值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>執行欄位的計算指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>執行欄位的驗證指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>執行物件的事件指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>返回指定項的選擇狀態</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>設定指定項的選擇狀態。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>檢索指定項索引的項顯示文本。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>檢索指定項索引的資料值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>刪除指定索引處的項。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>在當前欄位中設定指定的項。 它會取代預先存在的項目。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度的測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定佈局寬度的測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位佈局放置時，指定容器的錨點相對於父容器左上角的x坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位佈局放置時，指定容器的錨點相對於父容器左上角的y坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>標題對象描述與表單設計對象關聯的描述性標籤。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者提供資料的驗證。 驗證物件可在表單生命週期中啟動多次。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>指定此欄位的父子表單（頁面）。</td>
   <td>一律會傳回父子表單，而非傳回第一個非範圍的父子表單。<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>第一個所選項的索引。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 表單 {#form}

| **屬性** | **說明** | **例外** |
|---|---|---|
| formNodes | 返回綁定到指定資料對象的所有表單模型對象的清單。 |  |

## InstanceManager {#instancemanager}

| 屬性 | 說明 |
|---|---|
| `name` | 用於在指令碼運算式中識別此元素的識別碼。 |
| `occur` | 說明容器封閉容器允許的例項數的限制。 |
| `min` | 指定可實例化的最小實例數。 |
| `max` | 指定可實例化的實例數上限。 |
| `count` | 指定實例化的當前實例數。 |
| `setInstances` | 從此節點添加或刪除指定的子表單或子表單集。 |
| `addInstance` | 將子表單或子表單集的新實例添加到此節點。 |
| `removeInstance` | 從此節點中刪除子表單或子表單集。 |
| `moveInstance` | 將表單模型對象的子對象移動到表單模型內的另一個指定位置。 對象的相應資料模型資訊也被重新定位在資料模型內。 |
| `insertInstance` | 將子表單或子表單集的新實例插入到此節點。 |

## list {#list}

| 屬性 | 說明 |
|---|---|
| `length` | 清單中的元素數。 |
| `item` | 集合中的零索引。 |
| `append` | 將節點附加到節點清單的結尾。 |
| `remove` | 從節點清單中刪除節點。 |
| `insert` | 在節點清單中的特定節點前面插入節點。 |

## 節點 {#node}

| 屬性 | 說明 | 例外 |
|---|---|---|
| createNode | 根據有效的類名建立新節點。 | 無 |
| `isContainer` | 指定此物件是否為容器物件。 | 無 |
| `isNull` | 指示當前資料值是否為空值。 | 無 |
| `resolveNode` | 從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象的值。 | 無 |
| `resolveNodes` | 從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象的值。 | 無 |
| oneOfChild | 根據有效的類名建立新節點。 | 無 |
| getElement | 返回指定的子對象。 | 無 |
| getAttribute | 獲取指定的屬性值。 | 無 |
| setAttribute | 設定指定屬性的值。 | 無 |

## 模型 {#model}

| 屬性 | 說明 | 例外 |
|---|---|---|
| 不適用 | 不適用 | 不適用 |

## 子表單 {#subform}

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>指定對象的索引，相對於其他實例化實例。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>執行物件的事件指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>傳回子表單（含）中，未通過驗證測試的節點清單。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>邊框對象描述了對象周圍的邊框。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此欄位的邊框顏色值。 您必須將border.edge.presence屬性設為個別顯示。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度的測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定佈局寬度的測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位佈局放置時，指定容器的錨點相對於父容器左上角的x坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位佈局放置時，指定容器的錨點相對於父容器左上角的y坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者提供資料的驗證。 驗證物件可在表單生命週期中啟動多次。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定對象的可見性。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>存取</td>
   <td>控制對容器對象（如子表單）內容的用戶訪問。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>根據子表單或子表單集相對於相同表單對象的其他實例的位置來計算其索引。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager對象管理表單模型對象的實例建立、刪除和移動。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

### 提交 {#submit}

| 屬性 | 說明 |
|---|---|
| 目標 | 提交資料的URL。 遺漏此屬性表示XFA處理應用程式使用產品特定技術（如存取設定物件中的產品特定資訊）來取得URI。 |

## 樹 {#tree}

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>節點</td>
   <td>返回當前對象的所有子對象的清單。</td>
   <td>
    <ul>
     <li>xfa.nodes、desc不支援</li>
     <li>報告的PDF和HTML節點數不同。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定此節點的名稱。</td>
   <td>HTML中不允許使用指令碼設定名稱。</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>獲取此節點的父節點。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>索引</td>
   <td>返回此節點在其類名、範圍內、類子關係節點集合中的位置。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>獲取此節點的SOM表達式。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象的值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象的值。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| 屬性 | 說明 | 例外 |
|---|---|---|
| instanceManager | instanceManager對象管理表單模型對象的實例建立、刪除和移動。 | 無 |

## content {#content}

| **屬性** | **說明** | **例外** |
|---|---|---|
| isNull | 指示當前資料值是否為空值。 |  |

## dataValue {#datavalue}

| **屬性** | **說明** | **例外** |
|---|---|---|
| isNull | 指示當前資料值是否為空值。 |  |

## 邊緣 {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>屬性 </strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述了陣列對象的唯一顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 填充 {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>顏色屬性定義填充的唯一顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 線性 {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>顏色屬性描述表單上線性漸變填充的唯一顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 折線圖 {#line}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊緣</td>
   <td>邊對象描述弧、線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、大寫等屬性。<br /> </td>
  </tr>
 </tbody>
</table>

## 圖樣 {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述了陣列對象的唯一顏色。 </td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 徑向 {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>顏色屬性描述徑向對象的唯一顏色</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 石 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述拼接對象的唯一顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 繪圖 {#draw}

<table>
 <tbody>
  <tr>
   <td>屬性</td>
   <td>說明</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui對象封裝了表單對象的用戶介面說明。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>字幕</td>
   <td>標題對象描述與表單設計對象關聯的描述性標籤。</td>
   <td> </td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定對象的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定可用於在指令碼表達式中指定此對象或事件的標識符。</td>
   <td>不支援在執行階段設定值</td>
  </tr>
  <tr>
   <td>值</td>
   <td>值對象封裝了單個資料內容單位。<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 角 {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述了拐角對象的唯一顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>邊框對象描述了checkButton對象周圍的邊框。 </td>
   <td>變更會反映在模型中，且可供指令碼使用，但不會同步至HTML元素。 因此，UI不會反映這些變更。<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>屬性<br /> </strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>邊框對象描述了choiceList對象周圍的邊框。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊框 | 邊框物件說明了dateTimeEdit物件周圍的邊框。 |  |

## 影像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>指定引用文檔中的內容類型，以MIME類型表示。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>名稱<br /> </td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊框 | 邊框對象描述了imageEdit對象周圍的邊框。 |  |

## numericEdit {#numericedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊框 | 邊框對象描述了對象周圍的邊框。 | 無 |

## 物件 {#object}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>確定此對象的類的名稱。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 矩形 {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊緣</td>
   <td>邊對象描述弧、線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、大寫等屬性。</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>邊框對象描述了對象周圍的邊框。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>配置</td>
   <td>指定此對象要使用的佈局策略。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>指定此欄位周圍的邊框。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>強制</td>
   <td>指定欄位的nullTest值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此欄位的邊框顏色值。必須先定義邊框，然後才能通過指令碼更改顏色。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>指定此欄位的邊框寬度。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度的測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>瞬態</td>
   <td>指定處理應用程式是否必須將排除群組的值儲存為表單提交或儲存操作的一部分。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定佈局寬度的測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位佈局放置時，指定容器的錨點相對於父容器左上角的x坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位佈局放置時，指定容器的錨點相對於父容器左上角的y坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>字幕</td>
   <td>標題對象描述與表單設計對象關聯的描述性標籤。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者提供資料的驗證。 驗證物件可在表單生命週期中啟動多次。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>獲取合併後表單節點綁定到的資料節點。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定對象的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>存取</td>
   <td>控制對容器對象（如子表單）內容的用戶訪問。</td>
   <td>對於exclgrp中的個別項目，它一律會傳回open。 </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定可用於在指令碼表達式中指定此對象或事件的標識符。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>成員</td>
   <td>指定排除群組的成員。 </td>
   <td>無</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>返回排除組的選定成員。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>對指定對象的計算事件和任何子對象執行任何指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>計算</td>
   <td>計算對象控制欄位值的計算。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 弧 {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>屬性<strong></strong></strong></td>
   <td><strong>說明<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>邊緣</td>
   <td>邊對象描述弧、線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、大寫等屬性。 </td>
  </tr>
 </tbody>
</table>

## 邊框 {#border}

<table>
 <tbody>
  <tr>
   <td><strong>屬性<strong></strong></strong></td>
   <td><strong>說明<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>邊緣</td>
   <td>邊對象描述弧、線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、大寫等屬性。 </td>
  </tr>
 </tbody>
</table>

## $配置 {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>確定給定表單設計對象的高度。<br /> </td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援高度(h)屬性。 </li>
     <li>不支援「發生XFA-Form物件時從第一個內容區域偏移」參數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>寫</td>
   <td>確定指定的表單設計對象的寬度。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援寬度(w)屬性。 </li>
     <li>不支援「發生XFA-Form物件時從第一個內容區域偏移」參數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>確定指定表單設計對象相對於其父對象的x坐標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援x座標(x)屬性。 </li>
     <li>不支援「發生XFA-Form物件時從第一個內容區域偏移」參數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>確定給定表單設計對象相對於其父對象的y坐標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援y座標(y)屬性。 </li>
     <li>不支援「發生XFA-Form物件時從第一個內容區域偏移」參數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>決定目前表單的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法針對PDF和HTML表單傳回不同值。</li>
     <li>透過隱藏物件來降低頁面計數時，abspagecount方法會傳回錯誤值。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>從表單的指定頁面中檢索表單設計對象的類型。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>決定目前表單的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法針對PDF和HTML表單傳回不同值。</li>
     <li>透過隱藏物件來降低頁面計數時，abspagecount方法會傳回錯誤值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 項目 {#items}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 存在 | 指定對象的可見性。 | 無 |

## FormCalc {#formcalc}

FormCalc是XFA專用的語言，用於建立電子錶單中心邏輯和計算根。 FormCalculation提供了一組功能強大的生成函式。

### 支援的FormCalc函式 {#formcalc-supported-functions}

### 表單計算表達式支援 {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>類別 </strong></td>
   <td><strong>說明 </strong></td>
   <td><strong>範例 </strong></td>
  </tr>
  <tr>
   <td>簡單運算式</td>
   <td>加、減、乘、除和括弧</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>變數聲明</td>
   <td>定義變數</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>邏輯運算式</td>
   <td>
    <ul>
     <li>邏輯（和/或）</li>
     <li>比較（大/小/等於）</li>
    </ul> </td>
   <td>A或1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A或1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>If運算式</td>
   <td><br type="_moz" /> </td>
   <td>if(a&gt;b)然後2 endif</td>
  </tr>
  <tr>
   <td>whel</td>
   <td><br type="_moz" /> </td>
   <td>而(ilt 5)do i = i + 1結束時</td>
  </tr>
  <tr>
   <td>代表</td>
   <td><br type="_moz" /> </td>
   <td>若為i = 100，則從1 <br /> do s = s + i結束</td>
  </tr>
  <tr>
   <td>每</td>
   <td><br type="_moz" /> </td>
   <td>(1、2、3)中每個i <br /> do s = s + i結束</td>
  </tr>
  <tr>
   <td>函式聲明</td>
   <td>在FormCalc中定義自定義函式</td>
   <td>func foo(n)do var f = nendfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API支援 {#acrobat-api-support}

1. **算術函式**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. 計數()
   1. Floor()
   1. 最大值()
   1. 最小值()
   1. Mod()
   1. Round()
   1. 總計()

1. **科學功能**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. 棕褐色()
   1. Exp()
   1. 記錄檔()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **財務職能**

   1. 4月()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. 詞彙()

1. **邏輯函式**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **字串函式**

   1. 於()
   1. Concat()
   1. 左()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. 取代()
   1. 右()
   1. Rtrim()
   1. 空間()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **日期和時間**

   1. 日期()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>像差</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>此Acrobat API會將輸出轉儲到JavaScript控制台。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>此Acrobat API會透過JavaScript快顯視窗傳送警報訊息。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>導致系統播放聲音。</td>
   <td>未執行任何操作。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>對使用者顯示強制回應對話方塊。 使用者必須先關閉強制回應對話方塊，才能直接使用主機應用程式。</td>
   <td>未執行任何操作。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>在瀏覽器視窗中啟動URL。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>指定JavaScript指令碼和時段。 每次經過該時段時，就會執行指令碼。 此方法的傳回值必須保留在JavaScript變數中。 否則，間隔對象將被垃圾回收，這將導致時鐘停止。 要終止定期執行，請將返回的間隔對象傳遞到clearInterval。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>指定JavaScript指令碼和時段。 指令碼僅在經過該時段後執行一次。此方法的傳回值必須保留在JavaScript變數中。 否則，逾時物件會受到垃圾收集的限制，而這會導致時鐘停止。 若要取消逾時事件，請將傳回的逾時物件傳遞至clearTimeOut。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>取消先前由setInterval方法初始設定的註冊間隔。</td>
   <td>在HTML5表單中，API無法正常運作。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>取消先前註冊的超時間隔。 這樣的間隔最初由setTimeOut設定。</td>
   <td>在HTML5表單中，API無法正常運作。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>運行指令碼。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>包含每個活動文檔的Doc對象的陣列。 如果沒有活動的文檔，activeDocs將不返回任何內容；也就是說，其行為與d =核心JavaScript中的新陣列(0)相同。</td>
   <td>返回HTMl5表單的空陣列。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>如果為true（預設值），則可執行計算。 如果為false，則不允許計算。</td>
   <td>HTMl5Forms一律為true。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>用於保持各種常數值的包裝物對象。 目前，此屬性會傳回物件，並搭配單一屬性align。</td>
   <td>HTML5表單會傳回空白的對齊物件。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>開啟或關閉聚焦矩形。 焦點矩形是位於按鈕、核取方塊、選項按鈕和簽名周圍的微弱虛線，表示表單欄位具有鍵盤焦點。 若值為true，則會開啟焦點矩形。</td>
   <td>HTML5表單一律為true。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>檢視器表單軟體的版本號。 如果要在指令碼中保持向後相容性，請檢查此屬性以確定較新版本軟體中的對象、屬性或方法是否可用。</td>
   <td>11.001總是。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>執行中Acrobat檢視器的語言。</td>
   <td>HTMl5表單一律為「簡體中文」。</td>
  </tr>
 </tbody>
</table>

## 支援的XFA事件 {#supported-xfa-events}

支援下列用戶端XFA事件：

* 初始化
* 驗證
* 計算
* 按一下
* 輸入
* 結束
* 變更
* ValidationState

>[!NOTE]
>
>HTML5表單會在用戶端（瀏覽器）上轉譯。 建議使用用戶端 **驗證** 和 **計算** 指令碼，而非伺服器端指令碼。
