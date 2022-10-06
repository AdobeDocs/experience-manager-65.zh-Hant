---
title: AEM 6中的稽核記錄維護
seo-title: Audit Log Maintenance in AEM 6
description: 了解AEM中的稽核記錄維護。
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

# AEM 6中的稽核記錄維護{#audit-log-maintenance-in-aem}

符合稽核記錄資格的AEM事件會產生大量封存資料。 由於複製、資產上傳和其他系統活動，此資料可能會隨著時間而快速增長。

「審核日誌維護」包括幾個功能部分，這些功能允許在特定策略下自動執行審核日誌維護。

它作為可配置的每週維護任務實施，並可通過Operations Dashboard監視控制台訪問。

如需詳細資訊，請參閱 [操作儀表板文檔](/help/sites-administering/operations-dashboard.md).

審核日誌清除選項有三種類型：

1. [頁面稽核記錄清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM稽核記錄清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [複製審核日誌更新](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每個選項都可在AEM Web Console中建立規則來設定。 設定完成後，您可以前往 **工具 — 工序 — 維護 — 每週維護窗口** 並執行 **審核日誌維護任務**.

## 配置頁面審核日誌清除 {#configure-page-audit-log-purging}

請依照下列步驟來設定稽核記錄清除：

1. 將瀏覽器指向 `http://localhost:4502/system/console/configMgr/`

1. 搜尋名為 **頁審核日誌清除規則** 然後按一下。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下來，根據您的需求配置清除計畫程式。 可使用的選項包括：

   * **規則名稱：** 審計策略規則的名稱；
   * **內容路徑：** 規則要套用的內容路徑；
   * **最低年齡：** 需要保留審計日誌的時間（以天為單位）;
   * **審核日誌類型：** 應清除的稽核記錄類型。

   >[!NOTE]
   >
   >內容路徑僅適用於 `/var/audit/com.day.cq.wcm.core.page` 儲存庫中的節點。

1. 儲存規則。
1. 您剛建立的規則必須公開在「操作控制面板」中，才能執行。 為了這樣，請 **工具 — 操作 — 維護** 從AEM歡迎畫面。

1. 按下 **每週維護窗口** 卡片。

1. 您會在 **審核日誌維護任務** 卡片。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以檢查下次執行的日期、進行設定，或按播放按鈕手動執行。

在AEM 6.3中，如果計畫維護窗口在「審核日誌清除」任務完成之前關閉，則任務將自動停止。 下次維護視窗開啟時，就會繼續。

**使用AEM 6.5**，您可以按一下 **停止** 表徵圖。 在下次執行時，該任務將安全地恢復。

>[!NOTE]
>
>停止維護任務意味著暫停其執行，而不丟失已在進行中的作業的跟蹤。

## 設定DAM稽核記錄清除 {#configure-dam-audit-log-purging}

1. 導覽至系統主控台(位於 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 搜尋 **DAM審核日誌清除** 規則，然後按一下結果。
1. 在下一個視窗中，依此設定您的規則。 選項為：

   * **規則名稱：** 審計策略規則的名稱；
   * **內容路徑：** 規則將套用至的內容路徑
   * **最低年齡：** 需要保留審核日誌的時間（以天為單位）
   * **審核日誌Dam事件類型：** 應清除的DAM稽核事件類型。

1. 按一下 **儲存** 保存配置

## 配置複製審核日誌清除  {#configure-replication-audit-log-purging}

1. 導覽至系統主控台(位於 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 搜尋 **複製審核日誌清除調度程式** 然後按一下結果
1. 在下一個視窗中，依此設定您的規則。 選項為：

   * **規則名稱：** 審計策略規則的名稱
   * **內容路徑：** 規則將套用至的內容路徑
   * **最低年齡：** 需要保留審核日誌的時間（以天為單位）
   * **審核日誌複製事件類型：** 應清除的複製審核事件類型

1. 按一下 **儲存** 以儲存您的設定。
