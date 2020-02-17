---
title: 管理憑證和認證的基本知識
seo-title: 管理憑證和認證的基本知識
description: 瞭解管理憑證和認證的基本資訊。
seo-description: 瞭解管理憑證和認證的基本資訊。
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理憑證和認證的基本知識 {#basics-of-managing-certificates-and-credentials}

憑 *據包含* ，您簽署或識別檔案所需的私密金鑰資訊。 憑 *證* ，是您設定為信任的公開金鑰資訊。 AEM表單使用憑證和認證，用於數種用途：

* Acrobat Reader DC擴充功能使用憑證，以啟用PDF檔案中的Adobe Reader使用權限。 (請參 [閱設定認證以搭配Acrobat Reader DC擴充功能使用](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions))。
* 您可以設定Rights Management，以顯示憑證，僅供受信任發行者在Acrobat中使用。 (請參 [閱設定Rights Management顯示設定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings))。證書中必須包含通用名稱(CN)。
* 簽章服務會存取憑證和認證。 如需簽名服務的詳細資訊，請參閱服 [務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

**生成對密鑰**

AEM表單使用其信任商店來儲存和管理憑證、認證和憑證撤銷清單(CRL)。 此外，您還可以使用獨立的硬體安全模組(HSM)裝置來儲存私密金鑰。

AEM表格不提供任何產生金鑰對的選項。 不過，您可以使用工具（例如Java keytool）產生它，並將它匯入AEM Forms信任商店。 如需Java鍵工具的詳細資訊，請參閱下列：

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

支援下列簽名類型，並可在AEM表單中匯入：

* XML簽名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA簽名

**處理丟失或損壞的密鑰**

如果您懷疑密鑰丟失或已洩露，請採取以下措施：

1. 通知認證機構，使認證機構在證書撤銷清單上添加被危害的密鑰來撤銷密鑰。
1. 從認證機構取得新金鑰及其憑證。
1. 使用新密鑰再次使用受損密鑰簽署的文檔。

