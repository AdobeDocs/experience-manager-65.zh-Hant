---
title: 在互動式通信中使用圖表
seo-title: Chart component in Interactive Communications
description: 在互動式通信中使用圖表，可以將大量資訊濃縮成易於分析的視覺格式
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

# 在互動式通信中使用圖表{#using-charts-in-interactive-communications}

圖表或圖表是資料的視覺表示。 它將大量資訊濃縮成易於理解的視覺格式，使互動式通信的接收方能夠更好地對複雜的資料進行可視化、解譯和分析。

建立互動式通訊時，您可以新增圖表，以從互動式通訊的表單資料模型以視覺化方式呈現二維資料。 圖表元件允許您添加和配置以下類型的圖表：圓形圖、列、環形圖、條形圖、線條圖、線條圖和點圖、點圖、區域圖和像限圖。

## 在互動式通訊中新增及設定圖表 {#add-and-configure-chart-in-an-interactive-communication}

執行下列步驟以在互動式通訊中新增和設定圖表：

1. 點選 **元件** 從互動式通訊的旁邊。
1. 拖放 **圖表** 元件至下列其中一個元件：

   * 打印通道：目標區域或影像欄位
   * Web頻道：面板或目標區域

1. 在「互動式通訊」編輯器中點選圖表元件，然後選取 **[!UICONTROL 配置(]** ![configure_icon](assets/configure_icon.png))。

   圖表屬性顯示在左窗格中。

   ![打印通道中線型圖的基本屬性](assets/chart_properties_print_new.png)

   打印通道中線型圖的基本屬性

   ![Web通道中線型圖的基本屬性](assets/chart_properties_web_new.png)

   Web通道中線型圖的基本屬性

1. 設定 [圖表屬性](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) 根據通道類型。
1. （僅限列印管道） **[!UICONTROL 代理設定]**，指定代理是否必須使用此圖表。 如果 **[!UICONTROL t是代理使用此圖表的必填項目]** 選項，則代理可以點選 **[!UICONTROL 內容]** 頁簽顯示或隱藏圖表。

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. 點選 ![done_icon](assets/done_icon.png) 以保存圖表屬性。

   點選 **[!UICONTROL 預覽]** 查看與圖表關聯的外觀和資料。 點選 **[!UICONTROL 編輯]** 重新配置圖表的屬性。

## 配置圖表屬性 {#configure-chart-properties}

在為打印通道和Web通道建立圖表時配置以下屬性：

<table>
 <tbody>
  <tr>
   <td>欄位</td>
   <td>說明</td>
   <td>頻道類型</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>圖表元素的識別碼。 此欄位中指定的圖表名稱在圖表上不顯示。 當參考其他元件、指令碼和SOM運算式中的元素時，會使用它。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>圖表類型</td>
   <td>要生成的圖表類型。 可用選項有餅圖、列、環圈圖、條、線、線和點、點和區域。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>系列&gt;多系列</td>
   <td>選取，為在X軸和Y軸上繪製的表單資料模型收集項目新增多個系列。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>系列&gt;資料模型物件</td>
   <td>要向圖表添加多個系列的表單資料模型集合項的名稱。<br /> 為在X軸和Y軸上繪製的屬性選擇父表單資料模型對象屬性，以形成有意義的系列。 綁定的資料模型對象必須為Number、String或Date類型。</td>
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
   <td>X軸&gt;資料模型物件</td>
   <td><p>要在X軸上繪製的表單資料模型收集項目的名稱。</p> <p>選擇相同父資料模型對象的兩個集合/陣列類型屬性，這些屬性彼此相對有意義，以在圖表的X和Y軸上繪製。 綁定的資料模型對象必須為Number、String或Date類型。</p> </td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>Y軸&gt;標題</td>
   <td>Y軸的標題。 </td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>Y軸&gt;資料模型物件</td>
   <td><p>要在Y軸上繪製的表單資料模型收集項。 在「打印」通道中，Y軸的資料模型對象應為「編號」類型。</p> <p>選擇相同父資料模型對象的兩個集合/陣列類型屬性，這些屬性彼此相對有意義，以在圖表的X和Y軸上繪製。 </p> </td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>Y軸&gt;函式</td>
   <td>用於計算Y軸上值的統計/自訂函式。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>隱藏物件</td>
   <td>選擇以隱藏最終輸出中的圖表。</td>
   <td>打印和Web</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>圖表的標題。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>圖表的高度（像素）。</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>寬度</td>
   <td>圖表的寬度（像素）。 您可以使用樣式層或套用主題，控制Web通道中圖表的寬度。</td>
   <td>列印</td>
  </tr>
  <tr>
   <td>必要分頁符號之前</td>
   <td>選取「 」，在圖表前新增強制分頁符，並將圖表放在新頁面的頂端。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>之後強制分頁</td>
   <td>選取「 」，在圖表後新增強制分頁符，並將圖表後的內容放在新頁面頂端。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>縮排</td>
   <td>從頁面左側縮排圖表。 </td>
   <td>列印</td>
  </tr>
  <tr>
   <td>工具提示</td>
   <td><p>工具提示出現在Web頻道圖表中資料點滑鼠上的格式。 預設值為${x}(${y})。 根據圖表類型，當您將滑鼠指向圖表中的點、條或切片時，變數${x}和${y}將動態替換為X軸和Y軸上的相應值，並顯示在工具提示中。</p> <p>若要停用工具提示，請保留 <span class="uicontrol">工具提示</code> 欄位空白。 此選項不適用於折線圖和區域圖。 例如，請參閱 <a href="#chartoutputprintweb">範例1:打印和Web中的圖表輸出</a>.</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>圖表專屬設定</td>
   <td><p>除了常見設定外，還提供下列圖表專屬設定：</p>
    <ul>
     <li><strong>顯示圖例： </strong>顯示圓形圖或環圈圖的圖例。</li>
     <li><strong>圖例位置： </strong>指定圖例相對於圖表的位置。 可用選項有「右」、「左」、「上」和「下」。 建議在列印管道中使用右側圖例。</li>
     <li><strong>內半徑</strong>:供環圈圖指定圖表中內圓的半徑（以像素為單位）。</li>
     <li><strong>線條顏色</strong>:折線圖、折線圖、折線圖、點圖和面積圖可指定圖表中折線的顏色。</li>
     <li><strong>點顏色</strong>:可用於點圖、折線圖和點圖，以指定圖表中點的顏色。<br /> </li>
     <li><strong>區域顏色</strong>:區域圖可用於指定圖表中折線下方區域的顏色。</li>
     <li><strong>參考點&gt;綁定類型： </strong>可用於像限圖<strong> </strong>指定引用點的綁定類型。 使用靜態文本或資料模型對象屬性來定義參考點的值。</li>
     <li><strong>參照點&gt; X軸： </strong>如果選擇，則可用於像限圖 <span class="uicontrol">靜態</code> 從「綁定類型」(Binding Type)下拉清單中，指定參照點的X軸值。</code></li>
     <li><strong>參照點&gt; Y軸： </strong>如果選擇，則可用於像限圖 <span class="uicontrol">靜態</code> 從「綁定類型」(Binding Type)下拉清單中，指定參照點的Y軸值。</code></li>
     <li><strong>系列的參考點&gt;資料模型對象： </strong>如果選擇，則可用於多個系列像限圖 <span class="uicontrol">資料模型物件</code> 從「綁定類型」下拉清單中。 定義表單資料模型物件屬性以確認參考點的系列. </code></li>
     <li><strong>系列的參考點&gt;資料模型對象值： </strong>如果選擇，則可用於多個系列像限圖 <span class="uicontrol">資料模型物件</code> 從「綁定類型」下拉清單中。 使用系列的表單資料模型對象屬性和此欄位中定義的值，以標識參考點的系列。</code></li>
     <li><strong>參照點&gt;參照點的資料模型對象： </strong>如果選擇，則可用於像限圖 <span class="uicontrol">資料模型物件</code> 從「綁定類型」下拉清單中。 定義表單資料模型對象屬性，該屬性與在X軸和Y軸上繪製的屬性同級。 此外，對於多個系列，定義一個資料模型對象屬性，該屬性是為該系列定義的資料模型對象屬性的子實體。</code></li>
     <li><strong>參考點&gt;資料模型對象值參考點： </strong>如果選擇，則可用於像限圖 <span class="uicontrol">資料模型物件</code> 從「綁定類型」下拉清單中。 對參考點使用表單資料模型對象屬性以及此欄位中定義的值，以標識圖表的參考點。<br /> <strong>像限標籤&gt;左上：</strong> 可用於像限圖以指定左上像限的名稱。</code></li>
     <li><strong>像限標籤&gt;右上：</strong> 可用於像限圖表以指定右上像限的名稱。</li>
     <li><strong>像限標籤&gt;右下： </strong>可用於像限圖以指定右下像限的名稱。</li>
     <li><strong>像限標籤&gt;左下： </strong>可用於像限圖以指定左下像限的名稱。</li>
    </ul> </td>
   <td>打印和Web</td>
  </tr>
 </tbody>
</table>

## 在圖表中使用函式 {#use-functions-in-chart}

您可以設定圖表，使用統計函式從來源資料計算值，以便在圖表上繪製。 在圖表中套用函式，即可繪製非表單資料模型直接提供的資料。

![圖表中的函式](assets/functions_charts_new.png)

雖然圖表元件附帶一些內建功能，但您可以編寫 [自訂函式](#customfunctionsweb) 並讓它們可用於網頁頻道的圖表設定中。

圖表元件預設提供下列函式：

**平均值** 傳回X或Y軸上其他軸上指定值的平均值。

**總和** 傳回X或Y軸上其他軸上指定值的所有值總和。

**最大值** 傳回X或Y軸上另一個軸上給定值的最大值。

**頻率** 傳回X軸或Y軸上其他軸上指定值的值數。

**範圍** 傳回X或Y軸上另一個軸上指定值之值的最大值與最小值之差。

**中位數** 傳回在X或Y軸上，將較高和較低值分隔為一半的值，以分隔另一個軸上的指定值。

**最低** 傳回X或Y軸上另一個軸上給定值的最小值。

**模式** 傳回值，在X或Y軸上，最常出現另一個軸上指定值的值。

如需詳細資訊，請參閱 [範例2:和頻函式線上圖中的應用](#applicationsumfrequency).

### Web通道中的自訂函式 {#customfunctionsweb}

除了在圖表中使用預設函式外，您還可以在JavaScript™中編寫自定義函式，並在Web通道的圖表元件的函式清單中使用這些函式。

函式以陣列或值和類別名稱作為輸入，並返回值。 例如：

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

撰寫自訂函式後，請執行下列操作，使其可用於圖表配置：

1. 在與相關互動式通訊相關聯的用戶端程式庫中新增自訂函式。 如需詳細資訊，請參閱 [設定提交動作](/help/forms/using/configuring-submit-actions.md) 和 [使用用戶端程式庫](/help/sites-developing/clientlibs.md).

1. 若要在「函式」下拉式清單中顯示自訂函式，請在CRXDe Lite中建立 `nt:unstructured` 節點（位於應用資料夾中），具有以下屬性：

   * 新增屬性 `guideComponentType` 值為 `fd/af/reducer`. （強制）

   * 新增屬性 `value` 填入自訂JavaScript™函式的完全限定名稱。 （必要），並將其值設為自訂函式的名稱，例如「乘」。
   * 新增屬性 `jcr:description` 以「函式」下拉式清單中顯示的自訂函式名稱。 例如， **乘**.

   * 新增屬性 `qtip` 值，此值將簡短說明自訂函式。 將指標暫留在 **函式** 下拉式清單。

1. 按一下 **全部儲存** 以儲存設定。

函式現在可在圖表中使用。

## 範例1:打印和Web中的圖表輸出 {#chartoutputprintweb}

在「基本」頁簽中，可以定義圖表類型、包含資料的源表單資料模型屬性、要在圖表的X軸和Y軸上繪製的標籤，以及可選的統計函式，以計算要在圖表上繪製的值。

讓我們透過使用互動式通訊產生的卡片陳述式，詳細了解基本屬性中所需的最低資訊。 請考慮您要生成一個圖表來描述報表中不同費用的金額。 要使用不同類型的圖表來打印和Interactive Communication的Web輸出。

### 打印的清單 {#columnchartprint}

要完成此操作，請指定以下屬性：

* **[!UICONTROL 名稱]**  — 指定圖表的名稱。
* **[!UICONTROL 圖表類型]**  — 選擇 **欄** 從下拉式清單中。
* **[!UICONTROL 標題]**  — 指定X軸的費用類型和Y軸的事務處理金額。
* **[!UICONTROL 資料模型物件]**  — 選擇資料模型對象屬性，以建立X軸（費用類型）和Y軸（事務處理金額）的資料綁定。

![互動式通信的打印通道中的清單](assets/sample_chart_print_column_new.png)

互動式通信的打印通道中的清單

### Web環圈圖 {#donutchartweb}

要完成此操作，請指定以下屬性：

* **[!UICONTROL 名稱]**  — 指定圖表的名稱。
* **[!UICONTROL 圖表類型]**  — 選擇 **[!UICONTROL 環形圖]** 從下拉式清單中。
* **[!UICONTROL 資料模型物件]**  — 選擇資料模型對象屬性，以建立X軸（費用類型）和Y軸（事務處理金額）的資料綁定。
* **[!UICONTROL 內半徑]**  — 將「內半徑」值指定為150，以指定圖表中內圓的半徑（以像素為單位）。
* **[!UICONTROL 工具提示]**  — 使用${x}(${y})預設格式顯示工具提示。 工具提示顯示為：費用類型（事務處理金額）。 範例：比特幣借記(10000)。

![互動式通訊網路通道中的環圈圖](assets/sample_chart_web_new.png)

互動式通訊網路通道中的環圈圖

## 範例2:和頻函式線上圖中的應用 {#applicationsumfrequency}

在圖表中套用函式，即可繪製非表單資料模型直接提供的資料。 在此示例中，我們使用信用卡對帳單示例來了解如何將總和和頻率函式應用於圖表。

![線性圖，不含兩筆「AirBnB借記」交易](assets/line_chart_web_new.png)

線性圖，不含兩筆「AirBnB借記」交易

### 求和函式 {#sum-function}

您可以套用求和函式來加總相同資料屬性的多個例項的值，且只顯示一次。 例如，在下圖中，Sum函式應用於Y軸，以加總AirBnB交易（2050和1050）的兩個借記金額，並僅顯示一個交易(3100)。

當您想要對相同資料屬性的許多例項進行整理和顯示總和時，總和函式可讓圖表更實用。

![折線圖總和](assets/line_chart_web_sum_new.png)

### 頻率函式 {#frequency-function}

頻率函式返回另一個軸上給定值的Y軸數。 在Y軸（事務量）上應用頻率函式後，圖形顯示AirBnB事務有兩次借記，其餘事務有一次借記。

![折線圖頻率](assets/line_chart_web_functions_frequency_new.png)

## 範例3:Web中的多系列像限圖 {#example-multi-series-quadrant-chart-in-web}

圖表繪製在特定日期範圍內執行的事務處理的金額。 像限圖表可將圖表區域劃分為四個標籤部分。 該字元對X軸和Y軸使用靜態參照點。 使用多系列功能，根據銀行名稱來隔離資料。

要完成此操作，請指定以下屬性：

* **名稱：** 指定圖表的名稱。
* **圖表類型：** 選擇 **像限** 從下拉式清單中。

* 選取 **多系列** 核取方塊。
* **資料模型物件**:指定系列的資料模型對象屬性。 銀行名稱的資料模型對象屬性是在X軸和Y軸中繪製的資料模型對象屬性的父屬性。
* **資料模型對象：** 選擇資料模型對象屬性以建立X軸（事務日期）和Y軸（事務金額）的資料綁定。
* 在 **參考點** 部分，選擇 **靜態** 作為綁定類型。

* 指定X軸和Y軸參照點的值。
* 指定左上、右上、右下和左下四像限的像限標籤。
* 選取 **顯示圖例** 核取方塊以顯示銀行名稱的顏色代碼。

![像限圖](assets/charts_quadrant_example_new.png)
