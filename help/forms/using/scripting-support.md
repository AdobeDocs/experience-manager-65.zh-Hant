---
title: HTML5表單的指令碼支援
description: HTML5 Forms支援的JavaScript、FormCalc屬性及其他方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: HTML5 Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '3916'
ht-degree: 6%

---

# HTML5表單的指令碼支援 {#scripting-support-for-html-forms}

HTML5表單中支援的JavaScript、FormCalc屬性和方法如下所示：

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
   <td>指定欄位在回應使用者的動作而變更前的內容。 此值可以恢復，類似於恢復功能。</td>
   <td><p>下拉式清單和清單方塊無法運作。 <code>PrevText </code>在下列情況下無法正常運作：</p>
    <ul>
     <li>在iPad的數值欄位中輸入一些特殊字元鍵（例如$、、、或&amp;或@等等）時，以及 </li>
     <li>針對「日期」欄位（透過行事曆輸入日期時）。<br /> </li>
    </ul> <p>不支援透過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>指定事件對其採取動作的物件。</td>
   <td>不支援透過指令碼設定值。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>指定欄位在回應使用者動作而變更後的內容。</td>
   <td><p>此 <code>newText</code> 屬性在下列情況下無法正常運作：</p>
    <ul>
     <li>在選取 — 取代文字時</li>
     <li>在刪除、複製和貼上文字時。</li>
     <li>在數值欄位中輸入一些特殊字元鍵時（例如，$或、&amp;或@等）<br /> </li>
     <li>使用Shift+英數字元組合時。 </li>
     <li>使用日期/時間欄位時。</li>
    </ul>
    <div>
      不支援透過指令碼設定值。
    </div> </td>
  </tr>
  <tr>
   <td>變更</td>
   <td>指定使用者執行動作後，立即輸入或貼到欄位中的值。 </td>
   <td><p>變更屬性在下列情況下無法正常運作：</p>
    <ul>
     <li>在選取 — 取代文字時</li>
     <li>在刪除、複製和貼上文字時。</li>
     <li>在數值欄位中輸入一些特殊字元鍵時（例如，$或、&amp;或@等）<br /> </li>
     <li>使用Shift+英數字元組合時。 </li>
     <li>使用日期/時間欄位時。</li>
    </ul> <p>不支援透過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td>向下鍵</td>
   <td>決定使用者是否按箭頭鍵進行選取。 此屬性僅適用於清單方塊和下拉式清單。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>修飾元</td>
   <td>決定當特定事件執行時，是否按住修飾元鍵(例如Microsoft® Windows®上的Ctrl)。</td>
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
   <td>傳回主機的應用程式型別。 僅適用於使用者端應用程式。</td>
   <td>傳回 <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>傳回目前應用程式的名稱。</td>
   <td>傳回瀏覽器名稱及其版本。 例如，在Chrome瀏覽器中，傳回值為 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>傳回檔案中的頁數。</td>
   <td>HTML5表單的分頁原則與PDF forms分頁原則不同。 因此，在這兩種情況下， numPages API都可以傳回不同的值。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>傳回代表執行指令碼之電腦平台的字串。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>指定檔案的標題。 它僅適用於使用者端應用程式。</td>
   <td>它會傳回表單中HTML檔案的標題，而不是像存在PDF forms一樣傳回表單中繼資料標題。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>傳回代表目前應用程式版本編號的字串。</td>
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
   <td>移至上一頁。</td>
   <td>HTML5表單不遵循與PDF表單相同的分頁原則，因此HTML5表單的上一頁與PDF表單的上一頁不同。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>移至表單的下一頁。 在執行階段使用pageDown方法。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>將鍵盤焦點設定為指定的欄位。 欄位會指定為物件，或由欄位的SOM運算式指定。 它僅適用於使用者端應用程式。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>將檔案中的欄位重設為預設值。</td>
   <td>清除具有合併資料的表單中的所有資料，而不是將其還原為預設值。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>在熒幕上顯示對話方塊。 它僅適用於使用者端應用程式</td>
   <td>型別為「是/否」的MessageBox會轉換為「確定/取消」。 不支援含有三個按鈕的訊息方塊。</td>
  </tr>
  <tr>
   <td>currentpage</td>
   <td><p>在執行階段設定檔案的目前作用中頁面。</p> <p>頁面值是以0為基礎，因此檔案的第一頁會傳回0值。</p> <p>在使用者端上執行layout：ready時，currentPage屬性可用。 但是，當layout：ready在伺服器上執行時則無法使用，因為屬性要等到表單配置執行後才會執行。</p> </td>
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
   <td>控制關聯物件在不同處理階段的參與情況。 如果物件是容器，則容器的內容會繼承此控制項套用的任何限制。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>控制內容的使用者存取權。</td>
   <td>不適用於排除群組。 此外，HTML5表單對非互動和受保護物件也提供相同的處理方式。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>HTML5表單不允許設定物件的名稱屬性。 這是HTML5表單的唯讀屬性。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>包含單一資料內容單位的內容元素。</td>
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
   <td>設定 <code>formattedValue</code> 不支援透過指令碼。</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>指定此欄位的編輯值。</td>
   <td>設定 <code>editValue </code>不支援透過指令碼。</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>指定此欄位的格式驗證訊息字串。</td>
   <td>設定 <code>formatMessage </code>不支援透過指令碼。</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>指定此欄位的背景色彩值。 您需要將border.fill.presence屬性設定為單獨可見。</td>
   <td>它無法正確傳回欄位的預設顏色。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>border物件描述物件周圍的邊框。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui物件會包含表單物件的使用者介面說明。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>指定欄位的nullTest值。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>指定此欄位的邊框色彩值。 您必須將border.edge.presence屬性設定為個別可見。</td>
   <td>它無法正確傳回欄位的預設邊框顏色。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>清單中的專案數。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>將新專案新增到目前欄位。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>移除欄位中的所有專案。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>取得下拉式清單或清單方塊之特定顯示專案的繫結值。</td>
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
   <td>傳回指定專案的選取狀態</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>設定指定專案的選取狀態。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>擷取指定專案索引的專案顯示文字。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>擷取指定專案索引的資料值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>刪除指定索引處的專案。</td>
   <td>無</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>設定目前欄位中的指定專案。 它會取代現有的專案。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定版面寬度的測量值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的x座標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的y座標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>註解</td>
   <td>註解物件說明與表單設計物件關聯的描述性標籤。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者所提供資料的驗證。 驗證物件可在表單的生命週期中多次啟動。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>指定此欄位的父子表單（頁面）。</td>
   <td>一律會傳回父項子表單，而非傳回第一個非領域化的父項子表單。<br /> </td>
  </tr>
  <tr>
   <td>選定索引</td>
   <td>第一個選取專案的索引。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 表單 {#form}

| **屬性** | **說明** | **例外** |
|---|---|---|
| formNodes | 傳回繫結至指定資料物件的所有表單模型物件清單。 |  |

## InstanceManager {#instancemanager}

| 屬性 | 說明 |
|---|---|
| `name` | 用於在指令碼運算式中識別此元素的識別碼。 |
| `occur` | 說明其封閉容器允許執行個體數目的限制。 |
| `min` | 指定可具現化的執行個體數目下限。 |
| `max` | 指定可具現化的執行個體數目上限。 |
| `count` | 指定目前具現化的執行個體數目。 |
| `setInstances` | 從此節點新增或移除指定的子表單或子表單集。 |
| `addInstance` | 將子表單或子表單集的新執行個體新增到此節點。 |
| `removeInstance` | 從此節點移除子表單或子表單集。 |
| `moveInstance` | 將表單模型物件的子物件移至表單模型內的另一個指定位置。 物件的對應資料模型資訊也會在資料模型中重新定位。 |
| `insertInstance` | 將子表單或子表單集的新執行個體插入此節點。 |

## list {#list}

| 屬性 | 說明 |
|---|---|
| `length` | 清單中的元素數量。 |
| `item` | 集合中從零開始的索引。 |
| `append` | 在節點清單的結尾附加節點。 |
| `remove` | 從節點清單移除節點。 |
| `insert` | 在節點清單中的特定節點之前插入節點。 |

## 節點 {#node}

| 屬性 | 說明 | 例外 |
|---|---|---|
| createNode | 根據有效的類別名稱建立新節點。 | 無 |
| `isContainer` | 指定此物件是否為容器物件。 | 無 |
| `isNull` | 指出目前的資料值是否為Null值。 | 無 |
| `resolveNode` | 從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。 | 無 |
| `resolveNodes` | 從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。 | 無 |
| oneOfChild | 根據有效的類別名稱建立新節點。 | 無 |
| getElement | 傳回指定的子物件。 | 無 |
| getAttribute | 取得指定的屬性值。 | 無 |
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
   <td>指定物件相對於其他例項化執行個體的索引。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>執行物件的事件指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>傳回子表單（含）中包含且未通過驗證測試的節點清單。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>border物件描述物件周圍的邊框。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此欄位的邊框色彩值。 您必須將border.edge.presence屬性設定為個別可見。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定版面寬度的測量值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的x座標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的y座標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者所提供資料的驗證。 驗證物件可在表單的生命週期中多次啟動。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>是否存在</td>
   <td>指定物件的可見性。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>存取</td>
   <td>控制使用者對容器物件（如子表單）內容的存取權。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>execvalidate</td>
   <td>根據子表單或子表單集相對於相同表單物件其他例項的位置計算其索引。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager物件可管理表單模型物件的建立、移除和移動。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

### 提交 {#submit}

| 屬性 | 說明 |
|---|---|
| 目標 | 資料所要提交的URL。 遺漏此屬性表示XFA處理應用程式會使用產品特定技術取得URI，例如存取設定物件中的產品特定資訊。 |

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
   <td>傳回目前物件之所有子物件的清單。</td>
   <td>
    <ul>
     <li>不支援xfa.nodes、desc</li>
     <li>針對PDF和HTML報告的節點數不同。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定此節點的名稱。</td>
   <td>HTML中不允許使用指令碼設定名稱。</td>
  </tr>
  <tr>
   <td>父母</td>
   <td>取得此節點的父系。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>索引</td>
   <td>傳回此節點在其類似名稱、範圍內、類似子系關係節點的集合中的位置。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>somexpression</td>
   <td>取得此節點的SOM運算式。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。</td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 子表單集 {#subformset}

| 屬性 | 說明 | 例外 |
|---|---|---|
| instanceManager | instanceManager物件可管理表單模型物件的建立、移除和移動。 | 無 |

## content {#content}

| **屬性** | **說明** | **例外** |
|---|---|---|
| isNull | 指出目前的資料值是否為null值。 |  |

## 資料值 {#datavalue}

| **屬性** | **說明** | **例外** |
|---|---|---|
| isNull | 指出目前的資料值是否為null值。 |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>屬性 </strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性描述圖樣物件的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 填滿 {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>顏色屬性會定義填色的唯一顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
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
   <td>color屬性說明表單上線性漸層填色的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
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
   <td>edge</td>
   <td>edge物件會描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。<br /> </td>
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
   <td>color屬性描述圖樣物件的獨特顏色。 </td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 半徑 {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性說明放射狀物件的獨特顏色</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 點綴 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性說明點綴物件的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>屬性</td>
   <td>說明</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui物件會包含表單物件的使用者介面說明。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>註解</td>
   <td>註解物件說明與表單設計物件關聯的描述性標籤。</td>
   <td> </td>
  </tr>
  <tr>
   <td>是否存在</td>
   <td>指定物件的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定可用於在指令碼運算式中指定此物件或事件的識別碼。</td>
   <td>不支援在執行階段設定值</td>
  </tr>
  <tr>
   <td>值</td>
   <td>value物件會包含單一資料內容單位。<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 轉角 {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>色彩</td>
   <td>color屬性說明轉角物件的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
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
   <td>border物件描述了checkButton物件周圍的邊框。 </td>
   <td>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。<br /> </td>
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
   <td>border物件描述了choiceList物件周圍的邊框。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊框 | border物件說明圍繞dateTimeEdit物件的邊框。 |  |

## 影像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>contenttype</td>
   <td>指定參考檔案中的內容型別，以MIME型別表示。</td>
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
| 邊框 | border物件說明imageEdit物件周圍的邊框。 |  |

## numericEdit {#numericedit}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 邊框 | border物件描述物件周圍的邊框。 | 無 |

## 物件 {#object}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>類別名稱</td>
   <td>決定此物件的類別名稱。<br /> </td>
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
   <td>edge</td>
   <td>edge物件會描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。</td>
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
   <td>border物件描述物件周圍的邊框。<br /> </td>
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
   <td>指定此物件要使用的版面配置策略。</td>
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
   <td>指定此欄位的邊框色彩值。您必須先定義邊框，才能透過指令碼變更顏色。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>指定此欄位的邊框寬度。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度測量。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>暫時性</td>
   <td>指定處理應用程式是否必須將排除群組的值儲存為表單提交或儲存作業的一部分。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>寫</td>
   <td>指定版面寬度的測量值。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的x座標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的y座標。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>註解</td>
   <td>註解物件說明與表單設計物件關聯的描述性標籤。<br /> </td>
   <td>無</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者所提供資料的驗證。 驗證物件可在表單的生命週期中多次啟動。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>取得合併後表單節點繫結的資料節點。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>是否存在</td>
   <td>指定物件的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>存取</td>
   <td>控制使用者對容器物件（如子表單）內容的存取權。</td>
   <td>對於排除中的個別專案，一律會傳回open。 </td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>指定可用於在指令碼運算式中指定此物件或事件的識別碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>成員</td>
   <td>指定排除群組的成員。 </td>
   <td>無</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>傳回排除群組的選取成員。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>對指定物件的計算事件以及任何子物件執行任何指令碼。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>計算</td>
   <td>計算物件控制欄位值的計算。<br /> </td>
   <td>無</td>
  </tr>
 </tbody>
</table>

## 圓弧 {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>屬性<strong></strong></strong></td>
   <td><strong>說明<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>edge物件會描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。 </td>
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
   <td>edge</td>
   <td>edge物件會描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。 </td>
  </tr>
 </tbody>
</table>

## $layout {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>決定給定表單設計物件的高度。<br /> </td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援Height (h)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>寫</td>
   <td>決定給定表單設計物件的寬度。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援寬度(w)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>決定指定表單設計物件相對於其父物件的x座標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援x座標(x)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>決定指定表單設計物件相對於其父物件的y座標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援y座標(y)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>決定目前表單的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法會為PDF和HTML表單傳回不同的值。</li>
     <li>藉由隱藏物件來減少頁數時，abspagecount方法傳回不正確的值。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>從表單的指定頁面擷取表單設計物件的型別。</td>
   <td>無</td>
  </tr>
  <tr>
   <td>abspagecount</td>
   <td>決定目前表單的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法會為PDF和HTML表單傳回不同的值。</li>
     <li>藉由隱藏物件來減少頁數時，abspagecount方法傳回不正確的值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 項目 {#items}

| **屬性** | **說明** | **例外** |
|---|---|---|
| 是否存在 | 指定物件的可見性。 | 無 |

## FormCal {#formcalc}

FormCalc是XFA專屬的語言，用於建立以電子錶單為中心的邏輯和計算根。 FormCalculation提供了一組強大的建置函式。

### FormCalc支援的函式 {#formcalc-supported-functions}

### FormCalc運算式支援 {#formcalc-expression-support}

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
   <td>變數宣告</td>
   <td>定義變數</td>
   <td>變數a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>邏輯運算式</td>
   <td>
    <ul>
     <li>邏輯（和/或）</li>
     <li>比較（大/小/等）</li>
    </ul> </td>
   <td>A或1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A或1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>If運算式</td>
   <td><br type="_moz" /> </td>
   <td>如果(a&gt;b)則2 endif</td>
  </tr>
  <tr>
   <td>當</td>
   <td><br type="_moz" /> </td>
   <td>當(i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>的</td>
   <td><br type="_moz" /> </td>
   <td>針對i = 100，向下至1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>針對每個</td>
   <td><br type="_moz" /> </td>
   <td>每個i (1， 2， 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>函式宣告</td>
   <td>在FormCalc中定義自訂函式</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API支援 {#acrobat-api-support}

1. **算術函式**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. Count()
   1. Floor()
   1. Max()
   1. Min()
   1. Mod()
   1. Round()
   1. Sum()

1. **科學函式**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. Log()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **財務函式**

   1. 四月()
   1. Term()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. Term()

1. **邏輯函式**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **字串函式**

   1. At()
   1. Concat()
   1. Left()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Replace()
   1. Right()
   1. Rtrim()
   1. Space()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **日期和時間**

   1. Date()
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
   <td>此acrobat API會將輸出傾印至JavaScript主控台。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>此acrobat API會透過JavaScript快顯視窗傳送警示訊息。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>讓系統播放聲音。</td>
   <td>不會執行任何動作。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>向使用者顯示模型對話方塊。 必須先關閉強制回應對話方塊，使用者才能再次直接使用主機應用程式。</td>
   <td>不會執行任何動作。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>在瀏覽器視窗中啟動URL。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>指定JavaScript指令碼和時段。 指令碼會在每次經過期間時執行。 此方法的傳回值必須儲存在JavaScript變數中。 否則，間隔物件會接受記憶體回收，這會導致時鐘停止。 若要終止定期執行，請將傳回的間隔物件傳遞給clearInterval。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>指定JavaScript指令碼和時段。 指令碼只會在經過期間後執行一次。此方法的傳回值必須儲存在JavaScript變數中。 否則，逾時物件會接受記憶體回收，這會導致時鐘停止。 若要取消逾時事件，請將傳回的逾時物件傳遞給clearTimeOut。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>取消先前由setInterval方法設定的登入間隔。</td>
   <td>在HTML5表單中，API無法正常運作。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>取消先前登入的超時間隔。 此間隔最初由setTimeOut設定。</td>
   <td>在HTML5表單中，API無法正常運作。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>執行指定的指令碼。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>包含每個使用中檔案的Doc物件的陣列。 如果沒有使用中的檔案，activeDocs不會傳回任何內容；也就是說，它具有與d =核心JavaScript中的new Array(0)相同的行為。</td>
   <td>傳回HTMl5表單的空白陣列。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>如果為true （預設值），則可執行計算。 如果為false，則不允許計算。</td>
   <td>HTMl5 Forms一律為True。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>用來儲存各種常數值的包裝函式物件。 目前，此屬性會傳回具有單一屬性align的物件。</td>
   <td>HTML5表單傳回空的對齊物件。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>開啟和關閉焦點矩形。 焦點矩形是按鈕、核取方塊、選項按鈕和簽章周圍模糊的虛線，表示表單欄位具有鍵盤焦點。 若值為true，會開啟焦點矩形。</td>
   <td>HTML5表單一律為True。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>檢視器表單軟體的版本號碼。 若要維持指令碼中的回溯相容性，請核取此屬性以判斷較新版本軟體中的物件、屬性或方法是否可用。</td>
   <td>永遠是11.001。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>執行中Acrobat檢視器的語言。</td>
   <td>HTMl5表單一律為「繁體中文」。</td>
  </tr>
 </tbody>
</table>

## 支援的XFA事件 {#supported-xfa-events}

支援下列使用者端的XFA事件：

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
>HTML5表單會在使用者端（瀏覽器）上呈現。 使用使用者端 **驗證** 和 **計算** 指令碼而非伺服器端指令碼。
