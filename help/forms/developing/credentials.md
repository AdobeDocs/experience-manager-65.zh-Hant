---
title: 使用認證
seo-title: 使用認證
description: 'null'
seo-description: 'null'
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用認證 {#working-with-credentials}

**關於憑證服務**

憑證包含簽署或識別檔案所需的私密金鑰資訊。 憑證是您設定為信任的公開金鑰資訊。 AEM Forms使用憑證和認證以進行數種用途：

* Acrobat Reader DC擴充功能使用憑證，以啟用PDF檔案中的Adobe Reader使用權限。 (請參 [閱套用PDF檔案的使用權](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。)
* 簽名服務在執行數位簽署PDF檔案等作業時，會存取憑證和認證。 (請參 [閱數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

您可以使用Trust Manager Java API，以程式設計方式與憑證服務互動。 您可以執行下列工作：

* [使用信任管理器API匯入憑證](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用信任管理器API刪除憑證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您也可以使用管理控制台來匯入和刪除憑證。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63))。

## 使用信任管理器API匯入憑證 {#importing-credentials-by-using-the-trust-manager-api}

您可以使用Trust Manager API，以程式設計方式將憑證匯入AEM Forms。 例如，您可以匯入用於簽署PDF檔案的憑證。 (請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

在導入憑據時，可以指定憑據的別名。 別名用於執行需要憑據的Forms操作。 在匯入後，憑證就可以在管理控制台中檢視，如下圖所示。 請注意，憑證的別名是安全 *的*。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>您無法使用web services將憑證匯入AEM Forms。

### 步驟摘要 {#summary-of-steps}

若要將憑證匯入AEM Forms，請執行下列步驟：

1. 包含專案檔案。
1. 建立憑證服務客戶端。
1. 參考憑證。
1. 執行導入操作。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立憑證服務客戶端**

在以程式設計方式將憑證匯入AEM Forms之前，請先建立憑證服務用戶端。 有關資訊，請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考憑證**

參考您要匯入至AEM Forms的憑證。 與本節關聯的快速入門參考了位於檔案系統中的P12檔案。

**執行導入操作**

參考憑證後，請將憑證匯入AEM Forms。 如果憑證未成功匯入，則會擲回例外。 在導入憑據時，可以指定憑據的別名。

**另請參閱**

[使用Java API匯入認證](credentials.md#import-credentials-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[憑證服務API快速入門](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用信任管理器API刪除憑證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API匯入認證 {#import-credentials-using-the-java-api}

使用Trust Manager API(Java)將憑證匯入AEM Forms:

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-truststore-client.jar。

1. 建立憑證服務客戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `CredentialServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考憑證

   * 使用其 `java.io.FileInputStream` 建構函式建立物件。 傳遞指定憑證位置的字串值。
   * 使用建 `com.adobe.idp.Document` 構函式建立儲存憑證的物 `com.adobe.idp.Document` 件。 將包含 `java.io.FileInputStream` 憑證的物件傳遞至建構函式。

1. 執行導入操作

   * 建立包含一個元素的字串陣列。 將值指 `truststore.usage.type.sign` 派給元素。
   * 叫用物 `CredentialServiceClient` 件的方 `importCredential` 法並傳遞下列值：

      * 指定憑據別名值的字串值。
      * 存 `com.adobe.idp.Document` 儲憑據的實例。
      * 一個字串值，它指定與憑據關聯的口令。
      * 包含使用值的字串陣列。 例如，您可以指定此值 `truststore.usage.type.sign`。 若要匯入Reader Extension憑證，請指定 `truststore.usage.type.lcre`。

**另請參閱**

[使用信任管理器API匯入憑證](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速入門（SOAP模式）:使用Java API匯入認證](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用信任管理器API刪除憑證 {#deleting-credentials-by-using-the-trust-manager-api}

您可以使用信任管理器API以程式設計方式刪除憑證。 在刪除憑據時，可以指定與憑據對應的別名。 刪除後，將不能使用憑據來執行操作。

>[!NOTE]
>
>您無法使用web services將憑證刪除至AEM Forms。

### 步驟摘要 {#summary_of_steps-1}

要刪除憑據，請執行以下步驟：

1. 包含專案檔案。
1. 建立憑證服務客戶端。
1. 執行刪除操作。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立憑證服務客戶端**

在以程式設計方式刪除憑證之前，請先建立Data Integration服務用戶端。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**執行刪除操作**

要刪除憑據，請指定與憑據對應的別名。 如果指定不存在的別名，則會拋出異常。

**另請參閱**

[使用Java API匯入認證](credentials.md#import-credentials-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API匯入認證](credentials.md#import-credentials-using-the-java-api)

### 使用Java API刪除認證 {#deleting-credentials-using-the-java-api}

使用信任管理員API(Java)從AEM Forms刪除憑證：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-truststore-client.jar。

1. 建立憑證服務客戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `CredentialServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 執行刪除操作

   叫用物 `CredentialServiceClient` 件的方 `deleteCredential` 法並傳遞指定別名值的字串值。

**另請參閱**

[使用信任管理器API刪除憑證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速入門（SOAP模式）:使用Java API刪除認證](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
