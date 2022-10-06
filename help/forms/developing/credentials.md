---
title: 使用憑證
seo-title: Working with Credentials
description: 使用信任管理器API和Java API將憑證匯入AEM Forms。 此外，還可了解如何使用信任管理器API和Java API刪除憑證。
seo-description: Import credentials into AEM Forms using the Trust Manager API and Java API. In addition, learn how to delete credentials using the Trust Manager API and Java API.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# 使用憑證 {#working-with-credentials}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於憑據服務**

憑據包含簽名或標識文檔所需的私鑰資訊。 憑證是您為信任所設定的公開金鑰資訊。 AEM Forms使用憑證和憑證有數種用途：

* Acrobat Reader DC擴充功能會使用憑證，啟用PDF檔案中的Adobe Reader使用權限。 (請參閱 [將使用權應用於PDF文檔](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* 簽名服務在執行諸如數字簽名PDF文檔等操作時訪問證書和憑據。 (請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

您可以使用信任管理器Java API，以程式設計方式與憑證服務互動。 您可以執行下列工作：

* [使用信任管理器API導入憑據](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用信任管理器API刪除憑證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您也可以使用管理控制台來匯入和刪除憑證。 (請參閱 [管理說明。](https://www.adobe.com/go/learn_aemforms_admin_63))

## 使用信任管理器API導入憑據 {#importing-credentials-by-using-the-trust-manager-api}

您可以使用信任管理器API，以程式設計方式將憑證匯入AEM Forms。 例如，您可以導入用於簽署PDF文檔的憑據。 (請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

導入憑據時，需為憑據指定別名。 別名用於執行需要憑據的Forms操作。 匯入後，即可在管理控制台中檢視憑證，如下圖所示。 請注意，憑據的別名為 *安全*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>您無法使用網站服務將憑證匯入AEM Forms。

### 步驟摘要 {#summary-of-steps}

要將憑據導入AEM Forms，請執行以下步驟：

1. 包含專案檔案。
1. 建立憑據服務客戶端。
1. 引用憑據。
1. 執行導入操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立憑據服務客戶端**

在以寫程式方式將憑據導入AEM Forms之前，請先建立憑據服務客戶端。 如需詳細資訊，請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**引用憑據**

參考您要匯入AEM Forms的憑證。 與此部分關聯的快速入門參考位於檔案系統中的P12檔案。

**執行導入操作**

參考憑證後，將憑證匯入AEM Forms。 如果未成功導入憑據，則會引發異常。 導入憑據時，需為憑據指定別名。

**另請參閱**

[使用Java API匯入憑證](credentials.md#import-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[憑據服務API快速入門](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用信任管理器API刪除憑證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API匯入憑證 {#import-credentials-using-the-java-api}

使用信任管理器API(Java)將憑證匯入AEM Forms:

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-truststore-client.jar。

1. 建立憑據服務客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `CredentialServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 引用憑據

   * 建立 `java.io.FileInputStream` 物件，使用其建構子。 傳遞一個字串值，指定憑據的位置。
   * 建立 `com.adobe.idp.Document` 使用 `com.adobe.idp.Document` 建構子。 傳遞 `java.io.FileInputStream` 包含建構子憑據的對象。

1. 執行導入操作

   * 建立包含一個元素的字串陣列。 指派值 `truststore.usage.type.sign` 至元素。
   * 叫用 `CredentialServiceClient` 物件 `importCredential` 方法，並傳遞下列值：

      * 指定憑據的別名值的字串值。
      * 此 `com.adobe.idp.Document` 儲存憑證的例項。
      * 一個字串值，它指定與憑據關聯的密碼。
      * 包含使用值的字串陣列。 例如，您可以指定此值 `truststore.usage.type.sign`. 要導入Reader擴展憑據，請指定 `truststore.usage.type.lcre`.

**另請參閱**

[使用信任管理器API導入憑據](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速入門（SOAP模式）:使用Java API匯入憑證](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用信任管理器API刪除憑證 {#deleting-credentials-by-using-the-trust-manager-api}

您可以使用信任管理器API以程式設計方式刪除憑據。 在刪除憑據時，可以指定與憑據對應的別名。 刪除後，憑據無法用於執行操作。

>[!NOTE]
>
>您無法使用Web服務將憑證刪除至AEM Forms。

### 步驟摘要 {#summary_of_steps-1}

要刪除憑據，請執行以下步驟：

1. 包含專案檔案。
1. 建立憑據服務客戶端。
1. 執行刪除操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立憑據服務客戶端**

在以寫程式方式刪除憑據之前，請先建立資料整合服務客戶端。 建立服務客戶端時，您定義調用服務所需的連接設定。 如需詳細資訊，請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**執行刪除操作**

要刪除憑據，請指定與憑據對應的別名。 如果指定的別名不存在，則會引發異常。

**另請參閱**

[使用Java API匯入憑證](credentials.md#import-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API匯入憑證](credentials.md#import-credentials-using-the-java-api)

### 使用Java API刪除憑證 {#deleting-credentials-using-the-java-api}

使用信任管理器API(Java)從AEM Forms中刪除憑據：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-truststore-client.jar。

1. 建立憑據服務客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `CredentialServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 執行刪除操作

   叫用 `CredentialServiceClient` 物件 `deleteCredential` 方法，並傳遞指定別名值的字串值。

**另請參閱**

[使用信任管理器API刪除憑證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速入門（SOAP模式）:使用Java API刪除憑證](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
