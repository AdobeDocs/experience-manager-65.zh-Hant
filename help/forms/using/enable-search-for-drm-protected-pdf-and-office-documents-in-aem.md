---
title: 啟用AEM搜尋檔案安全性保護的PDF和Microsoft Office檔案
seo-title: 啟用AEM搜尋檔案安全性保護的PDF和Microsoft Office檔案
description: 瞭解如何啟用原AEM生搜尋，對受DRM保護的PDF檔案執行全文搜尋。
seo-description: 瞭解如何啟用原AEM生搜尋，對受DRM保護的PDF檔案執行全文搜尋。
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# 啟用AEM搜尋檔案安全性保護的PDF和Microsoft Office檔案{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供使用者介面，以搜尋及尋找儲存在中的各種資產AEM。 原生搜尋功能可搜尋和尋找AEM資產，並針對各種常用的檔案格式（例如純文字檔案、Microsoft Office檔案和PDF檔案）執行文字搜尋。 您也可以擴充並啟用原生搜尋功能，對受DRM保護的PDF和Microsoft Office檔案執行全文搜尋。

執行下列步驟，以AEM搜尋受檔案安全性保護的PDF和Microsoft Office檔案：

## 開始{#before-you-start}之前

* 安裝及設定AEM Forms檔案安全性。
* 將sun.util.calendar包添加到&#x200B;**還原序列化防火牆配置的允許清單中。** 配置列於 `https://'[server]:[port]'/system/console/configMgr`。
* 確保所有AEM捆綁包都已啟動並運行。 捆綁列在`https://'[server]:[port]'/system/console/bundles`。 如果所有捆綁包都未激活，請等待，並在幾分鐘後檢查捆綁包的狀態。

## 在AEM Forms工作流程中建立安全連接(AEM Forms在JEE上){#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全連接使JEE上的AEM Forms和在同一伺服器上運行的OSGi服務之間的資訊流暢無阻。 使用以下方法之一建立安全連接：

* 在JEE管理員認證上使用AEM Forms設定AEM Forms用戶端SDK套件
* 使用相互驗證配置AEM Forms客戶SDK套件

### 在JEE管理員憑證{#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}上使用AEM Forms設定AEM Forms用戶端SDK套件

1. 開啟AEM配置管理器，以管理員身份登錄。 預設URL為https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms用戶端SDK套件。 指定下列屬性的值：

   * **伺服器URL:** 指定JEE伺服器上AEM Forms的HTTP URL。若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數，在JEE伺服器上重新啟動AEM Forms。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。
   * **使用者名** 稱：指定JEE帳戶上AEM Forms的使用者名稱，以用來在JEE伺服器上啟動來自AEM Forms的呼叫。指定的帳戶必須具有在JEE伺服器上調用AEM Forms文檔服務的權限。
   * **密碼**:在「用戶名」欄位中提及的JEE帳戶上指定AEM Forms的密碼。

   按一下「**儲存**」。可AEM搜尋檔案安全性保護的PDF和Microsoft Office檔案。

### 使用相互驗證{#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}配置AEM Forms客戶端SDK包

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參閱[CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEM配置管理器，以管理員身份登錄。 預設URL為https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms用戶端SDK套件。 指定下列屬性的值：

   * **伺服器URL：指** 定JEE伺服器上AEM Forms的HTTPS URL。若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數，在JEE伺服器上重新啟動AEM Forms。
   * **啟用雙向SSL**:啟用「啟用2向SSL」選項。
   * **KeyStore檔案URL**:指定密鑰庫檔案的URL。
   * **TrustStore FIle URL**:指定truststore檔案的URL。
   * **KeyStore密碼**:指定密鑰庫檔案的密碼。
   * **TrustStorePassword**:指定truststore檔案的密碼。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。

   按一下「**儲存**」。已啟AEM用搜尋檔案安全性保護的PDF和Microsoft Office檔案

## 為受原則保護的範例PDF或Microsoft Office檔案建立索引{#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理員身份登錄AEM Assets。
1. 在Digital Asset Manager中建AEM立檔案夾，並將受原則保護的PDF或Microsoft Office檔案上傳至新建立的檔案夾。 現在，請使用搜尋來搜尋受原則保護檔案的AEM內容。 它必須返回包含搜索文本的文檔。

