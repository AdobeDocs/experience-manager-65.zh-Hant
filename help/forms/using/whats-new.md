---
title: 新功能摘要 | AEM 6.5Forms
seo-title: New features summary | AEM 6.5 Forms
description: 世界上最先進的數字型驗管理解決方案的最新功能和對表單和文檔的改進。
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# 新功能摘要 | AEM 6.5Forms{#new-features-summary-aem-forms}

## 事務處理報表 {#transaction-reports}

事務處理報表允許您捕獲和跟蹤已提交表單、已處理文檔和已呈現文檔的數量。 跟蹤這些交易的目的是對產品使用情況作出明智決策，並重新平衡硬體和軟體方面的投資。 一些事務示例包括：

* 提交自適應表單、HTML5表單或表單集
* 互動式通信的打印或網路版本的再現
* 文檔從一個檔案格式轉換到另一個檔案格式

有關配置和使用事務報表的資訊，請參閱 [事務處理報表概覽](../../forms/using/transaction-reports-overview.md)。

![示例交易記錄報表](assets/surface_transaction_reporting.png)

## 互動式通訊 {#interactive-communications}

**定義資料顯示模式**

互動式通信作者現在可以定義 [資料顯示模式](create-interactive-communication.md#datadisplaypatterns) 欄位、變數和窗體資料模型元素。 例如，日期、貨幣或電話格式。

**使用新類型的圖表**

現在可以添加 [具有多個系列的像限圖和圖表](../../forms/using/chart-component-interactive-communications.md) 到交互通信。

**對表中的列排序**

你現在可以 [對表列進行排序](../../forms/using/create-interactive-communication.md#sortcolumns) 的子菜單。 可以使用靜態文本或資料模型對象綁定和排序表列。

**在Web通道中使用新元件**

現在，您可以將Button和Separator元件添加到Web通道。 有關詳細資訊，請參見 [將按鈕元件添加到Web通道](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 和 [腹板通道中的分隔器元件](../../forms/using/create-interactive-communication.md#separatorcomponent)。

**調整元件大小的佈局模式**

您現在可以切換到 [佈局模式](../../forms/using/resize-using-layout-mode.md) 使用WYSIWYG介面調整Web通道中的元件大小。

**可用性改進**

互動式通信的作者現在可以利用各種易於使用的操作同時建立對應。 操作清單包括：

* [在打印和Web通道中執行撤消重做操作](../../forms/using/create-interactive-communication.md#undoredoactions)
* [使用@符號在文檔片段中添加變數](../../forms/using/texts-interactive-communications.md#searchvariables)
* [使用@符號在文檔片段中添加資料模型元素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [刪除或將Web通道添加到現有交互通信](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [使用拖放操作將資料源元素與欄位和變數綁定](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [在創作互動式通信時突出顯示未綁定的欄位和變數](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [對Web通道中繼承的元件執行其他操作，如複製、組或更多操作](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同步進程的改進**

在使用打印通道自動生成的Web通道佈局中有幾項改進。

![互動式通信圖表](assets/interactive-communication-charts.png)

## 最適化表單 {#adaptive-forms}

### 在自適應Forms中使用Adobe Sign基於雲的數字簽名 {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[基於雲的數字簽名](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 或遠程簽名是跨案頭、移動和Web工作的新一代數字簽名，滿足簽名者身份驗證的最高級別的合規性和保證。 你現在可以 [對自適應表單簽名](../../forms/using/working-with-adobe-sign.md) 基於雲的數字簽名。

#### 在AEM Sites單頁應用程式中嵌入自適應表單或交互通信 {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms讓你 [無縫嵌入自適應表單](../../forms/using/embed-adaptive-form-aem-sites-spa.md) 或在AEM Sites單頁應用程式(SPA)中交互通信。 嵌入式自適應表單和交互通信功能完全，用戶無需離開頁面即可填寫和提交表單。 它幫助用戶保持在網頁上其他元素的上下文中，並同時與自適應表單或交互通信進行交互。

#### 對自適應表單表的列排序 {#sort-columns-of-adaptive-form-tables}

你可以 [對自適應表單表的任意列進行排序](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) 按升序或降序排列。 可以對具有靜態文本、資料模型對象屬性或靜態文本和資料模型對象屬性的組合的表列應用排序。

#### 將自適應Forms模板的可用性限制為特定路徑 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

自適應表單增加了對cq:allowedPaths屬性的支援。 屬性 [將自適應Forms模板的可用性限制為特定路徑](creating-adaptive-form.md#adaptive-form-templates)。

#### 將複選框動態添加到自適應表單 {#add-check-boxes-to-the-adaptive-form-dynamically}

現在，您可以定義規則 [將複選框動態添加到Adaptive Form](../../forms/using/rule-editor.md#setpropertyrule) 基於自定義函式、表單對象或對象屬性。

## AEM 工作流程 {#aem-workflows}

### 在工作流中使AEM用變數 {#use-variables-in-aem-workflows}

變數允許工作流步驟在運行時保留和傳遞跨工作流步驟的元資料。 您可以建立不同類型的變數來儲存不同類型的資料。 例如，整數、字串、文檔或表單資料模型實例。 通常，當需要根據變數所包含的值做出決策或儲存在以後流程中需要的資訊時，您會使用變數或變數集合。

變數是 [元資料映射](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 介面在早期版本中可用。 它有助於節省在開發用於檢索和更新元資料值的自定義ECMAScript代碼時花費的時間。 繼續使用MetaDataMap介面和ECMAScript代碼來處理元資料。 將變數用於MetaDataMap和ECMAScript的一些好處是：

* 動態儲存、更新和使用儲存在整個工作流中的變數中的值，而不依賴於自定義代碼
* 將值直接檢索並更新到已提交表單的表單資料模型和資料檔案(XML/JSON)
* 將完整文檔儲存在變數中以執行文檔處理

「轉至」(Go To)步驟、「或分解」(OR Split)步驟和所有AEM Forms工作流步驟都支援變數。 可以使用MetaDataMap介面訪問工作流步驟中不支援變數的變數。 有關詳細資訊，請參見 [工作流中的AEM變數](../../forms/using/variable-in-aem-workflows.md)。

![在工作流中設定變數](assets/variable.png)

#### 使用具有不同自適應Forms的工作流  {#use-a-workflow-with-different-adaptive-forms}

你可以 [為分配任務指定自適應表單](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) 以及運行時上以表單為中心的工作流的記錄步驟文檔。 它允許工作流與不同的自適應Forms一起工作。 在設計工作流時，可以決定選擇「自適應表單」的方法。 「自適應表單」可以位於絕對路徑上，作為有效負載提交到工作流，或在使用變數計算的路徑上可用。

#### 使用以表單為中心的工作流步驟的增強日誌記錄功能 {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

以表單為中心的工作流步驟的日誌記錄功能已標準化。 現在，所有以表單為中心的工作流步驟都會生成類似的標準化日誌。 有助於提高調試速度。

## 資料整合 {#data-integration}

您現在可以：

* [驗證輸入資料](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 基於約束清單。 它有助於確保只將有效資料提交到資料源。
* [覆蓋預設終結點](../../forms/using/configure-data-sources.md#configure-soap-web-services) 在WSDL（Web服務描述語言）檔案中定義。

* [覆蓋預設值](../../forms/using/configure-data-sources.md#configure-restful-web-services) [方案、主機和基路徑](../../forms/using/configure-data-sources.md#configure-restful-web-services) 定義。

## 平台和安全更新 {#platform-and-security-updates}

### 主要平台更新 {#major-platform-updates}

AEM Forms可以使用支援的作業系統、應用程式伺服器、資料庫、資料庫驅動程式、JDK、LDAP伺服器和電子郵件伺服器的任意組合進行設定。 以下為於2014年12月31日 [支援的平台](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Component</td>
   <td>已刪除支援</td>
  </tr>
  <tr>
   <td>作業系統</td>
   <td>
    <ul>
     <li>MicrosoftWindows Server 2012 R2</li>
     <li>IBMAIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>應用程式伺服器<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty配置檔案</li>
    <li>OracleWebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>資料庫</td>
   <td>
    <ul>
     <li>IBMDB2 <br /> </li>
     <li>OracleRAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP伺服器</td>
   <td>
    <ul>
     <li>Microsoft2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM蓮達樂8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>電子郵件伺服器</td>
   <td>
    <ul>
     <li>IBM蓮達樂8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>連接器</td>
   <td>
    <ul>
     <li>MicrosoftSharepoint 2013連接器</li>
     <li>EMC Documentum 7.0連接器</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms應用<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1支援</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>爪哇11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; 聯繫Adobe支援，瞭解有關遷移到其他平台的資訊

#### 新的基於HTML5的UI {#new-html-based-uis}

按照計畫的AdobeFlash PlayerEOL和將基於Flash的內容遷移到開放標準的總體方向，AEM 6.5Forms用基於的UI取代了HTMLJEE管理控制台上基於Flash的健康監視器、流程管理、Reader擴展和類別管理用戶介面。

#### 安全性改進 {#security-improvements}

* AEM6.5Forms在JEE管理控制台UI上現在基於Apache Struts 2.5。
* AEM6.5Forms現在將jQuery用於3.2.1和jQuery UI 1.12.1。看， [升級文檔](/help/forms/home.md) 改變的影響。

#### 輔助功能改進 {#accessibility-improvements}

6.AEM5Forms改善了AEM Forms工作區的無障礙性。
