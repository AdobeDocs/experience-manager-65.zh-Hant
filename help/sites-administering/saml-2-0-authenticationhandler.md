---
title: SAML 2.0驗證處理常式
seo-title: SAML 2.0驗證處理常式
description: 瞭解AEM中的SAML 2.0驗證處理常式。
seo-description: 瞭解AEM中的SAML 2.0驗證處理常式。
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
translation-type: tm+mt
source-git-commit: a44d655871308dac34671f0af2c4a0017eba5793

---


# SAML 2.0驗證處理常式{#saml-authentication-handler}

AEM隨附 [SAML驗證處理](http://saml.xml.org/saml-specifications) 常式。 此處理常式支援使 [用系結的SAML](http://saml.xml.org/saml-specifications) 2.0驗證請求通訊協定（Web-SSO描述檔） `HTTP POST` 。

它支援：

* 簽署和加密訊息
* 自動建立使用者
* 同步群組至AEM中的現有群組
* 服務提供者和身分提供者啟始的驗證

此處理常式會將加密的SAML回應訊息儲存在使用者節點( `usernode/samlResponse`)中，以利與協力廠商服務提供者通訊。

>[!NOTE]
>
>檢 [視AEM和SAML整合的示範](https://helpx.adobe.com/cq/kb/saml-demo.html)。
>
>若要閱讀端對端社群文章，請按一下：將 [SAML與Adobe Experience Manager整合](https://helpx.adobe.com/experience-manager/using/aem63_saml.html)。

## 設定SAML 2.0驗證處理常式 {#configuring-the-saml-authentication-handler}

Web [主控台](/help/sites-deploying/configuring-osgi.md) ，提供對稱為 [Adobe Granite SAML 2.0驗證處理常式的](http://saml.xml.org/saml-specifications) SAML **2.0驗證處理常式設定的存取**。 可以設定以下屬性。

>[!NOTE]
>
>SAML 2.0驗證處理常式預設為停用。 您必須至少設定以下屬性之一才能啟用處理程式：
>
>* 身分提供者POST URL。
>* 服務提供者實體ID。
>



>[!NOTE]
>
>SAML斷言會經過簽署，並可選擇加密。 為了達到此目的，您必須至少在TrustStore中提供身分提供者的公開憑證。 如需 [詳細資訊，請參閱將IdP憑證新增至TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 區段。

**Path** Repository路徑，Sling應使用此驗證處理常式。 如果此為空白，則會停用驗證處理常式。

**服務排名** OSGi Framework服務排名值，以指出呼叫此服務的順序。 這是一個整數值，其中較高的值指定較高的優先順序。

**IDP憑證別名** ：全域信任存放區中IdP憑證的別名。 如果此屬性為空，則禁用驗證處理程式。 請參閱下方的「將IdP憑證新增至AEM TrustStore」一章，瞭解如何設定。

**IDP的身分提供者URL** URL,SAML驗證請求應傳送至此IDP。 如果此屬性為空，則禁用驗證處理程式。

>[!CAUTION]
>
>Identity Provider主機名稱必須新增至 **Apache Sling Referrer Filter** OSGi設定。 如需詳細 [資訊，請參閱](/help/sites-deploying/configuring-osgi.md) 「Web主控台」一節。

**服務提供者實體ID** ID，可唯一識別此服務提供者與身分提供者的身分識別。 如果此屬性為空，則禁用驗證處理程式。

**預設重新導向** ：成功驗證後，要重新導向的預設位置。

>[!NOTE]
>
>此位置僅在未設定Cookie `request-path` 時使用。 如果您要求設定路徑下方的任何頁面，但沒有有效的登入Token，請求的路徑會儲存在Cookie中
>成功驗證後，瀏覽器將重新導向至此位置。

**User-ID Attribute** （用戶ID屬性）包含用於在CRX儲存庫中驗證和建立用戶的用戶ID的屬性的名稱。

>[!NOTE]
>
>使用者ID不會從SAML斷言的 `saml:Subject` 節點取出，而是從此取出 `saml:Attribute`。

**使用加密** ：此驗證處理常式是否需要加密的SAML斷言。

**自動建立CRX用戶** ：是否在成功驗證後自動建立儲存庫中的非現有用戶。

>[!CAUTION]
>
>如果禁用了CRX用戶的自動建立，則必須手動建立用戶。

**新增至群組** ：成功驗證後，是否應自動將使用者新增至CRX群組。

**群組成員資格** ：包含此使用者應加入之CRX群組清單的saml：屬性的名稱。

## 將IdP憑證新增至AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML斷言會經過簽署，並可選擇加密。 為了使此功能發揮作用，您必須至少在儲存庫中提供IdP的公共證書。 為此，您需要：

1. 前往 *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 按建立 **[!UICONTROL 信任商店連結]**
1. 輸入TrustStore的密碼，然後按「 **[!UICONTROL 儲存」]**。
1. 按一下「管 **[!UICONTROL 理信任商店]**」。
1. 上傳IdP憑證。
1. 記下證書別名。 別名為 **[!UICONTROL admin#1436172864930]** ，如下例中。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 將服務提供者金鑰和憑證鏈新增至AEM金鑰庫 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下步驟為必要步驟，否則會引發下列例外： `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 前往： [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 編輯使 `authentication-service` 用者。
1. 按一下「帳戶設定」下 **的「建立KeyStore** 」, **建立KeyStore**。

>[!NOTE]
>
>只有當處理程式應能夠簽署或解密訊息時，才需要下列步驟。

1. 按一下「選取私密金鑰檔案」, **上傳私密金鑰檔案**。 密鑰表示為PKCS#8格式，具有DER編碼。
1. 按一下「選取憑證鏈 **檔案」上傳憑證檔案**。
1. 指定別名，如下所示：

   ![chlimage_1-373](assets/chlimage_1-373.png)

## 配置SAML的記錄器 {#configure-a-logger-for-saml}

您可以設定記錄器，以除錯任何因SAML設定錯誤而可能產生的問題。 您可以透過下列方式執行此動作：

1. 前往Web Console，網址為 *http://localhost:4502/system/console/configMgr*
1. 搜尋並按一下名為 **Apache Sling Logging Logger Configuration的項目**
1. 使用以下配置建立記錄器：

   * **** 記錄層級：除錯
   * **** 日誌檔案：logs/saml.log
   * **** 記錄器：com.adobe.granite.auth.saml

