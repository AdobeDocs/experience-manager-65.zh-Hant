---
title: 以寫程式AEM方式使用Document Services
seo-title: Using AEM Document Services Programmatically
description: 瞭解如何使用Document Services API對PDF文檔進行數字簽名、加密和生成。
seo-description: Learn how to use Document Services APIs to Digitally sign, encrypt, and generate PDF documents.
uuid: bf5ee197-4daf-4a64-8b6d-2c0d1f232b1c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 32118d3b-54d0-4283-b489-780bdcbfc8d2
exl-id: 9bf090db-2c14-439e-ad78-6832678a309d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6430'
ht-degree: 1%

---

# 以寫程式AEM方式使用Document Services  {#using-aem-document-services-programmatically}

本文檔中的示例和示例可幫助您瞭解和AEM使用OSGi環境中AEM Forms上的Document Services。 有關AEM FormsJEE環境的示例和示例，請參見

* [簽名服務Java API快速啟動](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/signature-service-java-api-quick.html?#programming-aem-forms-jee)

* [加密服務Java API快速啟動](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/encryption-service-java-api-quick.html?#developer-reference)

* [Acrobat Reader擴展服務Java API快速入門](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?#developer-reference)

## 必備條件 {#prerequisite}

* 在使用DocAssurance服務API之前， [配置DocAssurance服務](/help/forms/using/install-configure-document-services.md)。

* 下載和配置 [AEM Forms客戶端SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 和你的馬AEM文計畫。 使用Document Services生成Maven項目所需AEM的客戶端類可在 [AEM Forms客戶端SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)

* 學習 [如何使用MavenAEM構建項目](/help/sites-developing/ht-projects-maven.md)

## DocAssurance服務 {#docassurance-service}

DocAssurance服務包括以下服務：

* 簽名服務
* 加密服務
* Reader分機服務

您可以使用DocAssurance服務執行以下操作：

* [添加不可見簽名](/help/forms/using/aem-document-services-programmatically.md#p-adding-an-invisible-signature-field-p)

* [添加簽名欄位](/help/forms/using/aem-document-services-programmatically.md#p-adding-a-signature-field-nbsp-p)
* [套用文件時間戳記](/help/forms/using/aem-document-services-programmatically.md#apply-document-timestamp)

* [獲取簽名](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-p)
* [獲取簽名欄位清單](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-field-list-nbsp-p)
* [修改簽名欄位](/help/forms/using/aem-document-services-programmatically.md#p-modifying-signature-fields-nbsp-p)

* [安全保護文件](/help/forms/using/aem-document-services-programmatically.md#p-securing-documents-p)

* [獲取憑據使用權限](/help/forms/using/aem-document-services-programmatically.md#p-getting-credential-usage-rights-p)

* [獲取文檔使用權限](/help/forms/using/aem-document-services-programmatically.md#p-getting-document-usage-rights-p)

* [刪除使用權限](/help/forms/using/aem-document-services-programmatically.md#p-removing-usage-rights-p)
* [驗證數字簽名](/help/forms/using/aem-document-services-programmatically.md#p-verifying-digital-signatures-p)
* [驗證多個數字簽名](/help/forms/using/aem-document-services-programmatically.md#p-verifying-multiple-digital-signatures-p)
* [刪除數字簽名](/help/forms/using/aem-document-services-programmatically.md#p-removing-digital-signatures-p)

* [獲取驗證簽名欄位](/help/forms/using/aem-document-services-programmatically.md#p-getting-certifying-signature-field-p)
* [獲取PDF加密類型](/help/forms/using/aem-document-services-programmatically.md#p-getting-pdf-encryption-type-p)
* [刪除密碼加密](/help/forms/using/aem-document-services-programmatically.md#p-removing-password-encryption-from-pdf-p)

* [刪除證書加密](/help/forms/using/aem-document-services-programmatically.md#p-removing-certificate-encryption-p)

>[!NOTE]
>
>所有這些服務都使用Document對象作為輸入參數，在URL中可找到Javadoc [https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/index.html](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/index.html)

### 添加不可見簽名欄位 {#adding-an-invisible-signature-field}

數字簽名顯示在簽名欄位中，這些欄位是包含簽名的圖形表示形式的欄位。 簽名欄位可以是可見的或不可見的。 簽名者可以使用預先存在的簽名欄位，或者可以以寫程式方式添加簽名欄位。 在兩種情況下，簽名欄位都必須存在，才能簽名PDF文檔。 可以使用簽名服務Java API或簽名Web服務API以寫程式方式添加簽名欄位。 您可以向PDF文檔添加多個簽名欄位。 但是，每個簽名欄位名稱必須唯一。

**語法**: `addInvisibleSignatureField(Document inDoc, String signatureFieldName, FieldMDPOptionSpec fieldMDPOptionsSpec, PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>包含PDF的文檔對象。<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code> </td>
   <td>簽名欄位的名稱。 此參數是必需的，不能將null作為值。<br /> </td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>A <code>FieldMDPOptionSpec</code> 對象，指定簽名後鎖定的PDF文檔欄位。 此參數是可選的，可接受空值。</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>A <code>SeedValueOptions</code> 指定欄位的各種種子值的對象。 T此參數是可選的，可接受空值。<span class="acrolinxCursorMarker"></span></td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數，此參數僅對加密檔案是必需的。</td>
  </tr>
 </tbody>
</table>

下面是一個示例Java代碼，它將不可見的簽名欄位添加到PDF文檔。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds an invisible signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddInvisibleSignatureField.class)
public class AddInvisibleSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addInvisibleSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addInvisibleSignatureField(
       inDoc,
       fieldName,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

您還可以使用 [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)文檔簽名規範。 使用以下示例代碼將簽名格式設定為 [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)

```java
SigningFormat signingFormat = SigningFormat.CAdES;
sigAppearence.setSigningFormat(signingFormat);
signOptions.setSigAppearence(sigAppearence);
```

### 添加簽名欄位  {#adding-a-signature-field-nbsp}

可以使用簽名服務Java API或簽名Web服務API以寫程式方式添加簽名欄位。 您可以向PDF文檔添加多個簽名欄位。 但是，每個簽名欄位名稱必須唯一。

**語法**:

```java
public Document addSignatureField(Document inDoc,
 String signatureFieldName,
 Integer pageNo,
 PositionRectangle positionRectangle,
 FieldMDPOptionSpec fieldMDPOptionsSpec,
 PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)
```

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>包含PDF的文檔對象</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>簽名欄位的名稱。 此參數是必需的，不能接受空值。</td>
  </tr>
  <tr>
   <td><code>pageNumber</code></td>
   <td>添加簽名欄位的頁碼。 有效值是文檔中包含的頁數的1。 此參數是必需的，不能接受空值。<br /> </td>
  </tr>
  <tr>
   <td><code>positionRectangle</code></td>
   <td>A <code>PositionRectangle object</code> 指定簽名欄位的位置。 此參數是必需的，不能接受空值。 如果指定的矩形在指定頁面的裁剪框上不至少部分位於 <code>InvalidArgumentException</code> 。 此外，指定矩形的高度或寬度不能為0或負。 左下X或左下Y坐標可以為0或更大，但不為負，並且相對於頁面的裁剪框。</td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>A <code>FieldMDPOptionSpec</code> 對象，指定簽名後鎖定的PDF文檔欄位。 這是可選參數，可為Null。</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>A <code>SeedValueOptions</code> 指定欄位的各種種子值的對象。 這是可選參數，可為Null。</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數。 此參數僅對加密的檔案是必需的。</td>
  </tr>
 </tbody>
</table>

下面是一個示例Java代碼，它將簽名欄位添加到PDF文檔。

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds a signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddSignatureField.class)
public class AddSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addSignatureField(
       inDoc,
       fieldName,
       pageNum,
       post,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 套用文件時間戳記 {#apply-document-timestamp}

可以按順序以寫程式方式對文檔進行時間戳 [PAdES 4](https://en.wikipedia.org/wiki/PAdES) 規範。 您還可以使用 [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29) 事務處理相關單據的規格。

**語法**: `applyDocumentTimeStamp(Document doc, VerificationTime verificationTime, ValidationPreferences dssPrefs, ResourceResolver resourceResolver, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>doc</code> </td>
   <td>包含PDF的文檔對象。<br /> </td>
  </tr>
  <tr>
   <td><code>VerificationTime</code></td>
   <td>簽名的驗證時間<br /> </td>
  </tr>
  <tr>
   <td><code>ValidationPreferences</code> </td>
   <td>控制驗證配置的首選項。</td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>到花崗岩信任儲存的資源解析器。</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數。 僅當檔案已加密時，才需要此選項。</td>
  </tr>
 </tbody>
</table>

以下代碼示例將時間戳添加到文檔中 [PAdES 4](https://en.wikipedia.org/wiki/PAdES)。

```java
package com.adobe.signatures.test;

import java.io.File;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

 @Component
 @Service(value=Test.class)
 public class Test {

     @Reference
     private DocAssuranceService docAssuranceService;

     @Reference
     private SlingRepository slingRepository;

     @Reference
     private JcrResourceResolverFactory jcrResourceResolverFactory ;

     /**
      *
      * @param inputFile - path to the pdf document stored at disk
      * @param outputFile - path to the pdf document where the output needs to be stored
      * @throws Exception
      */
     public void TimeStamp(String inputFile, String outputFile) throws Exception{

         File inFile = new File(inputFile);
         Document inDoc = new Document(inFile);

         File outFile = new File(outputFile);
         Document outDoc = null;

         Session adminSession = null;
         ResourceResolver resourceResolver = null;
         try {

              /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
              the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
              the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
              here we are using the same resource resolver
              */
              adminSession = slingRepository.loginAdministrative(null);
              resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

              VerificationTime verificationTime = getVerificationTimeForPades();
              ValidationPreferences dssPrefs = getValidationPreferences();

              //retrieve specifications for each of the services, you may pass null if you don't want to use that service
              //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
               outDoc = docAssuranceService.applyDocumentTimeStamp(inDoc, verificationTime, dssPrefs, resourceResolver, null);
         }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

         outDoc.copyToFile(outFile);

     }

  public  VerificationTime getVerificationTimeForPades(){

         return VerificationTime.SECURE_TIME_ELSE_CURRENT_TIME;

     }

 /**
       * sets ValidationPreferences
       */
      private static ValidationPreferences getValidationPreferences(){

         ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
         prefs.setPKIPreferences(getPKIPreferences());

         //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected

         return prefs;

     }

   /**
       * sets PKIPreferences
       */
     private static PKIPreferences getPKIPreferences(){
         PKIPreferences pkiPref = new PKIPreferencesImpl();
         pkiPref.setCRLPreferences(getCRLPreferences());
         pkiPref.setPathPreferences(getPathValidationPreferences());
         pkiPref.setOCSPPreferences(getOCSPPref());
         pkiPref.setTSPPreferences(getTspPref());
         return pkiPref;
     }

   /**
      * sets CRL Preferences
      */
     private static CRLPreferences getCRLPreferences(){

         CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
         crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
         crlPrefs.setGoOnline(true);
         return crlPrefs;
     }

     /**
      *
      * sets PathValidationPreferences
      */
     private static PathValidationPreferences getPathValidationPreferences(){
         PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
         pathPref.setDoValidation(true);
         return pathPref;

     }

   public static TSPPreferences getTspPref(){
   TSPPreferencesImpl tspPrefs=new TSPPreferencesImpl();
   char pass[]=new char[9];

   tspPrefs.setTspServerURL("TSPPrefs_ServerURL");
   tspPrefs.setUsername("TSPPrefs_Username");
   tspPrefs.setPassword(pass);
   tspPrefs.setSize(10240);
   return tspPrefs;
   }

     private static OCSPPreferencesImpl getOCSPPref(){
         OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
         ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
         return ocsp;
     }

}
```

### 獲取簽名 {#getting-signature}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果您不確定PDF文檔中的簽名欄位名稱或驗證名稱，請以寫程式方式檢索這些名稱。 簽名服務返回簽名欄位的完全限定名稱，如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**語法**: `getSignature(Document doc, String signatureFieldName, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>doc</code> </td>
   <td>包含PDF的文檔對象。<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>包含簽名的簽名欄位的名稱。 指定簽名欄位的完全限定名稱。 使用基於XFA表單的PDF文檔時，可以使用簽名欄位的部分名稱。 比如說， <code>form1[0].#subform[1].SignatureField3[3]</code> 可指定為 <code>SignatureField3[3]</code>。</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數。 僅當檔案已加密時，才需要此選項。</td>
  </tr>
 </tbody>
</table>

下面的Java代碼示例檢索位於PDF文檔中的給定簽名欄位的簽名資訊。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.client.types.PDFSignature;

/**
 * You can retrieve the names of all signature fields that are located in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are located in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field located in a PDF document.
 */

@Component
@Service(value=GetSignature.class)
public class GetSignature {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void GetSignature(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignature pdfSignature = docAssuranceService.getSignature(inDoc,"fieldName",null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 獲取簽名欄位清單  {#getting-signature-field-list-nbsp}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果不確定PDF文檔中的簽名欄位名稱，可以以寫程式方式檢索和驗證它們。 簽名服務返回簽名欄位的完全限定名稱，如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**語法**: `public List <PDFSignatureField> getSignatureFieldList (Document inDoc, UnlockOptions unlockOptions)`

**輸入參數**

| 參數 | 說明 |
|---|---|
| `inDoc` | 包含PDF的文檔對象 |
| `unlockOptions` | 包括解鎖加密檔案所需的參數。 僅當檔案已加密時，才需要此選項。 |

下面的Java代碼示例檢索位於PDF文檔中的簽名欄位的名稱。

```java
/*************************************************************************
 *
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------
**************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are located in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are located in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the names of signature fields located in a PDF document.
 */

@Component
@Service(value=GetSignatureFields.class)
public class GetSignatureFields {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getSignatureFields(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve the name of the document's signature fields
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        List fieldNames = docAssuranceService.getSignatureFieldList(inDoc,null);

        //Obtain the name of each signature field by iterating through the
        //List object
        Iterator iter = fieldNames.iterator();
        int i = 0 ;
        String fieldName="";
        while (iter.hasNext()) {
            PDFSignatureField signatureField = (PDFSignatureField)iter.next();
            fieldName = signatureField.getName();
            System.out.println("The name of the signature field is " +fieldName);
            i++;
        }
   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 修改簽名欄位  {#modifying-signature-fields-nbsp}

您可以修改位於PDF文檔中的簽名欄位。 修改簽名欄位涉及操作其簽名欄位鎖定字典值或種子值字典值。

欄位鎖定字典指定簽名欄位時鎖定的欄位清單。 鎖定的欄位禁止用戶編輯該欄位。 種子值字典包含在應用簽名時使用的約束資訊。 例如，您可以更改權限，以控制在不使簽名無效的情況下可能發生的操作。

通過修改現有簽名欄位，您可以編輯PDF文檔以反映不斷變化的業務需求。 例如，新業務要求要求在文檔簽名後鎖定所有文檔欄位。

**語法**: `public Document modifySignatureField(Document inDoc, String signatureFieldName, PDFSignatureFieldProperties pdfSignatureFieldProperties, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>包含PDF的文檔對象</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>簽名欄位的名稱。 此參數是必需的，不能接受空值。<br /> </td>
  </tr>
  <tr>
   <td><code>pdfSignatureFieldProperties</code></td>
   <td>指定有關 <code>PDFSeedValueOptionSpec</code> 和 <code>FieldMDPOptionSpec</code> 簽名欄位的值。</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數。 僅當檔案已加密時，才需要此選項。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例通過在簽名應用於簽名欄位時鎖定表單中的所有欄位來修改簽名欄位。

```java
/*************************************************************************
 *

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.FieldMDPAction;
import com.adobe.fd.signatures.client.types.FieldMDPOptionSpec;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.PDFSeedValueOptionSpec;
import com.adobe.fd.signatures.client.types.PDFSignatureFieldProperties;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.MissingSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignatureFieldSignedException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can modify signature fields that are located in a PDF document by using the Java API and web service API. Modifying a signature field involves
 * manipulating its signature field lock dictionary values or seed value dictionary values.
 * A field lock dictionary specifies a list of fields that are locked when the signature field is signed. A locked field prevents users from making
 * changes to the field. A seed value dictionary contains constraining information that is used at the time the signature is applied.
 * For example, you can change permissions that control the actions that can occur without invalidating a signature.
 * By modifying an existing signature field, you can make changes to the PDF document to reflect changing business requirements. For example,
 * a new business requirement may require locking all document fields after the document is signed.
 * This section explains how to modify a signature field by amending both field lock dictionary and seed value dictionary values.
 * Changes made to the signature field lock dictionary result in all fields in the PDF document being locked when a signature field is signed.
 * Changes made to the seed value dictionary prohibit specific types of changes to the document.
 *
 * The following Java code example modifies a signature field named SignatureField1 by locking all fields in the form when a signature is applied to the signature field and ensuring that no changes are allowed.
 * After the Signature service returns the PDF document that contains the modified signature field
 */

@Component
@Service(value=ModifySignatureField.class)
public class ModifySignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  *
  *
  */
 public void modifySignatureField(String inputFile, String outFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a PDFSignatureFieldProperties
        PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();

         //Create a PDFSeedValueOptionSpec object that stores
         //seed value dictionary information.
         PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();

         //Disallow changes to the PDF document. Any change to the document invalidates
         //the signature
         seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);

         //Create a FieldMDPOptionSpec object that stores
         //signature field lock dictionary information.
         FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();

         //Lock all fields in the PDF document
         fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);

         //Set dictionary information
         fieldProperties.setSeedValue(seedOptionsSpec);
         fieldProperties.setFieldMDP(fieldMDPOptionsSpec);

         //Modify the signature field
         //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
         Document modSignatureField =  docAssuranceService.modifySignatureField(inDoc,fieldName,fieldProperties,null);

        //save the modSignatureField
         modSignatureField.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 驗證PDF文檔  {#certifying-pdf-documents-nbsp}

您可以通過使用稱為認證簽名的特定類型的簽名來驗證PDF文檔，從而保護文檔的安全。 通過以下方式將經認證的簽名與數字簽名區別：

* 它必須是應用於PDF文檔的第一個簽名。 換句話說，當應用經認證的簽名時，文檔中的其他簽名欄位必須未簽名。 在PDF文檔中只允許一個經認證的簽名。 要簽名和認證PDF文檔，請在簽名前對其進行認證。 驗證PDF文檔後，可以對其他簽名欄位進行數字簽名。
* 文檔的作者或發起者可以指定文檔可以以某些方式進行修改，而不會使經認證的簽名失效。 例如，文檔可允許填寫表單或注釋。 如果作者指定不允許某種修改，Acrobat將限制用戶以這種方式修改文檔。 如果進行了此類修改，則認證簽名無效。 此外，當用戶開啟文檔時，Acrobat會發出警告。 （使用未經認證的簽名，不會阻止修改，並且正常的編輯操作不會使原始簽名無效。）
* 在簽名時，將掃描文檔中特定類型的內容，這些內容可能使文檔的內容模糊或具有誤導性。 例如，批注可能會使頁面上的某些文本模糊，這些文本對於瞭解正在認證的內容非常重要。 可以提供關於此類內容的解釋（法律證明）。

**語法**:

```java
secureDocument(Document inDoc, EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions, ReaderExtensionOptions readerExtensionOptions, UnlockOptions unlockOptions)
```

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>文檔輸入PDF文檔<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code> </td>
   <td>包括加密PDF文檔所需的參數<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>包括簽名/驗證PDF文檔所需的選項</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>包括Reader擴展PDF文檔所需的選項</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數。僅當檔案已加密時，才需要此參數。<br /> </td>
  </tr>
 </tbody>
</table>

以下代碼示例驗證基於PDF檔案的PDF文檔。

```java
/*************************************************************************

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * You can secure a PDF document by certifying it with a particular type of signature called a certified signature.
 * A certified signature is distinguished from a digital signature in these ways:
 *
 * It must be the first signature applied to the PDF document; that is, at the time the certified signature is applied, any other signature fields in the document must be unsigned.
 * Only one certified signature is permitted in a PDF document. If you want to sign and certify a PDF document, you must certify it before signing it.
 * After you certify a PDF document, you can digitally sign additional signature fields.
 *
 * The author or originator of the document can specify that the document can be modified in certain ways without invalidating the certified signature. For example,
 * the document may permit filling in forms or commenting. If the author specifies that a certain modification is not permitted, Acrobat restricts users from modifying the document
 * in that way. If such modifications are made, such as by using another application, the certified signature is invalid and Acrobat issues a warning when a user opens the document.
 * (With non-certified signatures, modifications are not prevented, and normal editing operations do not invalidate the original signature.)
 *
 * At the time of signing, the document is scanned for specific types of content that could make the contents of a document ambiguous or misleading. For example, an annotation could
 * obscure some text on a page that is important for understanding what is being certified. An explanation (legal attestation) can be provided about such content.
 * You can programmatically certify PDF documents by using the Signature service Java API or the Signature web service API. When certifying a PDF document, you must reference a security
 * credential that exists in the Credential service.
 *
 * Note: When certifying and signing the same PDF document, if the certify signature is not trusted, a yellow triangle appears next to the first sign signature when you open the PDF document in Acrobat or Adobe Reader.
 * The certifying signature must be trusted to avoid this situation.
 *
 * The following Java code example certifies a PDF document that is based on a PDF file.
 *
 * PreRequisites - Digital certificate for certifying the document has to be uploaded on AEM Key Store.
 *
 */

@Component
@Service(value=Certify.class)
public class Certify {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void certify(String inputFile, String outputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //we are not extending the reader in this case, so passing null
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    try {
    outDoc = docAssuranceService.secureDocument(inDoc, null, getCertificationOptions(resourceResolver), null,null);
   } catch (Exception e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
   }

        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA256;

        //Reason for signing/certifying
        String reason = "Reason";

        //location of the signer
        String location = "Location";

        //contact info of the signer
        String contactInfo = "Contact Info";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, false, true, true, TextDirection.AUTO);
        signatureOptions.setLockCertifyingField(true);
        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 保護文檔安全 {#securing-documents}

secureDocument使您能夠單獨或按特定順序以任何組合對PDF文檔進行加密、簽名/認證和閱讀器擴展。 要訪問任何此功能，請傳遞相應的參數。 如果為空，則假定不需要特定處理。

**使用密碼加密PDF文檔**

使用密碼加密PDF文檔時，用戶必須指定密碼才能在Adobe Reader或Acrobat開啟PDF文檔。 此外，在AEM Forms文檔服務的另一個操作使用該文檔之前，必須解鎖密碼加密的PDF文檔。

**用證書加密PDF文檔**

基於證書的加密允許您使用公鑰技術為特定收件人加密文檔。

可以為文檔授予不同的權限。 公鑰技術使加密的許多方面成為可能。

算法用於生成兩個大數，即具有以下屬性的鍵：

* 一個密鑰用於加密一組資料。 以後，只能使用其他密鑰解密資料。
* 一把鑰匙和另一把鑰匙是無法區分的。
* 其中一個密鑰用作用戶的私鑰。 只有用戶才能訪問此密鑰，這一點非常重要。
* 另一個密鑰是用戶的公鑰，可以與他人共用。

公鑰證書包含用戶的公鑰和標識資訊。 X.509格式用於儲存證書。 證書通常由證書頒發機構(CA)頒發和數字簽名，該機構是一個被認可的實體，提供對證書有效性的信任度。 證書的到期日期已過，在此日期之後，證書不再有效。

此外，證書吊銷清單(CRL)提供了在證書過期之前已吊銷的證書的資訊。 CRL由證書頒發機構定期發佈。 還可以通過網路通過線上證書狀態協定(OCSP)檢索證書的吊銷狀態。

>[!NOTE]
>
>在使用證書加密PDF文檔之前，必須確保將證書添加到信AEM任儲存。

**對PDF文檔應用使用權限**

可以使用PDF擴展Java客戶端API和Web服務對Reader文檔應用使用權限。 使用權限與預設在Acrobat但在Adobe Reader不可用的功能有關，例如向表單添加註釋或填寫表單域並保存表單的功能。 對其應用了使用權限的PDF文檔稱為啟用權限的文檔。 在Adobe Reader開啟啟用權限的文檔的用戶可以執行為該特定文檔啟用的操作。

在Reader使用證書擴展PDF文檔之前，必須確保將證書添加到密鑰AEM庫。

**數字簽名PDF文檔**

數字簽名可以應用於PDF文檔以提供安全級別。 數字簽名與手寫簽名一樣，提供了一種手段，使簽名者能夠識別自己並就文檔發表聲明。

用於對文檔進行數字簽名的技術有助於確保簽名者和收件人都清楚簽名的內容，並確信文檔自簽名後沒有更改。

PDF檔案採用公鑰技術簽署。 簽名者有兩個密鑰：公鑰和私鑰。 私鑰儲存在用戶憑據中，簽名時必須可用。

公鑰儲存在用戶的證書中，收件人必須可以使用該證書來驗證簽名。 有關已吊銷證書的資訊可在由證書頒發機構(CA)分發的證書吊銷清單(CRL)和線上證書狀態協定(OCSP)響應中找到。 簽名時間可以從稱為時間戳頒發機構的可信源獲得。

>[!NOTE]
>
>在對PDF文檔進行數字簽名之前，必須確保在密鑰庫中添加AEM憑據。 憑據是用於簽名的私鑰。

>[!NOTE]
>
>AEM Forms也支援 *[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)* 用於數字簽名PDF文檔的規範。

**驗證PDF文檔**

您可以通過使用稱為認證簽名的特定類型的簽名來驗證PDF文檔，從而保護文檔的安全。 通過以下方式將經認證的簽名與數字簽名區別：

它必須是應用於PDF檔案的第一個簽名；即，在應用經認證的簽名時，文檔中的任何其他簽名欄位都必須未簽名。

在PDF文檔中只允許一個經認證的簽名。 如果要簽名和認證PDF文檔，則必須在簽名前對其進行認證。

驗證PDF文檔後，可以對其他簽名欄位進行數字簽名。

文檔的作者或發起者可以指定文檔可以以某些方式進行修改，而不會使經認證的簽名失效。

例如，文檔可允許填寫表單或注釋。 如果作者指定不允許進行某種修改，

Acrobat限制用戶以這種方式修改文檔。 如果進行此類修改，例如使用其他應用程式，則經認證的簽名無效，並且當用戶開啟文檔時，Acrobat發出警告。 （使用未經認證的簽名，不會阻止修改，並且正常的編輯操作不會使原始簽名無效。）

在簽名時，將掃描文檔中特定類型的內容，這些內容可能使文檔的內容模糊或具有誤導性。

例如，批注可能會使頁面上的某些文本模糊，這些文本對於瞭解正在認證的內容非常重要。 可以提供關於此類內容的解釋（法律證明）。

>[!NOTE]
>
>在對PDF文檔進行數字簽名之前，必須確保在密鑰庫中添加AEM憑據。 憑據是用於簽名的私鑰。

**語法**:

```java
secureDocument(Document inDoc,
 EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions,
 ReaderExtensionOptions readerExtensionOptions,
 UnlockOptions unlockOptions)
```

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>文檔輸入PDF文檔<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code> </td>
   <td>包括加密PDF文檔所需的參數<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>包括簽名/驗證PDF文檔所需的選項</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>包括Reader擴展PDF文檔所需的選項</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包括解鎖加密檔案所需的參數。僅當檔案已加密時，才需要此參數。<br /> </td>
  </tr>
 </tbody>
</table>

**示例1**:此示例用於執行密碼加密、驗證簽名欄位和Reader擴展PDF文檔。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.PasswordEncryptionCompatability;
import com.adobe.fd.encryption.client.PasswordEncryptionOption;
import com.adobe.fd.encryption.client.PasswordEncryptionOptionSpec;
import com.adobe.fd.encryption.client.PasswordEncryptionPermission;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * password encryption, certifying a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptCertifyExtend.class)
public class PassEncryptCertifyExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void SecureDocument(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getPassEncryptionOptions(), getCertificationOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getPassEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

  //Create a PasswordEncryptionOptionSpec object that stores encryption run-time values
        PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();

        //Specify the PDF document resource to encrypt
        passSpec.setEncryptOption(PasswordEncryptionOption.ALL);

        //Specify the permission associated with the password
        //These permissions enable data to be extracted from a password
        //protected PDF form
        List<PasswordEncryptionPermission> encrypPermissions = new ArrayList<PasswordEncryptionPermission>();
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_ADD);
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_MODIFY);
        passSpec.setPermissionsRequested(encrypPermissions);

        //Specify the Acrobat version
        passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);

        //Specify the password values
        passSpec.setDocumentOpenPassword("OpenPassword");
        passSpec.setPermissionPassword("PermissionPassword");

        //Set the encryption type to Password Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_PASSWORD);
        encryptionOptions.setPasswordEncryptionOptionSpec(passSpec);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

**示例2**:此示例用於執行PKI加密、簽名域和Reader擴展PDF文檔。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.CertificateEncryptionCompatibility;
import com.adobe.fd.encryption.client.CertificateEncryptionIdentity;
import com.adobe.fd.encryption.client.CertificateEncryptionOption;
import com.adobe.fd.encryption.client.CertificateEncryptionOptionSpec;
import com.adobe.fd.encryption.client.CertificateEncryptionPermissions;
import com.adobe.fd.encryption.client.Recipient;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * certificate encryption, signing a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for encrypting the document has to be uploaded on Granite Trust Store
       Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptSignExtend.class)
public class PassEncryptSignExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void CertEncryptSignReaderExtend(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getCertEncryptionOptions(), getSignatureOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getCertEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

        //Set the encryption type to Certificate Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_CERTIFCATE);

  //Set the List that stores PKI information
  List<CertificateEncryptionIdentity> pkiIdentities = new ArrayList<CertificateEncryptionIdentity>();

  //Set the Permission List
  List<CertificateEncryptionPermissions> permList = new ArrayList<CertificateEncryptionPermissions>();
  permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;

  //Create a Recipient object to store certificate information
  Recipient recipient = new Recipient();

  //Specify the alias of the public certificate present in the trust store that is used to encrypt the document
  recipient.setX509Cert("alias");
  /*
   * An alternative to add a certificate is by providing the alias
   * of the certificate stored in AEM trust store.
   * recipient.setAlias(alias);
   */

  //Create an EncryptionIdentity object
  CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
  encryptionId.setPerms(permList);
  encryptionId.setRecipient(recipient);

  //Add the EncryptionIdentity to the list
  pkiIdentities.add(encryptionId);

  //Set encryption run-time options
  CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
  certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
  certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_9);

  //Set the certificate encryption option
  encryptionOptions.setCertOptionSpec(certOptionsSpec)

  //Set the PKI Identities in encryption Options
        encryptionOptions.setPkiIdentities(pkiIdentities);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

如果讀取器擴展PDF文檔時顯示以下錯誤消息：

```javascript
org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.ThreadDeath: null at com.adobe.internal.pdftoolkit.services.javascript.GibsonContextFactory.observeInstructionCount(GibsonContextFactory.java:138)
```

它表示Reader擴展服務無法在定義的超時間隔內執行文檔中使用的JavaScript。

使用以下方式管理PDF文檔中為JavaScripts定義的超時間隔：

```javascript
ReaderExtensionsOptionSpec optionSpec = new ReaderExtensionsOptionSpec(usageRights, message);
optionSpec.setJsScriptExecutionTimeoutInterval(100);
```

其中100指為執行JavaScripts而定義的超時間隔（秒）。 為超時間隔設定適當的值。

### 獲取憑據使用權限 {#getting-credential-usage-rights}

獲取給定指定憑據的使用權限資訊 `credentialAlias`，從 `SecureDocument` API。

**語法**: `getCredentialUsageRights(String credentialAlias, ResourceResolver resourceResolver)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>credentialAlias</code> </td>
   <td>的 <code>credentialAlias</code> 指定憑據。<br /> </td>
  </tr>
  <tr>
   <td><code>credentialPassword</code> </td>
   <td>如果憑據已加密，則憑據的密碼；如果憑據未加密，則需要使用空值。<br /> </td>
  </tr>
 </tbody>
</table>

以下示例讀取指定憑據的使用權限資訊。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 *
 */
@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
 private ResourceResolverFactory resourceResolverFactory;
public void getCredentialUsageRights() {
  try {

   GetUsageRightsResult usageRightsResult = docAssuranceService.getCredentialUsageRights("production",
     resourceResolverFactory.getAdministrativeResourceResolver(null));

   System.out.println("Credential usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  }
 }
}
```

### 獲取文檔使用權限 {#getting-document-usage-rights}

要獲取給定文檔的使用權限資訊，請從 `docAssuranceService`API。

**語法**: `getDocumentUsageRights(Document inDocument, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDocument</code> </td>
   <td>要從中獲取使用權限資訊的文檔<br /> </td>
  </tr>
 </tbody>
</table>

下面的示例代碼返回文檔的使用權限資訊。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void getDocumentUsageRights() {
  Document inputDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/GetUsageRightsInfo/02_fromAcrobat7.0.8_Acro700_UB8_BS_signed_commenting.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   GetUsageRightsResult usageRightsResult = docAssuranceService.getDocumentUsageRights(inputDocument, unlockOptions);

   System.out.println("Document usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  } finally {
//   if (inputDocument != null) {
//    inputDocument.dispose(); //dispose off the document.
//   }
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

### 刪除使用權限 {#removing-usage-rights}

通過調用 `removeUsageRights`API來自 `docAssuranceService`API。

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDocument</code> </td>
   <td>要從中刪除使用權限的文檔。<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code> </td>
   <td>包括解鎖加密檔案所需的參數。 僅當檔案已加密時，才需要此選項。<br /> </td>
  </tr>
 </tbody>
</table>

下面的示例刪除給定文檔的使用權限。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void removeDocumentUsageRights() {
  Document inputDocument = null;
  Document outDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/RemoveUsageRights/01_Ubiquitized_50-267_PDF1.5_UB2_Rights.pdf";

   //Name of the output file where result will be saved.
   String outputFileName = "C:/RETest/output/samples/removeUsageRightsOutput.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   //Specify null encryption options and signatures options.
   //If requirement is also to encrypt and sign the document then, corresponding options can also be specified.
   outDocument = docAssuranceService.removeUsageRights(inputDocument, unlockOptions);

   File outputdir = new File("C:/RETest/output/samples");
   outputdir.mkdirs();

   outDocument.copyToFile(new File(outputFileName));
  } catch (Exception e) {
   e.printStackTrace();
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

#### 驗證數字簽名 {#verifying-digital-signatures}

可以驗證數字簽名，以確保簽名的PDF文檔未被修改，並且數字簽名有效。 驗證數字簽名時，可以檢查簽名的狀態和簽名的屬性，如簽名者的身份。 在信任數字簽名之前，建議您驗證它。 驗證數字簽名時，請參考包含數字簽名的PDF文檔。

**語法**: `verify( inDoc, signatureFieldName, revocationCheckStyle, verificationTime, dssPrefs, ResourceResolver resourceResolver)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>包含PDF的文檔對象<br /> </td>
  </tr>
  <tr>
   <td><code class="code">signatureField
      Name</code> </td>
   <td>要驗證的簽名欄位的名稱。 可以指定完全限定的名稱或部分名稱<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>控制驗證期間遇到的證書的吊銷檢查的選項</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>簽名的驗證時間</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>控制各種驗證配置的首選項。 對於加密文檔，使用 <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>到花崗岩信任儲存的資源解析器</td>
  </tr>
 </tbody>
</table>

此示例代碼使用 `DocAssuranceService` 驗證加密的PDF文檔中的簽名欄位。

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.IdentityInformation;
import com.adobe.fd.signatures.client.types.IdentityStatus;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of a signature field in an already Encrypted PDF Document
 *
 * Digital signatures can be verified to ensure that a signed PDF document was not modified and that the digital signature is valid.
 * When verifying a digital signature, you can check the signature's status and the signature's properties, such as the signer's identity.
 * Before trusting a digital signature, it is recommended that you verify it. When verifying a digital signature, reference a PDF document
 * that contains a digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyFieldEncryptedPDF.class)
public class VerifyFieldEncryptedPDF {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyFieldEncryptedPDF(String inputFile,String fieldName) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

         //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

           //Specify the name of the signature field

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.AlwaysCheck;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFSignatureVerificationInfo  signInfo = docAssuranceService.verify(
                 inDoc,
                 fieldName,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get the Signature Status
             SignatureStatus sigStatus = signInfo.getStatus();
             String myStatus="";

             //Determine the status of the signature
             if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                 myStatus = "The signatures located in the dynamic PDF form are unknown";
             else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                 myStatus = "The signatures located in the PDF document are unknown";
             else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                 myStatus = "The signatures located in a certified PDF form are valid";
             else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                 myStatus = "The signatures located in a signed dynamic PDF form are valid";
             else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                 myStatus = "The signatures located in a certified PDF document are valid";
             else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                 myStatus = "The signatures located in a signed PDF document are valid";
             else if (sigStatus == SignatureStatus.SignatureFormatError)
                 myStatus = "The format of a signature in a signed document is invalid";
             else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                 myStatus = "No changes were made to the signed dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                 myStatus = "No changes were made to the signed PDF document";
             else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified PDF document";
             else if (sigStatus == SignatureStatus.DocSigWithChanges)
                 myStatus = "There were changes to a signed PDF document";
            else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                 myStatus = "There were changes made to the PDF document.";

             //Get the signature type
             SignatureType sigType = signInfo.getSignatureType();
             String myType = "";

             if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                    myType="Certification";
             else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                    myType="Recipient";

             //Get the identity of the signer
             IdentityInformation signerId = signInfo.getSigner();
             String signerMsg = "";

            if (signerId.getStatus() == IdentityStatus.UNKNOWN)
                signerMsg = "Identity Unknown";
            else if (signerId.getStatus() == IdentityStatus.TRUSTED)
                signerMsg = "Identity Trusted";
            else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
                signerMsg = "Identity Not Trusted";

            //Get the Signature properties returned by the Signature service
            SignatureProperties sigProps = signInfo.getSignatureProps();
            String signerName =  sigProps.getSignerName();

           System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        pkiPref.setOCSPPreferences(getOCSPPref());
        pkiPref.setTSPPreferences(getTspPref());
        return pkiPref;
    }

    private static TSPPreferences getTspPref(){
     TSPPreferencesImpl tsp = new TSPPreferencesImpl();
     tsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return tsp;
    }
    private static OCSPPreferencesImpl getOCSPPref(){
     OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
     ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return ocsp;
    }
    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(true);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 驗證多個數字簽名 {#verifying-multiple-digital-signatures}

用AEM於驗證PDF文檔中的數字簽名。 如果PDF文檔受到業務流程的影響，需要多個簽名者的簽名，則該文檔可以包含多個數字簽名。 例如，財務交易要求貸款幹事和經理簽字。 您可以使用簽名服務API驗證PDF文檔中的所有簽名。 驗證多個數字簽名時，可以檢查每個簽名的狀態和屬性。 在信任數字簽名之前，Adobe建議您驗證它。

**語法**: `verifyDocument(Document doc, RevocationCheckStyle revocationCheckStyle, VerificationTime verificationTime, ValidationPreferences prefStore, ResourceResolver resourceResolver)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>包含PDF的文檔對象<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>控制驗證期間遇到的證書的吊銷檢查的選項</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>簽名的驗證時間</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>控制各種驗證配置的首選項。 對於加密文檔，使用 <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>到花崗岩信任儲存的資源解析器</td>
  </tr>
 </tbody>
</table>

以下示例代碼使用DocAssuranceService驗證已加密的PDF文檔中的簽名欄位。

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;
import java.util.Iterator;
import java.util.List;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFDocumentVerificationInfo;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of all the signature fields in an already Encrypted PDF Document
 *
 * Assume that a PDF document contains multiple digital signatures as a result of a business process that requires signatures from multiple
 * signers. For example, consider a financial transaction that requires both a loan officer's and a manager's signature. You can use the
 * Signature service Java API or web service API to verify all signatures within the PDF document. When verifying multiple digital signatures,
 * you can check the status and properties of each signature. Before you trust a digital signature, it is recommended that you verify it. It
 * is recommended that you are familiar with verifying a single digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyEncryptedPDFDoc.class)
public class VerifyEncryptedPDFDoc {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyEncryptedPDFDoc(String inputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.CheckIfAvailable;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFDocumentVerificationInfo  docInfo = docAssuranceService.verifyDocument(
                 inDoc,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get a list of all signatures that are located in the PDF document
             List allSignatures = docInfo.getVerificationInfos();

           //Create an Iterator object and iterate through
           //the List object
           Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();

           while (iter.hasNext()) {
                  PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();

                  //Get the Signature Status
                     SignatureStatus sigStatus = signInfo.getStatus();
                     String myStatus="";

                   //Determine the status of the signature
                     if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                         myStatus = "The signatures located in the dynamic PDF form are unknown";
                     else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                         myStatus = "The signatures located in the PDF document are unknown";
                     else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                         myStatus = "The signatures located in a certified PDF form are valid";
                     else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                         myStatus = "The signatures located in a signed dynamic PDF form are valid";
                     else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                         myStatus = "The signatures located in a certified PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                         myStatus = "The signatures located in a signed PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignatureFormatError)
                         myStatus = "The format of a signature in a signed document is invalid";
                     else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                         myStatus = "No changes were made to the signed dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                         myStatus = "No changes were made to the signed PDF document";
                     else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified PDF document";
                     else if (sigStatus == SignatureStatus.DocSigWithChanges)
                         myStatus = "There were changes to a signed PDF document";
                    else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                         myStatus = "There were changes made to the PDF document.";

                     //Get the signature type
                    SignatureType sigType = signInfo.getSignatureType();
                    String myType = "";

                    if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                        myType="Certification";
                    else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                        myType="Recipient";

                    //Get the Signature properties returned by the Signature service
                    SignatureProperties sigProps = signInfo.getSignatureProps();
                    String signerName =  sigProps.getSignerName();

                   System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
               }
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the document is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 刪除數字簽名 {#removing-digital-signatures}

只有在刪除以前的數字簽名後，才能將新的數字簽名應用於簽名欄位。 無法覆蓋數字簽名。 如果嘗試將數字簽名應用於已包含簽名的簽名欄位，則會發生異常。

**語法**: `clearSignatureField(Document inDoc, String signatureFieldName, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>包含PDF的文檔對象<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>簽名欄位的名稱<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code> </td>
   <td>包括解鎖加密檔案所需的參數，僅當檔案已加密時才需要此參數<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例從簽名欄位中刪除數字簽名。

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file
*from a source other than Adobe, then your use, modification, or distribution of it requires
*the prior written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures must be removed from a signature field before a newer digital signature can be applied.
 * A digital signature cannot be overwritten.
 * If you attempt to apply a digital signature to a signature field that contains a signature, an exception occurs
 *
 *The following Java code example removes a digital signature from a signature field named SignatureField1.
 *The name of the PDF file that contain the signature field is LoanSigned.pdf
 */

@Component
@Service(value=ClearSignatureField.class)
public class ClearSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;
 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  * @throws Exception
  */
 public void clearSignatureField(String inputFile, String outFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Clear the signature field
        //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        Document outPDF = docAssuranceService.clearSignatureField(inDoc,fieldName,null);

        //save the outPDF
        outPDF.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 正在獲取驗證簽名欄位 {#getting-certifying-signature-field}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果您不確定位於PDF文檔中的簽名欄位名稱或要驗證這些名稱，可以以寫程式方式檢索它們。 簽名服務返回簽名欄位的完全限定名稱，如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**語法**: `getCertifyingSignatureField(Document inDoc, UnlockOptions unlockOptions)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>包含PDF的文檔對象。<br /> </td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>UnlockOptions包括解鎖加密檔案所需的參數。 僅當檔案已加密時，才需要此選項。</td>
  </tr>
 </tbody>
</table>

下面的Java代碼示例檢索用於驗證文檔的簽名欄位。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are located in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are located in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the ignature field that was used to certify the document.
 */

@Component
@Service(value=GetCertifyingSignatureField.class)
public class GetCertifyingSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getCertifyingSignatureField(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignatureField pdfSignature = docAssuranceService.getCertifyingSignatureField(inDoc,null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 獲取PDF加密類型 {#getting-pdf-encryption-type}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果您不確定位於PDF文檔中的簽名欄位名稱或要驗證這些名稱，可以以寫程式方式檢索它們。 簽名服務返回簽名欄位的完全限定名稱，如 `asform1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**語法**: `void getPDFEncryption(Document inDoc)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>作為輸入提供的文檔。 它可能被加密，也可能不被加密。<br /> </td>
  </tr>
 </tbody>
</table>

下面的Java代碼示例檢索位於PDF文檔中的給定簽名欄位的簽名資訊。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.encryption.client.EncryptionTypeResult;

/**
 * You can retrieve the names of all signature fields that are located in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are located in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field located in a PDF document.
 */

@Component
@Service(value=GetPDFEncryption.class)
public class GetPDFEncryption {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getPDFEncryption(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        EncryptionTypeResult encryptionTypeResult = docAssuranceService.getPDFEncryption(inDoc);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 正在從PDF中刪除密碼加密 {#removing-password-encryption-from-pdf}

從PDF文檔中刪除基於密碼的加密，以便用戶在Adobe Reader或Acrobat開啟PDF文檔，而無需指定密碼。 從PDF文檔中刪除基於密碼的加密後，文檔不再安全。

**語法**: `Document removePDFPasswordSecurity (Document inDoc,String password)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>作為輸入提供的文檔。 它必須受密碼保護。<br /> </td>
  </tr>
  <tr>
   <td><code>password</code> </td>
   <td>開啟的文檔或用於從文檔中刪除安全性的權限密碼。<br /> </td>
  </tr>
 </tbody>
</table>

下面的代碼示例從PDF文檔中刪除基於密碼的加密。

```java
    package com.adobe.docassurance.samples;

    import java.io.File;
    import java.io.FileNotFoundException;
    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.jcr.api.SlingRepository;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes password-based encryption from a PDF document.
    * The master password value used to remove password-based encryption is PermissionPassword
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePasswordEncryption.class)
    public class RemovePasswordEncryption {

    // Create reference for DocAssuranceService
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    /**
    * The below sample code demonstrates removing password encryption from a PDF using AEM EncryptionService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_out.pdf"
    * @throws Exception
    */
    public void removePasswordEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

        try{

        String password = "PermissionPassword"; //master password with which the pdf was encrypted
                    //in case if the pdf is encrypted only with user password, specify the
                    //user password
        //Remove password-based encryption from the PDF document
        outDoc = docAssuranceService.removePDFPasswordSecurity(inDoc,password);

        }finally{
                    /**
                    * always close the PDFDocument object after your processing is done.
                    */
                    if(inDoc != null){
                        inDoc.close();
                    }

            }

            outDoc.copyToFile(outFile);

    }

    }
```

### 正在刪除證書加密 {#removing-certificate-encryption}

您可以從PDF文檔中刪除基於證書的加密，以便用戶可以在Adobe Reader或Acrobat開啟PDF文檔。 要從使用證書加密的PDF文檔中刪除加密，請引用私鑰。 從PDF文檔中刪除加密後，加密不再安全。

**語法**: `removePDFCertificateSecurity(Document inDoc, String alias, ResourceResolver resourceResolver)`

**輸入參數**

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>inDoc</code> </td>
   <td>表示證書加密的PDF文檔的文檔對象。<br /> </td>
  </tr>
  <tr>
   <td><code>alias</code> </td>
   <td>與用於從PDF文檔中刪除基於證書的加密的Granite Trust Store中的密鑰相對應的別名。<br /> </td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>ResourceResolver訪問特定用戶的密鑰儲存以獲取憑據。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例從PDF文檔中刪除基於證書的加密。

```java
    package com.adobe.docassurance.samples;

    import java.io.File;

    import javax.jcr.Session;

    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.api.resource.ResourceResolver;
    import org.apache.sling.jcr.api.SlingRepository;
    import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes certificate-based encryption from a PDF document
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePKIEncryption.class)
    public class RemovePKIEncryption {

    // Create reference for docAssuranceServiceInterface
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    @Reference
        private JcrResourceResolverFactory jcrResourceResolverFactory ;

    /**
    * The below sample code demonstrates encrypting PDF with Password using AEM docAssuranceService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_Encrypted.pdf"
    *
    * @throws Exception
    */
    public void removePKIEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

            Session adminSession = null;
            ResourceResolver resourceResolver = null;
            try{
        adminSession = slingRepository.loginAdministrative(null);
        resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

        //Remove certificate-based encryption from the PDF document
        /**
        * Here the alias("encryption") of the private credential stored in the keystore of the
        * user has been provided with the user's resource resolver
        */
        outDoc = docAssuranceService.removePDFCertificateSecurity(inDoc, "encryption",resourceResolver);

            }catch(Exception e){

            // TODO Auto-generated catch block
            }finally{
                /**
                * always close the PDFDocument object after your processing is done.
                */
                if(inDoc != null){
                    inDoc.close();
                }
                if(adminSession != null && adminSession.isLive()){
                    if(resourceResolver != null){
                        resourceResolver.close();
                    }
                    adminSession.logout();
                }
            }

            outDoc.copyToFile(outFile);
    }

    }
```

## 輸出服務 {#output-service}

輸出服務提供API以.pdf、.pcl、.zpl和.ps格式呈現XDP檔案。 該服務支援以下API:

* **[生成PDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p):** 通過將表單設計與儲存在網路位置、本地檔案系統或HTTP位置上的資料合併為文本值，生成PDF文檔。

* **[生成PDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p):** 通過將表單設計與儲存在應用程式中的資料合併來生成PDF文檔。
* **[generatePDFOutputBatch](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutputbatch-p):** 將表單設計與資料合併以建立PDF文檔。 可選地，為每個記錄生成元資料檔案或將輸出保存到PDF檔案。
* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p):** 從儲存在網路位置、本地檔案系統或HTTP位置上的表單設計和資料檔案生成PCL、PostScript或ZPL輸出作為文本值。

* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p):** 從儲存在應用程式中的表單設計和資料檔案生成PCL、PostScript和ZPL輸出。

### 生成PDFOutput {#generatepdfoutput}

generatePDFOutput API通過將表單設計與資料合併來生成PDF文檔。 可選地，為每個記錄生成元資料檔案或將輸出保存到PDF檔案。 將generatePDFOutput API用於儲存在網路位置、本地檔案系統或HTTP位置上的表單設計或資料作為文字值。 如果表單設計和XML資料儲存在應用程式中，請使用 [生成PDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API。

**語法：** `Document generatePDFOutput(String uriOrFileName, Document data, PDFOutputOptions options);`

#### 輸入參數 {#input-parameters}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>uri或檔案名</td>
   <td>指定輸入檔案的路徑和名稱。 檔案可以是PDF或XDP類型。 如果僅指定檔案名，則讀取該檔案時將與選項中指定的contentRoot相關。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>包含與PDF文檔合併的資料的XML檔案。<br /> </td>
  </tr>
  <tr>
   <td>選項</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF變數的值。 選項參數接受PDFOutputOptions類型的對象。 <br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例通過將表單設計與儲存在XML檔案中的資料合併而生成PDF文檔。

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput(String contentRoot,File inputXML,String templateStr,String acrobatVersion,String tagged,String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

    try {

            PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);         if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

            {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {             option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

            }

            if (tagged.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if (linearized.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if(locale!=null)

            {

                option.setLocale(locale);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePDFOutput(templateStr,new Document(in),option);         File toSave = new File(outputFolder+"Output.pdf");

            doc.copyToFile(toSave);

            return toSave;

        } catch (OutputServiceException e) {

            e.printStackTrace();

        }catch (FileNotFoundException e) {

            e.printStackTrace();

        } catch (IOException e) {

            e.printStackTrace();

        }finally{

                    doc.dispose();

        }

        return null;

    }
```

### 生成PDFOutput {#generatepdfoutput-1}

generatePDFOutput API通過將表單設計與資料合併來生成PDF文檔。 或者，為每個記錄生成元資料檔案或將輸出保存到PDF檔案。 將generatePrintedOutput API用於儲存在應用程式中的表單設計或資料。 如果表單設計和XML資料儲存在網路位置、本地或HTTP位置作為文本值，請使用 [生成PDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API。

**語法：** `Document generatePDFOutput(Document inputdocument, Document data, PDFOutputOptions options)`

#### 輸入參數 {#input-parameter}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定輸入檔案的路徑和名稱。 檔案可以是PDF或XDP類型。 如果僅指定檔案名，則讀取該檔案時將與選項中指定的contentRoot相關。 <br /> </td>
  </tr>
  <tr>
   <td>資料</td>
   <td>包含與PDF文檔合併的資料的XML檔案。<br /> </td>
  </tr>
  <tr>
   <td>選項</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF變數的值。 選項參數接受PDFOutputOptions類型的對象。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例通過將表單設計與儲存在XML檔案中的資料合併而生成PDF文檔。

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput2(String contentRoot, File inputXML, File templateStr, String acrobatVersion, String tagged, String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

        try {

                PDFOutputOptions option = new PDFOutputOptions();             option.setContentRoot(contentRoot);
                if(locale!=null)

                {

                    option.setLocale(locale);

                }

                if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

                {

                    option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

                }

                if (tagged.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                if (linearized.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                InputStream inputXMLStream = new FileInputStream(inputXML);

                InputStream templateStream = new FileInputStream(templateStr);;

                doc = outputService.generatePDFOutput(new Document(templateStream),new             Document(inputXMLStream),option);

                        File toSave = new File(outputFolder,"Output.pdf");

                        doc.copyToFile(toSave);

                        return toSave;

                    } catch (OutputServiceException e) {

                            e.printStackTrace();

                }catch (FileNotFoundException e) {

                            e.printStackTrace();

                } catch (IOException e) {

                            e.printStackTrace();

                }finally{

                                doc.dispose();

                }

                    return null;

    }
```

### generatePDFOutputBatch {#generatepdfoutputbatch}

將表單設計與資料合併以建立PDF文檔。 可選地，為每個記錄生成元資料檔案或將輸出保存到PDF檔案。 使用generatePDFOutputBatch API將儲存在網路位置、本地檔案系統或HTTP位置上的表單設計或資料用作文字值。

**語法：** `BatchResult generatePDFOutputBatch(Map templates, Map data, PDFOutputOptions options, BatchOptions batchOptions);`

#### 輸入參數 {#input-parameters-1}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>模板<br /> </td>
   <td>指定密鑰和模板檔案名的映射。<br /> </td>
  </tr>
  <tr>
   <td>資料</td>
   <td>指定鍵和資料文檔的映射。 如果鍵不為null，則使用模板映射中指定的相應鍵的模板來呈現資料文檔。 </td>
  </tr>
  <tr>
   <td>選項</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF變數的值。 選項參數接受PDFOutputOptions類型的對象。</td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>指定變數的值 <code>generateManyFiles</code>。 設定generateManyFiles標誌以生成多個檔案。 選項參數接受BatchOptions類型的對象。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例通過將表單設計與儲存在XML檔案中的資料合併來生成PDF文檔。

```java
private ArrayList generatePDFBatch(String contentRoot,String multipleFiles) {

String outputFolder="C:/Output";

    try {

        PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);

        Map templates = new LinkedHashMap();

        Map data = new LinkedHashMap();

        String template1 = "PurchaseOrder.xdp"; String template2 = "CardApp.xdp";         templates.put(template1.substring(0, template1.indexOf(".xdp")),template1);         templates.put(template1.substring(0, template2.indexOf(".xdp")),template2);

        File inputXML1 = new File("c:/InputFolder/PurchaseOrder.xml");

        File inputXML2 = new File("c:/InputFolder/CardApp.xml");

        InputStream in1 = new FileInputStream(inputXML1);

        InputStream in2 = new FileInputStream(inputXML2);

        data.put(template1.substring(0, template1.indexOf(".xdp")),new         Document((in1))); data.put(template1.substring(0,         template1.indexOf(".xdp")),new Document((in2))); BatchOptions bo = new         BatchOptions(); BatchResult ret=null;         if(multipleFiles.equalsIgnoreCase("true"))

        {

            bo.setGenerateManyFiles(true);

            ret = outputService.generatePDFOutputBatch(templates, data, option, bo);

        } else {

            ret = outputService.generatePDFOutputBatch(templates, data, option, new             BatchOptions());

        }

        ArrayList outputs = new ArrayList();

        int counter=0;

        if(ret.getMetaDataDoc() !=null ){

        File toSave = new File(outputFolder+"Output.xml");

        ret.getMetaDataDoc().copyToFile(toSave);

        outputs.add(toSave);

        List<Document> list = ret.getGeneratedDocs();

        for(Document doc:list){

        File toSave = new File(outputFolder,"Output"+"_"+counter+".pdf");         doc.copyToFile(toSave);                    outputs.add(toSave);

        counter++;

        doc.dispose();

        }

        return outputs;

       } catch (OutputServiceException e) {

            e.printStackTrace();

       }catch (FileNotFoundException e) {

            e.printStackTrace();

       }catch (IOException e) {

            e.printStackTrace();

       }

       return null;

}
```

### generatePrintedOutput {#generateprintedoutput}

從表單設計和資料檔案生成PCL、PostScript和ZPL輸出。 資料檔案與表單設計合併並格式化以打印。 您可以將輸出直接發送到打印機或另存為檔案。 將generatePrintedOutput API用於儲存在應用程式中的表單設計或資料。

**語法：** `Document generatePrintedOutput(String uriOrFileName, Document data, PrintedOutputOptions);`

#### 輸入參數 {#input-parameters-2}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>uri或檔案名<br /> </td>
   <td>指定輸入檔案的路徑和名稱。 如果僅指定檔案名，則讀取該檔案時將與選項中指定的contentRoot相關。 檔案可以是PDF或XDP類型。<br /> </td>
  </tr>
  <tr>
   <td>資料</td>
   <td>包含與PDF文檔合併的資料的XML檔案。<br /> </td>
  </tr>
  <tr>
   <td>選項</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF變數的值。 選項參數接受PrintedOutputOptions類型的對象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例從表單設計和資料生成PCL、PostScript和ZPL輸出。 輸出類型取決於傳遞給 `printConfig`的下界。

```java
@Reference private OutputService outputService;

private File generatePrintedOutput(String contentRoot,File inputXML,String templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

    try {

            PrintedOutputOptions options = new PrintedOutputOptions();                           options.setContentRoot(contentRoot);

            if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {

                            options.setPrintConfig(PrintConfig.HP_PCL_5e);

                     }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePrintedOutput(templateStr,new             Document(in),options);

            in.close();

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return  toSave;

        } catch (OutputServiceException e) {

             e.printStackTrace();

        }catch (FileNotFoundException e) {

             e.printStackTrace();

        }catch (IOException e) {

             e.printStackTrace();

        }finally{

             doc.dispose();

        }

        return null;

}
```

### generatePrintedOutput {#generateprintedoutput-1}

生成給定表單設計和資料檔案的PCL、PostScript和ZPL輸出。 資料檔案與表單設計合併並格式化以打印。 輸出可直接發送到打印機或另存為檔案。 將generatePrintedOutput API用於應用程式中儲存的表單設計或資料。

**語法：** `Document generatePrintedOutput(Document inputdocument, Document data, PrintedOutputOptions);`

#### 輸入參數 {#input-parameters-3}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定輸入檔案的路徑和名稱。 如果僅指定檔案名，則讀取該檔案時將與選項中指定的contentRoot相關。 檔案可以是XDP類型。 </td>
  </tr>
  <tr>
   <td>資料</td>
   <td>包含與PDF文檔合併的資料的XML檔案。<br /> </td>
  </tr>
  <tr>
   <td>選項</td>
   <td>此對象用於設定contentRoot、locale、printConfig、copys和paginationOverride的值。 選項參數接受PrintedOutputOptions類型的對象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例從表單設計和資料生成PCL、PostScript和ZPL輸出。 輸出類型取決於傳遞給 `printConfig`的下界。

```java
@Reference private OutputService outputService;

private File generatePrintedOutput2(File  inputXML,File templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

       try {

            PrintedOutputOptions options = new PrintedOutputOptions();             if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {                                   options.setPrintConfig(PrintConfig.HP_PCL_5e);

            }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

                             }

            InputStream inputXMlStream = new FileInputStream(inputXML);

            InputStream templateStream = new FileInputStream(templateStr); doc =             outputService.generatePrintedOutput(new Document(templateStream),new             Document(inputXMlStream),options);

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return toSave;

            } catch (OutputServiceException e) {

                e.printStackTrace();

            }catch (FileNotFoundException e) {

                e.printStackTrace();

            } catch (IOException e) {

                e.printStackTrace();

            }finally{

                doc.dispose();

            }

            return null;

}
```

### generatePrintedOutputBatch {#generateprintedoutputbatch}

通過將表單設計與資料合併，生成PS、PCL和ZPL格式的文檔。 或者，為每個記錄生成元資料檔案或將輸出保存到PDF檔案。 將generatePrintedOutputBatch API用於儲存在網路位置、本地檔案系統或HTTP位置上的表單設計或資料作為文本值。

**語法`:`** `BatchResult generatePrintedOutputBatch(Map templates, Map data, PrintedOutputOptions options, BatchOptions batchOptions);`

#### 輸入參數 {#input-parameters-4}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>模板<br /> </td>
   <td>指定密鑰和模板檔案名的映射。<br /> </td>
  </tr>
  <tr>
   <td>資料</td>
   <td>指定鍵和資料文檔的映射。 如果鍵不為null，則使用模板映射中相應鍵的模板來呈現資料文檔。<br /> </td>
  </tr>
  <tr>
   <td>選項</td>
   <td>指定PrintedOutputOptions類型的對象。 此對象用於設定contentRoot、locale、printConfig、copys、pagenitationOverride的值。<br /> </td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>指定變數generateManyFiles的值。 設定generateManyFiles標誌以生成多個檔案。 選項參數接受BatchOptions類型的對象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例從多個表單設計模板和資料檔案中批量生成PCL、PostScript和ZPL輸出。 輸出類型取決於傳遞給 `printConfig`的下界。

```java
@Reference private OutputService outputService;

private ArrayList generatePrintedOutputBatch(String contentRoot,String multipleFiles,String printConfig) {

String outputFolder="C:/Output";

        try {

                PrintedOutputOptions option = new PrintedOutputOptions();                 option.setContentRoot(contentRoot);

                Map templates = new LinkedHashMap();

                Map data = new LinkedHashMap();

                String template1 = "PurchaseOrder.xdp";

                String template2 = "CardApp.xdp";

                templates.put(template1.substring(0,                 template1.indexOf(".xdp")),template1);                 templates.put(template1.substring(0,                 template2.indexOf(".xdp")),template2);

                File inputXML1 = new                                   File("c:/InputFolder/PurchaseOrder.xml");

                File inputXML2 = new File("c:/InputFolder/CardApp.xml");

                InputStream in1 = new FileInputStream(inputXML1);

                InputStream in2 = new FileInputStream(inputXML2);                  data.put(template1.substring(0,                     template1.indexOf(".xdp")),new Document((in1)));

                 data.put(template2.substring(0,                     template2.indexOf(".xdp")),new Document((in2)));

                 if(printConfig.equalsIgnoreCase("ps"))

                 {

                    option.setPrintConfig(PrintConfig.PS_PLAIN);

                 } else if(printConfig.equalsIgnoreCase("pcl"))

                 {

                    option.setPrintConfig(PrintConfig.HP_PCL_5e);

                 } else if(printConfig.equalsIgnoreCase("zpl")){

                                         option.setPrintConfig(PrintConfig.ZPL300);

                 }

                 option.setContentRoot(contentRoot);

                 BatchOptions bo = new BatchOptions();

                 BatchResult ret =                             outputService.generatePrintedOutputBatch(temp                                    lates, data, option, new                                                     BatchOptions());

                 ArrayList outputs = new ArrayList();

                 int counter=0;

                 if(ret.getMetaDataDoc() !=null ){

                 File toSave = new File(outputFolder,"Output"+".xml");                    ret.getMetaDataDoc().copyToFile(toSave);

                 outputs.add(toSave);

                 List<Document> list = ret.getGeneratedDocs();

                 for(Document doc:list){

                 File toSave = new                                                               File(outputFolder,"Output"+"_"+counter+".                                        "+printConfig);                                    doc.copyToFile(toSave);

                 outputs.add(toSave);

                 counter++;

                 doc.dispose();

                 }

                 return outputs;

          }

            catch (OutputServiceException e) {

                e.printStackTrace();

          }catch (FileNotFoundException e) {

                e.printStackTrace();

          } catch (IOException e) {

                e.printStackTrace();

          }

            return null;

  }
```

## Forms 服務 {#forms-service}

Forms服務提供API，以向互動式PDF表單導入和從互動式報表導出資料。 互動式PDF表單是PDF文檔，包含一個或多個用於顯示和收集用戶資訊的欄位。 該服務支援以下API:

* **[導出資料](/help/forms/using/aem-document-services-programmatically.md#p-exportdata-p):** 從PDF窗體導出資料。
* **[導入資料](/help/forms/using/aem-document-services-programmatically.md#p-importdata-p):** 將資料導入到互動式PDF窗體。

### 導出資料 {#exportdata}

以XML和XDP格式從互動式PDF表單中導出表單資料。

**語法：** `Document exportData(Document xdpOrPdf, DataFormat dataFormat)`

#### 輸入參數 {#input-parameters-5}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>xdpOrPdf<br /> </td>
   <td>指定包含XDP或PDF檔案的文檔對象。 </td>
  </tr>
  <tr>
   <td>資料格式<br /> </td>
   <td>指定導出資料的格式。 它接受類型enum(XDP、XmlData、Auto)的變數。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例以XML和XDP格式從互動式PDF表單中導出表單資料。

#### 範例 {#sample}

```java
@Reference private FormsService formsService;
private File exportData(String  dataFormat, File  inDoc) {

String outputFolder="C:/Output";

InputStream in; Document doc=null;

try {

        in = new FileInputStream(inDoc);

        if(dataFormat.equalsIgnoreCase("xml"))

        {

          doc=formsService.exportData(new Document(in),                                       DataFormat.XmlData);

        }

        else if(dataFormat.equalsIgnoreCase("xdp")) {

        doc =formsService.exportData(new Document(in),                       DataFormat.XDP);

        }

        File toSave = new File(outputFolder,"Output"+"."+dataFormat);

        doc.copyToFile(toSave);

        return toSave;

    } catch (FormsServiceException e) {

       e.printStackTrace();

    }catch (FileNotFoundException e) {

       e.printStackTrace();

    } catch (IOException e) {

       e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

 }
```

### 導入資料 {#importdata}

將表單資料導入到互動式PDF表單。

**語法：** `Document importData(Document PDF, Document data)`

#### 輸入參數 {#input-parameters-6}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>PDF<br /> </td>
   <td>指定包含PDF檔案的文檔對象。 </td>
  </tr>
  <tr>
   <td>資料<br /> </td>
   <td>包含XML格式的資料的XML檔案。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例將表單資料導入到互動式PDF表單中。

#### 範例 {#sample-1}

```java
@Reference private FormsService formsService

private File importData(File inDoc, File inXML)

{

 String outputFolder="C:/Output";

 Document doc=null;

 try {

        InputStream in = new FileInputStream(inDoc);

        InputStream in2 = new FileInputStream(inXML);

        doc=formsService.importData(new Document(in), new Document(in2));

        File toSave = new File(outputFolder,"Output.pdf");

        doc.copyToFile(toSave);

    } catch (FormsServiceException e) {

         e.printStackTrace();

    }catch (FileNotFoundException e) {

         e.printStackTrace();

    } catch (IOException e) {

         e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

}
```

## PDF生成器服務 {#pdfgeneratorservice}

PDF生成器服務提供API以將本機檔案格式轉換為PDF。 它還將PDF轉換為其他檔案格式，並優化PDF文檔的大小。

### 生成PDF服務 {#generatepdfservice}

GeneratePDFService提供API將各種檔案格式(如.doc、.docx、.ppt、.pptx、.xls、.xlsx、.odp、.odt、.ods、（棄用）。swf、.jpg、.bmp、.tif、.png、.html和許多其他檔案格式)轉換為PDF。 它還提供API將PDF導出為各種檔案格式並優化PDF。 該服務支援以下API:

* **建立PDF**:將支援的檔案類型轉換為PDF文檔。 它支援檔案格式，如MicrosoftWord、MicrosoftPowerPoint、MicrosoftExcel和Microsoft項目。 除了這些應用程式外，任何第三方通用PDF生成應用程式類型也可插入到API中。
* **導出PDF**:將PDF文檔轉換為支援的檔案類型。 該方法接受PDF作為輸入，並以指定檔案類型格式導出PDF的內容。 可以在Encapsulated PostScript(eps)、HTML3.2(htm,html)、HTML4.01(帶CSS 1.0(htm,html)、JPEG(jpg,jpeg,jpe)、JPEG2000(jpf,jpx,jp2,j2k,j2c,jpc)、MicrosoftWord文檔()中導出PDF文檔doc, docx)MicrosoftExcel工作簿(xlsx)、MicrosoftPowerPoint演示文稿(pptx)、PNG(png)、PostScript(ps)、RTF格式、Text(Accessible)(txt)、Text(Plain)(txt)TIFF(tif, tiff)、XML 1.0(xml)、PDF/A-1a(sRGB)、PDF/A-1b、PDF/A-2a(sRGB)、PDF/A-2b(sRGB)、PDF/A-3a(sRGB)、PDF/A-3b(sRGB)格式。 也可以指定 [自定義印前檢查配置檔案](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html) PDF輸出。

* **優化PDF**:優化PDF文檔，還將PDF文檔從一種類型轉換為另一種類型。 該方法接受PDF文檔作為輸入。
* **htmlToPdf2**:將HTML頁轉換為PDF文檔。 它接受HTML頁的URL作為輸入。

>[!NOTE]
>
>HTMLtoPDF API不建議用於在AIX作業系統上運行的AEM Forms伺服器。

#### PDF生成器API在MicrosoftWindows和Linux上提供 {#pdf-generator-api-available-on-microsoft-windows-and-linux}

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><p><strong>Microsoft窗 </strong></p> </td>
   <td><strong>Linux </strong></td>
  </tr>
  <tr>
   <td>建立PDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
  <tr>
   <td>htmlToPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
   <td>優化PDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>導出PDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>OCRPDF(可搜索PDF)</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
 </tbody>
</table>

#### 建立PDF {#createpdf}

createPDF API將支援的檔案類型轉換為PDF文檔。 它支援各種檔案格式，如MicrosoftWord、MicrosoftPowerPoint、MicrosoftExcel和Microsoft項目。 除了這些應用程式外，任何第三方通用PDF生成應用程式類型也可插入到API中。

對於轉換，只有幾個參數是必需的。 輸入文檔是必需參數。 您以後可以將安全權限、PDF輸出設定和元資料資訊應用到輸出PDF文檔。

createPDF服務返回帶結果的java.util.Map。 映射的鍵為：

* 轉換文檔：它包含新建立的PDF文檔。
* 日誌文檔：它包含日誌檔案。

createPDF服務引發以下異常：

* 轉換異常
* InvalidParameterException
* FileFormatNotSupportedException

**語法：** `Map createPDF(Document inputDoc, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws InvalidParameterException, ConversionException, FileFormatNotSupportedException;`

#### 輸入參數 {#input-parameters-7}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定文檔對象。 文檔對象包含輸入檔案。 在輸入文檔上建立com.adobe.aemfd.docmanager.Document對象。 它是強制參數。</td>
  </tr>
  <tr>
   <td>輸入檔案名<br /> </td>
   <td>輸入檔案的名稱以及副檔名。 它是強制參數。<br /> </td>
  </tr>
  <tr>
   <td>fileTypeSettings</td>
   <td>它是可選參數。</td>
  </tr>
  <tr>
   <td>pdf設定</td>
   <td><p>PDF轉換文檔的輸出。 您只能應用以下設定：</p>
    <ul>
     <li>高質量打印<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>按質量<br /> </li>
     <li>最小檔案大小</li>
    </ul> <p>它是可選參數。<br /> </p> </td>
  </tr>
  <tr>
   <td>安全設定</td>
   <td><p>已轉換文檔的安全設定。 可以應用以下設定：</p>
    <ul>
     <li>無安全性</li>
     <li>密碼安全<br /> </li>
     <li>證書安全<br /> </li>
     <li>Adobe策略伺服器</li>
    </ul> <p>它是可選參數。</p> </td>
  </tr>
  <tr>
   <td>設定文檔</td>
   <td>該檔案包含在生成PDF文檔時應用的設定(例如，為Web視圖優化PDF文檔)和在建立PDF文檔後應用的設定（例如，初始視圖和安全性）。 它是可選參數。<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>該檔案包含應用於生成的PDF文檔的元資料資訊。 此參數是可選的。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼將支援檔案類型的文檔轉換為PDF文檔。

```java
@Reference GeneratePDFService generatePdfService;
File createPDF(File inputFile, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = generatePdfService.createPDF(inDoc, inputFilename, fileTypeSettings, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

#### 導出PDF {#exportpdf}

將PDF文檔轉換為支援的檔案類型。 該方法接受PDF作為輸入，並以指定檔案類型格式導出PDF的內容。

createPDF服務返回帶結果的java.util.Map。 映射的鍵為：

* 轉換文檔：它包含輸出文檔。

createPDF服務引發以下異常：

* 轉換異常
* InvalidParameterException
* FileFormatNotSupportedException

**語法：**

```java
Map exportPDF(Document inputDoc, String inputFileName, String formatType, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 輸入參數 {#input-parameters-8}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定要轉換的文檔。 </td>
  </tr>
  <tr>
   <td>輸入檔案名<br /> </td>
   <td>檔案的名稱以及副檔名。<br /> </td>
  </tr>
  <tr>
   <td>格式類型</td>
   <td>導出PDF API的輸出檔案格式。<br /> </td>
  </tr>
  <tr>
   <td>設定文檔 </td>
   <td>該檔案包含在生成輸出文檔時要應用的配置。 通常是XML檔案。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例將PDF文檔轉換為指定的檔案類型。

```java
(tx == null)
OSGiUtils.getTransactionManager().begin();
String outputFolder="C:/Output"
Document convertedDoc = null;
Document inDoc = null;
Document settingsDoc = null;
try
{
 inDoc = new Document(inputFile);
 if(inputFileName == null || inputFileName.trim().equals("")) {
  throw new Exception("Input file name cannot be null");
 }
 if(inputFileExtension.lastIndexOf('.') == -1) {
  throw new Exception("Input file should have an extension");
 }
 if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
 settingsDoc = new Document(settingsFile);
 Map result = generatePdfService.exportPDF(inDoc, inputFileName, formatType, settingsDoc);
 convertedDoc = (Document)result.get("ConvertedDoc");
 OSGiUtils.getTransactionManager().commit();
 File outputFile = new File(outputFolder,"OutputFile");
 doc.copyToFile(outputFile);
 return outputFile;
}
catch (Exception e)
{
 if (OSGiUtils.getTransactionManager().getTransaction() != null)
 OSGiUtils.getTransactionManager().rollback();
 throw e;
}
finally {
 if (convertedDoc != null) {
  convertedDoc.dispose();
  convertedDoc = null;
 }
 if (inDoc != null) {
  inDoc.dispose();
  inDoc = null;
 }
 if (settingsDoc != null) {
  settingsDoc.dispose();
  settingsDoc = null;
 }
}
}
```

#### 優化PDF {#optimizepdf}

OptimizePDF API通過減小PDF檔案的大小來優化壓縮檔案。 此轉換的結果是PDF檔案可能小於其原始版本。 此操作還將PDF文檔轉換為優化參數中指定的PDF版本。 它返回包含優化PDF的OptimizePDFResult對象。

createPDF服務引發以下異常：

* 轉換異常
* InvalidParameterException
* FileFormatNotSupportedException

**語法：**

```java
OptimizePDFResult optimizePDF(Document inputDoc, String fileTypeSettings, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 輸入參數 {#input-parameters-9}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定輸入文檔。 它是強制參數。</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>它是可選參數。<br /> </td>
  </tr>
  <tr>
   <td>設定文檔 </td>
   <td>該檔案包含在生成PDF文檔時應用的設定(例如，為Web視圖優化PDF文檔)和在建立PDF文檔後應用的設定（例如，初始視圖和安全性）。 它是可選參數。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例通過減小輸入PDF檔案的大小來優化其大小。

```java
@Reference GeneratePDFService generatePdfService;
File optimizePDF(File inputFile, String fileTypeSettings, File settingsFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  OptimizePDFResult result = generatePdfService.optimizePDF(inDoc, fileTypeSettings, settingsDoc);
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

#### htmlToPdf2 {#htmltopdf}

將HTML頁轉換為PDF文檔。 它接受HTML頁的URL作為輸入。

htmlToPdf2服務返回HtmlToPdfResult對象。 可以通過result.getConvertedDocument()獲取轉換的PDF。

htmlToPdf2服務引發以下異常：

* 轉換異常
* InvalidParameterException
* FileFormatNotSupportedException

**語法：**

```java
HtmlToPdfResult htmlToPdf2(String inputUrl, String fileTypeSettingsName, String securitySettingsName, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 輸入參數 {#input-parameters-10}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定輸入文檔。 它是強制參數。</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>它是可選參數。<br /> </td>
  </tr>
  <tr>
   <td>設定文檔 </td>
   <td>該檔案包含在生成PDF文檔時應用的設定(例如，為Web視圖優化PDF文檔)和在建立PDF文檔後應用的設定（例如，初始視圖和安全性）。 它是可選參數。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代碼示例將HTML頁轉換為PDF文檔。

```java
Reference GeneratePDFService generatePdfService;
File htmlToPdf(String inputUrl, String fileTypeSettingsName, String securitySettingsName, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  HtmlToPdfResult result = generatePdfService.htmlToPdf2(inputURL, fileTypeSettingsName, securitySettingsName, settingsDoc, xmpDoc);;
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

### Distiller服務 {#distillerservice}

Distiller服務將PostScript、封裝的PostScript(EPS)和打印機文本檔案(PRN)轉換為PDF檔案。 Distiller服務經常用於將大量打印檔案轉換成電子檔案，如發票和報表。 將文檔轉換為PDF還允許企業向其客戶發送文檔的紙面版本和電子版本。 支援的檔案格式為.ps 、 .eps和.prn。 該服務支援以下API:

createPDF服務返回帶結果的java.util.Map。 映射的鍵為：

* ConvertedDoc :它包含新建立的PDF文檔。
* 日誌文檔：它包含日誌檔案。

createPDF服務引發以下異常：

* 轉換異常
* InvalidParameterException
* FileFormatNotSupportedException

#### 建立PDF {#createpdf-1}

將支援的格式轉換為PDF文檔。 該方法將檔案格式.ps、.eps和.prn作為輸入。 您可以將特定的安全權限、輸出設定和元資料資訊應用到輸出PDF文檔。

**語法：**

```java
Map createPDF(Document inputDoc, String inputFileName, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 輸入參數 {#input-parameters-11}

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>輸入文檔<br /> </td>
   <td>指定輸入文檔。 它是強制參數。</td>
  </tr>
  <tr>
   <td>輸入檔案名</td>
   <td>指定輸入檔案的完整名稱以及檔案的副檔名。 它是強制參數。</td>
  </tr>
  <tr>
   <td>pdf設定</td>
   <td><p>PDF轉換文檔的輸出設定。 您只能應用以下設定：</p>
    <ul>
     <li>高質量打印<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>按質量<br /> </li>
     <li>最小檔案大小</li>
    </ul> <p>它是可選參數。</p> </td>
  </tr>
  <tr>
   <td>安全設定</td>
   <td><p>已轉換文檔的安全設定。 可以應用以下設定：</p>
    <ul>
     <li>無安全性</li>
     <li>密碼安全<br /> </li>
     <li>證書安全<br /> </li>
     <li>Adobe策略伺服器</li>
    </ul> <p>它是可選參數。</p> </td>
  </tr>
  <tr>
   <td>設定文檔 </td>
   <td>該檔案包含在生成PDF文檔時應用的設定(例如，為Web視圖優化PDF文檔)和在建立PDF文檔後應用的設定（例如，初始視圖和安全性）。 它是可選參數。<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>該檔案包含生成的PDF文檔的元資料資訊。 它是可選參數。</td>
  </tr>
 </tbody>
</table>

以下Java代碼示例將PostScript(PS)、Encapsulated PostScript(EPS)和打印機文本檔案(PRN)類型的輸入檔案轉換為PDF檔案。

```java
@Reference DistillerService distillerService;
File createPDF(File inputFile, String inputFilename, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = distillerService.createPDF(inDoc, inputFilename, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```
