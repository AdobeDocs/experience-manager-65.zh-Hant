---
title: 配置SAML服務提供程式設定
seo-title: Configure SAML service provider settings
description: 您可以設定SAML服務提供者設定，讓使用者透過指定的第三方身分提供者(IDP)登入及驗證AEM表單。
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# 配置SAML服務提供程式設定{#configure-saml-service-provider-settings}

安全斷言標籤語言(SAML)是在為企業或混合域配置授權時可選擇的選項之一。 SAML主要用於支援跨多個網域的SSO。 將SAML設為驗證提供者時，使用者會透過指定的協力廠商身分提供者(IDP)登入AEM表單並進行驗證。

如需SAML的說明，請參閱 [安全聲明標籤語言(SAML)V2.0技術概述](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. 在管理控制台中，按一下「設定>使用者管理>設定> SAML服務提供者設定」 。
1. 在「服務提供者實體ID」方塊中，輸入唯一ID以用作AEM表單服務提供者實作的識別碼。 您也可在設定IDP時指定此唯一ID(例如 `um.lc.com`.) 您也可以使用用來存取AEM表單的URL(例如 `https://AEMformsserver`)。
1. 在「服務提供者基本URL」方塊中，輸入表單伺服器的基本URL(例如， `https://AEMformsserver:8080`)。
1. （可選）若要讓AEM表單傳送已簽署的驗證請求給IDP，請執行下列工作：

   * 使用信任管理器以PKCS #12格式導入憑據，並選擇文檔簽名憑據作為信任儲存類型。 (請參閱 [管理本機憑證](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * 在「服務提供程式憑據密鑰別名」清單中，選擇在信任儲存中分配給憑據的別名。
   * 按一下「匯出」 ，將URL內容儲存至檔案，然後將該檔案匯入您的IDP。

1. （選用）在「服務提供者名稱ID原則」清單中，選取IDP在SAML斷言中用來識別使用者的名稱格式。 選項為「未指定」、「電子郵件」和「Windows網域限定名稱」。

   >[!NOTE]
   >
   >名稱格式不區分大小寫。

1. （可選）選擇為本地用戶啟用身份驗證提示。 選取此選項後，使用者會看到兩個連結：

   * 第三方SAML身分提供者的登入頁面連結，屬於企業網域的使用者可在此驗證。
   * AEM表單登入頁面的連結，屬於本機網域的使用者可在此頁面驗證。

   若未選取此選項，系統會直接將使用者帶往協力廠商SAML身分提供者的登入頁面，屬於企業網域的使用者可在此進行驗證。

1. （可選）選擇啟用對象綁定以啟用對象綁定支援。 依預設，POST系結會與SAML搭配使用。 但是，如果已配置對象綁定，請選擇此選項。 選取此選項時，實際的使用者斷言不會透過瀏覽器請求傳遞。 而是會傳遞斷言的指標，並使用後端Web服務呼叫來擷取斷言。
1. （選用）選取「啟用重新導向系結」 ，以支援使用重新導向的SAML系結。
1. （選用）在自訂屬性中，指定其他屬性。 其他屬性是由新行分隔的name=value對。

   * 您可以設定AEM表單，以針對符合第三方聲明之有效期的有效期發出SAML聲明。 若要遵循協力廠商SAML斷言逾時，請在自訂屬性中新增下列行：

      `saml.sp.honour.idp.assertion.expiry=true`

   * 添加以下自定義屬性以使用RelayState來確定成功驗證後將重定向用戶的URL。

      `saml.sp.use.relaystate=true`

   * 添加以下自定義屬性以配置自定義Java Server Pages(JSP)的URL，該URL將用於呈現身份提供程式的註冊清單。 如果尚未部署自定義Web應用程式，它將使用預設的「用戶管理」頁來呈現清單。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 按一下「儲存」。
