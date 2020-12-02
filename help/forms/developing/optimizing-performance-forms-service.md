---
title: 最佳化Forms Service的效能
seo-title: 最佳化Forms Service的效能
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 0%

---


# 優化Forms服務的效能{#optimizing-the-performance-of-theforms-service}

## 優化Forms服務的效能{#optimizing-the-performance-of-the-forms-service}

在轉譯表單時，您可以設定執行時期選項，以最佳化Forms服務的效能。 另一個可以執行的任務是將XDP檔案儲存在儲存庫中，以提高Forms服務的效能。 不過，本節不說明如何執行此任務。 （請參閱[使用Java客戶端庫叫用服務](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)。）

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要最佳化在轉譯表單時的Forms服務效能，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定效能運行時選項。
1. 演算表格。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API操作。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms web service API，請建立`FormsService`物件。

**設定效能運行時選項**

您可以設定以下效能運行時選項來改進Forms服務的效能：

* **表單快取**:您可以快取在伺服器快取中呈現為PDF的表格。每個表單在首次產生後都會快取。 在後續的演算中，如果快取的表單比表單設計的時間戳記還新，則會從快取中擷取表單。 通過快取表單，可以提高Forms服務的效能，因為它不必從儲存庫檢索表單設計。
* 表單參考線（已過時）的轉換時間可能比其他轉換類型要長。 建議您快取表單參考線（已過時），以改善效能。
* **獨立選項**:如果您不需要Forms服務來執行伺服器端計算，可將「單機版」選項設為 `true`，如此會產生沒有狀態資訊的表單。如果您想要將互動式表單轉譯給使用者，然後使用者將資訊輸入表單並將表單提交回表單服務，則需要狀態資訊。 然後，Forms服務會執行計算操作，並將表單呈現回用戶，並將結果顯示在表單中。 如果沒有狀態資訊的表單會提交回Forms服務，則只有XML資料可供使用，且不會執行伺服器端計算。
* **線性化的PDF**:組織線性化的PDF檔案，以便在網路環境中提供有效率的漸進式存取。PDF檔案在所有方面都是有效的PDF，並與所有現有檢視器和其他PDF應用程式相容。 也就是說，在PDF仍在下載時，可以檢視其線性化。
* 在用戶端上轉譯PDF表格時，這個選項無法改善效能。
* **GuideRSL選項**:啟用使用執行時期共用程式庫產生表單指南（已過時）的功能。這表示第一個要求會下載較小的SWF檔案，以及儲存在瀏覽器快取中的較大共用程式庫。 如需詳細資訊，請參閱Flex說明檔案中的RSL。
* 您也可以在用戶端上轉譯表單，以改善Forms服務的效能。 （請參閱用戶端上的[轉換表單。）](/help/forms/developing/rendering-forms-client.md)

**轉譯表單**

若要在設定效能選項後轉換表格，請使用與轉換沒有效能選項的表格相同的應用程式邏輯。

**將表單資料串流寫入用戶端網頁瀏覽器**

在Forms服務轉譯表單後，它會傳回必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到表單。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將表單轉換為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#optimize-the-performance-using-the-java-api}最佳化效能

使用Forms API(Java)演算具最佳效能的表單：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 設定效能運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`對象。
   * 調用`PDFFormRenderSpec`物件的`setCacheEnabled`方法並傳遞`true`，以設定表單快取選項。
   * 調用`PDFFormRenderSpec`物件的`setLinearizedPDF`方法並傳遞`true.`，以設定線性化選項

1. 轉譯表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * `PDFFormRenderSpec`物件，可儲存執行時期選項以改善效能。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 建立`javax.servlet.ServletOutputStream`物件，用來傳送表單資料串流至用戶端網頁瀏覽器。
   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 建立位元組陣列，並以`InputStream`物件的`read`方法來填入表單資料流，並將位元組陣列傳入為引數。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API最佳化效能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#optimize-the-performance-using-the-web-service-api}最佳化效能

使用Forms API(web service)演算具最佳效能的表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 設定效能運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`對象。
   * 調用`PDFFormRenderSpec`物件的`setCacheEnabled`方法並傳遞true，以設定表單快取選項。
   * 調用`PDFFormRenderSpec`物件的`setStandAlone`方法並傳遞true，以設定獨立選項。
   * 調用`PDFFormRenderSpec`物件的`setLinearizedPDF`方法並傳遞true，以設定線性化選項。

1. 轉譯表單

   叫用`FormsService`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。
   * 儲存運行時選項的`PDFFormRenderSpecc`對象。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`對象。 這可用來儲存轉譯的PDF表單。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`對象。 （此引數將儲存表單中的頁數）。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。 （此引數將儲存地區值）。
   * 空的`com.adobe.idp.services.holders.FormsResultHolder`對象，將包含此操作的結果。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個參數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象`value`資料成員的值，建立`FormResult`對象。
   * 建立`javax.servlet.ServletOutputStream`物件，用來傳送表單資料串流至用戶端網頁瀏覽器。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
