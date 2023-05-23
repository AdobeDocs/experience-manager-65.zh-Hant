---
title: 使用憑據
seo-title: Working with Credentials
description: 使用Trust Manager API和Java API將憑據導入AEM Forms。 此外，學習如何使用Trust Manager API和Java API刪除憑據。
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

# 使用憑據 {#working-with-credentials}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於憑據服務**

憑據包含簽名或標識文檔所需的私鑰資訊。 證書是您為信任配置的公鑰資訊。 AEM Forms使用證書和證書用於以下目的：

* Acrobat Reader DC擴展使用憑據在PDF文檔中啟用Adobe Reader使用權。 (請參閱 [將使用權限應用於PDF文檔](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。)
* 簽名服務在執行諸如數字簽名PDF文檔等操作時訪問證書和憑據。 (請參閱 [數字簽名PDF文檔](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

可以使用Trust Manager Java API以寫程式方式與憑據服務交互。 您可以執行以下任務：

* [使用Trust Manager API導入憑據](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用Trust Manager API刪除憑據](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您還可以使用管理控制台導入和刪除證書。 (請參閱 [管理幫助。](https://www.adobe.com/go/learn_aemforms_admin_63))

## 使用Trust Manager API導入憑據 {#importing-credentials-by-using-the-trust-manager-api}

可以使用信任管理器API以寫程式方式將憑據導入AEM Forms。 例如，可以導入用於簽名PDF文檔的憑據。 (請參閱 [數字簽名PDF文檔](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

導入憑據時，請為憑據指定別名。 別名用於執行需要憑據的Forms操作。 導入後，可以在管理控制台中查看憑據，如下圖所示。 請注意，憑據的別名 *安全*。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>無法使用Web服務將憑據導入AEM Forms。

### 步驟摘要 {#summary-of-steps}

要將憑據導入AEM Forms，請執行以下步驟：

1. 包括項目檔案。
1. 建立憑據服務客戶端。
1. 引用憑據。
1. 執行導入操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立憑據服務客戶端**

在以寫程式方式將憑據導入AEM Forms之前，請建立憑據服務客戶端。 有關資訊，請參見 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用憑據**

引用要導入到AEM Forms的憑據。 與此部分關聯的快速啟動引用了位於檔案系統中的P12檔案。

**執行導入操作**

引用憑據後，將憑據導入AEM Forms。 如果憑據未成功導入，則會引發異常。 導入憑據時，請為憑據指定別名。

**另請參閱**

[使用Java API導入憑據](credentials.md#import-credentials-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[憑據服務API快速啟動](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用Trust Manager API刪除憑據](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API導入憑據 {#import-credentials-using-the-java-api}

使用信任管理器API(Java)將憑據導入AEM Forms:

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-truststore-client.jar。

1. 建立憑據服務客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `CredentialServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用憑據

   * 建立 `java.io.FileInputStream` 對象。 傳遞指定憑據位置的字串值。
   * 建立 `com.adobe.idp.Document` 使用 `com.adobe.idp.Document` 建構子。 通過 `java.io.FileInputStream` 包含建構子的憑據的對象。

1. 執行導入操作

   * 建立包含一個元素的字串陣列。 分配值 `truststore.usage.type.sign` 到元素。
   * 調用 `CredentialServiceClient` 對象 `importCredential` 方法並傳遞以下值：

      * 一個字串值，它指定憑據的別名值。
      * 的 `com.adobe.idp.Document` 儲存憑據的實例。
      * 一個字串值，它指定與憑據關聯的密碼。
      * 包含使用值的字串陣列。 例如，可以指定此值 `truststore.usage.type.sign`。 要導入Reader擴展憑據，請指定 `truststore.usage.type.lcre`。

**另請參閱**

[使用Trust Manager API導入憑據](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速啟動（SOAP模式）:使用Java API導入憑據](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Trust Manager API刪除憑據 {#deleting-credentials-by-using-the-trust-manager-api}

可以使用Trust Manager API以寫程式方式刪除憑據。 刪除憑據時，指定與憑據對應的別名。 刪除後，無法使用憑據執行操作。

>[!NOTE]
>
>無法使用Web服務將憑據刪除到AEM Forms。

### 步驟摘要 {#summary_of_steps-1}

要刪除憑據，請執行以下步驟：

1. 包括項目檔案。
1. 建立憑據服務客戶端。
1. 執行刪除操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立憑據服務客戶端**

在以寫程式方式刪除憑據之前，請建立Data Integration服務客戶端。 建立服務客戶端時，定義調用服務所需的連接設定。 有關資訊，請參見 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**執行刪除操作**

要刪除憑據，請指定與憑據對應的別名。 如果指定的別名不存在，則會引發異常。

**另請參閱**

[使用Java API導入憑據](credentials.md#import-credentials-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API導入憑據](credentials.md#import-credentials-using-the-java-api)

### 使用Java API刪除憑據 {#deleting-credentials-using-the-java-api}

使用信任管理器API(Java)從AEM Forms刪除憑據：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-truststore-client.jar。

1. 建立憑據服務客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `CredentialServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 執行刪除操作

   調用 `CredentialServiceClient` 對象 `deleteCredential` 方法並傳遞一個指定別名值的字串值。

**另請參閱**

[使用Trust Manager API刪除憑據](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速啟動（SOAP模式）:使用Java API刪除憑據](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
