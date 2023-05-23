---
title: 在交互通信中使用圖表
seo-title: Chart component in Interactive Communications
description: 在互動式通信中使用圖表，可以將大量資訊壓縮成易於分析的可視格式
seo-description: AEM Forms provides a chart component that you can use to create charts in your Interactive Communication. This document explains basic and agent configurations of the chart component.
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
feature: Interactive Communication
exl-id: 0f877a15-a17f-427f-8d89-62ada4d20918
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2613'
ht-degree: 2%

---

# 在交互通信中使用圖表{#using-charts-in-interactive-communications}

圖表或圖表是資料的可視表示。 它將大量資訊濃縮成易於理解的可視格式，使互動式通信的接收方能夠更好地直觀、解釋和分析複雜的資料。

在建立互動式通信時，可以添加圖表以從互動式通信的表單資料模型直觀地表示二維資料。 圖表元件允許您添加和配置以下類型的圖表：餅圖、列圖、甜圈圖、條圖、線圖、線圖和點圖、點圖、面積圖和像限圖。

## 在交互通信中添加和配置圖表 {#add-and-configure-chart-in-an-interactive-communication}

執行以下步驟以在互動式通信中添加和配置圖表：

1. 點擊 **元件** 從互動交流的旁邊。
1. 拖放 **圖表** 元件到以下元件之一：

   * 打印通道：目標區域或影像欄位
   * Web通道：面板或目標區域

1. 在「交互通信」編輯器中按一下圖表元件並選擇 **[!UICONTROL 配置(]** ![configure_icon](assets/configure_icon.png))。

   圖表屬性顯示在左窗格中。

   ![打印通道中折線型圖表的基本屬性](assets/chart_properties_print_new.png)

   打印通道中折線型圖表的基本屬性

   ![Web通道中線型圖的基本屬性](assets/chart_properties_web_new.png)

   Web通道中線型圖的基本屬性

1. 配置 [圖表屬性](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) 基於頻道類型。
1. （僅打印通道） **[!UICONTROL 代理設定]**，指定代理是否必須使用此圖表。 如果 **[!UICONTROL t是座席使用此圖表的必需項]** 表徵圖 **[!UICONTROL 內容]** 的子菜單。

   ![圖表屬性](assets/chart_agentproperties.png)

1. 點擊 ![完成表徵圖](assets/done_icon.png) 按鈕。

   點擊 **[!UICONTROL 預覽]** 查看與圖表關聯的外觀和資料。 點擊 **[!UICONTROL 編輯]** 重新配置圖表的屬性。

## 配置圖表屬性 {#configure-chart-properties}

在為打印和Web通道建立圖表時配置以下屬性：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
   <td>頻道類型</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>圖表元素的標識符。 在此欄位中指定的圖表名稱在圖表上不可見。 在引用來自其他元件、指令碼和SOM表達式的元素時使用它。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>圖表類型</td>
   <td>要生成的圖表類型。 可用選項有餅圖、列、甜圈、條形、線、線和點、點和區域。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>「系列」&gt;「多個系列」</td>
   <td>選擇以為在X軸和Y軸上繪製的表單資料模型集合項添加多個系列。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>系列&gt;資料模型對象</td>
   <td>向圖表添加多個系列的表單資料模型集合項的名稱。<br /> 為在X軸和Y軸上繪製的屬性選擇父窗體資料模型對象屬性，以形成有意義的系列。 綁定的資料模型對象必須為Number、String或Date類型。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>顯示排列</td>
   <td>選擇將各系列的數值排列成序。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>X軸&gt;標題</td>
   <td>X軸的標題。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>X軸&gt;資料模型對象</td>
   <td><p>要在X軸上繪製的表單資料模型收集項的名稱。</p> <p>選擇相同父資料模型對象的兩個集合/陣列類型屬性，這些屬性對彼此有意義，以在圖表的X軸和Y軸上出圖。 綁定的資料模型對象必須為Number、String或Date類型。</p> </td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>Y軸&gt;標題</td>
   <td>Y軸的標題。 </td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>Y軸&gt;資料模型對象</td>
   <td><p>要在Y軸上繪製的表單資料模型收集項。 在打印通道中，Y軸的資料模型對象應為「編號」類型。</p> <p>選擇相同父資料模型對象的兩個集合/陣列類型屬性，這些屬性對彼此有意義，以在圖表的X軸和Y軸上出圖。 </p> </td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>Y軸&gt;函式</td>
   <td>用於計算Y軸上值的統計/自定義函式。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>隱藏物件</td>
   <td>選擇以在最終輸出中隱藏圖表。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>圖表標題。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>圖表高度（以像素為單位）。</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>寬度</td>
   <td>圖表寬度（以像素為單位）。 可以使用樣式層或通過應用主題來控制Web通道中圖表的寬度。</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>強制分頁符之前</td>
   <td>選擇以在圖表前添加強制分頁符，並將圖表置於新頁的頂部。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>必需的分頁符</td>
   <td>選擇以在圖表後添加強制分頁符，並將圖表後的內容放在新頁面的頂部。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>縮排</td>
   <td>圖表從頁面左側縮進。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>工具提示</td>
   <td><p>工具提示在Web通道圖表中資料點上滑鼠上顯示的格式。 預設值為${x}(${y})。 根據圖表類型，當您將滑鼠指向圖表中的點、條或切片時，變數${x}和${y}將動態地替換為X軸和Y軸上的相應值，並顯示在工具提示中。</p> <p>要禁用工具提示，請保留 <span class="uicontrol">工具提示</code> 欄位為空。 此選項不適用於折線圖和面積圖。 例如，請參見 <a href="#chartoutputprintweb">示例1:打印和Web中的圖表輸出</a>。</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>圖表特定的配置</td>
   <td><p>除了常用配置外，還提供以下圖表特定的配置：</p>
    <ul>
     <li><strong>顯示圖例： </strong>啟用時顯示餅圖或甜圈圖的圖例。</li>
     <li><strong>圖例位置： </strong>指定圖例相對於圖表的位置。 可用選項有「右」、「左」、「上」和「下」。 建議在打印通道中使用右側圖例。</li>
     <li><strong>內半徑</strong>:可用於「圓圈」圖表指定圖表中內圓的半徑（以像素為單位）。</li>
     <li><strong>線條顏色</strong>:可用於折線圖、折線圖、點圖和面積圖以指定圖表中折線的顏色。</li>
     <li><strong>點顏色</strong>:可用於點圖、折線圖和點圖以指定圖表中點的顏色。<br /> </li>
     <li><strong>區域顏色</strong>:「面積圖」可用於指定圖表折線下區域的顏色。</li>
     <li><strong>「參照點」(Reference Point)&gt;「綁定類型」(Binding Type): </strong>可用於像限圖<strong> </strong>指定參照點的綁定類型。 使用靜態文本或資料模型對象屬性來定義參考點的值。</li>
     <li><strong>參照點&gt; X軸： </strong>如果選擇，則可用於像限圖 <span class="uicontrol">靜態</code> 從「綁定類型」(Binding Type)下拉清單中為參照點指定X軸值。</code></li>
     <li><strong>參照點&gt; Y軸： </strong>如果選擇，則可用於像限圖 <span class="uicontrol">靜態</code> 從「綁定類型」(Binding Type)下拉清單中為參照點指定Y軸值。</code></li>
     <li><strong>「參考點」(Reference Point)&gt;「系列的資料模型對象」(Data Model Object for Series): </strong>如果選擇，則可用於多個系列像限圖 <span class="uicontrol">資料模型對象</code> 從「綁定類型」下拉清單中。 定義表單資料模型物件屬性以確認參考點的系列. </code></li>
     <li><strong>「參考點」(Reference Point)&gt;「系列的資料模型對象值」(Data Model Object Value for Series): </strong>如果選擇，則可用於多個系列像限圖 <span class="uicontrol">資料模型對象</code> 從「綁定類型」下拉清單中。 使用系列的表單資料模型對象屬性和此欄位中定義的值來標識參考點的系列。</code></li>
     <li><strong>「參照點」(Reference Point)&gt;「參照點的資料模型對象」(Data Model Object for Reference Point): </strong>如果選擇，則可用於像限圖 <span class="uicontrol">資料模型對象</code> 從「綁定類型」下拉清單中。 定義表單資料模型對象屬性，該屬性是X軸和Y軸上繪製的屬性的同級。 此外，對於多個系列，定義資料模型對象屬性，該屬性是為系列定義的資料模型對象屬性的子實體。</code></li>
     <li><strong>「參照點」(Reference Point)&gt;「參照點的資料模型對象值」(Data Model Object Value for Reference Point): </strong>如果選擇，則可用於像限圖 <span class="uicontrol">資料模型對象</code> 從「綁定類型」下拉清單中。 使用表單資料模型對象屬性作為參考點，以及在此欄位中定義的值來標識圖表的參考點。<br /> <strong>像限標籤&gt;左上：</strong> 可用於像限圖以指定左上像限的名稱。</code></li>
     <li><strong>像限標籤&gt;右上：</strong> 可用於像限圖以指定右上像限的名稱。</li>
     <li><strong>像限標籤&gt;右下： </strong>可用於像限圖以指定右下像限的名稱。</li>
     <li><strong>像限標籤&gt;左下： </strong>可用於像限圖以指定左下像限的名稱。</li>
    </ul> </td>
   <td>打印和Web</td>
  </tr>
 </tbody>
</table>

## 在圖表中使用函式 {#use-functions-in-chart}

您可以配置圖表，使用統計函式從源資料計算值以在圖表上繪製。 通過在圖表中應用函式，可以繪製表格資料模型未直接提供的資料。

![圖表中的函式](assets/functions_charts_new.png)

當圖表元件附帶一些內置函式時，您可以編寫 [自定義函式](#customfunctionsweb) 並使其可用於Web通道的圖表配置中。

預設情況下，圖表元件可以使用以下函式：

**平均值（平均值）** 返回X軸或Y軸上其它軸上給定值的平均值。

**和** 返回X軸或Y軸上其它軸上給定值的所有值之和。

**最大** 返回X軸或Y軸上其它軸上給定值的最大值。

**頻率** 返回X軸或Y軸上其它軸上給定值的值數。

**範圍** 返回X軸或Y軸上給定值在其它軸上的最大值和最小值之間的差。

**中值** 返回在X軸或Y軸上對另一軸上的給定值以半分隔高值和低值的值。

**最小** 返回X軸或Y軸上其它軸上給定值的最小值。

**模式** 返回X軸或Y軸上具有其它軸上給定值的最多值。

有關詳細資訊，請參見 [示例2:和頻函式線上圖中的應用](#applicationsumfrequency)。

### Web通道中的自定義函式 {#customfunctionsweb}

除了使用圖表中的預設函式外，您還可以在JavaScript™中編寫自定義函式，並在圖表元件中用於Web通道的函式清單中提供這些函式。

函式將陣列或值和類別名稱作為輸入並返回值。 例如：

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

編寫自定義函式後，請執行以下操作使其可用於圖表配置：

1. 在與相關交互通信關聯的客戶端庫中添加自定義函式。 有關詳細資訊，請參見 [配置提交操作](/help/forms/using/configuring-submit-actions.md) 和 [使用客戶端庫](/help/sites-developing/clientlibs.md)。

1. 要在「函式」下拉菜單中顯示自定義函式，請在CRXDe Lite中建立 `nt:unstructured` 資料夾中具有以下屬性的節點：

   * 添加屬性 `guideComponentType` 值為 `fd/af/reducer`。 （強制）

   * 添加屬性 `value` 到自定義JavaScript™函式的完全限定名稱。 （必需），並將其值設定為自定義函式的名稱，如Multiply。
   * 添加屬性 `jcr:description` 以「函式」(Function)下拉清單中顯示的自定義函式的名稱顯示。 比如說， **乘**。

   * 添加屬性 `qtip` 值將簡短地描述自定義函式。 將指針懸停在函式名稱上時，它將顯示為工具提示 **函式** 的子菜單。

1. 按一下 **全部保存** 的子菜單。

該函式現在可在圖表中使用。

## 示例1:打印和Web中的圖表輸出 {#chartoutputprintweb}

在「基本」頁籤中，定義圖表類型、包含資料的源表單資料模型屬性、要在圖表的X軸和Y軸上繪製的標籤，以及（可選）用於計算圖表上繪製值的統計函式。

讓我們借助使用互動式通信生成的卡語句，詳細瞭解基本屬性中所需的最低資訊。 請考慮您要生成一個圖表來描述報表中不同費用的金額。 您希望使用不同類型的圖表來打印和Web輸出交互通信。

### 打印清單 {#columnchartprint}

為此，請指定以下屬性：

* **[!UICONTROL 名稱]**  — 指定圖表的名稱。
* **[!UICONTROL 圖表類型]**  — 選擇 **列** 從下拉清單中。
* **[!UICONTROL 標題]**  — 為X軸指定費用類型，為Y軸指定事務處理金額。
* **[!UICONTROL 資料模型對象]**  — 選擇資料模型對象屬性以為X軸（支出類型）和Y軸（事務處理金額）建立資料綁定。

![互動式通信的打印通道中的清單](assets/sample_chart_print_column_new.png)

互動式通信的打印通道中的清單

### Web的甜圈圖 {#donutchartweb}

為此，請指定以下屬性：

* **[!UICONTROL 名稱]**  — 指定圖表的名稱。
* **[!UICONTROL 圖表類型]**  — 選擇 **[!UICONTROL 甜甜圈]** 從下拉清單中。
* **[!UICONTROL 資料模型對象]**  — 選擇資料模型對象屬性以為X軸（支出類型）和Y軸（事務處理金額）建立資料綁定。
* **[!UICONTROL 內半徑]**  — 將「內半徑」值指定為150，以指定圖表中內圓的半徑（以像素為單位）。
* **[!UICONTROL 工具提示]**  — 使用${x}(${y})預設格式顯示工具提示。 工具提示顯示為：費用類型（事務處理金額）。 示例：比特幣借記(10000)。

![互動式通信網路通道中的圓形圖](assets/sample_chart_web_new.png)

互動式通信網路通道中的圓形圖

## 示例2:和頻函式線上圖中的應用 {#applicationsumfrequency}

通過在圖表中應用函式，可以繪製表格資料模型未直接提供的資料。 在此示例中，我們使用信用卡對帳單示例來瞭解如何將Sum和Frequency函式應用於圖表。

![沒有帶兩個「Debit for AirBnB」交易的函式的折線圖](assets/line_chart_web_new.png)

沒有帶兩個「Debit for AirBnB」交易的函式的折線圖

### 求和函式 {#sum-function}

您可以應用sum函式來添加同一資料屬性的多個實例的值，並只顯示一次。 例如，在下圖中，Sum函式應用在Y軸上，以便為AirBnB事務（2050和1050）合計兩個借項的金額，並且只顯示一個事務(3100)。

Sum函式可使圖表在要對同一資料屬性的多個實例進行匯總和顯示時更有用。

![折線圖和](assets/line_chart_web_sum_new.png)

### 頻率函式 {#frequency-function}

Frequency函式返回另一個軸上給定值的Y軸數。 在Y軸（事務處理金額）上應用Frequency函式時，該圖表顯示AirBnB事務已發生兩次Debit，其餘事務類型已發生一次。

![折線圖頻率](assets/line_chart_web_functions_frequency_new.png)

## 示例3:Web中的多系列像限圖 {#example-multi-series-quadrant-chart-in-web}

圖表以曲線表示在特定日期範圍內執行的事務處理的金額。 像限圖提供了將圖表區域分為四個標籤部分的能力。 該字元對X軸和Y軸使用靜態參照點。 使用多系列功能根據銀行名稱來分離資料。

為此，請指定以下屬性：

* **名稱：** 指定圖表的名稱。
* **圖表類型：** 選擇 **像限** 從下拉清單中。

* 選擇 **多系列** 複選框。
* **資料模型對象**:指定系列的資料模型對象屬性。 銀行名稱的資料模型對象屬性是在X軸和Y軸中繪製的資料模型對象屬性的父項。
* **資料模型對象：** 選擇資料模型對象屬性以為X軸（事務處理日期）和Y軸（事務處理金額）建立資料綁定。
* 在 **參考點** 選擇 **靜態** 作為綁定類型。

* 指定X軸和Y軸參照點的值。
* 指定左上、右上、右下和左下像限的像限標籤。
* 選擇 **顯示圖例** 複選框可顯示銀行名稱的顏色代碼。

![像限圖](assets/charts_quadrant_example_new.png)
