---
title: 管理憑證和憑證的基本知識
seo-title: 管理憑證和憑證的基本知識
description: 了解管理憑證和憑證的基本知識。
seo-description: 了解管理憑證和憑證的基本知識。
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 管理證書和憑據的基本知識{#basics-of-managing-certificates-and-credentials}

*憑據*&#x200B;包含簽名或標識文檔所需的私鑰資訊。 *certificate*&#x200B;是您為信任配置的公鑰資訊。 AEM forms使用憑證和憑證有數種用途：

* Acrobat Reader DC擴充功能使用憑證來啟用PDF檔案中的Adobe Reader使用權限。 (請參閱[設定憑證以與Acrobat Reader DC擴充功能搭配使用](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)。)
* 您可以設定Rights Management以顯示憑證，僅供信任發行者在Acrobat中使用。 (請參閱[配置Rights Management顯示設定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)。) 證書中必須包含通用名稱(CN)。
* 簽名服務訪問證書和憑據。 有關簽名服務的詳細資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

**產生配對金鑰**

AEM表單使用其信任儲存來儲存和管理憑證、憑證和憑證撤銷清單(CRL)。 此外，您可以使用獨立的硬體安全模組(HSM)設備來儲存私鑰。

AEM Forms不提供產生金鑰組的任何選項。 不過，您可以使用工具（例如Java鍵值工具）產生它，然後將其匯入AEM Forms信任存放區。 如需Java鍵工具的詳細資訊，請參閱下列內容：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

支援下列簽名類型，並可以在AEM表單中匯入：

* XML簽名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA簽名

**處理丟失或損壞的密鑰**

如果您懷疑密鑰丟失或已被洩露，請採取以下操作：

1. 通知認證機構，使其在證書撤銷清單上添加被破壞的密鑰以撤銷密鑰。
1. 向認證機構獲取新密鑰及其證書。
1. 使用新密鑰再次使用已損壞的密鑰簽名的文檔。
