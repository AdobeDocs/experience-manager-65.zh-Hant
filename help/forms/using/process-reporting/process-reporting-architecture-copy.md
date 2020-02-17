---
title: 流程報告的運作方式
seo-title: 流程報告的運作方式
description: JEE流程報表上AEM表單的服務說明及流程報表UI簡介
seo-description: JEE流程報表上AEM表單的服務說明及流程報表UI簡介
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 流程報告的運作方式 {#how-process-reporting-works}

「流程報表」是JEE上AEM Forms的報表模組。

「流程報表」可讓您執行AEM Forms流程和工作的報表。

Process Reporting使用嵌入的Process Reporting儲存庫發佈Forms資料。 然後，它會使用該資料來執行報表。

Process Reporting由以下模組組成：

* [ProcessDataPublisher服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorage服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi服務](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [查詢資料servlet](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [流程報告用戶介面](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## 流程報告體系結構 {#process-reporting-architecture-br}

![處理報告架構](assets/processreportingarchitecture.png)

## 流程報告模組 {#process-reporting-modules}

### ProcessDataPublisher服務 {#processdatapublisher-service-br}

ProcessDataPublisher伺服器會定期在AEM Forms資料庫上執行，並擷取自上次執行服務後變更的資料。 然後，它將資料發佈到「流程資料儲存」服務。

有關配置服務的詳細資訊，請參 [閱Configure ProcessDataPublisher服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)。

### ProcessDataStorageProvider服務 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服務從ProcessDataPublisher服務接收流程資料，並將資料保存到Process Reporting儲存庫。

有關配置服務的詳細資訊，請參 [閱配置ProcessDataStorageProvider服務](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)。

### OSGi服務 {#osgi-service-br}

QueryDataServlet使用此服務從「進程報告」儲存庫中獲取報告資料。

### QueryDataServlet服務 {#querydataservlet-service-br}

QueryDataServlet服務接受來自Process Reporting用戶介面的查詢。

然後，該服務使用OSGi服務獲取相關的報告資料，處理資料，並將資料返回到用戶介面。

### 流程報告用戶介面 {#process-reporting-user-interface-br}

「流程報告」用戶介面是基於Web瀏覽器的介面。 您可使用此介面來檢視從AEM Forms資料庫發佈的程式和任務資訊。

### QueryDataServlet服務 {#querydataservlet-service-br-1}

QueryDataServlet服務接受來自Process Reporting用戶介面的查詢。

然後，該服務使用OSGi服務獲取相關的報告資料，處理資料，並將資料返回到用戶介面。

### 自訂報表 {#custom-reports-br}

您可以建立自己的自訂報表，並在「流程報表」使用者介面的「自訂報表」標籤中顯示這些報表。

如需建立自訂報表的步驟，請參閱「在流程報表中自訂報表」文章中的「 [若要建立自訂報表」](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
