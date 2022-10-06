---
title: 使用API叫用AEM Forms
seo-title: Invoking AEM Forms using APIs
description: 使用API叫用AEM Forms
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

# 使用API叫用AEM Forms {#invoking-aem-forms-using-apis}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Adobe Experience Manager Forms是基於J2EE的企業軟體，包含在共用基礎架構中運行的服務。 服務操作通常使用或生成文檔。 使用AEM Forms，您可以將表單工作流程與電子錶單、檔案安全性，以及檔案產生等功能結合為一組整合且緊密的服務。 這些服務可從防火牆內外存取。

用戶端應用程式可使用Java API、Web服務、Remoting和REST，以程式設計方式叫用AEM Forms服務。 使用Administration Console，您可以設定服務以公開端點，以程式叫用AEM Forms服務。 預設情況下，大多數服務都預先配置為公開遠程、Java和Web服務端點。

您的業務需求決定要使用的叫用方法。 例如，使用Java API，您可以將AEM Forms功能整合到Java企業應用程式中，如Java實體和消息Bean。 同樣，您可以使用Web服務將AEM Forms功能整合到.NET項目（或與支援Web服務標準的開發環境一起開發的其他項目）中。

服務需要服務容器才能運行，與Enterprise JavaBeans™(EJB)需要J2EE容器的方式類似。 AEM Forms僅包含服務容器的一個實作。 服務容器負責管理服務的存留期，包括部署服務，並確保所有請求都傳送至正確的服務。 它還管理服務使用或生成的文檔。

>[!NOTE]
>
>使用AEM表單進行程式設計時，不包含如何使用監看資料夾或電子郵件叫用AEM Forms的資訊。
