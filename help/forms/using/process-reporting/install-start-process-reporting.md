---
title: 流程報告快速入門
seo-title: 流程報告快速入門
description: 開始使用AEM Forms on JEE Process Reporting時，您需要遵循的步驟
seo-description: 開始使用AEM Forms on JEE Process Reporting時，您需要遵循的步驟
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# 流程報告快速入門{#getting-started-with-process-reporting}

「流程報表」可讓AEM Forms使用者查詢目前在AEM Forms實作中定義的AEM Forms進程相關資訊。 不過，「流程報表」不會直接從AEM Forms儲存庫存取資料。 資料首先按計畫發佈到「流程報告」儲存庫(由ProcessDataPublisher *和ProcessDataStorage服*&#x200B;務發佈)。 然後，從發佈到儲存庫的「流程報告」資料中生成「流程報告」中的報告和查詢。 Process Reporting是作為Forms Workflow模組的一部分安裝的。

本文詳細說明啟用將AEM Forms資料發佈至「流程報表」儲存庫的步驟。 之後，您將可以使用「流程報告」來執行報告和查詢。 文章也涵蓋設定「流程報表」服務的可用選項。

## 流程報告先決條件 {#process-reporting-pre-requisites}

### 清除非必要流程 {#purge-non-essential-processes}

如果您目前使用Forms Workflow,AEM Forms資料庫可能會包含大量資料

「流程報表」發佈服務會發佈資料庫中目前可用的所有AEM Forms資料。 這意味著，如果資料庫包含您不想運行報告和查詢的舊資料，則所有該資料也將發佈到儲存庫，即使報告不需要它。 建議您在執行服務之前清除此資料，以將資料發佈到Process Reporting儲存庫。 這將改善發佈者服務和查詢資料以進行報告的服務的效能。

有關清除AEM Forms流程資料的詳細資訊，請參閱 [清除流程資料](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)。

>[!NOTE]
>
>如需清除公用程式的秘訣與訣竅，請參閱Adobe Developer Connection中有關清除程式與工 [作的文章](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)。

## 配置進程報告服務 {#configuring-process-reporting-services}

### 排程流程資料發佈 {#schedule-process-data-publishing}

「流程報表」服務會排程將資料從AEM Forms資料庫發佈至「流程報表」儲存庫。

此作業會耗用大量資源，並會影響AEM Forms伺服器的效能。 建議您在AEM Forms伺服器忙碌時段以外排程此作業。

依預設，資料發佈會排程在每天凌晨2:00執行。

執行下列步驟以變更發佈排程：

>[!NOTE]
>
>如果您正在叢集上執行AEM Forms實作，請在叢集的每個節點上執行下列步驟。

1. 停止AEM Forms伺服器例項。
1. 

   * （適用於Windows）在編輯 `[JBoss root]/bin/run.conf.bat` 器中開啟檔案。
   * （適用於Linux、AIX和Solaris） `[JBoss root]/bin/run.conf.sh` 檔案。

1. 添加JVM參數 `-Dreporting.publisher.cron = <expression>.`

   範例：下列cron運算式會使「流程報表」每5小時將AEM Forms資料發佈至「流程報表」儲存庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 儲存並關閉 `run.conf.bat` 檔案。

1. 重新啟動AEM Forms伺服器例項。

1. 停止AEM Forms伺服器例項。
1. 登入WebSphere管理控制台。 在導覽樹中，按一 **下「伺服器** >應 **用程式伺服器** 」，然後在右窗格中按一下伺服器名稱。

1. 在「伺服器基礎結構」下，單 **擊「Java和流程管理** 」 > 「 **流程定義」**。

1. 在「其他屬性」下，單 **擊「Java虛擬機**」。

   在「通用JVM參數」框中，添加參數 `-Dreporting.publisher.cron = <expression>.`

   **範例**:下列cron運算式會使「流程報表」每5小時將AEM Forms資料發佈至「流程報表」儲存庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一 **下「套用**」、按一下「確定」，然後按 **一下「直接儲存至主配置」**。
1. 重新啟動AEM Forms伺服器例項。
1. 停止AEM Forms伺服器例項。
1. 登入WebLogic管理控制台。 WebLogic管理控制台的預設位址為 `https://[hostname]:[port]/console`。
1. 在「變更中心」下，按一下「 **鎖定與編輯」**。
1. 在「域結構」下，單 **擊「環境** 」 > 「服 **務器** 」 ，然後在右窗格中按一下受控伺服器名稱。
1. 在下一個畫面中，按一下「 **設定** 」標籤> **「伺服器開始** 」標籤。
1. 在「參數」框中，添加JVM參數 `-Dreporting.publisher.cron = <expression>`。

   **範例**:下列cron運算式會使「流程報表」每5小時將AEM Forms資料發佈至「流程報表」儲存庫：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一 **下「儲存** 」，然後按一 **下「啟用變更」**。
1. 重新啟動AEM Forms伺服器例項。

![processdatabublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服務 {#processdatastorage-service}

ProcessDataStorageProvider服務從ProcessDataPublisher服務接收流程資料，並將資料保存到Process Reporting儲存庫。

在每個發佈週期中，資料都會儲存至預先定義之根資料夾的子檔案夾。

您可以使用管理控制台來設定根目錄(預&#x200B;**設值**: `/content/reporting/pm`)位置和子資料夾(預&#x200B;**設值**: `/yyyy/mm/dd/hh/mi/ss`)將儲存流程資料的層次格式。

#### 要配置Process Reporting儲存庫位置，請執行以下操作： {#to-configure-the-process-reporting-repository-locations}

1. 使用管理員 **憑證登入** 「管理控制台」。 管理控制台的預設URL為 `https://[server]:[port]/adminui`
1. 導覽至「 **首頁** >服務 **** >應用程 **式與服務** >服務管&#x200B;******** 理流程和開放DataStorageProvider Service」。

   ![過程——資料儲存——服務](assets/process-data-storage-service.png)

   **RootFolder**

   儲存流程資料以用於報告的CRX位置。

   `Default`: `/content/reporting/pm`

   **資料夾階層**

   根據流程建立時間儲存流程資料的資料夾層次結構。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 按一下&#x200B;**「儲存」**。

### ReportConfiguration服務 {#reportconfiguration-service}

Process Reporting使用ReportConfiguration服務來配置流程報告查詢服務。

#### 要配置ReportingConfiguration服務 {#to-configure-the-reportingconfiguration-service}

1. 使用CRX管理員 **憑證登入Configuration Manager** 。 配置管理器的預設URL是 `https://[server]:[port]/lc/system/console/configMgr`
1. 開啟 **ReportingConfiguration** 服務。
1. **記錄數**

   在儲存庫上運行查詢時，結果可能包含大量記錄。 如果結果集很大，則查詢執行可以佔用伺服器資源。

   要處理大型結果集，ReportConfiguration服務會將查詢處理拆分為多個記錄批。 這樣可減輕系統負載。

   `Default`: `1000`

   **CRX儲存路徑**

   儲存流程資料以用於報告的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置與在ProcessDataStorage配置選項根資料夾中指 **定的位置相同**。
   >
   >
   >如果更新ProcessDataStorage配置中的根資料夾選項，則需要更新ReportConfiguration服務中的CRX儲存路徑位置。

1. 按一 **下「儲存** 」並關 **閉「CQ設定管理員」**。

### ProcessDataPublisher服務 {#processdatapublisher-service}

ProcessDataPublisher服務從AEM Forms資料庫導入流程資料，並將資料發佈到ProcessDataStorageProvider服務以進行儲存。

#### 要配置ProcessDataPublisher服務 {#to-configure-processdatapublisher-service-nbsp}

1. 使用管理員 **憑證登入** 「管理控制台」。

   預設URL為 `https://[server]:port]/adminui/`。

1. 導航至「 **Services** > **Services** > Applications and Services **>********** Open Management And Open The Publisher Service」。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**發佈資料**

啟用此選項可開始發佈程式資料。 依預設，此選項會停用。

僅當與Process Reporting元件相關的所有配置都已正確設定時，才啟用Process Reporting。

或者，使用此選項可在不再需要發佈流程資料時停用。

`Default`: `Off`

**批次間隔（秒）**

每次ProcessDataPublisher服務運行時，服務首先按批次間隔分割自上次運行服務以來的時間。 然後，服務會分別處理AEM Forms資料的每個間隔。

這有助於控制發佈者在週期內每次執行（批次）時，端對端處理的資料大小。

例如，如果發佈者每天執行，則依預設，不會在單次執行中處理一天的整個資料，而是將處理分為24批，每批一小時。

`Default`: `3600`

`Unit`: `Seconds`

**鎖定超時（秒）**

發佈者服務在開始處理資料時獲取鎖定，使得發佈者的多個實例不同時開始運行和處理資料。

如果已獲取鎖定的發佈者服務在「鎖定超時」值定義的秒數內處於空閒狀態，則其鎖定將被釋放，以便其他發佈者服務實例可以繼續處理。

`Default`: `3600`

`Unit`: `Seconds`

**發佈資料自**

AEM Forms環境包含環境設定時的資料。

依預設，ProcessDataPublisher服務會從AEM Forms資料庫匯入所有資料。

根據您的報表需求，如果您打算在特定日期和時間後對資料執行報表和查詢，建議您指定日期和時間。 然後，發佈服務會從那時開始發佈日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 訪問Process Reporting用戶介面 {#accessing-the-process-reporting-user-interface}

「流程報告」的用戶介面基於瀏覽器。

在設定「流程報表」後，您可以在AEM Forms安裝的下列位置開始使用「流程報表」:

`https://<server>:<port>/lc/pr`

### 登入流程報表 {#log-in-to-process-reporting}

當您導覽至「程式報表URL」(https://&lt;server>:&lt;port>/lc/pr)時，會顯示登入畫面。

指定您的憑據以登錄到Process Reporting模組。

>[!NOTE]
>
>若要登入Process Reporting使用者介面，您需要下列AEM Forms權限：
>
>`PERM_PROCESS_REPORTING_USER`

![登入流程報表](assets/capture1_new.png)

當您登入「流程報表」時，會顯示「 **[!UICONTROL 首頁]** 」畫面。

### 流程報告主螢幕 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**** 流程報告樹視圖：主螢幕左側的樹視圖包含「流程報告」模組的項。

樹視圖由下列頂層項目組成：

**** 報表：此項目包含隨「流程報告」一起提供的現成報表。

有關預定義報表的詳細資訊，請參 [閱「在處理中預定義報表」](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)。

**** 臨機查詢：此項目包含對進程和任務執行基於篩選的搜索的選項。

如需臨機查詢的詳細資訊，請參 [閱「處理中的臨機查詢」](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**** 自訂：「自訂」節點會顯示您建立的自訂報表。

如需建立和顯示自訂報表的程式，請參閱「 [流程報表中的自訂報表」](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**** 流程報告標題欄：「流程報表」標題列包含一些在使用者介面中工作時可使用的一般選項。

**** 流程報告標題：「流程報表」標題會顯示在標題列的左角。

隨時按一下標題，返回「首頁」畫面。

**** 上次更新時間：流程資料會從AEM Forms資料庫以排程方式發佈至「流程報表」儲存庫。

「上次更新時間」會顯示資料更新推送至「流程報表」儲存庫的最後日期和時間。

有關資料發佈服務以及如何計畫此服務的詳細資訊，請參閱「流程報告快速入門 [」中的](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) 「計畫流程資料發佈」。

**** 流程報告用戶：登入的使用者名稱會顯示在「上次更新」時間的右側。

**** 處理報表標題列下拉式清單：「流程報表」標題列右角的下拉式清單包含下列選項：

* **[!UICONTROL 同步]**:將內嵌的Process Reporting儲存庫與AEM Forms資料庫同步。
* **[!UICONTROL 說明]**:查看有關流程報告的幫助文檔。
* **[!UICONTROL 註銷]**:註銷進程報告

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
