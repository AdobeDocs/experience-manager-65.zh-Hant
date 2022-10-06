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

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

AdobeAEM Forms API快速入門可協助您加速開發與AEM Forms服務互動的程式。 *快速入門*&#x200B;是完整的方案，您可以複製並貼到自己的專案中，並作為起點使用。 您可以運行快速入門以查看其操作方式，並根據您自己的需求對其進行修改。

AEM Forms操作可使用AEM Forms強制類型API來執行，且連線模式應設為SOAP。

Java強類型API快速入門提供了執行Java應用程式所需的JAR檔案清單。 大多數Java快速啟動是在內運行的控制台應用程式 `main`. 不過，Forms Java強式型API快速入門是以在Web應用程式內執行的Java servlet實作。

JAR檔案清單位於快速入門的注釋部分。 例如，以下注釋位於「輸出」快速啟動中，是每個Java快速啟動中找到的典型JAR檔案清單。

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

## 多項服務快速入門 {#multiple-services-quick-start}

位於 *在JEE上與AEM Forms一起撰寫程式* 調用特定服務以執行操作。 不過，有些快速入門功能會叫用多個AEM Forms服務，以執行指定的工作流程。 下列清單提供叫用多個AEM Forms服務的Java快速入門：

[快速入門（SOAP模式）:使用Java API將AEM Forms存放庫中的檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （調用儲存庫和輸出服務）

[快速入門（SOAP模式）:使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （調用組合器和輸出服務）

[快速入門（SOAP模式）:使用Java API使用已提交的XML資料建立PDF文檔](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (調用Forms、輸出和文檔管理服務)

[快速入門（SOAP模式）:使用Java API將檔案傳遞至Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (調用Forms和文檔管理服務)

[快速入門（SOAP模式）:使用Java API以數位方式簽署XFA型表單](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (調用Forms和簽名服務)

[快速入門（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （調用DirectoryManager和AuthorizationManager服務）

[快速入門（SOAP模式）:使用Java API將檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （調用輸出和文檔管理服務）

>[!NOTE]
>
>「使用AEM Forms進行程式設計」中的「快速入門」以部署在JBoss® Application Server和Microsoft® Windows®作業系統上的AEM Forms為基礎。 但是，如果您使用的是其他作業系統(如UNIX®)，請用適用作業系統支援的路徑替換Windows專用路徑。 同樣，如果您正在使用其他J2EE應用程式伺服器，請確保指定有效的連接屬性。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>大多數Web服務快速入門都以C#編寫，並使用.NET框架。 不過，您可以建立客戶端應用程式邏輯，以便在支援SOAP標準的任何開發環境中調用AEM Forms服務。 (請參閱 [使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
