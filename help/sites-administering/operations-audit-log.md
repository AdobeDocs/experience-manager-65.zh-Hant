---
title: AEM 6中的稽核記錄維護
seo-title: AEM 6中的稽核記錄維護
description: 瞭解AEM中的「稽核記錄維護」。
seo-description: 瞭解AEM中的「稽核記錄維護」。
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# AEM 6中的稽核記錄維護{#audit-log-maintenance-in-aem}

符合稽核記錄資格的AEM事件會產生許多封存資料。 由於複製、資產上傳和其他系統活動，這些資料會隨著時間快速增長。

Audit Log Maintenance包括幾個功能部分，可讓您在特定原則下自動執行審核記錄維護。

它實作為可配置的每週維護任務實施，並可通過Operations Dashboard監控控制台訪問。

如需詳細資訊，請參閱「 [Operations Dashboard檔案」](/help/sites-administering/operations-dashboard.md)。

審核日誌清除選項有三種類型：

1. [頁面審核日誌清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM審核日誌清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [複製審核日誌更新](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每個設定都可在AEM Web Console中建立規則。 在配置完它們後，您可以通過轉到 **Tools - Operations - Maintenance - Weekly Maintenance Window** ，並運行 **AuditLog Maintenance Task來觸發它們**。

## 配置頁面審核日誌清除 {#configure-page-audit-log-purging}

請遵循下列步驟，以配置審核日誌清除：

1. 前往「Web Console管理」，方法是將您的瀏覽器指向 `http://localhost:4502/system/console/configMgr/`

1. 搜索名為「頁面」 **審計日誌清除規則的項目** ，然後按一下它。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接著，根據您的要求配置清除調度程式。 可用的選項包括：

   * **** 規則名稱：審計策略規則的名稱；
   * **** 內容路徑：規則所套用內容的路徑；
   * **** 最低年齡：需要保存審計日誌的時間（以天為單位）;
   * **** 審計日誌類型：應清除的審核日誌類型。
   >[!NOTE]
   >
   >內容路徑僅適用於儲存庫中節 `/var/audit/com.day.cq.wcm.core.page` 點的子節點。

1. 儲存規則。
1. 您剛建立的規則必須在「作業控制面板」中公開，才能執行。 若要這麼做，請從「AEM歡迎」畫 **面前往「工具** -作業——維護」。

1. 按「 **Weekly Maintenance Window** （每週維護窗口）」卡。

1. 您將在AuditLog Maintenance Task卡下找到已存在的 **維護任務** 。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以檢查下次執行的日期、進行設定，或按播放按鈕手動執行。

在AEM 6.3中，如果排程的維護視窗在「稽核記錄清除」工作完成之前關閉，則工作會自動停止。 下次維護視窗開啟時，它會繼續。

**使用AEM 6.5**，您可以按一下「停止」圖示，手動停止執行中的「稽核記錄清除 **工作** 」。 在下次執行時，任務將安全恢復。

>[!NOTE]
>
>停止維護任務意味著暫停其執行，而不丟失對已在進行中的作業的跟蹤。

## 配置DAM審核日誌清除 {#configure-dam-audit-log-purging}

1. 導覽至位於https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr的 *系統控制台*
1. 搜索 **DAM審計日誌清除規則** ，然後按一下結果。
1. 在下一個視窗中，請據以設定您的規則。 選項包括：

   * **** 規則名稱：審計策略規則的名稱；
   * **** 內容路徑：規則將套用至的內容路徑
   * **** 最低年齡：需要保留審核日誌的時間（以天為單位）
   * **** 審計日誌Dam事件類型：應清除的DAM審計事件類型。

1. 按一 **下「儲存** 」以儲存您的設定

## 配置複製審核日誌清除 {#configure-replication-audit-log-purging}

1. 導覽至位於https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr的 *系統控制台*
1. 搜索復 **制審計日誌清除調度程式** ，然後按一下結果
1. 在下一個視窗中，請據以設定您的規則。 選項包括：

   * **** 規則名稱：審計策略規則的名稱
   * **** 內容路徑：規則將套用至的內容路徑
   * **** 最低年齡：需要保留審核日誌的時間（以天為單位）
   * **** 審計日誌複製事件類型：應清除的複製審核事件類型

1. 按一 **下「儲存** 」以儲存您的設定。

