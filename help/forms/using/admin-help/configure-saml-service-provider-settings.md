---
title: 設定SAML服務提供者設定
description: 您可以設定SAML服務提供者設定，讓使用者透過指定的協力廠商身分提供者(IDP)登入並驗證AEM Forms。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# 設定SAML服務提供者設定{#configure-saml-service-provider-settings}

安全宣告標籤語言(SAML)是您在設定企業或混合式網域的授權時可以選取的選項之一。 SAML主要用於支援跨多個網域的SSO。 當SAML設定為您的驗證提供者時，使用者會透過指定的第三方身分提供者(IDP)登入並驗證AEM Forms。

如需SAML的說明，請參閱 [安全性宣告標籤語言(SAML) V2.0技術概覽](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

1. 在管理控制檯中，按一下「設定>使用者管理>設定> SAML服務提供者設定」。
1. 在「服務提供者實體ID」方塊中，輸入唯一ID以用作AEM表單服務提供者實作的識別碼。 您也可以在設定IDP時指定此唯一ID (例如 `um.lc.com`.) 您也可以使用用來存取AEM表單的URL (例如 `https://AEMformsserver`)。
1. 在「服務提供者基本URL」方塊中，輸入您Forms伺服器的基本URL (例如 `https://AEMformsserver:8080`)。
1. （選擇性）若要讓AEM Forms傳送已簽署的驗證要求給IDP，請執行下列工作：

   * 使用信任管理員匯入PKCS #12格式的認證，並選取檔案簽署認證作為信任存放區型別。 (請參閱 [管理本機認證](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * 在「服務提供者認證金鑰別名」清單中，選取您在「信任存放區」中指派給認證的別名。
   * 按一下「匯出」，將URL內容儲存至檔案，然後將該檔案匯入IDP。

1. （選擇性）在「服務提供者名稱ID原則」清單中，選取IDP在SAML宣告中用來識別使用者的名稱格式。 選項包括「未指定」、「電子郵件」和「Windows網域限定名稱」。

   >[!NOTE]
   >
   >名稱格式不區分大小寫。

1. （選擇性）選取「為本機使用者啟用驗證提示」。 選取此選項時，使用者會看到兩個連結：

   * 第三方SAML識別提供者登入頁面的連結，屬於企業網域的使用者可在此進行驗證。
   * AEM表單登入頁面的連結，屬於本機網域的使用者可在此進行驗證。

   如果未選取此選項，使用者會直接進入第三方SAML身分提供者的登入頁面，其中屬於企業網域的使用者可以驗證。

1. （選擇性）選取啟用成品繫結以啟用成品繫結支援。 根據預設，POST繫結會與SAML搭配使用。 但如果您已設定成品繫結，請選取此選項。 選取此選項時，不會透過瀏覽器請求傳遞實際使用者宣告。 相反地，會傳遞宣告指標，並使用後端Web服務呼叫擷取宣告。
1. （選擇性）選取「啟用重新導向繫結」以支援使用重新導向的SAML繫結。
1. （選用）在自訂屬性中，指定其他屬性。 其他屬性為名稱=值配對，以新行分隔。

   * 您可以設定AEM表單，針對符合協力廠商宣告有效期間的有效期間發出SAML宣告。 若要遵守第三方SAML宣告逾時，請在自訂屬性中新增下列行：

     `saml.sp.honour.idp.assertion.expiry=true`

   * 新增下列自訂屬性，以使用RelayState判斷在成功驗證後要將使用者重新導向的URL。

     `saml.sp.use.relaystate=true`

   * 新增下列自訂屬性，讓您能夠設定自訂Java™ Server Pages (JSP)的URL，此自訂URL用於呈現已註冊的身分識別提供者清單。 如果您尚未部署自訂Web應用程式，則會使用預設的「使用者管理」頁面來呈現清單。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 按一下「儲存」。
