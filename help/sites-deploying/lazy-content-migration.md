---
title: 延遲內容移轉
seo-title: 延遲內容移轉
description: 了解AEM 6.4中的延遲內容移轉。
seo-description: 了解AEM 6.4中的延遲內容移轉。
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: 升級
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 6%

---

# 延遲內容移轉{#lazy-content-migration}

為了回溯相容性，從AEM 6.3開始的&#x200B;**/etc**&#x200B;和&#x200B;**/content**&#x200B;中的內容和設定，在升級時不會立即接觸或轉換。 這樣做是為了確保客戶應用程式在這些結構上的依賴性保持不變。 與這些內容結構相關的功能仍相同，即使現成可用的AEM 6.5中的內容會托管在其他位置。

雖然並非所有位置都可自動轉換，但仍有一些延遲的`CodeUpgradeTasks`也稱為「延遲內容移轉」。 這可讓客戶使用此系統屬性重新啟動執行個體，以觸發這些自動轉換：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

這會導致在移轉期間執行`CodeUpgradeTasks`。

雖然目標是高效執行，但此升級過程是同步的，因此會因需要處理的內容量而導致停機。 建議在生產系統之前評估階段環境上的執行時間，以根據維護窗口進行規劃。

由於這通常也需要調整應用程式，因此應該連同對應的應用程式部署一起執行此活動。

以下是6.5中推出的`CodeUpgradeTasks`完整清單：

| **名稱** | **** **與AEM之前的版本相關** | **** **MigrationType** | **詳細資料** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5=&quot;&quot;> | 立即 |  |
| `Cq60MSMContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 檢測已刪除的`VersionStorage`中的所有`LiveRelationShips`，並將排除屬性添加到父級 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 預設設定為安全重構雲服務 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 立即 | 移除從&#x200B;**/content**&#x200B;到&#x200B;**/conf**（由OSGi機制取代）的屬性連結，並產生對應的OSGi設定 |
| `Cq62FormsContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 由於merge_preserve預設處理安全拒絕規則會覆寫指定的權限，導致需要在升級時重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 檢測使用Html5SmartFile介面工具集的元件，在內容中搜索元件的用法並重構持久性，有效地將二進位移到下一級，而不將其儲存在元件級。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 將舊樣式項目從&#x200B;**/etc/projects**&#x200B;移動到&#x200B;**/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 將容器層引入層次結構（區域），並調整參照。 |
| `Cq62TargetContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 將固定位置名稱設定為目標元件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 在6.2結構、實例、通知之前對工作流模型進行複雜的轉換，然後從&#x200B;**/var/backup**&#x200B;中的備份位置進行合併 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 立即 | 將資產、自訂中繼資料結構和處理設定檔從&#x200B;**/apps**&#x200B;移至&#x200B;**/conf**，並將中繼資料結構和中繼資料描述檔表單從coral2轉譯至coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6=&quot;&quot;> | 立即 | 將資產和自訂搜尋Facet從&#x200B;**/apps**&#x200B;移至&#x200B;**/conf**，並將中繼資料結構和中繼資料描述檔表單從coral2轉譯至coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 更新收件箱項以排序收件箱項（調整元資料以有效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6=&quot;&quot;> | 立即 | 借由將相對路徑取代為&#x200B;**/apps**&#x200B;以調整資料夾上的metadataSchema屬性&#x200B;**** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 調整導覽結構 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6=&quot;&quot;> | 立即 | 從&#x200B;**/libs**&#x200B;和&#x200B;**/apps**&#x200B;移動監控控制面板的自訂配置 |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6=&quot;&quot;> | 立即 | 轉譯Assets中的processingProfile屬性（使用至6.1），以符合6.3和更新的結構。 也會將設定檔的相對路徑調整為&#x200B;**/conf**，以取代&#x200B;**/apps**。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6=&quot;&quot;> | 立即 | 升級任務，在升級時刪除過時的CRXDE Lite和Web控制台菜單項。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6=&quot;&quot;> | 延遲 | 移動SRP雲端設定、社群關注字設定、清除&#x200B;**/etc/social**&#x200B;和&#x200B;**/etc/enablement**（執行延遲移轉時需要調整任何參考和資料 — 應用程式部分不再取決於此結構）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6=&quot;&quot;> | 延遲 | 清除&#x200B;**/etc/cloudsettings**（包含ContextHub配置）。 設定會在首次存取時自動移轉。 如果啟動延遲內容遷移並升級&#x200B;**/etc/cloudsettings**&#x200B;中的此內容，則必須在升級前通過包保留並重新安裝，以便隱式轉換開始，並在完成後卸載該包。 |
| `CQ64UsersTitleFixTask` | &lt; 6=&quot;&quot;> | 延遲 | 將舊版標題結構調整為使用者設定檔節點中的標題。 |
| `CQ64CommerceMigrationTask` | &lt; 6=&quot;&quot;> | 延遲 | 將商務內容從&#x200B;**/etc/commerce**&#x200B;移轉至&#x200B;**/var/commerce**。 移動移轉內容期間，會更新對移動內容的參考，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6=&quot;&quot;> | 延遲 | 將舊版目錄設定和Dynamic MediaCloud Services設定從&#x200B;**/etc**&#x200B;移轉至&#x200B;**/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6=&quot;&quot;> | 延遲 | 清除&#x200B;**/etc/clientlibs**&#x200B;下現有的舊版clientlibs |
