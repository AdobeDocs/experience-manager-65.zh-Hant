---
title: 為檔案安全性設定來自外部瀏覽器的延伸驗證
description: 瞭解如何設定外部瀏覽器驗證，讓使用者能使用系統預設網頁瀏覽器，在Acrobat或Reader中驗證受原則保護的PDF檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 98a772829d3568a5826ea9e3ae65760f1587040f
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 1%

---

# 為檔案安全性設定來自外部瀏覽器的延伸驗證 {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> 確保您擁有存取AEM Forms管理控制檯的管理員許可權。

來自外部瀏覽器的延伸驗證可讓使用者使用系統的預設網頁瀏覽器（例如Microsoft Edge或Google Chrome），而不是Acrobat或Reader中的內嵌瀏覽器控制項，來驗證受原則保護的PDF檔案。 如此可啟用現代化的驗證方法，例如PassKey、生物測定驗證，以及其他需要現代化瀏覽器的身分提供者(IDP)功能。

啟用後，在Acrobat或Reader中開啟受原則保護的檔案會在使用者的預設瀏覽器中啟動IDP登入頁面。 驗證後，系統會自動將使用者重新導向回Acrobat或Reader，且檔案會解除鎖定。

## 先決條件 {#prerequisites}

在設定外部瀏覽器驗證之前，請確定符合以下要求：

* JEE上的AEM Forms 6.5已部署Service Pack 6.5.25.0，或Service Pack 6.5.24.0，並在支援的應用程式伺服器（JBoss、WebLogic或WebSphere）上安裝適用的JEE Hotfix修補程式。 檢視AEM Forms JEE Hotfix2的[軟體發佈連結6.5.24.0](#software-distribution-links)。
* 延伸驗證（協力廠商驗證）已啟用，且可與IDP搭配使用。 請參閱[伺服器組態設定](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)和[新增延伸驗證提供者](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider)。
* 使用最新更新安裝在使用者端Windows電腦上的Adobe Acrobat Pro或Adobe Acrobat Reader （64位元）

### AEM Forms JEE Hotfix2 6.5.24.0的軟體發佈連結 {#software-distribution-links}

JEE Service Pack 6.5.25.0和更新版本上的AEM Forms提供外部瀏覽器驗證。

如果您使用JEE Service Pack 6.5.24.0或更舊版本的AEM Forms，請執行下列任一項作業：

* 升級至JEE Service Pack 6.5.25.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)上的[AEM Forms。
* 使用以下連結，為您的應用程式伺服器和平台安裝AEM Forms JEE Hotfix 6.5.24.0修補程式。

從[AEM Forms Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載並安裝您平台的Adobe JEE Hotfix 6.5.24.0修補程式：

**JBoss**

* Windows：適用於JBoss JEE伺服器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)的Windows上AEM Service Pack 6.5.24.0的[Hotfix
* Linux：適用於JBoss JEE伺服器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)的Linux上AEM Service Pack 6.5.24.0的[Hotfix

**WebSphere**

* Windows：適用於WebSphere JEE伺服器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)的Windows上AEM Service Pack 6.5.24.0的[Hotfix
* Linux：適用於WebSphere JEE伺服器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)的Linux上AEM Service Pack 6.5.24.0的[Hotfix

**WebLogic**

* Windows：適用於WebLogic JEE伺服器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)的Windows上AEM Service Pack 6.5.24.0的[Hotfix
* Linux：適用於WebLogic JEE伺服器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)的Linux上AEM Service Pack 6.5.24.0的[Hotfix

如需安裝指示，請參閱[安裝JEE修補程式](/help/release-notes/jee-patch-installer-65.md)。

## 啟用外部瀏覽器驗證 {#enable-external-browser-authentication}

本影片說明如何在AEM Forms Document Security伺服器上啟用外部瀏覽器驗證。

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. 在管理主控台中，按一下&#x200B;**服務** > **Document Security** > **設定** > **伺服器設定**。
1. 找到&#x200B;**允許外部瀏覽器對Adobe使用者端應用程式的延伸驗證**&#x200B;區段。
1. 選取您要啟用之每個Adobe使用者端平台的核取方塊：
   * **Adobe Acrobat和Reader （64位元） — 案頭**
   * **Adobe Acrobat Reader （32位元） — 案頭**
1. 按一下&#x200B;**「確定」**。

如需伺服器設定描述，請參閱[伺服器組態設定](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)。

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## 驗證 {#verification}

本影片將展示如何驗證外部瀏覽器驗證：在Acrobat中開啟受原則保護的PDF，透過您的預設瀏覽器登入，並確認檔案在驗證後解除鎖定。

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. 使用Document Security伺服器建立受原則保護的PDF檔案。
1. 在Windows使用者端電腦上，在Acrobat Pro或Acrobat Reader中開啟受保護的PDF。
1. 同意對話方塊會顯示在Acrobat中。 按一下&#x200B;**登入**。
1. 確認系統預設瀏覽器會以IDP登入頁面開啟。
1. 完成驗證。
1. 確認受保護的檔案已成功開啟。

## 疑難排解 {#troubleshooting}

### 內嵌瀏覽器會開啟，而非系統瀏覽器 {#embedded-browser-opens-instead-of-system-browser}

* 確認伺服器已啟用外部瀏覽器驗證。 請參閱[啟用外部瀏覽器驗證](#enable-external-browser-authentication)。
* 確認Acrobat或Reader版本支援此功能。

### 在瀏覽器中驗證成功，但檔案未解鎖 {#authentication-succeeds-but-document-does-not-unlock}

* 請確定Acrobat或Reader正在執行且未被防火牆或安全軟體封鎖。
* 如果問題仍然存在，請重新安裝或修復Acrobat或Reader安裝，以還原通訊協定處理常式註冊。

### Acrobat中出現「您無法登入」訊息 {#we-couldnt-sign-you-in-message}

* 使用者可能需要太長時間才能完成驗證。 請再試一次。
* 檢查瀏覽器與AEM Forms伺服器之間的網路連線。

### 驗證選項未出現在登入頁面上 {#authentication-option-does-not-appear}

* 驗證方法和選項是由IDP設定，而非由AEM Forms或Acrobat設定。 請確定IDP支援您要使用的驗證方法。
* 確認系統瀏覽器（而非內嵌瀏覽器）中已載入登入頁面。
