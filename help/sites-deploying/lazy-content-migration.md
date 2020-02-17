---
title: 延遲內容移轉
seo-title: 延遲內容移轉
description: 瞭解AEM 6.4中的「延遲內容移轉」。
seo-description: 瞭解AEM 6.4中的「延遲內容移轉」。
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34

---


# 延遲內容移轉 {#lazy-content-migration}

為了向後相容，從AEM 6.3開始的內容和 **/etc** 和 **/content** （內容與組態）不會立即在升級時觸及或轉換。 這樣做是為了確保客戶應用程式對這些結構的依賴性保持不變。 即使AEM 6.5現成可用的內容會裝載在其他位置，與這些內容結構相關的功能仍然相同。

雖然並非所有位置都可自動轉換，但有一些延遲的位置也 `CodeUpgradeTasks` 稱為「延遲內容移轉」。 這允許客戶通過使用此系統屬性重新啟動實例來觸發這些自動轉換：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

這將導致在 `CodeUpgradeTasks` 遷移期間執行。

雖然目標是高效執行，但此升級程式是同步的，因此會根據需要處理的內容量造成停機。 建議在生產系統之前評估階段環境中的執行時間，以根據維護窗口進行規劃。

這通常也需要調整應用程式，因此應同時執行此活動以及對應的應用程式部署。

以下是6.5版中 `CodeUpgradeTasks` 的完整清單：

| **名稱** | **與舊****版AEM相關** | **移轉類****型** | **詳細資料** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 立即 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 立即 | 偵測所 `LiveRelationShips` 有已刪 `VersionStorage` 除的項目，並將排除屬性新增至父項 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 立即 | 依預設設定重新架構雲端服務以確保安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 立即 | 刪除從 **/content到/conf****** （由OSGi機制替換）的基於屬性的連結，生成相應的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 立即 | 由於merge_preserve依預設會處理保全拒絕規則會覆寫指定的權限，因此需要在升級時重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 立即 | 偵測使用Html5SmartFile介面工具集的元件，搜尋元件在內容中的使用實例並重新建構永續性，有效地將二進位檔移至下一層級，而不將其儲存在元件層級。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 立即 | 將舊式專案從 **/etc/projects移至****/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 立即 | 將容器圖層引入階層（區域）並調整參照。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 立即 | 將固定位置名稱設定為目標元件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 立即 | 對6.2結構、實例、通知之前的工作流模型進行複雜的轉換，然後從備份位置從 **/var/備份合併回來** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 立即 | 將資產、自訂中繼資料結構描述和處理描述檔從 **/apps** 移至 **/conf** ，並將中繼資料結構描述檔和中繼資料描述檔表單從coral2轉譯至coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 立即 | 將資產和自訂搜尋Facet從 **/app移至** /conf **** ，並將中繼資料架構和中繼資料描述檔表單從coral2轉換為coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 立即 | 更新收件箱項目以對收件箱項目進行排序（調整元資料以有效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 立即 | 調整資料夾上的metadataSchema屬性，方法是取代 **/conf** ，取代 **/apps的相對路徑** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 立即 | 調整導覽結構 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 立即 | 從 **/libs和****/應用程式移動監控控制面板的自訂組態** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 立即 | 轉換Assets中的processingProfile屬性（直到6.1），以符合6.3和更新版本的結構。 此外，還可調整描述檔的相對路徑 **/conf** ，以取代 **/apps**。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 立即 | 升級任務：在升級時刪除過時的CRXDE Lite和Web控制台菜單項。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延遲 | 移動SRP雲端設定、社群關注字詞設定、清除 **/etc/social和** /etc/enablement **** （執行延遲移轉時，需要調整任何參照和資料——應用程式部分不應再依據此結構）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延遲 | 清除 **/etc/cloudsettings** （包含ContextHub配置）。 設定會在第一次存取時自動移轉。 如果啟動「延遲內容移轉」並升級此內容(在 **/etc/cloudsettings中)** ，則必須在升級前透過套件保留此內容，然後重新安裝，以便隱含轉換啟動，並在完成後解除安裝此套件。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延遲 | 將舊版標題結構調整為使用者描述檔節點中的標題。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延遲 | 將商務內容從 **/etc/commerce移轉至****/var/commerce**。 移動移轉內容時，會更新移動內容的參考，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延遲 | 將舊版目錄設定和動態媒體雲端服務設定從 **/etc** 移轉至 **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延遲 | 清除存在於 **/etc/clientlibs下的舊式clientlibs** |
