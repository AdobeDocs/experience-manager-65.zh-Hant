---
title: Reader使用Portable Protection Library擴展受策略保護的PDF文檔
seo-title: Reader extending policy-protected PDF documents using Portable Protection Library
description: Reader擴展通過Acrobat Reader在Adobe PDF檔案中提供互動功能。 可以使用攜帶型保護庫(PPL)來讀取器擴展受DRM保護的PDF文檔。
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

您必須熟悉文檔安全性、讀取器擴展和Java寫程式語言等概念，以便讀取器擴展文檔安全策略保護的PDF文檔。

您可以使用文檔安全性將特定PDF文檔的訪問權限限制為僅限授權用戶。 您還可以確定收件人如何使用受保護的文檔。 例如，您可以指定收件人是否可以打印、複製或編輯受文檔安全策略保護的文檔的文本。 要瞭解有關文檔安全性的詳細資訊，請參閱 [關於文檔安全性](/help/forms/using/admin-help/document-security.md)。

您可以使用閱讀器擴展功能通過Acrobat Reader在Adobe PDF文檔中啟用交互功能。 這些交互功能通常僅通過Adobe Acrobat專業和標準提供。 要瞭解讀者擴展可啟用的交互功能，請參見 [Adobe Experience Manager FormsDocAssurance服務&#x200B;](/help/forms/using/overview-aem-document-services.md)**。**

您可以使用攜帶型保護庫對文檔應用策略，而無需通過網路傳輸文檔。 只有安全憑據和保護策略詳細資訊才能通過網路傳輸。 實際文檔從不離開客戶機，保護策略在客戶機上本地應用。

## Reader擴展文檔安全策略保護的PDF文檔 {#reader-extending-document-security-policy-protected-pdf-documents}

受策略保護的文檔是加密的文檔。 不能使用標準讀取器擴展API來應用、刪除和檢索受策略保護的PDF文檔的使用權限。 只有攜帶型保護庫的Reader擴展服務才提供API來應用、刪除和檢索文檔安全策略保護的PDF文檔的使用權限。

### Reader擴展服務 {#reader-extensions-service}

讀取器擴展服務將使用權限添加到受策略保護的PDF文檔，激活當使用Adobe Acrobat Reader開啟PDF文檔時不正常可用的特徵。 它還具有API，用於刪除和檢索受策略保護的文檔的使用權限。

Reader擴展服務完全支援基於PDF標準1.6及更高版本的PDF文檔。 除Acrobat Reader外，第三方用戶不需要任何額外的軟體或插件來使用受策略保護的PDF文檔。

可以使用Reader擴展服務完成以下任務：

* 將使用權限應用於受策略保護的PDF文檔。
* 刪除受策略保護的PDF文檔的使用權限。
* 檢索應用於受策略保護的PDF文檔的使用權限。

### 將使用權限應用於文檔安全策略保護的PDF文檔 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用 `applyUsageRights`Java API，用於將使用權限應用於受策略保護的PDF文檔。 使用權限與預設在Acrobat但在Adobe Reader不可用的功能有關，例如向表單添加註釋或填寫表單域並保存表單的功能。 對其應用了使用權限的PDF文檔稱為啟用權限的文檔。 在Adobe Reader開啟啟用權限的文檔的用戶可以執行為該特定文檔啟用的操作。

**語法：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>輸入檔案</p> </td>
   <td><p>指定表示要應用使用權的PDF文檔的InputStream。 您可以使用LiveCycleRights Management或AEM Forms文檔安全保護文檔。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>指定表示.jks檔案的檔案對象。 .jks檔案是密鑰庫檔案。 它指向授予使用權的證書。</p> </td>
  </tr>
  <tr>
   <td><p>憑據密碼</p> </td>
   <td><p>指定密鑰庫的口令。 </p> </td>
  </tr>
  <tr>
   <td><p>使用權限</p> </td>
   <td><p>指定類型的對象 <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">使用權限</a>。 usageRights對象表示可應用於受策略保護的PDF文檔的個人權限。</p> </td>
  </tr>
 </tbody>
</table>

### 檢索應用於受策略保護的PDF文檔的使用權限。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用 `getDocumentUsageRights`Java API，用於檢索應用於受策略保護的PDF文檔的讀取器擴展使用權限。 通過檢索有關使用權限的資訊，您可以瞭解已為受策略保護的PDF文檔啟用的功能讀取器擴展。

**語法：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>在文檔中</p> </td>
   <td><p>指定表示要從中檢索使用權的PDF文檔的InputStream。 您可以使用LiveCycleRights Management或AEM Forms文檔安全保護文檔。</p> </td>
  </tr>
 </tbody>
</table>

#### 代碼示例 {#code-sample}

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

您可以使用 `removeUsageRights`從受策略保護的文檔中刪除使用權限的Java API。 從受策略保護的PDF文檔中刪除使用權限是對文檔執行其他AEM Forms操作所必需的。 例如，在設定使用權限之前，必須對PDF文檔進行數字簽名（或認證）。 因此，如果要對受策略保護的文檔執行操作，必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後對文檔重新應用使用權限。

**語法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>輸入檔案</p> </td>
   <td>指定表示使用情況的PDF文檔的InputStream<br /> 將刪除權限。 您可以使用LiveCycleRights Management或AEM Forms文檔安全保護文檔。</td>
  </tr>
 </tbody>
</table>

#### 代碼示例 {#code-sample-1}

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
