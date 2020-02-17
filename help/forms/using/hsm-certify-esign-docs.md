---
title: 使用HSM數位簽署或認證檔案
seo-title: 使用HSM來認證電子簽名檔案
description: 使用HSM或etoken裝置來認證電子簽署檔案
seo-description: 使用HSM或etoken裝置來認證電子簽署檔案
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# 使用HSM數位簽署或認證檔案 {#use-hsm-to-digitally-sign-or-certify-documents}

硬體安全性模組(HSM)和Token是專用、強化和防竄改的運算裝置，旨在安全地管理、處理和儲存數位金鑰。 這些設備直接連接到電腦或網路伺服器。

Adobe Experience Manager Forms可以使用儲存在HSM或etoken上的認證來電子簽名，或將伺服器端數位簽名套用至檔案。 若要搭配AEM Forms使用HSM或etoken裝置：

1. 啟用DocAssurance服務。
1. 設定Reader擴充功能的憑證。
1. 在AEM Web Console中建立HSM或etoken裝置的別名。
1. 使用DocAssurance Service API，使用儲存在裝置上的數位金鑰來簽署或認證檔案。

## 在您使用AEM Forms設定HSM或etoken裝置之前 {#configurehsmetoken}

* 安 [裝AEM Forms附加套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。
* 在與AEM伺服器相同的電腦上安裝及設定HSM或etoken用戶端軟體。 用戶端軟體必須與HSM和etoken裝置通訊。
* （僅限Microsoft Windows）將JAVA_HOME_32環境變數設定為指向安裝32位版本Java 8開發工具包(JDK 8)的目錄。 目錄的預設路徑是C:\Program Files(x86)\Java\jdk&lt;version>
* （僅限OSGi上的AEM Forms）在信任存放區中安裝根憑證。 需要驗證已簽署的PDF

>[!NOTE]
>
>在Microsoft windows上，僅支援32位LunaSA或EToken客戶端。

## 啟用DocAssurance服務 {#configuredocassurance}

預設情況下，DocAssurance服務未啟用。 執行以下步驟以啟用服務：

1. 停止AEM Forms環境的「作者」例項。

1. 開啟 [AEM_root]\crx-quickstart\conf\sling.properties檔案以進行編輯。

   >[!NOTE]
   >
   >如果您已使用 [AEM_root]\crx-quickstart\bin\start.bat檔案來啟動AEM例項，請開啟 [AEM_root]\crx-quickstart\sling.properties檔案以進行編輯。

1. 將下列屬性新增或取代至sling.properties檔案：

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 儲存並關閉sling.properties檔案。
1. 重新啟動AEM例項。

## 為Reader擴充功能設定憑證 {#set-up-certificates-for-reader-extensions}

執行以下步驟來設定證書：

1. 以管理員身分登入AEM Author例項。

1. 按一&#x200B;**下全域導覽列上的** 「Adobe Experience Manager」。 前往「工 **具** >安 **全性** >使 **用者**」。
1. 按一 **下使用** 者帳戶的名稱欄位。 「編 **輯使用者設定** 」頁面隨即開啟。
1. 在AEM Author例項中，憑證位於KeyStore中。 如果您尚未先前建立KeyStore，請按一 **下「建立KeyStore** 」，並為KeyStore設定新密碼。 如果伺服器已包含KeyStore，請略過此步驟。

1. 在「編輯使 **用者設定」頁面** ，按一下「 **管理金鑰商店」**。

1. 在「KeyStore管理」對話方塊中，展開「從 **Key Store檔案新增私密金鑰** 」選項並提供別名。 別名用於執行Reader Extensions操作。
1. 若要上傳憑證檔案，請按一 **下「選取金鑰存放區檔案** 」並上傳 `.pfx` 檔案。
1. 將與憑 **證關聯的金鑰存放****區密碼、私密金鑰密碼**、 **** 私密金鑰別名新增至各欄位。 按一 **下提交**。

   >[!NOTE]
   >
   >要確定證&#x200B;**書的私鑰別名** ，可以使用Java keytool命令： `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >在「金 **鑰存放區密碼** 」和「 **** 私密金鑰密碼」欄位中，指定憑證檔案所提供的密碼。

>[!NOTE]
>
>對於OSGi上的AEM Forms，若要驗證已簽署的PDF（信任商店中安裝的根憑證）。

>[!NOTE]
>
>移至生產環境時，請以生產認證取代您的評估認證。 在更新過期或評估憑證之前，請確定您已刪除舊的Reader Extensions憑證。

## 為設備建立別名 {#configuredeviceinaemconsole}

別名包含HSM或etoken所需的所有參數。 請執行下列指示，為電子簽名或數位簽章使用的每個HSM或etoken憑證建立別名：

1. 開啟AEM主控台。 AEM主控台的預設URL為https://&lt;host>:&lt;port>/system/console/configMgr
1. 開啟 **HSM憑據配置服務** ，並指定以下欄位的值：

   * **憑據別名**:指定用於標識別名的字串。 此值用作某些數位簽章作業的屬性，例如「簽章欄位」作業。
   * **DLL路徑**:指定伺服器上HSM或etoken用戶端程式庫的完全限定路徑。 例如，C:\Program Files\LunaSA\cryptoki.dll。 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
   * **HSM針腳**:指定存取裝置金鑰所需的密碼。
   * **HSM插槽Id**:指定整數類型的插槽標識符。 插槽ID是逐個客戶機設定的。 如果將第二台電腦註冊到不同的分區（例如，在同一HSMPART設備上的HSMPART2），則插槽1與客戶機的HSMPART2分區相關聯。
   **** 注意：設 *定Etoken時，請為HSM槽ID欄位指定數值。 要使「簽名」操作正常運作，需要數值。*

   * **證書SHA1**:為您使用的憑證指定公開金鑰(.cer)檔案的SHA1值（指紋）。 請確定SHA1值中沒有使用空格。 如果您使用實體憑證，則不需要。
   * **HSM設備類型**:選擇HSM（Luna或其他）或eToken裝置的製造商。
   按一下&#x200B;**「儲存」**。硬體安全性模組已針對AEM Forms設定。 現在，您可以搭配AEM Forms使用硬體安全性模組來簽署或認證檔案。

## 使用DocAssurance Service API，使用儲存在裝置上的數位金鑰簽署或認證檔案 {#programatically}

下列范常式式碼使用HSM或etoken來簽署或認證檔案。

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
import java.io.IOException;
import java.io.InputStream;

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
import com.adobe.fd.docassurance.client.api.SignatureOptions;
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
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
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
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
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
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
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

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

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
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
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
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

如果您已從AEM 6.0 Form或AEM 6.1 Forms升級，而且您在舊版中使用DocAssurance服務，則：

* 若要在沒有HSM或etoken裝置的情況下使用DocAssurance服務，請繼續使用現有的程式碼。
* 若要將DocAssurance服務與HSM或etoken裝置搭配使用，請以下列的API取代您現有的CredentialContext物件程式碼。

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

如需有關API和DocAssurance服務范常式式碼的詳細資訊，請參 [閱以程式設計方式使用AEM Document Services](/help/forms/using/aem-document-services-programmatically.md)。
