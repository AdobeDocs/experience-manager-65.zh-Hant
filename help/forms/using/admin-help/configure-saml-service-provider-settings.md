---
title: 配置SAML服務提供程式設定
seo-title: Configure SAML service provider settings
description: 您可以配置SAML服務提供程式設定，以允許用戶通過指AEM定的第三方身份提供程式(IDP)登錄和驗證表單。
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

安全斷言標籤語言(SAML)是配置企業或混合域授權時可以選擇的選項之一。 SAML主要用於支援跨多個域的SSO。 將SAML配置為身份驗證提供程式時，用戶將通過指定的第AEM三方身份提供程式(IDP)登錄表單並對表單進行身份驗證。

有關SAML的說明，請參見 [安全斷言標籤語言(SAML)V2.0技術概述](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf)。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「SAML服務提供程式設定」。
1. 在「服務提供方實體ID」框中，鍵入一個唯一ID，以用作表單服務提供方實AEM現的標識符。 在配置IDP時，您還指定此唯一ID(例如， `um.lc.com`。) 您還可以使用用於訪問表單的URLAEM(例如， `https://AEMformsserver`)。
1. 在「服務提供商基本URL」框中，鍵入表單伺服器的基本URL(例如， `https://AEMformsserver:8080`)。
1. （可選）要啟用表AEM單向IDP發送簽名的身份驗證請求，請執行以下任務：

   * 使用信任管理器導入PKCS #12格式的憑據，並將文檔簽名憑據選作信任儲存類型。 (請參閱 [管理本地憑據](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)。)
   * 在服務提供程式憑據密鑰別名清單中，選擇您在信任儲存中分配給憑據的別名。
   * 按一下「導出」將URL內容保存到檔案，然後將該檔案導入到IDP中。

1. （可選）在「服務提供程式名稱ID策略」清單中，選擇IDP用於在SAML斷言中標識用戶的名稱格式。 這些選項包括「未指定」、「電子郵件」和「Windows域限定名稱」。

   >[!NOTE]
   >
   >名稱格式不區分大小寫。

1. （可選）選擇「為本地用戶啟用身份驗證提示」。 選擇此選項後，用戶將看到兩個連結：

   * 指向第三方SAML標識提供程式的登錄頁的連結，屬於企業域的用戶可以在此進行身份驗證。
   * 到表單登錄頁AEM的連結，屬於本地域的用戶可以在此進行身份驗證。

   如果未選擇此選項，則用戶將直接進入第三方SAML標識提供程式的登錄頁，在該頁中，屬於企業域的用戶可以進行身份驗證。

1. （可選）選擇啟用對象綁定以啟用對象綁定支援。 預設情況下，POST綁定與SAML一起使用。 但是，如果已配置「對象綁定」，請選擇此選項。 選擇此選項後，實際用戶斷言不會通過瀏覽器請求傳遞。 相反，傳遞指向斷言的指針並使用後端Web服務調用檢索斷言。
1. （可選）選擇啟用重新定向綁定以支援使用重定向的SAML綁定。
1. （可選）在自定義屬性中，指定其他屬性。 附加屬性是由新行分隔的name=value對。

   * 您可以AEM配置表單以在與第三方斷言的有效期相匹配的有效期內發出SAML斷言。 要遵守第三方SAML斷言超時，請在「自定義屬性」中添加以下行：

      `saml.sp.honour.idp.assertion.expiry=true`

   * 添加以下自定義屬性以使用RelayState來確定成功驗證後將重定向用戶的URL。

      `saml.sp.use.relaystate=true`

   * 添加以下自定義屬性以配置自定義Java伺服器頁(JSP)的URL，該URL將用於呈現已註冊的身份提供程式清單。 如果尚未部署自定義Web應用程式，它將使用預設的「用戶管理」頁來呈現清單。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 按一下「儲存」。
