---
title: Reader擴展證書的過期及其影響
description: Reader擴展證書的過期及其影響
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 6e9a7f3307ed05f887d60c7c7310100cd4596b23
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 2%

---


# Reader擴展證書的過期及其影響 {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Experience Manager Forms(AEM Forms)擁有Adobe托管服務或內部部署企業基礎許可證的客戶有權使用Acrobat Reader DC擴展服務。 該服務通過擴展Acrobat Reader的功能和附加的使用權限，使組織能夠方便地共用互動式PDF文檔。 該服務將使用權限添加到PDF文檔，並激活在使用Adobe Acrobat Reader開啟PDF文檔時不可用的功能，例如向文檔添加註釋、填寫表單和保存文檔。 第三方用戶不需要使用其他軟體或插件來處理啟用權限的文檔。 PDF文檔添加了使用權限，稱為啟用權限的文檔。 在Acrobat Reader開啟啟用了權限的PDF文檔的用戶可以執行為該文檔啟用的操作。

Adobe利用公鑰基礎結構(PKI)頒發數字證書，用於許可和功能啟用。 Adobe一直根據證書頒發機構頒發證書 **Adobe根CA**，將於2023年1月7日到期。 證書的過期不會影響使用從以下站點頒發的生產證書擴展的PDF文檔 **Adobe根CA** 基於證書（舊證書）。 所有PDF文檔、在2023年1月7日之前使用舊證書擴展的Reader，包括您的客戶下載的證書，都將繼續使用應用到它們的所有使用權限，並且不需要任何更新。

新的證書頒發機構， **Adobe根CA G2**，並且基於新證書頒發機構的證書現在可用。 2023年1月7日或之前，開始使用新證書 — 這些證書基於 **Adobe根CA G2**  — 以Reader擴展新的PDF文檔。  你可以 [從Adobe許可網站獲取新證書](https://licensing.adobe.com/) 或Adobe支援。

## 常見問答

**問：Adobe根證書和Acrobat Reader擴展證書之間有何區別？ Adobe根證書是否依賴於Acrobat Reader擴展證書？ 這兩份證書是否將於2023年1月到期？**

答：Adobe根CA是頒發Acrobat Reader擴展證書的證書頒發機構。 2023年1月7日，「Adobe根CA」及其頒發的所有證書將到期。

**問：以前曾有Adobe就證書過期和對使用/開啟PDF檔案的影響發來過信。 這種溝通應該被忽視嗎？**

答：根據對情況的重新評估，2023年1月7日以前使用舊的&quot;PDF根證書&quot;簽發的生產證書延期的所有Adobe檔案在2023年1月7日以後繼續工作，沒有任何變化。 如果已更新PDF文檔，則體驗沒有更改。

**問：如果我有其他問題，應聯繫誰？**

答：您可以聯繫 [Adobe支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 或者提出支援票。

**問：如果我在2023年1月7日之前不更新我的證書，會發生什麼情況？**

答：在2023年1月7日之前，使用舊的「PDF根CA」頒發的生產證書擴展的所有Adobe檔案在2023年1月7日之後繼續工作，沒有任何更改。 使用評估證書擴展的PDF在到期日期後不工作。

**問：新證書的說明是否與舊證書有任何不同？**

答：新Acrobat Reader分機證書的說明 **G3-P24** 作為程式名。 在舊證書(基於「Adobe根CA」的證書)的說明中， **P24** 作為程式名稱。

**問：如何獲取最新的證書？**

答：所有有權獲得Forms客戶（具有活動許可證）都可以從以下站點下載新證書(基於「Adobe根CA G2」的證書): [Adobe許可網站](https://licensing.adobe.com/)。 如果在Adobe授權網站上找不到證書，請聯繫 [Adobe支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) 或者提出支援票。

**問：使用「Adobe根CA」（舊證書頒發機構）頒發的證書擴展的PDF文檔是否在2023年1月7日之後繼續工作？**

答：是的，在2023年1月7日之前，所有使用「Adobe根CA」（舊證書頒發機構）頒發的生產證書擴展的PDF文檔，在2023年1月7日之後繼續工作，但不作任何更改。 使用評估證書擴展的PDF文檔在過期日期後停止工作。

**問：繼續使用由「Adobe Acrobat Reader根CA」（舊證書頒發機構）頒發的證書擴展的PDF文檔，需要哪個版本的Adobe?**

答：Adobe Acrobat Reader2020或更高版本需要使用擴展為「Adobe根CA」（舊證書頒發機構）的PDF文檔。 它是發佈本文檔時支援的Acrobat Reader版本。 如果使用 [不支援的Adobe Acrobat版本](https://helpx.adobe.com//tw/support/programs/eol-matrix.html),Adobe建議您 [下載並安裝最新版本的Adobe Acrobat Reader](https://get.adobe.com/reader/)。

**問：需要哪個版本的Adobe Acrobat Reader才能繼續使用擴展了「Adobe根CA 2」（新證書頒發機構）頒發的證書的PDF文檔？**

答：Adobe Acrobat Reader2020或更高版本需要使用擴展為「Adobe根CA 2」（新證書頒發機構）的PDF文檔。 如果使用 [不支援的Adobe Acrobat Reader版本](https://helpx.adobe.com//tw/support/programs/eol-matrix.html),Adobe建議您 [下載並安裝最新版本的Adobe Acrobat Reader](https://get.adobe.com/reader/)。

**問：是否可以刪除舊的Acrobat Reader擴展證書，並在繼續使用現有別名時在Adobe Experience Manager Forms伺服器上添加新證書？**

答：是，您可以刪除舊的Acrobat Reader擴展證書，並將具有現有別名的新證書添加到Adobe Experience Manager Forms伺服器。

**問：我能否將新的和舊的Acrobat Reader擴展證書都保留在Adobe Experience Manager Forms伺服器上？**

答：是的，您可以在Adobe Experience Manager Forms伺服器上同時保留兩個證書，但別名不同。 自2023年1月7日起，您只能使用新證書來Reader擴展PDF文檔。

**問：是否可以將相同的Acrobat Reader擴展證書導入所有Adobe Experience Manager Forms環境？**

答：是的，同一個Acrobat Reader擴展證書可以跨多個環境使用。

**問：如何檢查應用於PDF文檔的使用權限？**

答：您可以使用 [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API，用於檢索有關應用於PDF文檔的使用權限的資訊。

**問：如何更改Acrobat Reader擴展證書檔案的密碼？**

答：在MicrosoftWindows上，要更改證書密碼，請使用Microsoft管理控制台(MMC)安裝證書並選擇 **將密鑰標籤為可導出**。 安裝後，使用私鑰導出證書，並為PFX檔案使用其他密碼。


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
