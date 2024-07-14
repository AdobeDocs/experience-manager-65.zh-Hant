---
title: 開始使用程式報告
description: 開始使用JEE程式報告AEM Forms的步驟
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# 開始使用程式報告{#getting-started-with-process-reporting}

流程報表可讓AEM Forms使用者查詢目前在AEM Forms實作中定義的AEM Forms流程相關資訊。 不過，程式報告不會直接從AEM Forms存放庫存取資料。 資料會先以排程方式發佈到Process Reporting存放庫（*由ProcessDataPublisher和ProcessDataStorage服務*）。 接著，會從發佈至存放庫的「程式報告」資料產生「程式報告」中的報告和查詢。 程式報告會安裝為Forms Workflow模組的一部分。

本文詳細說明啟用將AEM Forms資料發佈到Process Reporting存放庫的步驟。 之後，您將能夠使用「程式報告」來執行報告和查詢。 本文也介紹可供設定「程式報告」服務的選項。

## 程式報告先決條件 {#process-reporting-pre-requisites}

### 永久刪除非必要處理 {#purge-non-essential-processes}

如果您目前使用Forms Workflow，AEM Forms資料庫可能會包含大量資料

Process Reporting發佈服務會發佈資料庫中目前可用的所有AEM Forms資料。 這表示，如果資料庫包含您不想執行報表和查詢的舊資料，即使報表不需要這些資料，也會將所有這些資料發佈到存放庫。 建議您在執行服務將資料發佈至Process Reporting儲存庫之前，先清除這些資料。 這麼做可以改善發佈者服務和查詢報表資料之服務的效能。

如需有關永久刪除AEM Forms程式資料的詳細資訊，請參閱[永久刪除程式資料](/help/forms/using/admin-help/purging-process-data.md)。

>[!NOTE]
>
>如需「清除公用程式」的提示與秘訣，請參閱有關[清除程式與工作](/help/forms/using/admin-help/purging-process-data.md)的Adobe Developer Connection文章。

## 設定程式Reporting Services {#configuring-process-reporting-services}

### 排程程式資料發佈 {#schedule-process-data-publishing}

Process Reporting服務會依排程從AEM Forms資料庫發佈資料至Process Reporting儲存庫。

這項作業相當耗用資源，且可能影響AEM Forms伺服器的效能。 建議您在AEM Forms伺服器忙碌時段以外排程此專案。

根據預設，資料的發佈排程為每天2:00 am執行。

若要變更發佈排程，請執行下列步驟：

>[!NOTE]
>
>如果您在叢集上執行AEM Forms實作，請在叢集的每個節點上執行下列步驟。

1. 停止AEM Forms伺服器執行個體。
1. &#x200B;URL

   * （適用於Windows）在編輯器中開啟`[JBoss root]/bin/run.conf.bat`檔案。
   * (適用於Linux®、AIX®和Solaris™) `[JBoss root]/bin/run.conf.sh`檔案在編輯器中。

1. 新增JVM引數`-Dreporting.publisher.cron = <expression>.`

   範例：以下cron運算式會導致Process Reporting每五小時將AEM Forms資料發佈到Process Reporting存放庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 儲存並關閉`run.conf.bat`檔案。

1. 重新啟動AEM Forms伺服器執行個體。

1. 停止AEM Forms伺服器執行個體。
1. 登入WebSphere®管理主控台。 在導覽樹狀結構中，按一下&#x200B;**伺服器** > **應用程式伺服器**，然後在右窗格中按一下伺服器名稱。

1. 在[伺服器基礎結構]下，按一下[™0}Java}和[處理程式管理]**> [處理程式定義]****。**

1. 在[其他內容]下，按一下[**Java™ Virtual Machine**]。

   在「一般JVM引數」方塊中，新增引數`-Dreporting.publisher.cron = <expression>.`

   **範例**：下列cron運算式導致Process Reporting每五小時將AEM Forms資料發佈到Process Reporting存放庫：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下[套用]****，按一下[確定]，然後按一下[直接儲存至主組態]**。**
1. 重新啟動AEM Forms伺服器執行個體。
1. 停止AEM Forms伺服器執行個體。
1. 登入WebLogic管理主控台。 WebLogic管理主控台的預設位址是`https://[hostname]:[port]/console`。
1. 在[變更中心]下，按一下[鎖定與編輯]。****
1. 在[網域結構]下，按一下[環境&#x200B;**] > [伺服器**] **，然後在右窗格中按一下[受管理的伺服器名稱]。**
1. 在下一個畫面中，按一下&#x200B;**組態**&#x200B;標籤> **伺服器啟動**&#x200B;標籤。
1. 在[引數]方塊中，新增JVM引數`-Dreporting.publisher.cron = <expression>`。

   **範例**：下列cron運算式導致Process Reporting每五小時將AEM Forms資料發佈到Process Reporting存放庫：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 按一下[儲存]****，然後按一下[啟動變更]****。
1. 重新啟動AEM Forms伺服器執行個體。

![processdatapublisherservice](assets/processdatapublisherservice.png)

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

### ProcessDataStorage服務 {#processdatastorage-service}

ProcessDataStorageProvider服務會從ProcessDataPublisher服務接收處理作業資料，並將資料儲存到Process Reporting儲存庫。

在每個發佈週期，資料都會儲存到預先定義的根資料夾的子資料夾中。

您可以使用管理主控台來設定用來儲存處理序資料的根（**預設**： `/content/reporting/pm`）位置和子資料夾（**預設**： `/yyyy/mm/dd/hh/mi/ss`）階層格式。

#### 設定「處理報告」存放庫位置 {#to-configure-the-process-reporting-repository-locations}

1. 使用系統管理員認證登入&#x200B;**管理主控台**。 管理主控台的預設URL為`https://'[server]:[port]'/adminui`
1. 導覽至&#x200B;**首頁** > **服務** > **應用程式及服務** >**服務管理**，然後開啟&#x200B;**ProcessDataStorageProvider**&#x200B;服務。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **根資料夾**

   儲存程式資料以供報告的CRX位置。

   `Default`: `/content/reporting/pm`

   **資料夾階層**

   根據流程建立時間儲存流程資料的資料夾階層。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 按一下「**儲存**」。

### ReportConfiguration服務 {#reportconfiguration-service}

Process Reporting會使用ReportConfiguration服務來設定程式報表查詢服務。

#### 設定ReportingConfiguration服務的方式 {#to-configure-the-reportingconfiguration-service}

1. 使用CRX系統管理員認證登入&#x200B;**組態管理員**。 組態管理員的預設URL為`https://'[server]:[port]'/lc/system/console/configMgr`
1. 開啟&#x200B;**ReportingConfiguration**&#x200B;服務。
1. **記錄數**

   對存放庫執行查詢時，結果可能包含許多記錄。 如果結果集很大，查詢執行可能會消耗伺服器資源。

   若要處理大型結果集，ReportConfiguration服務會將查詢處理分割成記錄批次。 這樣做會減少系統負載。

   `Default`: `1000`

   **CRX儲存路徑**

   要儲存程式資料以便進行報告的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置與ProcessDataStorage組態選項&#x200B;**根資料夾**&#x200B;中指定的位置相同。
   >
   >
   >如果您更新ProcessDataStorage設定中的Root Folder選項，則必須更新ReportConfiguration服務中的CRX Storage Path位置。

1. 按一下&#x200B;**儲存**&#x200B;並關閉&#x200B;**CQ Configuration Manager**。

### ProcessDataPublisher服務 {#processdatapublisher-service}

ProcessDataPublisher服務會從AEM Forms資料庫匯入處理作業資料，並將資料發佈至ProcessDataStorageProvider服務以進行儲存。

#### 若要設定ProcessDataPublisher服務   {#to-configure-processdatapublisher-service-nbsp}

1. 使用系統管理員認證登入&#x200B;**管理主控台**。

   預設URL為`https://'server':port]/adminui/`。

1. 導覽至&#x200B;**首頁** > **服務** > **應用程式與服務** >**服務管理**，然後開啟&#x200B;**ProcessDataPublisher**&#x200B;服務。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publish資料**

啟用此選項以開始發佈程式資料。 依預設，會停用選項。

只有在正確設定與「程式報告」元件相關的所有設定時，才啟用「程式報告」。

或者，當不再需要流程資料發佈時，也可以使用此選項來停用它。

`Default`: `Off`

**批次間隔（秒）**

每次ProcessDataPublisher服務執行時，服務都會先依批次間隔分割自上次執行服務以來的時間。 然後，該服務會分別處理每個AEM Forms資料間隔，以幫助控制發佈者在一個週期內每次執行（批次）時端對端處理的資料大小。

例如，如果發佈程式每天執行，則預設會將處理分為24個批次，每個批次各一個小時，而不是以單一執行處理一天的所有資料。

`Default`: `3600`

`Unit`: `Seconds`

**鎖定逾時（秒）**

發行者服務會在開始處理資料時取得鎖定，這樣發行者的多個執行個體就不會同時開始執行及處理資料。

如果已取得鎖定的發行者服務在「鎖定逾時」值所定義的秒數內閒置，則會釋放其鎖定，讓其他發行者服務執行個體可以繼續處理。

`Default`: `3600`

`Unit`: `Seconds`

**來自**&#x200B;的Publish資料

AEM Forms環境包含設定環境時的資料。

依預設，ProcessDataPublisher服務會從AEM Forms資料庫匯入所有資料。

根據您的報告需求，如果您打算在特定日期和時間之後對資料執行報告和查詢，建議您指定日期和時間。 發佈服務接著會發佈該時間之後的日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 存取「程式報表」使用者介面 {#accessing-the-process-reporting-user-interface}

「程式報告」的使用者介面是以瀏覽器為基礎。

設定「程式報告」後，您就可以開始在AEM Forms安裝的下列位置使用「程式報告」：

`https://<server>:<port>/lc/pr`

### 登入程式報告 {#log-in-to-process-reporting}

當您導覽至「程式報表」URL (https://&lt;server>：&lt;port>/lc/pr)時，畫面會顯示登入畫面。

若要登入「程式報告」模組，請指定您的認證。

>[!NOTE]
>
>若要登入「程式報告」使用者介面，您需要下列AEM Forms許可權：
>
>`PERM_PROCESS_REPORTING_USER`

![登入程式報告](assets/capture1_new.png)

當您登入「程式報告」時，會顯示&#x200B;**[!UICONTROL 首頁]**&#x200B;畫面。

### 程式報告首頁畫面 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**程式報告樹狀檢視：**&#x200B;主畫面左側的樹狀檢視包含[程式報告]模組的專案。

樹狀結構檢視包含下列最上層專案：

**報告：**&#x200B;此專案包含隨程式報告提供的現成報告。

如需預先定義報表的詳細資訊，請參閱[程式報表中的預先定義報表](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)。

**臨機查詢：**&#x200B;此專案包含用於執行以篩選為基礎的程式與工作的選項。

如需特定查詢的詳細資訊，請參閱[程式報表中的特定查詢](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**自訂：**&#x200B;自訂節點會顯示您建立的自訂報表。

如需建立及顯示自訂報表的程式，請參閱[處理中的自訂報表](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**程式報告標題列：**&#x200B;程式報告標題列包含一些一般選項，您可以在使用者介面中使用這些選項。

**程式報告標題：**&#x200B;程式報告標題會顯示在標題列的左角。

隨時按一下標題以返回首頁畫面。

**上次更新時間：**&#x200B;處理序資料會依排程從AEM Forms資料庫發佈至Process Reporting存放庫。

「上次更新時間」會顯示資料更新已推送至「程式報表」存放庫的上次日期與時間。

如需資料發佈服務以及如何排程此服務的詳細資訊，請參閱「程式報告快速入門」一文中的[排程程式資料發佈](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p)。

**處理序報告使用者：**&#x200B;登入的使用者名稱會顯示在上次更新時間的右側。

**程式報告標題列下拉式清單：**&#x200B;程式報告標題列右角的下拉式清單包含下列選項：

* **[!UICONTROL 同步]**：將內嵌的Process Reporting儲存庫與AEM Forms資料庫同步。
* **[!UICONTROL 說明]**：檢視程式報告的說明檔案。
* **[!UICONTROL 登出]**：登出程式報告


