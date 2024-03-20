---
title: 使用認證
description: 使用信任管理員API和Java API將憑證匯入AEM Forms。 此外，瞭解如何使用信任管理員API和Java API來刪除認證。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---

# 使用認證 {#working-with-credentials}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於認證服務**

認證包含簽署或識別檔案所需的私密金鑰資訊。 憑證是您設定為信任的公開金鑰資訊。 AEM Forms將憑證和認證用於多種用途：

* Acrobat Reader DC擴充功能會使用認證，在PDF檔案中啟用Adobe Reader使用許可權。 (請參閱 [將使用許可權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* 簽章服務會在執行作業(例如數位簽署PDF檔案)時存取憑證和認證。 (請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

您可以使用信任管理員Java API，以程式設計方式與認證服務互動。 您可以執行下列工作：

* [使用信任管理員API匯入認證](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用信任管理員API刪除認證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您也可以使用管理控制檯來匯入和刪除憑證。 (請參閱 [管理說明。](https://www.adobe.com/go/learn_aemforms_admin_63))

## 使用信任管理員API匯入認證 {#importing-credentials-by-using-the-trust-manager-api}

您可以使用信任管理員API，以程式設計方式將認證匯入AEM Forms。 例如，您可以匯入用來簽署PDF檔案的認證。 (請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

匯入認證時，您需指定認證的別名。 別名可用來執行需要認證的Forms作業。 匯入後，可在管理主控台中檢視認證，如下圖所示。 請注意，認證的別名是 *安全*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>您無法使用Web服務將認證匯入AEM Forms。

### 步驟摘要 {#summary-of-steps}

若要將認證匯入AEM Forms，請執行以下步驟：

1. 包含專案檔案。
1. 建立認證服務使用者端。
1. 參考認證。
1. 執行匯入作業。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立認證服務使用者端**

以程式設計方式將認證匯入AEM Forms之前，請先建立認證服務使用者端。 如需詳細資訊，請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**參考認證**

參考您要匯入AEM Forms的認證。 與此區段相關的快速入門會參考檔案系統中的P12檔案。

**執行匯入作業**

參考認證後，請將認證匯入AEM Forms。 如果未成功匯入認證，則會擲回例外狀況。 匯入認證時，您需指定認證的別名。

**另請參閱**

[使用Java API匯入認證](credentials.md#import-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[認證服務API快速啟動](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用信任管理員API刪除認證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API匯入認證 {#import-credentials-using-the-java-api}

使用信任管理員API (Java)將認證匯入AEM Forms：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-truststore-client.jar。

1. 建立認證服務使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `CredentialServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考認證

   * 建立 `java.io.FileInputStream` 物件（使用其建構函式）。 傳遞字串值，指定認證的位置。
   * 建立 `com.adobe.idp.Document` 使用儲存認證的物件 `com.adobe.idp.Document` 建構函式。 傳遞 `java.io.FileInputStream` 包含建構函式認證的物件。

1. 執行匯入作業

   * 建立容納一個元素的字串陣列。 指派值 `truststore.usage.type.sign` 至元素。
   * 叫用 `CredentialServiceClient` 物件的 `importCredential` 方法並傳遞下列值：

      * 字串值，指定認證的別名值。
      * 此 `com.adobe.idp.Document` 儲存認證的執行個體。
      * 字串值，指定與認證相關的密碼。
      * 包含使用值的字串陣列。 例如，您可以指定此值 `truststore.usage.type.sign`. 若要匯入Reader擴充功能認證，請指定 `truststore.usage.type.lcre`.

**另請參閱**

[使用信任管理員API匯入認證](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速入門（SOAP模式）：使用Java API匯入認證](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用信任管理員API刪除認證 {#deleting-credentials-by-using-the-trust-manager-api}

您可以使用信任管理員API，以程式設計方式刪除認證。 刪除認證時，請指定與認證對應的別名。 刪除後，認證就無法用來執行作業。

>[!NOTE]
>
>您無法使用Web服務刪除AEM Forms中的認證。

### 步驟摘要 {#summary_of_steps-1}

若要刪除認證，請執行下列步驟：

1. 包含專案檔案。
1. 建立認證服務使用者端。
1. 執行刪除作業。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立認證服務使用者端**

在您以程式設計方式刪除認證之前，請先建立資料整合服務使用者端。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。 如需詳細資訊，請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**執行刪除作業**

若要刪除認證，請指定與認證對應的別名。 如果指定的別名不存在，則會擲回例外狀況。

**另請參閱**

[使用Java API匯入認證](credentials.md#import-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API匯入認證](credentials.md#import-credentials-using-the-java-api)

### 使用Java API刪除認證 {#deleting-credentials-using-the-java-api}

使用信任管理員API (Java)從AEM Forms刪除認證：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-truststore-client.jar。

1. 建立認證服務使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `CredentialServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 執行刪除作業

   叫用 `CredentialServiceClient` 物件的 `deleteCredential` 方法，並傳遞指定別名值的字串值。

**另請參閱**

[使用信任管理員API刪除認證](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速入門（SOAP模式）：使用Java API刪除認證](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
