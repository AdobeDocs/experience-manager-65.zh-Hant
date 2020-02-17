---
title: 啟用AEM以搜尋檔案安全性保護的PDF檔案
seo-title: 啟用AEM以搜尋檔案安全性保護的PDF檔案
description: '瞭解如何啟用原生AEM搜尋，對受DRM保護的PDF檔案執行全文搜尋。  '
seo-description: '瞭解如何啟用原生AEM搜尋，對受DRM保護的PDF檔案執行全文搜尋。  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 啟用AEM以搜尋檔案安全性保護的PDF檔案{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜尋功能可以搜尋和尋找AEM資產，並對各種常用的檔案格式（例如純文字檔案、Microsoft office檔案和PDF檔案）執行文字搜尋。 您也可以延伸原生搜尋功能，對使用AEM Document Security保護的 [PDF檔案執行全文搜尋](../../forms/using/admin-help/document-security.md)。 若要讓AEM對此類檔案執行全文搜尋，請執行下列步驟：

1. 建立安全連接
1. 為受原則保護的範例PDF檔案建立索引

## 必備條件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 在 [AEM Forms伺服器上安裝](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms Document Security Indexer套件。

   * 請確定JEE伺服器上的AEM Forms已啟動並正在執行，而且JEE伺服器上的對應AEM Forms上已安裝檔案安全性。 JEE伺服器上的AEM表格是為受保護的檔案建立索引的必要項。

* 如果您只在JEE伺服器上使用AEM Forms，則已安裝索引器套件。
* 確保所有捆綁包均已啟動並運行。 如果所有捆綁包都未激活，請等待所有捆綁包都啟動並運行。

   * 對於OSGi上的AEM Forms，這些組合會列在https://[server]:[port]/system/console/bundles。
   * 對於JEE上的AEM Forms，這些組合會列在https://[server]:[port]/[context-path]/system/console/bundles中。 例如https://localhost:8080/lc/system/console/bundles。

* 將 *sun.util.calendar包列入白名單* 。 要將軟體包列入白名單，請執行以下步驟：

   1. 開啟AEM Web Console。 URL是https://[server]:[port]/system/console/configMgr。
   1. 找到並開啟「還原序列化 **防火牆設定」**。

   1. 將sun.util.calendar包添加到白名單類或包前置詞欄位，然後按一下 **保存**。

### 在AEM Forms JEE和OSGi堆疊之間建立安全連線 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用下列方法之一來建立安全連接：

* 在JEE管理員認證上，使用AEM Forms設定Adobe LiveCycle Client SDK Bundle
* 使用相互驗證來設定Adobe LiveCycle Client SDK套件

#### 在JEE管理員認證上，使用AEM Forms設定Adobe LiveCycle Client SDK Bundle {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM Web Console。 URL是https://[server]:[port]/system/console/configMgr。
1. 尋找並開啟 **Adobe LiveCycle Client SDK Bundle**。 指定下列欄位的值：

   * **** 伺服器URL:指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數重新啟動伺服器。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。
   * **** 使用者名稱：指定JEE帳戶上的AEM Forms使用者名稱，以用來從AEM伺服器啟動呼叫。 指定的帳戶必須擁有在JEE伺服器上的AEM Forms上啟動檔案服務的權限。
   * **密碼**:指定「使用者名稱」欄位中提及之AEM Forms on JEE帳戶的密碼。
   按一下&#x200B;**「儲存」**。AEM已啟用，可搜尋檔案保全保護的PDF檔案。

#### 使用相互驗證來設定Adobe LiveCycle Client SDK套件 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參 [閱CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEM Web Console。 URL是https://[server]:[port]/system/console/configMgr。
1. 尋找並開啟 **Adobe LiveCycle Client SDK** Bundle。 指定下列屬性的值：

   * **伺服器URL**:指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數重新啟動AEM伺服器。
   * **啟用雙向SSL**:啟用「啟用2向SSL」選項。
   * **KeyStore檔案URL**:指定密鑰庫檔案的URL。
   * **TrustStore FIle URL**:指定truststore檔案的URL。
   * **KeyStore密碼**:指定密鑰庫檔案的密碼。
   * **TrustStorePassword**:指定truststore檔案的密碼。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。
   按一下&#x200B;**「儲存」**。AEM已啟用，可搜尋檔案安全性保護的PDF檔案

### 為受原則保護的範例PDF檔案建立索引 {#index-a-sample-policy-protected-pdf-document}

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset manager中建立檔案夾，並將受原則保護的PDF檔案上傳至新建立的檔案夾。

   現在，您可以使用AEM搜尋來搜尋受原則保護的檔案。

