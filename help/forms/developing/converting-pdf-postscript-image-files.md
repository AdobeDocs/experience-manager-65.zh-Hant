---
title: 將PDF轉換為Postscript和Image檔案
description: 使用「轉換PDF」服務，透過Java API和Web服務API將PDF檔案轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# 將PDF轉換為Postscript和影像檔案 {#converting-pdf-to-postscript-andimage-files}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於轉換PDF服務**

轉換PDF服務會將PDF檔案轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。 將PDF檔案轉換為PostScript對於任何PostScript印表機上的自動伺服器式列印很有用。 將PDF檔案轉換為多頁TIFF檔案對於在不支援PDF檔案的內容管理系統中封存檔案而言是切實可行的。

您可以使用轉換PDF服務完成這些工作：

* 將PDF檔案轉換為PostScript。
* 將PDF檔案轉換為影像格式。

>[!NOTE]
>
>如需有關轉換PDF服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF檔案轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題說明如何使用轉換PDF服務API （Java和Web服務），以程式設計方式將PDF檔案轉換為PostScript檔案。 轉換為PostScript檔案的PDF檔案必須是非互動式PDF檔案。 也就是說，如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外狀況。

>[!NOTE]
>
>如需有關轉換PDF服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為PostScript檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務使用者端。
1. 參照要轉換成PostScript檔案的PDF檔案。
1. 設定轉換執行階段選項。
1. 將PDF檔案轉換為PostScript檔案。
1. 儲存PostScript檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF使用者端**

您必須先建立轉換PDF服務使用者端，才能以程式設計方式執行轉換PDF服務作業。 如果您使用Java API，請建立`ConvertPdfServiceClient`物件。 如果您使用網站服務API，請建立`ConvertPDFServiceService`物件。

本節使用AEM Forms中介紹的Web服務功能。 若要存取新功能，您必須使用`lc_version`屬性建構您的Proxy物件。 (請參閱[使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)中的「使用Web服務存取新功能」。)

**參考要轉換成PostScript檔案的PDF檔案**

參考您要轉換成PostScript檔案的PDF檔案。 如本主題前面所述，PDF檔案必須是非互動式PDF檔案。 如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外狀況。

**設定轉換執行階段選項**

將PDF檔案轉換為PostScript檔案時，您可以定義執行階段選項，以指定所建立的PostScript型別。 例如，您可以定義層級3的PostScript檔案。

一般而言，產生的PostScript檔案會反映輸入PDF檔案的大小。 如果您選取`ShrinkToFit`選項(縮減PostScript檔案的輸出以符合頁面)，您不會看到輸入PDF檔案與產生的PostScript檔案之間的差異。 `ShrinkToFit`選項只有在您選擇在小於輸入PDF檔案的頁面大小上列印時才生效。 若要選取較小的頁面大小，請定義`PageSize`選項。 此外，建議您將`RotateAndCenter`選項設為`true`，以取得正確的PostScript輸出。

同樣地，如果您選取`ExpandToFit`選項(會展開PostScript檔案的輸出以符合頁面)，則只有在您選取在大於輸入PDF檔案的頁面大小上列印時，才會生效。 若要選取較大的頁面大小，請定義`PageSize`選項。 此外，建議您將`RotateAndCenter`選項設為`true`，以取得正確的PostScript輸出。

>[!NOTE]
>
>如需您可以設定的執行階段值相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`類別參考。

**將PDF檔案轉換為PostScript檔案**

建立服務使用者端並設定執行階段選項後，您就可以叫用PostScript轉換作業。 此操作需要轉換檔案的相關資訊，包括目標檔案偏好的PostScript層級。

**儲存PostScript檔案**

將PDF檔案轉換為PostScript後，您可以將輸出儲存為PostScript檔案。

**另請參閱**

[使用Java API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用網站服務API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用轉換PDF服務API (Java)將PDF檔案轉換為PostScript：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`ConvertPdfServiceClient`物件。

1. 參照要轉換成PostScript檔案的PDF檔案。

   * 使用物件的建構函式建立`java.io.FileInputStream`物件，並傳遞字串值，指定轉換PDF檔案的位置。
   * 使用`com.adobe.idp.Document`建構函式建立儲存PDF檔案的`com.adobe.idp.Document`物件。 傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 設定轉換執行階段選項。

   * 透過叫用它的建構函式來建立`ToPSOptionsSpec`物件。
   * 透過叫用屬於`ToPSOptionsSpec`物件的適當方法來設定執行階段選項。 例如，若要定義已建立的PostScript層級，請叫用`ToPSOptionsSpec`物件的`setPsLevel`方法，並傳遞指定PostScript層級的`PSLevel`列舉值。 如需您可以設定的所有執行階段值相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`類別參考。

1. 將PDF檔案轉換為PostScript檔案。

   叫用`ConvertPdfServiceClient`物件的`toPS2`方法，並傳遞下列值：

   * 代表要轉換成PostScript檔案之PDF檔案的`com.adobe.idp.Document`物件。
   * 指定PostScript執行階段選項的`ToPSOptionsSpec`物件。

   `toPS2`方法傳回包含新PostScript檔案的`Document`物件。

1. 儲存PostScript檔案。

   * 建立`java.io.File`物件，並確定副檔名為.ps。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`toPS2`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API將PDF檔案轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將PDF檔案轉換為PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用轉換PDF服務API （Web服務），將PDF檔案轉換為PostScript：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立轉換PDF使用者端。

   * 使用預設建構函式建立`ConvertPdfServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ConvertPdfServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您不需要使用`lc_version`屬性。 但是，請指定`?blob=mtom`。
   * 取得`ConvertPdfServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參照要轉換成PostScript檔案的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存已轉換為PostScript檔案的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要轉換之PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，並將位元組陣列、起始位置及資料流長度傳入，以使用資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定轉換執行階段選項。

   * 透過叫用它的建構函式來建立`ToPSOptionsSpec`物件。
   * 將值指派給`ToPSOptionsSpec`物件的資料成員，以設定執行階段選項。 例如，若要定義已建立的PostScript層級，請將`PSLevel`列舉值指派給`ToPSOptionsSpec`物件的`psLevel`資料成員。

1. 將PDF檔案轉換為PostScript檔案。

   叫用`GeneratePDFServiceService`物件的`toPS2`方法，並傳遞下列值：

   * 代表要轉換成PostScript檔案之PDF檔案的`BLOB`物件
   * 指定執行階段選項的`ToPSOptionsSpec`物件

   轉換完成後，存取其`BLOB`物件的`MTOM`屬性，以擷取代表PostScript檔案的二進位資料。 這會傳回您可以寫出至PostScript檔案的位元組陣列。

1. 儲存PostScript檔案。

   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表PS檔案之檔案位置的字串值。
   * 建立位元組陣列，儲存`encryptPDFUsingPassword`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，以將位元組陣列的內容寫入PostScript檔案。

**另請參閱**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF檔案轉換為影像格式 {#converting-pdf-documents-to-image-formats}

您可以使用轉換PDF服務，以程式設計方式將PDF檔案轉換為影像格式，包括JPEG、JPEG2000、TIFF和PNG。 透過將PDF檔案轉換為影像檔案，您可以將PDF檔案用作影像檔案。 例如，您可以將影像放入企業內容管理系統以進行儲存。

將PDF檔案轉換為影像時，轉換PDF服務會為檔案中的每個頁面建立個別的影像。 也就是說，如果檔案有20頁，轉換PDF服務會建立20個影像檔案。 將PDF檔案轉換為影像格式時，您可以為PDF檔案中的每個頁面建立個別影像，或為整個PDF檔案建立單一影像檔案。

>[!NOTE]
>
>如需有關轉換PDF服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要將PDF檔案轉換為任何支援的型別，請執行下列步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務使用者端。
1. 擷取要轉換的PDF檔案。
1. 設定執行階段選項。
1. 將PDF轉換為影像。
1. 從集合中擷取影像檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF使用者端**

您必須先建立轉換PDF服務使用者端，才能以程式設計方式執行轉換PDF服務作業。 如果您使用Java API，請建立`ConvertPdfServiceClient`物件。 如果您使用網站服務API，請建立`ConvertPDFServiceService`物件。

**擷取要轉換的PDF檔案**

擷取PDF檔案以轉換為影像。 您無法將互動式PDF檔案轉換為影像。 如果嘗試這麼做，會發生例外狀況。 若要將互動式PDF檔案轉換為影像檔案，您必須先將PDF檔案平面化，才能進行轉換。 (請參閱[將PDF檔案平面化](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。)

**設定執行階段選項**

設定執行階段選項，例如影像格式和解析度值。 如需有關執行階段值的資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToImageOptionsSpec`類別參考。

**將PDF轉換為影像**

建立服務使用者端並設定執行階段選項後，您可以將PDF檔案轉換為影像。 會傳回包含影像的集合物件。

**從集合擷取影像檔案**

您可以從ConvertPDF服務傳回的集合物件擷取影像檔案。 集合中的每個元素都是可儲存為影像檔案(例如JPG檔案)的`com.adobe.idp.Document`執行個體（或如果您使用Web服務則為`BLOB`執行個體）。

影像檔案的格式取決於`ImageConvertFormat`執行階段選項。 也就是說，如果您將`ImageConvertFormat`執行階段選項設為`ImageConvertFormat.JPEG`，您可以將影像檔案儲存為JPG檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速入門](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用轉換PDF服務API (Java)將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`ConvertPdfServiceClient`物件。

1. 擷取要轉換的PDF檔案。

   * 建立代表要轉換之PDF檔案的`java.io.FileInputStream`物件，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定執行階段選項。

   * 使用物件的建構函式建立`ToImageOptionsSpec`物件。
   * 視需要叫用屬於此物件的方法。 例如，透過叫用`setImageConvertFormat`方法並傳遞指定格式型別的`ImageConvertFormat`列舉值來設定影像型別。

   >[!NOTE]
   >
   >必須設定`ImageConvertFormat`列舉值。

1. 將PDF轉換為影像。

   叫用`ConvertPdfServiceClient`物件的`toImage2`方法，並傳遞下列值：

   * 代表要轉換之PDF檔案的`com.adobe.idp.Document`物件。
   * 包含目標影像格式各種偏好設定的`com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec`物件。

   `toImage2`方法傳回包含影像的`java.util.List`物件。 集合中的每個元素都是`com.adobe.idp.Document`執行個體。

1. 從集合中擷取影像檔案。

   逐一檢視`java.util.List`物件，以判斷影像是否存在。 每個元素都是`com.adobe.idp.Document`執行個體。 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件以儲存影像。

**另請參閱**

[快速入門(SOAP模式)：使用Java API將PDF檔案轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服務API將PDF檔案轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用轉換PDF服務API （Web服務）將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立轉換PDF使用者端。

   * 使用預設建構函式建立`ConvertPdfServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ConvertPdfServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您不需要使用`lc_version`屬性。 但是，請指定`?blob=mtom`。
   * 取得`ConvertPdfServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 此`BLOB`物件是用來儲存PDF表單。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞字串值，該值會指定PDF表單的位置以及開啟檔案的模式。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 取得`System.IO.FileStream`物件的`Length`屬性，以決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定執行階段選項。

   * 使用物件的建構函式建立`ToImageOptionsSpec`物件。
   * 視需要叫用屬於此物件的方法。 例如，透過叫用`setImageConvertFormat`方法並傳遞指定格式型別的`ImageConvertFormat`列舉值來設定影像型別。

   >[!NOTE]
   >
   >必須設定`ImageConvertFormat`列舉值。

1. 將PDF轉換為影像。

   叫用`ConvertPDFServiceService`物件的`toImage2`方法，並傳遞下列值：

   * 代表要轉換之檔案的`BLOB`物件
   * 包含目標影像格式各種偏好設定的`ToImageOptionsSpec`物件

   `toImage2`方法傳回包含新建立之影像檔的`MyArrayOfBLOB`物件。

1. 從集合中擷取影像檔案。

   * 透過取得物件`Count`欄位的值來決定`MyArrayOfBLOB`物件中的元素數目。 每個元素都是包含影像的`BLOB`物件。
   * 逐一檢視`MyArrayOfBLOB`物件並儲存每個影像檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
