---
title: 管理證書和憑據的基礎知識
seo-title: Basics of managing certificates and credentials
description: 瞭解管理證書和憑據的基本知識。
seo-description: Learn about the basics of managing certificates and credentials.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 管理證書和憑據的基礎知識 {#basics-of-managing-certificates-and-credentials}

A *憑據* 包含簽名或標識文檔所需的私鑰資訊。 A *證書* 是您為信任配置的公鑰資訊。 AEM表單使用證書和憑據用於以下幾種用途：

* Acrobat Reader DC擴展使用憑據在PDF文檔中啟用Adobe Reader使用權。 (請參閱 [配置用於Acrobat Reader DC擴展的憑據](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。)
* 您可以配置Rights Management，以顯示僅由受信任的發行方在Acrobat使用的憑據。 (請參閱 [配置Rights Management顯示設定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)。) 證書中必須存在公用名(CN)。
* 簽名服務訪問證書和憑據。 有關簽名服務的詳細資訊，請參見 [服務參考](https://www.adobe.com/go/learn_aemforms_services_65)。

**生成對密鑰**

表AEM單使用其信任儲存來儲存和管理證書、憑據和證書吊銷清單(CRL)。 此外，您還可以使用獨立的硬體安全模組(HSM)設備來儲存私鑰。

表AEM單不提供任何生成密鑰對的選項。 但是，您可以使用Java鍵工具等工具生成它，然後在Trust Store窗體中AEM導入它。 有關Java鍵工具的詳細資訊，請參見以下內容：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

支援以下簽名類型，並可以以表單形式導AEM入：

* XML簽名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA簽名

**處理丟失或損壞的密鑰**

如果您懷疑您的密鑰丟失或已被洩露，請執行以下操作：

1. 通知認證機構，以便他們在證書吊銷清單中添加被洩露的密鑰以吊銷密鑰。
1. 從認證機構獲取新密鑰及其證書。
1. 再次使用新密鑰對使用被洩露的密鑰簽名的文檔進行簽名。
