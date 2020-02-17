---
title: 使用API叫用AEM Forms
seo-title: 使用API叫用AEM Forms
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用API叫用AEM Forms {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms是以J2EE為基礎的企業軟體，包含可在共用基礎架構中運作的服務。 服務操作通常使用或生成文檔。 透過使用AEM Forms，您可以將表單工作流程與電子錶單、檔案安全性和檔案產生結合為整合且緊密整合的服務集。 這些服務可從防火牆內外存取。

用戶端應用程式可使用Java API、web services、Remoting和REST，以程式設計方式叫用AEM Forms服務。 使用管理控制台，您可以設定服務來公開端點，讓AEM Forms服務透過程式調用。 依預設，大部分服務都已預先設定為公開Remoting、Java和web服務端點。

您的業務需求會決定要使用哪種呼叫方法。 例如，您可以使用Java API，將AEM Forms功能整合到Java企業應用程式，例如Java Entity和Message Bean。 同樣地，您也可以使用web services，將AEM Forms功能整合至。NET專案（或是使用支援web services標準的開發環境開發的其他專案）。

服務需要服務容器才能執行，類似於Enterprise javaBeans™(EJB)需要J2EE容器的方式。 AEM Forms只包含一個服務容器的實作。 服務容器負責管理服務的存留期，包括部署服務，並確保所有請求都發送到正確的服務。 它還管理服務所消費或產生的檔案。

>[!NOTE]
>
>使用AEM表格進行程式設計時，並未包含如何使用「監看的檔案夾」或電子郵件叫用AEM表格的資訊。

