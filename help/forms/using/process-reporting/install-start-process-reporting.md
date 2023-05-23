---
title: 流程報告入門
description: 開始使用AEM Forms的JEE流程報告步驟
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# 流程報告入門{#getting-started-with-process-reporting}

進程報告使AEM Forms用戶能夠查詢有關AEM Forms進程的資訊，這些進程當前在AEM Forms實施中定義。 但是， Process Reporting不直接從AEM Forms儲存庫訪問資料。 資料首先按計畫發佈到Process Reporting儲存庫(*由ProcessDataPublisher和ProcessDataStorage服務* s)。 然後，將從發佈到儲存庫的Process Reporting資料中生成Process Reporting中的報告和查詢。 Process Reporting作為Forms Workflow模組的一部分安裝。

本文詳細介紹了啟用將AEM Forms資料發佈到Process Reporting儲存庫的步驟。 之後，您將能夠使用Process Reporting運行報告和查詢。 文章還介紹了配置Process Reporting服務的可用選項。

## 流程報告先決條件 {#process-reporting-pre-requisites}

### 清除非基本流程 {#purge-non-essential-processes}

如果您當前正在使用Forms Workflow,AEM Forms資料庫可能包含大量資料

進程報告發佈服務發佈資料庫中當前可用的所有AEM Forms資料。 它意味著，如果資料庫包含不想運行報告和查詢的舊資料，則所有這些資料也會發佈到儲存庫，即使報告不需要它。 建議在運行服務以將資料發佈到Process Reporting儲存庫之前清除此資料。 這樣可以提高發佈服務和查詢資料以進行報告的服務的效能。

有關清除AEM Forms流程資料的詳細資訊，請參閱 [清除流程資料](/help/forms/using/admin-help/purging-process-data.md)。

>[!NOTE]
>
>有關清除實用程式的提示和技巧，請參閱Adobe Developer Connection上的文章 [清除進程和作業](/help/forms/using/admin-help/purging-process-data.md)。

## 配置Process Reporting服務 {#configuring-process-reporting-services}

### 計畫流程資料發佈 {#schedule-process-data-publishing}

進程報告服務按計畫將資料從AEM Forms資料庫發佈到進程報告儲存庫。

此操作可能佔用大量資源，並可能影響AEM Forms伺服器的效能。 建議您在AEM Forms伺服器忙時隙外安排此時間。

預設情況下，資料發佈計畫每天凌晨2:00運行。

要更改發佈計畫，請執行以下步驟：

>[!NOTE]
>
>如果您正在群集上運行AEM Forms實現，請在群集的每個節點上執行以下步驟。

1. 停止AEM Forms伺服器實例。
1. &#x200B;

   * （對於Windows）開啟 `[JBoss root]/bin/run.conf.bat` 的子菜單。
   * （適用於Linux®、AIX®和Solaris™） `[JBoss root]/bin/run.conf.sh` 的子菜單。

1. 添加JVM參數 `-Dreporting.publisher.cron = <expression>.`

   示例：以下cron表達式使Process Reporting每五小時將AEM Forms資料發佈到Process Reporting儲存庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 保存並關閉 `run.conf.bat` 的子菜單。

1. 重新啟動AEM Forms伺服器實例。

1. 停止AEM Forms伺服器實例。
1. 登錄到WebSphere®管理控制台。 在導航樹中，按一下 **伺服器** > **應用程式伺服器** 然後，在右窗格中，按一下伺服器名。

1. 在「伺服器基礎架構」下，按一下 **Java™和進程管理** > **流程定義**。

1. 在「其他屬性」下，按一下 **Java™虛擬機**。

   在「一般JVM參數」框中，添加參數 `-Dreporting.publisher.cron = <expression>.`

   **示例**:以下cron表達式使Process Reporting每五小時將AEM Forms資料發佈到Process Reporting儲存庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下 **應用**，按一下確定，然後按一下 **直接保存到主配置**。
1. 重新啟動AEM Forms伺服器實例。
1. 停止AEM Forms伺服器實例。
1. 登錄到WebLogic管理控制台。 WebLogic管理控制台的預設地址為 `https://[hostname]:[port]/console`。
1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯**。
1. 在「域結構」(Domain Structure)下，按一下 **環境** > **伺服器** 在右窗格中，按一下受控伺服器名稱。
1. 在下一螢幕上，按一下 **配置** 頁籤 **伺服器啟動** 頁籤。
1. 在「參數」框中，添加JVM參數 `-Dreporting.publisher.cron = <expression>`。

   **示例**:以下cron表達式使Process Reporting每五小時將AEM Forms資料發佈到Process Reporting儲存庫：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下 **保存** 然後按一下 **激活更改**。
1. 重新啟動AEM Forms伺服器實例。

![processdatablisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服務 {#processdatastorage-service}

ProcessDataStorageProvider服務從ProcessDataPublisher服務接收進程資料，並將資料保存到Process Reporting儲存庫。

在每個發佈週期，資料都保存到預定義根資料夾的子資料夾中。

可以使用管理控制台配置根(**預設**: `/content/reporting/pm`)位置和子資料夾(**預設**: `/yyyy/mm/dd/hh/mi/ss`)儲存流程資料的層次結構格式。

#### 配置Process Reporting儲存庫位置 {#to-configure-the-process-reporting-repository-locations}

1. 登錄到 **管理控制台** 具有管理員憑據。 管理控制台的預設URL為 `https://'[server]:[port]'/adminui`
1. 導航到 **首頁** > **服務** > **應用程式和服務** >**服務管理** 開啟 **ProcessDataStorageProvider** 服務。

   ![過程資料儲存服務](assets/process-data-storage-service.png)

   **根資料夾**

   儲存流程資料以用於報告的CRX位置。

   `Default`: `/content/reporting/pm`

   **資料夾層次結構**

   根據進程建立時間儲存進程資料的資料夾層次結構。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 按一下「**儲存**」。

### ReportConfiguration服務 {#reportconfiguration-service}

Process Reporting使用ReportConfiguration服務來配置Process Reporting查詢服務。

#### 配置ReportingConfiguration服務 {#to-configure-the-reportingconfiguration-service}

1. 登錄到 **配置管理器** 具有CRX管理員憑據。 Configuration Manager的預設URL為 `https://'[server]:[port]'/lc/system/console/configMgr`
1. 開啟 **報告配置** 服務。
1. **記錄數**

   在儲存庫上運行查詢時，結果可能包含許多記錄。 如果結果集很大，則查詢執行會佔用伺服器資源。

   要處理大的結果集，ReportConfiguration服務會將查詢處理拆分為記錄批。 這樣可減少系統負載。

   `Default`: `1000`

   **CRX儲存路徑**

   儲存流程資料以用於報告的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置與ProcessDataStorage配置選項中指定的位置相同 **根資料夾**。
   >
   >
   >如果在ProcessDataStorage配置中更新根資料夾選項，則必須更新ReportConfiguration服務中的CRX儲存路徑位置。

1. 按一下 **保存** 關閉 **CQ配置管理器**。

### ProcessDataPublisher服務 {#processdatapublisher-service}

ProcessDataPublisher服務從AEM Forms資料庫導入進程資料，並將資料發佈到ProcessDataStorageProvider服務以進行儲存。

#### 配置ProcessDataPublisher服務   {#to-configure-processdatapublisher-service-nbsp}

1. 登錄到 **管理控制台** 具有管理員憑據。

   預設URL為 `https://'server':port]/adminui/`。

1. 導航到 **首頁** > **服務** > **應用程式和服務** >**服務管理** 開啟 **進程資料發佈器** 服務。

![processdatablisherservice-1](assets/processdatapublisherservice-1.png)

**發佈資料**

啟用此選項可開始發佈進程資料。 預設情況下，該選項處於禁用狀態。

僅當與Process Reporting元件相關的所有配置都已正確設定時才啟用Process Reporting。

或者，如果不再需要此選項，則使用此選項禁用進程資料發佈。

`Default`: `Off`

**批處理間隔（秒）**

每次運行ProcessDataPublisher服務時，服務首先按批處理間隔分割自上次運行服務以來的時間。 然後，該服務分別處理AEM Forms資料的每個間隔，以幫助控制發佈者在週期內的每次運行（批處理）期間端到端處理的資料的大小。

例如，如果發佈伺服器每天運行，則預設情況下，它不會在一次運行中處理整個資料一天，而是將處理分解為24個批次，每個批次一小時。

`Default`: `3600`

`Unit`: `Seconds`

**鎖定超時（秒）**

發佈服務在開始處理資料時獲取鎖，使得發佈服務的多個實例不同時開始運行和處理資料。

如果已獲取鎖的發佈服務在鎖超時值定義的秒數內處於空閒狀態，則釋放其鎖，以便其他發佈服務實例可以繼續處理。

`Default`: `3600`

`Unit`: `Seconds`

**發佈資料的來源**

AEM Forms環境包含環境設定時的資料。

預設情況下，ProcessDataPublisher服務從AEM Forms資料庫導入所有資料。

根據報告需要，如果您計畫在特定日期和時間後對資料運行報告和查詢，建議您指定日期和時間。 然後，發佈服務將從那時起發佈該日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 訪問Process Reporting用戶介面 {#accessing-the-process-reporting-user-interface}

Process Reporting的用戶介面基於瀏覽器。

在設定Process Reporting後，可以開始在AEM Forms安裝中的以下位置使用Process Reporting:

`https://<server>:<port>/lc/pr`

### 登錄到Process Reporting {#log-in-to-process-reporting}

導航到Process Reporting URL(https://)時&lt;server>:&lt;port>/lc/pr)，將顯示登錄螢幕。

要登錄到Process Reporting模組，請指定憑據。

>[!NOTE]
>
>要登錄到Process Reporting用戶介面，您需要以下AEM Forms權限：
>
>`PERM_PROCESS_REPORTING_USER`

![登錄到流程報告](assets/capture1_new.png)

登錄Process Reporting時， **[!UICONTROL 首頁]** 螢幕。

### 「進程報告」首頁螢幕 {#process-reporting-home-screen}

![進程報告 — 主屏](assets/process-reporting-home-screen.png)

**Process Reporting樹視圖：** 「首頁」螢幕左側的樹視圖包含「流程報告」模組的項。

樹視圖由以下頂級項目組成：

**報告：** 此項目包含隨Process Reporting一起提供的現成報表。

有關預定義報告的詳細資訊，請參見 [預定義的在製品報告](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)。

**臨時查詢：** 此項目包含用於對進程和任務執行基於篩選器的搜索的選項。

有關即席查詢的詳細資訊，請參見 [Oracle Process報告中的即席查詢](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**自定義：** 「自定義」節點顯示您建立的自定義報告。

有關建立和顯示自定義報告的過程，請參見 [正在處理的自定義報表](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**流程報告標題欄：** 「流程報告」標題欄包含一些在用戶介面中工作時可以使用的常規選項。

**流程報告標題：** 「流程報告」標題顯示在標題欄的左角。

隨時按一下標題以返回主螢幕。

**上次更新時間：** 進程資料按計畫從AEM Forms資料庫發佈到進程報告儲存庫。

上次更新時間顯示資料更新推送到Process Reporting儲存庫的最後日期和時間。

有關資料發佈服務以及如何安排此服務的詳細資訊，請參見 [計畫流程資料發佈](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) 在「Getting Started with Process Reporting（入門流程報告）」一文中。

**Process Reporting用戶：** 登錄的用戶名顯示在上次更新時間的右側。

**處理報告標題欄下拉清單：** 「流程報告」標題欄右角的下拉清單包含以下選項：

* **[!UICONTROL 同步]**:將嵌入式Process Reporting儲存庫與AEM Forms資料庫同步。
* **[!UICONTROL 幫助]**:查看有關Process Reporting的幫助文檔。
* **[!UICONTROL 註銷]**:註銷進程報告
