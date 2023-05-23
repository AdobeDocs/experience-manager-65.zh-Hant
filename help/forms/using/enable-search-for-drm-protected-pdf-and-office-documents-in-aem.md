---
title: 啟用AEM搜索文檔安全保護PDF和MicrosoftOffice文檔
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: 瞭解如何啟用本AEM機搜索以對受DRM保護的PDF文檔執行全文搜索。
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

# 啟用AEM搜索文檔安全保護PDF和MicrosoftOffice文檔{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供用戶介面來搜索和查找儲存在中的各種AEM資產 本機搜索能夠搜索和定AEM位資產，並對各種常用文檔格式執行文本搜索，如純文字檔案檔案、Microsoft辦公室文檔和PDF文檔。 您還可以擴展並啟用本機搜索，以對受DRM保護的PDF和MicrosoftOffice文檔執行全文搜索。

執行以下步驟以AEM便搜索文檔安全保護PDF和Microsoft辦公室文檔：

## 開始之前 {#before-you-start}

* 安裝和配置AEM Forms文檔安全性。
* 將包sun.util.calendar添加到 **反序列化防火牆配置。** 配置列於 `https://'[server]:[port]'/system/console/configMgr`。
* 確保所有AEM捆綁包都已啟動並運行。 捆綁包列於 `https://'[server]:[port]'/system/console/bundles`。 如果所有捆綁包都未處於活動狀態，請等待幾分鐘後檢查捆綁包的狀態。

## 在AEM Forms工作流內建立安全連接(AEM Forms在JEE上) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全連接使JEE上的AEM Forms和在同一伺服器上運行的OSGi服務之間能夠無縫地流動資訊。 使用以下方法之一建立安全連接：

* 在JEE管理憑據上配置AEM Forms客戶端SDK包和AEM Forms
* 使用相互驗證配置AEM Forms客戶端SDK包

### 在JEE管理憑據上配置AEM Forms客戶端SDK包和AEM Forms {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 開啟AEM配置管理器並以管理員身份登錄。 預設URL為https://&lt;servername>:&lt;port>/lc/system/console/configMgr。
1. 搜索並開啟AEM Forms客戶端SDK包。 為以下屬性指定值：

   * **伺服器URL:** 在JEE伺服器上指定AEM Forms的HTTP URL。 要啟用通過https的通信，請使用-Djavax.net.ssl.trustStore=重新啟動JEE伺服器上的AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 的下界。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單。
   * **用戶名：** 在JEE帳戶上指定用於在JEE伺服器上啟動來自AEM Forms的呼叫的AEM Forms的用戶名。 指定的帳戶必須具有在JEE伺服器上調用AEM Forms上的文檔服務的權限。
   * **密碼**:在「用戶名」欄位中提及的JEE帳戶上指定AEM Forms的密碼。

   按一下「**儲存**」。啟AEM用搜索文檔安全保護PDF和Microsoft辦公室文檔。

### 使用相互驗證配置AEM Forms客戶端SDK包 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 在JEE上為AEM Forms啟用相互身份驗證。 有關詳細資訊，請參見 [CAC和互認證](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 開啟AEM配置管理器並以管理員身份登錄。 預設URL為https://&lt;servername>:&lt;port>/lc/system/console/configMgr。
1. 搜索並開啟AEM Forms客戶端SDK包。 為以下屬性指定值：

   * **伺服器URL:** 在JEE伺服器上指定AEM Forms的HTTPS URL。 要啟用通過https的通信，請使用-Djavax.net.ssl.trustStore=重新啟動JEE伺服器上的AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 的下界。
   * **啟用雙向SSL**:啟用「啟用雙向SSL」選項。
   * **密鑰儲存檔案URL**:指定密鑰庫檔案的URL。
   * **TrustStore檔案URL**:指定信任儲存檔案的URL。
   * **密鑰儲存密碼**:指定密鑰庫檔案的密碼。
   * **信任儲存密碼**:指定信任儲存檔案的密碼。
   * **服務名稱**:將RightsManagementService添加到指定服務的清單。

   按一下「**儲存**」。已AEM啟用搜索文檔安全保護PDF和MicrosoftOffice文檔

## 索引受策略保護的PDF或Microsoft辦公室文檔的示例 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理員身份登錄到AEM Assets。
1. 在AEMDigital Asset Manager中建立資料夾，並將受策略保護的PDF或MicrosoftOffice文檔上載到新建立的資料夾。 現在，使用搜索搜索策略保護文檔的AEM內容。 它必須返回包含搜索文本的文檔。
