---
title: 設定SAML服務提供者設定
seo-title: 設定SAML服務提供者設定
description: 您可以設定SAML服務提供者設定，讓使用者透過指定的第三方身分提供者(IDP)登入AEM表單並進行驗證。
seo-description: 您可以設定SAML服務提供者設定，讓使用者透過指定的第三方身分提供者(IDP)登入AEM表單並進行驗證。
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定SAML服務提供者設定{#configure-saml-service-provider-settings}

安全斷言標籤語言(SAML)是您在為企業或混合網域設定授權時可選擇的選項之一。 SAML主要用於支援跨多個網域的SSO。 當SAML設定為您的驗證提供者時，使用者會透過指定的第三方身分提供者(IDP)登入並驗證至AEM表單。

如需SAML的說明，請參 [閱安全性斷言標籤語言(SAML)V2.0技術概觀](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf)。

1. 在管理控制台中，按一下「設定>使用者管理>設定> SAML服務供應商設定」。
1. 在「服務提供者實體ID」方塊中，輸入唯一ID以用作AEM表單服務提供者實作的識別碼。 您也可在設定IDP時指定此唯一ID(例如 `um.lc.com`。)您也可以使用用來存取AEM表單的URL(例如 `https://AEMformsserver`)。
1. 在「服務提供者基本URL」方塊中，輸入表單伺服器的基本URL(例如 `https://AEMformsserver:8080`)。
1. （選擇性）若要啟用AEM表格以傳送簽署的驗證要求給IDP，請執行下列工作：

   * 使用Trust Manager可以導入PKCS #12格式的憑據，並將文檔簽名憑據選為信任儲存類型。 (請參 [閱管理本機憑證](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)。)
   * 在服務提供者憑據密鑰別名清單中，選擇在信任儲存中分配給憑據的別名。
   * 按一下「匯出」，將URL內容儲存至檔案，然後將該檔案匯入IDP。

1. （可選）在「服務提供者名稱ID原則」清單中，選取IDP用來在SAML斷言中識別使用者的名稱格式。 選項包括「未指定」、「電子郵件」和「Windows網域限定名稱」。

   >[!NOTE]
   >
   >名稱格式不區分大小寫。

1. （可選）選擇「為本地用戶啟用驗證提示」。 選取此選項時，使用者會看到兩個連結：

   * 協力廠商SAML身分提供者登入頁面的連結，屬於企業網域的使用者可在此驗證。
   * AEM表單登入頁面的連結，屬於本機網域的使用者可在此驗證。
   如果未選取此選項，使用者將直接進入第三方SAML身分提供者的登入頁面，屬於企業網域的使用者可在此頁面進行驗證。

1. （可選）選擇啟用對象綁定以啟用對象綁定支援。 依預設，POST系結會與SAML搭配使用。 但是，如果您已配置「對象綁定」，請選擇此選項。 選取此選項時，實際的使用者斷言不會透過瀏覽器請求傳遞。 而是傳遞斷言的指針，並使用後端Web服務呼叫來擷取斷言。
1. （可選）選取「啟用重新導向系結」，以支援使用重新導向的SAML系結。
1. （可選）在自訂屬性中，指定其他屬性。 其他屬性是由新行分隔的name=value對。

   * 您可以設定AEM表單，以針對符合第三方聲明之有效期的有效期發佈SAML聲明。 若要遵守協力廠商SAML斷言逾時，請在自訂屬性中新增下列行：

      `saml.sp.honour.idp.assertion.expiry=true`

   * 添加以下自定義屬性以使用RelayState來確定成功驗證後將重定向用戶的URL。

      `saml.sp.use.relaystate=true`

   * 新增下列自訂屬性，以設定自訂Java伺服器頁面(JSP)的URL，此URL將用來呈現身分提供者的註冊清單。 如果您尚未部署自訂Web應用程式，則會使用預設的「使用者管理」頁面來呈現清單。
   `saml.sp.discovery.url=/custom/custom.jsp`

1. 按一下「儲存」。

