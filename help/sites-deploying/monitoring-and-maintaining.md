---
title: 監控及維護您的Adobe Experience Manager執行個體
description: 瞭解如何監控及維護您的Adobe Experience Manager執行個體。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: d3375935-090d-4052-8234-68ef4ddbab6a
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '5755'
ht-degree: 0%

---

# 監控及維護您的Adobe Experience Manager執行個體{#monitoring-and-maintaining-your-aem-instance}

部署AEM執行個體後，您必須監控並維護其操作、效能和完整性。

這裡的關鍵因素是，您必須知道系統在正常條件下的外觀和行為，才能識別潛在問題。 若要使用此功能，最好監視系統並收集一段時間內的資訊。

| 檢查 | 考量事項 | 註解/動作 |
|---|---|---|
| 備份計畫。 |  | 瞭解如何[備份您的執行個體](/help/sites-deploying/monitoring-and-maintaining.md#backups)。 |
| 災難回覆計畫。 | 貴公司的災難回覆指引。 |  |
| 錯誤追蹤系統可用於報告問題。 | 例如，[Bugzilla](https://www.bugzilla.org/)、[Jira](https://www.atlassian.com/software/jira)或許多其他其中之一。 |  |
| 正在監視檔案系統。 | 如果可用磁碟空間不足，CRX存放庫「凍結」。 空間可用後會繼續。 | 可用空間變少時，可在記錄檔中看到`*ERROR* LowDiskSpaceBlocker`訊息。 |
| 正在監視[記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)。 |  |  |
| 系統監控在背景中（不斷）執行。 | 包括CPU、記憶體、磁碟及網路使用量。 例如，使用iostat / vmstat / perfmon。 | 記錄的資料會視覺化，且可用於追蹤效能問題。 也可存取原始資料。 |
| 正在監視[AEM效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)。 | 包括[要求計數器](/help/sites-deploying/monitoring-and-maintaining.md#request-counters)以監視流量層級。 | 如果發現顯著或長期效能損失，應進行詳細調查。 |
| 您正在監視您的[復寫代理程式](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)。 |  |  |
| 定期清除工作流程例項。 | 存放庫大小和工作流程效能。 | 請參閱[定期清除工作流程執行個體](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。 |

## 備份 {#backups}

備份以下專案是良好的作法：

* 您的軟體安裝 — 組態重大變更之前/之後
* 存放庫中的內容 — 定期

貴公司很可能有您遵循的備份原則，對於要備份的內容與時間的其他考量事項包括：

* 系統和資料的重要性。
* 變更軟體或資料的頻率。
* 資料量；容量偶爾也會造成問題，執行備份的時間也會造成問題。
* 是否可以在使用者上線時進行備份；如果可能，會對效能造成什麼影響。
* 使用者的地理分佈；也就是說，何時是最佳備份時間（將影響降至最低）？
* 您的災難回覆原則；是否有必須儲存備份資料的准則（例如，離站和特定媒體）。

通常，會定期進行完整備份（例如，每天、每週或每月），並在中間進行增量備份（例如，每小時、每日或每週）。

>[!CAUTION]
>
>實作生產執行個體的備份時，必須執行測試&#x200B;**，以確保您可以成功還原備份。
>
>如果沒有這項測試，備份可能會毫無用處（最壞的情況）。

>[!NOTE]
>
>如需有關備份效能的詳細資訊，請閱讀[備份效能](/help/sites-deploying/configuring-performance.md#backup-performance)區段。

### 備份您的軟體安裝 {#backing-up-your-software-installation}

在安裝或組態重大變更後，建立軟體安裝的備份。

若要完成此工作，請[備份整個存放庫](#backing-up-your-repository)，然後：

1. 停止AEM。
1. 從您的檔案系統備份整個`<cq-installation-dir>`。

>[!CAUTION]
>
>如果您正在操作協力廠商應用程式伺服器，其他資料夾可能位於不同的位置，也必須進行備份。 如需安裝應用程式伺服器的相關資訊，請參閱[如何使用應用程式伺服器安裝AEM](/help/sites-deploying/application-server-install.md)。

>[!CAUTION]
>
>支援檔案資料存放區的增量備份；當對其他元件使用增量備份時（例如Lucene索引），請確保已刪除的檔案在備份中也標籤為已刪除。

>[!NOTE]
>
>磁碟映象也可作為備份機制使用。

### 備份您的存放庫 {#backing-up-your-repository}

CRX檔案的[備份與還原](/help/sites-administering/backup-and-restore.md)區段涵蓋所有與CRX存放庫備份相關的問題。

如需建立線上「熱」備份的完整詳細資訊，請參閱[建立線上備份](/help/sites-administering/backup-and-restore.md#online-backup)。

## 版本清除 {#version-purging}

**清除版本**&#x200B;工具旨在清除存放庫中節點或節點階層的版本。 其主要用途是協助您移除舊版節點，以縮小存放庫的大小。

本節將討論與AEM的版本設定功能相關的維護操作。 **清除版本**&#x200B;工具旨在清除存放庫中節點或節點階層的版本。 其主要用途是協助您移除舊版節點，以縮小存放庫的大小。

### 概觀 {#overview}

**清除版本**&#x200B;工具可做為每週維護工作使用。 在第一次使用之前，必須先新增該變數，然後進行設定。 之後，可依請求或每週執行。

### 清除網站的版本 {#purging-versions-of-a-web-site}

若要清除網站的版本，請依照下列步驟進行：

1. 導覽至&#x200B;**[工具](/help/sites-administering/tools-consoles.md)** **主控台**，選取&#x200B;**作業**、**維護**，然後選取&#x200B;**每週維護期間**。

1. 從頂端工具列選取&#x200B;**+新增**。

   ![新增版本清除](assets/version-purge-add.png)

1. 在&#x200B;**新增工作**&#x200B;對話方塊的下拉式清單中選取&#x200B;**版本清除**。 然後&#x200B;**儲存**。

   ![新增版本清除](assets/version-purge-add-new-task.png)

1. 已新增&#x200B;**版本清除**&#x200B;工作。 使用卡片動作可以：
   * Select — 在頂端工具列中顯示其他動作
   * 執行 — 立即執行已設定的整個清除
   * 設定 — 設定每週清除工作

   ![版本清除動作](assets/version-purge-actions.png)

1. 選取&#x200B;**設定**&#x200B;動作以開啟&#x200B;**Day CQ WCM版本清除工作**&#x200B;的Web主控台，您可以在其中設定：

   ![版本清除設定](assets/version-purge-configuration.png)

   * **清除路徑**
設定要清除之內容的開始路徑；例如，`/content/wknd`。

     >[!CAUTION]
     >
     >Adobe建議您為每個網站定義多個路徑。
     >
     >定義含有太多子項的路徑，會大幅延長執行整個清除的時間。

   * **遞回清除版本**

      * 如果您只想永久刪除路徑所定義的節點，請取消選取。
      * 選取是否要永久刪除由路徑及其子系所定義的節點。

   * **版本數目上限**
設定要保留的版本數目上限（針對每個節點）。 留空將不使用此設定。

   * **版本數目下限**
設定要保留的版本數目下限（針對每個節點）。 留空將不使用此設定。

   * **最大版本期限**
設定您想要保留的最大版本保留時間（以天為單位，針對每個節點）。 留空將不使用此設定。

   然後&#x200B;**儲存**。

1. 瀏覽/返回&#x200B;**每週維護期間**&#x200B;視窗，並選取&#x200B;**執行**&#x200B;以立即啟動程式。

>[!CAUTION]
>
>您可以使用傳統UI對話方塊來執行設定的[試用](#analyzing-the-console)：
>
>* http://localhost:4502/etc/versioning/purge.html
>
>必須還原存放庫，才能還原已清除的節點。 在清除之前，請一律執行試用，以處理您的設定。

#### 試用 — 分析主控台 {#analyzing-the-console}

傳統UI提供&#x200B;**試用**&#x200B;選項，來源為：

* http://localhost:4502/etc/versioning/purge.html

程式會列出所有已處理的節點。 處理期間，節點可以有下列其中一種狀態：

* `ignore (not versionnable)`：節點不支援版本設定，而且會在處理序期間被忽略。

* `ignore (no version)`：節點沒有任何版本，在處理期間會略過。

* `retained`：節點未清除。
* `purged`：節點已清除。

此外，主控台還提供版本的實用資訊：

* `V 1.0`：版本號碼。
* `V 1.0.1`&#42;：星號表示版本是目前（基礎）版本，無法清除。

* `Thu Mar 15 2012 08:37:32 GMT+0100`：版本的日期。

在下列範例中：

* **[!DNL Shirts]**&#x200B;版本已清除，因為其版本保留時間超過兩天。
* **[!DNL Tonga Fashions!]**&#x200B;版本已清除，因為其版本數大於5。

![global_version_screenshot](assets/global_version_screenshot.png)

## 使用稽核記錄和記錄檔 {#working-with-audit-records-and-log-files}

您可以在不同的位置找到與Adobe Experience Manager (AEM)相關的稽核記錄和記錄檔。 以下提供您可找到內容及位置的概觀。

### 使用記錄檔 {#working-with-logs}

AEM WCM會記錄詳細的記錄。 拆開包裝並開始快速入門後，您可在以下位置找到記錄檔：

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 記錄檔輪換 {#log-file-rotation}

記錄檔案旋轉是指透過定期建立檔案來限制檔案增長的程式。 在AEM中，名為`error.log`的記錄檔會根據指定規則每天輪換一次：

* 已根據模式`{original_filename}.yyyy-MM-dd`重新命名`error.log`檔案。 例如，在2010年7月11日，將目前的記錄檔重新命名為`error.log-2010-07-10`，然後建立新的`error.log`。

* 先前的記錄檔不會被刪除，因此您有責任定期清理舊記錄檔，以限制磁碟的使用量。

>[!NOTE]
>
>如果您升級AEM安裝，則AEM不再使用的任何現有記錄檔會保留在磁碟上。 您無須冒風險即可移除這些專案。 所有新的記錄專案都會寫入新的記錄檔中。

### 尋找記錄檔 {#finding-the-log-files}

各種記錄檔會儲存在您安裝AEM的檔案伺服器上：

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
對AEM WCM和存放庫的所有存取請求都會在此處註冊。

   * `audit.log`
仲裁動作在此註冊。

   * `error.log`
錯誤訊息（嚴重性各異）會在此處註冊。

   * [`ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html?lang=zh-Hant)
此記錄檔只有在啟用[!DNL Dynamic Media]時才使用。 它提供用於分析內部ImageServer處理作業行為的統計資料和分析資訊。

   * `request.log`
每個存取要求都會在這裡與回應一起註冊。

   * [`s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html?lang=zh-Hant)
此記錄檔只有在啟用[!DNL Dynamic Media]時才使用。 s7access記錄檔會記錄透過`/is/image`和`/is/content`向[!DNL Dynamic Media]提出的每個要求。

   * `stderr.log`
會保留啟動期間產生的錯誤訊息，同樣是不同嚴重性層級的錯誤訊息。 依預設，記錄層級設定為`Warning` ( `WARN`)

   * `stdout.log`
保留指示啟動期間事件的記錄訊息。

   * `upgrade.log`
提供從`com.day.compat.codeupgrade`和`com.adobe.cq.upgradesexecutor`封裝執行的所有升級作業記錄。

* `<cq-installation-dir>/crx-quickstart/repository/segmentstore`

   * `journal.log`
修訂日誌資訊。

>[!NOTE]
>
>從&#x200B;**system/console/status-Bundlelist**&#x200B;頁面產生的&#x200B;**Download Full**&#x200B;package中不包含ImageServer和s7access記錄檔。 基於支援目的，如果您有[!DNL Dynamic Media]個問題，請在聯絡客戶支援時附加ImageServer和s7access記錄。

### 啟動DEBUG記錄層級 {#activating-the-debug-log-level}

預設記錄層級（[Apache Sling記錄組態](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)）為Information，因此不會記錄偵錯訊息。

若要啟動記錄器的偵錯記錄層級，請在儲存庫中設定屬性`org.apache.sling.commons.log.level`為偵錯。 例如，在`/libs/sling/config/org.apache.sling.commons.log.LogManager`上設定[全域Apache Sling記錄](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)。

>[!CAUTION]
>
>請勿將記錄保留在偵錯記錄層級的時間超過所需時間，因為它會產生許多記錄專案，佔用資源。

偵錯檔案中的某一行通常以DEBUG開頭，然後提供記錄層級、安裝程式動作和記錄訊息。 例如：

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

記錄層級如下：

| 0 | 嚴重錯誤 | 動作已失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 錯誤 | 動作已失敗。 安裝會繼續，但部分AEM WCM未正確安裝且無法運作。 |
| 2 | 警告 | 動作成功但發生問題。 AEM WCM可能正常運作，也可能無法正常運作。 |
| 3 | 資訊 | 動作已成功。 |

### 建立自訂記錄檔 {#create-a-custom-log-file}

>[!NOTE]
>
>使用Adobe Experience Manager時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

在特定情況下，您可能想要使用不同的記錄層級來建立自訂記錄檔。 在存放庫中，執行以下操作：

1. 如果不存在，請為您的專案`/apps/<project-name>/config`建立設定資料夾( `sling:Folder`)。
1. 在`/apps/<project-name>/config`底下，建立新[Apache Sling記錄記錄器設定](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)的節點：

   * 名稱：`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`

     其中`<identifier>`由您（必須）輸入以識別執行個體的任意文字取代（您無法忽略此資訊）。

     例如 `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 類型：`sling:OsgiConfig`

   >[!NOTE]
   >
   >雖然不是技術要求，但建議您將`<identifier>`設為唯一。

1. 在此節點上設定下列屬性：

   * 名稱：`org.apache.sling.commons.log.file`

     型別：字串

     值：指定記錄檔；例如，`logs/myLogFile.log`

   * 名稱：`org.apache.sling.commons.log.names`

     型別：字串[] （字串+多個）

     值：指定記錄器要記錄訊息的OSGi服務；例如，下列全部：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`

   * 名稱：`org.apache.sling.commons.log.level`

     型別：字串

     值：指定必要的記錄層級（`debug`、`info`、`warn`或`error`）；例如`debug`

   * 視需要設定其他引數：

      * 名稱：`org.apache.sling.commons.log.pattern`

        類型：`String`

        值：視需要指定記錄訊息的模式；例如，

        `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern`支援最多六個引數。
   >
   >{0}型別`java.util.Date`的時間戳記
   >
   >{1}記錄標籤
   >
   >{2}目前執行緒的名稱
   >
   >{3}記錄器的名稱
   >
   >{4}記錄層級
   >
   >{5}記錄訊息
   >
   >如果記錄呼叫包含`Throwable`，則會將棧疊追蹤附加至訊息。

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names必須有一個值。

   >[!NOTE]
   >
   >記錄寫入器路徑相對於`crx-quickstart`位置。
   >
   >因此，記錄檔指定為：
   >
   >`logs/thelog.log`
   >
   >寫入：
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`。
   >
   >以及指定為的記錄檔：
   >
   >`../logs/thelog.log`
   >
   >寫入目錄：
   >
   >`<cq-installation-dir>/logs/`\
   >（亦即`<cq-installation-dir>/crx-quickstart/`旁）

1. 只有在需要新的Writer時（也就是使用與預設Writer不同的設定），才需要執行此步驟。

   >[!CAUTION]
   >
   >只有當現有的預設值不適用時，才需要新的記錄寫入器組態。
   >
   >如果未設定明確的Writer，則系統會根據預設值自動產生隱含的Writer。

   在`/apps/<project-name>/config`底下，為新的[Apache Sling記錄寫入器組態](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)建立節點：

   * 名稱： `org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` （寫入者）

     和記錄器一樣，`<identifier>`會由您（必須）輸入以識別執行個體的任意文字取代（您無法忽略此資訊）。 例如 `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 類型：`sling:OsgiConfig`

   >[!NOTE]
   >
   >雖然不是技術要求，但建議您將`<identifier>`設為唯一。

   在此節點上設定下列屬性：

   * 名稱：`org.apache.sling.commons.log.file`

     類型：`String`

     值：指定記錄檔，使其符合記錄器中指定的檔案；

     在此範例中，`../logs/myLogFile.log`。

   * 視需要設定其他引數：

      * 名稱：`org.apache.sling.commons.log.file.number`

        類型：`Long`

        值：指定您要保留的記錄檔數目；例如`5`

      * 名稱：`org.apache.sling.commons.log.file.size`

        類型：`String`

        值：視需要指定，以大小/日期控制檔案旋轉；例如`'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size`藉由設定下列任一專案來控制記錄檔的旋轉：
   >
   >* 檔案大小上限
   >* 時間/日期排程
   >
   >指示何時建立新檔案（以及根據名稱模式重新命名現有檔案）。
   >
   >* 可使用數字指定大小限制。 如果未指定大小指標，則會將其視為位元組數，或者您可以新增其中一個大小指標 — `KB`、`MB`或`GB` （忽略大小寫）。
   >* 可將時間/日期排程指定為`java.util.SimpleDateFormat`模式。 它會定義檔案旋轉的時間段。 此外，尾碼也會附加至旋轉後的檔案（用於識別）。
   >
   >預設值為&#39;.&#39;yyyy-MM-dd （用於每日記錄輪換）。
   >
   >例如，在2010年1月20日午夜（或在此日期之後第一個記錄訊息發生精確時），../logs/error.log將重新命名為../logs/error.log.2010-01-20。 1月21日的記錄會輸出到（新的和空的） ../logs/error.log ，直到該日次變更時為止。
   >
   >| `'.'yyyy-MM` | 每個月初的輪換 |
   >|---|---|
   >| `'.'yyyy-ww` | 每週第一天的輪換（視地區設定而定）。 |
   >| `'.'yyyy-MM-dd` | 在每天的午夜輪換。 |
   >| `'.'yyyy-MM-dd-a` | 在每天的午夜和正午輪換。 |
   >| `'.'yyyy-MM-dd-HH` | 每小時頂端旋轉。 |
   >| `'.'yyyy-MM-dd-HH-mm` | 每分鐘開頭的旋轉。 |
   >
   >注意：指定時間/日期時：
   >
   >1. 您應該在一對單引號(&#39; &#39;)中「逸出」常值文字；
   >
   >    避免將某些字元解譯為模式字母。
   >
   >1. 在選項中的任何位置，都只能使用有效檔案名稱所允許的字元。

1. 使用您選擇的工具讀取您的新記錄檔。

   此範例建立的記錄檔為`../crx-quickstart/logs/myLogFile.log`。

Felix主控台也提供有關`../system/console/slinglog`的Sling記錄檔支援資訊；例如`https://localhost:4502/system/console/slinglog`。

### 尋找稽核記錄 {#finding-the-audit-records}

稽核記錄的保留是為了提供誰做了什麼以及何時做了什麼的記錄。 AEM WCM和OSGi事件會產生不同的稽核記錄。

#### 頁面製作時顯示的AEM WCM稽核記錄 {#aem-wcm-audit-records-shown-when-page-authoring}

1. 開啟頁面。
1. 從sidekick中，您可以選取帶有鎖定圖示的標籤，然後按兩下&#x200B;**稽核記錄……**
1. 隨即開啟新視窗，顯示目前頁面的稽核記錄清單。

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 當您要關閉視窗時，請按一下&#x200B;**確定**。

#### AEM WCM稽核儲存庫內的記錄 {#aem-wcm-auditing-records-within-the-repository}

在`/var/audit`資料夾內，根據資源保留稽核記錄。 您可以向下鑽研，直到您看到個別記錄及其包含的資訊。

這些專案儲存的資訊與編輯頁面時顯示的資訊相同。

#### 來自Web主控台的OSGi稽核記錄 {#osgi-audit-records-from-the-web-console}

OSGi事件也會產生稽核記錄，您可以從AEM Web Console的&#x200B;**組態狀態**&#x200B;標籤> **記錄檔**&#x200B;標籤看到這些記錄：

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 監視復寫代理程式 {#monitoring-your-replication-agents}

您可以監視您的[復寫佇列](/help/sites-deploying/replication.md)，以偵測佇列何時關閉或遭到封鎖 — 這反過來可能表示發佈執行個體或外部系統有問題：

* 是否已啟用所有必要的佇列？
* 仍然需要任何停用的佇列嗎？
* 所有`enabled`佇列的狀態應該是`idle`或`active`，表示作業正常；任何佇列都不應該是`blocked`，這通常是接收者端發生問題的徵兆。

* 如果佇列的大小隨著時間而增加，則可能表示封鎖的佇列。

監督復寫代理程式：

1. 存取AEM中的&#x200B;**工具**&#x200B;索引標籤。
1. 按一下&#x200B;**復寫**。
1. 連按兩下適當環境的代理程式連結（左窗格或右窗格）；例如，作者上的&#x200B;**代理程式**。

   產生的視窗會顯示製作環境的所有復寫代理程式概觀，包括其目標和狀態。

1. 按一下適當的代理程式名稱（連結）以顯示該代理程式的詳細資訊：

   ![chlimage_1](assets/chlimage_1.jpeg)

   您可以在這裡：

   * 檢視代理程式是否已啟用。
   * 檢視任何復寫的目標。
   * 檢視復寫佇列是否為使用中（已啟用）。
   * 檢視佇列中是否有任何專案。
   * **重新整理**&#x200B;或&#x200B;**清除**&#x200B;以更新佇列專案的顯示。 這麼做有助於檢視進入和離開佇列的專案。
   * **檢視記錄檔**&#x200B;以存取復寫代理程式的任何動作記錄檔。
   * **測試目標執行個體的連線**。
   * 如有需要，對任何佇列專案強制重試&#x200B;**&#x200B;**。

   >[!CAUTION]
   >
   >請勿對發佈執行個體上的「反向復寫寄件匣」使用「測試連線」連結。
   >
   >如果對Outbox佇列執行復寫測試，則任何早於測試復寫的專案都會透過每次反向復寫重新處理。
   >
   >如果佇列中存有這類專案，可在下列XPath JCR查詢中找到並移除它們。
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

您可以再次開發解決方案以偵測所有復寫代理程式（位於`/etc/replication/author`或`/etc/replication/publish`下），然後檢查代理程式( `enabled`、`disabled`)和基礎佇列( `active`、`idle`、`blocked`)的狀態。

## 監控效能 {#monitoring-performance}

[效能最佳化](/help/sites-deploying/configuring-performance.md)是互動式處理序，在開發期間接收焦點。 部署後，會在特定間隔或事件後進行稽核。

收集最佳化資訊時使用的方法也可用於持續監控。

>[!NOTE]
>
>也可以檢查可改善效能[&#128279;](/help/sites-deploying/configuring-performance.md#configuring-for-performance)的特定組態。

以下列出常見的效能問題，以及如何發現和處理這些問題的建議。

| 區域 | 症狀 | 若要增加容量…… | 若要減少磁碟區…… |
|---|---|---|---|
| 用戶端 | 高使用者端CPU使用量。 | 安裝具有較高效能的使用者端CPU。 | 簡化(HTML)版面。 |
|   | 伺服器CPU使用量低。 | 升級至更快的瀏覽器。 | 改善使用者端快取。 |
|   | 有些使用者端速度很快，有些速度很慢。 |  |  |
| 伺服器 |  |  |  |
| 網路 | 伺服器和使用者端的CPU使用量都偏低。 | 移除任何網路瓶頸。 | 改善/最佳化使用者端快取的設定。 |
|   | 在伺服器上本機瀏覽的速度（相對）比較快。 | 增加網路頻寬。 | 減少網頁的「重量」(例如，減少影像數量、最佳化的HTML)。 |
| Web伺服器 | 網頁伺服器上的CPU使用量很高。 | 叢集您的Web伺服器。 | 減少每頁的點選數（造訪）。 |
|   |  | 使用硬體負載平衡器。 |  |
| 應用程式 | 伺服器CPU使用量很高。 | 叢集您的AEM執行個體。 | 搜尋並清除CPU和記憶體雜湊（使用程式碼檢閱和計時輸出）。 |
|   | 記憶體耗電量高。 |  | 改善所有層級的快取。 |
|   | 回應時間過短。 |  | 最佳化範本和元件（例如結構、邏輯）。 |
| 存放庫 |  |  |  |
| 快取 |  |  |  |

效能問題可能起因於與您網站無關的各種原因，包括連線速度暫時放慢、CPU載入等等。

也可能會影響所有訪客或僅影響其中一部分訪客。

您必須先取得、排序及分析所有這些資訊，才能最佳化一般效能或解決特定問題。

* 在您遇到效能問題之前：

   * 收集儘可能多的資訊，以建立正常情況下系統的良好運作知識

* 當您遇到效能問題時：

   * 嘗試在您知道有良好一般效能和/或伺服器本身（如果可能）的其他使用者端上，使用一個（或最好是更多）標準網頁瀏覽器來複製它
   * 檢查在適當的時段內是否有任何變更（與系統相關），以及這些變更是否可能影響效能
   * 提出問題，例如：

      * 問題是否只會在特定時間發生？
      * 問題是否只發生在特定頁面？
      * 其他請求是否會受到影響？

   * 收集儘可能多的資訊，以便與您在正常情況下的系統知識進行比較：

### 監控及分析效能的工具 {#tools-for-monitoring-and-analyzing-performance}

以下提供可用於監控及分析效能的部分工具的簡短概觀。

其中有些工具取決於您的作業系統。

<table>
 <tbody>
  <tr>
   <td>工具</td>
   <td>用於分析……</td>
   <td>使用狀況/詳細資訊……</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>回應時間和並行。</td>
   <td><a href="#interpreting-the-request-log">解譯request.log</a>。</td>
  </tr>
  <tr>
   <td>桁架/桁架</td>
   <td>頁面載入</td>
   <td><p>追蹤系統呼叫和訊號的Unix/Linux命令。 將記錄層級增加到<code>INFO</code>。</p> <p>分析每個請求的頁面載入次數，以及哪些頁面。</p> </td>
  </tr>
  <tr>
   <td>執行緒傾印</td>
   <td>觀察JVM執行緒。 識別爭用、鎖定和長時間執行者。</td>
   <td><p>依存於作業系統： <br /> - Unix/Linux： <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows （主控台模式）： Ctrl-Break<br /> </p> <p>也提供分析工具，例如<a href="https://github.com/irockel/tda">TDA</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td>棧積傾印</td>
   <td>記憶體不足問題會導致效能降低。</td>
   <td><p>將：<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br />選項新增至前往AEM的Java™呼叫。</p> <p>請參閱JVM疑難排解頁面</a>的<a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/prepapp002.html#CEGBHDFH">選項/旗標。</p> </td>
  </tr>
  <tr>
   <td>系統呼叫</td>
   <td>識別時間問題。</td>
   <td><p>呼叫<code>System.currentTimeMillis()</code>或<code>com.day.util</code>。 計時可用來從您的程式碼產生時間戳記，或是透過<a href="#html-comments">HTML-comments</a>產生。</p> <p><strong>注意：</strong>實作這些專案，以便視需要啟用/停用它們；當系統順利執行時，不需要收集統計資料的額外負荷。</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>識別記憶體遺漏，選擇性地分析回應時間。</td>
   <td><p>基本用法為：</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>如需完整詳細資訊，請參閱<a href="#apache-bench">Apache Bench</a>和<a href="https://httpd.apache.org/docs/2.4/programs/ab.html">ab線上手冊</a>。</p> </td>
  </tr>
  <tr>
   <td>搜尋分析</td>
   <td> </td>
   <td>離線執行搜尋查詢、識別查詢的回應時間、測試及確認結果集。<br /> </td>
  </tr>
  <tr>
   <td>Jmeter</td>
   <td>載入和功能測試。</td>
   <td><a href="https://jmeter.apache.org/">https://jmeter.apache.org/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>深入的CPU和記憶體分析。</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>Java™飛行記錄器</td>
   <td>Java™ Flight Recorder (JFR)是一種工具，用於收集有關執行中Java™應用程式的診斷和設定檔資料。</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>觀察JVM量度和執行緒。</td>
   <td><p>使用方式： jconsole</p> <p>請參閱<a href="https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html">jconsole</a>和<a href="#monitoring-performance-using-jconsole">使用JConsole</a>監控效能。</p> <p><strong>注意：</strong>若使用JDK 1.8，JConsole可透過外掛程式擴充；例如Top或TDA （對話串傾印分析器）。</p> </td>
  </tr>
  <tr>
   <td>Java™ VisualVM</td>
   <td>觀察JVM量度、執行緒、記憶體及設定檔分析。</td>
   <td><p>使用方式： visualvm或visualvm<br /> </p> <p>請參閱<a href="https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/">visualvm</a>和<a href="#monitoring-performance-using-j-visualvm">使用(J)VisualVM</a>監控效能。</p> <p><strong>注意：</strong>若使用JDK 1.8，VisualVM可使用外掛程式進行擴充。 VisualVM在JDK 9之後即終止。 請改用Java™ Flight Recorder。</p> </td>
  </tr>
  <tr>
   <td>桁架/桁架， lsof</td>
   <td>深入的核心呼叫與程式分析(UNIX®)。</td>
   <td>Unix/Linux命令。</td>
  </tr>
  <tr>
   <td>計時統計資料</td>
   <td>請參閱頁面轉譯的時間統計資料。</td>
   <td><p>若要檢視頁面轉譯的時間統計資料，您可以使用<strong>Ctrl-Shift-U</strong>搭配URL中設定的<code>?debugClientLibs=true</code>。</p> </td>
  </tr>
  <tr>
   <td>CPU與記憶體分析工具<br /> </td>
   <td><a href="#interpreting-the-request-log">在開發期間分析緩慢要求時使用</a>。</td>
   <td>例如，<a href="https://www.yourkit.com/">您的套件</a>。 或<a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">Java™飛行錄製器</a>。</td>
  </tr>
  <tr>
   <td><a href="#information-collection">資訊彙集</a></td>
   <td>您正在執行的安裝狀態。</td>
   <td>儘可能瞭解您的安裝，也可協助您追蹤可能導致效能變更的原因，以及這些變更是否合理。 定期收集這些量度，以便輕鬆檢視重大變更。</td>
  </tr>
 </tbody>
</table>

### 解譯request.log {#interpreting-the-request-log}

此檔案會註冊向AEM提出之每個請求的基本資訊。 從這裡可以提取有價值的結論。

`request.log`提供內建方式，可檢視要求所需的時間。 若是開發目的，`tail -f` `request.log`並觀察緩慢回應時間會很有用。 若要分析較大的`request.log`，Adobe建議使用[個`rlog.jar`，讓您排序和篩選回應時間](#using-rlog-jar-to-find-requests-with-long-duration-times)。

Adobe建議將「慢」頁面與`request.log`隔離，然後個別調整這些頁面，以獲得較佳的效能。 包含每個元件的效能測量結果，或使用效能分析工具，例如` [yourkit](https://www.yourkit.com/)`。

#### 監視網站流量 {#monitoring-traffic-on-your-website}

要求記錄檔會註冊每個要求，以及要求的回應：

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

透過總計特定期間（例如，各種24小時期間）內的所有GET專案，您可以對網站上的平均流量進行陳述。

#### 使用request.log監控回應時間 {#monitoring-response-times-with-the-request-log}

要求記錄檔是效能分析的良好起點：

`<cq-installation-dir>/crx-quickstart/logs/request.log`

記錄如下所示（為了簡單起見，這些行會縮短）：

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

此記錄檔的每個請求或回應都有一行：

* 提出每個要求或回應的日期。
* 方括弧內的請求編號。 此數字元合請求和回應。
* 表示要求（向右箭頭）或回應（向左箭頭）的箭頭。
* 對於請求，該行包含：

   * 方法(通常是GET、HEAD或POST)
   * 請求的頁面
   * 通訊協定

* 對於回應，該行包含：

   * 狀態代碼(200表示「成功」，404表示「找不到頁面」
   * MIME型別
   * 回應時間

您可以使用小型指令碼從記錄檔中擷取所需的資訊，並組合您想要的統計資料。 根據這些統計資料，您可以看到哪些頁面或頁面型別速度緩慢，以及整體效能是否令人滿意。

#### 使用request.log監控搜尋回應時間 {#monitoring-search-response-times-with-the-request-log}

搜尋要求也會在記錄檔中註冊：

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

因此，如上所述，您可以使用指令碼來擷取相關資訊並建立統計資料。

不過，在您決定回應時間後，請分析要求花時間的原因，以及可採取哪些措施來改善回應。

#### 監控同時使用者的數量和影響 {#monitoring-the-number-and-impact-of-concurrent-users}

再次使用`request.log`來監視並行，以及系統對此的反應。

在負面影響出現之前，必須進行測試以決定系統可處理多少同時使用者。 同樣地，指令碼可用於從記錄檔擷取結果：

* 監視在特定時間範圍內（例如1分鐘）提出的請求數。
* 測試特定數量的使用者同時（儘可能接近）提出相同請求的影響。 例如，30位使用者同時按一下&#x200B;**儲存**。

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

### 使用rlog.jar尋找持續時間長的請求 {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM包含下列各種協助程式工具：
`<cq-installation-dir>/crx-quickstart/opt/helpers`

這些工具之一`rlog.jar`可用來快速排序`request.log`，以便依持續時間顯示請求，從最長到最短。

下列命令會顯示可能的引數：

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

例如，您可以指定`request.log`檔案作為引數來執行，並顯示持續時間最長的前10個要求：

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

如果必須對大型資料範例執行此作業，請串連個別`request.log`檔案。

### Apache Bench {#apache-bench}

為了將特殊情況（例如垃圾收集）的影響降至最低，建議使用諸如`apachebench`之類的工具（例如，[ab](https://httpd.apache.org/docs/2.4/programs/ab.html)以供進一步檔案使用），以協助識別記憶體洩漏並選擇性地分析回應時間。

Apache Bench的用法如下：

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

上述數字取自存取Geometrixx公司頁面的標準MAcBook Pro筆記型電腦（2010年中），如預設AEM安裝中所包含。 頁面簡單，但未針對效能最佳化。

`apachebench`也會將每個請求的時間顯示為所有並行請求的平均值；請參閱`Time per request: 54.595 [ms]` （所有並行請求的平均值）。 您可以變更並行引數`-c`的值（一次要執行的多個要求數目），以檢視任何效果。

### 要求計數器 {#request-counters}

有關請求流量（特定時段內的請求數）的資訊可讓您指出執行個體的負載。 此資訊可從[request.log](#interpreting-the-request-log)擷取，不過使用計數器會自動收集資料，讓您看到：

* 活動中的重大差異（即區分「許多請求」和「低活動」）
* 當執行個體未使用時
* 任何重新啟動（計數器重設為0）

若要自動收集資訊，您也可以安裝RequestFilter，在每個要求上增加計數器。 多個計數器可用於不同的時段。

收集的資訊可用於指出：

* 活動中的重大變更
* 備援執行個體
* 任何重新啟動（計數器重設為0）

### HTML註解 {#html-comments}

建議每個專案都包含`html comments`以提高伺服器效能。 您可以找到許多不錯的公開範例。 選取頁面、開啟頁面來源以供檢視，然後捲動至底部。 可以檢視以下程式碼：

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### 使用JConsole監控效能 {#monitoring-performance-using-jconsole}

JDK可使用工具命令`jconsole`。

1. 啟動您的AEM執行個體。
1. 執行`jconsole.`
1. 選取您的AEM執行個體並&#x200B;**連線**。

1. 在`Local`應用程式中，連按兩下`com.day.crx.quickstart.Main`；「概觀」會顯示為預設值：

   ![chlimage_1-1](assets/chlimage_1-1.png)

   現在您可以選取其他選項。

### 使用(J)VisualVM監控效能 {#monitoring-performance-using-j-visualvm}

對於JDK 6-8，工具命令`visualvm`可用。 安裝JDK後，您可以執行下列動作：

1. 啟動您的AEM執行個體。

   >[!NOTE]
   >
   >如果使用Java™ 5，您可以將`-Dcom.sun.management.jmxremote`引數新增到啟動JVM的Java™命令列。 Java™ 6依預設會啟用JMX。

1. 執行：

   * `jvisualvm`：在JDK 1.6 bin資料夾（已測試的版本）中
   * `visualvm`：可從[VisualVM](https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/) （leading edge版本）下載

1. 在`Local`應用程式中，按兩下`com.day.crx.quickstart.Main`。 「概述」會顯示為預設值：

   ![chlimage_1-2](assets/chlimage_1-2.png)

   現在您可以選取其他選項，包括「監視」：

   ![chlimage_1-3](assets/chlimage_1-3.png)

您可以使用此工具來產生對話串傾印和記憶體磁頭傾印。 技術支援團隊通常會要求您提供此資訊。

### 資訊彙集 {#information-collection}

儘可能瞭解您的安裝狀況，有助於您追蹤可能導致效能變更的原因，以及這些變更是否合理。 定期收集這些量度，以便輕鬆檢視重大變更。

下列資訊相當實用：

* [有多少作者使用系統？](#how-many-authors-are-working-with-the-system)
* [每天的平均頁面啟用次數是多少？](#what-is-the-average-number-of-page-activations-per-day)
* [您目前在此系統上維護多少個頁面？](#how-many-pages-do-you-currently-maintain-on-this-system)
* [如果您使用MSM，每個月的平均轉出次數是多少？](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [每個月的即時副本平均數量是多少？](#what-is-the-average-number-of-live-copies-per-month)
* [如果您使用AEM Assets，目前在Assets中維護多少資產？](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [資產的平均大小是多少？](#what-is-the-average-size-of-the-assets)
* [目前使用了多少範本？](#how-many-templates-are-currently-used)
* [目前使用多少元件？](#how-many-components-are-currently-used)
* [您在高峰時間每小時在製作系統上有多少請求？](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [您每小時在發佈系統尖峰時段有多少請求？](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 有多少作者使用系統？ {#how-many-authors-are-working-with-the-system}

若要檢視自安裝以來使用系統的作者人數，請使用命令列：

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

若要檢視在指定日期工作的作者人數：

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 每天的平均頁面啟用次數是多少？ {#what-is-the-average-number-of-page-activations-per-day}

若要檢視自伺服器安裝以來的頁面啟用總數，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`

* **路徑** `/`

* **查詢** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

然後計算自安裝後經過的天數來計算平均值。

#### 您目前在此系統上維護多少個頁面？ {#how-many-pages-do-you-currently-maintain-on-this-system}

若要檢視目前伺服器上的頁數，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`

* **路徑** `/`

* **查詢** `//element(*, cq:Page)`

#### 如果您使用MSM，每個月的平均轉出次數是多少？ {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

若要確定自安裝以來的轉出總數，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`

* **路徑** `/`

* **查詢** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

計算安裝後經過的月數以計算平均值。

#### 每個月的即時副本平均數量是多少？ {#what-is-the-average-number-of-live-copies-per-month}

若要確定自安裝以來進行的即時副本總數，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`

* **路徑** `/`

* **查詢** `//element(*, cq:LiveSyncConfig)`

再次使用安裝後經過的月數來計算平均值。

#### 如果您使用AEM Assets，目前在Assets中維護多少資產？ {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

要檢視您目前維護的DAM資產數量，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`
* **路徑** `/`
* **查詢** `/jcr:root/content/dam//element(*, dam:Asset)`

#### 資產的平均大小是多少？ {#what-is-the-average-size-of-the-assets}

若要判斷`/var/dam`資料夾的總大小：

1. 使用WebDAV將存放庫對應到本機檔案系統。

1. 使用命令列：

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   若要取得平均大小，請將全域大小除以`/var/dam`中的資產總數（以上取得）。

#### 目前使用了多少範本？ {#how-many-templates-are-currently-used}

若要檢視目前伺服器上的範本數量，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`
* **路徑** `/`
* **查詢** `//element(*, cq:Template)`

#### 目前使用多少元件？ {#how-many-components-are-currently-used}

若要檢視目前伺服器上的元件數量，請使用存放庫查詢；透過CRXDE — 工具 — 查詢：

* **型別** `XPath`
* **路徑** `/`
* **查詢** `//element(*, cq:Component)`

#### 您在高峰時間每小時在製作系統上有多少請求？ {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

若要決定在尖峰時間您在編寫系統上每小時的要求：

1. 若要判斷安裝後的要求總數，請使用命令列：

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 若要決定開始和結束日期：

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   使用這些值可計算安裝後經過的時數，然後是每小時的平均要求數。

#### 您每小時在發佈系統尖峰時段有多少請求？ {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

在發佈執行個體上重複上述程式。

## 分析特定案例 {#analyzing-specific-scenarios}

以下為建議清單，說明如果您開始遇到某些效能問題，應檢查哪些專案。 此清單並（很遺憾）不完整。

>[!NOTE]
>
>另請參閱下列文章以取得詳細資訊：
>
>* [執行緒傾印](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=zh-Hant)
>* [分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=zh-Hant)
>* [使用內建分析工具](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17499.html?lang=zh-Hant)進行分析
>

### 記憶體不足 {#out-of-memory}

雖然在開發和測試期間應該會偵測到這類錯誤，但某些案例可能會漏過。

如果您的系統記憶體不足，可以透過各種方式發現此問題，包括效能降低和錯誤訊息，包括潛台詞：

`java.lang.OutOfMemoryError`

在這些情況下，請檢查：

* 用於[啟動AEM](/help/sites-deploying/deploy.md#getting-started)的JVM設定
* 知識庫：

* [分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=zh-Hant)

### 磁碟I/O {#disk-i-o}

如果您的系統磁碟空間不足，或您注意到磁碟顛簸，請參閱：

* 無論您是否已停用除錯資訊的收集，都可以在各種位置進行設定，包括：

   * [Apache Sling JSP指令碼處理常式](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling JavaScript處理常式](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling記錄設定](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML資料庫管理員](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [記錄器](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)

* 您是否設定[版本清除](/help/sites-deploying/version-purging.md)，以及設定方式
* 知識庫：

   * [開啟的檔案過多]&#x200B;(https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17470.html?lang=zh-Hant

### 定期效能降低 {#regular-performance-degradation}

如果您在每次重新開機後（有時是一週或以後）發現執行個體的效能惡化，則可以檢查下列專案：

* [記憶體不足](#outofmemory)
* 知識庫：

   * [未關閉的資源解析器](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23761)

### JVM調整 {#jvm-tuning}

Java™ Virtual Machine (JVM)在調整方面已有所改善(尤其是自Java™ 7以來)。 因此，指定合理的固定JVM大小並使用預設值通常是合適的。

如果預設設定不適用，則建立方法來監控和評估GC效能很重要。 請先執行此動作，然後再嘗試調整JVM。 此程式可能涉及監視因素，包括棧積大小、演演算法及其他方面。

常見的選項包括：

* VerboseGC：

  ```
  -verbose:gc \
   -Xloggc:$LOGS/verbosegc.log \
   -XX:+PrintGCDetails \
   -XX:+PrintGCDateStamps
  ```

產生的記錄檔可由GC視覺化檢視器擷取，例如：

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

或JConsole：

* 這些設定適用於「廣開」的JMX連線：

  ```
  -Dcom.sun.management.jmxremote \
   -Dcom.sun.management.jmxremote.port=8889 \
   -Dcom.sun.management.jmxremote.authenticate=false \
   -Dcom.sun.management.jmxremote.ssl=false
  ```

* 然後使用JConsole連線到JVM；請參閱以下內容：
  ` [https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html)`

您可以檢視使用了多少記憶體、使用了哪些GC演演算法、執行時間長短，以及此過程對您的應用程式效能有何影響。 如果沒有它，調整只是「隨機地轉動旋鈕」。

>[!NOTE]
>
>若為Oracle的VM，也可在下列網址取得資訊：
>
>[https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html)
