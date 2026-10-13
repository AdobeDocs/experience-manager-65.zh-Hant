---
title: Reader使用Portable Protection Library擴充受原則保護的PDF檔案
description: Reader擴充功能可透過Acrobat Reader啟用Adobe PDF檔案中的互動功能。 您可以使用Portable Protection Library (PPL)來讀取器延伸受DRM保護的PDF檔案。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security,Reader Extensions
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%
---
# Reader使用Portable Protection Library擴充受原則保護的PDF檔案 {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

熟悉Document Security、Reader Extension和Java程式語言的概念，以便透過Reader對Document Security受原則保護的PDF檔案進行擴展。

您可以使用Document Security，限制僅授權使用者存取特定PDF檔案。 您也可以決定收件者如何使用受保護檔案。 例如，您可以指定收件人是否可以列印、複製或編輯受Document Security原則保護檔案的文字。 若要深入瞭解Document Security，請參閱[關於Document Security](/help/forms/using/admin-help/document-security.md)。

您可以使用Reader延伸模組，透過Acrobat Reader啟用Adobe PDF檔案中的互動功能。 這些互動式功能通常只能透過Adobe Acrobat Professional和Standard使用。 若要瞭解Reader延伸模組可啟用的互動功能，請參閱[Adobe Experience Manager Forms DocAssurance服務&#x200B;](/help/forms/using/overview-aem-document-services.md)**。**

您可以使用可攜式保護程式庫在檔案上套用原則，而不需要透過網路傳輸檔案。 只有安全性認證和保護原則詳細資料會透過網路傳遞。 實際檔案永遠不會離開使用者端，而保護原則會套用至使用者端的本機。

## Reader延伸document security受原則保護的PDF檔案 {#reader-extending-document-security-policy-protected-pdf-documents}

受原則保護的檔案是加密檔案。 您無法使用標準Reader-Extension API來套用、移除和擷取受原則保護的PDF檔案的使用許可權。 只有Portable Protection Library的Reader擴充功能服務提供可套用、移除和擷取受Document Security原則保護的PDF檔案使用許可權的API。

### Reader擴充功能服務 {#reader-extensions-service}

Reader擴充功能服務將使用許可權新增至受原則保護的PDF檔案，並啟用使用Adobe Acrobat Reader開啟PDF檔案時通常無法使用的功能。 它也有可移除和擷取受原則保護檔案使用許可權的API。

Reader擴充功能服務完全支援以PDF standard 1.6和更新版本為基礎的PDF檔案。 除了Acrobat Reader之外，協力廠商使用者不需使用任何其他軟體或外掛程式，即可使用受原則保護的PDF檔案。

您可以使用Reader擴充功能服務完成下列工作：

* 將使用許可權套用至受原則保護的PDF檔案。
* 移除受原則保護的PDF檔案的使用許可權。
* 擷取套用至受原則保護的PDF檔案的使用許可權。

### 將使用許可權套用至受Document Security原則保護的PDF檔案 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用`applyUsageRights`Java API將使用許可權套用至受原則保護的PDF檔案。 使用許可權與Acrobat預設提供但不適用於Adobe Reader的功能相關，例如新增註解至表單或填寫表單欄位及儲存表單的功能。 已套用使用許可權的PDF檔案稱為許可權啟用檔案。 在Adobe Reader中開啟許可權啟用檔案的使用者，可以執行為該特定檔案啟用的操作。

**語法：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>輸入檔案</p> </td>
   <td><p>指定代表要套用使用許可權的PDF檔案的InputStream。 您可以使用LiveCycle Rights Management或AEM Forms document security受保護的檔案。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>指定代表.jks檔案的檔案物件。 .jks檔案是金鑰庫檔案。 它會指向授予使用許可權的憑證。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>指定金鑰存放區的密碼。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>指定型別<a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>的物件。 usageRights物件代表可套用至受原則保護的PDF檔案的個別權利。</p> </td>
  </tr>
 </tbody>
</table>

### 擷取套用至受原則保護的PDF檔案的使用許可權。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用`getDocumentUsageRights`Java API來擷取套用到受原則保護的PDF檔案的Reader延伸使用許可權。 透過擷取使用許可權的相關資訊，您可以瞭解為受原則保護的PDF檔案啟用的Reader擴充功能。

**語法：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>指定代表要從中擷取使用許可權之PDF檔案的InputStream。 您可以使用LiveCycle Rights Management或AEM Forms document security受保護的檔案。</p> </td>
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

### 移除受原則保護的PDF檔案的使用許可權 {#remove-usage-rights-of-a-policy-protected-pdf-document}

您可以使用`removeUsageRights`Java API從受原則保護的檔案中移除使用許可權。 若要在檔案上執行其他PDF操作，必須從受原則保護的AEM Forms檔案中移除使用許可權。 例如，在設定使用許可權之前，您必須以數位方式簽署（或認證）PDF檔案。 因此，如果要在受原則保護的檔案上執行操作，您必須從PDF檔案中移除使用許可權，執行其他操作，例如以數位方式簽署檔案，然後重新將使用許可權套用至檔案。

**語法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>輸入檔案</p> </td>
   <td>指定代表PDF檔案的InputStream，將會從中移除使用<br />許可權。 您可以使用LiveCycle Rights Management或AEM Forms document security受保護的檔案。</td>
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
