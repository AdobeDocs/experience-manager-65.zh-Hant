---
title: Java API快速入門簡介
seo-title: Introducing Java API QuickStart
description: Java API快速入門簡介
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Java API快速入門簡介 {#introducing-java-api-quickstart}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

AdobeAEM FormsAPI快速入門可幫助您加快開發與AEM Forms服務交互的程式的速度。 *快速啟動* s是完整的程式，您可以將其複製並貼上到您自己的項目中，並用作起點。 您可以運行快速入門以查看其行為方式，並根據自己的需要修改它。

AEM Forms操作可以使用AEM Forms強類型API執行，連接模式應設定為SOAP。

Java強類型API快速啟動提供了執行Java應用程式所需的JAR檔案清單。 大多數Java快速啟動是運行在 `main`。 但是，FormsJava強類型API快速啟動是作為在Web應用程式內運行的Java Servlet實現的。

JAR檔案清單位於快速啟動開始處的注釋部分。 例如，以下注釋位於「輸出快速啟動」中，是每個Java快速啟動中都找到的典型JAR檔案清單。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 多服務快速啟動 {#multiple-services-quick-start}

位於的大多數快速入門 *與AEM Forms就JEE進行方案編製* 調用特定服務以執行操作。 但是，某些快速啟動會調用多個AEM Forms服務以執行給定的工作流。 以下清單提供調用多個AEM Forms服務的Java快速啟動：

[快速啟動（SOAP模式）:使用Java API將位於AEM Forms資料檔案庫中的文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （調用儲存庫和輸出服務）

[快速啟動（SOAP模式）:使用Java API基於片段建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （調用匯編器和輸出服務）

[快速啟動（SOAP模式）:使用Java API使用提交的XML資料建立PDF文檔](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (調用Forms、輸出和文檔管理服務)

[快速啟動（SOAP模式）:使用Java API將文檔傳遞到Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (調用Forms和文檔管理服務)

[快速啟動（SOAP模式）:使用Java API對基於XFA的表單進行數字簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (調用Forms和簽名服務)

[快速啟動（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （調用DirectoryManager和AuthorizationManager服務）

[快速啟動（SOAP模式）:使用Java API將文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （調用輸出和文檔管理服務）

>[!NOTE]
>
>「Quick Start（快速入門）」位於「Programming withAEM Forms」中，它基於部署在JBoss® Application Server和Microsoft® Windows®作業系統上的AEM Forms。 但是，如果您使用的是其他作業系統（如UNIX®），請將Windows特定路徑替換為適用作業系統支援的路徑。 同樣，如果您使用的是另一個J2EE應用程式伺服器，請確保指定有效的連接屬性。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE]
>
>大多數Web服務快速啟動都以C#編寫，並使用.NET框架。 但是，您可以建立客戶端應用程式邏輯，該邏輯能夠在任何支援SOAP標準的開發環境中調用AEM Forms服務。 (請參閱 [使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)
