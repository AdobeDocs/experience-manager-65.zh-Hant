---
title: 讓AEM搜尋受檔案安全性保護的PDF和Microsoft office檔案
seo-title: 讓AEM搜尋受檔案安全性保護的PDF和Microsoft office檔案
description: 瞭解如何啟用原生AEM搜尋，對受DRM保護的PDF檔案執行全文搜尋。
seo-description: 瞭解如何啟用原生AEM搜尋，對受DRM保護的PDF檔案執行全文搜尋。
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 讓AEM搜尋受檔案安全性保護的PDF和Microsoft office檔案{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience manager提供使用者介面，可搜尋及尋找儲存在AEM中的各種資產。 原生搜尋功能可搜尋和尋找AEM資產，並針對各種常用的檔案格式（例如純文字檔案、Microsoft office檔案和PDF檔案）執行文字搜尋。 您也可以擴充並啟用原生搜尋功能，對受DRM保護的PDF和Microsoft office檔案執行全文搜尋。

執行下列步驟，讓AEM搜尋受檔案安全性保護的PDF和Microsoft office檔案：

## 開始之前 {#before-you-start}

* 安裝及設定AEM Forms檔案安全性。
* 將sun.util.calendar包添加到還原序列化防火牆配 **置的白名單中。** 配置列於 `https://[server]:[port]/system/console/configMgr`。
* 確定所有AEM搭售都已啟動並執行。 捆綁包列於 `https://[server]:[port]/system/console/bundles`。 如果所有捆綁包都未激活，請等待，並在幾分鐘後檢查捆綁包的狀態。

## 在AEM Forms工作流程中建立安全連線（JEE上的AEM Forms） {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全連線可讓JEE上的AEM Forms與在同一伺服器上執行的OSGi服務之間順暢地傳送資訊。 使用以下方法之一建立安全連接：

* 在JEE管理員認證上使用AEM Forms設定AEM Forms用戶端SDK套裝
* 使用相互驗證來設定AEM Forms Client SDK套件

### 在JEE管理員認證上使用AEM Forms設定AEM Forms用戶端SDK套裝 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM設定管理員，並以管理員身分登入。 預設URL為https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms Client SDK套裝。 指定下列屬性的值：

   * **** 伺服器URL:指定JEE伺服器上AEM Forms的HTTP URL。 若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數，重新啟動JEE伺服器上的AEM Forms。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。
   * **** 使用者名稱：指定JEE帳戶上的AEM Forms使用者名稱，以用來從JEE伺服器上的AEM Forms啟動呼叫。 指定的帳戶必須擁有在JEE伺服器上叫用AEM Forms的Document Services的權限。
   * **密碼**:指定「使用者名稱」欄位中提及之AEM Forms on JEE帳戶的密碼。
   按一下&#x200B;**「儲存」**。AEM已啟用，可搜尋受檔案安全性保護的PDF和Microsoft office檔案。

### 使用相互驗證來設定AEM Forms Client SDK套件 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參 [閱CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEM設定管理員，並以管理員身分登入。 預設URL為https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms Client SDK套裝。 指定下列屬性的值：

   * **** 伺服器URL:指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數，重新啟動JEE伺服器上的AEM Forms。
   * **啟用雙向SSL**:啟用「啟用2向SSL」選項。
   * **KeyStore檔案URL**:指定密鑰庫檔案的URL。
   * **TrustStore FIle URL**:指定truststore檔案的URL。
   * **KeyStore密碼**:指定密鑰庫檔案的密碼。
   * **TrustStorePassword**:指定truststore檔案的密碼。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。
   按一下&#x200B;**「儲存」**。AEM已啟用，可搜尋受檔案安全性保護的PDF和Microsoft office檔案

## 為受原則保護的範例PDF或Microsoft office檔案建立索引 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset manager中建立檔案夾，並將受原則保護的PDF或Microsoft office檔案上傳至新建立的檔案夾。 現在，請使用AEM搜尋來搜尋受原則保護檔案的內容。 它必須返回包含搜索文本的文檔。

