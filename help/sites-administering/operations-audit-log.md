---
title: 6中的審核日誌維AEM護
seo-title: Audit Log Maintenance in AEM 6
description: 瞭解有關中的審核日誌維護AEM。
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 6中的審核日誌維AEM護{#audit-log-maintenance-in-aem}

符合審AEM計日誌記錄的事件會生成大量存檔資料。 由於複製、資產上載和其他系統活動，此資料可以隨著時間的推移而快速增長。

「審核日誌維護」包括幾個功能部分，這些功能允許在特定策略下自動執行審核日誌維護。

它作為可配置的每週維護任務實施，並可通過Operations Dashboard監控控制台訪問。

有關詳細資訊，請參閱 [操作儀表板文檔](/help/sites-administering/operations-dashboard.md)。

「審核日誌清除」選項有三種類型：

1. [頁面審核日誌清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM審核日誌清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [複製審核日誌打印](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每個配置都可以通過在Web控制台中創AEM建規則來配置。 配置完它們後，您可以通過 **工具 — 操作 — 維護 — 每週維護窗口** 並運行 **AuditLog維護任務**。

## 配置頁審核日誌清除 {#configure-page-audit-log-purging}

按照以下步驟配置審核日誌清除：

1. 通過將瀏覽器指向 `http://localhost:4502/system/console/configMgr/`

1. 搜索名為 **頁面審核日誌清除規則** 點擊它。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下來，根據您的要求配置清除計畫程式。 可使用的選項包括：

   * **規則名稱：** 審計策略規則的名稱；
   * **內容路徑：** 規則將應用到的內容的路徑；
   * **最低年齡：** 需要保留審計日誌的時間（以天為單位）;
   * **審核日誌類型：** 應清除的審核日誌的類型。

   >[!NOTE]
   >
   >內容路徑僅適用於 `/var/audit/com.day.cq.wcm.core.page` 的子菜單。

1. 保存規則。
1. 您剛建立的規則需要在「操作」操控板中公開，以便執行。 為了做到這一點，請 **工具 — 操作 — 維護** 的上AEM界。

1. 按 **每週維護窗口** 卡。

1. 您將在 **AuditLog維護任務** 卡。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以檢查下次執行的日期、配置它，或通過按播放按鈕手動執行它。

在AEM6.3中，如果計畫維護窗口在「審核日誌清除」任務完成之前關閉，則任務將自動停止。 下次維護窗口開啟時，它將恢復。

**6AEM.5**，可通過按一下 **停止** 表徵圖 下次執行時，任務將安全恢復。

>[!NOTE]
>
>停止維護任務意味著暫停其執行，而不丟失已在進行中的作業的跟蹤。

## 配置DAM審核日誌清除 {#configure-dam-audit-log-purging}

1. 導航至System Console（系統控制台） *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 搜索 **DAM審核日誌清除** 規則，然後按一下結果。
1. 在下一個窗口中，相應地配置規則。 選項包括：

   * **規則名稱：** 審計策略規則的名稱；
   * **內容路徑：** 規則將應用到的內容的路徑
   * **最低年齡：** 需要保留審核日誌的時間（以天為單位）
   * **審核日誌資料庫事件類型：** 應清除的DAM審核事件的類型。

1. 按一下 **保存** 保存配置

## 配置複製審核日誌清除  {#configure-replication-audit-log-purging}

1. 導航至System Console（系統控制台） *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 搜索 **複製審核日誌清除計畫程式** 並按一下結果
1. 在下一個窗口中，相應地配置規則。 選項包括：

   * **規則名稱：** 審計策略規則的名稱
   * **內容路徑：** 規則將應用到的內容的路徑
   * **最低年齡：** 需要保留審核日誌的時間（以天為單位）
   * **審核日誌複製事件類型：** 應清除的複製審核事件的類型

1. 按一下 **保存** 保存配置。
