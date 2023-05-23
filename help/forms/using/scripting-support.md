---
title: 對HTML5表單的指令碼支援
seo-title: Scripting support for HTML5 forms
description: JavaScript、FormCalc屬性和HTML5Forms中支援的其他方法。
seo-description: JavaScript, FormCalc properties, and other methods that are supported in HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
feature: Mobile Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: c4045313200ffecbf05abfacd67aabc80ad67e7f
workflow-type: tm+mt
source-wordcount: '3892'
ht-degree: 6%

---

# 對HTML5表單的指令碼支援 {#scripting-support-for-html-forms}

HTML5表單中支援的JavaScript、FormCalc屬性和方法如下所列：

## $event（$事件） {#event}

<table>
 <tbody>
  <tr>
   <th>屬性 </th>
   <th>說明<br /> </th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>指定欄位內容，然後根據用戶的操作進行更改。 可以回調此值，類似於撤消特徵。</td>
   <td><p>對下拉清單和清單框不起作用。 <code>PrevText </code>在以下情況下無法正確工作：</p>
    <ul>
     <li>在iPad的「數字」欄位中鍵入一些特殊字元鍵(例如$、(、)、&amp;、@等等), </li>
     <li>「日期」欄位（通過日曆輸入日期）。<br /> </li>
    </ul> <p>不支援通過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>指定事件在其上操作的對象。</td>
   <td>不支援通過指令碼設定值。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>指定在響應用戶操作而更改欄位後的內容。</td>
   <td><p>的 <code>newText</code> 屬性在以下情況下無法正常工作：</p>
    <ul>
     <li>論文本的選替</li>
     <li>刪除、複製和貼上文本時。</li>
     <li>在「數字」欄位中鍵入一些特殊字元鍵(例如$、(、)、&amp;、@等)<br /> </li>
     <li>使用shift+字母數字組合時。 </li>
     <li>使用日期/時間欄位。</li>
    </ul>
    <div>
      不支援通過指令碼設定值。
    </div> </td>
  </tr>
  <tr>
   <td>變更</td>
   <td>指定用戶在執行操作後立即鍵入或貼上到欄位中的值。 </td>
   <td><p>更改屬性對以下情況無法正常工作：</p>
    <ul>
     <li>論文本的選替</li>
     <li>刪除、複製和貼上文本時。</li>
     <li>在「數字」欄位中鍵入一些特殊字元鍵(例如$、(、)、&amp;、@等)<br /> </li>
     <li>使用shift+字母數字組合時。 </li>
     <li>使用日期/時間欄位。</li>
    </ul> <p>不支援通過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td>按鍵</td>
   <td>確定用戶是否按箭頭鍵進行選擇。 此屬性僅可用於清單框和下拉清單。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>修飾</td>
   <td>確定在執行特定事件時是否按住修飾鍵(例如，Microsoft® Windows®上的Ctrl)。</td>
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
   <td>返回 <code>HTML 5</code>。</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>返回當前應用程式的名稱。</td>
   <td>返回瀏覽器名稱及其版本。 例如，在Chrome瀏覽器中，返回的值為 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>返回文檔中的頁數。</td>
   <td>HTML5表單的分頁策略與PDF forms分頁策略不相同。 因此，numPages API可以在這兩種情況下返回不同的值。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>返回一個字串，該字串表示運行指令碼的電腦的平台。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>指定文檔的標題。 它僅可用於客戶端應用程式。</td>
   <td>它以表單形式返回HTML文檔的標題，而不是像PDF forms那樣返回表單元資料標題。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>返回表示當前應用程式的版本號的字串。</td>
   <td>它返回窗體的版本。</td>
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
   <td>轉到上一頁。</td>
   <td>HTML5表單與PDF表單不遵循相同的分頁策略，因此HTML5表單的上一頁與PDF表單的上一頁不同。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>移到窗體的下一頁。 在運行時使用pageDown方法。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>將鍵盤焦點設定為指定的欄位。 該欄位被指定為對象，或由欄位的SOM表達式指定。 它僅可用於客戶端應用程式。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>將欄位重置為文檔中的預設值。</td>
   <td>清除具有合併資料的表單中的所有資料，而不是將其還原為預設值。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>在螢幕上顯示一個對話框。 它僅可用於客戶端應用程式</td>
   <td>「是/否」類型的消息框將轉換為「確定/取消」。 不支援包含三個按鈕的消息框。</td>
  </tr>
  <tr>
   <td>當前頁</td>
   <td><p>設定運行時文檔的當前活動頁面。</p> <p>頁面值基於0，因此文檔的第一頁返回值0。</p> <p>當layout:ready在客戶端上執行時，currentPage屬性可用。 但是，當layout:ready在伺服器上執行時，該屬性不可用，因為在執行表單佈局之前，該屬性不會執行。</p> </td>
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
   <td>控制關聯對象在不同處理階段的參與。 如果對象是容器，則容器的內容將繼承此控制項所應用的任何限制。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>控制用戶對內容的訪問。</td>
   <td>不適用於排除組。 此外，HTML5形式對非交互和受保護的物體給予相同的處理。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>用於在指令碼表達式中標識此元素的標識符。</td>
   <td>HTML5表單不允許為對象設定name屬性。 它是HTML5窗體的只讀屬性。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>一種包圍單一資料內容的內容元素。</td>
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
   <td>指定此欄位的背景色值。 您需要將border.fill.presence屬性設定為單獨可見。</td>
   <td>它無法正確返回欄位的預設顏色。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>邊框對象描述對象周圍的邊框。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui對象包圍了表單對象的用戶介面描述。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>指定欄位的nullTest值。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>指定此欄位的邊框顏色值。 您需要將border.edge.presence屬性設定為單獨可見。</td>
   <td>它無法正確返回欄位的預設邊框顏色。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>清單中的項數。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>將新項目添加到當前欄位。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>從欄位中刪除所有項。</td>
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
   <td>執行欄位的validate指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>執行對象的事件指令碼。</td>
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
   <td>設定當前欄位中的指定項。 它替換了預先存在的項目。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>佈局的高度測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定佈局寬度的度量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定當放置到放置佈局時容器錨點相對於父容器左上角的x坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定當放置時放置有定位佈局時容器錨點相對於父容器左上角的y坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>標題對象描述與表單設計對象關聯的描述性標籤。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證對象控制表單上用戶提供的資料的驗證。 在表單生命期間，可多次激活驗證對象。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>父子窗體</td>
   <td>指定此欄位的父子窗體（頁）。</td>
   <td>始終返回父子窗體，而不是返回第一個非作用域父子窗體。<br /> </td>
  </tr>
  <tr>
   <td>選定索引</td>
   <td>第一個選定項的索引。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 表單 {#form}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 表單節點 | 返回綁定到指定資料對象的所有窗體模型對象的清單。 |  |

## 實例管理器 {#instancemanager}

| 屬性 | 說明 |
|---|---|
| `name` | 用於在指令碼表達式中標識此元素的標識符。 |
| `occur` | 描述其封裝容器允許的實例數的約束。 |
| `min` | 指定可實例化的最小實例數。 |
| `max` | 指定可實例化的實例的最大數量。 |
| `count` | 指定實例化的當前實例數。 |
| `setInstances` | 從此節點添加或刪除指定的子表單或子表單集。 |
| `addInstance` | 將子表單或子表單集的新實例添加到此節點。 |
| `removeInstance` | 從此節點中刪除子表單或子表單集。 |
| `moveInstance` | 將表單模型對象的子對象移動到表單模型內的另一個指定位置。 對象的相應資料模型資訊也被重新定位在資料模型內。 |
| `insertInstance` | 將子窗體或子窗體集的新實例插入到此節點。 |

## list {#list}

| 屬性 | 說明 |
|---|---|
| `length` | 清單中的元素數。 |
| `item` | 集合中的基於零的索引。 |
| `append` | 將節點附加到節點清單的末尾。 |
| `remove` | 從節點清單中刪除節點。 |
| `insert` | 在節點清單中的特定節點之前插入節點。 |

## 節點 {#node}

| 屬性 | 說明 | 例外 |
|---|---|---|
| createNode | 基於有效類名建立新節點。 | 無 |
| `isContainer` | 指定此對象是否為容器對象。 | 無 |
| `isNull` | 指示當前資料值是否為空值。 | 無 |
| `resolveNode` | 從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象值。 | 無 |
| `resolveNodes` | 從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象值。 | 無 |
| 一個孩子 | 基於有效類名建立新節點。 | 無 |
| getElement | 返回指定的子對象。 | 無 |
| getAttribute | 獲取指定的屬性值。 | 無 |
| setAttribute | 設定指定屬性的值。 | 無 |

## 模型 {#model}

| 屬性 | 說明 | 例外 |
|---|---|---|
| 不適用 | 不適用 | 不適用 |

## 子窗體 {#subform}

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>說明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>實例索引</td>
   <td>指定對象相對於其他實例化實例的索引。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>exec事件</td>
   <td>執行對象的事件指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>返回子表單（包括）中包含的未通過驗證test的節點清單。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊界</td>
   <td>邊框對象描述對象周圍的邊框。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊框顏色</td>
   <td>指定此欄位的邊框顏色值。 您需要將border.edge.presence屬性設定為單獨可見。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>佈局的高度測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定佈局寬度的度量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定當放置到放置佈局時容器錨點相對於父容器左上角的x坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定當放置時放置有定位佈局時容器錨點相對於父容器左上角的y坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證對象控制表單上用戶提供的資料的驗證。 在表單生命期間，可多次激活驗證對象。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>用於在指令碼表達式中標識此元素的標識符。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定對象的可見性。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>訪問</td>
   <td>控制用戶對容器對象（如子窗體）內容的訪問。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>執行驗證</td>
   <td>根據子窗體或子窗體集相對於同一窗體對象的其他實例的位置計算其索引。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>實例管理器</td>
   <td>instanceManager對象管理表單模型對象的實例建立、刪除和移動。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

### 提交 {#submit}

| 屬性 | 說明 |
|---|---|
| 目標 | 資料提交到的URL。 省略此屬性意味著XFA處理應用程式使用產品特定技術（例如訪問配置對象中的產品特定資訊）來獲取URI。 |

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
     <li>xfa.nodes不支援，desc</li>
     <li>為PDF和HTML報告的節點數不同。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定此節點的名稱。</td>
   <td>HTML中不允許使用指令碼設定名稱。</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>獲取此節點的父級。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>索引</td>
   <td>返回此節點在其類似命名、範圍內、類似子關係節點集合中的位置。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>som表達式</td>
   <td>獲取此節點的SOM表達式。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>從當前XML表單對象模型對象開始計算指定的SOM表達式，並返回在SOM表達式中指定的對象值。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 子形式集 {#subformset}

| 屬性 | 說明 | 例外 |
|---|---|---|
| 實例管理器 | instanceManager對象管理表單模型對象的實例建立、刪除和移動。 | 無 |

## content {#content}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 為Null | 指示當前資料值是否為空值。 |  |

## 資料值 {#datavalue}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 為Null | 指示當前資料值是否為空值。 |  |

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
   <td>color屬性描述圖案對象的唯一顏色。</td>
   <td>
    <ul>
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
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
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
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
   <td>color屬性描述窗體上線性漸變填充的唯一顏色。</td>
   <td>
    <ul>
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
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
   <td>邊緣對象描述邊框或矩形的弧、線或一側。<br /> </td>
   <td>不支援顏色、帽等屬性。<br /> </td>
  </tr>
 </tbody>
</table>

## 圖案 {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述圖案對象的唯一顏色。 </td>
   <td>
    <ul>
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
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
   <td>color屬性描述徑向對象的唯一顏色</td>
   <td>
    <ul>
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 酒 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述了筆觸對象的唯一顏色。</td>
   <td>
    <ul>
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 畫 {#draw}

<table>
 <tbody>
  <tr>
   <td>屬性</td>
   <td>說明</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>用戶</td>
   <td>ui對象包圍了表單對象的用戶介面描述。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
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
   <td>不支援在運行時設定值</td>
  </tr>
  <tr>
   <td>值</td>
   <td>值對象包含單個資料內容單位。<br /> </td>
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
   <td>color屬性描述拐角對象的唯一顏色。</td>
   <td>
    <ul>
     <li>無法檢索預設值。 </li>
     <li>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。</li>
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
   <td>邊界</td>
   <td>邊框對象描述了checkButton對象周圍的邊框。 </td>
   <td>這些更改反映在模型中，可用於編寫指令碼，但未同步到HTML元素。 因此，更改不會反映在UI中。<br /> </td>
  </tr>
 </tbody>
</table>

## 選擇清單 {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>屬性<br /> </strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊界</td>
   <td>邊框對象描述choiceList對象周圍的邊框。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 日期時間編輯 {#datetimeedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊界 | 邊框對象描述圍繞dateTimeEdit對象的邊框。 |  |

## 影像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>內容類型</td>
   <td>指定引用文檔中以MIME類型表示的內容類型。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>名稱<br /> </td>
   <td>用於在指令碼表達式中標識此元素的標識符。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 影像編輯 {#imageedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊界 | 邊框對象描述imageEdit對象周圍的邊框。 |  |

## 數字編輯 {#numericedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊界 | 邊框對象描述對象周圍的邊框。 | 無 |

## 物件 {#object}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>類名</td>
   <td>確定此對象類的名稱。<br /> </td>
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
   <td>邊緣對象描述邊框或矩形的弧、線或一側。<br /> </td>
   <td>不支援顏色、帽等屬性。</td>
  </tr>
 </tbody>
</table>

## 文本編輯 {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊界</td>
   <td>邊框對象描述對象周圍的邊框。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## excl組 {#exclgroup}

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
   <td>邊界</td>
   <td>指定此欄位周圍的邊框。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>強制</td>
   <td>指定欄位的nullTest值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊框顏色</td>
   <td>指定此欄位的邊框顏色值。必須先定義邊框，然後才能通過指令碼更改顏色。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊框寬度</td>
   <td>指定此欄位的邊框寬度。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>佈局的高度測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>瞬態</td>
   <td>指定處理應用程式是否必須將排除組的值作為表單提交或保存操作的一部分進行保存。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定佈局寬度的度量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定當放置到放置佈局時容器錨點相對於父容器左上角的x坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定當放置時放置有定位佈局時容器錨點相對於父容器左上角的y坐標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>標題對象描述與表單設計對象關聯的描述性標籤。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證對象控制表單上用戶提供的資料的驗證。 在表單生命期間，可多次激活驗證對象。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>資料節點</td>
   <td>獲取合併後表單節點綁定到的資料節點。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定對象的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>訪問</td>
   <td>控制用戶對容器對象（如子窗體）內容的訪問。</td>
   <td>對於exclgrp中的單個項，它始終返回open。 </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定可用於在指令碼表達式中指定此對象或事件的標識符。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>成員</td>
   <td>指定排除組的成員。 </td>
   <td>無</td>
  </tr>
  <tr>
   <td>選定成員</td>
   <td>返回排除組的選定成員。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>exec計算</td>
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
   <td>邊緣對象描述邊框或矩形的弧、線或一側。<br /> </td>
   <td>不支援顏色、帽等屬性。 </td>
  </tr>
 </tbody>
</table>

## 邊界 {#border}

<table>
 <tbody>
  <tr>
   <td><strong>屬性<strong></strong></strong></td>
   <td><strong>說明<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>邊緣</td>
   <td>邊緣對象描述邊框或矩形的弧、線或一側。<br /> </td>
   <td>不支援顏色、帽等屬性。 </td>
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
   <td>確定給定窗體設計對象的高度。<br /> </td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援高度(h)屬性。 </li>
     <li>不支援參數「從XFA-Form對象發生的第一個內容區域偏移」。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>寫</td>
   <td>確定給定窗體設計對象的寬度。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援Width(w)屬性。 </li>
     <li>不支援參數「從XFA-Form對象發生的第一個內容區域偏移」。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>確定給定窗體設計對象相對於其父對象的x坐標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援x coordinate(x)屬性。 </li>
     <li>不支援參數「從XFA-Form對象發生的第一個內容區域偏移」。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>確定給定窗體設計對象相對於其父對象的y坐標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援y coordinate(y)屬性。 </li>
     <li>不支援參數「從XFA-Form對象發生的第一個內容區域偏移」。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>分頁</td>
   <td>確定當前窗體的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法返回PDF和HTML表單的不同值。</li>
     <li>在通過隱藏對象來減少頁數時， abspagount方法返回不正確的值。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>頁內容</td>
   <td>從表單的指定頁面檢索表單設計對象的類型。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>確定當前窗體的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法返回PDF和HTML表單的不同值。</li>
     <li>在通過隱藏對象來減少頁數時， abspagount方法返回不正確的值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 項目 {#items}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 存在 | 指定對象的可見性。 | 無 |

## 窗體計算 {#formcalc}

FormCalc是一種特定於XFA的語言，用於建立以電子錶單為中心的邏輯和計算根。 FormCalculation提供一組功能強大的生成函式。

### FormCalc支援的函式 {#formcalc-supported-functions}

### FormCalc表達式支援 {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>類別 </strong></td>
   <td><strong>說明 </strong></td>
   <td><strong>範例 </strong></td>
  </tr>
  <tr>
   <td>簡單表達式</td>
   <td>加、減、乘、除和括弧</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>變數聲明</td>
   <td>定義變數</td>
   <td>var<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>邏輯表達式</td>
   <td>
    <ul>
     <li>邏輯（和/或）</li>
     <li>比較（大於/小於/等於）</li>
    </ul> </td>
   <td>A或1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A或1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>If表達式</td>
   <td><br type="_moz" /> </td>
   <td>如果(a&gt;b)，則2 endif</td>
  </tr>
  <tr>
   <td>同時</td>
   <td><br type="_moz" /> </td>
   <td>而(ilt 5)do i = i + 1 hile</td>
  </tr>
  <tr>
   <td>代表</td>
   <td><br type="_moz" /> </td>
   <td>i = 100至1 <br /> do s = s + i結束</td>
  </tr>
  <tr>
   <td>每</td>
   <td><br type="_moz" /> </td>
   <td>(1、2、3)中的每個i <br /> do s = s + i結束</td>
  </tr>
  <tr>
   <td>函式聲明</td>
   <td>在FormCalc中定義自定義函式</td>
   <td>func foo(n)do var f = nendfunc</td>
  </tr>
 </tbody>
</table>

### AcrobatAPI支援 {#acrobat-api-support}

1. **算術函式**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. 計數()
   1. 樓層()
   1. 最大值()
   1. 最小值()
   1. Mod()
   1. 捨入()
   1. 總計()

1. **科學功能**

   1. Acos()
   1. 阿辛()
   1. 阿坦()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. 棕褐色()
   1. Exp()
   1. 記錄檔()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2度()
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
   1. 速率()
   1. 術語()

1. **邏輯函式**

   1. 選擇()
   1. If()
   1. 之一()
   1. 在()

1. **字串函式**

   1. 於()
   1. Concat()
   1. 左()
   1. Len()
   1. 低()
   1. Ltrim()
   1. 取代()
   1. 右()
   1. Rtrim()
   1. 空間()
   1. 材料()
   1. Substr()
   1. 上()
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
   <td>此acrobat API將輸出轉儲到JavaScript控制台。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>此acrobat API通過JavaScript彈出菜單發送警報消息。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>使系統播放聲音。</td>
   <td>未執行任何操作。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>向用戶顯示模式對話框。 必須先由用戶關閉模式對話框，然後才能直接使用主機應用程式。</td>
   <td>未執行任何操作。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>在瀏覽器窗口中啟動URL。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>指定JavaScript指令碼和時段。 每經過一段時間就執行指令碼。 此方法的返回值必須保存在JavaScript變數中。 否則，間隔對象將被垃圾收集，這將導致時鐘停止。 要終止定期執行，請將返回的間隔對象傳遞給clearInterval。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>指定JavaScript指令碼和時段。 該指令碼僅在經過一段時間後執行一次。此方法的返回值必須保存在JavaScript變數中。 否則，超時對象將受垃圾收集的影響，這將導致時鐘停止。 要取消超時事件，請將返回的超時對象傳遞給clearTimeOut。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>取消由setInterval方法初始設定的先前註冊的間隔。</td>
   <td>在HTML5窗體中，API無法正確運行。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>取消以前註冊的超時間隔。 此間隔最初由setTimeOut設定。</td>
   <td>在HTML5窗體中，API無法正確運行。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>運行給定指令碼。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>包含每個活動文檔的Doc對象的陣列。 如果沒有活動文檔，則activeDocs將不返回任何內容；即，它在核心JavaScript中與d =新Array(0)的行為相同。</td>
   <td>返回HTMl5表單的空陣列。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>如果為true（預設值），則可以執行計算。 如果為false，則不允許計算。</td>
   <td>HTMl5Forms始終正確。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>用於保持各種常數值的包裝對象。 當前，此屬性返回具有單個屬性的對象， align。</td>
   <td>HTML5表單返回空對齊對象。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>開啟和關閉聚焦矩形。 焦點矩形是圍繞按鈕、複選框、單選按鈕和簽名的模糊虛線，以指示表單域具有鍵盤焦點。 值為true會開啟聚焦矩形。</td>
   <td>對於HTML5窗體始終為true。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>查看器表單軟體的版本號。 如果希望在指令碼中保持向後相容性，請檢查此屬性以確定軟體較新版本中的對象、屬性或方法是否可用。</td>
   <td>11.001。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>正在運行的Acrobat查看器的語言。</td>
   <td>HTMl5窗體始終為"ENU"。</td>
  </tr>
 </tbody>
</table>

## 支援的XFA事件 {#supported-xfa-events}

支援以下客戶端XFA事件：

* 初始化
* 驗證
* 計算
* 按一下
* 輸入
* 結束
* 更改
* 驗證狀態

>[!NOTE]
>
>HTML5表單在客戶端（瀏覽器）上呈現。 建議使用客戶端 **驗證** 和 **計算** 指令碼而不是伺服器端指令碼。
