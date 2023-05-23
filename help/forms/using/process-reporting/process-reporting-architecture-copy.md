---
title: 流程報告的工作方式
seo-title: How Process Reporting Works
description: AEM FormsJEE Process Reporting服務描述和Process Reporting UI簡介
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 流程報告的工作方式 {#how-process-reporting-works}

Process Reporting是AEM Forms關於JEE的報告模組。

「進程報告」允許您運行有關AEM Forms進程和任務的報告。

Process Reporting使用嵌入式Process Reporting儲存庫發佈Forms資料。 然後，它使用該資料來運行報告。

Process Reporting由以下模組組成：

* [ProcessDataPublisher服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorage服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [查詢資料servlet](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Process Reporting用戶介面](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## 流程報告體系結構 {#process-reporting-architecture-br}

![進程報告體系結構](assets/processreportingarchitecture.png)

## 流程報告模組 {#process-reporting-modules}

### ProcessDataPublisher服務 {#processdatapublisher-service-br}

ProcessDataPublisher伺服器定期在AEM Forms資料庫上運行，並提取自上次運行服務以來已更改的資料。 然後，它將資料發佈到「進程資料儲存」服務。

有關配置服務的詳細資訊，請參見 [配置ProcessDataPublisher服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)。

### ProcessDataStorageProvider服務 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服務從ProcessDataPublisher服務接收進程資料，並將資料保存到Process Reporting儲存庫。

有關配置服務的詳細資訊，請參見 [配置ProcessDataStorageProvider服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)。

### OSGi服務 {#osgi-service-br}

QueryDataServlet使用此服務從Process Reporting儲存庫獲取報告資料。

### QueryDataServlet服務 {#querydataservlet-service-br}

QueryDataServlet服務接受來自Process Reporting用戶介面的查詢。

然後，該服務使用OSGi服務來獲取相關的報告資料，處理該資料，並將該資料返回到用戶介面。

### Process Reporting用戶介面 {#process-reporting-user-interface-br}

Process Reporting用戶介面是基於Web瀏覽器的介面。 使用此介面可以查看從AEM Forms資料庫發佈的進程和任務資訊。

### QueryDataServlet服務 {#querydataservlet-service-br-1}

QueryDataServlet服務接受來自Process Reporting用戶介面的查詢。

然後，該服務使用OSGi服務來獲取相關的報告資料，處理該資料，並將該資料返回到用戶介面。

### 自定義報告 {#custom-reports-br}

您可以建立自己的自定義報告，並在「流程報告」用戶介面的「自定義報告」頁籤中顯示這些報告。

有關建立自定義報告的步驟，請參閱文章中的建立自定義報告 [正在處理的自定義報表](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。
