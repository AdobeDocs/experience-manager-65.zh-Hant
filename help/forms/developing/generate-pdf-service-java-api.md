---
title: 產生PDF服務Java API QuickStart(SOAP)
seo-title: 產生PDF服務Java API QuickStart(SOAP)
description: 'null'
seo-description: 'null'
uuid: f8c4a476-de5e-440a-b419-0bd1d7fde5ca
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a7c0c4cf-7476-41e7-8d4e-564e6a21458d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 產生PDF服務Java API快速入門(SOAP) {#generate-pdf-service-java-api-quickstart-soap}

Java API快速入門(SOAP)適用於「產生PDF」服務。

[快速入門（SOAP模式）:使用Java API將Microsoft word檔案轉換為PDF檔案](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API（SOAP模式）將PDF檔案轉換為RTF檔案](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode)

AEM Forms作業可以使用AEM Forms強式型別API來執行，連線模式應設為SOAP。

***注意&#x200B;**:「使用AEM Forms進行程式設計」中的「快速入門」是以部署在JBoss Application server和Microsoft windows作業系統上的Forms server為基礎。 但是，如果您使用其他作業系統（例如UNIX），請以適用作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請確定您指定有效的連線屬性。 (請參[閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)*

## 快速入門（SOAP模式）:使用Java API將Microsoft word檔案轉換為PDF檔案 {#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api}

以下代碼示例將名為 *Loan.doc的Word檔案轉換為名* 為Loan.pdf的PDF文檔 **。 (請參 [閱將Word檔案轉換為PDF檔案](/help/forms/developing/converting-file-formats-pdf.md#converting-word-documents-to-pdf-documents)。)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 public class ConvertWordDocumentSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get a Microsoft Word file document to convert to a PDF document
         String inputFileName = "C:\\Adobe\\Loan.doc";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Set createPDF2 parameter values
         String adobePDFSettings = "Smallest_File_Size";
          String securitySettings = "No Security";
          String fileTypeSettings = "Filetype Settings";
 
          //Convert the Word document to a PDF document
          CreatePDFResult result = pdfGenClient.createPDF2(
             inDoc,
             inputFileName,
             fileTypeSettings,
             adobePDFSettings,
             securitySettings,
             null,
             null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the converted PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

## 快速入門（SOAP模式）:使用Java API將HTML內容轉換為PDF檔案 {#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api}

下列Java程式碼範例會將位於https://www.adobe.com的HTML內容轉換為名為 *AdobeHTML.pdf的PDF檔案*。 (請參 [閱將HTML檔案轉換為PDF檔案](/help/forms/developing/converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)。)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 import com.adobe.livecycle.generatepdf.client.HtmlToPdfResult;
 
 public class ConvertHTMLSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get an HTML document to convert to a PDF document a
         String inputFileName = "https://www.adobe.com";
 
          String securitySettings = "No Security";
         String fileTypeSettings = "Standard";
 
          //Convert HTML content to a PDF document
          HtmlToPdfResult result = pdfGenClient.htmlToPDF2(
                  inputFileName,
                  fileTypeSettings,
                  securitySettings,
                  null,
                 null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\AdobeHTML.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
     }
     }
 }
```

## 快速入門（SOAP模式）:使用Java API（SOAP模式）將PDF檔案轉換為RTF檔案 {#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode}

以下代碼示例將名為 *Loan.pdf* 的PDF文檔轉換為名為 *Loan.rtf的RTF文檔*。 (請參 [閱將PDF檔案轉換為非影像格式](/help/forms/developing/converting-file-formats-pdf.md#converting-pdf-documents-to-non-image-formats))。

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.ConvertPDFFormatType;
 import com.adobe.livecycle.generatepdf.client.ExportPDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 
 public class GeneratePdf_ExportPDFSOAP {
 
     public static void main(String[] args)
     {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a GeneratePdfServiceClient object
             GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(factory);
 
             //Get a PDF document to convert to an RTF document
             String inputFileName = "C:\\Adobe\\Loan.pdf.pdf";
             FileInputStream fileInputStream = new FileInputStream(inputFileName);
             Document inDoc = new Document(fileInputStream);
 
             //Convert a PDF document to a RTF document
             ExportPDFResult result = pdfGenClient.exportPDF2(
                 inDoc,
                 inputFileName,
                 ConvertPDFFormatType.RTF,
                 null);
 
          //Get the newly created RTF document
          Document createdDocument = result.getConvertedDocument();
 
          //Save the RTF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf.rtf"));
         }
         catch (Exception e) {
             System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

