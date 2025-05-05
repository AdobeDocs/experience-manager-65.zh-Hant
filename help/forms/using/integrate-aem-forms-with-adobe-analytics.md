---
title: 如何將AEM Forms與Adobe Analytics整合？
description: AEM Forms與Adobe Analytics整合，以擷取及追蹤您已發佈表單的績效量度。
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
feature: Adaptive Forms
source-git-commit: 38e3439b5b9f3b4bc56bb1618d33e570ca0603f5
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---

# 使用[!DNL Adobe Launch]的Analytics {#analyticsusingadobelaunch}

AEM Forms與[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=zh-Hant)整合，可讓您擷取及追蹤已發佈表單的績效量度。 分析這些量度是為了讓業務使用者深入瞭解一般使用者行為，並最佳化資料擷取體驗。 您可以透過Adobe Analytics for Adaptive Forms擷取及追蹤已登入和未登入（匿名）使用者的行為。

您也可以使用Cloud Service框架執行分析。 如需如何將AEM Forms與Cloud Service架構整合的詳細資訊，請參閱[使用Cloud Service架構的分析](/help/forms/using/configure-analytics-forms-documents.md)。 與使用Analytics架構的Analytics相比，使用Adobe Cloud Service Launch的主要優點在於，除了這些現成可用的事件之外，您還可以定義自訂事件。 自訂事件是使用規則編輯器或客戶clientlibs定義，並對應至[!DNL Adobe Analytics]中的事件。

執行本文所述的動作後，您可以在[!DNL Adobe Analytics]中設定並檢視報表，如下列影片所示：

>[!VIDEO](https://video.tv.adobe.com/v/337262)

您可以使用[!DNL Adobe Analytics]來探索使用者在使用最適化表單時遇到的互動模式和問題。 [!DNL Adobe Analytics]開箱即用地追蹤並儲存下列事件的相關資訊：

* **轉譯**：表單開啟的次數。

* **提交**：提交表單的次數。

* **放棄**：使用者未完成表單就離開的次數。

* **錯誤**：在面板和面板的欄位上遇到的錯誤數。

* **說明**：使用者開啟面板說明及面板欄位的次數。

* **欄位造訪**：使用者造訪表單中欄位的次數。

* **儲存**：使用者將表單儲存至Forms入口網站的次數。

除了這些立即可用的事件以外，您也可以定義自訂事件。

下圖說明在[!DNL Adobe Analytics]中檢視報表之前需要執行的動作：

![Analytics概觀](/help/forms/using/assets/analyticsworkflow.png)

## 1.設定[!DNL Adobe Analytics] {#Configure-adobe-analytics}

在設定[!DNL Adobe Analytics]之前，請建立：

* 要登入[Adobe Experience Cloud](https://experience.adobe.com/#/home)的Adobe ID。
* [報告套裝](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=zh-Hant)。


### 安裝AEM Forms和[!DNL Adobe Analytics]擴充功能 {#install-extensions}

執行以下步驟來設定AEM Forms和[Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hant)擴充功能：

1. 登入Adobe Experience Cloud並為公司選取適當的名稱。

1. 選取&#x200B;**[!UICONTROL 啟動/資料彙集]**&#x200B;並選取&#x200B;**[!UICONTROL 移至啟動/資料彙集]**。

1. 選取&#x200B;**[!UICONTROL 新增屬性]**&#x200B;並指定組態的名稱。

1. 指定網域名稱並選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存屬性。

1. 選取標籤屬性清單中可用的設定名稱。

1. 在&#x200B;**[!UICONTROL 編寫]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 擴充功能]**。

1. 選取&#x200B;**[!UICONTROL 目錄]**，並針對&#x200B;**[!UICONTROL Adobe Experience Manager Forms]**&#x200B;擴充功能選取&#x200B;**[!UICONTROL 安裝]**。 **[!UICONTROL Adobe Experience Manager Forms]**&#x200B;會顯示在&#x200B;**已安裝**&#x200B;索引標籤中可用的已安裝擴充功能清單中。

1. 選取&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;擴充功能的&#x200B;**[!UICONTROL 安裝]**。
1. 在&#x200B;**[!UICONTROL 開發報表套裝]**、**[!UICONTROL 測試報表套裝]**&#x200B;和&#x200B;**[!UICONTROL 產品報表套裝]**&#x200B;下拉式清單中選取報表套裝名稱，並選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存擴充功能。

### 設定資料元素 {#configure-data-elements}

您可以在為事件建立的規則中，選取任何已設定的資料元素。 當最適化表單上發生事件時，AEM Forms會將這些資料元素傳送至[!DNL Adobe Analytics]。

安裝&#x200B;**[!UICONTROL Adobe Experience Manager Forms]**&#x200B;擴充功能後，您可以建立下列資料元素：

<table>
 <tbody>
  <tr>
   <td>欄位名稱</th>
   <td>欄位標題</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>表單名稱<br /> </td>
   <td>FormTitle<br /> </td>
   <td>頁面名稱</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>逗留時間</td>
  </tr>
 </tbody>
</table>

執行以下步驟來設定資料元素：

1. 在&#x200B;**[!UICONTROL 製作]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 資料元素]**。

1. 選取&#x200B;**[!UICONTROL 建立新資料元素]**。

1. 指定資料元素的名稱。 例如，FormTitle資料元素型別的表單標題。

1. 指定&#x200B;**[!UICONTROL Adobe Experience Manager Forms]**&#x200B;作為擴充功能名稱。

1. 選取&#x200B;**[!UICONTROL 資料元素型別]**。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存資料元素。

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 設定規則 {#configure-rules}

執行以下步驟，根據&#x200B;**[!UICONTROL Adobe Experience Manager Forms]**&#x200B;擴充功能建立規則：

1. 在&#x200B;**[!UICONTROL 製作]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 規則]**。

1. 選取&#x200B;**[!UICONTROL 建立新規則]**。

1. 指定規則的名稱。 例如，表單提交以記錄表單提交。

1. 在&#x200B;**[!UICONTROL 事件]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 新增]**。

1. 指定&#x200B;**[!UICONTROL Adobe Experience Manager Forms]**&#x200B;作為擴充功能名稱。

1. 選取事件型別。 **[!UICONTROL Name]**&#x200B;欄位的輸入會根據選取的事件型別自動填入。

1. 選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以儲存事件。

1. 在&#x200B;**[!UICONTROL 動作]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 新增]**。

1. 指定&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;作為擴充功能名稱。

1. 選取&#x200B;**[!UICONTROL 設定變數]**&#x200B;作為動作型別。 下拉式清單中可用的選項包括：

   * **[!UICONTROL 設定變數]**：使用此動作型別來定義從AEM Forms傳送所選資料元素給[!DNL Adobe Analytics]的事件型別。

   * **[!UICONTROL 傳送信標]**：使用此動作型別從AEM Forms傳送資料給[!DNL Adobe Analytics]。

   * **[!UICONTROL 清除變數]**：使用此動作型別來清除資料追蹤，讓事件在[!DNL Adobe Analytics]中僅註冊一次。

     建議的方法是使用&#x200B;**[!UICONTROL 設定變數]**&#x200B;動作型別來設定事件和資料元素，然後使用&#x200B;**[!UICONTROL 傳送信標]**&#x200B;來傳送資料，再使用&#x200B;**[!UICONTROL 清除變數]**&#x200B;來清除資料追蹤。

1. 在&#x200B;**[!UICONTROL Props]**&#x200B;區段中，將下拉式清單中可用的報表套裝選項與使用[設定資料元素](#configure-data-elements)定義的資料元素對應。

   例如，若要在您提交表單時從AEM Forms將&#x200B;**表單標題**&#x200B;資料元素傳送至[!DNL Adobe Analytics]：
   1. 在&#x200B;**[!UICONTROL Props]**&#x200B;區段中，選取報表套裝中可用表單標題的prop，然後選取![資料庫圖示](/help/forms/using/assets/database-icon.svg)，將其對應至在[設定資料元素](#configure-data-elements)中建立的表單標題。

      ![define-props](/help/forms/using/assets/define-props.png)

   1. 選取「**[!UICONTROL 新增其他]**」以新增更多資料元素至清單。

1. 在&#x200B;**[!UICONTROL 事件]**&#x200B;區段中，從報表套裝中可用的選項中選取事件，並選取&#x200B;**[!UICONTROL 保留變更]**。

1. 在&#x200B;**[!UICONTROL 動作]**&#x200B;區段中，選取+並指定&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;作為擴充功能名稱。

1. 選取&#x200B;**[!UICONTROL 傳送信標]**&#x200B;作為動作型別。 在右窗格中，選取&#x200B;**[!UICONTROL s.t()]**&#x200B;將資料傳送至[!DNL Adobe Analytics]並將它視為頁面檢視，或選取&#x200B;**[!UICONTROL s.tl()]**&#x200B;將資料傳送至[!DNL Adobe Analytics]，而不將其視為頁面檢視。 選取&#x200B;**[!UICONTROL 保留變更]**。

1. 在&#x200B;**[!UICONTROL 動作]**&#x200B;區段中，選取+並指定&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;作為擴充功能名稱。

1. 選取&#x200B;**[!UICONTROL 清除變數]**&#x200B;作為動作型別。 選取&#x200B;**[!UICONTROL 保留變更]**。 執行這些步驟後，**[!UICONTROL 動作]**&#x200B;區段顯示為：
   ![動作設定](/help/forms/using/assets/actions-config.png)

   根據您的需求自訂&#x200B;**[!UICONTROL 動作]**&#x200B;區段。 例如，您可以在「動作」流程中定義兩個&#x200B;**傳送信標**&#x200B;步驟，將資料傳送至[!DNL Adobe Analytics]，並在一個步驟中將它視為頁面檢視，將資料傳送至[!DNL Adobe Analytics]，並在第二個步驟中不要將其視為頁面檢視。

   ![動作設定](/help/forms/using/assets/actions-config-2.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存規則。

   您可以為所有事件型別建立規則，例如「放棄」、「錯誤」、「欄位瀏覽」、「說明」、「呈現」、「儲存」和「提交」。

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Publish流程 {#publish-flow}

在建立資料元素並在規則中使用它們之後，發佈設定以在[!DNL Adobe Analytics]中收集表單資料。

執行以下步驟以發佈設定：

1. 在&#x200B;**[!UICONTROL 發佈]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 發佈流程]**。

1. 選取&#x200B;**[!UICONTROL 新增程式庫]**&#x200B;並指定名稱及選取程式庫的環境。

1. 選取&#x200B;**[!UICONTROL 新增所有變更的資源]**，然後選取&#x200B;**[!UICONTROL 儲存並建置至開發]**。

1. 在&#x200B;**[!UICONTROL 開發]**&#x200B;區段中，選取![更多選項](/help/forms/using/assets/more-options-icon.svg)，然後選取&#x200B;**[!UICONTROL 核准並讓Publish投入生產]**。

1. 確認變更，發佈流程將很快顯示在&#x200B;**[!UICONTROL 已發佈]**&#x200B;區段中。

![Publish流程](/help/forms/using/assets/publish-flow.png)

## 2.設定AEM Forms {#configure-aem-forms}

在建立Adobe Launch設定之前，請先使用Adobe Launch做為雲端解決方案來建立[Adobe IMS設定](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=zh-Hant)。

### 建立 Adobe Launch 設定 {#create-adobe-launch-configuration}

執行以下步驟來建立Adobe Launch設定：

1. 在AEM Forms作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe啟動設定]**。

1. 選取資料夾以建立組態，並選取&#x200B;**[!UICONTROL 建立]**。

1. 在&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中指定組態的標題。

1. 選取[關聯的Adobe IMS設定](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=zh-Hant)。

1. 選取在[設定Adobe Analytics](#Configure-adobe-analytics)時使用的公司名稱。

1. 選取在[設定Adobe Analytics](#install-extensions)時所建立之屬性的名稱。

1. 選取「**[!UICONTROL 儲存並關閉]**」。

1. Publish設定。

>[!NOTE]
>
> 當您[將AEM Forms內嵌於AEM Sites頁面](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites)時，最適化表單的iFrame中不支援Adobe Launch設定。 若要解決此問題，請直接在Sites頁面上設定Adobe啟動規則，或將現有Adobe啟動設定從AEM Forms移轉至Sites頁面。


### 為最適化表單啟用[!DNL Adobe Analytics] {#enable-analytics-adaptive-form}

若要在現有的最適化表單中使用[!DNL Adobe Launch]設定：

1. 在AEM Forms Author執行個體上，瀏覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**。
1. 選取最適化表單並選取&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，選取建立Adobe啟動設定時所使用的[設定容器](#create-adobe-launch-configuration)。
1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**。 已為[!DNL Adobe Analytics]啟用最適化表單。
1. Publish表單。

為最適化表單啟用[!DNL Adobe Analytics]後，如果AEM Forms和[!DNL Adobe Analytics]之間有適當的資料事件流程，您可以[驗證](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=zh-Hant#validate-the-page-view-beacon)。 AEM Forms與Adobe Analytics的整合已完成。 您現在可以[在Adobe Analytics](#view-reports-adobe-analytics)中設定和檢視報告。

>[!NOTE]
>如果同時啟用使用Cloud Service架構[&#128279;](/help/forms/using/configure-analytics-forms-documents.md)的分析以及使用Adobe啟動項&#x200B;**功能的**&#x200B;分析，則使用Adobe啟動項&#x200B;**的**&#x200B;分析將會取得優先權。
> 

### 建立規則以擷取自訂事件（選用） {#capture-custom-events}

使用規則編輯器在最適化表單的特定欄位上建立規則，以將最適化表單中的Analytics資料傳送至[!DNL Adobe Analytics]。

在兩階段程式中，您會在最適化表單的欄位上定義規則。 規則會傳送事件。 事件名稱會對應至Adobe Launch中的自訂擷取事件。

若要在最適化表單中使用規則編輯器建立規則：

1. 選取欄位並選取![規則編輯器](/help/forms/using/assets/rule-editor-icon.svg)以開啟規則編輯器頁面。
1. 在規則的[!UICONTROL When]區段中定義條件。
1. 在規則的[!UICONTROL Then]區段中，從&#x200B;**[!UICONTROL 選取動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 分派事件]**。
1. 在&#x200B;**[!UICONTROL 輸入事件名稱]**&#x200B;欄位中指定事件的名稱。

例如，如果出生日期在某個日期之前，AEM Forms會傳送&#x200B;**安全性**&#x200B;事件。

![分派事件](/help/forms/using/assets/security-event.png)

若要將事件對應至[!DNL Adobe Analytics]中的自訂擷取事件：

1. [建立規則](#configure-rules)。

1. 在&#x200B;**[!UICONTROL 事件]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 新增]**。

1. 指定&#x200B;**[!UICONTROL Adobe Experience Manager Forms]**&#x200B;作為擴充功能名稱。

1. 從&#x200B;**[!UICONTROL 事件型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 擷取自訂事件]**。

1. 使用規則編輯器建立規則時，請指定您在步驟4中指定的事件名稱。

1. 選取&#x200B;**保留變更**&#x200B;並執行[設定規則](#configure-rules)中指定的其餘動作。

## 3.在[!DNL Adobe Analytics]中設定並檢視報表 {#view-reports-adobe-analytics}

設定最適化表單以傳送事件資料至[!DNL Adobe Analytics]後，您就可以在[!DNL Adobe Analytics]中開始檢視報表：

1. 選取![選取產品](/help/forms/using/assets/select-analytics.png)並選取&#x200B;**[!UICONTROL Analytics]**。

1. 選取&#x200B;**[!UICONTROL 建立專案]**&#x200B;並選取&#x200B;**[!UICONTROL 空白專案]**。

1. 從自由表格右上角的下拉式清單中選取報表套裝名稱。

1. 在&#x200B;**[!UICONTROL 搜尋維度專案]**&#x200B;文字中指定&#x200B;**表單標題**&#x200B;以檢視所有表單標題。

1. 將最適化表單標題拖放到&#x200B;**[!UICONTROL 將區段拖放到這裡（或任何其他元件）]**&#x200B;文字方塊。

1. 從&#x200B;**[!UICONTROL Metrics]**&#x200B;區段，將要追蹤的事件拖曳到&#x200B;**[!UICONTROL 將量度拖曳到這裡（或任何其他元件）]**&#x200B;文字方塊。

1. 選取「![視覺效果](/help/forms/using/assets/visualization-icon.svg)」，並將圖表型別拖放至「自由格式」區段。 同樣地，您可以將多個圖表型別新增至自由格式區段。

1. 選取Ctrl + S鍵，並指定名稱以儲存專案。

如需有關檢視表單分析報表的詳細資訊，請參閱[檢視和瞭解AEM Forms分析報表](../../forms/using/view-understand-aem-forms-analytics-reports.md)。
