---
title: 為自適應表單生成記錄文檔
seo-title: Generate Document of Record for adaptive forms
description: 說明如何為自適應表單的記錄文檔(DoR)生成模板。
seo-description: Explains how you can generate a template for a document of record (DoR) for adaptive forms.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '3466'
ht-degree: 2%

---

# 為自適應表單生成記錄文檔{#generate-document-of-record-for-adaptive-forms}

## 概觀 {#overview}

在提交表單後，您的客戶通常希望以打印或文檔格式記錄他們在表單中填寫的資訊，以供將來參考。 這稱為記錄文檔。

本文說明了如何為自適應表單生成記錄文檔。

>[!NOTE]
>
>基於XFA的自適應表單不支援記錄文檔的自動生成。 但是，可以使用用於建立自適應表單作為記錄文檔的XDP。

## 自適應表單類型及其記錄文檔 {#adaptive-form-types-and-their-documents-of-record}

建立自適應表單時，可以選擇表單模型。 您的選項包括：

* [表單模板](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
用於為自適應表單選擇XFA模板。 選擇XFA模板時，可以使用關聯的XDP檔案來記錄文檔，如上所述。

* [XML架構](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
用於為自適應表單選擇XML架構定義。 為自適應表單選擇XML架構時，可以：

   * 將XFA模板關聯到記錄文檔。 確保關聯的XFA模板使用與自適應表單相同的XML架構
   * 自動生成記錄文檔

* 無用於建立沒有表單模型的自適應表單。 記錄文檔將自動為您的自適應表單生成。

選擇表單模型時，請使用記錄模板配置文檔下的可用選項配置記錄文檔。 請參閱 [記錄模板配置文檔](#document-of-record-template-configuration)。

## 自動生成的記錄文檔 {#automatically-generated-document-of-record}

記錄文檔允許客戶保留已提交表單的副本，以便打印。 當您自動生成記錄文檔時，每次更改表單時，其記錄文檔都會立即更新。 例如，您刪除了選擇美利堅合眾國作為其國家的客戶的年齡欄位。 當這些客戶生成記錄文檔時，他們在記錄文檔中看不到年齡欄位。

自動生成的記錄文檔具有以下優點：

* 它負責資料綁定。
* 它自動隱藏在提交時標籤為從記錄文檔中排除的欄位。 無需額外努力。
* 它為記錄模板的文檔設計節省了時間。
* 它允許您使用不同的基本模板嘗試不同的樣式和外觀，並為「記錄文檔」選擇最佳樣式和外觀。 造型外觀是可選的，如果未指定造型，則系統樣式將設定為預設樣式。
* 它確保任何形式的變化都立即反映在記錄檔案中。

## 自動生成記錄文檔的元件 {#components-to-automatically-generate-a-document-of-record}

要為自適應表單生成記錄文檔，需要以下元件：

**自適應形式** 要為其生成記錄文檔的自適應表單。

**基本模板（推薦）** 在設計器中建立的XFA模AEM板（XDP檔案）。 基本模板用於為記錄模板的文檔指定樣式和品牌資訊。

請參閱 [記錄文檔的基本模板](#base-template-of-a-document-of-record)

>[!NOTE]
>
>記錄文檔的基本模板也稱為記錄文檔的元模板。

**記錄模板的文檔** 從自適應表單生成的XFA模板（XDP檔案）。

請參閱 [記錄模板配置文檔](#document-of-record-template-configuration)。

**表單資料** 用戶以自適應形式填寫的資訊。 它與記錄模板文檔合併，生成記錄文檔。

## 自適應表單元的映射 {#mapping-of-adaptive-form-elements}

以下各節介紹了自適應表單元素在記錄文檔中的顯示方式。

### 欄位 {#fields}

<table>
 <tbody>
  <tr>
   <th>自適應表單元件</th>
   <th>對應的XFA元件</th>
   <th>預設包含在記錄模板文檔中？</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>按鈕</td>
   <td>按鈕</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>複選框</td>
   <td>核取方塊</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期選取器</td>
   <td>日期/時間欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉清單</td>
   <td>下拉式清單</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>草寫簽名</td>
   <td>簽名Scribble</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>數字框</td>
   <td>數字欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>密碼框</td>
   <td>密碼欄位</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td>選項按鈕</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文本框</td>
   <td>文字欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>重設按鈕</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>「提交」按鈕</td>
   <td><p>電子郵件提交按鈕</p> <p>HTTP提交按鈕</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>條款和條件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td> </td>
   <td>false</td>
   <td>記錄模板的文檔中不可用。 僅通過附件在記錄文檔中可用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>自適應表單元件</th>
   <th>對應的XFA元件</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子窗體<br /> </td>
   <td>可重複面板映射到可重複子窗體。</td>
  </tr>
 </tbody>
</table>

### 靜態元件 {#static-components}

| 自適應表單元件 | 對應的XFA元件 | 附註 |
|---|---|---|
| 影像 | 影像 | TextDraw和Image元件（無論綁定還是未綁定）始終出現在基於XSD的自適應表單的記錄文檔中，除非使用記錄設定文檔排除。 |
| 文字 | 文字 |

>[!NOTE]
>
>在標準UI中，您可以獲取不同的頁籤，以編輯欄位屬性。

### 表 {#tables}

自適應表單表元件，如頁眉、頁腳和行映射到相應的XFA元件。 您可以將可重複面板映射到記錄文檔中的表。

## 記錄文檔的基本模板 {#base-template-of-a-document-of-record}

基本模板為記錄文檔提供樣式和外觀資訊。 它允許您自定義自動生成的記錄文檔的預設外觀。 例如，您希望在頁眉中添加公司徽標，在記錄文檔的頁腳中添加版權資訊。 基本模板中的母版頁用作記錄模板文檔的母版頁。 母版頁可以包含可應用於記錄文檔的頁眉、頁腳和頁碼等資訊。 您可以使用基本模板將此類資訊應用於記錄文檔，以自動生成記錄文檔。 使用基本模板可更改欄位的預設屬性。

請關注 [基本模板約定](#base-template-conventions) 設計基模板。

## 基本模板約定 {#base-template-conventions}

基本模板用於定義記錄文檔的頁眉、頁腳、樣式和外觀。 頁眉和頁腳可以包括公司徽標和版權文本等資訊。 基本模板中的第一個母版頁被複製並用作記錄文檔的母版頁，該母版頁包含頁眉、頁腳、頁碼或記錄文檔中所有頁面上應出現的任何其他資訊。 如果使用的基本模板不符合基本模板約定，則基本模板的第一個母版頁仍用於記錄模板的文檔。 強烈建議您根據基本模板的約定設計基本模板，並將其用於記錄文檔的自動生成。

**母版頁約定**

* 在基本模板中，應將根子窗體命名為 `AF_METATEMPLATE` 母版頁 `AF_MASTERPAGE`。

* 具有名稱的母版頁 `AF_MASTERPAGE` 位於 `AF_METATEMPLATE` 根子表單優先於提取頁眉、頁腳和樣式資訊。

* 如果 `AF_MASTERPAGE` 缺少，則使用基模板中存在的第一母版頁。

**域的樣式約定**

* 要對記錄文檔中的欄位應用樣式，基本模板將提供位於 `AF_FIELDSSUBFORM` 從 `AF_METATEMPLATE` 根子窗體。

* 這些欄位的屬性將應用於記錄文檔中的欄位。 這些欄位應跟在 `AF_<name of field in all caps>_XFO` 命名約定。 例如，複選框的欄位名應為 `AF_CHECKBOX_XFO`。

要建立基本模板，請在設計器中執AEM行以下操作。

1. 按一下 **檔案>新建**。
1. 選擇 **基於模板** 的雙曲餘切值。

1. 選擇 **Forms — 記錄文檔** 的子菜單。
1. 選擇 **DoR基本模板**。
1. 按一下 **下一個** 提供所需資訊。

1. （可選）修改要應用於記錄文檔中欄位的欄位的樣式和外觀。
1. 保存窗體。

現在，您可以將保存的表單用作記錄文檔的基本模板。
不要修改或刪除基本模板中存在的任何指令碼。

**修改基本模板**

* 如果不對基本模板中的欄位應用任何樣式，建議從基本模板中刪除這些欄位，以便自動提取對基本模板的任何升級。
* 修改基本模板時，不要刪除、添加或修改指令碼。

>[!NOTE]
>
>使用約定設計基本模板並嚴格遵循上述步驟。

## 記錄範本文件配置 {#document-of-record-template-configuration}

配置表單的記錄模板文檔，讓客戶下載已提交表單的打印友好副本。 XDP檔案用作記錄模板的文檔。 記錄客戶下載的文檔根據XDP檔案中指定的佈局格式化。

執行以下步驟來為自適應表單配置記錄文檔：

1. 在作AEM者實例中，按一下 **Forms>Forms和文檔。**
1. 選擇表單，然後按一下 **查看屬性**。
1. 在「屬性」窗口中，按一下 **窗體模型**。
建立表單時，也可選取表單模型。

   >[!NOTE]
   >
   >在「表單模型」(Form Model)頁籤中，確保 **架構** 或 **無** 從 **從中選擇** 下拉。 **[!UICONTROL 基於XFA或以表單模板作為表單模型的自適應表單不支援記錄文檔。]**

1. 在「表單模型」頁籤的「記錄模板配置文檔」部分，選擇以下選項之一。

   **無** 如果不想為表單配置記錄文檔，請選擇此選項。

   **將表單模板與記錄模板文檔關聯** 如果有要用作記錄文檔模板的XDP檔案，請選擇此選項。 選擇此選項時，將顯示AEM Forms儲存庫中可用的所有XDP檔案。 選擇相應的檔案。

   選定的XDP檔案將與自適應表單相關聯。

   **生成記錄文檔** 選擇此選項可將XDP檔案用作定義記錄文檔的樣式和外觀的基本模板。 選擇此選項時，將顯示AEM Forms儲存庫中可用的所有XDP檔案。 選擇相應的檔案。

   >[!NOTE]
   >
   >在以下情況下，確保用於建立XFA表單的自適應表單和模式（資料模式）的架構相同：
   >
   >
   >
   >    * 自適應表單基於模式
   >    * 您正在使用 **將表單模板與記錄模板文檔關聯** 文檔的選項


1. 按一下 **搞定。**

## 定制記錄文檔中的品牌資訊 {#customize-the-branding-information-in-document-of-record}

在生成記錄文檔時，您可以在「記錄文檔」頁籤上更改記錄文檔的品牌資訊。 「記錄文檔」頁籤包括徽標、外觀、佈局、頁眉和頁腳、免責聲明，以及是否要包括未選定的複選框和單選按鈕選項等選項。

要本地化您在「記錄文檔」頁籤中輸入的品牌資訊，您需要確保正確設定瀏覽器的區域設定。 要自定義記錄文檔的品牌資訊，請完成以下步驟：

1. 在記錄文檔中選擇一個面板（根面板），然後點擊 ![配置](assets/configure.png)。
1. 點擊 ![多拉](/help/forms/using/assets/dortab.png)。 此時將顯示「記錄文檔」頁籤。
1. 選擇用於呈現記錄文檔的預設模板或自定義模板。 如果選擇預設模板，則記錄文檔的縮覽圖預覽會顯示在「模板」(Template)下拉菜單下方。

   ![品牌模板](/help/forms/using/assets/brandingtemplate.png)

   如果選擇選擇自定義模板，請瀏覽在AEM Forms伺服器上選擇XDP。 如果要使用尚未在AEM Forms伺服器上的模板，則需要先將XDP上載到AEM Forms伺服器。

1. 根據您是選擇預設模板還是自定義模板，「記錄文檔」頁籤中將顯示以下部分或全部屬性。 相應地指定以下項：

   * **徽標影像**:您可以選擇使用自適應表單中的徽標影像，從DAM中選擇一個，或從電腦上載一個。
   * **表單標題**
   * **頁首文字**
   * **免責聲明標籤**
   * **免責聲明**
   * **免責聲明文字**
   * **強調色**:在文檔或記錄PDF中呈現標題文本和分隔線的顏色
   * **字型系列**:記錄文檔中文本的字型系列PDF
   * **對於複選框和單選按鈕元件，只顯示所選值**
   * **所選多個值的分隔符號**
   * **包括未綁定到資料模型的表單對象**
   * **從記錄文檔中排除隱藏欄位**
   * **隱藏面板描述**

   如果您選擇的自定義XDP模板包含多個母版頁，則這些頁的屬性將顯示在 **[!UICONTROL 內容]** 的下界 **[!UICONTROL 記錄文檔]** 頁籤。

   ![主版頁面屬性](assets/master-page-properties.png)

   母版頁屬性包括徽標影像、標題文本、表單標題、免責聲明標籤和免責聲明文本。 您可以將自適應表單或XDP模板屬性應用於記錄文檔。 AEM Forms預設將模板屬性應用於記錄文檔。 您還可以為母版頁屬性定義自定義值。 有關如何在記錄文檔中應用多個母版頁的資訊，請參閱 [將多個母版頁應用於記錄文檔](#apply-multiple-master-pages-dor)。

   >[!NOTE]
   >
   >如果使用在6.3之前使用Designer版本建立的自適應表單模板，以便使用「強調顏色」和「字型系列」屬性，請確保在根子表單下的自適應表單模板中存在以下內容：

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. 要保存品牌更改，請點擊「完成」。

## 記錄文檔中面板的表和列佈局 {#table-and-column-layouts-for-panels-in-document-of-record}

自適應表單可能是一個包含多個表單域的長表單。 您可能不想將記錄文檔另存為自適應表單的精確副本。 現在，您可以選擇表或列佈局，以在記錄PDF的文檔中保存一個或多個自適應表單面板。

在生成記錄文檔之前，在面板的設定中，選擇該面板的「記錄文檔的佈局」作為「表」或「列」。 在記錄文檔中相應地組織面板中的欄位。

![在記錄文檔的表佈局中呈現的面板中的欄位](assets/dortablelayout.png)

在記錄文檔的表佈局中呈現的面板中的欄位

![在記錄文檔的列佈局中呈現的面板中的欄位](assets/dorcolumnlayout.png)

在記錄文檔的列佈局中呈現的面板中的欄位

## 記錄設定的文檔 {#document-of-record-settings}

記錄文檔設定允許您選擇要包括在記錄文檔中的選項。 例如，銀行接受表單中的姓名、年齡、社會保險號碼和電話號碼。 表單生成銀行帳號和分行詳細資訊。 您可以選擇只在記錄文檔中顯示姓名、社會保險編號、銀行帳戶和分支詳細資訊。

元件的記錄設定文檔在其屬性下可用。 要訪問元件的屬性，請選擇該元件並按一下 ![招商](assets/cmppr.png) 的上界。 這些屬性列在提要欄中，您可以在其中找到以下設定。

**欄位級別設定**

* **從記錄文檔中排除**:將屬性設定為true會從記錄文檔中排除欄位。 這是名為的可指令碼的屬性 `excludeFromDoR`。 它的行為取決於 **如果隱藏，則從DoR中排除欄位** 窗體級別屬性。

* **以表格形式顯示面板：** 如果面板中的欄位少於6個，則將屬性設定為顯示面板作為記錄文檔中的表。 僅適用於面板。
* **從記錄文檔中排除標題：** 設定屬性會從記錄文檔中排除面板/表的標題。 僅適用於面板和表。
* **從記錄文檔中排除說明：** 設定屬性不包括記錄文檔中對面板/表的說明。 僅適用於面板和表。
* **[!UICONTROL 分頁]** > **[!UICONTROL 位置]**:確定選擇放置面板的位置。
   * **[!UICONTROL 位置]** > **[!UICONTROL 跟隨上一個]**:將面板置於父面板中上一個對象之後。
   * **[!UICONTROL 位置]** > **[!UICONTROL 在內容區域]** >內容區域的名稱：將面板置於指定的內容區域。
   * **[!UICONTROL 位置]** > **[!UICONTROL 下一個內容區域的頂部]**:將面板置於下一個內容區域的頂部。
   * **[!UICONTROL 位置]** > **[!UICONTROL 內容區域頂部]** >內容區域的名稱：將面板置於指定內容區域的頂部。
   * **[!UICONTROL 位置]** > **[!UICONTROL 頁上]** >母版頁名稱：將面板置於指定頁面上。 如果分頁符未自動插入， [!DNL AEM Forms] 添加分頁符。
   * **[!UICONTROL 位置]** > **[!UICONTROL 下一頁頂部]**:將面板置於下一頁的頂部。 如果分頁符未自動插入， [!DNL AEM Forms] 添加分頁符。
   * **[!UICONTROL 位置]** > **[!UICONTROL 頁首]** >母版頁名稱：當呈現指定頁面時，將面板置於頁面頂部。 如果分頁符未自動插入， [!DNL AEM Forms] 添加分頁符。
* **[!UICONTROL 分頁]** > **[!UICONTROL 之後]**:確定放置面板後要填充的區域。 **[!UICONTROL 之後]** 部分：
   * **[!UICONTROL 之後]** > **[!UICONTROL 繼續填充父項]**:繼續合併父面板中剩餘要填充的所有對象的資料。
   * **[!UICONTROL 之後]** > **[!UICONTROL 轉到下一個內容區域]**:放置面板後開始填充下一個內容區域。
   * **[!UICONTROL 之後]** > **[!UICONTROL 轉到內容區域]** >內容區域的名稱：放置面板後開始填充指定的內容區域。
   * **[!UICONTROL 之後]** > **[!UICONTROL 轉到下一頁]**:放置面板後開始填充下一頁。
   * **[!UICONTROL 之後]** > **[!UICONTROL 轉到頁面]** >頁名：放置面板後開始填充指定的頁面。
* **[!UICONTROL 分頁]** > **[!UICONTROL 溢出]**:為跨頁的面板或表設定溢出。 以下欄位可在 **[!UICONTROL 溢出]** 部分：
   * **[!UICONTROL 溢出]** > **[!UICONTROL 無]**:開始填充下一頁。 如果分頁符未自動插入， [!DNL AEM Forms] 添加分頁符。
   * **[!UICONTROL 溢出]** > **[!UICONTROL 轉到內容區域]** >內容區域的名稱：開始填充指定的內容區域。
   * **[!UICONTROL 溢出]** > **[!UICONTROL 轉到頁面]** >頁名：開始填充指定的頁。

有關如何應用分頁符和應用「記錄文檔」中多個母版頁的資訊，請參閱 [在記錄文檔中應用分頁符](#apply-page-breaks-in-dor) 和 [將多個母版頁應用於記錄文檔](#apply-multiple-master-pages-dor)。

**表單級別設定**

* **在DoR中包括未綁定欄位：** 設定屬性包括記錄文檔中基於模式的自適應表單中的未綁定欄位。 預設情況下為true。
* **如果隱藏，則從DoR中排除欄位：** 設定屬性以從中排除隱藏欄位 [!UICONTROL 記錄文檔] 表格提交。 啟用時 [在伺服器上重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)，伺服器在將這些欄位從 [!UICONTROL 記錄文檔]。

## 在記錄文檔中應用分頁符 {#apply-page-breaks-in-dor}

可以使用多種方法在「記錄文檔」中應用分頁符。

要將分頁符應用於記錄文檔，請執行以下操作：

1. 按一下面板並選擇 ![配置](/help/forms/using/assets/configure.png)
1. 展開 **[!UICONTROL 記錄文檔]** 的子菜單。

1. 在 **[!UICONTROL 分頁]** 部分，點擊 ![資料夾](/help/forms/using/assets/folder-icon.png) 的 **[!UICONTROL 位置]** 的子菜單。
1. 點擊 **[!UICONTROL 下一頁頂部]** 點擊 **[!UICONTROL 選擇]**。 也可以點擊 **[!UICONTROL 頁首]**，選擇母版頁，然後點擊 **[!UICONTROL 選擇]** 按鈕。
1. 點擊 ![保存](/help/forms/using/assets/save_icon.png) 的子菜單。

選定的面板將移到下一頁。

## 將多個母版頁應用於記錄文檔 {#apply-multiple-master-pages-dor}

如果您選擇的自定義XDP模板包含多個母版頁，則這些頁的屬性將顯示在 [!UICONTROL 內容] 的下界 [!UICONTROL 記錄文檔] 頁籤。 有關詳細資訊，請參見 [定制記錄文檔中的品牌資訊](#customize-the-branding-information-in-document-of-record)。

通過將不同的母版頁應用於自適應表單的元件，可以將多個母版頁應用於「記錄文檔」。 使用 [分頁](#document-of-record-settings) 的子頁面。

以下是如何將多個母版頁應用於記錄文檔的示例：將包含四個母版頁的XDP模板上載到 [!DNL AEM Forms] 伺服器。 [!DNL AEM Forms] 預設情況下，將模板屬性應用於記錄文檔。 [!DNL AEM Forms] 還將模板中的第一個母版頁屬性應用於「記錄文檔」。

要將第二個母版頁屬性應用到面板，將第三個母版頁屬性應用到後面的面板，請執行以下步驟：

1. 按一下面板以應用第二個母版頁並選擇 ![配置](assets/cmppr.png)。
1. 在 **[!UICONTROL 分頁]** 部分，點擊 ![資料夾](/help/forms/using/assets/folder-icon.png) 的 **[!UICONTROL 位置]** 的子菜單。
1. 點擊 **[!UICONTROL 第頁]**，選擇第二個母版頁並點擊 **[!UICONTROL 選擇]**。
AEM Forms將第二母版頁應用於面板和所有後續面板，格式為自適應。
1. 在 **[!UICONTROL 分頁]** 部分，點擊 ![資料夾](/help/forms/using/assets/folder-icon.png) 的 **[!UICONTROL 之後]** 的子菜單。
1. 點擊 **[!UICONTROL 轉到頁面]**，選擇第三個母版頁並點擊 **[!UICONTROL 選擇]**。
1. 點擊 ![保存](/help/forms/using/assets/save_icon.png) 的子菜單。
AEM Forms將第三母版頁應用於面板和所有後續面板，格式為自適應。


## 處理記錄文檔時的主要考慮事項 {#key-considerations-when-working-with-document-of-record}

在處理自適應表單的記錄文檔時，請記住以下考慮事項和限制。

* 記錄模板的文檔不支援RTF。 因此，靜態自適應表單或最終用戶填寫的資訊中的任何富文本都顯示為記錄文檔中的純文字檔案。
* 自適應格式的文檔片段不會出現在記錄的文檔中。 但是，支援自適應形式片段。
* 不支援為基於XML Schema的自適應表單生成的記錄文檔中的內容綁定。
* 當用戶請求呈現記錄文檔時，根據區域設定的要求建立記錄文檔的本地化版本。 記錄文檔的定位與自適應格式的定位同步進行。 有關記錄文檔和自適應表單本地化的更多資訊，請參見 [使用AEM翻譯工作流本地化記錄的自適應表單和文檔](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。
