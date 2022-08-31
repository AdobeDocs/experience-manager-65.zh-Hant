---
title: SAML 2.0 驗證處理常式
seo-title: SAML 2.0 Authentication Handler
description: 了解AEM中的SAML 2.0驗證處理常式。
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 1%

---

# SAML 2.0 驗證處理常式{#saml-authentication-handler}

AEM隨附 [SAML](https://saml.xml.org/saml-specifications) 驗證處理常式。 此處理常式可支援 [SAML](https://saml.xml.org/saml-specifications) 2.0驗證請求協定（Web-SSO配置檔案），使用 `HTTP POST` 綁定。

它支援：

* 郵件的簽名和加密
* 自動建立使用者
* 將群組同步至AEM中的現有群組
* 服務提供程式和身份提供程式啟動的身份驗證

此處理常式會將加密的SAML回應訊息儲存在使用者節點中( `usernode/samlResponse`)，以方便與協力廠商的通訊。

>[!NOTE]
>
>請參閱 [AEM與SAML整合的示範](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>若要閱讀端對端社群文章，請按一下： [整合SAML與Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## 設定SAML 2.0驗證處理常式 {#configuring-the-saml-authentication-handler}

此 [Web主控台](/help/sites-deploying/configuring-osgi.md) 提供 [SAML](https://saml.xml.org/saml-specifications) 2.0驗證處理程式配置稱為 **AdobeGranite SAML 2.0驗證處理常式**. 可設定下列屬性。

>[!NOTE]
>
>預設會停用SAML 2.0驗證處理常式。 必須至少設定以下屬性之一才能啟用處理程式：
>
>* 身分提供者POSTURL。
>* 服務提供商實體ID。
>


>[!NOTE]
>
>SAML聲明經過簽名，並可以選擇進行加密。 為了讓此功能發揮作用，您必須在TrustStore中至少提供身份提供程式的公開證書。 請參閱 [將IdP憑證新增至TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 一節以取得詳細資訊。

**路徑** Sling應使用此驗證處理常式的存放庫路徑。 如果為空，則會停用驗證處理常式。

**服務排名** OSGi Framework服務排名值，用以指出呼叫此服務的順序。 這是整數值，其中值越高，優先順序越高。

**IDP憑證別名** 全域信任存放區中IdP憑證的別名。 如果此屬性為空，則禁用身份驗證處理程式。 請參閱下方的「將IdP憑證新增至AEM TrustStore」一章，了解如何設定。

**身分提供者URL** IDP的URL，應將SAML驗證要求傳送至此處。 如果此屬性為空，則禁用身份驗證處理程式。

>[!CAUTION]
>
>必須將身分提供者主機名稱新增至 **Apache Sling反向連結篩選器** OSGi配置。 請參閱 [Web主控台](/help/sites-deploying/configuring-osgi.md) 一節以取得詳細資訊。

**服務提供商實體ID** 此ID可唯一識別此服務提供者與身分提供者。 如果此屬性為空，則禁用身份驗證處理程式。

**預設重新導向** 成功驗證後重新導向的預設位置。

>[!NOTE]
>
>此位置僅在 `request-path` cookie未設定。 如果您在未使用有效登入代號的情況下，要求設定路徑下方的任何頁面，則要求的路徑會儲存在Cookie中
>而且，成功驗證後，瀏覽器會重新導向至此位置。

**User-ID屬性** 屬性的名稱，包含在CRX存放庫中用於驗證和建立使用者的使用者ID。

>[!NOTE]
>
>系統不會從 `saml:Subject` SAML聲明的節點，但來自此 `saml:Attribute`.

**使用加密** 此驗證處理常式是否需要加密的SAML斷言。

**自動建立CRX用戶** 是否在成功驗證後自動建立儲存庫中的非現有用戶。

>[!CAUTION]
>
>如果停用CRX使用者的自動建立，則必須手動建立使用者。

**新增至群組** 成功驗證後，是否應自動將使用者新增至CRX群組。

**群組成員資格** 此使用者應新增至的saml:Attribute名稱包含CRX群組清單。

## 將IdP憑證新增至AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML聲明經過簽名，並可以選擇進行加密。 為了讓此功能發揮作用，您必須在存放庫中提供至少IdP的公開憑證。 為此，您需要：

1. 前往 *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 按下 **[!UICONTROL 建立TrustStore連結]**
1. 輸入TrustStore的密碼，然後按 **[!UICONTROL 儲存]**.
1. 按一下 **[!UICONTROL 管理TrustStore]**.
1. 上傳IdP憑證。
1. 記下憑證別名。 別名為 **[!UICONTROL admin#1436172864930]** 在以下範例中。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 將服務提供者金鑰和憑證鏈新增至AEM金鑰存放區 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下步驟為必要步驟，否則將擲回下列例外： `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 前往： [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 編輯 `authentication-service` 使用者。
1. 按一下 **建立KeyStore** 在 **帳戶設定**.

>[!NOTE]
>
>只有當處理程式能夠對消息進行簽名或解密時，才需要執行以下步驟。

1. 按一下以上傳私密金鑰檔案 **選擇私鑰檔案**. 密鑰表示為PKCS#8格式，且具有DER編碼。
1. 按一下「 」，上傳憑證檔案 **選擇證書鏈檔案**.
1. 分配別名，如下所示：

   ![chlimage_1-373](assets/chlimage_1-373.png)

## 為SAML配置記錄器 {#configure-a-logger-for-saml}

您可以設定記錄器，以偵錯因錯誤設定SAML而可能產生的任何問題。 您可以透過以下方式達成此目的：

1. 前往Web主控台，位於 *http://localhost:4502/system/console/configMgr*
1. 搜尋並按一下以下項目： **Apache Sling Logging Logger Configuration**
1. 使用以下配置建立記錄器：

   * **記錄層級：** 除錯
   * **日誌檔案：** logs/saml.log
   * **記錄器：** com.adobe.granite.auth.saml
