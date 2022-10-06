---
title: 程式報告的運作方式
seo-title: How Process Reporting Works
description: 說明在JEE流程報表上組成AEM Forms的服務，以及流程報表UI的簡介
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# 程式報告的運作方式{#how-process-reporting-works}

程式報表是JEE上AEM Forms的報表模組。

「程式報表」可讓您執行AEM Forms程式和任務的報表。

「流程報表」使用內嵌的「流程報表」存放庫來發佈Forms資料。 然後會使用該資料執行報表。

Process Reporting包含以下模組：

* [ProcessDataPublisher服務](#processdatapublisher-service-br-p)
* [ProcessDataStorage服務](#processdatastorageprovider-service-br-p)
* [OSGi服務](#osgi-service-br-p)
* [查詢資料Servlet](#querydataservlet-service-br-p)
* [進程報告用戶介面](#process-reporting-user-interface-br-p)

## 流程報告體系結構 {#process-reporting-architecture-br}

![處理報告架構](assets/processreportingarchitecture.png)

## 流程報告模組 {#process-reporting-modules}

### ProcessDataPublisher服務 {#processdatapublisher-service-br}

ProcessDataPublisher伺服器在AEM Forms資料庫上定期運行，並提取自上次運行服務後更改的資料。 然後，它會將資料發佈到「處理資料儲存」服務。

如需設定服務的詳細資訊，請參閱 [配置ProcessDataPublisher服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### ProcessDataStorageProvider服務 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服務從ProcessDataPublisher服務接收進程資料，並將資料保存到Process Reporting儲存庫。

如需設定服務的詳細資訊，請參閱 [配置ProcessDataStorageProvider服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### OSGi服務 {#osgi-service-br}

QueryDataServlet使用此服務從進程報告儲存庫中獲取報告資料。

### QueryDataServlet服務 {#querydataservlet-service-br}

QueryDataServlet服務接受來自進程報告用戶介面的查詢。

然後，該服務使用OSGi服務來取得相關的報告資料、處理資料，並將資料傳回至使用者介面。

### 進程報告用戶介面 {#process-reporting-user-interface-br}

「流程報告」用戶介面是基於Web瀏覽器的介面。 使用此介面可以查看從AEM Forms資料庫發佈的流程和任務資訊。

有關「流程報告」用戶介面的介紹，請參見 [進程報告用戶介面](/help/forms/using/process-reporting/introduction-process-reporting.md).

### QueryDataServlet服務 {#querydataservlet-service-br-1}

QueryDataServlet服務接受來自進程報告用戶介面的查詢。

然後，該服務使用OSGi服務來取得相關的報告資料、處理資料，並將資料傳回至使用者介面。

### 自訂報表 {#custom-reports-br}

您可以建立自己的自訂報表，並在「流程報表」使用者介面的「自訂報表」標籤中顯示這些報表。

如需建立自訂報表的步驟，請參閱文章中的建立自訂報表 [自訂處理中報表](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
