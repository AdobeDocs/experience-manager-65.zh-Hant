---
title: Reader使用Portable Protection Library擴展受策略保護的PDF文檔
seo-title: Reader使用Portable Protection Library擴展受策略保護的PDF文檔
description: Reader擴充功能可透過Acrobat Reader，在Adobe PDF檔案中啟用互動式功能。 您可以使用Portable Protection Library(PPL)來讀取器擴展受DRM保護的PDF文檔。
seo-description: Reader擴充功能可透過Acrobat Reader，在Adobe PDF檔案中啟用互動式功能。 您可以使用Portable Protection Library(PPL)來讀取器擴展受DRM保護的PDF文檔。
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: 文件安全性
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---

# Reader使用Portable Protection Library {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}擴展受策略保護的PDF文檔

您必須熟悉檔案安全性、讀者擴充功能和Java程式設計語言等概念，才能閱讀者擴充受原則保護的檔案安全性PDF檔案。

您可以使用檔案安全性，限制僅授權使用者存取特定PDF檔案。 您也可以確定收件者如何使用受保護的檔案。 例如，您可以指定收件者是否可以打印、複製或編輯受文檔安全策略保護的文檔的文本。 要了解有關文檔安全性的詳細資訊，請參閱[關於文檔安全性](/help/forms/using/admin-help/document-security.md)。

您可以使用Reader延伸模組，透過Acrobat Reader啟用Adobe PDF檔案中的互動式功能。 這些互動式功能通常僅透過Adobe Acrobat Professional和Standard提供。 要了解讀者擴展功能可啟用的互動式功能，請參閱[Adobe Experience Manager Forms DocAssurance服務&#x200B;](/help/forms/using/overview-aem-document-services.md)**。**

您可以使用攜帶型保護庫在文檔上應用策略，而無需通過網路傳輸文檔。 只有安全憑據和保護策略詳細資訊才能通過網路傳輸。 實際文檔從不離開客戶端，保護策略將在客戶端上本地應用。

## Reader擴展受策略保護的PDF文檔{#reader-extending-document-security-policy-protected-pdf-documents}

受策略保護的文檔是加密的文檔。 您無法使用標準讀者擴展API來應用、刪除和檢索受策略保護的PDF文檔的使用權限。 只有Portable Protection Library的Reader擴展服務才提供API，以應用、刪除和檢索文檔安全策略保護的PDF文檔的使用權限。

### Reader擴展服務{#reader-extensions-service}

Reader延伸功能服務會將使用權限新增至受原則保護的PDF檔案，以啟用使用Adobe AcrobatReader開啟PDF檔案時無法正常使用的功能。 它還具有API，用於刪除和檢索受策略保護文檔的使用權限。

Reader延伸模組服務完全支援以PDF standard 1.6及更新版本為基礎的PDF檔案。 除了Acrobat Reader，協力廠商使用者不需要任何其他軟體或外掛程式，即可使用受原則保護的PDF檔案。

您可以使用Reader擴充功能服務來完成下列工作：

* 將使用權限應用於受策略保護的PDF文檔。
* 刪除受策略保護的PDF文檔的使用權限。
* 檢索應用於受策略保護的PDF文檔的使用權限。

### 將使用權應用於受文檔安全策略保護的PDF文檔{#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用`applyUsageRights`Java API將使用權限應用於受策略保護的PDF文檔。 使用權限屬於Acrobat預設提供但Adobe Reader未提供的功能，例如可向表單新增註解，或填寫表單欄位並儲存表單。 套用使用權限的PDF檔案稱為啟用權限的檔案。 在Adobe Reader中開啟啟用權限的檔案的使用者可以執行針對該特定檔案啟用的操作。

**語法：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>指定表示要應用使用權限的PDF文檔的InputStream。 您可以使用LiveCycleRights Management或AEM Forms檔案安全性保護檔案。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>指定表示.jks檔案的檔案對象。 .jks檔案是密鑰庫檔案。 它指向授予使用權的憑證。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>指定金鑰存放區的密碼。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>指定類型<a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>的對象。 usageRights物件代表可套用至受原則保護PDF檔案的個別權限。</p> </td>
  </tr>
 </tbody>
</table>

### 檢索應用於受策略保護的PDF文檔的使用權限。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用`getDocumentUsageRights`Java API來檢索應用於受策略保護的PDF文檔的讀取器擴展使用權限。 通過檢索有關使用權限的資訊，您可以了解受策略保護的PDF文檔中啟用的讀者擴展功能。

**語法：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>指定表示要從中檢索使用權的PDF文檔的InputStream。 您可以使用LiveCycleRights Management或AEM Forms檔案安全性保護檔案。</p> </td>
  </tr>
 </tbody>
</table>

#### 程式碼範例{#code-sample}

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

### 刪除受策略保護的PDF文檔{#remove-usage-rights-of-a-policy-protected-pdf-document}的使用權限

您可以使用`removeUsageRights`Java API從受策略保護的文檔中刪除使用權限。 若要對檔案執行其他AEM Forms作業，必須從受原則保護的PDF檔案移除使用權限。 例如，您必須先以數位方式簽署（或認證）PDF檔案，才能設定使用權限。 因此，如果要對受策略保護的文檔執行操作，必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後對文檔重新應用使用權限。

**語法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>指定表示將從中刪除使用<br />權限的PDF文檔的InputStream。 您可以使用LiveCycleRights Management或AEM Forms檔案安全性保護檔案。</td>
  </tr>
 </tbody>
</table>

#### 程式碼範例{#code-sample-1}

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
