---
title: 監控和維護您的AEM實例
seo-title: 監控和維護您的AEM實例
description: 瞭解如何監控AEM。
seo-description: 瞭解如何監控AEM。
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# 監控和維護您的AEM實例{#monitoring-and-maintaining-your-aem-instance}

在您的AEM例項部署後，將需要某些工作來監控和維護其運作、效能和完整性。

這裡的一個關鍵因素是，要識別潛在問題，您需要瞭解系統在正常條件下的外觀和行為。 最好的做法是監控系統，並在一段時間內收集資訊。

| 檢查 | 考量事項 | 注釋／動作 |
|---|---|---|
| 備份計畫。 |  | 瞭解如何 [備份實例](/help/sites-deploying/monitoring-and-maintaining.md#backups)。 |
| 災難恢復計畫。 | 貴公司的災難恢復指導方針。 |  |
| 錯誤追蹤系統可用於報告問題。 | 例如， [bugzilla](https://www.bugzilla.org/)、 [jira](https://www.atlassian.com/software/jira/)，或其他眾多。 |  |
| 正在監視檔案系統。 | 如果可用磁碟空間不足，CRX儲存庫將「凍結」。 當空間可用時，它將恢復。 | 當可 `*ERROR* LowDiskSpaceBlocker`用空間變低時，可以在日誌檔案中看到「 」消息。 |
| [正在監視日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 。 |  |  |
| 系統監控（持續）在後台運行。 | 包括CPU、記憶體、磁碟和網路使用。 例如，使用iostat / vmstat / perfmon。 | 記錄的資料是可視化的，可用於追蹤效能問題。 您也可存取原始資料。 |
| [AEM效能受到監控](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)。 | 包含 [請求計數器](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) ，以監控流量等級。 | 如果出現嚴重或長期的業績損失，應進行詳細調查。 |
| 您正在監視您的 [複製代理](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)。&quot; |  |  |
| 定期清除工作流程例項。 | 儲存庫大小和工作流效能。 | 請參 [閱定期清除工作流實例](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。 |

## 備份 {#backups}

執行以下備份是一個好做法：

* 您的軟體安裝——在配置發生重大更改之前／之後
* 存放在儲存庫中的內容——定期

您的公司可能會有需要遵循的備份策略、備份內容以及備份時間的其他考慮：

* 系統和資料的重要性。
* 軟體或資料的變更頻率。
* 資料量；容量有時可能是問題，執行備份所需的時間也是問題。
* 用戶線上時，是否可以進行備份；如果可能，效能影響將是什麼。
* 用戶的地域分佈；例如，何時是備份的最佳時間（以最大限度地減少影響）?
* 您的災難恢復政策；是否有必要儲存備份資料的指導原則（如離站、特定介質等）。

通常，完整備份會定期執行（例如每日、每週或每月），增量備份介於之間（例如每小時、每日或每週）。

>[!CAUTION]
>
>實施生產實例的備份時，必 *須進行測試* ，以確保能夠成功恢復備份。

>如果沒有這一點，備份可能無用（最壞的情況）。
>
>[!NOTE]
有關備份效能的詳細資訊，請閱讀「備 [份效能](/help/sites-deploying/configuring-performance.md#backup-performance) 」部分。

### 備份軟體安裝 {#backing-up-your-software-installation}

在安裝後，或在配置中進行重大更改後，備份軟體安裝。

為此，您需要備份整 [個儲存庫](#backing-up-your-repository) ，然後：

1. 停止AEM。
1. 從檔案系統 `<cq-installation-dir>` 備份整個。

>[!CAUTION]
如果您正在操作第三方應用程式伺服器，則其他資料夾可能位於不同的位置，也可能需要備份。 如需 [有關安裝應用程式伺服器的詳細資訊，請參閱如何與應用程式伺服器一起安裝AEM](/help/sites-deploying/application-server-install.md) 。 [](/content/docs/en/aem/6-3/deploy/installing.md#將adobe experience Manager與應用程式伺服器一起安裝)

>[!CAUTION]
支援檔案資料儲存的增量備份；對其他元件（如Lucene索引）使用增量備份時，請確保在備份中也將已刪除的檔案標籤為已刪除。

>[!NOTE]
磁碟鏡像也可用作備份機制。

### 備份儲存庫 {#backing-up-your-repository}

CRX文 [檔的「備份和還原](/help/sites-administering/backup-and-restore.md) 」部分涵蓋與CRX儲存庫備份相關的所有問題。

有關建立線上「熱」備份的完整詳細資訊，請參 [閱建立線上備份](/help/sites-administering/backup-and-restore.md#online-backup)。

## 版本清除 {#version-purging}

清除 **版本工具** ，用於清除儲存庫中節點版本或節點層次結構。 其主要用途是通過刪除節點的舊版本來幫助您減小儲存庫的大小。

本節討論與AEM版本控制功能相關的維護作業。 清 **除版本** (Purge Version)工具用於清除儲存庫中節點的版本或節點層次。 其主要用途是通過刪除節點的舊版本來幫助您減小儲存庫的大小。

### 概覽 {#overview}

「清 **除版本** 」工具可在「工具」控制台的「版本控制」下使用，或直接在下 **[列位置](/help/sites-administering/tools-consoles.md)******:

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**開始路徑** ：必須執行清除的絕對路徑。 按一下儲存庫樹導航器可以選擇「開始路徑」。

**遞歸** ：在清除資料時，可通過選擇遞歸，在一個節點上或整個層次上執行操作。 在最後一種情況下，給定路徑定義了層次的根節點。

**要保留的最大版本** ：節點要保留的最大版本數。 當這些數字超過此值時，會清除最舊的版本。

**最大版本** ：節點版本的最大版本。 當版本的年齡超過此值時，會清除它。

**乾式執行** ：由於移除內容的版本是確定的，而且在不還原備份的情況下無法還原，因此「清除版本」工具提供乾式執行模式，允許您預覽已清除的版本。 要啟動清除流程的乾式運行，請按一下「乾式運行」。

**清除** ：啟動清除由「開始路徑」定義的節點上的版本。

### 清除網站版本 {#purging-versions-of-a-web-site}

要清除網站版本，請按如下步驟進行：

1. 導覽至「工 **[具](/help/sites-administering/tools-consoles.md)**」控&#x200B;**制台**，選取「版本&#x200B;**修訂**」並按兩下「清&#x200B;**除版本」。**
1. 設定要清除之內容的開始路徑(例如 `/content/geometrixx-outdoors`)。

   * 如果只想清除路徑定義的節點，請取消選擇「遞 **歸」**。
   * 如果要清除路徑定義的節點及其子代，請選擇「遞 **歸」**。

1. 設定您要保留的最大版本數（每個節點）。 留空以不使用此設定。

1. 設定您要保留的最大版本年齡（針對每個節點），以天為單位。 留空以不使用此設定。

1. 按一下 **「乾式運行** 」(Dry Run)以預覽清除過程的作用。
1. 按一下 **清除** ，啟動流程。

>[!CAUTION]
如果不還原儲存庫，則無法還原已清除的節點。 您應該處理配置，因此建議您在清除前始終執行乾式運行。

### 分析控制台 {#analyzing-the-console}

「乾 **式運行** 」和「清 **除** 」進程將列出所有已處理的節點。 在過程中，節點可以具有以下狀態之一：

* `ignore (not versionnable)`:該節點不支援版本控制，並在處理過程中被忽略。

* `ignore (no version)`:該節點沒有任何版本，在進程中將被忽略。&quot;

* `retained`:不清除該節點。
* `purged`:節點將被清除。

此外，主控台還提供版本的有用資訊：

* `V 1.0`:版本號。
* `V 1.0.1`*:星號表示版本為當前版本。

* `Thu Mar 15 2012 08:37:32 GMT+0100`:版本的日期。

在下一個範例中：

* The **Thirts** versions are purged are grepted are their version ager that 2 days.
* 東加 **時尚界！** 版本會被清除，因為其版本數大於5。

![global_version_screenshot](assets/global_version_screenshot.png)

## 使用審計記錄和日誌檔案 {#working-with-audit-records-and-log-files}

您可以在不同位置找到與Adobe Experience Manager(AEM)相關的稽核記錄和記錄檔。 以下提供您可在何處找到的概觀。

### 使用日誌 {#working-with-logs}

AEM WCM會記錄詳細記錄檔。 開啟包裝並啟動Quickstart後，您可以找到以下日誌：

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 日誌檔案旋轉 {#log-file-rotation}

日誌檔案旋轉是指通過定期建立新檔案來限制檔案增長的過程。 在AEM中，呼叫的記錄檔 `error.log` 將會根據指定規則每天旋轉一次：

* 檔 `error.log` 案會根據模式{original_filename}重新命名 `.yyyy-MM-dd`。 例如，在2010年7月11日，目前的記錄檔會重新命 `error.log-2010-07-10`名，然後建立 `error.og` 新的檔案。

* 以前的日誌檔案不會刪除，因此您有責任定期清除舊日誌檔案以限制磁碟使用。

>[!NOTE]
如果您升級AEM安裝，請注意，AEM不再使用的任何現有記錄檔都將保留在磁碟中。 您可以不冒險地移除它們。 所有新日誌條目都將寫入新日誌檔案中。

### 查找日誌檔案 {#finding-the-log-files}

安裝AEM的檔案伺服器上會保留各種記錄檔：

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
AEM WCM和儲存庫的所有存取要求都會在此處註冊。

   * `audit.log`
協調動作會在此處註冊。

   * `error.log`
此處會註冊錯誤消息（嚴重性級別不同）。

   * [ 只 `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_image_server_log.html)有在啟用動態媒體時才使用此記錄檔。 它提供用於分析內部ImageServer進程行為的統計和分析資訊。

   * `request.log`
每個存取請求都會在此與回應一起註冊。

   * [ 只 `s7access-<yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_Access_Log.html)有在啟用動態媒體時才使用此記錄檔。 s7access記錄透過和記錄對動態媒體提出的每個 `/is/image` 要求 `/is/content`。

   * `stderr.log`
保存在啟動期間生成的、嚴重性級別不同的錯誤消息。 根據預設，記錄層級設 `Warning` 為( `WARN`)

   * `stdout.log`
保存指示啟動期間事件的日誌消息。

   * `upgrade.log`
提供從和軟體包運行的所有升級操作的 `com.day.compat.codeupgrade` 日 `com.adobe.cq.upgradesexecutor` 志。

* `<*cq-installation-dir*>/crx-quickstart/repository`

   * `revision.log`
修訂日誌資訊。

>[!NOTE]
ImageServer和s7access記錄檔不包含在**下載完整**套件中，此套件是從**system/console/status-Bundlelist **頁面產生。 為了支援，如果您有動態媒體問題，請在聯絡客戶支援時附加ImageServer和s7access記錄檔。

### 啟用DEBUG日誌級別 {#activating-the-debug-log-level}

預設記錄層級([Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration))為資訊，因此不記錄除錯訊息。

要激活Logger的調試日誌級別，請將屬性設定為 `org.apache.sling.commons.log.level` 在儲存庫中調試。 例如，在上 `/libs/sling/config/org.apache.sling.commons.log.LogManager` 設定全 [域Apache Sling記錄](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)。

>[!CAUTION]
請勿將日誌保留在調試日誌級別，因為它會生成大量日誌條目，因而佔用資源。

除錯檔案中的一行通常以DEBUG開頭，然後提供記錄檔層級、安裝程式動作和記錄檔訊息。 例如：

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日誌級別如下：

| 0 | 致命錯誤 | 動作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作失敗。 安裝會繼續，但AEM WCM的部分安裝不正確，因此無法運作。 |
| 2 | 警告 | 行動成功，但遇到問題。 AEM WCM可能無法正常運作。 |
| 3 | 資訊 | 動作成功。 |

### 建立自訂記錄檔 {#create-a-custom-log-file}

>[!NOTE]
使用Adobe Experience manager時，有幾種方法可管理此類服務的組態設定；如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

在某些情況下，您可能希望建立具有不同日誌級別的自定義日誌檔案。 您可以通過以下方式在儲存庫中執行此操作：

1. 如果尚未存在，請為您的項目建立新的配 `sling:Folder`置資料夾() `/apps/<*project-name*>/config`。
1. 在 `/apps/<*project-name*>/config`下，為新的 [Apache Sling Logging Logger Configuration建立節點](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration):

   * 名稱： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (as this is a Logger)

      其中 `<*identifier*>` 由您（必須）輸入以標識實例的自由文本替換（您不能忽略此資訊）。

      例如， `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 類型: `sling:OsgiConfig`
   >[!NOTE]
   雖然不是技術要求，但最好是獨一無 `<*identifier*>` 二。

1. 在此節點上設定以下屬性：

   * 名稱: `org.apache.sling.commons.log.file`

      類型：字串

      值：指定日誌檔案；例如， `logs/myLogFile.log`

   * 名稱: `org.apache.sling.commons.log.names`

      類型：字串[] （字串+多重）

      值：指定Logger要記錄訊息的OSGi services;例如，以下所有項目：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名稱: `org.apache.sling.commons.log.level`

      類型：字串

      值：指定所需的日誌級 `debug`別( `info`、 `warn` 或 `error`);例如 `debug`

   * 視需要設定其他參數：

      * 名稱: `org.apache.sling.commons.log.pattern`

         類型: `String`

         值：根據需要指定日誌消息的模式；例如，

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   `org.apache.sling.commons.log.pattern` 最多支援6個引數。

   >{0}類型的時間戳記 `java.util.Date`{1}記錄標籤{2}目前執行緒的名稱{3}記錄器{4}、記錄層級{5}和記錄訊息

   >如果日誌調用包含 `Throwable` 堆棧跟蹤，則附加到消息。

   >[!CAUTION]
   org.apache.sling.commons.log.names必須有值。

   >[!NOTE]
   日誌寫入器路徑與位置相 `crx-quickstart` 對。
   因此，日誌檔案指定為：
   `logs/thelog.log`

   >寫入：
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`。
   以及指定為：
   `../logs/thelog.log`

   >寫入目錄：
   ` <*cq-installation-dir*>/logs/`
&quot;(即&lt; ` `cq-installation-dir *>/*`crx-quickstart/`)

1. 只有在需要新寫入器時（即配置與預設寫入器不同），才需要此步驟。

   >[!CAUTION]
   只有當現有預設值不適合時，才需要新的記錄寫入器配置。

   >如果未配置顯式寫入器，系統將根據預設自動生成隱式寫入器。

   在下 `/apps/<*project-name*>/config`方，為新的 [Apache Sling Logging Writer Configuration建立節點](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration):

   * 名稱： `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` （因為這是作家）

      與Logger一樣， `<*identifier*>` 由您（必須）enter用來識別實例的自由文本（您不能忽略此資訊）替換。 例如， `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 類型: `sling:OsgiConfig`
   >[!NOTE]
   雖然不是技術要求，但最好是獨一無 `<*identifier*>` 二。

   在此節點上設定以下屬性：

   * 名稱: `org.apache.sling.commons.log.file`

      類型: `String`

      值：指定Log File，使其與Logger；中指定的檔案匹配

      例如， `../logs/myLogFile.log`。

   * 視需要設定其他參數：

      * 名稱: `org.apache.sling.commons.log.file.number`

         類型: `Long`

         值：指定要保留的日誌檔案數；例如， `5`

      * 名稱: `org.apache.sling.commons.log.file.size`

         類型: `String`

         值：指定依大小／日期控制檔案旋轉；例如， `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` 通過設定以下任一設定控制日誌檔案的旋轉：
   * 最大檔案大小
   * 時間／日期計畫
   以指示何時將建立新檔案（並根據名稱模式更名現有檔案）。
   * 可以用數字指定大小限制。 如果沒有提供大小指示器，則此指示器被視為位元組數，或者您可以添加一個大小指示器- `KB`、 `MB`或 `GB` （忽略大小寫）。
   * 時間／日期排程可指定為模 `java.util.SimpleDateFormat` 式。 這定義了檔案旋轉的時段；也附加到旋轉檔案的字尾（用於識別）。
   預設值為&#39;.&#39;。yyyy-MM-dd（用於每日日誌旋轉）。
   例如，在2010年1月20日的午夜（或當發生此事後的第一個記錄訊息時，請務必精確）,../logs/error.log將重新命名為../logs/error.log.2010-01-20。 1月21日的記錄將輸出為（新的和空的）../logs/error.log，直到在下一天的變更時滾動。
       | `&#39;.&#39;
    yyyy-MM`|每月初的輪值|
 |—|—|     | &#39;&#39;。&#39;yyyy-ww`|每週第一天的旋轉（視地區而定）。 |
       | `&#39;.&#39;yyyy-MM-dd`每天午夜時輪流。 |
       | `&#39;.&#39;yyyy-MM-dd-a`在每天的午夜和中午旋轉。 |
       | `&#39;.&#39;yyyy-MM-dd-HH`每小時最上方的旋轉。 |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm`每分鐘開始時輪流。 
 |    
     
Note:指定時間／日期時：      1. 
 您應「逸出」一對單引號(&#39; &#39;)中的常值文字；  這     是為了避免某些字元被解譯為圖樣字母。
       1. 在選項中的任何位置，僅允許使用有效檔案名的字元。
   

1. 使用您選擇的工具讀取您的新記錄檔。

   由此示例建立的日誌檔案將為 `../crx-quickstart/logs/myLogFile.log`。

Felix Console也提供Sling Log Support的相關資訊，網址為 `../system/console/slinglog`;例如 `https://localhost:4502/system/console/slinglog`。

### 查找審計記錄 {#finding-the-audit-records}

會保存審計記錄，以記錄誰在何時執行了什麼。 AEM WCM和OSGi事件都會產生不同的稽核記錄。

#### AEM WCM審核記錄在頁面編寫時顯示 {#aem-wcm-audit-records-shown-when-page-authoring}

1. 開啟頁面。
1. 從側鏈中，您可以選取具有鎖定圖示的標籤，然後連按兩下「 **稽核記錄……」**
1. 將會開啟一個新視窗，顯示目前頁面的稽核記錄清單。

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 當您 **要關閉視窗** 時，按一下「確定」。

#### AEM WCM資料庫中的稽核記錄 {#aem-wcm-auditing-records-within-the-repository}

在資料夾 `/var/audit` 中，會根據資源保存審計記錄。 您可以深入探究，直到您看到個別記錄及其所包含的資訊為止。

這些條目包含的資訊與編輯頁面時顯示的資訊相同。

#### OSGi Audit records from the Web Console {#osgi-audit-records-from-the-web-console}

OSGi事件也會產生稽核記錄，您可從AEM Web Console的「 **Configuration Status** 」（設定狀態）標籤-> **Log Files **tab中看到這些記錄：

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 監視複製代理 {#monitoring-your-replication-agents}

您可以監視復 [制隊列](/help/sites-deploying/replication.md) ，以檢測隊列是關閉還是被阻止的時間——這反過來又可能表示發佈實例或外部系統有問題：

* 所有必要的隊列都啟用了嗎？
* 是否仍然需要任何禁用的隊列？
* 所有 `enabled` 隊列都應具有狀態 `idle` 或 `active`，這表示正常操作；不應該有隊 `blocked`伍，這通常是接收方出現問題的一個跡象。

* 如果隊列的大小隨著時間而增加，這可能表示已阻止的隊列。

要監視複製代理，請執行以下操作：

1. 存取AEM中 **的** 「工具」索引標籤。
1. 按一下 **複製**。
1. 連按兩下適當環境（左窗格或右窗格）的代理連結；例如， **作者上的代理**。

   生成的窗口顯示了作者環境的所有複製代理的概述，包括其目標和狀態。

1. 按一下相應的代理名（即連結）以顯示有關該代理的詳細資訊：

   ![chlimage_1](assets/chlimage_1.jpeg)

   您可以：

   * 查看是否啟用了代理。
   * 查看任何複製的目標。
   * 查看複製隊列當前是否處於活動狀態（已啟用）。
   * 瞭解佇列中是否有任何項目。
   * **刷新** 或 **清除** ，更新隊列條目的顯示；這可協助您查看項目進入並離開佇列。

   * **查看日誌** ，以訪問複製代理所執行的任何操作的日誌。
   * **測試與目標實例的連接** 。
   * **如有需要** ，請對任何佇列項目強制重試。
   >[!CAUTION]
   請勿在發佈實例的「反向複製輸出」框中使用「測試連接」連結。
   如果對Outbox隊列執行複製測試，則所有早於測試複製的項目都將通過每個反向複製重新處理。
   如果此類項目已存在於隊列中，則可使用以下XPath JCR查詢找到，並應將其刪除。
   `/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

同樣，您可以開發一個解決方案來檢測所有複製代理(位於 `/etc/replication/author` 或 `/etc/replication/publish`)，然後檢查代理( `enabled`, `disabled`)和基礎隊列(、、 `active`、 `idle``blocked`)的狀態。

## 監控效能 {#monitoring-performance}

[效能最佳化](/help/sites-deploying/configuring-performance.md) (Performance Optimization)是互動式程式，在開發過程中會受到重視。 在部署後，通常會在特定間隔或事件後進行審查。

在收集資訊以進行優化時使用的方法也可以用於進行中的監控。

>[!NOTE]
還可 [以檢查可用於提高效能](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 的特定配置。

以下列出發生的常見效能問題，以及如何找出和抵消這些問題的建議。

| 區域 | 症狀 | 要提高容量…… | 要減少卷…… |
|---|---|---|---|
| 用戶端 | 用戶端CPU使用量高。 | 安裝效能更高的客戶端CPU。 | 簡化(HTML)版面。 |
|  | 伺服器CPU使用量低。 | 升級至更快速的瀏覽器。 | 改善用戶端快取。 |
|  | 有些客戶速度快，有些客戶速度慢。 |  |  |
| 伺服器 |  |  |  |
| 網路 | 伺服器和客戶端的CPU使用率都較低。 | 消除網路瓶頸。 | 改進／優化客戶機快取的配置。 |
|  | （相對而言）在伺服器上本機瀏覽的速度較快。 | 增加網路頻寬。 | 降低網頁的「重量」（例如，影像較少、最佳化HTML）。 |
| Web伺服器 | 網頁伺服器上的CPU使用量很高。 | 叢集您的Web伺服器。 | 減少每頁點擊（瀏覽）。 |
|  |  | 使用硬體負載平衡器。 |  |
| 應用程式 | 伺服器CPU使用量很高。 | 叢集您的AEM例項。 | 搜尋並消除CPU和記憶體記憶體記憶體記憶體記憶體記憶體記憶體（使用程式碼檢閱、計時輸出等）。 |
|  | 高記憶體消耗。 |  | 改善所有層級的快取。 |
|  | 回應時間較短。 |  | 最佳化範本和元件（例如結構、邏輯）。 |
| 存放庫 |  |  |  |
| 快取 |  |  |  |

效能問題可能源自許多與您網站無關的原因，包括連線速度的暫時慢速、CPU負載等。

此外，它也可能會影響您的所有訪客，或僅影響其中的子集。

您必須先取得、排序和分析所有這些資訊，才能最佳化整體效能或解決特定問題。

* 在遇到效能問題之前：

   * 收集盡可能多的資訊，以建立正常情況下系統的良好工作知識

* 當您遇到效能問題時：

   * 嘗試在您知道具有良好一般效能的不同用戶端上，使用一種（或更好）標準網頁瀏覽器複製它，以及（如果可能）在伺服器本身複製它
   * 檢查是否在適當的時間空間內有任何變更（與系統相關），以及這些變更中是否有可能影響效能
   * 提出以下問題：

      * 問題是否只發生在特定時間？
      * 問題是否只發生在特定頁面上？
      * 其他請求是否受到影響？
   * 收集盡可能多的資訊，以便與您在正常情況下的系統知識進行比較：


### 監控和分析效能的工具 {#tools-for-monitoring-and-analyzing-performance}

以下簡要概述了一些可用於監視和分析效能的工具。

其中一些將取決於您的作業系統。

<table>
 <tbody>
  <tr>
   <td>工具</td>
   <td>用於分析……</td>
   <td>使用／詳細資訊……</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>回應時間與並行處理。</td>
   <td><a href="#interpreting-the-request-log">解讀request.log</a>。</td>
  </tr>
  <tr>
   <td>桁架／桁架</td>
   <td>頁面載入</td>
   <td><p>用於跟蹤系統調用和信號的Unix/Linux命令。 將日誌級別提高到 <code>INFO</code>。</p> <p>分析每個請求的頁面載入次數，以及哪些頁面等。</p> </td>
  </tr>
  <tr>
   <td>線程轉儲</td>
   <td>觀察JVM線程。 識別競爭、鎖定和長跑者。</td>
   <td><p><br /> 取決於作業系統：- Unix/Linux: <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows（控制台模式）:Ctrl-Break<br /> </p> <p>也提供分析工具，例如 <a href="https://java.net/projects/tda/">TDA</a>。<br /> </p> </td>
  </tr>
  <tr>
   <td>堆轉儲</td>
   <td>記憶體不足導致效能降低。</td>
   <td><p><br /> 新增： <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> 的Java呼叫。</p> <p>請參 <a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">閱Java SE 6 with HotSpot VM的故障排除指南</a>。</p> </td>
  </tr>
  <tr>
   <td>系統呼叫</td>
   <td>識別時間問題。</td>
   <td><p>呼叫或 <code>System.currentTimeMillis()</code> . <code>com.day.util</code>Timing會用來從程式碼或透過 <a href="#html-comments">HTML-comments產生時間戳記</a>。</p> <p><strong></strong> 注意：這些應該實施，以便根據需要激活／停用；當系統運行順利時，不需要收集統計資訊的開銷。</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>識別記憶體洩漏，選擇性分析回應時間。</td>
   <td><p>基本用法為：</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>有關 <a href="#apache-bench">完整詳細資訊</a> ，請參 <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">見Apache Bench和ab手冊頁</a> 。</p> </td>
  </tr>
  <tr>
   <td>搜尋分析</td>
   <td> </td>
   <td>離線執行搜尋查詢，識別查詢的回應時間，測試並確認結果集。<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>負載和功能測試。</td>
   <td><a href="https://jakarta.apache.org/jmeter/">https://jakarta.apache.org/jmeter/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>深入分析CPU和記憶體。</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>觀察JVM度量和線程。</td>
   <td><p>用法：jconsole</p> <p>請參 <a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">閱使用JConsole</a><a href="#monitoring-performance-using-jconsole">的jconsole和監視效能</a>。</p> <p><strong></strong> 注意：在JDK 1.6中，JConsole可以通過插件進行擴展；例如，Top或TDA（線程轉儲分析器）。</p> </td>
  </tr>
  <tr>
   <td>Java visualVM</td>
   <td>觀察JVM度量、線程、記憶體和分析。</td>
   <td><p>用法：jvisualvm或visualvm<br /> </p> <p>請參 <a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">閱使用(J)VisualVM</a>、 <a href="https://visualvm.dev.java.net/">visualvm</a><a href="#monitoring-performance-using-j-visualvm">和監控效能</a>。</p> <p><strong></strong> 注意：使用JDK 1.6,VisualVM可以通過插件進行擴展。</p> </td>
  </tr>
  <tr>
   <td>桁架／網架，lsof</td>
   <td>深入瞭解內核調用和進程分析(Unix)。</td>
   <td>Unix/Linux命令。</td>
  </tr>
  <tr>
   <td>計時統計資料</td>
   <td>請參閱頁面演算的時間統計資料。</td>
   <td><p>若要查看頁面演算的時間統計資料，您可 <strong>搭配使用Ctrl-Shift</strong> -U <code>?debugClientLibs=true</code> 和URL中的設定。</p> </td>
  </tr>
  <tr>
   <td>CPU和記憶體分析工具<br /> </td>
   <td><a href="#interpreting-the-request-log">用於分析開發期間的慢速請求</a>。</td>
   <td>例如， <a href="https://www.yourkit.com/">YourKit</a>。</td>
  </tr>
  <tr>
   <td><a href="#information-collection">資訊收集</a></td>
   <td>安裝的持續狀態。</td>
   <td>盡可能瞭解您的安裝，也有助於您追蹤可能導致效能變更的原因，以及這些變更是否合理。 這些量度需要定期收集，以便您輕鬆看到重大變更。</td>
  </tr>
 </tbody>
</table>

### 解讀request.log {#interpreting-the-request-log}

此檔案會註冊對AEM提出每個要求的基本資訊。 從中可以得出有價值的結論。

本 `request.log` 軟體提供內建方式，讓您瞭解要求需要多長時間。 為了開發目的，它對於 `tail -f` 和觀 `request.log` 察響應速度很有用。 若要分析更 `request.log` 大的項目， [我們建 `rlog.jar` 議您使用它來排序和篩選回應時間](#using-rlog-jar-to-find-requests-with-long-duration-times)。

我們建議將「慢速」頁面與頁面隔離 `request.log`，然後個別調整頁面以獲得更佳的效能。 這通常是透過為每個元件加入效能量度或使用效能分析工具（例如）來完成 ` [yourkit](https://www.yourkit.com/)`。

#### 監控您網站上的流量 {#monitoring-traffic-on-your-website}

請求記錄會註冊每個發出的請求，以及作出的回應：

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

透過在特定時段內（例如在不同的24小時時段內）匯總所有GET項目，您可以對網站的平均流量做出陳述。

#### 使用request.log監控回應時間 {#monitoring-response-times-with-the-request-log}

效能分析的好起點是請求記錄：

`<*cq-installation-dir*>/crx-quickstart/logs/request.log`

日誌如下所示（為了簡單起見，會縮短行數）:

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

此記錄檔每個請求或回應有一行：

* 提出每個請求或回應的日期。
* 請求數，以方括弧表示。 此數字元合請求和回應。
* 箭頭，指出這是請求（指向右箭頭）或回應（向左箭頭）。
* 對於請求，行包含：

   * 方法（通常為GET、HEAD或POST）
   * 要求的頁面
   * 協定

* 對於回應，行包含：

   * 狀態碼（200表示「success」,404表示「page not found」）
   * MIME類型
   * 響應時間

使用小指令碼，您可以從記錄檔擷取所需資訊，並組合所需的統計資料。 從這些頁面中，您可以看到哪些頁面或類型的頁面速度緩慢，以及整體效能是否令人滿意。

#### 使用request.log監控搜尋回應時間 {#monitoring-search-response-times-with-the-request-log}

搜尋請求也會在記錄檔中註冊：

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

因此，如上所述，您可以使用指令碼來擷取相關資訊並建立統計資料。

不過，一旦您確定回應時間，您可能需要分析請求花費的時間，以及可以採取哪些措施來改善回應。

#### 監控併發用戶的數量和影響 {#monitoring-the-number-and-impact-of-concurrent-users}

同樣地， `request.log` 還可以用於監視併發以及系統對它的反應。

必須進行測試，以判斷系統可處理的並行使用者數，才會看到負面影響。 Again scripts can be used to extract results from the log file:

* 監控特定時段（例如一分鐘）內發出的請求數
* 測試特定數量的使用者同時提出相同要求（盡可能接近）的效果；例如，30位使用者同時按 **一下** 「儲存」。

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### 使用rlog.jar查找持續時間較長的請求 {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM包含各種協助工具，位於：
`<*cq-installation-dir*>/crx-quickstart/opt/helpers`

其中一項可 `rlog.jar`用來快速排序， `request.log` 讓請求依持續時間顯示，從最長到最短。

以下命令顯示可能的參數：

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

例如，您可以執行它，指 `request.log` 定檔案為參數，並顯示持續時間最長的10個前1個請求：

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

如果您需要對大型資料范 `request.log` 例執行此作業，則可能需要串連個別檔案。

### Apache Bench {#apache-bench}

為了將特殊情況（如垃圾回收等）的影響降至最低，建議使用例如 `apachebench` (如需進一步說明檔案，請參閱 [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) )的工具，以協助識別記憶體洩漏並選擇性地分析回應時間。

Apache Bench可以通過以下方式使用：

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

上述數字取自可存取geometrixx公司頁面的標準MAcBook pro筆記型電腦（2010年中），如預設AEM安裝所示。 頁面非常簡單，但未針對效能最佳化。

`apachebench` 也會以平均方式顯示每個請求的時間，以涵蓋所有併發請求；請參 `Time per request: 54.595 [ms]` 閱（平均值，涵蓋所有並行請求）。 您可以變更並行參數的值( `-c` 一次要執行多個請求數)，以查看任何效果。

### 請求計數器 {#request-counters}

請求流量的相關資訊（特定時段內的請求數）會提供您例項負載的指示。 這項資訊可從 [request.log中擷取](#interpreting-the-request-log)，不過使用計數器會自動收集資料，讓您看到：

* 活動的顯著差異（即區分「許多要求」和「低活動」）
* 不使用實例時
* 任何重新啟動（計數器重設為0）

若要自動收集資訊，您也可以安裝RequestFilter，以在每個請求上增加計數器。 多個計數器可用於不同的時段。

收集到的資訊可用於指示：

* 活動的重大變化
* 冗餘實例
* 任何重新啟動（計數器重設為0）

### HTML注釋 {#html-comments}

建議每個專案都包含伺服器 `html comments` 效能的項目。 許多好的公開例子，選取頁面，開啟頁面來源以檢視並捲動至底部，可看到下列程式碼：

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### 使用JConsole監控效能 {#monitoring-performance-using-jconsole}

工具命令 `jconsole` 可用於JDK。

1. 啟動您的AEM實例。
1. 執行 `jconsole.`
1. 選取您的AEM例項和 **Connect**。

1. 在應用程 `Local` 式中，按兩下 `com.day.crx.quickstart.Main`;概述將顯示為預設值：

   ![chlimage_1-1](assets/chlimage_1-1.png)

   之後，您可以選取其他選項。

### 使用(J)VisualVM監控效能 {#monitoring-performance-using-j-visualvm}

自從JDK 1.6起，工具命令就 `jvisualvm` 可用。 安裝JDK 1.6後，您可以：

1. 啟動您的AEM實例。

   >[!NOTE]
   如果使用Java 5，則可將引 `-Dcom.sun.management.jmxremote` 數添加到啟動JVM的java命令行。 JMX依預設會在Java 6中啟用。

1. 執行下列任一項：

   * `jvisualvm`:在JDK 1.6 bin資料夾中（已測試版本）
   * `visualvm`:可從 [VisualVM](https://visualvm.dev.java.net/) （放血邊緣版本）下載

1. 在應用程 `Local` 式中，按兩下 `com.day.crx.quickstart.Main`;概述將顯示為預設值：

   ![chlimage_1-2](assets/chlimage_1-2.png)

   在此之後，您可以選擇其他選項，包括監視器：

   ![chlimage_1-3](assets/chlimage_1-3.png)

您可以使用此工具生成線程轉儲和記憶體頭轉儲。 技術支援團隊通常會要求此項資訊。

### 資訊收集 {#information-collection}

盡可能瞭解您的安裝，有助於您追蹤可能導致效能變更的原因，以及這些變更是否合理。 這些量度需要定期收集，以便您輕鬆看到重大變更。

下列資訊可能很有用：

* [有多少作者使用此系統？](#how-many-authors-are-working-with-the-system)
* [每天啟動頁面的平均次數是多少？](#what-is-the-average-number-of-page-activations-per-day)
* [您目前在此系統上維護多少頁？](#how-many-pages-do-you-currently-maintain-on-this-system)
* [如果您使用MSM，每個月的平均推廣次數是多少？](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [每月的即時副本平均數是多少？](#what-is-the-average-number-of-live-copies-per-month)
* [如果您使用AEM Assets，您目前在Assets中會維護多少資產？](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [資產的平均規模是多少？](#what-is-the-average-size-of-the-assets)
* [目前使用多少個範本？](#how-many-templates-are-currently-used)
* [目前使用多少個元件？](#how-many-components-are-currently-used)
* [您在尖峰時間時，在作者系統上每小時有多少請求？](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [在尖峰時段，您在發佈系統上每小時有多少個請求？](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 有多少作者使用此系統？ {#how-many-authors-are-working-with-the-system}

要查看自安裝以來使用系統的作者人數，請使用命令行：

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

要查看在指定日期工作的作者人數，請執行以下操作：

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 每天啟動頁面的平均次數是多少？ {#what-is-the-average-number-of-page-activations-per-day}

查看自伺服器安裝以來使用儲存庫查詢的頁面激活總數；via CRXDE - Tools - Query:

* **類型**`XPath`

* **路徑**`/`

* **查詢**`//element(*, cq:AuditEvent)[@cq:type='Activate']`

然後計算安裝後經過的天數，以計算平均值。

#### 您目前在此系統上維護多少頁？ {#how-many-pages-do-you-currently-maintain-on-this-system}

查看伺服器上當前使用儲存庫查詢的頁數；via CRXDE - Tools - Query:

* **類型**`XPath`

* **路徑**`/`

* **查詢**`//element(*, cq:Page)`

#### 如果您使用MSM，每個月的平均推廣次數是多少？ {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

要確定自安裝以來使用儲存庫查詢的推出總數；via CRXDE - Tools - Query:

* **類型**`XPath`

* **路徑**`/`

* **查詢**`//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

計算自安裝以來經過的月數，以計算平均值。

#### 每月的即時副本平均數是多少？ {#what-is-the-average-number-of-live-copies-per-month}

要確定自安裝以來使用儲存庫查詢建立的即時拷貝總數；via CRXDE - Tools - Query:

* **類型**`XPath`

* **路徑**`/`

* **查詢**`//element(*, cq:LiveSyncConfig)`

再次使用安裝後經過的月數來計算平均值。

#### 如果您使用AEM Assets，您目前在Assets中會維護多少資產？ {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

要查看您當前維護的DAM資產數量，請使用儲存庫查詢；via CRXDE - Tools - Query:

* **類型**`XPath`
* **路徑**`/`
* **查詢**`/jcr:root/content/dam//element(*, dam:Asset)`

#### 資產的平均規模是多少？ {#what-is-the-average-size-of-the-assets}

要確定資料夾的總大 `/var/dam` 小：

1. 使用WebDAV將儲存庫映射到本地檔案系統。

1. 使用命令行：

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   若要取得平均大小，請將全域大小除以中（取自上方）的 `/var/dam` 資產總數。

#### 目前使用多少個範本？ {#how-many-templates-are-currently-used}

要查看伺服器上當前使用儲存庫查詢的模板數；via CRXDE - Tools - Query:

* **類型**`XPath`
* **路徑**`/`
* **查詢**`//element(*, cq:Template)`

#### 目前使用多少個元件？ {#how-many-components-are-currently-used}

要查看伺服器上當前使用儲存庫查詢的元件數；via CRXDE - Tools - Query:

* **類型**`XPath`
* **路徑**`/`
* **查詢**`//element(*, cq:Component)`

#### 您在尖峰時間時，在作者系統上每小時有多少請求？ {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

要確定您在作者系統上的尖峰時間每小時請求：

1. 要確定自安裝以來請求的總數，請使用命令行：

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 要確定起始日期和終止日期，請執行以下操作：

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   使用這些值可計算自安裝以來經過的小時數，然後計算每小時的平均請求數。

#### 在尖峰時段，您在發佈系統上每小時有多少個請求？ {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

在您的發佈實例上重複上述步驟。

## 分析特定藍本 {#analyzing-specific-scenarios}

以下列出您是否開始遇到某些效能問題時要檢查的建議。 （不幸的是）這份清單並不全面。

>[!NOTE]
如需詳細資訊，請參閱下列文章：
* [線程轉儲](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
* [分析記憶體問題](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
* [使用內建設定器進行分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
* [分析緩慢和被阻止的進程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)



### CPU佔100% {#cpu-at}

如果系統的CPU持續以100%的速度運行，請參閱：

* 知識庫：

   * [分析慢速和阻止的進程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### 記憶體不足 {#out-of-memory}

雖然在「開發與測試」期間應偵測到此類錯誤，但某些情形可能會漏掉。

如果您的系統記憶體不足，可以通過各種方式看到，包括效能降級和錯誤消息（包括子文本）:

`java.lang.OutOfMemoryError`

在這些情況下，請檢查：

* 用於啟動AEM的JVM [設定](/help/sites-deploying/deploy.md#getting-started)
* 知識庫：

   * [分析記憶體問題](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### 磁碟I/O {#disk-i-o}

如果系統的磁碟空間不足，或者您注意到磁碟已過時，請參閱：

* 您是否已停用除錯資訊的收集；這可以配置在各種位置，包括：

   * [Apache Sling JSP指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling記錄設定](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM除錯篩選](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [伐木工](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)[](/help/sites-deploying/configuring.md#loggersandwritersforindividualservices)

* 是否已配置版本清 [除？](/help/sites-deploying/version-purging.md)
* 知識庫：

   * [開啟的檔案太多](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [日誌佔用太多磁碟空間](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 常規效能降級 {#regular-performance-degradation}

如果您看到實例在每次重新引導後（有時一週或更晚）效能惡化，則可以檢查以下內容：

* [記憶體不足](#outofmemory)
* 知識庫：

   * [未關閉的會話](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM調整 {#jvm-tuning}

Java Virtual Machine(JVM)在微調方面已大幅改善（尤其是自Java 7以來）。 因此，通常適合指定合理的固定JVM大小和使用預設值。

如果預設設定不適合，則在嘗試調整JVM之前，請務必建立一種方法來監控和評估GC效能；這可能涉及到監控因素，包括堆大小、算法等。

一些常見選擇是：

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

產生的記錄檔可由GC視覺化器擷取，例如：

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

或JConsole:

* 這些設定適用於「寬開啟」JMX連線：

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 然後使用JConsole連接到JVM;請參閱：
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

這可協助您瞭解使用了多少記憶體、使用了哪些GC演算法、執行時間，以及這對您的應用程式效能有何影響。 若沒有這一點，調音就只是「隨意擺弄旋鈕」。

>[!NOTE]
對於Oracle的VM，還有以下資訊：
[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)