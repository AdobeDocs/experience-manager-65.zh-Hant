---
title: 根據片段呈現表單
seo-title: 根據片段呈現表單
description: 使用Forms服務來轉換以使用Designer建立的片段為基礎的表單。
seo-description: 使用Forms服務來轉換以使用Designer建立的片段為基礎的表單。
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 0%

---


# 根據片段{#rendering-forms-based-on-fragments}轉換表單

## 根據片段{#rendering-forms-based-on-fragments-inner}轉換表單

Forms服務可以根據您使用Designer建立的片段來轉換表單。 *fragment*&#x200B;是表單中可重複使用的部分，並儲存為可插入多個表單設計的個別XDP檔案。 例如，片段可以包含地址塊或合法文字。

使用片段可簡化並加速建立和維護大量表單。 建立新表單時，插入對所需片段的引用，該片段將出現在表單中。 片段參考包含指向物理XDP檔案的子表單。 如需建立以片段為基礎的表單設計的詳細資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

片段可以包括多個子表單，這些子表單被包裝在選擇子表單集中。 選擇子表單集基於來自資料連接的資料流來控制子表單的顯示。 您使用條件陳述式來判斷傳送的表單中會出現該集合中的哪些子表單。 例如，集合中的每個子表單可以包括特定地理位置的資訊，而顯示的子表單可以基於用戶的位置來確定。

*指令碼片段*&#x200B;包含可重複使用的JavaScript函式或值，這些函式或值與任何特定物件（例如日期剖析器或web service呼叫）分開儲存。 這些片段包含單一指令碼物件，在「階層」浮動視窗中會顯示為變數的子系。 無法從屬於其他物件屬性的指令碼建立片段，例如驗證、計算或初始化等事件指令碼。

以下是使用片段的優點：

* **內容重複使用**:您可以使用片段，在多個表單設計中重複使用內容。當您需要在多個表單中使用某些相同的內容時，使用片段比複製或重新建立內容更快更簡單。 使用片段也可確保表格設計中常用的部分在所有參照表格中具有一致的內容和外觀。
* **全域更新**:您可以使用片段，在單一檔案中僅對多個表單進行一次全域變更。您可以變更片段中的內容、指令碼物件、資料系結、版面或樣式，而所有參照片段的XDP表單都會反映變更。
* 例如，許多表單中的共同元素可能是包含國家／地區下拉式清單物件的位址區塊。 如果您需要更新下拉式清單物件的值，您必須開啟許多表單才能進行變更。 如果將地址塊包含在片段中，則只需開啟一個片段檔案即可進行更改。
* 若要更新PDF表單中的片段，您必須在Designer中儲存表單。
* **共用表單建立**:您可以使用片段，在多個資源間共用表單建立。具備指令碼專業知識的開發人員或Designer其他進階功能的表單，可開發並共用可運用指令碼和動態屬性的片段。 表單設計人員可以使用這些片段來配置表單設計版面，並確保表單的所有部分在由多人設計的多個表單中具有一致的外觀和功能。

### 使用片段{#assembling-a-form-design-assembled-using-fragments}組合表單設計

您可以組合表單設計，以便根據多個片段傳遞至Forms服務。 要組合多個片段，請使用Assembler服務。 如要查看使用Assemble服務建立由其他Forms服務（Output服務）使用的表單設計的示例，請參閱[使用片段建立PDF文檔](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)。 您可以使用Forms服務來執行相同的工作流程，而不是使用Output服務。

使用Assembler服務時，將傳遞使用片段組合的表單設計。 建立的表單設計不會參照其他片段。 相反地，本主題討論將參照其他片段的表單設計傳遞至Forms服務。 但是，表單設計並非由Assembler裝配。 它是在Designer中建立的。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關建立基於Web的應用程式以根據片段呈現表單的資訊，請參閱[建立用於呈現表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)。

### 步驟{#summary-of-steps}摘要

若要根據片段來轉換表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 指定URI值。
1. 演算表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API操作。

**指定URI值**

若要根據片段成功轉換表單，您必須確保Forms服務能夠找到表單設計參考的表單和片段（XDP檔案）。 例如，假設表單名為PO.xdp，且此表單使用兩個名為FooterUS.xdp和FooterCanada.xdp的片段。 在這種情況下，Forms服務必須能夠找到所有三個XDP檔案。

您可以將表單放在某個位置，將片段放在另一個位置，以組織表單及其片段，或將所有XDP檔案放在同一位置。 為了本節的目的，請假設所有XDP檔案都位於AEM Forms存放庫中。 如需將XDP檔案置入AEM Forms儲存庫的詳細資訊，請參閱[寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources)。

在根據片段呈現表格時，您只能參考表格本身，而不參考片段。 例如，您必須參考PO.xdp，而非FooterUS.xdp或FooterCanada.xdp。 請確定您將片段放置在Forms服務可以找到的位置。

**轉譯表單**

基於片段的表單可以與非碎片表單相同的方式呈現。 也就是說，您可以將表單轉譯為PDF、HTML或表單參考線（已過時）。 本節中的範例會根據片段將表單轉譯為互動式PDF表單。 （請參閱[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)）。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉譯表單時，它會傳回必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到表單。

**另請參閱**

[使用Java API根據片段演算表單](#render-forms-based-on-fragments-using-the-java-api)

[使用web service API，根據片段來轉換表單](#render-forms-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-forms-based-on-fragments-using-the-java-api}根據片段來轉換表單

使用Forms API(Java)，根據片段來轉換表單：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 指定URI值

   * 使用`URLSpec`的建構函式建立儲存URI值的&lt;a0/>物件。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根目錄的字串值。
   * 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 請確定表單設計和片段位於內容根URI中。 否則，Forms服務會引發例外。 要引用儲存庫，請指定`repository://`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。

1. 轉譯表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。
   * `URLSpec`物件，包含Forms服務根據片段來呈現表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 通過調用`getContentType`方法獲取`com.adobe.idp.Document`對象的內容類型。
   * 調用`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 通過調用`InputStream`對象的`read`方法並將位元組陣列作為引數傳遞，建立以表單資料流填充的位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[根據片段呈現表單](#rendering-forms-based-on-fragments)

[快速入門（SOAP模式）:使用Java API根據片段轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#render-forms-based-on-fragments-using-the-web-service-api}根據片段來呈現表單

使用Forms API(web service)，根據片段來轉換表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 指定URI值

   * 使用其建構子建立儲存URI值的`URLSpec`對象。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根目錄的字串值。
   * 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 請確定表單設計位於內容根URI中。 否則，Forms服務會引發例外。 要引用儲存庫，請指定`repository://`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。

1. 轉譯表單

   叫用`FormsService`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 請注意，如果輸入檔案是PDF檔案，則無法設定標籤的PDF選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`對象。 此參數用於儲存渲染的表單。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`對象。 此引數將儲存表單中的頁數。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。 此引數將儲存地區值。
   * 空的`com.adobe.idp.services.holders.FormsResultHolder`對象，將包含此操作的結果。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個參數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象`value`資料成員的值，建立`FormResult`對象。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 通過調用`getContentType`方法獲取`BLOB`對象的內容類型。
   * 調用`setContentType`方法並傳遞`BLOB`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[根據片段呈現表單](#rendering-forms-based-on-fragments)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
