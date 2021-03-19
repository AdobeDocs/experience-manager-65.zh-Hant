---
title: Java API QuickStart簡介
seo-title: Java API QuickStart簡介
description: Java API QuickStart簡介
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Java API快速入門簡介{#introducing-java-api-quickstart}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

AdobeAEM FormsAPI快速入門可協助您加速開發與AEM Forms服務互動的程式。 *快速*&#x200B;啟動是完整的程式，您可將它複製並貼入您自己的專案中，並當做起點使用。您可以執行快速入門來查看其運作方式，並依您自己的需求加以修改。

AEM Forms操作可以使用AEM Forms強類型API執行，連接模式應設定為SOAP。

Java強類型API快速啟動提供執行Java應用程式所需的JAR檔案清單。 大多數Java快速啟動是運行在`main`中的控制台應用程式。 不過，FormsJava強式型API快速入門是以在Web應用程式中執行的Java servlet實作。

JAR檔案清單位於「快速啟動」開頭的注釋部分。 例如，以下注釋位於「輸出快速啟動」中，是每個Java快速啟動中的典型JAR檔案清單。

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

## 多服務快速入門{#multiple-services-quick-start}

位於&#x200B;*Programming withAEM Forms on JEE*&#x200B;的大多數快速入門程式調用特定服務以執行操作。 不過，有些「快速入門」會叫用多個AEM Forms服務，以執行指定的工作流程。 以下清單提供調用多個AEM Forms服務的Java快速啟動：

[快速入門（SOAP模式）:使用Java API將位於AEM Forms資料檔案庫中的文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （調用資料檔案庫和輸出服務）

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （叫用Assembler and Output服務）根據片段建立PDF檔案

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (叫用「Forms」、「輸出」和「檔案管理」服務)使用提交的XML資料建立PDF檔案

[快速入門（SOAP模式）:使用Java API將檔案傳送至Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (叫用Forms和檔案管理服務)

[快速入門（SOAP模式）:使用Java API數位簽署以XFA為基礎的表單](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (叫用Forms和簽名服務)

[快速入門（SOAP模式）:使用Java API管理角色和權限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （調用DirectoryManager和AuthorizationManager服務）

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （叫用「輸出與檔案管理」服務）將檔案傳送至「輸出服務」

>[!NOTE]
>
>「與AEM Forms一起寫程式」中的「快速入門」基於部署在JBoss® Application Server和Microsoft® Windows®作業系統上的AEM Forms。 但是，如果您使用其他作業系統（例如UNIX®），請以適用作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請確定您指定有效的連線屬性。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>大多數Web服務快速入門都以C#編寫，使用。NET架構。 不過，您可以建立用戶端應用程式邏輯，以便在支援SOAP標準的任何開發環境中叫用AEM Forms服務。 (請參閱[使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)

