---
title: 使AEM能夠搜索受文檔安全保護的PDF和Microsoft Office文檔
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: 了解如何啟用原生AEM搜尋，以對受DRM保護的PDF檔案執行全文搜尋。
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# 使AEM能夠搜索受文檔安全保護的PDF和Microsoft Office文檔{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供使用者介面，可供搜尋及尋找儲存在AEM中的各種資產。 本機搜索能夠搜索和定位AEM資產，並對各種常用的文檔格式(如純文字檔案檔案、Microsoft Office文檔和PDF文檔)執行文本搜索。 您還可以擴展並啟用本機搜索，以對受DRM保護的PDF和Microsoft Office文檔執行全文搜索。

執行下列步驟以使AEM能夠搜索受文檔安全保護的PDF和Microsoft Office文檔：

## 開始之前 {#before-you-start}

* 安裝及設定AEM Forms檔案安全性。
* 將sun.util.calendar包添加到 **反序列化防火牆配置。** 設定列於 `https://'[server]:[port]'/system/console/configMgr`.
* 請確定所有AEM套件組合皆已啟動並執行。 套件組合列於 `https://'[server]:[port]'/system/console/bundles`. 如果所有套件都未啟用，請等待，並在幾分鐘後檢查套件的狀態。

## 在AEM Forms工作流程中建立安全連線(JEE上的AEM Forms) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全連線可讓JEE上的AEM Forms和同一伺服器上執行的OSGi服務之間順暢地傳送資訊。 使用以下方法之一建立安全連接：

* 使用JEE上的AEM Forms管理員憑證設定AEM Forms用戶端SDK套件組合
* 使用相互驗證設定AEM Forms用戶端SDK套件組合

### 使用JEE上的AEM Forms管理員憑證設定AEM Forms用戶端SDK套件組合 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM Configuration Manager並以管理員身分登入。 預設URL為https://&lt;servername>:&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms用戶端SDK套件組合。 指定下列屬性的值：

   * **伺服器URL:** 指定JEE伺服器上AEM Forms的HTTP URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=在JEE伺服器上重新啟動AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 參數。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單中。
   * **用戶名：** 指定JEE帳戶上用來起始來自JEE伺服器上AEM Forms呼叫的AEM Forms使用者名稱。 指定的帳戶必須具有在JEE伺服器上叫用AEM Forms上的檔案服務的權限。
   * **密碼**:在使用者名稱欄位中提及的JEE帳戶上指定AEM Forms的密碼。

   按一下「**儲存**」。AEM可用於搜索受文檔安全保護的PDF和Microsoft Office文檔。

### 使用相互驗證設定AEM Forms用戶端SDK套件組合 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參閱 [CAC與相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. 開啟AEM Configuration Manager並以管理員身分登入。 預設URL為https://&lt;servername>:&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms用戶端SDK套件組合。 指定下列屬性的值：

   * **伺服器URL:** 指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=在JEE伺服器上重新啟動AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 參數。
   * **啟用雙向SSL**:啟用「啟用2向SSL」選項。
   * **KeyStore檔案URL**:指定金鑰存放區檔案的URL。
   * **TrustStore FIle URL**:指定信任儲存檔案的URL。
   * **KeyStore密碼**:指定金鑰存放區檔案的密碼。
   * **TrustStorePassword**:指定信任儲存檔案的密碼。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單中。

   按一下「**儲存**」。AEM可用於搜索受文檔安全保護的PDF和Microsoft Office文檔

## 索引受策略保護的PDF或Microsoft Office文檔的示例 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset Manager中建立資料夾，並將受原則保護的PDF或Microsoft Office檔案上傳至新建立的資料夾。 現在，使用AEM搜索搜索受策略保護文檔的內容。 它必須返回包含搜索文本的文檔。
