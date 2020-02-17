---
title: 建立互動式通訊
seo-title: 建立互動式通訊
description: 使用「互動式通訊」編輯器建立互動式通訊。 使用拖放功能建立互動式通訊，並在不同裝置類型上預覽列印和網頁輸出。
seo-description: 使用「互動式通訊」編輯器建立互動式通訊。 使用拖放功能建立互動式通訊，並在不同裝置類型上預覽列印和網頁輸出。
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# 建立互動式通訊{#create-an-interactive-communication}

## 概覽 {#overview}

互動式通訊可集中管理建立、組裝和傳遞個人化和互動式通訊。 運用列印為網頁的主要通道，在建立互動式通訊的網頁輸出時，您可將工作重複的工作降至最低。

### 必備條件 {#prerequisites}

以下是建立互動式通訊的先決條件：

* 設定包含測 [試資料或實際資料來源的表單資料模型](/help/forms/using/data-integration.md) ，例如Microsoft® Dynamics的例項。
* 請確定您有「檔案」 [片段](/help/forms/using/document-fragments.md)。
* 確保您有印刷 [和網頁通道的範本](/help/forms/using/web-channel-print-channel.md)。
* 請確定您有必要 [的](/help/forms/using/themes.md) Web頻道主題。

## 建立互動式通訊 {#createic}

1. 登入AEM作者例項並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**。
1. 點選「 **[!UICONTROL 建立]** 」並選 **[!UICONTROL 取「互動式通訊」]**。 「建立互動式通信」頁面。

   ![建立互動式通訊](assets/create-interactive-communication.png)

1. 輸入以下資訊。 :

   * **[!UICONTROL 標題]**:輸入「互動式通訊」的標題。
   * **[!UICONTROL 名稱]**:「互動式通訊」的名稱是從您輸入的標題衍生而來。 視需要編輯。
   * **[!UICONTROL 說明]**:輸入有關互動式通信的說明。
   * **[!UICONTROL 表單資料模型]**:瀏覽並選取表單資料模型。 如需表單資料模型的詳細資訊，請參閱「 [AEM Forms資料整合」](/help/forms/using/data-integration.md)。

   * **[!UICONTROL 預填服務]**:選擇預填充服務以檢索資料並預填充互動式通信。
   * **[!UICONTROL 後處理類型]**:您可以選取在提交「互動式通訊」時觸發的AEM或Forms工作流程。 選擇要觸發的工作流類型。

   * **[!UICONTROL 後處理]**:選擇要觸發的工作流的名稱。 當您選取AEM工作流程時，請提供「附件路徑」、「版面路徑」、「PDF路徑」、「列印資料路徑」和「Web資料路徑」。
   * **[!UICONTROL 標籤]**:選擇要套用至互動式通訊的標籤。 您也可以輸入新的／自訂標籤名稱，然後按Enter鍵建立它。
   * **[!UICONTROL 作者]**：作者名稱會自動取自已登入使用者的使用者名稱。
   * **** 發佈日期：輸入發佈互動式通訊的日期。
   * **[!UICONTROL 取消發佈日期]**:輸入取消發佈互動式通訊的日期。

1. 點選「 **[!UICONTROL 下一步]**」。 此時會出現指定列印和網頁頻道詳細資訊的畫面。
1. 輸入以下內容：

   * **[!UICONTROL 列印]**:選擇此選項可生成互動式通信的打印通道。
   * **[!UICONTROL 列印範本]**:瀏覽並選擇XDP作為打印模板。
   * **[!UICONTROL Web]**:選取此選項，可產生Web頻道或互動式通訊的回應式輸出。
   * **[!UICONTROL 互動式通訊Web範本]**:瀏覽並選取網頁範本。
   * **[!UICONTROL 主題]** 和 **[!UICONTROL 選擇主題]**:瀏覽並選取主題，以設定互動式通訊網路頻道的樣式。 如需詳細資訊，請參 [閱「AEM Forms中的主題」](/help/forms/using/themes.md)。

   * **[!UICONTROL 使用列印為Web頻道的主版]**:選取此選項，可建立與列印頻道同步的網頁頻道。 使用列印頻道作為網頁頻道的主節點，可確保網頁頻道的內容與資料系結是從列印頻道衍生而來，當您點選「同步化」時，列印頻道中所做的變更會反映在網頁頻道中。 但是，作者可以視需要中斷Web頻道中特定元件的繼承。 如需詳細資訊，請參 [閱同步Web頻道與列印頻道](../../forms/using/create-interactive-communication.md#synchronize)。
如果您選取「 **[!UICONTROL 使用列印為網頁頻道的主版」選項]** ，您可以選取下列任一種模式來產生網頁頻道：

      * **[!UICONTROL 自動版面]**:選取此模式可自動從列印頻道產生網頁頻道的預留位置、內容和資料系結。
      * **[!UICONCONTROL手動組織**:選取此模式，即可使用「資料來源」標籤中的主版內容，手動選取列印渠道元素並將其新 **[!UICONTROL 增至Web]** 頻道。 如需詳細資訊，請參 [閱選取列印頻道元素以建立網頁頻道內容](#selectprintchannelelements)。
   如需有關列印頻道和網路頻道的詳細資訊，請參 [閱列印頻道和網路頻道](/help/forms/using/web-channel-print-channel.md)。

1. 點選「 **[!UICONTROL 建立]**」。 將建立「交互通信」並顯示一個警報框。 點選「 **[!UICONTROL 編輯]** 」開始建立互動式通訊的內容，如「使用互動式通訊製作使用者介 [面新增內容」中所述](#step2)。 或者，您也可以點選「 **[!UICONTROL 完成]** 」，並選擇稍後編輯互動式通訊。

## 將內容新增至互動式通訊 {#step2}

建立互動式通訊後，您可以使用互動式通訊製作介面來建立其內容。

如需互動式通訊製作介面的詳細資訊，請參 [閱互動式通訊製作簡介](/help/forms/using/introduction-interactive-communication-authoring.md)。

1. 如「建立互動式通訊」中所述，當您點選「編輯」時，就會啟動「互動式通訊 [」製作介面](#createic)。 或者，您也可以導覽至AEM上現有的互動式通訊資產，選取它，然後點選「編 **[!UICONTROL 輯]** 」以啟動互動式通訊製作介面。

   依預設，互動式通訊的列印頻道會出現，除非互動式通訊僅限網頁頻道。 「互動式通訊」的「列印」頻道會顯示目標區域，如所選XDP/列印頻道範本中所示。 在這些目標區域和欄位中，您可以新增元件或資產。

1. 在選取「列印」渠道後，選取「元 **[!UICONTROL 件]** 」標籤。 列印頻道提供下列元件：

   | **元件** | **功能** |
   |---|---|
   | 圖表 | 新增可在互動式通訊中使用的圖表，以視覺化方式呈現從表單資料模型收集擷取的二維資料。 如需詳細資訊，請參 [閱在互動式通訊中使用圖表](/help/forms/using/chart-component-interactive-communications.md)。 |
   | 文件片段 | 可讓您將可重複使用的元件（例如文字、清單或條件）新增至互動式通訊。 添加的元件可以是基於表單資料模型的元件，也可以是沒有表單資料模型的元件。 |
   | 影像 | 讓您插入影像。 |

   將元件拖放至您的互動式通訊中，並視需要加以設定。

   您也可以在針對列印和網頁頻道製作互動式通訊時，使用還原和重做作業。

   使用還原操作可放棄上次執行的操作，而重做操作可再次合併已放棄的操作。 例如，如果您已在「互動式通訊」中插入影像或建立資料系結，且需要捨棄它，請使用還原操作。

   ![還原重做動作](assets/undo_redo_actions_new.png)

   還原和重做選項會顯示在編寫UI頁面工具列上。 僅當執行動作後，才會顯示還原選項。 重做選項僅在執行撤消操作後才會顯示在頁面工具欄上。 重新整理頁面時，會重設這些動作。

1. 在選取列印渠道後，請前往「 **[!UICONTROL Assets]** 」索引標籤，並套用篩選以僅顯示您想要查看的資產。

   使用「資產」瀏覽器，您也可以直接將資產拖放至「互動式通訊」目標區域。

   ![assets-docfragments](assets/assets-docfragments.png)

1. 將檔案片段拖放至互動式通訊。 以下是您可在互動式通訊的列印管道中使用的檔案片段類型。

<table>
 <tbody>
  <tr>
   <td><strong>文件片段類型</strong></td>
   <td><strong>範例用途</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">文字</a></td>
   <td>新增地址、收件者電子郵件和信件正文的文字 </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">條件</a></td>
   <td>根據策略類型，將適當的標頭映像添加到通信的條件：Standard或Premium。 <br /> </td>
  </tr>
  <tr>
   <td>清單</td>
   <td>檔案片段群組，包括文字、條件、其他清單和影像。 <br /> </td>
  </tr>
 </tbody>
</table>

您也可以使用「資產」索引標籤，將新片段拖曳至目標區域，以取代目標區域與檔案片段之 **間的系** 結。 拖曳片段時目標區域的藍色陰影表示檔案片段可以拖曳至目標區域。

如需檔案片段的詳細資訊，請參 [閱檔案片段](/help/forms/using/document-fragments.md)。

製作介面可讓您區分互動式通訊中未系結和系結的欄位和變數。 介面會使用橘色邊框反白標示未系結的欄位和變數。

![unboind_fields_variables_highlights_dc](assets/unbound_fields_variables_highlights_dc.jpg)

此外，當您將滑鼠暫留在這些元素上時，工具提示會顯示「欄位（未系結）」或「變數（未系結）」訊息。

文檔片段中使用的未綁定變數有時不能顯示在編寫介面上。 這可能是因為檔案片段中的內嵌文字規則，或是條件片段的情況。 在這種情況下，以藍色反白顯示的工具提示會顯示為檔案片段的一部分。 工具提示會顯示檔案片段中使用的未系結變數數目。

![未系結變數](assets/df_unbound_variable_new.png)

點選檔案片段、點選 ![configure_icon](assets/configure_icon.png) (Configure)，然後從「互動式通訊」的側點點選「 **[!UICONTROL Properties]** 」。 「變 **[!UICONTROL 數與資料模型物件]** 」區段會列出變數，包括隱藏變數，以及檔案片段中使用的資料模型物件。 使用每 ![個資料模型](https://helpx.adobe.com/content/dam/help/images/en/edit.png) 物件或變數旁的編輯（編輯）圖示來編輯屬性。

1. 若要設定變數的系結，請點選變數並選取 ![configure_icon](assets/configure_icon.png) (Configure)，然後在側欄的「屬性」面板中設定系結屬性。

   * **無**:代理將填寫變數的值。
   * **文字片段**:如果選中此選項，您可以瀏覽並選擇文本文檔片段，其內容將呈現在欄位中。 只有這些文字檔案片段可以系結至其中沒有變數的變數。
   * **資料模型物件**:選擇在欄位中填入其值的表單資料模型屬性。
   * **** 預設值：您可以使用此欄位來定義變數的預設值。 當您預覽「互動式通訊」或在「代理」使用者介面中時，就會顯示該值。
   * **** 顯示模式：您也可以定義變數的顯示格式。 從「類型」( **Type** )下拉式清單中選取任何預先定義的選項，以套用顯示格式至變數。 選擇 **「自定義** 」(Custom)可定義清單中不可用的顯示模式。 如需詳細資訊，請參 [閱資料顯示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)。
   導覽至 [變數和資料模型物件](../../forms/using/create-interactive-communication.md#hiddenvariables) ，以設定檔案片段中隱藏變數的系結。

   您也可以拖放資料來源元素或文字檔案片段，以設定變數的系結。  若要建立與任何資料來源元素的系結，請選取「 **Data Sources** 」標籤，並將元素拖放至變數名稱。 資料來源元素和變數必須是相同類型，才能成功設定系結。 如果您將資料來源元素拖放至已系結的變數，新元素會取代先前的元素，以建立與變數的新系結。 同樣地，請選取「 **資產** 」標籤，並將文字檔案片段拖放至變數名稱，以設定它們之間的系結。 文字檔案片段不得包含任何變數。

1. 若要新增表格（已選取列印渠道），請在「 **[!UICONTROL Assets]** 」標籤中套用篩選條件，以僅顯示「版面片段」。 將所需的版面片段拖放至互動式通訊。 版面片段是以XDP為基礎，可用於在互動式通訊中建立圖形版面或靜態和動態表格，以填入動態資料。

   範例：可顯示毛額溢價、忠誠度折扣%，以及舊政策與新政策的緊急路邊協助。

   如需版面片段的詳細資訊，請參閱 [檔案片段](/help/forms/using/document-fragments.md)。

1. 在選取列印渠道後，「資產 **[!UICONTROL 」索引標籤中]** ，會將篩選套用至顯示影像。 將所需影像拖放至互動式通訊，例如公司標誌。

   此外，在互動式通訊中管理下列項目：

   * [添加和配置圖表](/help/forms/using/chart-component-interactive-communications.md)
   * [將網頁頻道與列印頻道同步](../../forms/using/create-interactive-communication.md#synchronize)

      * 自動同步
      * 取消繼承
      * 重新啟用繼承
      * 同步
   * [附件與資料庫存取](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [XDP/佈局欄位屬性](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [新增規則至元件](../../forms/using/create-interactive-communication.md#rules)


1. 切換至 **[!UICONTROL Web頻道]**。 網頁頻道會出現在互動式通訊編輯器中。 當您第一次從列印頻道切換至Web頻道時，會進行自動同步。 如需詳細資訊，請參 [閱從列印頻道同步化網頁頻道](../../forms/using/create-interactive-communication.md#synchronize)。

   由於我們在此範例中使用「列印」做為網頁的主版，因此列印頻道預留位置、內容和資料系結會同步至網頁頻道。 不過，您可以變更和自訂網路頻道中的特定內容。 [取消繼承](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) （對於使用列印頻道產生的目標區域和變數），以便自訂內容。

   ![網路頻道資產](assets/webchannelassets.png)

   點選檔案片段、點選 ![configure_icon](assets/configure_icon.png) (Configure)，然後從「互動式通訊」的側點點選「 **[!UICONTROL Properties]** 」。 「變 **[!UICONTROL 數與資料模型物件]** 」區段會列出變數，包括隱藏變數，以及檔案片段中使用的資料模型物件。 使用每 ![個資料模型](https://helpx.adobe.com/content/dam/help/images/en/edit.png) 物件或變數旁的編輯（編輯）圖示來編輯屬性。 此外，對於使用列印頻道在 [Web頻道中自動產生的檔案片段](../../forms/using/create-interactive-communication.md#main-pars-header-1213963149) ，請使用每個資料模型物件和變數旁的 ![](assets/cancelinheritance.png) （取消繼承）圖示來取消繼承 [](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) ，並可加以編輯。

1. 若要在選取網頁頻道時，在網頁頻道中新增其他元件，請點選「元 **[!UICONTROL 件]**」。 視需要將元件拖放至互動式通訊的網路頻道，然後繼續進行設定。

   | 元件 | 功能 |
   |---|---|
   | 圖表 | 新增可在互動式通訊中使用的圖表，以視覺化方式呈現從表單資料模型收集擷取的二維資料。 如需詳細資訊，請參 [閱使用圖表元件](../../forms/using/chart-component-interactive-communications.md)。 |
   | 文件片段 | 可讓您將可重複使用的元件、文字、清單或條件新增至互動式通訊。 您新增至互動式通訊的可重複使用元件可以是以表單資料模型為基礎，或是沒有表單資料模型。 |
   | 影像 | 讓您插入影像。 |
   | 面板 | 可讓您將面板新 [增至](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) 「互動式通訊」。 |
   | 表格 | 新增表格以整理行和欄中的資料。 |
   | 目標區域 | 在Web頻道中插入目標區域，以組織Web頻道特定的元件。 目標區域是一個簡單容器，可讓您將Web頻道特定元件分組。 |
   | 文字 | 將豐富式文字新增至互動式通訊的網路頻道。 文本還可以利用表單資料模型對象使內容動態化。 |
   | 按鈕 | 允許您將「按 [鈕](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 」添加到交互通信。 您可以使用Button元件來導覽至其他互動式通訊、最適化表單、其他資產（例如影像或檔案片段）或外部URL。 |
   | 分隔符號 | 允許您在互動式通信中插入水準線。 使用此元件可以區分通信中的各個部分。 例如，您可以使用「分隔符號」元件來區分信用卡對帳單中的「客戶詳細資訊」和「信用卡詳細資訊」部分。 |

1. 視需要，將資產插入您的網頁頻道。

   您可以 [預覽互動式通訊](#previewic) ，以檢視互動式通訊的列印和網頁輸出外觀，並視需要繼續進行變更。

## 預覽互動式通訊 {#previewic}

您可以使用「預 **覽」選項** ，評估「互動式通訊」的外觀。 互動式通訊的網路頻道也提供多種裝置模擬互動式通訊體驗的選項。 例如，iPhone、iPad和Desktop。 您可以搭配使 **用「預覽** 」和「模擬器 **** 」尺標選項 ![](assets/ruler.png) ，以預覽不同螢幕大小的裝置的網頁輸出。 預覽中的範例資料會從指定的表單資料模型填入。

1. 選取（列印或網頁）頻道以預覽並點選預覽。 出現「Interactive Communication（互動式通信）」。

   >[!NOTE]
   >
   >預覽會填入指定表單資料模型的範例資料。 如需有關使用某些其他資料或使用預填服務來預覽互動式通訊的詳細資訊，請參閱「使用表單資料模型 [」](/help/forms/using/using-form-data-model.md) 和「使用表單資料模型」 [](/help/forms/using/work-with-form-data-model.md)。

1. 對於Web頻道，請使用尺 ![標](assets/ruler.png) ，檢視互動式通訊在各種裝置上的外觀。

   ![網路頻道預覽](assets/webchannelpreview.png)

此外，您還可 [以使用Agent UI準備和發送互動式通信](/help/forms/using/prepare-send-interactive-communication.md)。

## 在互動式通訊中設定屬性 {#configure-properties-in-interactive-communication}

### 附件與資料庫存取 {#attachmentslibrary}

在打印渠道中，您可以配置附件和庫訪問權限，以允許代理在互動式通信的代理UI中管理附件：

1. 在「列印」頻道中，反白標示「檔案容器」並點選「 **屬性**」。

   ![文檔容器屬性](assets/documentcontainerproperties.png)

   「屬性」面板出現在側欄中。

   ![屬性附件](assets/propertiesattachments.png)

1. 展開 **附件** ，並指定以下屬性：

   * **[!UICONTROL 允許程式庫存取]**:在「代理UI」中選擇以啟用代理的庫訪問。 如果啟用，代理可在準備互動式通訊時從程式庫新增檔案。
   * **[!UICONTROL 允許重新排序附件]**:選擇此選項可讓代理使用互動式通信重新排序附件。
   * **[!UICONTROL 允許的附件數上限]**:指定「互動式通訊」允許的附件數上限。
   * **[!UICONTROL 要附加的檔案]**:點選 **[!UICONTROL 「新增]** 」並瀏覽以選取要附加的檔案，並指定下列項目：

      * **[!UICONTROL 依預設將此檔案附加至檔案]**:如果附件不是「強制」，則可以更改此選項。
      * **** 強制：代理將無法刪除代理UI中的附件。
   ![附件](assets/attachfiles.png)

1. 點選「 **[!UICONTROL 完成]**」。

### XDP/佈局欄位屬性 {#xdplayoutfieldproperties}

1. 編輯互動式通訊的列印頻道時，將滑鼠指標暫留在列印頻道範本內建的欄位上，然後選取 ![configure_icon](assets/configure_icon.png) (Configure)。

   「屬性」對話框出現在側欄中。

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. 指定下列項目：

   * **[!UICONTROL 名稱]**:JCR節點名稱。
   * **[!UICONTROL 標題]**:在「代理UI」和「文檔容器」樹中輸入座席可見的標題。
   * **[!UICONTROL 綁定類型]**:為欄位選擇以下綁定類型之一。

      * 無：工程師將填寫屬性的值。
      * 文字片段：如果選中此選項，您可以瀏覽並選擇文本文檔片段，其內容將呈現在欄位中。 或者，將文字檔案片段拖放至欄位名稱，以設定它們之間的系結。 文字檔案片段不得包含任何變數。
      * 資料模型對象：選擇在欄位中填入其值的表單資料模型屬性。 或者，選取「 **資料來源」標籤** ，並將屬性拖放至欄位。
   * **[!UICONTROL 預設值]**:當指定的資料模型對象或文本片段沒有提供值時，預設值可確保欄位不為空。 如果資料系結類型為無，則會在欄位中預先填入預設值。
   * **[!UICONTROL 顯示模式]**:您也可以定義欄位的顯示格式。 從「類型」( **Type** )下拉式清單中選取任何預先定義的選項，以套用顯示格式至欄位。 選擇 **「自定義** 」(Custom)可定義清單中不可用的顯示模式。 如需詳細資訊，請參閱「資 [料顯示模式」](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Editable By Agent]**:選擇此選項可允許代理編輯代理UI中欄位中的值。 如果「綁定類型」是「文本片段」，則此設定不適用。
   * **[!UICONTROL 標籤]**:在Agent UI中為Agent指定與欄位一起顯示的文本字串。 如果「綁定類型」是「文本片段」，則此設定不適用。
   * **[!UICONTROL 工具提示]**:在Agent UI中，將滑鼠移到Agent上，輸入文本字串。 如果「綁定類型」是「文本片段」，則此設定不適用。
   * **[!UICONTROL 必要]**:選擇該選項可使座席的欄位成為必填欄位。 如果「綁定類型」是「文本片段」，則此設定不適用。
   * **[!UICONTROL 允許多行]**:選取此欄位可允許在欄位中輸入多行文字。 如果「綁定類型」是「文本片段」，則此設定不適用。


1. 點選 ![done_icon](assets/done_icon.png)。

### 資料顯示模式 {#datadisplaypatterns}

製作介面可讓您定義欄位、變數和表單資料模型元素的資料顯示模式，以建立適用於印刷和網頁通道的互動式通訊。

若要設定資料顯示模式，請點選元素，選取 ![configure_icon](assets/configure_icon.png) (Configure)，然後在側欄的「屬性 **** 」面板中設定顯示模式。 從「類型」( **[!UICONTROL Type]** )下拉式清單中選取任何預先定義的選項，以檢視與所選類型相關聯的模式。 從「類 **[!UICONTROL 型」(]** Type **[!UICONTROL )下拉式清單中選取「自訂」(Custom]** )，以定義清單中不可用的模式。 在「模式」欄位中編 **[!UICONTROL 輯值]** ，會自動將類型修改為「 **[!UICONTROL 自訂」]**。

若要套用顯示模式，「模式」欄位中定義的字元或位數必須符合或超過欄位、變數和表單資料模型元素值中定義的字元或位數。 如需詳細資訊，請參 [閱範例](../../forms/using/create-interactive-communication.md#greaternumberofdigits)。

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

從列印頻道產生Web內容後，您可重新定義欄位、變數或表單資料模型元素的顯示模式。 因此，元素可以具有為打印和網頁通道定義的不同顯示模式。 如果您未定義列印頻道中的元素的顯示模式，並使用列印頻道自動產生網頁內容，則為列印頻道中的元素定義的資料系結會定義「類型」下拉式清單中可用的顯示模式選項。 **** 如果沒有為元素定義綁定，元素的資料類型將定義可用的顯示陣列選項。 例如，如果您為列印頻道中的元素建立「編號」類型的資料系結，「類型」下拉式清單中可用的顯示模式選項會以各種格式呈現「編號」類型。 ****

切換至「預 **覽** 」模式或開啟Agent UI，以檢視套用至這些元素的顯示模式。

下表列出設定變數資料顯示模式後所顯示之值的範例：

| 類型 | 預設值 | 顯示圖樣 | 顯示值 | 說明 |
|---|---|---|---|---|
| SocialSecurityNumber | 123456789 | text{999-99-9999} | 123-45-6789 | 預設值欄位中的位數與「模式」欄位中的位數匹配。 根據圖樣的值會成功顯示。 |
| SocialSecurityNumber | 1234567 | text{999-99-9999} | 1-23-4567 | 預設值欄位中的位數小於「模式」欄位中的位數。 該模式適用於7個可用數字。 |
| SocialSecurityNumber | 1234567890 | text{999-99-9999} | 1234567890 | 預設值欄位中的位數大於「模式」欄位中的位數。 因此，顯示值沒有變化。 |

如果未為變數或表單資料模型元素指定顯示模式，則 [預設會使用全域檔案片段設定](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) 。

如果您未將顯示模式套用至數字資料類型的變數，「列印預覽」會根據全域檔案片段設定來顯示模式。 如果對預設全局文檔片段配置應用更改，代理UI仍會根據為區域設定定義的預設分隔符顯示模式。

同樣地，對於欄位，如果未指定顯示模式，則建立打印模板(XDP)時定義的模式將應用於欄位。 如果在建立打印模板時沒有模式，則基於XFA規範的預設模式將應用於這些欄位。

此外，如果指定的顯示模式不正確或無法應用，則基於XFA規範的預設模式將應用於欄位、變數或表單資料模型元素。

## 套用規則至互動式通訊元件 {#rules}

若要在互動式通訊中條件化元件或內容，請點選元件／內容片段，然後選取「建立 ![規則](assets/createruleicon.png) 」(Create Rule)以啟動「規則編輯器」。

如需詳細資訊，請參閱：

* [規則編輯器](/help/forms/using/rule-editor.md)
* [互動式通訊製作簡介](/help/forms/using/introduction-interactive-communication-authoring.md)

## 使用表 {#tables}

### 互動式通訊中的動態表格 {#dynamic-tables-in-interactive-communication}

您可以使用版面片段在互動通訊中新增動態表格。 下列步驟使用信用卡對帳單的範例來說明在互動式通訊中建立動態表格時使用版面片段的情形。

1. 請確定建立表格所需的版面片段可在AEM中使用。
1. 在互動式通訊的列印頻道中，從資產瀏覽器將版面片段（含多欄表格）拖放至目標區域。

   ![lf_dragdrop](assets/lf_dragdrop.png)

   「互動式通訊」版面配置區域中會出現一個表格。

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. 指定表格各儲存格的資料系結。 要建立可重複行，請在屬於公共收集屬性的行中插入表單資料模型屬性。

   1. 點選表格中的儲存格，並選 ![取configure_icon](assets/configure_icon.png) (Configure)。

      「屬性」對話框出現在側欄中。

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. 設定屬性：

      * **[!UICONTROL 名稱]**:JCR節點名稱。
      * **[!UICONTROL 標題]**:輸入將在交互通信編輯器中顯示的標題。
      * **[!UICONTROL 綁定類型]**:為欄位選擇以下綁定類型之一。

         * **[!UICONTROL 無]**
         * **[!UICONTROL 資料模型物件]**:表單資料模型屬性的值會填入欄位中。 或者，選取「 **資料來源」標籤** ，並將屬性拖放至欄位。
      * **[!UICONTROL 資料模型物件]**:在欄位中填入其值的表單資料模型屬性。
      * **[!UICONTROL 預設值]**:當指定的資料模型對象沒有提供值時，預設值可確保欄位不為空。 預設值會預先填入欄位中。

      * **[!UICONTROL Editable By Agent]**:選擇此選項可允許代理編輯代理UI中欄位中的值。
   1. 點選 ![done_icon](assets/done_icon.png)。



1. 預覽互動式通訊，以檢視以資料呈現的表格。

   ![lf_preview](assets/lf_preview.png)

### 僅限Web通道的表 {#webchanneltables}

點選Web範本中的根面板，並點選 **+** ，將 **Table** 元件新增至互動式通訊。 在交互通信中插入包含兩行的表。 表的第一行表示表標題。

#### 將行和列添加到表 {#addrowscolumnstable}

**要添加或刪除列：**

1. 點選表格標題列中的預設文字方塊以檢視元件工具列。
1. 分別 **選擇「添加列** 」或「 **刪除列** 」以添加或刪除表列。

![component_toolbar_table1](assets/component_toolbar_table1.png)

**要添加或刪除行：**

1. 點選任何表格列以檢視元件工具列。 您也可以使用互動式通訊旁邊的「內容」瀏覽器來選取表格列。
1. 選 **擇「添加行** 」或「 **刪除行** 」分別添加或刪除表行。 使用工 **具列中的** 「上移」(Move Up)和「 **下移」(Move Down** )選項重新排清單格中的行。

![元件工具列](assets/component_toolbar_table_row_new.png)

******** 答：添加行 **B。刪除**&#x200B;行C.**上**&#x200B;移D。向下移動

#### 在表格儲存格中新增或編輯文字 {#addedittexttable}

1. 在表格儲存格中選取預設文字方塊，然後點選 ![](assets/edit.png) （編輯）。
1. 在表格儲存格中輸入文字，然後點選 ![](assets/done_icon.png) 以儲存它。

#### 在表格儲存格和資料模型物件元素之間建立系結 {#createbindingtablecells}

1. 在表格列中選取預設文字方塊，然後點選 ![](assets/edit.png) （編輯）。
1. 點選「資料模型物件」下拉式清單，並選取屬性。
1. 點選以儲存表格儲存格和資料模型物件屬性之間的系結。

![建立資料系結](assets/create_data_binding_table_new.png)

#### 為表格儲存格中的文字建立超連結 {#createhyperlinktable}

1. 在表格儲存格中選取預設文字方塊，然後點選 ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) （編輯）。
1. 選取表格儲存格中的文字，並點選「超連結」圖示。
1. 在「路徑」欄位中指 **定URL** 。
1. 點選 ![](assets/done_icon.png) 以儲存超連結屬性。

![建立超連結](assets/create_hyperlink_table_new.png)

#### 建立動態表格 {#createdynamictables}

您可以使用類型集合的資料模型屬性，在「互動式通訊」中建立僅限Web頻道的動態表格。 此表是集合屬性的子屬性的表示。 您只能編輯表格中各個儲存格的格式屬性。

1. 切換至Web頻道，然後選擇顯示Data Sources瀏覽器。
1. 將系列屬性拖放至子表單。 在子表單中建立表。
1. 在互動式通訊的網頁預覽中預覽表格。

#### 對表中的列進行排序 {#sortcolumns}

您可以根據互動式通訊中表格中的任何欄來排序資料。 列中的值可以按升序或降序排序。

排序可應用於包含：

* 靜態文字
* 資料模型對象屬性
* 靜態文字與資料模型物件屬性的組合

要啟用排序：

1. 選取表格並點選 ![](assets/configure_icon.png) （設定）。 您也可以使用互動式通訊的側 **邊** ，使用內容瀏覽器選取表格。
1. 選擇 **啟用排序。**
1. 點選 ![](assets/done_icon.png) 以儲存表格屬性。 欄標題中的排序圖示（向上和向下箭頭）表示已啟用排序。

   ![啟用排序](assets/enable_sorting_new-1.png)

1. 切換至「 **預覽** 」模式以檢視輸出。 表格會根據表格的第一欄自動排序。
1. 按一下欄標題，以根據欄排序值。

   具有向上箭頭的欄標題代表：

   * 表格會根據該欄排序。
   * 列中的值以升序顯示。
   ![升序排序](assets/sorting_ascending_new-1.png)

   同樣地，帶有向下箭頭的列標題表示列中的值以降序顯示。

## 編輯互動式通訊屬性 {#edit-interactive-communication-properties}

建立互動式通訊後，您就可以在稍後階段編輯其屬性。

使用「屬 **性** 」頁可以：

* 編輯建立互動通訊時指定欄位的值，例如「標題」和「說明」。
* 新增或刪除現有互動式通訊的網路頻道。
* 預覽、下載或刪除互動式通訊
* 開啟 [Agent UI](/help/forms/using/prepare-send-interactive-communication.md)。

要訪問「屬 **性** 」頁：

1. 登入AEM作者例項並導覽至 **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**。
1. 選擇「互動式通訊」並點選「 **屬性**」。
1. 選擇「 **一般** 」標籤以編輯「 **標題** 」和「 **說明** 」欄位。

### 新增或刪除Web頻道 {#add-or-delete-the-web-channel}

執行以下步驟，為現有互動式通信添加Web通道：

1. 在「屬 **性** 」頁面上，選 **取「渠道** 」標籤。
1. 選取「 **Web** 」核取方塊，並選取「Web頻道」的範本。
1. 選擇 **使用打印作為Web渠道的主要內容** ，以啟用Web渠道和打印渠道之間的同步。
1. 點選 **「儲存並關閉** 」以儲存變更。

   同樣地，您也可以點選「 **頻道** 」標籤上的「網頁」核取方 **** 塊，從「互動式通訊」中刪除網頁頻道。

## 新增按鈕元件至Web頻道 {#add-button-component-to-the-web-channel}

您可以將按鈕新增為互動式通訊的網路頻道元件。 使用規則編 [輯器](../../forms/using/rule-editor.md) ，定義規則，以便能夠導覽至其他互動式通訊、最適化表單、其他資產（例如影像或檔案片段），或在點選按鈕時導覽外部URL。

若要新增按鈕並定義其上的規則：

1. 點選Web範本中的根面板，並點選 **+** ，將 **Button** （按鈕）元件新增至互動式通訊。
1. 點選按鈕元件並點選 ![](assets/edit-rules.png) 以在點選按鈕時定義規則。
1. 在「 **When** 」區段中，從 **** 按鈕下拉式清單的狀態中選取「已點按」。
1. 在Then **區** :

   1. 從下拉式清單中選取動作。 例如，選擇「 **導航至** 」作為操作類型。

   1. 指定互動式通訊、最適化表單、資產或網頁的URL。 例如，以下列格式指定URL，以導覽至另一個互動式通訊：https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;互動式通訊名稱>/channels/&lt;channel name - print or web>.html
   1. 指定在相同標籤、新標籤或新視窗中開啟資產的選項。
   1. 點選 **「完成** 」，然後點選「 **關閉** 」以儲存規則。
   同樣地，您也可以從動作類型下拉式清單中選取其他可用選項，例如叫用服務和送出表單。 如需詳細資訊，請參 [閱規則編輯器](../../forms/using/rule-editor.md)。

1. 預覽互動式通訊並點選按鈕，以檢視在步驟4(b)中指定的互動式通訊、調適性表單、資產或網頁。

## 新增面板元件至網頁頻道 {#add-panel-component-to-the-web-channel}

「面板」元件是將其他元件分組在一起的預留位置，可控制在「互動式通訊」中如何排列一組元件，例如accordion和標籤。 面板元件還允許您讓一組元件為最終用戶重複使用，例如在填寫教育證書所需的多個條目中。

執行下列步驟，將面板元件新增至網頁頻道：

1. 使用下 **列任一選項** ，將面板元件插入網頁頻道：

   * 點選元件，點選 **+** ，然後選取 **面板元件** 。

   * 從「元 **件** 」瀏覽器面板，拖放「互動式通訊」上的 **「面板** 」元件。

   * 點選「 **內容** 」瀏覽器面板中的「面板 **」，然後點選「** 新增子面板」 ****。 選擇「添 **加子面板** 」選項會顯 **** 示「添加子面板」對話框。 輸入Panel元件的標題和可選說明和名稱。

1. 從「內容 **** 」瀏覽器點選面板，在「面板」上執行其他動作，例如設定、編輯規則、複製、刪除和插入元件。

   您也可以在「內容」瀏覽器中拖放面板，以反映右窗格中「互動式通訊」結構的變更。 ****

## 同步化網頁頻道與列印頻道 {#synchronize}

當您在建立互動式通訊時選取「列印為網頁頻道的主版」時，會建立與列印頻道同步的網頁頻道，而網頁頻道的內容與資料系結會從列印頻道衍生出來，當您點選「同步化」時，列印頻道中所做的變更可能會反映在網頁頻道中。

但是，作者可以視需要中斷Web頻道中元件的繼承。

![建立打印主版](assets/create_ic_print_master_new-1.png)![打印主版Web](assets/create_ic_print_master_web_new-1.png)

### 自動同步 {#autosync}

如果您選取「 **[!UICONTROL 使用列印為網頁頻道的主版」選項]** ，您可以選取下列任一種模式來產生網頁頻道：

* **[!UICONTROL 自動版面]**:選取此模式可自動從列印頻道產生網頁頻道的預留位置、內容和資料系結。
* **[!UICONTROL 手動組織]**:選取此模式，可使用「資料來源」標籤中的主要內容，手動選取列印渠道元素並新增至網路渠道。 如需詳細資訊，請參 [閱選取列印頻道元素以建立網頁頻道內容](#selectprintchannelelements)。

![建立IC選項](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>同步化頻道時，僅會同步從列印頻道到網頁頻道的檔案片段、影像、條件、清單和版面片段。 包含這些元素的子表單或父節點不會同步。

### 選擇列印頻道元素以建立網頁頻道內容 {#selectprintchannelelements}

如果您在建立「互動式通信」時選擇「打印為主版」，但不選擇自動同步選項，則還可以將打印渠道元素拖放到Web渠道編寫介面。

導覽至「 **資料來源** >主 **要內容** 」以檢視列印渠道元素。 將目標區域、欄位或表格拖放至網頁頻道製作介面。 元素名稱旁的藍色圓圈圖示表示「列印」色版元素已包含在網頁色版中。

![主要內容](assets/master_content.png)

### 取消繼承 {#cancelinheritance}

在Web頻道中，元件會內嵌在目標區域中。

將滑鼠指標暫留在Web頻道中的相關目標區域或變數上，然後選取「取消繼承 ![」（取消繼承），然後在「取消繼承」對話方塊中，點選「](assets/cancelinheritance.png) 是」 ****。

目標區域內元件的繼承將被取消，現在您可以根據需要進行編輯。

### 重啟先前設定 {#re-enable-inheritance}

在Web渠道中，如果已取消元件的繼承，則可重新啟用它。 若要重新啟用繼承，請將滑鼠指標暫留在包含元件的相關目標區域的邊界上，然後點選重新啟 ![用繼承](assets/reenableinheritance.png)。

將出現「恢復繼承」對話框。

![尊重遺產](assets/revertinheritance.png)

如果需要，請選 **[!UICONTROL 擇「還原繼承後同步頁面」]**。 選擇此選項可同步整個互動通信。 如果未選擇此選項，則恢復繼承時，只會同步相關目標區域。

點選「 **[!UICONTROL 是」]**。

### 同步 {#synchronize-1}

如果您使用「列印為網頁頻道的主版」並變更「列印」頻道，則可同步化內容，將最新變更帶入網頁頻道。

1. 若要將Web頻道與列印頻道同步，請切換至Web頻道，然後點選「更多選項」圖示。

   ![自動同步選項](assets/auto_sync_options_new.png)

1. 點選下列其中一項：

   * **[!UICONTROL 與列印同步]**:僅同步未取消繼承的目標區域的內容。
   * **[!UICONTROL 重設]**:將網路頻道內容與列印頻道同步，並捨棄對網路頻道所做的所有變更。

### 使用元件工具列對繼承的元件執行動作 {#componenttoolbar}

使用「同步」選項在網頁頻道中自動產生內容後，您就可以在元件上執行更多動作，而不會取消繼承。

![元件工具列](assets/component_toolbar_inherited_web_new.png)

點選元件可檢視下列選項：

* **** 複製：複製元件並貼至「互動式通訊」的其他位置。
* **** 剪下：在「互動式通訊」中，將元件從一個位置移至另一個位置。
* **** 插入元件：在選定元件上方插入元件。
* **** 貼上：使用上述選項貼上您剪切或複製的元件。
* **** 群組：如果要剪下、複製或貼上多個元件，請選擇多個元件。
* **** 父級：選擇元件的父代。
* **** 查看SOM表達式：查看 [元件的SOM表達式](../../forms/using/using-som-expressions-adaptive-forms.md) 。

* **** 在面板中對對象進行分組：將面板中的元件分組，以便能夠同時對這些元件執行操作。 如需詳細資訊，請參 **[閱「面板」中的「群組物件」](../../forms/using/create-interactive-communication.md#main-pars-header-1815149576)**。

* **** 取消繼承：取 [消目標區域](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) 內元件的繼承以進行編輯。

### Group objects in Panel {#groupobjectspanel}

網頁頻道製作介面有助於將面板中的元件分組，以便能夠同時對這些元件執行操作。 「內 **容** 」頁籤將分組的元件列為內容樹中面板的子元素。

1. 點選元件並選取「群組( ![群組](assets/group.jpg))」作業。
1. 選取多個元件並點選「 **面板」中的「群組物件」**。

   ![群組物件](assets/component_toolbar_group_objects_new.png)

1. 在「面板 **中的組對象** 」對話框中，輸入面板的名稱。
1. 輸入面板的可選標題和說明。
1. 按一 ![下bullet_checkmark](assets/bullet_checkmark.png)。

   分組的元件在內容樹中顯示為「面板」的子元素。

   ![content_tree_grouping](assets/content_tree_grouping.png)

