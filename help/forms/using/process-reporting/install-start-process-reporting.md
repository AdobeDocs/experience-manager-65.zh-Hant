---
title: 程式報告快速入門
description: 在JEE程式報表上開始使用AEM Forms的步驟
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# 程式報告快速入門{#getting-started-with-process-reporting}

「程式報表」可讓AEM Forms使用者查詢目前在AEM Forms實作中定義之AEM Forms程式的相關資訊。 不過，「程式報表」不會直接從AEM Forms存放庫存取資料。 資料會先排程發佈至「流程報告」存放庫(*由ProcessDataPublisher和ProcessDataStorage服務* s)。 然後，將從發佈到儲存庫的Process Reporting資料中生成Process Reporting中的報告和查詢。 流程報表作為Forms Workflow模組的一部分安裝。

本文詳細說明將AEM Forms資料發佈至Process Reporting存放庫的步驟。 之後，您將能使用「處理報告」來執行報表和查詢。 文章還介紹了配置流程報告服務的可用選項。

## 流程報表的先決條件 {#process-reporting-pre-requisites}

### 清除非必要流程 {#purge-non-essential-processes}

如果您目前使用Forms Workflow,AEM Forms資料庫可能會包含大量資料

Process Reporting發佈服務會發佈資料庫中目前可用的所有AEM Forms資料。 這意味著，如果資料庫包含您不想對其運行報告和查詢的舊資料，則所有這些資料也將發佈到儲存庫，即使不需要報告。 建議您在執行將資料發佈到流程報告儲存庫的服務之前清除此資料。 這麼做可改善發佈者服務和查詢資料以進行報告之服務的效能。

如需清除AEM Forms程式資料的詳細資訊，請參閱 [清除進程資料](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/maintain-aem-forms-database/purging-process-data.html?lang=en).

>[!NOTE]
>
>如需清除公用程式的秘訣和技巧，請參閱Adobe Developer Connection文章，位於 [清除程式和作業](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/maintain-aem-forms-database/purging-process-data.html?lang=en).

## 配置進程報告服務 {#configuring-process-reporting-services}

### 計畫流程資料發佈 {#schedule-process-data-publishing}

Process Reporting服務按計畫將資料從AEM Forms資料庫發佈到Process Reporting儲存庫。

此作業可能耗用大量資源，且可能影響AEM Forms伺服器的效能。 建議您在AEM Forms伺服器繁忙時段之外排程此作業。

依預設，資料發佈排程在每天凌晨2:00執行。

若要變更發佈排程，請執行下列步驟：

>[!NOTE]
>
>如果您在叢集上執行AEM Forms實作，請在叢集的每個節點上執行下列步驟。

1. 停止AEM Forms伺服器執行個體。
1. &#x200B;

   * （適用於Windows）開啟 `[JBoss root]/bin/run.conf.bat` 檔案。
   * (Linux®、AIX®和Solaris™) `[JBoss root]/bin/run.conf.sh` 檔案。

1. 添加JVM參數 `-Dreporting.publisher.cron = <expression>.`

   範例：以下cron運算式會使「處理報表」每五小時將AEM Forms資料發佈至「處理報表」存放庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 儲存並關閉 `run.conf.bat` 檔案。

1. 重新啟動AEM Forms伺服器執行個體。

1. 停止AEM Forms伺服器執行個體。
1. 登入WebSphere®管理控制台。 在導覽樹中，按一下 **伺服器** > **應用程式伺服器** 然後，在右窗格中，按一下伺服器名稱。

1. 在「伺服器基礎架構」下，按一下 **Java™和進程管理** > **進程定義**.

1. 在「其他屬性」下，按一下 **Java™虛擬機**.

   在「通用JVM參數」框中，添加參數 `-Dreporting.publisher.cron = <expression>.`

   **範例**:以下cron運算式會使「處理報表」每五小時將AEM Forms資料發佈至「處理報表」存放庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下 **套用**，按一下「確定」，然後按一下 **直接儲存至主配置**.
1. 重新啟動AEM Forms伺服器執行個體。
1. 停止AEM Forms伺服器執行個體。
1. 登入WebLogic管理控制台。 WebLogic管理控制台的預設地址為 `https://[hostname]:[port]/console`.
1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯**.
1. 在「域結構」(Domain Structure)下，按一下 **環境** > **伺服器** 在右窗格中，按一下受控伺服器名稱。
1. 在下一個畫面中，按一下 **設定** 標籤> **伺服器啟動** 標籤。
1. 在「參數」框中，添加JVM參數 `-Dreporting.publisher.cron = <expression>`.

   **範例**:以下cron運算式會使「處理報表」每五小時將AEM Forms資料發佈至「處理報表」存放庫：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下 **儲存** 然後按一下 **啟動變更**.
1. 重新啟動AEM Forms伺服器執行個體。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服務 {#processdatastorage-service}

ProcessDataStorageProvider服務從ProcessDataPublisher服務接收進程資料，並將資料保存到Process Reporting儲存庫。

在每個發佈週期中，資料都會儲存至預先定義之根資料夾的子資料夾。

您可以使用管理控制台來設定根目錄(**預設**: `/content/reporting/pm`)位置和子資料夾(**預設**: `/yyyy/mm/dd/hh/mi/ss`)階層格式，用於儲存處理資料。

#### 配置Process Reporting儲存庫位置 {#to-configure-the-process-reporting-repository-locations}

1. 登入 **管理控制台** 具有管理員憑據。 管理控制台的預設URL為 `https://'[server]:[port]'/adminui`
1. 導覽至 **首頁** > **服務** > **應用程式和服務** >**服務管理** 然後開啟 **ProcessDataStorageProvider** 服務。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **RootFolder**

   要儲存處理資料以便報告的CRX位置。

   `Default`: `/content/reporting/pm`

   **資料夾階層**

   根據進程建立時間儲存進程資料的資料夾層次結構。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 按一下「**儲存**」。

### ReportConfiguration服務 {#reportconfiguration-service}

Process Reporting使用ReportConfiguration服務來配置Process Reporting查詢服務。

#### 配置ReportingConfiguration服務 {#to-configure-the-reportingconfiguration-service}

1. 登入 **Configuration Manager** 具有CRX管理員憑證。 Configuration Manager的預設URL為 `https://'[server]:[port]'/lc/system/console/configMgr`
1. 開啟 **報表設定** 服務。
1. **記錄數**

   在存放庫上執行查詢時，結果可能會包含許多記錄。 如果結果集很大，則查詢執行可能會佔用伺服器資源。

   若要處理大型結果集，ReportConfiguration服務會將查詢處理分割為多個記錄批次。 這樣會降低系統負載。

   `Default`: `1000`

   **CRX儲存路徑**

   要儲存處理資料以供報告的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置與ProcessDataStorage配置選項中指定的位置相同 **根資料夾**.
   >
   >
   >如果更新ProcessDataStorage配置中的根資料夾選項，則必須更新ReportConfiguration服務中的CRX儲存路徑位置。

1. 按一下 **儲存** 關閉 **CQ Configuration Manager**.

### ProcessDataPublisher服務 {#processdatapublisher-service}

ProcessDataPublisher服務從AEM Forms資料庫導入進程資料，並將資料發佈到ProcessDataStorageProvider服務以進行儲存。

#### 配置ProcessDataPublisher服務   {#to-configure-processdatapublisher-service-nbsp}

1. 登入 **管理控制台** 具有管理員憑據。

   預設URL為 `https://'server':port]/adminui/`.

1. 導覽至 **首頁** > **服務** > **應用程式和服務** >**服務管理** 然後開啟 **ProcessDataPublisher** 服務。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**發佈資料**

啟用此選項可開始發佈流程資料。 依預設，會停用選項。

僅當與流程報告元件相關的所有配置都已正確設定時，才啟用流程報告。

或者，使用此選項可在不再需要流程資料發佈時禁用它。

`Default`: `Off`

**批時間間隔（秒）**

每次ProcessDataPublisher服務運行時，服務首先將自上次運行服務以來的時間按批時間間隔進行拆分。 然後，服務會分別處理AEM Forms資料的每個間隔，以協助控制發佈商在一個週期內每次執行（批次）期間端對端處理的資料大小。

例如，如果發佈者每天執行，則依預設，會將處理分為24個批次，每個批次1小時，而非在單一執行中處理一天的整個資料。

`Default`: `3600`

`Unit`: `Seconds`

**鎖定超時（秒）**

發佈者服務在開始處理資料時取得鎖，使發佈者的多個執行個體不會同時開始執行和處理資料。

如果已獲取鎖的發佈服務在「鎖超時」值定義的秒數內處於空閒狀態，則釋放其鎖，以便其他發佈服務實例可以繼續處理。

`Default`: `3600`

`Unit`: `Seconds`

**從發佈資料**

AEM Forms環境包含環境設定時的資料。

預設情況下，ProcessDataPublisher服務會從AEM Forms資料庫導入所有資料。

根據您的報表需求，如果您打算在特定日期和時間之後對資料執行報表和查詢，建議您指定日期和時間。 然後，發佈服務會從那時起發佈日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 訪問Process Reporting用戶介面 {#accessing-the-process-reporting-user-interface}

「程式報表」的使用者介面是以瀏覽器為基礎。

設定Process Reporting後，您就可以在AEM Forms安裝中的以下位置開始使用Process Reporting:

`https://<server>:<port>/lc/pr`

### 登入處理報告 {#log-in-to-process-reporting}

導覽至「程式報表」URL時(https://)&lt;server>:&lt;port>/lc/pr)，則顯示登錄螢幕。

若要登入「程式報表」模組，請指定您的憑證。

>[!NOTE]
>
>若要登入「程式報表」使用者介面，您需要下列AEM Forms權限：
>
>`PERM_PROCESS_REPORTING_USER`

![登入處理報告](assets/capture1_new.png)

登入「處理報告」時， **[!UICONTROL 首頁]** 畫面隨即顯示。

### 流程報告主螢幕 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**進程報告樹視圖：** 主螢幕左側的樹視圖包含「進程報告」模組的項。

樹視圖由以下頂級項目組成：

**報表：** 此項目包含隨流程報告一起提供的現成報表。

如需預先定義報表的詳細資訊，請參閱 [預先定義的在制報告](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**臨機查詢：** 此項目包含對流程和任務執行基於篩選的搜索的選項。

如需臨機查詢的詳細資訊，請參閱 [流程報告中的臨機查詢](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**自訂：** 「自訂」節點會顯示您建立的自訂報表。

有關建立和顯示自定義報告的過程，請參見 [自訂處理中報表](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**流程報告標題欄：** 「程式報表」標題列包含一些在使用者介面中工作時可使用的一般選項。

**流程報告標題：** 「程式報表」標題會顯示在標題列的左角。

隨時按一下標題，返回主畫面。

**上次更新時間：** 流程資料將按計畫從AEM Forms資料庫發佈到Process Reporting儲存庫。

「上次更新時間」顯示資料更新推送至流程報告儲存庫的最後日期和時間。

如需資料發佈服務及如何排程此服務的詳細資訊，請參閱 [計畫流程資料發佈](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) （位於「流程報告快速入門」一文中）。

**進程報告用戶：** 登入的使用者名稱會顯示在「上次更新」時間的右側。

**處理報表標題列下拉式清單：** 「流程報告」標題欄右角的下拉式清單包含下列選項：

* **[!UICONTROL 同步]**:將嵌入的Process Reporting儲存庫與AEM Forms資料庫同步。
* **[!UICONTROL 說明]**:查看有關流程報告的幫助文檔。
* **[!UICONTROL 登出]**:註銷進程報告
