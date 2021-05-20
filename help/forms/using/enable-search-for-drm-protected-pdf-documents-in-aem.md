---
title: 啟用AEM以搜索受文檔安全保護的PDF文檔
seo-title: 啟用AEM以搜索受文檔安全保護的PDF文檔
description: '了解如何啟用原生AEM搜尋，對受DRM保護的PDF檔案執行全文搜尋。  '
seo-description: '了解如何啟用原生AEM搜尋，對受DRM保護的PDF檔案執行全文搜尋。  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: 文件安全性
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# 啟用AEM以搜索受文檔安全保護的PDF文檔{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜尋能夠搜尋及找到AEM資產，並對各種常用的檔案格式（例如純文字檔案、Microsoft Office檔案和PDF檔案）執行文字搜尋。 您也可以延伸原生搜尋功能，對受AEM檔案安全性保護的[PDF檔案執行全文搜尋](../../forms/using/admin-help/document-security.md)。 要啟用AEM對此類文檔執行全文搜索，請執行以下步驟：

1. 建立安全連接
1. 為受策略保護的PDF文檔的示例編製索引

## 必備條件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 在AEM Forms伺服器上安裝[AEM Forms Document Security Indexer套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   * 確認JEE伺服器上的AEM Forms正常運作，且JEE伺服器上對應的AEM Forms上已安裝檔案安全性。 JEE伺服器上的AEM表單必須為受保護的檔案建立索引。

* 如果您只在JEE伺服器上使用AEM Forms，則已安裝索引器套件。
* 請確定所有套件組合皆已啟動並執行。 如果所有套件組合都未啟用，請等待所有套件組合都啟動並運行。

   * 對於OSGi上的AEM Forms，套件組合列在https://&#39;[server]:[port]&#39;/system/console/bundles。
   * 對於JEE上的AEM Forms，套件組合列在https://&#39;[server]:[port]`/[context-path]/system/console/bundles。 例如https://localhost:8080/lc/system/console/bundles。

* 將&#x200B;*sun.util.calendar*&#x200B;包添加到允許清單。 要將包添加到允許清單，請執行以下步驟：

   1. 開啟AEM Web Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
   1. 找到並開啟&#x200B;**反序列化防火牆配置**。

   1. 將sun.util.calendar包添加到「允許列出的類或包前置詞」欄位，然後按一下「**保存**」。

### 在AEM Forms JEE和OSGi堆疊{#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}之間建立安全連線

您可以使用下列其中一種方法來建立安全連線：

* 在JEE上使用AEM Forms管理憑證設定AdobeLiveCycle用戶端SDK套件
* 使用相互驗證來設定AdobeLiveCycle用戶端SDK套件組合

#### 在JEE管理員憑證{#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}上使用AEM Forms設定AdobeLiveCycle用戶端SDK套件組合

1. 開啟AEM Web Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 找到並開啟&#x200B;**AdobeLiveCycle用戶端SDK套件組合**。 指定下列欄位的值：

   * **伺服器URL:** 指定JEE伺服器上AEM Forms的HTTPS URL。若要透過https啟用通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰存放區檔案上AEM Forms的路徑>參數重新啟動伺服器。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單中。
   * **使用者名稱：** 指定JEE帳戶上用來起始來自AEM伺服器呼叫的AEM Forms的使用者名稱。指定的帳戶必須擁有在JEE伺服器上的AEM Forms上啟動檔案服務的權限。
   * **密碼**:在使用者名稱欄位中提及的JEE帳戶上指定AEM Forms的密碼。

   按一下「**儲存**」。AEM可用來搜尋受檔案安全性保護的PDF檔案。

#### 使用相互驗證{#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}設定AdobeLiveCycle用戶端SDK套件組合

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參閱[CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEM Web Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 找到並開啟&#x200B;**AdobeLiveCycle用戶端SDK**&#x200B;套件組合。 指定下列屬性的值：

   * **伺服器URL**:指定JEE伺服器上AEM Forms的HTTPS URL。若要透過https啟用通訊，請使用-Djavax.net.ssl.trustStore=&lt;JEE金鑰存放區檔案上AEM Forms的路徑>參數重新啟動AEM伺服器。
   * **啟用雙向SSL**:啟用「啟用2向SSL」選項。
   * **KeyStore檔案URL**:指定金鑰存放區檔案的URL。
   * **TrustStore FIle URL**:指定信任儲存檔案的URL。
   * **KeyStore密碼**:指定金鑰存放區檔案的密碼。
   * **TrustStorePassword**:指定信任儲存檔案的密碼。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單中。

   按一下「**儲存**」。AEM可用於搜尋受檔案安全保護的PDF檔案

### 為受策略保護的PDF文檔{#index-a-sample-policy-protected-pdf-document}的示例編製索引

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset Manager中建立資料夾，並將受原則保護的PDF檔案上傳至新建立的資料夾。

   現在，您可以使用AEM搜索來搜索受策略保護的文檔。
