---
title: 新功能摘要 | AEM 6.5 Forms
description: 全球最進階數位體驗管理解決方案的表單與檔案的最新功能與改良。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 1%

---

# 新功能摘要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## 交易報告 {#transaction-reports}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/latest-innovations.html) |
| AEM 6.5 | 本文章 |


交易報表可讓您擷取及追蹤已提交表單、已處理檔案及已轉譯檔案的數量。 追蹤這些交易的目的是，針對產品使用狀況做出明智的決策，並重新平衡軟硬體投資。 交易的一些範例包括：

* 提交最適化表單、HTML5表單或表單集
* 互動式通訊的列印或網頁版本轉譯
* 將檔案從一種檔案格式轉換為另一種檔案格式

有關設定和使用交易報表的資訊，請參閱 [交易報表概觀](../../forms/using/transaction-reports-overview.md).

![範例交易報告](assets/surface_transaction_reporting.png)

## 互動式通訊 {#interactive-communications}

**定義資料顯示模式**

互動式通訊作者現在可以定義 [資料顯示模式](create-interactive-communication.md#datadisplaypatterns) 適用於欄位、變數和表單資料模型元素。 例如日期、貨幣或電話格式。

**使用新型別的圖表**

您現在可以新增 [象限圖表和含有多個數列的圖表](../../forms/using/chart-component-interactive-communications.md) 至互動式通訊。

**排序表格中的欄**

您現在可以 [排序表格的欄](../../forms/using/create-interactive-communication.md#sortcolumns) 在互動式通訊中。 您可以使用靜態文字或資料模型物件來繫結及排序表格欄。

**在Web Channel中使用新元件**

您現在可以新增Button和Separator元件至Web Channel。 如需詳細資訊，請參閱 [新增Button元件至Web Channel](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 和 [Web Channel中的分隔符號元件](../../forms/using/create-interactive-communication.md#separatorcomponent).

**調整元件大小的佈局模式**

您現在可以切換至 [版面模式](../../forms/using/resize-using-layout-mode.md) 使用WYSIWYG介面調整Web channel中元件的大小。

**可用性改善**

互動式通訊作者現在可利用各種簡單易用的操作，同時建立對應。 操作清單包括：

* [在列印和Web通道中執行復原/重做動作](../../forms/using/create-interactive-communication.md#undoredoactions)
* [使用@符號在檔案片段中新增變數](../../forms/using/texts-interactive-communications.md#searchvariables)
* [使用@符號在檔案片段中新增資料模型元素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [刪除或新增Web Channel至現有的互動式通訊](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [使用拖放動作將資料來源元素與欄位和變數繫結](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [編寫互動式通訊時反白未繫結的欄位和變數](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [在Web Channel中對繼承的元件執行其他動作，例如複製、群組等等](../../forms/using/create-interactive-communication.md#componenttoolbar)

**改善同步程式**

使用Print channel自動產生的Web channel版面配置有幾項改進。

![互動式通訊圖表](assets/interactive-communication-charts.png)

## 最適化表單 {#adaptive-forms}

### 在最適化Forms中使用Adobe Sign的雲端型數位簽名 {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[雲端數位簽名](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 或遠端簽名是新一代的數位簽名，可在案頭、行動裝置和Web上運作，並符合簽名者驗證的最高規範與保證。 您現在可以 [簽署最適化表單](../../forms/using/working-with-adobe-sign.md) 雲端數位簽名。

#### 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊 {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms可讓您 [順暢地內嵌最適化表單](../../forms/using/embed-adaptive-form-aem-sites-spa.md) 或AEM Sites單頁應用程式(SPA)中的互動式通訊。 內嵌的最適化表單和互動式通訊功能齊全，使用者無需離開頁面即可填寫和提交表單。 它有助於使用者停留在網頁上其他元素的內容中，同時與最適化表單或互動式通訊互動。

#### 排序最適化表單的欄 {#sort-columns-of-adaptive-form-tables}

您可以 [排序最適化表單表格的任何欄](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) 以遞增或遞減順序顯示。 您可以將排序套用至具有靜態文字、資料模型物件屬性或靜態文字與資料模型物件屬性組合的表格欄。

#### 限制特定路徑可使用最適化Forms範本 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

調適型表單已新增對cq：allowedPaths屬性的支援。 屬性 [將最適化Forms範本的可用性限制在特定路徑](creating-adaptive-form.md#adaptive-form-templates).

#### 動態新增核取方塊至最適化表單 {#add-check-boxes-to-the-adaptive-form-dynamically}

您現在可以將規則定義為 [動態新增核取方塊至最適化表單](../../forms/using/rule-editor.md#setpropertyrule) 根據自訂函式、表單物件或物件屬性。

## AEM 工作流程 {#aem-workflows}

### 在AEM工作流程中使用變數 {#use-variables-in-aem-workflows}

變數可讓工作流程步驟在執行階段跨工作流程步驟保留和傳遞中繼資料。 您可以建立不同型別的變數來儲存不同型別的資料。 例如，整數、字串、檔案或表單資料模型例項。 通常情況下，當您需要根據變數或變數集合持有的值來做出決定，或儲存您稍後在程式中需要的資訊時，會使用變數或變數集合。

變數是 [中繼資料地圖](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 舊版中可用的介面。 這有助於節省開發自訂ECMAScript程式碼以擷取和更新中繼資料值的時間。 您繼續使用MetaDataMap介面和ECMAScript程式碼來操作中繼資料。 在MetaDataMap和ECMAScript上使用變數的一些優點包括：

* 可在整個工作流程中以動態方式儲存、更新及使用儲存在變數中的值，不需依賴自訂程式碼
* 擷取值並直接更新至表單資料模型和已提交表單的資料檔案(XML/JSON)
* 將完整檔案儲存在變數中，以執行檔案處理

「跳至」步驟、 「OR分割」步驟以及所有AEM Forms工作流程步驟都支援變數。 您可以使用MetaDataMap介面來存取工作流程步驟中無變數原生支援的變數。 如需詳細資訊，請參閱 [AEM工作流程中的變數](../../forms/using/variable-in-aem-workflows.md).

![在工作流程中為設定變數](assets/variable.png)

#### 搭配其他最適化Forms使用工作流程  {#use-a-workflow-with-different-adaptive-forms}

您可以 [為指派工作指定最適化表單](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) 以及執行階段表單中心工作流程的記錄檔案步驟。 它讓工作流程可搭配不同的最適化Forms運作。 您可以在設計工作流程時，決定選取最適化表單的方法。 最適化表單可位於絕對路徑下、作為裝載提交至工作流程，或位於使用變數計算的路徑。

#### 使用以表單為中心的工作流程步驟的增強記錄功能 {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

以表單為中心的工作流程步驟的記錄功能已標準化。 現在，所有以表單為中心的工作流程步驟都會產生類似的標準化記錄。 這有助於改善偵錯速度。

## 資料整合 {#data-integration}

您現在可以：

* [驗證輸入資料](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 根據限制清單。 它有助於確保只將有效資料提交給資料來源。
* [覆寫預設端點](../../forms/using/configure-data-sources.md#configure-soap-web-services) 在WSDL （Web服務描述語言）檔案中定義。

* [覆寫預設值](../../forms/using/configure-data-sources.md#configure-restful-web-services) [配置、主機和基本路徑](../../forms/using/configure-data-sources.md#configure-restful-web-services) 定義於Swagger定義檔案中。

## 平台與安全性更新 {#platform-and-security-updates}

### 主要平台更新 {#major-platform-updates}

AEM Forms可透過支援的作業系統、應用程式伺服器、資料庫、資料庫驅動程式、JDK、LDAP伺服器和電子郵件伺服器的任意組合進行設定。 以下為中的主要變更 [支援平台](../../forms/using/aem-forms-jee-supported-platforms.md)：

<table>
 <tbody>
  <tr>
   <td>元件</td>
   <td>已移除支援</td>
  </tr>
  <tr>
   <td>作業系統</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>應用程式伺服器<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty設定檔</li>
    <li>oracleWebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>資料庫</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>ORACLERAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP伺服器</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>電子郵件伺服器</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>聯結器</td>
   <td>
    <ul>
     <li>Microsoft Sharepoint 2013聯結器</li>
     <li>EMC Documentum 7.0聯結器</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms應用程式<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1支援</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; 如需移轉至其他平台的相關資訊，請聯絡Adobe支援

#### 全新HTML5型UI {#new-html-based-uis}

為了遵循AdobeFlash Player的規劃EOL以及將Flash型內容移轉至開放標準的整體方向，AEM 6.5 Forms已在JEE Administration Console上以HTML5型UI取代AEM Forms的Flash型健全監控、程式管理、Reader延伸模組以及類別管理UI。

#### 安全性改善 {#security-improvements}

* JEE管理主控台UI上的AEM 6.5 Forms現在以Apache Struts 2.5為基礎。
* AEM 6.5 Forms現在使用jQuery to 3.2.1和jQuery UI 1.12.1。請參閱， [升級檔案](/help/forms/home.md) 以瞭解變更的影響。

#### 改善協助工具 {#accessibility-improvements}

AEM 6.5 Forms已改善AEM Forms Workspace的協助工具。
