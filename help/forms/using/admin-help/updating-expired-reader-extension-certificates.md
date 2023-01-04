---
title: Reader擴充功能憑證的到期日及其影響
description: Reader擴充功能憑證的到期日及其影響
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 6e9a7f3307ed05f887d60c7c7310100cd4596b23
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 2%

---


# Reader擴充功能憑證的到期日及其影響 {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Experience Manager Forms(AEM Forms)擁有Adobe Managed Services或內部部署企業基礎授權的客戶，有權使用Acrobat Reader DC擴充功能服務。 此服務可讓組織透過擴充Acrobat Reader的功能與其他使用權限，輕鬆共用互動式PDF檔案。 該服務向PDF文檔添加使用權限，並激活在使用Adobe Acrobat Reader開啟PDF文檔時不可用的功能，如向文檔添加註釋、填寫表單和保存文檔。 協力廠商使用者不需要其他軟體或外掛程式，即可使用啟用權限的檔案。 添加了使用權限的PDF文檔稱為啟用權限的文檔。 在Acrobat Reader中開啟啟用權限的PDF文檔的用戶可以執行為該文檔啟用的操作。

Adobe利用公鑰基礎設施(PKI)發放用於許可和功能啟用的數字證書。 Adobe一直在憑證機構簽發證書 **Adobe根CA**，該服務將於2023年1月7日到期。 憑證的過期不會影響使用下列產品核發的生產憑證延長的PDF檔案： **Adobe根CA** 基於證書（舊證書）。 所有PDF檔案(使用2023年1月7日之前的舊憑證延長的Reader，包括客戶下載的憑證)都會繼續使用套用至這些檔案的所有使用權限，且不需要任何更新。

新的證書頒發機構， **Adobe根CA G2**&#x200B;現在提供以新憑證授權為基礎的、和憑證。 2023年1月7日或之前，開始使用新憑證，這些憑證以 **Adobe根CA G2** —Reader擴展新PDF文檔。  您可以 [從Adobe授權網站取得新憑證](https://licensing.adobe.com/) 或Adobe支援。

## 常見問答

**問：Adobe根憑證和Acrobat Reader擴充功能憑證有何不同？ Adobe根憑證是否與Acrobat Reader擴充功能憑證相依？ 這兩份證書是否將於2023年1月到期？**

A.Adobe根CA是核發Acrobat Reader擴充功能憑證的憑證機構。 2023年1月7日起，「Adobe根CA」及其核發的所有憑證即將到期。

**Q.之前曾有一份Adobe來函，內容涉及證書的過期以及對使用/開啟PDF檔案的影響。 應該忽略這種溝通嗎？**

A.根據對情況的重新評估，2023年1月7日之前使用舊的&quot;Adobe根CA&quot;簽發的生產證書延期的所有PDF檔案在2023年1月7日之後仍可繼續運作，且無任何變更。 如果您已更新PDF檔案，體驗不會有任何變更。

**如果有其他問題，我應該聯絡誰？**

A.您可以聯絡 [Adobe支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 或提供支援票。

**問：如果我在2023年1月7日前未更新憑證，會發生什麼事？**

A. 2023年1月7日之前，所有使用舊版「Adobe根CA」核發的生產憑證延期的PDF檔案，在2023年1月7日之後仍可繼續運作，且無任何變更。 使用評估證書擴展的PDF在到期日後無法工作。

**新憑證的說明是否與舊憑證有所不同？**

A.新Acrobat Reader擴充功能憑證的說明提及 **G3-P24** 作為方案名稱。 在舊憑證的說明中(以「Adobe根CA」為基礎的憑證), **P24** 被提及為方案名稱。

**問：如何取得最新憑證？**

A.所有獲授權的Forms客戶（具有作用中授權）都可從以下網址下載新憑證(以「Adobe根CA G2」為基礎的憑證): [Adobe授權網站](https://licensing.adobe.com/). 如果您在Adobe授權網站上找不到憑證，請聯絡 [Adobe支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) 或提供支援票。

**問：我使用「Adobe根CA」（舊的憑證授權單位）核發的憑證延期的PDF檔案，在2023年1月7日之後能繼續運作嗎？**

A.是的，在2023年1月7日之前，所有使用「Adobe根CA」（舊憑證授權單位）核發的生產憑證延期的PDF檔案，在2023年1月7日之後仍可繼續運作，且無任何變更。 使用評估證書擴展的PDF文檔在過期後停止工作。

**問：若要繼續使用以「Adobe根CA」（舊的憑證授權單位）核發的憑證擴充的PDF檔案，需要使用哪個Adobe Acrobat Reader版本？**

A.Adobe Acrobat Reader 2020或更新版本必須使用以「Adobe根CA」（舊的憑證授權單位）擴充的PDF檔案。 這是發佈本檔案時支援的Acrobat Reader版本。 如果您使用 [不支援的Adobe Acrobat版本](https://helpx.adobe.com/tw/support/programs/eol-matrix.html),Adobe建議您 [下載並安裝最新版Adobe Acrobat Reader](https://get.adobe.com/reader/).

**問：若要繼續使用以「Adobe根CA 2」（新憑證授權單位）核發的憑證擴充的PDF檔案，需要使用哪個Adobe Acrobat Reader版本？**

A.Adobe Acrobat Reader 2020或更新版本必須使用以「Adobe根CA 2」（新憑證授權單位）擴充的PDF檔案。 如果您使用 [不支援的Adobe Acrobat Reader版本](https://helpx.adobe.com/tw/support/programs/eol-matrix.html),Adobe建議您 [下載並安裝最新版Adobe Acrobat Reader](https://get.adobe.com/reader/).

**問：我可以刪除舊的Acrobat Reader擴充功能憑證，並在Adobe Experience Manager Forms伺服器上新增憑證，同時繼續使用現有的別名嗎？**

答：可以，您可以刪除舊的Acrobat Reader擴充功能憑證，並以現有別名新增憑證至Adobe Experience Manager Forms伺服器。

**問：我可以將新和舊的Acrobat Reader擴充功能憑證保留在Adobe Experience Manager Forms伺服器上嗎？**

答：可以，您可以在Adobe Experience Manager Forms伺服器上保留兩個憑證，但使用不同別名。 在2023年1月7日之後，您只能使用新憑證來Reader擴充PDF檔案。

**問：我可以匯入相同的Acrobat Reader擴充功能憑證至所有Adobe Experience Manager Forms環境嗎？**

答：是，可在多個環境中使用相同的Acrobat Reader擴充功能憑證。

**問：如何檢查套用至PDF檔案的使用權限？**

A.您可以使用 [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API，擷取套用至PDF檔案的使用權限相關資訊。

**問：如何變更Acrobat Reader擴充功能憑證檔案的密碼？**

A.在Microsoft Windows上，若要變更憑證密碼，請使用Microsoft管理控制台(MMC)安裝憑證，然後選取 **將密鑰標籤為可導出**. 安裝後，使用私鑰導出證書，並為PFX檔案使用其他密碼。


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
