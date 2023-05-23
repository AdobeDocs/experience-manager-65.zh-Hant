---
title: 啟用搜AEM索文檔安全保護的PDF文檔
seo-title: Enable AEM to search document security protected PDF documents
description: 瞭解如何啟用本AEM機搜索以對受DRM保護的PDF文檔執行全文搜索。
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 啟用搜AEM索文檔安全保護的PDF文檔{#enable-aem-to-search-document-security-protected-pdf-documents}

搜AEM索可搜索和定AEM位資產，並對各種常用文檔格式執行文本搜索，如純文字檔案檔案、Microsoft辦公室文檔和PDF文檔。 您還可以擴展本機搜索，以對 [PDF文檔受文AEM檔安全保護](../../forms/using/admin-help/document-security.md)。 要啟用AEM對此類文檔執行全文搜索，請執行以下步驟：

1. 建立安全連接
1. 索引策略保護的示例PDF文檔

## 必備條件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 安裝 [AEM Forms文檔安全索引器包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 在AEM Forms伺服器上。

   * 確保JEE伺服器上的AEM Forms已啟動並正在運行，並且JEE伺服器上的相應AEM Forms上安裝了文檔安全。 JEE服AEM務器上的表單是為受保護文檔編製索引所必需的。

* 如果在JEE伺服器上僅使用AEM Forms，則已安裝索引器包。
* 確保所有捆綁包都已啟動並運行。 如果所有捆綁包都未處於活動狀態，請等待所有捆綁包都啟動並運行。

   * 對於OSGi上的AEM Forms，這些捆綁包列在https://&#39;[伺服器]:[埠]「/system/console/bundles。
   * 對於JEE上的AEM Forms，這些捆綁包列在https://&#39;[伺服器]:[埠]&#39;/[上下文路徑]/system/console/bundles。 例如https://localhost:8080/lc/system/console/bundles。

* 添加 *sun.util.calendar* 檔案包。 要將包添加到允許清單，請執行以下步驟：

   1. 開啟AEMWeb控制台。 URL為https://&#39;[伺服器]:[埠]「/system/console/configMgr。
   1. 查找並開啟 **反序列化防火牆配置**。

   1. 將sun.util.calendar包添加到「允許列出的類」或包前置詞欄位中，然後按一下 **保存**。

### 在AEM FormsJEE和OSGi堆棧之間建立安全連接 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

可以使用以下方法之一建立安全連接：

* 在JEE管理憑據上配置AdobeLiveCycle客戶端SDK包和AEM Forms
* 使用相互身份驗證配置AdobeLiveCycle客戶端SDK包

#### 在JEE管理憑據上配置AdobeLiveCycle客戶端SDK包和AEM Forms {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEMWeb控制台。 URL為https://&#39;[伺服器]:[埠]「/system/console/configMgr。
1. 查找並開啟 **AdobeLiveCycle客戶端SDK包**。 指定以下欄位的值：

   * **伺服器URL:** 在JEE伺服器上指定AEM Forms的HTTPS URL。 要啟用通過https的通信，請使用-Djavax.net.ssl.trustStore=重新啟動伺服器&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 的下界。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單。
   * **用戶名：** 在JEE帳戶上指定用於從伺服器啟動呼叫的AEM Forms的AEM用戶名。 指定的帳戶必須具有在JEE伺服器上的AEM Forms啟動文檔服務的權限。
   * **密碼**:在「用戶名」欄位中提及的JEE帳戶上指定AEM Forms的密碼。

   按一下「**儲存**」。啟AEM用以搜索文檔安全保護的PDF文檔。

#### 使用相互身份驗證配置AdobeLiveCycle客戶端SDK包 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 在JEE上為AEM Forms啟用相互身份驗證。 有關詳細資訊，請參見 [CAC和互認證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEMWeb控制台。 URL為https://&#39;[伺服器]:[埠]「/system/console/configMgr。
1. 查找並開啟 **AdobeLiveCycle客戶端SDK** 捆綁。 為以下屬性指定值：

   * **伺服器URL**:在JEE伺服器上指定AEM Forms的HTTPS URL。 要啟用通過https的通信，請使AEM用-Djavax.net.ssl.trustStore=重新啟動伺服器&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 的下界。
   * **啟用雙向SSL**:啟用「啟用雙向SSL」選項。
   * **密鑰儲存檔案URL**:指定密鑰庫檔案的URL。
   * **TrustStore檔案URL**:指定信任儲存檔案的URL。
   * **密鑰儲存密碼**:指定密鑰庫檔案的密碼。
   * **信任儲存密碼**:指定信任儲存檔案的密碼。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單。

   按一下「**儲存**」。啟AEM用搜索文檔安全保護的PDF文檔

### 索引策略保護的示例PDF文檔 {#index-a-sample-policy-protected-pdf-document}

1. 以管理員身份登錄到AEM Assets。
1. 在Digital Asset Manager中創AEM建資料夾，並將受策略保護的PDF文檔上載到新建立的資料夾。

   現在，您可以使用搜索來搜索受策略保護的AEM文檔。
