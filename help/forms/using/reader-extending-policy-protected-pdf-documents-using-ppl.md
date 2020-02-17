---
title: Reader使用可攜式保護程式庫擴充受原則保護的PDF檔案
seo-title: Reader使用可攜式保護程式庫擴充受原則保護的PDF檔案
description: Reader擴充功能可透過Acrobat Reader，在Adobe PDF檔案中啟用互動功能。 您可以使用可攜式保護庫(PPL)來讀取器擴充DRM保護的PDF檔案。
seo-description: Reader擴充功能可透過Acrobat Reader，在Adobe PDF檔案中啟用互動功能。 您可以使用可攜式保護庫(PPL)來讀取器擴充DRM保護的PDF檔案。
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Reader使用可攜式保護程式庫擴充受原則保護的PDF檔案 {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

您必須熟悉檔案安全性、讀者擴充功能和Java程式設計語言的概念，才能擴充受原則保護的檔案安全性PDF檔案。

您可以使用檔案安全性，將特定PDF檔案的存取權限限制給僅授權的使用者。 您也可以決定收件者如何使用受保護的檔案。 例如，您可以指定收件者是否可以列印、複製或編輯受原則保護之檔案的文字。 若要進一步瞭解檔案安全性，請參閱 [檔案安全性](/help/forms/using/admin-help/document-security.md)。

您可以使用Reader擴充功能，透過Acrobat Reader在Adobe PDF檔案中啟用互動功能。 這些互動功能通常只能透過Adobe Acrobat Professional和Standard提供。 若要瞭解Reader擴充功能可啟用的互動式功能，請參 [閱Adobe Experience Manager Forms docAssurance服務](/help/forms/using/overview-aem-document-services.md)**。**

您可以使用可攜式保護程式庫，在檔案上套用原則，而不需要透過網路傳送檔案。 只有安全證書和保護策略詳細資訊才能通過網路傳輸。 實際文檔永遠不會離開客戶機，保護策略將在客戶機上本地應用。

## Reader擴充檔案安全性原則保護的PDF檔案 {#reader-extending-document-security-policy-protected-pdf-documents}

受原則保護的檔案是加密的檔案。 您無法使用標準的Reader-Extension API來套用、移除和擷取受原則保護PDF檔案的使用權限。 只有可攜式保護程式庫的Reader Extensions服務才提供API，以套用、移除和擷取檔案安全性原則保護之PDF檔案的使用權。

### Reader Extensions服務 {#reader-extensions-service}

Reader擴充功能服務會將使用權新增至受原則保護的PDF檔案，並啟用在使用Adobe Acrobat Reader開啟PDF檔案時無法正常使用的功能。 此外，它還具備API，可移除和擷取受原則保護檔案的使用權限。

Reader Extensions服務完全支援以PDF標準1.6及更新版本為基礎的PDF檔案。 除了Acrobat Reader，協力廠商使用者不需使用任何其他軟體或外掛程式，即可使用受原則保護的PDF檔案。

您可以使用Reader Extensions服務完成下列工作：

* 套用使用權限至受原則保護的PDF檔案。
* 移除受原則保護PDF檔案的使用權限。
* 擷取套用至受原則保護之PDF檔案的使用權限。

### 將使用權套用至受原則保護的檔案保全PDF檔案 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用 `applyUsageRights`Java API，將使用權套用至受原則保護的PDF檔案。 使用權限與Acrobat預設為Acrobat但Adobe reader未提供的功能相關，例如在表格中新增註解或填寫表格欄位並儲存表格的功能。 具有套用使用權限的PDF檔案稱為具有權限的檔案。 在Adobe Reader中開啟具權限檔案的使用者，可以執行針對該特定檔案啟用的作業。

**** 語法： `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>指定InputStream，它代表要套用使用權的PDF檔案。 您可以使用LiveCycle Rights Management或AEM Forms檔案安全性保護檔案。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>指定表示。jks檔案的檔案對象。 .jks檔案是密鑰庫檔案。 它指向授與使用權的憑證。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>指定密鑰庫的密碼。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>指定UsageRights類型的 <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">對象</a>。 usageRights物件代表可套用至受原則保護之PDF檔案的個別權限。</p> </td>
  </tr>
 </tbody>
</table>

### 擷取套用至受原則保護之PDF檔案的使用權限。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用 `getDocumentUsageRights`Java API擷取套用至受原則保護PDF檔案的Reader擴充功能使用權限。 透過擷取使用權的相關資訊，您可以瞭解受原則保護的PDF檔案所啟用的讀者擴充功能。

**** 語法： `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>指定InputStream，它代表要從中擷取使用權的PDF檔案。 您可以使用LiveCycle Rights Management或AEM Forms檔案安全性保護檔案。</p> </td>
  </tr>
 </tbody>
</table>

#### 程式碼範例 {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ”);
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### 移除受原則保護PDF檔案的使用權限 {#remove-usage-rights-of-a-policy-protected-pdf-document}

您可以使用 `removeUsageRights`Java API來移除受原則保護檔案的使用權限。 若要對檔案執行其他AEM Forms作業，必須從受原則保護的PDF檔案移除使用權。 例如，您必須先數位簽署（或認證）PDF檔案，才能設定使用權。 因此，如果您想要對受原則保護的檔案執行作業，您必須從PDF檔案移除使用權限、執行其他作業，例如數位簽署檔案，然後重新套用檔案的使用權限。

**** 語法： `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>指定InputStream，它代表要移除其使用權限的PDF檔案<br /> 。 您可以使用LiveCycle Rights Management或AEM Forms檔案安全性保護檔案。</td>
  </tr>
 </tbody>
</table>

#### 程式碼範例 {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

