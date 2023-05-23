---
title: 如何把AEM Forms與Adobe Analytics整合起來？
description: AEM Forms與Adobe Analytics整合，以捕獲和跟蹤已發佈表單的效能指標。
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
source-git-commit: 45ca98ffb68e1e31e2f45f352e86f5aa1b6f0f00
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# 分析使用 [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms整合 [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) 以便您捕獲和跟蹤已發佈表單的效能度量。 分析這些指標的目的是使業務用戶能夠洞察最終用戶的行為，並優化資料捕獲體驗。 您可以通過Adobe Analytics為Adaptive Forms捕獲和跟蹤已登錄和未登錄（匿名）用戶的行為。

您還可以使用Cloud Service框架執行分析。 有關如何將AEM Forms與Cloud Service框架整合的詳細資訊，請參見 [使用Cloud Service框架的分析](/help/forms/using/configure-analytics-forms-documents.md)。 通過使用Adobe框架使用Cloud Service啟動在分析之上的主要優勢是，除了這些現成的事件外，您還可以定義自定義事件。 自定義事件是使用規則編輯器或客戶客戶端定義的，並映射到中的事件 [!DNL Adobe Analytics]。

執行本文中提到的操作後，可以在中配置和查看報告 [!DNL Adobe Analytics]，如以下視頻所示：

>[!VIDEO](https://video.tv.adobe.com/v/337262)

您可以使用 [!DNL Adobe Analytics] 發現用戶在使用自適應表單時遇到的交互模式和問題。 出局了， [!DNL Adobe Analytics] 跟蹤並儲存有關以下事件的資訊：

* **呈現**:開啟窗體的次數。

* **提交**:提交表單的次數。

* **放棄**:用戶在未完成表單的情況下離開的次數。

* **錯誤**:在面板和面板欄位上遇到的錯誤數。

* **幫助**:用戶開啟面板幫助和面板欄位的次數。

* **現場訪問**:用戶訪問表單中欄位的次數。

* **保存**:用戶將表單保存到Forms門戶的次數。

除了這些現成的事件外，您還可以定義自定義事件。

下圖說明了在查看報告之前需要執行的操作 [!DNL Adobe Analytics]:

![分析概述](/help/forms/using/assets/analyticsworkflow.png)

## 1。配置 [!DNL Adobe Analytics] {#Configure-adobe-analytics}

配置前 [!DNL Adobe Analytics]，建立：

* 要登錄的Adobe ID [Adobe Experience Cloud](https://experience.adobe.com/#/home)。
* A [報告套件](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html)。


### 安裝AEM Forms和 [!DNL Adobe Analytics] 擴展 {#install-extensions}

執行以下步驟來配置AEM Forms和 [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) 擴展：

1. 登錄Adobe Experience Cloud，為公司選擇適當的名稱。

1. 點擊 **[!UICONTROL 啟動/資料收集]** 點擊 **[!UICONTROL 轉到啟動/資料收集]**。

1. 點擊 **[!UICONTROL 新建屬性]** 並指定配置的名稱。

1. 指定域名並點擊 **[!UICONTROL 保存]** 的子菜單。

1. 按一下「Tag Properties（標籤屬性）」清單中可用的配置名稱。

1. 在 **[!UICONTROL 創作]** 部分，點擊 **[!UICONTROL 擴展]**。

1. 點擊 **[!UICONTROL 目錄]** 點擊 **[!UICONTROL 安裝]** 為 **[!UICONTROL Adobe Experience Manager Forms]** 擴展。 **[!UICONTROL Adobe Experience Manager Forms]** 顯示在 **已安裝** 頁籤。

1. 點擊 **[!UICONTROL 安裝]** 為 **[!UICONTROL Adobe Analytics]** 擴展。
1. 在 **[!UICONTROL 開發報告套件]**。 **[!UICONTROL 暫存報表套件]**, **[!UICONTROL 產品報告套件]** 下拉清單並點擊 **[!UICONTROL 保存]** 的子菜單。

### 配置資料元素 {#configure-data-elements}

可以在為事件建立的規則中選擇任何已配置的資料元素。 當在自適應表單上發生事件時，AEM Forms將這些資料元素發送到 [!DNL Adobe Analytics]。

安裝後 **[!UICONTROL Adobe Experience Manager Forms]** 擴展，可以建立以下資料元素：

<table>
 <tbody>
  <tr>
   <td>欄位名</th>
   <td>欄位標題</th>
   <td>窗體實例</th>
  </tr>
  <tr>
   <td>表單名稱<br /> </td>
   <td>窗體標題<br /> </td>
   <td>頁名</td>
  </tr>
  <tr>
   <td>頁面URL<br /> </td>
   <td>面板標題<br /> </td>
   <td>花費的時間</td>
  </tr>
 </tbody>
</table>

執行以下步驟來配置資料元素：

1. 在 **[!UICONTROL 創作]** 部分，點擊 **[!UICONTROL 資料元素]**。

1. 點擊 **[!UICONTROL 建立新資料元素]**。

1. 指定資料元素的名稱。 例如，FormTitle資料元素類型的Form Title。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為副檔名。

1. 選擇 **[!UICONTROL 資料元素類型]**。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 配置規則 {#configure-rules}

執行以下步驟以根據 **[!UICONTROL Adobe Experience Manager Forms]** 擴展：

1. 在 **[!UICONTROL 創作]** 部分，點擊 **[!UICONTROL 規則]**。

1. 點擊 **[!UICONTROL 建立新規則]**。

1. 指定規則的名稱。 例如，「表單提交」可記錄表單提交。

1. 在 **[!UICONTROL 事件]** 部分，點擊 **[!UICONTROL 添加]**。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為副檔名。

1. 選擇事件類型。 輸入 **[!UICONTROL 名稱]** 欄位將根據所選事件類型自動填充。

1. 點擊 **[!UICONTROL 保留更改]** 的子菜單。

1. 在 **[!UICONTROL 操作]** 部分，點擊 **[!UICONTROL 添加]**。

1. 指定 **[!UICONTROL Adobe Analytics]** 作為副檔名。

1. 選擇 **[!UICONTROL 設定變數]** 作為操作類型。 下拉清單中可用的選項包括：

   * **[!UICONTROL 設定變數]**:使用此操作類型可定義將選定資料元素從AEM Forms發送到 [!DNL Adobe Analytics]。

   * **[!UICONTROL 發送信標]**:使用此操作類型將資料從AEM Forms發送到 [!DNL Adobe Analytics]。

   * **[!UICONTROL 清除變數]**:使用此操作類型清除資料跟蹤，以便事件只在 [!DNL Adobe Analytics]。

      建議的方法是 **[!UICONTROL 設定變數]** 操作類型以配置事件和資料元素，然後使用 **[!UICONTROL 發送信標]** 發送資料，然後使用 **[!UICONTROL 清除變數]** 清除資料跟蹤。

1. 在 **[!UICONTROL 道具]** 部分，將下拉清單中可用的報告套件選項與使用 [配置資料元素](#configure-data-elements)。

   例如，要發送 **窗體標題** 從AEM Forms到 [!DNL Adobe Analytics] 提交表格時：
   1. 在 **[!UICONTROL 道具]** 選擇報表套件中可用的表單標題的屬性，然後按一下 ![資料庫表徵圖](/help/forms/using/assets/database-icon.svg) 將其映射到在中建立的窗體標題 [配置資料元素](#configure-data-elements)。

      ![定義屬性](/help/forms/using/assets/define-props.png)

   1. 點擊 **[!UICONTROL 添加其他]** 添加更多資料元素。

1. 在 **[!UICONTROL 事件]** ，從報表套件中的可用選項中選擇事件，然後按一下 **[!UICONTROL 保留更改]**。

1. 在 **[!UICONTROL 操作]** 部分，點擊+並指定 **[!UICONTROL Adobe Analytics]** 作為副檔名。

1. 選擇 **[!UICONTROL 發送信標]** 作為操作類型。 在右窗格中，選擇 **[!UICONTROL s.t()]** 要發送資料 [!DNL Adobe Analytics] 將其視為頁面視圖或 **[!UICONTROL s.tl()]** 要發送資料 [!DNL Adobe Analytics] 不要把它當作頁面視圖。 點擊 **[!UICONTROL 保留更改]**。

1. 在 **[!UICONTROL 操作]** 部分，點擊+並指定 **[!UICONTROL Adobe Analytics]** 作為副檔名。

1. 選擇 **[!UICONTROL 清除變數]** 作為操作類型。 點擊 **[!UICONTROL 保留更改]**。 執行這些步驟後， **[!UICONTROL 操作]** 部分顯示為：
   ![操作配置](/help/forms/using/assets/actions-config.png)

   自定義 **[!UICONTROL 操作]** 按您的要求。 例如，可以定義兩個 **發送信標** 操作流中將資料發送到的步驟 [!DNL Adobe Analytics] 並將其作為頁面視圖一步處理，然後將資料發送到 [!DNL Adobe Analytics] 不要將其作為第二步的頁面視圖。

   ![操作配置](/help/forms/using/assets/actions-config-2.png)

1. 點擊 **[!UICONTROL 保存]** 來保存規則。

   您可以為所有事件類型建立規則，如放棄、錯誤、現場訪問、幫助、呈現、保存和提交。

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### 發佈流 {#publish-flow}

在建立資料元素並在規則中使用它們後，發佈配置以在 [!DNL Adobe Analytics]。

執行以下步驟以發佈配置：

1. 在 **[!UICONTROL 發佈]** 部分，點擊 **[!UICONTROL 發佈流]**。

1. 點擊 **[!UICONTROL 添加庫]** 並指定名稱，然後為庫選擇環境。

1. 點擊 **[!UICONTROL 添加所有更改的資源]** 然後點擊 **[!UICONTROL 保存並構建到開發]**。

1. 在 **[!UICONTROL 開發]** 部分，點擊 ![更多選項](/help/forms/using/assets/more-options-icon.svg) 然後點擊 **[!UICONTROL 批准並發佈到生產]**。

1. 確認更改，並且發佈流很快顯示在 **[!UICONTROL 已發佈]** 的子菜單。

![發佈流](/help/forms/using/assets/publish-flow.png)

## 2.配置AEM Forms {#configure-aem-forms}

在建立Adobe啟動配置之前，請建立 [使用Adobe啟動作為雲解決方案的Adobe IMS配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html)。

### 建立 Adobe Launch 設定 {#create-adobe-launch-configuration}

執行以下步驟建立Adobe啟動配置：

1. 在AEM Forms作者實例上，導航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe啟動配置]**。

1. 選擇要建立配置的資料夾並點擊 **[!UICONTROL 建立]**。

1. 在中為配置指定標題 **[!UICONTROL 標題]** 的子菜單。

1. 選擇 [關聯的Adobe IMS配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html)。

1. 選擇當時使用的公司名稱 [配置Adobe Analytics](#Configure-adobe-analytics)。

1. 選擇在建立時建立的屬性的名稱 [配置Adobe Analytics](#install-extensions)。

1. 點擊 **[!UICONTROL 保存並關閉]**。

1. 發佈配置。

### 啟用 [!DNL Adobe Analytics] 自適應窗體 {#enable-analytics-adaptive-form}

要使用 [!DNL Adobe Launch] 在現有自適應窗體中配置：

1. 在AEM Forms作者實例上，導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇「自適應表單」並點擊 **[!UICONTROL 屬性]**。
1. 在 **[!UICONTROL 基本]** 頁籤 [配置容器](#create-adobe-launch-configuration) 建立Adobe啟動配置時使用。
1. 點擊 **[!UICONTROL 保存並關閉]**。 已為 [!DNL Adobe Analytics]。
1. 發佈窗體。

啟用後 [!DNL Adobe Analytics] 對於自適應的窗體， [驗證](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) 如果在AEM Forms和 [!DNL Adobe Analytics]。 AEM Forms與Adobe Analytics的整合已經完成。 你現在可以 [配置和查看Adobe Analytics](#view-reports-adobe-analytics)。

>[!NOTE]
>以防萬一，如果兩者 [使用Cloud Service框架的分析](/help/forms/using/configure-analytics-forms-documents.md) 和 **使用Adobe啟動的分析** 同時啟用功能， **使用Adobe啟動的分析** 會優先。

### 建立規則以捕獲自定義事件（可選） {#capture-custom-events}

使用規則編輯器在自適應表單的特定欄位上建立規則，以將分析資料從自適應表單發送到 [!DNL Adobe Analytics]。

在兩階段處理中，可以以自適應形式在欄位上定義規則。 規則派發事件。 事件名稱映射到Adobe啟動中的自定義捕獲事件。

要使用自適應表單中的規則編輯器建立規則：

1. 按一下該欄位並選擇 ![規則編輯器](/help/forms/using/assets/rule-editor-icon.svg) 開啟規則編輯器頁面。
1. 在 [!UICONTROL 當] 的子菜單。
1. 在 [!UICONTROL 然後] 選擇 **[!UICONTROL 派單事件]** 從 **[!UICONTROL 選擇操作]** 的子菜單。
1. 在中指定事件的名稱 **[!UICONTROL 鍵入事件名稱]** 的子菜單。

例如，如果出生日期早於某一日期，則AEM Forms將 **安全** 的子菜單。

![分派事件](/help/forms/using/assets/security-event.png)

將事件映射到中的自定義捕獲事件 [!DNL Adobe Analytics]:

1. [建立規則](#configure-rules).

1. 在 **[!UICONTROL 事件]** 部分，點擊 **[!UICONTROL 添加]**。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作為副檔名。

1. 選擇 **[!UICONTROL 捕獲自定義事件]** 從 **[!UICONTROL 事件類型]** 的子菜單。

1. 使用規則編輯器建立規則時，指定在步驟4中指定的事件的名稱。

1. 點擊 **保留更改** 並執行中指定的其餘操作 [配置規則](#configure-rules)。

## 3.在中配置和查看報告 [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

配置自適應表單以將事件資料發送到 [!DNL Adobe Analytics]，您可以開始在 [!DNL Adobe Analytics]:

1. 點擊 ![選擇產品](/help/forms/using/assets/select-analytics.png) 選擇 **[!UICONTROL 分析]**。

1. 點擊 **[!UICONTROL 建立項目]** 選擇 **[!UICONTROL 空白項目]**。

1. 從自由形式右上角的下拉清單中選擇報表套件名稱。

1. 指定 **窗體標題** 的 **[!UICONTROL 搜索維度項]** 的子菜單。

1. 將自適應表單標題拖放到 **[!UICONTROL 將段（或任何其他元件）拖放到此處]** 的子菜單。

1. 從 **[!UICONTROL 度量]** 部分，刪除要跟蹤的事件 **[!UICONTROL 將度量（或任何其他元件）放在此處]** 的子菜單。

1. 點擊 ![可視化](/help/forms/using/assets/visualization-icon.svg) 並將圖表類型拖放到「自由形式」節。 同樣，可向「自由形式」節添加多個圖表類型。

1. 按一下Ctrl + S鍵並指定保存項目的名稱。

有關查看表單分析報表的詳細資訊，請參閱 [查看和瞭解AEM Forms分析報告](../../forms/using/view-understand-aem-forms-analytics-reports.md)。
