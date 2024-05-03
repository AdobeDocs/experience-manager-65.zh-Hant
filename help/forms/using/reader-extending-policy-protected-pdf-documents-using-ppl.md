---
title: 使用Portable Protection LibraryReader擴充受原則保護的PDF檔案
description: Reader擴充功能可透過Acrobat Reader啟用Adobe PDF檔案中的互動功能。 您可以使用Portable Protection Library (PPL)來讀取器延伸受DRM保護的PDF檔案。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# 使用Portable Protection LibraryReader擴充受原則保護的PDF檔案 {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

熟悉Document Security、Reader Extension和Java程式語言的概念，以便透過Reader對Document Security受原則保護的PDF檔案進行擴展。

您可以使用Document Security，將特定PDF檔案的存取許可權製為僅供授權使用者存取。 您也可以決定收件者如何使用受保護檔案。 例如，您可以指定收件人是否可以列印、複製或編輯受Document Security原則保護檔案的文字。 若要深入瞭解Document Security，請參閱 [關於document security](/help/forms/using/admin-help/document-security.md).

您可以使用Reader延伸模組，透過Acrobat Reader啟用Adobe PDF檔案中的互動功能。 這些互動式功能通常只能透過Adobe Acrobat Professional和Standard使用。 若要瞭解Reader擴充功能可啟用的互動功能，請參閱 [Adobe Experience Manager Forms DocAssurance服務&#x200B;](/help/forms/using/overview-aem-document-services.md)**.**

您可以使用可攜式保護程式庫在檔案上套用原則，而不需要透過網路傳輸檔案。 只有安全性認證和保護原則詳細資料會透過網路傳遞。 實際檔案永遠不會離開使用者端，而保護原則會套用至使用者端的本機。

## Reader延伸document security受原則保護的PDF檔案 {#reader-extending-document-security-policy-protected-pdf-documents}

受原則保護的檔案是加密檔案。 您無法使用標準Reader-Extension API來套用、移除和擷取受原則保護的PDF檔案的使用許可權。 只有Portable Protection Library的Reader擴充功能服務提供可套用、移除和擷取受Document Security原則保護之PDF檔案使用許可權的API。

### Reader延伸模組服務 {#reader-extensions-service}

Reader擴充功能服務會將使用許可權新增至受原則保護的PDF檔案，以啟用使用Adobe Acrobat Reader開啟PDF檔案時通常無法使用的功能。 它也有可移除和擷取受原則保護檔案使用許可權的API。

Reader延伸功能服務完全支援以PDF標準1.6和更新版本為基礎的PDF檔案。 除了Acrobat Reader之外，協力廠商使用者不需要任何額外的軟體或外掛程式即可使用受原則保護的PDF檔案。

您可以使用Reader擴充功能服務完成下列工作：

* 將使用許可權套用至受原則保護的PDF檔案。
* 移除受原則保護的PDF檔案的使用許可權。
* 擷取套用到受原則保護的PDF檔案的使用許可權。

### 將使用許可權套用至受Document Security原則保護的PDF檔案 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

您可以使用 `applyUsageRights`Java API可將使用許可權套用至受原則保護的PDF檔案。 使用許可權與Acrobat中預設提供的功能有關，但不適用於Adobe Reader，例如新增註解至表單或填寫表單欄位及儲存表單的功能。 已套用使用許可權的PDF檔案稱為許可權啟用檔案。 在Adobe Reader中開啟許可權啟用檔案的使用者可執行針對該特定檔案啟用的操作。

**語法：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>輸入檔案</p> </td>
   <td><p>指定代表要套用使用許可權的PDF檔案的InputStream。 您可以使用LiveCycleRights Management或AEM Forms Document Security保護的檔案。</p> </td>
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
   <td><p>指定物件型別 <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">使用許可權</a>. usageRights物件代表可套用至受原則保護之PDF檔案的個別權利。</p> </td>
  </tr>
 </tbody>
</table>

### 擷取套用到受原則保護的PDF檔案的使用許可權。   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

您可以使用 `getDocumentUsageRights`Java API可擷取套用到受原則保護之PDF檔案的Reader擴充功能使用許可權。 透過擷取使用許可權的相關資訊，您可以瞭解為受原則保護的PDF檔案啟用的Reader擴充功能。

**語法：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>指定InputStream，代表要從中擷取使用許可權的PDF檔案。 您可以使用LiveCycleRights Management或AEM Forms Document Security保護的檔案。</p> </td>
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

您可以使用 `removeUsageRights`Java API可從受原則保護的檔案中移除使用許可權。 若要在檔案上執行其他AEM Forms操作，必須從受原則保護的PDF檔案中移除使用許可權。 例如，在設定使用許可權之前，您必須以數位方式簽署（或認證）PDF檔案。 因此，如果要在受原則保護的檔案上執行操作，您必須從PDF檔案中移除使用許可權，執行其他操作，例如以數位方式簽署檔案，然後重新將使用許可權套用至檔案。

**語法：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>參數</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>輸入檔案</p> </td>
   <td>指定代表使用方式之PDF檔案的InputStream<br /> 許可權將被移除。 您可以使用LiveCycleRights Management或AEM Forms Document Security保護的檔案。</td>
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
