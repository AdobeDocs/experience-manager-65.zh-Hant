---
title: 如何使用API叫用AEM Forms？
description: 瞭解如何使用Java&trade、API、網站服務、遠端處理和REST來叫用AEM Forms服務。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 使用API叫用AEM Forms {#invoking-aem-forms-using-apis}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

Adobe Experience Manager Forms是以J2EE為基礎的企業軟體，由可在共用基礎架構中操作的服務所組成。 服務作業通常會沖銷或產生檔案。 透過使用AEM Forms，您可以將Forms Workflow與電子錶單、Document Security和檔案產生結合在完整且具凝聚力的服務組合中。 這些服務可從防火牆內外存取。

使用者端應用程式能使用Java™ API、網站服務、Remoting和REST，以程式設計方式叫用AEM Forms服務。 使用管理主控台，您可以設定服務以程式化方式叫用來公開讓AEM Forms服務的端點。 依預設，大部分服務都已預先設定為公開遠端、Java™和Web服務端點。

您的業務需求會決定要使用的呼叫方法。 例如，使用Java™ API時，您可以將AEM Forms功能整合至Java™企業應用程式，例如Java™實體和訊息Bean。 同樣地，您可以使用Web服務，將AEM Forms功能整合到.NET專案（或是使用支援Web服務標準的開發環境所開發的其他專案）中。

服務需要服務容器才能執行，就像Enterprise JavaBeans™ (EJB)需要J2EE容器一樣。 AEM Forms僅包含服務容器的一個實作。 服務容器負責管理服務的存留期，包括部署服務，並確保將所有要求傳送至正確的服務。 它也會管理服務使用或產生的檔案。

>[!NOTE]
>
>使用AEM表單進行程式設計時，不會包含如何使用Watched資料夾或電子郵件叫用AEM Forms的資訊。
