---
title: 啟用AEM以搜尋受Document Security保護的PDF檔案
description: 瞭解如何啟用原生AEM搜尋，以在受DRM保護的PDF檔案上執行全文搜尋。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 啟用AEM以搜尋受Document Security保護的PDF檔案{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜尋可搜尋和找到AEM資產，並對各種常用的檔案格式(例如純文字檔、Microsoft Office檔案和PDF檔案)執行文字搜尋。 您也可以擴充原生搜尋，以對[受AEM Document Security保護的PDF檔案](../../forms/using/admin-help/document-security.md)執行全文搜尋。 若要讓AEM對這類檔案執行全文搜尋，請執行下列步驟：

1. 建立安全連線
1. 為受原則保護的PDF範例檔案建立索引

## 先決條件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms：

   * 在AEM Forms伺服器上安裝[AEM Forms Document Security Indexer套件](https://helpx.adobe.com/tw/aem-forms/kb/aem-forms-releases.html)。

   * 確保JEE伺服器上的AEM Forms啟動並執行，且JEE伺服器上的對應AEM Forms已安裝Document Security。 必須有JEE伺服器上的AEM表單，才能為受保護的檔案建立索引。

* 如果您在JEE伺服器上只使用AEM Forms，表示已安裝索引器套件。
* 確認所有套件組合皆已啟動且執行中。 如果所有套件組合並非作用中，請等待直到所有套件組合都啟動並執行。

   * 若為OSGi上的AEM Forms，套件組合會列在https://&#39;[server]：[port]&#39;/system/console/bundles。
   * 若為JEE上的AEM Forms，套件組合會列在https://&#39;[server]：[port]&#39;/[context-path]/system/console/bundles。 例如， https://localhost:8080/lc/system/console/bundles。

* 將&#x200B;*sun.util.calendar*&#x200B;套件新增至允許清單。 若要將套件新增至允許清單，請執行下列步驟：

   1. 開啟AEM Web Console。 URL是https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr。
   1. 找到並開啟&#x200B;**還原序列化防火牆設定**。

   1. 將sun.util.calendar套件新增至[允許清單的類別]或[套件首碼]欄位，然後按一下[儲存]。**&#x200B;**

### 在AEM Forms JEE和OSGi棧疊之間建立安全連線 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用下列其中一種方法來建立安全連線：

* 使用AEM Forms在JEE管理員憑證上設定AdobeLiveCycle使用者端SDK套件組合
* 使用相互驗證設定AdobeLiveCycle使用者端SDK套裝

#### 使用AEM Forms在JEE管理員憑證上設定AdobeLiveCycle使用者端SDK套件組合 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM Web Console。 URL是https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr。
1. 找到並開啟&#x200B;**AdobeLiveCycle使用者端SDK套件**。 指定下列欄位的值：

   * **伺服器URL：**&#x200B;指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>引數重新啟動伺服器。
   * **服務名稱**：將RightsManagementService新增至指定的服務清單。
   * **使用者名稱：**&#x200B;指定JEE帳戶上AEM Forms的使用者名稱，以用於起始來自AEM伺服器的呼叫。 指定的帳戶必須具有在JEE伺服器上的AEM Forms上啟動檔案服務的許可權。
   * **密碼**：指定使用者名稱欄位中提及的AEM Forms on JEE帳戶密碼。

   按一下「**儲存**」。AEM已啟用來搜尋受Document Security保護的PDF檔案。

#### 使用相互驗證設定AdobeLiveCycle使用者端SDK套裝 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 啟用JEE上AEM Forms的相互驗證。 如需詳細資訊，請參閱[CAC和相互驗證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEM Web Console。 URL是https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr。
1. 找到並開啟&#x200B;**AdobeLiveCycle使用者端SDK**&#x200B;套件。 指定下列屬性的值：

   * **伺服器URL**：指定JEE伺服器上AEM Forms的HTTPS URL。 若要啟用透過https的通訊，請使用-Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>引數重新啟動AEM伺服器。
   * **啟用雙向SSL**：啟用「啟用雙向SSL」選項。
   * **KeyStore檔案URL**：指定Keystore檔案的URL。
   * **TrustStore檔案URL**：指定truststore檔案的URL。
   * **KeyStore密碼**：指定金鑰存放區檔案的密碼。
   * **TrustStorePassword**：指定truststore檔案的密碼。
   * **服務名稱**：將RightsManagementService新增至指定的服務清單。

   按一下「**儲存**」。AEM已啟用以搜尋受Document Security保護的PDF檔案

### 為受原則保護的PDF範例檔案建立索引 {#index-a-sample-policy-protected-pdf-document}

1. 以管理員身分登入AEM Assets。
1. 在AEM Digital Asset Manager中建立資料夾，並將受原則保護的PDF檔案上傳到新建立的資料夾。

   現在，您可以使用AEM搜尋來搜尋受原則保護的檔案。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。
