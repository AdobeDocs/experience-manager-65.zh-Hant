---
title: 使用HSM對文檔進行數字簽名或認證
seo-title: Use HSM to certify eSigned documents
description: 使用HSM或etoken設備驗證電子簽名文檔
seo-description: Use HSM or etoken devices to certify eSigned documents
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
exl-id: 4d423881-18e0-430a-849d-e1762366a849
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 使用HSM對文檔進行數字簽名或認證 {#use-hsm-to-digitally-sign-or-certify-documents}

硬體安全模組(HSM)和令牌是專用的、加固的和抗篡改的計算設備，旨在安全地管理、處理和儲存數字密鑰。 這些設備直接連接到電腦或網路伺服器。

Adobe Experience Manager Forms可以使用HSM或etoken上儲存的憑據對文檔進行eSign或應用伺服器側數字簽名。 要將HSM或令牌設備與AEM Forms一起使用：

1. 啟用DocAssurance服務。
1. 設定Reader擴展的證書。
1. 在Web控制台中為HSM或令牌設備創AEM建別名。
1. 使用DocAssurance Service API使用儲存在設備上的數字密鑰對文檔進行簽名或認證。

## 在配置HSM或令牌設備之前，請使用AEM Forms {#configurehsmetoken}

* 安裝 [AEM Forms附加](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 檔案。
* 在與伺服器相同的電腦上安裝和配置HSM或etoken客AEM戶端軟體。 客戶端軟體需要與HSM和令牌設備通信。
* (僅限MicrosoftWindows)將JAVA_HOME_32環境變數設定為指向安裝32位版本的Java 8開發工具包(JDK 8)的目錄。 目錄的預設路徑是C:\Program Files(x86)\Java\jdk&lt;version>
* (僅AEM Forms在OSGi上)在信任儲存中安裝根證書。 需要驗證已簽名的PDF

>[!NOTE]
>
>在MicrosoftWindows上，僅支援32位LunaSA或EToken客戶端。

## 啟用DocAssurance服務 {#configuredocassurance}

預設情況下，未啟用DocAssurance服務。 執行以下步驟以啟用服務：

1. 停止您的AEM Forms環境的作者實例。

1. 開啟 [AEM根]\crx-quickstart\conf\sling.properties檔案進行編輯。

   >[!NOTE]
   >
   >如果你用過 [AEM根]\crx-quickstart\bin\start.bat檔案以啟AEM動實例，然後開啟 [AEM根]\crx-quickstart\sling.properties檔案，用於編輯。

1. 將以下屬性添加或替換到sling.properties檔案：

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 保存並關閉sling.properties檔案。
1. 重新啟動AEM實例。

## 設定Reader擴展的證書 {#set-up-certificates-for-reader-extensions}

執行以下步驟以設定證書：

1. 以管理員身份登錄到AEM Author實例。

1. 按一下&#x200B;**Adobe Experience Manager** 的子菜單。 轉到 **工具** >  **安全** >  **用戶**。
1. 按一下 **名稱** 的子菜單。 的 **編輯用戶設定** 的上界。
1. 在AEM Author實例上，證書駐留在KeyStore中。 如果您之前未建立KeyStore，請按一下 **建立密鑰儲存** 並為KeyStore設定新密碼。 如果伺服器已包含KeyStore，請跳過此步驟。

1. 在 **編輯用戶設定** 的 **管理密鑰儲存**。

1. 在KeyStore管理對話框上，展開 **從密鑰儲存檔案添加私鑰** 選項並提供別名。 別名用於執行Reader擴展操作。
1. 要上載證書檔案，請按一下 **選擇密鑰儲存檔案** 上傳 `.pfx` 的子菜單。
1. 添加 **密鑰儲存密碼**。**私鑰密碼**, **私鑰別名** 與證書關聯到相應欄位的。 按一下 **提交**。

   >[!NOTE]
   >
   >確定P **私鑰別名** 在證書中，可以使用Java keytool命令： `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >在 **密鑰儲存密碼** 和 **私鑰密碼** 欄位中，指定證書檔案提供的密碼。

>[!NOTE]
>
>對於OSGi上的AEM Forms，要驗證已簽名的PDF，信任儲存中安裝的根證書。

>[!NOTE]
>
>轉到生產環境時，請用生產憑據替換您的評估憑據。 在更新過期或評估憑據之前，請確保刪除舊Reader擴展憑據。

## 為設備建立別名 {#configuredeviceinaemconsole}

別名包含HSM或etoken需要的所有參數。 執行下面列出的說明，為eSign或數字簽名使用的每個HSM或etoken憑據建立別名：

1. 開啟控AEM制台。 控制台的默AEM認URL為https://&lt;host>:&lt;port>/system/console/configMgr
1. 開啟 **HSM憑據配置服務** 並指定以下欄位的值：

   * **憑據別名**:指定用於標識別名的字串。 此值用作某些數字簽名操作的屬性，如簽名欄位操作。
   * **DLL路徑**:指定伺服器上HSM或etoken客戶端庫的完全限定路徑。 例如，C:\Program Files\LunaSA\cryptoki.dll。 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
   * **HSM針腳**:指定訪問設備密鑰所需的密碼。
   * **HSM插槽ID**:指定整數類型的插槽標識符。 插槽ID是按客戶端逐個設定的。 如果將第二台電腦註冊到不同的分區（例如，在同一HSM設備上的HSMPART2），則插槽1與客戶端的HSMPART2分區相關聯。

   >[!NOTE]
   >
   >配置Etoken時，為HSM插槽ID欄位指定一個數值。 要使「簽名」操作正常工作，需要一個數值。

   * **證書SHA1**:為您使用的憑據指定公鑰(.cer)檔案的SHA1值（指紋）。 確保SHA1值中沒有使用空格。 如果您使用的是物理證書，則不需要該證書。
   * **HSM設備類型**:選擇HSM（Luna或其他）或eToken設備的製造商。

   按一下「**儲存**」。硬體安全模組已配置為AEM Forms。 現在，您可以使用硬體安全模組與AEM Forms一起對文檔進行簽名或認證。

## 使用DocAssurance Service API使用儲存在設備上的數字密鑰對文檔進行簽名或認證  {#programatically}

以下示例代碼使用HSM或etoken對文檔進行簽名或認證。

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

如果您已從AEM6.0表單或AEM6.1Forms升級，並且您正在舊版本中使用DocAssurance服務，則：

* 若要在沒有HSM或令牌設備的情況下使用DocAssurance服務，請繼續使用現有代碼。
* 要將DocAssurance服務與HSM或etoken設備一起使用，請用下面列出的API替換現有的CredentialContext對象代碼。

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

有關DocAssurance服務的API和示例代碼的詳細資訊，請參見 [以寫程式AEM方式使用Document Services](/help/forms/using/aem-document-services-programmatically.md)。
