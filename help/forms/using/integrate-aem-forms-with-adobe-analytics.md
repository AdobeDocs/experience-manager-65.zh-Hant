---
title: 如何整合AEM Forms與Adobe Analytics?
description: AEM Forms與Adobe Analytics整合，以擷取及追蹤已發佈表單的效能量度。
docset: aem65
source-git-commit: 503e579a00c9e029393b0a8a580faba2231c7589
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---


# Analytics使用 [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms整合 [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) 來擷取及追蹤已發佈表單的效能量度。 分析這些量度的目標是讓業務使用者能夠深入分析一般使用者行為，並最佳化資料擷取體驗。 您可以透過Adobe Analytics for Adaptive Forms，擷取及追蹤登入和非登入（匿名）使用者的行為。

您也可以使用Cloud Service架構執行分析。 如需如何將AEM Forms與Cloud Service架構整合的詳細資訊，請參閱 [使用Cloud Service架構的Analytics](/help/forms/using/configure-analytics-forms-documents.md). 透過Cloud Service架構使用Adobe啟動（而非Analytics）的主要優點，是除了這些現成可用的事件外，您也可以定義自訂事件。 自訂事件是使用規則編輯器或客戶客戶端lib來定義，並對應至 [!DNL Adobe Analytics].

執行本文提及的動作後，您可以在 [!DNL Adobe Analytics]，如下列影片所示：

>[!VIDEO](https://video.tv.adobe.com/v/337262)

您可以使用 [!DNL Adobe Analytics] 探索使用者使用最適化表單時所面臨的互動模式和問題。 現成可用， [!DNL Adobe Analytics] 追蹤並儲存下列事件的相關資訊：

* **呈現**:表單開啟的次數。

* **提交**:表單的提交次數。

* **放棄**:使用者未填妥表單就離開的次數。

* **錯誤**:在面板和面板欄位上遇到的錯誤數。

* **說明**:使用者開啟面板說明和面板欄位的次數。

* **欄位造訪**:使用者造訪表單中欄位的次數。

* **儲存**:使用者將表單儲存至Forms入口網站的次數。

除了這些現成可用的事件，您也可以定義自訂事件。

下圖說明在中檢視報表之前，您需要執行的動作 [!DNL Adobe Analytics]:

![Analytics概觀](/help/forms/using/assets/analyticsworkflow.png)

## 1.配置 [!DNL Adobe Analytics] {#Configure-adobe-analytics}

設定前 [!DNL Adobe Analytics]，建立：

* 要登入的Adobe ID [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [報表套裝](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### 安裝AEM Forms和 [!DNL Adobe Analytics] 擴充功能 {#install-extensions}

執行下列步驟來設定AEM Forms和 [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) 擴充功能：

1. 登入Adobe Experience Cloud，並為公司選取適當的名稱。

1. 點選 **[!UICONTROL 啟動/資料收集]** 點選 **[!UICONTROL 前往Launch/資料收集]**.

1. 點選 **[!UICONTROL 新屬性]** 並指定設定的名稱。

1. 指定網域名稱並點選 **[!UICONTROL 儲存]** 以儲存屬性。

1. 點選「標籤屬性」清單中可用的設定名稱。

1. 在 **[!UICONTROL 製作]** 區段，點選 **[!UICONTROL 擴充功能]**.

1. 點選 **[!UICONTROL 目錄]** 點選 **[!UICONTROL 安裝]** 針對 **[!UICONTROL Adobe Experience Manager Forms]** 擴充功能。 **[!UICONTROL Adobe Experience Manager Forms]** 顯示在 **已安裝** 標籤。

1. 點選 **[!UICONTROL 安裝]** 針對 **[!UICONTROL Adobe Analytics]** 擴充功能。
1. 在 **[!UICONTROL 開發報表套裝]**, **[!UICONTROL 測試報表套裝]**，和 **[!UICONTROL 產品報表套裝]** 下拉式清單並點選 **[!UICONTROL 儲存]** 以儲存擴充功能。

### 設定資料元素 {#configure-data-elements}

您可以在為事件建立的規則中選取任何已設定的資料元素。 適用性表單上發生事件時，AEM Forms會將這些資料元素傳送至 [!DNL Adobe Analytics].

安裝 **[!UICONTROL Adobe Experience Manager Forms]** 擴充功能，您可以建立下列資料元素：

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>表單標題<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

執行下列步驟來設定資料元素：

1. 在 **[!UICONTROL 製作]** 區段，點選 **[!UICONTROL 資料元素]**.

1. 點選 **[!UICONTROL 建立新資料元素]**.

1. 指定資料元素的名稱。 例如， FormTitle資料元素類型的表單標題。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為擴充功能名稱。

1. 選取 **[!UICONTROL 資料元素類型]**.

1. 點選 **[!UICONTROL 儲存]** 儲存資料元素。

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 設定規則 {#configure-rules}

執行下列步驟，根據 **[!UICONTROL Adobe Experience Manager Forms]** 擴充功能：

1. 在 **[!UICONTROL 製作]** 區段，點選 **[!UICONTROL 規則]**.

1. 點選 **[!UICONTROL 建立新規則]**.

1. 指定規則的名稱。 例如，表單提交可記錄表單提交。

1. 在 **[!UICONTROL 事件]** 區段，點選 **[!UICONTROL 新增]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為擴充功能名稱。

1. 選取事件類型。 輸入 **[!UICONTROL 名稱]** 欄位會根據選取的事件類型自動填入。

1. 點選 **[!UICONTROL 保留變更]** 以儲存事件。

1. 在 **[!UICONTROL 動作]** 區段，點選 **[!UICONTROL 新增]**.

1. 指定 **[!UICONTROL Adobe Analytics]** 作為擴充功能名稱。

1. 選擇 **[!UICONTROL 設定變數]** 作為動作類型。 下拉式清單中可用的選項包括：

   * **[!UICONTROL 設定變數]**:使用此動作類型來定義所選資料元素從AEM Forms傳送至的事件類型 [!DNL Adobe Analytics].

   * **[!UICONTROL 傳送信標]**:使用此動作類型將資料從AEM Forms傳送至 [!DNL Adobe Analytics].

   * **[!UICONTROL 清除變數]**:使用此動作類型來清除資料追蹤，讓事件只在 [!DNL Adobe Analytics].

      建議的方法是使用 **[!UICONTROL 設定變數]** 動作類型以設定事件和資料元素，然後使用 **[!UICONTROL 傳送信標]** 傳送資料，然後使用 **[!UICONTROL 清除變數]** 來清除資料追蹤。

1. 在 **[!UICONTROL Prop]** 區段中，將下拉式清單中可用的報表套裝選項與使用 [設定資料元素](#configure-data-elements).

   例如，若要傳送 **表單標題** 資料元素從AEM Forms到 [!DNL Adobe Analytics] 提交表單時：
   1. 在 **[!UICONTROL Prop]** 區段中，選取報表套裝中可用「表單標題」的屬性，然後點選 ![資料庫表徵圖](/help/forms/using/assets/database-icon.svg) 將其對應至中建立的表單標題 [設定資料元素](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. 點選 **[!UICONTROL 新增其他]** 新增更多資料元素至清單。

1. 在 **[!UICONTROL 事件]** 區段中，從報表套裝中可用的選項中選取事件，然後點選 **[!UICONTROL 保留變更]**.

1. 在 **[!UICONTROL 動作]** 區段，點選+並指定 **[!UICONTROL Adobe Analytics]** 作為擴充功能名稱。

1. 選擇 **[!UICONTROL 傳送信標]** 作為動作類型。 在右窗格中，選擇 **[!UICONTROL s.t()]** 將資料傳送至 [!DNL Adobe Analytics] 並視為頁面檢視，或 **[!UICONTROL s.tl()]** 將資料傳送至 [!DNL Adobe Analytics] 並且請勿將其視為頁面檢視。 點選 **[!UICONTROL 保留變更]**.

1. 在 **[!UICONTROL 動作]** 區段，點選+並指定 **[!UICONTROL Adobe Analytics]** 作為擴充功能名稱。

1. 選擇 **[!UICONTROL 清除變數]** 作為動作類型。 點選 **[!UICONTROL 保留變更]**. 執行這些步驟後， **[!UICONTROL 動作]** 區段顯示為：
   ![動作設定](/help/forms/using/assets/actions-config.png)

   自訂 **[!UICONTROL 動作]** 區段。 例如，您可以定義兩個 **傳送信標** 動作流程中將資料傳送至 [!DNL Adobe Analytics] 並將其視為單一步驟中的頁面檢視，然後將資料傳送至 [!DNL Adobe Analytics] 並且請勿在第二個步驟中將其視為頁面檢視。

   ![動作設定](/help/forms/using/assets/actions-config-2.png)

1. 點選 **[!UICONTROL 儲存]** 來儲存規則。

   您可以為所有事件類型建立規則，例如「放棄」、「錯誤」、「欄位造訪」、「說明」、「轉譯」、「儲存」和「提交」。

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### 發佈流程 {#publish-flow}

建立資料元素並在規則中使用後，請發佈設定以收集 [!DNL Adobe Analytics].

執行下列步驟以發佈設定：

1. 在 **[!UICONTROL 發佈]** 區段，點選 **[!UICONTROL 發佈流程]**.

1. 點選 **[!UICONTROL 新增程式庫]** 並指定名稱，然後選取程式庫的環境。

1. 點選 **[!UICONTROL 新增所有已變更的資源]** 然後點選 **[!UICONTROL 儲存並建置至開發]**.

1. 在 **[!UICONTROL 開發]** 區段，點選 ![更多選項](/help/forms/using/assets/more-options-icon.svg) 然後點選 **[!UICONTROL 核准並發佈至生產環境]**.

1. 確認變更，發佈流程很快會顯示在 **[!UICONTROL 已發佈]** 區段。

![發佈流程](/help/forms/using/assets/publish-flow.png)

## 2.設定AEM Forms {#configure-aem-forms}

建立AdobeLaunch設定前，請先建立 [使用AdobeLaunch雲端解決方案設定Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### 建立 Adobe Launch 設定 {#create-adobe-launch-configuration}

執行下列步驟以建立AdobeLaunch設定：

1. 在AEM Forms Author例項上，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe啟動設定]**.

1. 選取要建立設定的資料夾，然後點選 **[!UICONTROL 建立]**.

1. 在 **[!UICONTROL 標題]** 欄位。

1. 選取 [相關聯的Adobe IMS設定](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. 選取使用的公司名稱 [設定Adobe Analytics](#Configure-adobe-analytics).

1. 選取在 [設定Adobe Analytics](#install-extensions).

1. 點選 **[!UICONTROL 儲存並關閉]**.

1. 發佈設定。

### 啟用 [!DNL Adobe Analytics] 最適化表單 {#enable-analytics-adaptive-form}

使用 [!DNL Adobe Launch] 設定：

1. 在AEM Forms Author例項上，導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取「最適化表單」並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 頁簽，選擇 [組態容器](#create-adobe-launch-configuration) 建立Adobe啟動設定時使用。
1. 點選 **[!UICONTROL 儲存並關閉]**. 適用性表單已啟用 [!DNL Adobe Analytics].
1. 發佈表單。

啟用後 [!DNL Adobe Analytics] 對於最適化表單，您可以 [驗證](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) 如果AEM Forms和之間有適當的資料事件流 [!DNL Adobe Analytics]. AEM Forms與Adobe Analytics的整合已完成。 您現在可以 [在Adobe Analytics中設定和檢視報表](#view-reports-adobe-analytics).

>[!NOTE]
>在情況下，如果兩者 [使用Cloud Service架構的Analytics](/help/forms/using/configure-analytics-forms-documents.md) 和 **使用Adobe啟動的Analytics** 功能同時啟用， **使用Adobe啟動的Analytics** 會優先。

### 建立規則以擷取自訂事件（選用） {#capture-custom-events}

使用規則編輯器，針對適用性表單的特定欄位建立規則，以將適用性表單的Analytics資料傳送至 [!DNL Adobe Analytics].

在兩階段程式中，您可以在最適化表單的欄位上定義規則。 規則分派事件。 事件名稱會對應至AdobeLaunch中的自訂擷取事件。

若要使用適用性表單中的規則編輯器建立規則：

1. 點選欄位並選取 ![規則編輯器](/help/forms/using/assets/rule-editor-icon.svg) 來開啟規則編輯器頁面。
1. 在 [!UICONTROL 當] 區段。
1. 在 [!UICONTROL 然後] ，請選取 **[!UICONTROL 派單事件]** 從 **[!UICONTROL 選擇操作]** 下拉式清單。
1. 指定 **[!UICONTROL 類型事件名稱]** 欄位。

例如，如果出生日期早於特定日期，AEM Forms會將 **安全性** 事件。

![分派事件](/help/forms/using/assets/security-event.png)

將事件對應至 [!DNL Adobe Analytics]:

1. [建立規則](#configure-rules).

1. 在 **[!UICONTROL 事件]** 區段，點選 **[!UICONTROL 新增]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為擴充功能名稱。

1. 選擇 **[!UICONTROL 擷取自訂事件]** 從 **[!UICONTROL 事件類型]** 下拉式清單。

1. 使用規則編輯器建立規則時，指定您在步驟4中指定的事件名稱。

1. 點選 **保留變更** 並執行 [設定規則](#configure-rules).

## 3.設定並檢視 [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

設定最適化表單以傳送事件資料至 [!DNL Adobe Analytics]，您可以開始在 [!DNL Adobe Analytics]:

1. 點選 ![選擇產品](/help/forms/using/assets/select-analytics.png) 選取 **[!UICONTROL Analytics]**.

1. 點選 **[!UICONTROL 建立專案]** 選取 **[!UICONTROL 空白專案]**.

1. 從自由格式右上角的下拉式清單中選取報表套裝名稱。

1. 指定 **表單標題** 在 **[!UICONTROL 搜尋維度項目]** 文本，查看所有表單標題。

1. 將最適化表單標題拖曳至 **[!UICONTROL 將區段拖曳至此（或任何其他元件）]** 框。

1. 從 **[!UICONTROL 量度]** 區段中，將要追蹤的事件拖放至 **[!UICONTROL 將量度拖曳到此處（或任何其他元件）]** 框。

1. 點選 ![視覺效果](/help/forms/using/assets/visualization-icon.svg) 並將圖表類型拖放至「自由格式」區段。 同樣地，您也可以新增多個圖表類型至自由格式區段。

1. 點選Ctrl + S鍵並指定名稱以儲存專案。

如需檢視表單分析報表的詳細資訊，請參閱 [檢視及了解AEM Forms分析報表](../../forms/using/view-understand-aem-forms-analytics-reports.md).
