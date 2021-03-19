---
title: 啟用搜AEM尋檔案安全性保護的PDF檔案
seo-title: 啟用搜AEM尋檔案安全性保護的PDF檔案
description: '瞭解如何啟用原AEM生搜尋，對受DRM保護的PDF檔案執行全文搜尋。  '
seo-description: '瞭解如何啟用原AEM生搜尋，對受DRM保護的PDF檔案執行全文搜尋。  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---


# 啟用AEM搜尋檔案安全性保護的PDF檔案{#enable-aem-to-search-document-security-protected-pdf-documents}

搜AEM尋功能可搜尋和尋AEM找資產，並對各種常用的檔案格式（例如純文字檔案、Microsoft Office檔案和PDF檔案）執行文字搜尋。 您也可以延伸原生搜尋功能，對使用AEMDocument Security](../../forms/using/admin-help/document-security.md)保護的[PDF檔案執行全文搜尋。 要啟AEM用對此類文檔執行全文搜索，請執行以下步驟：

1. 建立安全連接
1. 為受原則保護的範例PDF檔案建立索引

## 必備條件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 在AEM Forms伺服器上安裝[AEM FormsDocument Security Indexer軟體包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   * 確保JEE伺服器上的AEM Forms已啟動並正在運行，並且JEE伺服器上相應的AEM Forms安裝了文檔安全。 JEEAEM伺服器上的表單是為受保護文檔編製索引所必需的。

* 如果您只在JEE伺服器上使用AEM Forms，則已安裝索引器包。
* 確保所有捆綁包均已啟動並運行。 如果所有捆綁包都未激活，請等待所有捆綁包都啟動並運行。

   * 對於OSGi上的AEM Forms，這些捆綁列在https://&#39;[server]:[port]&#39;/system/console/bundles中。
   * 對於JEE上的AEM Forms，捆綁包列在https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles中。 例如https://localhost:8080/lc/system/console/bundles。

* 將&#x200B;*sun.util.calendar*&#x200B;軟體包添加到allowlist。 要將包添加到allowlist，請執行以下步驟：

   1. 開啟AEMWeb Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
   1. 找到並開啟&#x200B;**還原序列化防火牆配置**。

   1. 將sun.util.calendar包添加到Allowlisted classes或package prefixes欄位中，然後按一下&#x200B;**Save**。

### 在AEM FormsJEE和OSGi堆棧之間建立安全連接{#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用下列方法之一來建立安全連接：

* 在JEE管理員認證上使用AEM Forms配置AdobeLiveCycle用戶端SDK套件
* 使用相互驗證配置AdobeLiveCycle客戶端SDK包

#### 在JEE管理員憑證{#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}上使用AEM Forms設定AdobeLiveCycle用戶端SDK套件

1. 開啟AEMWeb Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 找到並開啟&#x200B;**AdobeLiveCycle客戶端SDK包**。 指定下列欄位的值：

   * **伺服器URL：指** 定JEE伺服器上AEM Forms的HTTPS URL。若要啟用透過https進行通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數重新啟動伺服器。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。
   * **使用者名** 稱：指定JEE帳戶上用來從伺服器啟動呼叫的AEM FormsAEM使用者名稱。指定的帳戶必須具有在JEE伺服器上的AEM Forms啟動文檔服務的權限。
   * **密碼**:在「用戶名」欄位中提及的JEE帳戶上指定AEM Forms的密碼。

   按一下「**儲存**」。可AEM搜尋檔案安全性保護的PDF檔案。

#### 使用相互驗證{#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}配置AdobeLiveCycle客戶端SDK包

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參閱[CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEMWeb Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 找到並開啟&#x200B;**AdobeLiveCycle用戶端SDK**&#x200B;套件。 指定下列屬性的值：

   * **伺服器URL**:在JEE伺服器上指定AEM Forms的HTTPS URL。若要啟用透過https進行通訊，請使AEM用-Djavax.net.ssl.trustStore=&lt;JEE金鑰庫檔案上的AEM Forms路徑>參數重新啟動伺服器。
   * **啟用雙向SSL**:啟用「啟用2向SSL」選項。
   * **KeyStore檔案URL**:指定密鑰庫檔案的URL。
   * **TrustStore FIle URL**:指定truststore檔案的URL。
   * **KeyStore密碼**:指定密鑰庫檔案的密碼。
   * **TrustStorePassword**:指定truststore檔案的密碼。
   * **服務名稱**:將RightsManagementService新增至指定服務的清單。

   按一下「**儲存**」。已啟AEM用搜尋檔案安全性保護的PDF檔案

### 為受原則保護的範例PDF檔案建立索引{#index-a-sample-policy-protected-pdf-document}

1. 以管理員身份登錄AEM Assets。
1. 在Digital Asset Manager中建AEM立檔案夾，並將受原則保護的PDF檔案上傳至新建立的檔案夾。

   現在，您可以使用搜尋來搜尋受原則保護的AEM檔案。

