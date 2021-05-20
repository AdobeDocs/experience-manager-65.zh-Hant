---
title: 新功能摘要 | AEM 6.5 Forms
seo-title: 新功能摘要 | AEM 6.5 Forms
description: 全球最先進數位體驗管理解決方案的最新功能及表單與檔案改良項目。
seo-description: 全球最先進數位體驗管理解決方案的最新功能及表單與檔案改良項目。
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# 新功能摘要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## 事務報表{#transaction-reports}

交易報表可讓您擷取及追蹤已提交的表單、已處理的檔案及已轉譯的檔案數量。 跟蹤這些交易的目標是就產品使用情況做出明智的決策，並重新平衡對硬體和軟體的投資。 交易的一些示例包括：

* 提交最適化表單、HTML5表單或表單集
* 交互通信的打印或Web版本的轉譯
* 將文檔從一個檔案格式轉換為另一個檔案格式

有關配置和使用事務報表的資訊，請參閱[事務報表概述](../../forms/using/transaction-reports-overview.md)。

![交易報表範例](assets/surface_transaction_reporting.png)

## 互動式通訊 {#interactive-communications}

**定義資料顯示模式**

互動式通訊作者現在可以為欄位、變數和表單資料模型元素定義[資料顯示模式](create-interactive-communication.md#datadisplaypatterns)。 例如日期、貨幣或電話格式。

**使用新類型的圖表**

您現在可以將[具有多個系列](../../forms/using/chart-component-interactive-communications.md)的像限圖表和圖表添加到互動式通信中。

**對表中的列進行排序**

您現在可以在互動式通訊中對表](../../forms/using/create-interactive-communication.md#sortcolumns)的列進行[排序。 可以使用靜態文本或資料模型對象綁定和排序表列。

**在Web通道中使用新元件**

您現在可以新增「按鈕」和「分隔符號」元件至Web通道。 如需詳細資訊，請參閱將按鈕元件新增至Web頻道](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel)和Web頻道](../../forms/using/create-interactive-communication.md#separatorcomponent)中的[分隔符號元件。[

**版面模式以調整元件大小**

您現在可以切換至[版面模式](../../forms/using/resize-using-layout-mode.md)，使用WYSIWYG介面調整Web通道中元件的大小。

**可用性改善**

互動式通訊作者現在可在建立對應時，運用各種簡單易用的操作。 操作清單包括：

* [在列印和網頁頻道中執行還原 — 重做動作](../../forms/using/create-interactive-communication.md#undoredoactions)
* [使用@符號在文檔片段中添加變數](../../forms/using/texts-interactive-communications.md#searchvariables)
* [使用@符號在文檔片段中添加資料模型元素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [刪除或添加Web通道到現有互動式通信](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [使用拖放動作，將資料來源元素與欄位和變數系結](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [編寫互動式通訊時反白標示未系結的欄位和變數](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [在Web通道中對繼承的元件執行其他操作，如複製、分組等](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同步程式的改善**

使用「列印」管道自動產生的Web管道版面有幾項改善。

![互動式通訊圖表](assets/interactive-communication-charts.png)

## 調適型表單 {#adaptive-forms}

### 在適用性Forms中使用Adobe Sign的雲端型數位簽名{#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[雲端數位簽](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 名或遠端簽名是新一代的數位簽名，可跨台式機、行動裝置和Web運行，並滿足最高級別的合規性和簽署者驗證保證。您現在可以使用雲端數位簽名[簽署最適化表單](../../forms/using/working-with-adobe-sign.md)。

#### 在AEM Sites單頁應用程式{#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}中內嵌最適化表單或互動式通訊

AEM Forms可讓您在AEM Sites單頁應用程式(SPA)中無縫內嵌適用性表單](../../forms/using/embed-adaptive-form-aem-sites-spa.md)或互動式通訊。 [內嵌的最適化表單和互動式通訊功能完整，使用者無需離開頁面即可填寫及提交表單。 它可協助使用者停留在網頁上的其他元素上，並同時與最適化表單或互動式通訊互動。

#### 對適用性表單表格的列排序{#sort-columns-of-adaptive-form-tables}

您可以[以升序或降序來排序適用性表單表格](../../forms/using/adaptive-forms-tables.md#sortcolumnstable)的任何欄。 可以對具有靜態文本、資料模型對象屬性或靜態文本和資料模型對象屬性的組合的表列應用排序。

#### 將適用性Forms範本的可用性限制為特定路徑{#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

適用性表單已新增對cq:allowedPaths屬性的支援。 屬性[將適用性Forms範本的可用性限制為特定路徑](creating-adaptive-form.md#adaptive-form-templates)。

#### 動態將核取方塊新增至適用性表單{#add-check-boxes-to-the-adaptive-form-dynamically}

您現在可以根據自訂函式、表單物件或物件屬性，以動態方式定義規則，將核取方塊新增至適用性表單[。](../../forms/using/rule-editor.md#setpropertyrule)

## AEM 工作流程 {#aem-workflows}

### 在AEM工作流程{#use-variables-in-aem-workflows}中使用變數

變數可讓工作流程步驟在執行階段保留並傳遞跨工作流程步驟的中繼資料。 您可以建立不同類型的變數，以儲存不同類型的資料。 例如，整數、字串、檔案或表單資料模型例項。 通常，當您需要根據變數的保留值做出決策，或儲存您之後在程式中需要的資訊時，會使用變數或變數的集合。

變數是舊版中可用的[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)介面的擴充功能。 這有助於節省開發自訂ECMAScript程式碼所花的時間，這些程式碼用於擷取和更新中繼資料值。 您可以繼續使用MetaDataMap介面和ECMAScript程式碼來操控中繼資料。 使用變數比MetaDataMap和ECMAScript更有一些好處：

* 在整個工作流程中動態儲存、更新和使用儲存在變數中的值，而不需依賴自訂程式碼
* 擷取值並直接更新至已提交表單的表單資料模型和資料檔案(XML/JSON)
* 將完整的檔案儲存在變數中，以執行檔案處理

「移至」步驟、「或」分割步驟，以及所有AEM Forms工作流程步驟都支援變數。 在沒有變數原生支援的工作流程步驟中，您可以使用MetaDataMap介面來存取變數。 如需詳細資訊，請參閱AEM工作流程中的[變數](../../forms/using/variable-in-aem-workflows.md)。

![在工作流程中為設定變數](assets/variable.png)

#### 使用具有不同適用性Forms {#use-a-workflow-with-different-adaptive-forms}的工作流程

您可以[為指派任務](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step)指定最適化表單，以及執行階段上以表單為中心的工作流程的記錄步驟檔案。 它可讓工作流程搭配不同的適用性Forms運作。 您可以在設計工作流程時決定選取最適化表單的方法。 適用性表單可位於絕對路徑、以裝載形式提交至工作流程，或位於使用變數計算的路徑。

#### 使用以表單為中心的工作流程步驟{#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}的增強記錄功能

以表單為中心的工作流程步驟的記錄功能已標準化。 現在，所有以表單為中心的工作流程步驟都會產生類似的標準化記錄檔。 有助於改善偵錯速度。

## 資料整合{#data-integration}

您現在可以：

* [根據約](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 束清單驗證輸入資料庫。有助於確保僅將有效資料提交至資料來源。
* [覆蓋在](../../forms/using/configure-data-sources.md#configure-soap-web-services) WSDL（網站服務描述語言）檔案中定義的預設端點。

* [覆](../../forms/using/configure-data-sources.md#configure-restful-web-services) [寫Swagger定義檔案中定義的](../../forms/using/configure-data-sources.md#configure-restful-web-services) 預設配置、主機和基本路徑。

## 平台和安全性更新{#platform-and-security-updates}

### 主要平台更新{#major-platform-updates}

可使用支援的作業系統、應用程式伺服器、資料庫、資料庫驅動程式、 JDK、LDAP伺服器和電子郵件伺服器的任意組合來設定AEM Forms。 以下是[支援平台](../../forms/using/aem-forms-jee-supported-platforms.md)中的重大更改：

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
    <li>WebSphere Liberty配置檔案</li>
    <li>OracleWebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>資料庫</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>OracleRAC</li>
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
   <td>連接器</td>
   <td>
    <ul>
     <li>Microsoft Sharepoint 2013的連接器</li>
     <li>EMC Documentum 7.0的連接器</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
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

*如需移轉至不同平台的相關資訊，請聯絡Adobe支援

#### 新的HTML5型UI {#new-html-based-uis}

根據AdobeFlash Player的計畫EOL，以及將Flash型內容移轉至開放標準的整體方向，AEM 6.5 Forms已將AEM Forms JEE Administration Console上以HTML5為基礎的UI取代為JEE上以Flash為基礎的健康監視器、程式管理、Reader擴充功能和類別管理UI。

#### 安全性改善{#security-improvements}

* AEM 6.5 Forms on JEE管理控制台UI現在是以Apache Struts 2.5為基礎。
* AEM 6.5 Forms現在使用jQuery到3.2.1和jQuery UI 1.12.1。請參閱[升級檔案](/help/forms/home.md)以了解變更的影響。

#### 協助工具改善{#accessibility-improvements}

AEM 6.5 Forms已改善AEM Forms Workspace的協助工具。
