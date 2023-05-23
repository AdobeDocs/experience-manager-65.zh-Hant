---
title: 使用API調用AEM Forms
seo-title: Invoking AEM Forms using APIs
description: 使用API調用AEM Forms
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 使用API調用AEM Forms {#invoking-aem-forms-using-apis}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

Adobe Experience Manager Forms是基於J2EE的企業軟體，由在共用基礎架構中運行的服務組成。 服務操作通常使用或生成文檔。 通過使用AEM Forms，您可以將表單工作流與電子錶單、文檔安全性和文檔生成結合起來，形成一組整合且緊密結合的服務。 這些服務可以從防火牆內外訪問。

客戶端應用程式可以使用Java API、Web服務、遠程處理和REST以寫程式方式調用AEM Forms服務。 使用管理控制台，可以配置服務以公開允許以寫程式方式調用AEM Forms服務的終結點。 預設情況下，大多數服務都預先配置為公開遠程處理、Java和Web服務端點。

您的業務需求決定了要使用的調用方法。 例如，使用Java API，可以將AEM Forms功能整合到Java企業應用程式中，如Java實體和消息Bean。 同樣，您可以使用Web服務將AEM Forms功能整合到.NET項目（或使用支援Web服務標準的開發環境開發的其他項目）中。

服務需要運行服務容器，與Enterprise JavaBeans™(EJB)需要J2EE容器的方式類似。 AEM Forms只包括一個服務容器的實現。 服務容器負責管理服務的生命週期，包括部署服務並確保所有請求都發送到正確的服務。 它還管理服務使用或生成的文檔。

>[!NOTE]
>
>使用表AEM格寫程式不包括如何使用受監視資料夾或電子郵件調用AEM Forms的資訊。
