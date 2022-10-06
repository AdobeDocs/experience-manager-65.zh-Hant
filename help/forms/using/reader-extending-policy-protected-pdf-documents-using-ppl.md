---
title: Reader使用Portable Protection Library擴展受策略保護的PDF文檔
seo-title: Reader extending policy-protected PDF documents using Portable Protection Library
description: Reader擴充功能可透過Acrobat Reader，在Adobe PDF檔案中啟用互動式功能。 您可以使用可移植保護庫(PPL)來擴展受DRM保護的PDF文檔。
seo-description: Reader extensions enable interactive features in Adobe PDF documents through Acrobat Reader. You can use the Portable Protection Library (PPL) to reader extend the DRM protected PDF documents.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Reader使用Portable Protection Library擴展受策略保護的PDF文檔 {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

您必須熟悉文檔安全性、讀者擴展和Java寫程式語言等概念，才能對文檔安全策略保護的PDF文檔進行讀者擴展。

您可以使用文檔安全性來限制僅對授權用戶訪問特定PDF文檔。 您也可以確定收件者如何使用受保護的檔案。 例如，您可以指定收件者是否可以打印、複製或編輯受文檔安全策略保護的文檔的文本。 若要深入了解檔案安全性，請參閱 [關於檔案安全性](/help/forms/using/admin-help/document-security.md).

您可以使用Reader延伸模組，透過Acrobat Reader啟用Adobe PDF檔案中的互動式功能。 這些互動式功能通常只能透過Adobe Acrobat Professional和Standard提供。 若要了解Reader擴充功能可啟用的互動式功能，請參閱 [Adobe Experience Manager Forms DocAssurance服務&#x200B;](/help/forms/using/overview-aem-document-services.md)**.**

您可以使用攜帶型保護庫在文檔上應用策略，而無需通過網路傳輸文檔。 只有安全憑據和保護策略詳細資訊才能通過網路傳輸。 實際文檔從不離開客戶端，保護策略將在客戶端上本地應用。

## Reader擴展文檔安全策略保護的PDF文檔 {#reader-extending-document-security-policy-protected-pdf-documents}

受策略保護的文檔是加密的文檔。 不能使用標準讀者擴展API來應用、刪除和檢索受策略保護的PDF文檔的使用權限。 只有「可移植保護庫」的「Reader擴展」服務提供API，以應用、刪除和檢索文檔安全策略保護的PDF文檔的使用權限。

### Reader擴充功能服務 {#reader-extensions-service}

讀者擴展服務將使用權添加到受策略保護的PDF文檔，激活在使用Adobe Acrobat Reader開啟PDF文檔時不正常可用的功能。 它還具有API，用於刪除和檢索受策略保護文檔的使用權限。

Reader擴充功能服務完全支援以PDF標準1.6和更新版本為基礎的PDF檔案。 除了Acrobat Reader，第三方用戶不需要任何其他軟體或插件來使用受策略保護的PDF文檔。

您可以使用Reader擴充功能服務來完成下列工作：

* 將使用權應用於受策略保護的PDF文檔。
* 刪除受策略保護的PDF文檔的使用權限。
* 檢索應用於受策略保護的PDF文檔的使用權限。

### 將使用權應用於文檔安全策略保護的PDF文檔 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用 `applyUsageRights`Java API，用於將使用權限應用於受策略保護的PDF文檔。 使用權限屬於Acrobat預設提供但Adobe Reader未提供的功能，例如可向表單新增註解，或填寫表單欄位並儲存表單。 應用了使用權限的PDF文檔稱為啟用權限的文檔。 在Adobe Reader中開啟啟用權限的檔案的使用者可以執行針對該特定檔案啟用的操作。

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
   <td><p>指定類型的對象 <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">使用權限</a>. usageRights對象表示可應用於受策略保護的PDF文檔的個別權限。</p> </td>
  </tr>
 </tbody>
</table>

### 檢索應用於受策略保護的PDF文檔的使用權限。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用 `getDocumentUsageRights`Java API用於檢索應用於受策略保護的PDF文檔的讀取器擴展使用權限。 通過檢索有關使用權限的資訊，您可以了解受策略保護的PDF文檔中啟用了閱讀器擴展的功能。

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

System.out.println("UsageRights applied successfully to the document. ");
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

### 刪除受策略保護的PDF文檔的使用權限 {#remove-usage-rights-of-a-policy-protected-pdf-document}

您可以使用 `removeUsageRights`從受策略保護的文檔中刪除使用權限的Java API。 從受策略保護的PDF文檔中刪除使用權限是對文檔執行其他AEM Forms操作所必需的。 例如，您必須先以數位方式簽署（或認證）PDF檔案，才能設定使用權限。 因此，如果要對受策略保護的文檔執行操作，則必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後重新將使用權限應用於文檔。

**語法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>指定表示使用PDF文檔的InputStream<br /> 權限將被移除。 您可以使用LiveCycleRights Management或AEM Forms檔案安全性保護檔案。</td>
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
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
