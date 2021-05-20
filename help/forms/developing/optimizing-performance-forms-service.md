---
title: 優化表單服務的效能
seo-title: 優化表單服務的效能
description: 在轉譯表單時設定執行階段選項，並將XDP檔案儲存在存放庫中，以最佳化Forms服務的效能。
seo-description: 在轉譯表單時設定執行階段選項，並將XDP檔案儲存在存放庫中，以最佳化Forms服務的效能。
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---

# 最佳化Forms服務的效能{#optimizing-the-performance-of-theforms-service}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 最佳化Forms服務的效能{#optimizing-the-performance-of-the-forms-service}

轉譯表單時，您可以設定執行階段選項，以最佳化Forms服務的效能。 為了改善Forms服務的效能，您可以執行的另一項任務是將XDP檔案儲存在存放庫中。 不過，本節不說明如何執行此工作。 （請參閱[使用Java客戶端庫調用服務](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)。）

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

若要在轉譯表單時最佳化Forms服務的效能，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定效能運行時選項。
1. 轉譯表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsService`物件。

**設定效能運行時選項**

您可以設定下列效能執行時間選項以改善Forms服務的效能：

* **表單快取**:您可以快取在伺服器快取中呈現為PDF的表單。每個表單在首次產生後都會快取。 在後續呈現時，如果快取的表單比表單設計的時間戳記還新，則會從快取中擷取表單。 透過快取表單，可改善Forms服務的效能，因為它不需要從存放庫擷取表單設計。
* 表單參考線（已過時）的轉換時間可能會比其他轉換類型長。 建議您快取表單參考線（已淘汰），以提高效能。
* **獨立選項**:若您不需要Forms服務執行伺服器端計算，可將「獨立」選項設為， `true`如此即會呈現表單，且不含狀態資訊。如果您想要將互動式表單轉譯給一般使用者，然後使用者在表單中輸入資訊，並將表單提交回Forms服務，則需要狀態資訊。 然後，Forms服務執行計算操作，並將表單呈現回使用者，並將結果顯示在表單中。 如果將沒有狀態資訊的表單提交回Forms服務，則只有XML資料可供使用，且不會執行伺服器端計算。
* **線性化PDF**:組織線性化的PDF檔案，以在網路環境中實現高效的增量訪問。PDF檔案在所有方面都是有效的PDF，並與所有現有的檢視器和其他PDF應用程式相容。 也就是說，可在下載線性化的PDF時加以檢視。
* 在用戶端上轉譯PDF表單時，此選項無法改善效能。
* **GuideRSL選項**:啟用使用執行階段共用程式庫產生表單指南（已淘汰）。這表示第一個請求將下載較小的SWF檔案，以及儲存在瀏覽器快取中的較大共用庫。 如需詳細資訊，請參閱Flex檔案中的RSL 。
* 您也可以在用戶端上轉譯表單，以改善Forms服務的效能。 (請參閱在用戶端上呈現Forms](/help/forms/developing/rendering-forms-client.md) 。)[

**轉譯表單**

若要在設定效能選項後呈現表單，請使用與呈現沒有效能選項的表單相同的應用程式邏輯。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯表單後，會傳回表單資料流，您必須將其寫入用戶端網頁瀏覽器。 寫入客戶端Web瀏覽器時，用戶可以看到該表單。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms轉譯為HTML](/help/forms/developing/rendering-forms-html.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#optimize-the-performance-using-the-java-api}優化效能

使用Forms API(Java)演算效能最佳的表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 設定效能運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`物件。
   * 調用`PDFFormRenderSpec`對象的`setCacheEnabled`方法並傳遞`true`來設定表單快取選項。
   * 調用`PDFFormRenderSpec`對象的`setLinearizedPDF`方法並傳遞`true.`來設定線性化選項

1. 轉譯表單

   調用`FormsServiceClient`對象的`renderPDFForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * `PDFFormRenderSpec`物件，可儲存執行時選項以改善效能。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立`javax.servlet.ServletOutputStream`物件，用於將表單資料流傳送至用戶端網頁瀏覽器。
   * 調用`FormsResult`對象s `getOutputContent`方法，建立`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 通過調用`InputStream`對象的`read`方法並將位元組陣列作為參數傳遞，建立位元組陣列並用表單資料流填充。
   * 調用`javax.servlet.ServletOutputStream`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API最佳化效能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#optimize-the-performance-using-the-web-service-api}優化效能

使用Forms API（網站服務）演算效能最佳的表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`物件並設定驗證值。

1. 設定效能運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`物件。
   * 調用`PDFFormRenderSpec`對象的`setCacheEnabled`方法並傳遞true，設定表單快取選項。
   * 叫用`PDFFormRenderSpec`物件的`setStandAlone`方法並傳遞true，以設定獨立選項。
   * 調用`PDFFormRenderSpec`對象的`setLinearizedPDF`方法並傳遞true，設定線性化選項。

1. 轉譯表單

   調用`FormsService`對象的`renderPDFForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。
   * 儲存運行時選項的`PDFFormRenderSpecc`對象。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。
   * 由方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 這可用來儲存轉譯的PDF表單。
   * 由方法填入的空`javax.xml.rpc.holders.LongHolder`物件。 （此引數會以表單儲存頁數）。
   * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 （此參數將儲存區域設定值）。
   * 將包含此操作結果的空`com.adobe.idp.services.holders.FormsResultHolder`對象。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象的`value`資料成員的值，以建立`FormResult`對象。
   * 建立`javax.servlet.ServletOutputStream`物件，用於將表單資料流傳送至用戶端網頁瀏覽器。
   * 調用`FormsResult`對象的`getOutputContent`方法，建立包含表單資料的`BLOB`對象。
   * 建立位元組陣列，並調用`BLOB`對象的`getBinaryData`方法來填入。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 調用`javax.servlet.http.HttpServletResponse`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
