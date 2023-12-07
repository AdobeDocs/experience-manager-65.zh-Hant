---
title: 啟用AEM以搜尋受Document Security保護的PDF和Microsoft Office檔案
description: 瞭解如何啟用原生AEM搜尋，以在受DRM保護的PDF檔案上執行全文搜尋。
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 啟用AEM以搜尋受Document Security保護的PDF和Microsoft Office檔案{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供使用者介面，可搜尋和找出儲存在AEM中的各種資產。 原生搜尋可搜尋和找到AEM資產，並對各種常用的檔案格式(例如純文字檔、Microsoft Office檔案和PDF檔案)執行文字搜尋。 您也可以擴充及啟用原生搜尋，以對DRM保護的PDF和Microsoft Office檔案執行全文搜尋。

執行以下步驟以允許AEM搜尋受Document Security保護的PDF和Microsoft Office檔案：

## 開始之前 {#before-you-start}

* 安裝及設定AEM Forms Document Security。
* 將套裝程式sun.util.calendar新增至 **還原序列化防火牆設定。** 此設定列於 `https://'[server]:[port]'/system/console/configMgr`.
* 確認所有AEM套件組合皆已啟動且執行中。 這些套件組合列於 `https://'[server]:[port]'/system/console/bundles`. 如果所有套件組合並非作用中，請稍候片刻，然後在片刻後檢查套件組合的狀態。

## 在AEM Forms工作流程中建立安全連線(JEE上的AEM Forms) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全連線可讓JEE上的AEM Forms與相同伺服器上執行的OSGi服務之間順暢地傳輸資訊。 使用下列其中一種方法來建立安全連線：

* 使用AEM Forms在JEE管理員憑證上設定AEM Forms使用者端SDK套件組合
* 使用相互驗證設定AEM Forms使用者端SDK套件組合

### 使用AEM Forms在JEE管理員憑證上設定AEM Forms使用者端SDK套件組合 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM設定管理員，並以管理員身分登入。 預設URL為https://&lt;servername>：&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms使用者端SDK套件組合。 指定下列屬性的值：

   * **伺服器URL：** 指定JEE伺服器上AEM Forms的HTTP URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=重新啟動JEE伺服器上的AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 引數。
   * **服務名稱**：將RightsManagementService新增至指定服務的清單。
   * **使用者名稱：** 指定JEE伺服器上AEM Forms的使用者名稱，以用來起始從JEE伺服器AEM Forms的呼叫。 指定的帳戶必須有權在JEE伺服器上的AEM Forms上叫用檔案服務。
   * **密碼**：指定使用者名稱欄位中提及的JEE帳戶AEM Forms密碼。

   按一下 **儲存**. AEM已啟用來搜尋受Document Security保護的PDF和Microsoft Office檔案。

### 使用相互驗證設定AEM Forms使用者端SDK套件組合 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參閱 [CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. 開啟AEM設定管理員，並以管理員身分登入。 預設URL為https://&lt;servername>：&lt;port>/lc/system/console/configMgr。
1. 搜尋並開啟AEM Forms使用者端SDK套件組合。 指定下列屬性的值：

   * **伺服器URL：** 指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=重新啟動JEE伺服器上的AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 引數。
   * **啟用雙向SSL**：啟用「啟用雙向SSL」選項。
   * **KeyStore檔案URL**：指定Keystore檔案的URL。
   * **TrustStore檔案網址**：指定信任庫檔案的URL。
   * **KeyStore密碼**：指定Keystore檔案的密碼。
   * **TrustStPassword**：指定Truststore檔案的密碼。
   * **服務名稱**：將RightsManagementService新增至指定服務的清單。

   按一下 **儲存**. AEM已啟用以搜尋受Document Security保護的PDF和Microsoft Office檔案

## 為受原則保護的PDF範例或Microsoft Office檔案建立索引 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset Manager中建立資料夾，並將受原則保護的PDF或Microsoft Office檔案上傳到新建立的資料夾。 現在，使用AEM搜尋來搜尋受原則保護檔案的內容。 它必須傳回包含搜尋文字的檔案。
