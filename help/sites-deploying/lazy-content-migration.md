---
title: 懶惰內容遷移
seo-title: Lazy Content Migration
description: 瞭解6.4中的懶AEM散內容遷移。
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

# 懶惰內容遷移 {#lazy-content-migration}

為了向後相容， **/etc** 和 **/內容** 從AEM6.3開始，不會立即在升級時被觸碰或轉換。 這樣做是為了確保客戶應用程式對這些結構的依賴性保持不變。 與這些內容結構相關的功能仍然相同，即使現成6.5中的內容將在AEM另一個地方托管。

雖然並非所有這些位置都可以自動轉換，但有一些延遲 `CodeUpgradeTasks` 也稱為「懶惰內容遷移」。 這允許客戶通過使用此系統屬性重新啟動實例來觸發這些自動轉換：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

這將導致 `CodeUpgradeTasks` 執行。

雖然目標是高效執行，但此升級過程是同步的，因此會因需要處理的內容數量而導致停機。 建議在生產系統之前評估階段環境上的執行時間，以規劃相應的維護窗口。

由於這通常也需要調整應用程式，因此應同時執行此活動和相應的應用程式部署。

下面是 `CodeUpgradeTasks` 6.5中介紹：

| **名稱** | **相關** **對於AEM以前的版本** | **遷移** **類型** | **詳細資料** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 立即 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 立即 | 檢測所有 `LiveRelationShips` 從 `VersionStorage` 已刪除並將排除屬性添加到父級 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 立即 | 在預設設定下重構雲服務以確保安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 立即 | 從中刪除基於屬性的連結 **/內容** 至 **/conf** （由OSGi機制替換），生成相應的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 立即 | 由於merge_preserve在預設情況下處理安全拒絕規則覆蓋給定的權限，因此需要在升級時重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 立即 | 檢測使用Html5SmartFile構件的元件，搜索內容中元件的使用實例並重新構建持久性，從而有效地將二進位檔案向下移動一個級別，而不將其儲存在元件級別。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 立即 | 從 **/etc/projects** 至 **/內容/項目** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 立即 | 將容器層引入到層次（區域）並調整參照。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 立即 | 將固定位置名稱設定為目標元件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 立即 | 對工作流模型的複雜轉換，在6.2結構、實例、通知之前進行，然後從備份位置合併回 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 立即 | 將資產、自定義元資料架構和處理配置檔案從 **/app** 至 **/conf** 並將元資料模式和元資料配置檔案表單從coral2轉換到coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 立即 | 將資產和自定義搜索小平面從 **/app** 至 **/conf** 並將元資料模式和元資料配置檔案表單從coral2轉換到coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 立即 | 更新收件箱項的排序項（調整元資料以高效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 立即 | 通過將相對路徑替換為 **/conf** 代替 **/app** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 立即 | 調整導航結構 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 立即 | 將監控儀表板的自定義配置從 **/libs** 和 **/app** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 立即 | 轉換Assets中的processingProfile屬性（使用到6.1），以匹配6.3及更高版本的結構。 還將配置檔案的相對路徑調整為 **/conf** 代替 **/app**。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 立即 | 升級任務，在升級時刪除過時的CRXDE Lite和Web Console菜單項。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延遲 | 移動SRP雲配置、社區監視字配置、清理 **/etc/social** 和 **/etc/enablement** （運行延遲遷移時需要調整任何引用和資料 — 任何應用程式部分都不應再依賴於此結構）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延遲 | 清理 **/etc/cloudsettings** （包含ContextHub配置）。 配置在第一次訪問時自動遷移。 如果啟動了「懶惰內容遷移」並在中升級此內容 **/etc/cloudsettings** 必須在升級前通過包進行保留並重新安裝，以便隱式轉換開始，並在完成後卸載包。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延遲 | 將舊標題結構調整為用戶配置檔案節點中的標題。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延遲 | 將商務內容從 **/etc/commerce** 至 **/var/commerce**。 在遷移內容期間，移動內容並更新對移動內容的引用以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延遲 | 從遷移舊目錄設定和Dynamic MediaCloud Services設定 **/etc** 至 **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延遲 | 清除現有的舊客戶端 **/etc/clientlibs** |
