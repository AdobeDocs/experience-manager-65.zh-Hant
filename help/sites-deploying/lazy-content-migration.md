---
title: 延遲內容移轉
seo-title: Lazy Content Migration
description: 了解AEM 6.4中的延遲內容移轉。
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 6%

---

# 延遲內容移轉 {#lazy-content-migration}

為了回溯相容性， **/etc** 和 **/content** 從AEM 6.3開始，升級後不會立即接觸或轉換。 這樣做是為了確保客戶應用程式在這些結構上的依賴性保持不變。 與這些內容結構相關的功能仍相同，即使現成可用的AEM 6.5中的內容會托管在其他位置。

雖然並非所有這些地點都能自動轉換，但有些地方還是被推遲了 `CodeUpgradeTasks` 也稱為「延遲內容移轉」。 這可讓客戶使用此系統屬性重新啟動執行個體，以觸發這些自動轉換：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

這會導致 `CodeUpgradeTasks` 執行。

雖然目標是高效執行，但此升級過程是同步的，因此會因需要處理的內容量而導致停機。 建議在生產系統之前評估階段環境上的執行時間，以根據維護窗口進行規劃。

由於這通常也需要調整應用程式，因此應該連同對應的應用程式部署一起執行此活動。

以下是 `CodeUpgradeTasks` 在6.5中介紹：

| **名稱** | **相關** **適用於AEM舊版** | **移轉** **類型** | **詳細資料** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 立即 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 立即 | 全部檢測 `LiveRelationShips` 從 `VersionStorage` 已刪除，並將排除屬性新增至父項 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 立即 | 預設設定為安全重構雲服務 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 立即 | 從中刪除基於屬性的連結 **/content** to **/conf** （由OSGi機制取代），會產生對應的OSGi設定 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 立即 | 由於merge_preserve預設處理安全拒絕規則會覆寫指定的權限，導致需要在升級時重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 立即 | 檢測使用Html5SmartFile介面工具集的元件，在內容中搜索元件的用法並重構持久性，有效地將二進位檔向下移動一個級別，而不將其儲存在元件級別。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 立即 | 將舊樣式的專案從 **/etc/projects** to **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 立即 | 將容器層引入層次結構（區域），並調整參照。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 立即 | 將固定位置名稱設定為目標元件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 立即 | 在6.2結構、實例、通知之前對工作流模型進行複雜的轉換，然後從備份位置合併回 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 立即 | 將資產、自訂中繼資料結構和處理設定檔從 **/apps** to **/conf** 並將中繼資料結構和中繼資料描述檔表單從coral2轉譯為coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 立即 | 將資產和自訂搜尋Facet從 **/apps** to **/conf** 並將中繼資料結構和中繼資料描述檔表單從coral2轉譯為coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 立即 | 更新收件箱項以排序收件箱項（調整元資料以有效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 立即 | 通過將相對路徑替換為 **/conf** 取代 **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 立即 | 調整導覽結構 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 立即 | 將監控控制面板的自訂設定從 **/libs** 和 **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 立即 | 轉譯Assets中的processingProfile屬性（使用至6.1），以符合6.3和更新的結構。 也會將設定檔的相對路徑調整為 **/conf** 取代 **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 立即 | 升級任務，在升級時刪除過時的CRXDE Lite和Web控制台菜單項。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延遲 | 移動SRP雲端設定、社群觀看字設定、清除 **/etc/social** 和 **/etc/enablement** （執行延遲移轉時，需要調整任何參考和資料 — 應用程式部分不再取決於此結構）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延遲 | 清除 **/etc/cloudsettings** （包含ContextHub設定）。 設定會在首次存取時自動移轉。 如果延遲內容移轉是隨著升級，請在 **/etc/cloudsettings** 必須在升級前透過套件保留並重新安裝，以便隱含轉換開始運作，並在完成後解除安裝套件。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延遲 | 將舊版標題結構調整為使用者設定檔節點中的標題。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延遲 | 將商務內容從 **/etc/commerce** to **/var/commerce**. 移動移轉內容期間，會更新對移動內容的參考，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延遲 | 將舊版目錄設定和Dynamic MediaCloud Services設定從 **/etc** to **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延遲 | 清除下方現有的舊版clientlib **/etc/clientlibs** |
