---
title: 在互動式通訊中使用圖表
description: 在互動式通訊中使用圖表，您可以將大量資訊壓縮成易於分析的視覺格式
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 0f877a15-a17f-427f-8d89-62ada4d20918
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 1%

---

# 在互動式通訊中使用圖表{#using-charts-in-interactive-communications}

圖表或圖表是資料的視覺化表示法。 它會將大量資訊壓縮為容易理解的視覺格式，讓互動式通訊的收件者更能將複雜資料視覺化、解讀及分析。

建立互動式通訊時，您可以新增圖表，以視覺化方式呈現互動式通訊表單資料模型中的二維資料。 「圖表」元件可讓您新增及設定下列型別的圖表：圓形圖、直條圖、環形圖、橫條圖、折線圖、折線圖和點圖、點圖、區域圖以及象限圖。

## 在互動式通訊中新增及設定圖表 {#add-and-configure-chart-in-an-interactive-communication}

執行以下步驟，在互動式通訊中新增及設定圖表：

1. 從互動式通訊的Sidekick中選取&#x200B;**元件**。
1. 將&#x200B;**圖表**&#x200B;元件拖放至下列其中一個元件：

   * 列印管道：目標區域或影像欄位
   * Web channel：面板或目標區域

1. 在互動式通訊編輯器中選取圖表元件，並從元件工具列選取&#x200B;**[!UICONTROL 設定(]** ![configure_icon](assets/configure_icon.png))。

   圖表屬性會顯示在左窗格中。

   ![列印通道中折線圖的基本屬性](assets/chart_properties_print_new.png)

   列印管道中折線圖的基本屬性

   ![Web Channel中折線圖的基本屬性](assets/chart_properties_web_new.png)

   Web Channel中折線圖的基本屬性

1. 根據通道型別設定[圖表屬性](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties)。
1. （僅列印通道）在&#x200B;**[!UICONTROL 代理程式設定]**&#x200B;中，指定代理程式是否必須使用此圖表。 如果未選取代理程式使用此圖表&#x200B;]**選項，代理程式可以在Agent UI的**[!UICONTROL &#x200B;內容&#x200B;]**標籤中選取圖表的眼睛圖示，以顯示或隱藏圖表。**[!UICONTROL 

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. 選取![done_icon](assets/done_icon.png)以儲存圖表屬性。

   選取&#x200B;**[!UICONTROL 預覽]**&#x200B;以檢視與圖表關聯的外觀和資料。 選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以重新設定圖表內容。

## 設定圖表屬性 {#configure-chart-properties}

為列印和Web通道建立圖表時，請設定下列屬性：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
   <td>通道類型</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>圖表元素的識別碼。 在此欄位中指定的圖表名稱在圖表上不可見。 當從其他元件、指令碼和SOM運算式參照元素時，就會使用它。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>圖表類型</td>
   <td>您要產生的圖表型別。 可用的選項有「圓餅圖」、「欄」、「環圈圖」、「長條圖」、「直線」、「線和點」、「點」和「區域」。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>數列&gt;多個數列</td>
   <td>選取此項可為繪製在X軸和Y軸上的表單資料模型集合專案新增多個系列。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>系列&gt;資料模型物件</td>
   <td>要新增多個序列至圖表的表單資料模型集合專案名稱。<br />為繪製在X軸和Y軸上的屬性選擇父級表單資料模型物件屬性，以形成有意義的系列。 您繫結的資料模型物件必須是Number、String或Date型別。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>顯示排列</td>
   <td>選擇將各系列的數值排列成序。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>X軸&gt;標題</td>
   <td>X軸的標題。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>X軸&gt;資料模型物件</td>
   <td><p>將在X軸繪製的表單資料模型集合專案的名稱。</p> <p>選擇相同父資料模型物件的兩個集合/陣列型別屬性，這些屬性彼此有意義，以便繪製在圖表的X軸和Y軸上。 您繫結的資料模型物件必須是Number、String或Date型別。</p> </td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>Y軸&gt;標題</td>
   <td>Y軸的標題。 </td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>Y軸&gt;資料模型物件</td>
   <td><p>將在Y軸繪製的表單資料模型集合專案。 在「列印」管道中，Y軸的資料模型物件應為「數字」型別。</p> <p>選擇相同父資料模型物件的兩個集合/陣列型別屬性，這些屬性彼此有意義，以便繪製在圖表的X軸和Y軸上。 </p> </td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>Y軸&gt;函式</td>
   <td>用於計算y軸值的統計/自訂函式。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>隱藏物件</td>
   <td>選取以在最終輸出中隱藏圖表。</td>
   <td>列印和網頁</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>圖表的標題。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>圖表的高度（畫素）。</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>寬度</td>
   <td>圖表的寬度（畫素）。 您可以使用樣式圖層或套用佈景主題，控制Web Channel中的圖表寬度。</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>強制之前的分頁符號</td>
   <td>選取此項可在圖表前新增強制分頁符號，並將圖表放在新頁面的頂端。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>強制之後的分頁符號</td>
   <td>選取此項可在圖表後新增必要的分頁符號，並將圖表後的內容放在新頁面的頂端。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>縮排</td>
   <td>圖表從頁面左側的縮排。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>工具提示</td>
   <td><p>工具提示在Web Channel圖表資料點滑鼠游標上顯示的格式。 預設值為${x}(${y})。 根據圖表型別，當您將滑鼠指向圖表的點、長條圖或分割圖時，變數${x}和${y}會以X軸和Y軸上的對應值動態取代，並顯示在工具提示中。</p> <p>若要停用工具提示，請保留<span class="uicontrol">工具提示</code> 欄位空白。 此選項不適用於折線圖和面積圖。 例如，請參閱<a href="#chartoutputprintweb">範例1：列印和網頁中的圖表輸出</a>。</p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>圖表專屬設定</td>
   <td><p>除了常用組態外，還提供下列圖表專用組態：</p>
    <ul>
     <li><strong>顯示圖例： </strong>啟用時顯示圓形圖或環圈圖的圖例。</li>
     <li><strong>圖例位置： </strong>指定圖例相對於圖表的位置。 可用的選項有「右」、「左」、「上」和「下」。 在列印管道中使用右邊的圖例。</li>
     <li><strong>內徑</strong>：可用於環形圖，以指定圖表中內圓的半徑（畫素）。</li>
     <li><strong>線條色彩</strong>：可用於線條、線條、點和面積圖，以指定圖表中線條的色彩。</li>
     <li><strong>點色彩</strong>：可用於點、線和點圖表，以指定圖表中的點色彩。<br /> </li>
     <li><strong>區域色彩</strong>：可用於區域圖，以指定圖表中線段下方的區域色彩。</li>
     <li><strong>參考點&gt;繫結型別： </strong>可供象限圖表使用，以<strong> </strong>指定參考點的繫結型別。 使用靜態文字或資料模型物件屬性來定義參考點的值。</li>
     <li><strong>參考點&gt; X軸： </strong>如果選取<span class="uicontrol">靜態，可用於象限圖</code> 從「繫結型別」下拉式清單中，指定參照點的X軸值。</li>
     <li><strong>參考點&gt; Y軸： </strong>如果選取<span class="uicontrol">靜態，可用於象限圖</code> 從「繫結型別」下拉式清單中，指定參照點的Y軸值。</li>
     <li><strong>參考點&gt;數列的資料模型物件： </strong>如果您選取<span class="uicontrol">資料模型物件，則可用於多個數列象限圖表</code> 從「繫結型別」下拉式清單。 定義表單資料模型物件屬性，以識別參考點的系列。 </li>
     <li><strong>參考點&gt;數列的資料模型物件值： </strong>如果您選取<span class="uicontrol">資料模型物件，則可用於多個數列象限圖表</code> 從「繫結型別」下拉式清單。 使用系列表單資料模型物件屬性，以及此欄位中定義的值來識別參考點的系列。</li>
     <li><strong>參考點&gt;參考點的資料模型物件： </strong>如果選取<span class="uicontrol">資料模型物件，可用於象限圖</code> 從「繫結型別」下拉式清單。 定義與X軸和Y軸上繪製的屬性同等的表單資料模型物件屬性。 此外，對於多個系列，定義資料模型物件屬性，該屬性是為系列定義的資料模型物件屬性的子實體。</li>
     <li><strong>參考點&gt;參考點的資料模型物件值： </strong>如果選取<span class="uicontrol">資料模型物件，可用於象限圖</code> 從「繫結型別」下拉式清單。 使用表單資料模型物件屬性作為參考點，使用此欄位中定義的值來識別圖表的參考點。<br /> <strong>象限標籤&gt;左上方：</strong>可用於象限圖表，以指定左上方象限的名稱。</li>
     <li><strong>象限標籤&gt;右上方：</strong>可用於象限圖表，以指定右上象限的名稱。</li>
     <li><strong>象限標籤&gt;右下方： </strong>可供象限圖表指定右下象限的名稱。</li>
     <li><strong>象限標籤&gt;左下方： </strong>可用於象限圖表，以指定左下方的象限名稱。</li>
    </ul> </td>
   <td>列印和網頁</td>
  </tr>
 </tbody>
</table>

## 在圖表中使用函式 {#use-functions-in-chart}

您可以設定圖表以使用統計函式來計算來源資料的值，以便在圖表上繪圖。 透過在圖表中套用函式，您可以繪圖表單資料模型不直接提供的資料。

圖表中的![函式](assets/functions_charts_new.png)

雖然圖表元件隨附一些內建函式，但您可以撰寫[自訂函式](#customfunctionsweb)，使其可用於Web Channel的圖表設定。

下列函式預設可用於圖表元件：

**平均值(Average)**&#x200B;傳回X或Y軸上指定值在其他軸上的平均值。

**Sum**&#x200B;傳回X或Y軸上指定值在其他軸上的總和。

**Maximum**&#x200B;傳回X或Y軸上指定值在另一個軸上的最大值。

**Frequency**&#x200B;傳回X或Y軸上另一個軸上指定值的值數目。

**Range**&#x200B;傳回X或Y軸上指定值在另一個軸上的最大值和最小值之間的差異。

**中位數**&#x200B;傳回將另一個軸上指定值在X或Y軸上一半的高值和低值分隔開的值。

**最小值**&#x200B;傳回X或Y軸上指定值在其他軸上的最小值。

**Mode**&#x200B;傳回另一個座標軸上指定值在X或Y座標軸上出現次數最多的值。

如需詳細資訊，請參閱[範例2：在折線圖](#applicationsumfrequency)中套用Sum和Frequency函式。

### Web Channel中的自訂函式 {#customfunctionsweb}

除了在圖表中使用預設函式之外，您還可以在JavaScript中編寫自訂函式，並™Web channel的Chart元件中，讓這些函式可在函式清單中使用。

函式將一或多個值和類別名稱視為輸入並傳回值。 例如：

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

編寫自訂函式後，請執行以下操作以使其可用於圖表設定：

1. 在與相關互動式通訊相關聯的使用者端資料庫中新增自訂函式。 如需詳細資訊，請參閱[設定送出動作](/help/forms/using/configuring-submit-actions.md)和[使用使用者端資料庫](/help/sites-developing/clientlibs.md)。

1. 若要在「函式」下拉式清單中顯示自訂函式，請在CRXDe Lite的apps資料夾中建立具有以下屬性的`nt:unstructured`節點：

   * 新增值為`fd/af/reducer`的屬性`guideComponentType`。 （必要）

   * 將屬性`value`新增至自訂JavaScript™函式的完整名稱。 （必要），並將其值設為自訂函式的名稱，例如Multiply。
   * 新增屬性`jcr:description`，其值要顯示為「函式」下拉式清單中自訂函式的名稱。 例如，**乘**。

   * 新增屬性`qtip`，其值將是自訂函式的簡短描述。 將指標暫留在&#x200B;**函式**&#x200B;下拉式清單中的函式名稱上時，它會顯示為工具提示。

1. 按一下「儲存全部&#x200B;**」**&#x200B;以儲存組態。

函式現在可用於圖表中。

## 範例1：列印和網頁中的圖表輸出 {#chartoutputprintweb}

在「基本」標籤中，您可以定義圖表型別、包含資料的來源表單資料模型屬性、要在圖表的X軸和Y軸繪製的標籤，以及可選的統計函式，以計算圖表上繪製的值。

讓我們透過使用互動式通訊產生的卡片陳述式，詳細瞭解基本屬性中最低必要資訊。 假設您要產生圖表，以描述對帳單中不同費用的金額。 您想要使用不同型別的圖表來列印互動式通訊及Web輸出。

### 列印用的柱狀圖 {#columnchartprint}

若要完成此作業，請指定下列屬性：

* **[!UICONTROL 名稱]** — 指定圖表的名稱。
* **[!UICONTROL 圖表型別]** — 從下拉式清單中選取&#x200B;**資料行**。
* **[!UICONTROL 標題]** — 指定X軸的費用型別和Y軸的交易金額。
* **[!UICONTROL 資料模型物件]** — 選取資料模型物件屬性，以建立X軸（費用型別）和Y軸（交易金額）的資料繫結。

![互動式通訊列印管道中的直條圖](assets/sample_chart_print_column_new.png)

互動式通訊列印管道中的直條圖

### 適用於Web的環形圖 {#donutchartweb}

若要完成此作業，請指定下列屬性：

* **[!UICONTROL 名稱]** — 指定圖表的名稱。
* **[!UICONTROL 圖表型別]** — 從下拉式清單中選取&#x200B;**[!UICONTROL 環形圖]**。
* **[!UICONTROL 資料模型物件]** — 選取資料模型物件屬性，以建立X軸（費用型別）和Y軸（交易金額）的資料繫結。
* **[!UICONTROL 內徑]** — 指定內徑值為150，以指定圖表內圓的半徑（畫素）。
* **[!UICONTROL 工具提示]** — 使用${x}(${y})預設格式來顯示工具提示。 工具提示顯示為：費用型別（交易金額）。 範例：Bitcoin(10000)的Debit。

互動式通訊的Web channel中的![環形圖](assets/sample_chart_web_new.png)

互動式通訊Web channel中的環形圖

## 範例2：在折線圖中使用總和和和頻率函式 {#applicationsumfrequency}

透過在圖表中套用函式，您可以繪圖表單資料模型不直接提供的資料。 在此範例中，我們使用信用卡對帳單範例來瞭解如何將總和和和頻率函式套用至圖表。

![沒有函式的折線圖，具有兩個「AirBnB借記」交易](assets/line_chart_web_new.png)

沒有函式的折線圖，具有兩個「AirBnB的借方」交易

### Sum函式 {#sum-function}

您可以套用sum函式將相同資料屬性的多個執行個體的值相加，並且只顯示一次。 例如，在下圖中，Sum函式套用在Y軸，以加總兩個AirBnB交易（2050和1050）的Debit金額，並且只顯示一個交易(3100)。

當您想要為相同資料屬性的許多執行個體進行排序及顯示總和時，Sum函式可讓圖表變得更實用。

![折線圖總和](assets/line_chart_web_sum_new.png)

### 頻率函式 {#frequency-function}

Frequency函式會傳回另一個軸上指定值Y軸的值數目。 在Y軸（「交易金額」）上套用「頻率」函式後，圖表顯示AirBnB交易出現兩次「借方」，其餘交易型別出現一次。

![折線圖頻率](assets/line_chart_web_functions_frequency_new.png)

## 範例3：Web中的多系列象限圖 {#example-multi-series-quadrant-chart-in-web}

圖表會繪製在特定日期範圍內執行的交易金額。 象限圖表可將圖表區域分成四個標示的區段。 字元會針對X軸和Y軸使用靜態參考點。 使用多重序列功能，根據銀行名稱來分隔資料。

若要完成此作業，請指定下列屬性：

* **名稱：**&#x200B;指定圖表的名稱。
* **圖表型別：**&#x200B;從下拉式清單中選取&#x200B;**象限**。

* 選取&#x200B;**多個系列**&#x200B;核取方塊。
* **資料模型物件**：指定系列的資料模型物件屬性。 銀行名稱的資料模型物件屬性是以X軸和Y軸繪製的資料模型物件屬性的父項。
* **資料模型物件：**&#x200B;選取資料模型物件屬性，以建立X軸（交易日期）和Y軸（交易金額）的資料繫結。
* 在&#x200B;**參考點**&#x200B;區段中，選取&#x200B;**靜態**&#x200B;做為繫結型別。

* 指定X軸和Y軸參照點的值。
* 指定左上、右上、右下和左下象限的象限標籤。
* 選取&#x200B;**顯示圖例**&#x200B;核取方塊，以顯示銀行名稱的顏色代碼。

![象限圖](assets/charts_quadrant_example_new.png)
