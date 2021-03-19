---
title: 加密服務Java API QuickStart(SOAP)
seo-title: 加密服務Java API QuickStart(SOAP)
description: 加密服務Java API QuickStart(SOAP)
uuid: 3e29b3e9-340b-4b35-80cc-f0aff4180892
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f12c10c3-1ce6-4415-ba9d-5349d1888237
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# 加密服務Java API快速入門(SOAP){#encryption-service-java-api-quickstart-soap}

[快速入門（SOAP模式）:使用Java API加密PDF檔案](encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API移除密碼加密](encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

[快速入門（SOAP模式）:使用Java API使用憑證加密PDF檔案](encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[快速入門（SOAP模式）:使用Java API移除憑證式加密](encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[快速入門（SOAP模式）:使用Java API解除加密的PDF檔案鎖定](encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API確定加密類型](encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

AEM Forms操作可以使用AEM Forms強類型API執行，連接模式應設定為SOAP。

>[!NOTE]
>
>使用表單進行寫程式的「快速AEM入門」基於部署在JBoss Application Server和Microsoft Windows作業系統上的Forms伺服器。 但是，如果您使用其他作業系統（例如UNIX），請以適用作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請確定您指定有效的連線屬性。 請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

## 快速入門（SOAP模式）:使用Java API {#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api}加密PDF檔案

以下Java代碼示例使用密碼值`OpenPassword`加密名為&#x200B;*Loan.pdf*&#x200B;的PDF文檔。 主密碼為`PermissionPassword`。 安全的PDF檔案會儲存為名為&#x200B;*EncryptLoan.pdf*&#x200B;的PDF檔案。 （請參閱[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.util.ArrayList;
 import java.util.List;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class PasswordEncryptPDFSoap{
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an EncryptionServiceClient object
         EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
         //Specify the PDF document to encrypt with a password
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inDoc = new Document (fileInputStream);
 
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
 
         //Encrypt the PDF document
         Document encryptDoc = encryptClient.encryptPDFUsingPassword(inDoc,passSpec);
 
         //Save the password-encrypted PDF document
         File outFile = new File("C:\\Adobe\EncryptLoan.pdf");
         encryptDoc.copyToFile (outFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）:使用Java API {#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api}刪除基於密碼的加密

以下Java代碼示例從名為&#x200B;*EncryptLoan.pdf*&#x200B;的PDF文檔中刪除基於密碼的加密。 用於刪除基於密碼的加密的主密碼值為&#x200B;*PermissionPassword*。 無擔保的PDF檔案會儲存為名為&#x200B;*noEncryptionLoan.pdf*&#x200B;的PDF檔案。 （請參閱[刪除密碼加密](/help/forms/developing/encrypting-decrypting-pdf-documents.md#removing-password-encryption)。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import com.adobe.livecycle.encryption.client.*;
 
 public class RemovePasswordFromPDFSOAP {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the encrypted PDF from which to remove password-based encryption
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Remove password-based encryption from the PDF document
             Document encryptDoc = encryptClient.removePDFPasswordSecurity(inDoc,"PermissionPassword");
 
             //Save the unsecured PDF document
             File outFile = new File("C:\\Adobe\noEncryptionLoan.pdf");
             encryptDoc.copyToFile (outFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## 快速入門（SOAP模式）:使用Java API {#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api}使用憑證加密PDF檔案

以下Java代碼示例使用名為&#x200B;*Encryption.cer*&#x200B;的證書加密名為&#x200B;*Loan.pdf*&#x200B;的PDF文檔。 加密的PDF檔案會儲存為名為&#x200B;*EncryptLoanCert.pdf*&#x200B;的PDF檔案。 （請參閱[使用憑證加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.util.ArrayList;
 import java.util.List;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class PKIEncryptPDFSoap {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Specify the PDF document to encrypt with a certificate
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Set the List that stores PKI information
             List pkiIdentities = new ArrayList();
 
             //Set the Permission List
             List permList = new ArrayList();
             permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;
 
             //Create a Recipient object to store certificate information
             Recipient recipient = new Recipient();
 
             //Specify the private key that is used to encrypt the document
             FileInputStream fileInputStreamCert = new FileInputStream("C:\\Adobe\Encryption.cer");
             Document privateKey = new Document (fileInputStreamCert);
             recipient.setX509Cert(privateKey);
 
             //Create an EncryptionIdentity object
             CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
             encryptionId.setPerms(permList);
             encryptionId.setRecipient(recipient);
 
             //Add the EncryptionIdentity to the list
             pkiIdentities.add(encryptionId);
 
             //Set encryption run-time options
             CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
             certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
             certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_7);
 
             //Encrypt the PDF document with a certificate
             Document encryptDoc = encryptClient.encryptPDFUsingCertificates(inDoc,pkiIdentities, certOptionsSpec);
 
             //Save the encrypted PDF document
             File outFile = new File("C:\\Adobe\EncryptLoanCert.pdf");
             encryptDoc.copyToFile (outFile);
 
             }catch (Exception e) {
                 e.printStackTrace();
             }
     }
 }
 
```

## 快速入門（SOAP模式）:使用Java API {#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api}移除憑證式加密

以下Java代碼示例從名為&#x200B;*EncryptLoanCert.pdf*&#x200B;的PDF文檔中刪除基於證書的加密。 用於刪除加密的公鑰的別名為`Encryption`。 無擔保的PDF檔案會儲存為名為&#x200B;*noEncryptionLoan.pdf*&#x200B;的PDF檔案。 （請參閱[刪除基於證書的加密](/help/forms/developing/encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
     * <install directory>/jboss/bin/client/jboss/bin/client
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
 import com.adobe.livecycle.encryption.client.*;
 
 public class RemovePKIFromPDFSOAP {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the encrypted PDF document
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoanCert.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Remove certificate-based encryption from the PDF document
             Document encryptDoc = encryptClient.removePDFCertificateSecurity(inDoc, "Encryption");
 
             //Save the unsecured PDF document
             File outFile = new File("C:\\Adobe\noEncryptionLoan.pdf");
             encryptDoc.copyToFile (outFile);
 
         }catch (Exception e) {
                 e.printStackTrace();
             }
     }
 }
```

## 快速入門（SOAP模式）:使用Java API {#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api}解除加密的PDF檔案鎖定

下列Java程式碼範例解除鎖定名為&#x200B;*EncryptLoan.pdf*&#x200B;的密碼加密PDF檔案。 （請參閱[解除加密的PDF檔案鎖定](/help/forms/developing/encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if forms server is not deployed
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class UnlockPDFSOAP {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the password-encrypted PDF document to unlock
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Specify the password to open the password-encrypted PDF document
             String openPassword = "OpenPassword" ;
 
             //Unlock the password-encrypted PDF document
             Document unlockedDoc = encryptClient.unlockPDFUsingPassword(inDoc,openPassword);
 
         }catch (Exception e) {
                 System.out.println("The following error occurred during this operation " +e.getMessage());
         }
     }
 }
 
```

## 快速入門（SOAP模式）:使用Java API {#quick-start-soap-mode-determining-encryption-type-using-the-java-api}確定加密類型

以下Java代碼示例確定保護名為&#x200B;*EncryptLoan.pdf*&#x200B;的PDF文檔的加密類型。 （請參閱[確定加密類型](/help/forms/developing/encrypting-decrypting-pdf-documents.md#determining-encryption-type)。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class GetEncryptionTypeSOAP {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the PDF document
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Determine the type of encryption of the PDF document
             EncryptionTypeResult encryptTypeResult = encryptClient.getPDFEncryption(inDoc);
 
             if (encryptTypeResult.getEncryptionType() == EncryptionType.PASSWORD)
                 System.out.println("The PDF document is protected with password-based encryption");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.POLICY_SERVER)
                 System.out.println("The PDF document is protected with policy");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.CERTIFICATE)
                 System.out.println("The PDF document is protected with certificate-based encryption");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.OTHER)
                 System.out.println("The PDF document is protected with another type of encryption");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.NONE)
                 System.out.println("The PDF document is not protected.");
         }catch (Exception e) {
                 e.printStackTrace();
         }
     }
 }
 
 
 
```

