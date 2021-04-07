---
title: 6中的審核日誌維護AEM
seo-title: 6中的審核日誌維護AEM
description: 瞭解中的審計日誌維護AEM。
seo-description: 瞭解中的審計日誌維護AEM。
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: 運作
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# 6{#audit-log-maintenance-in-aem}中AEM的審核日誌維護

符合審AEM核記錄資格的事件會產生許多封存資料。 由於複製、資產上傳和其他系統活動，這些資料會隨著時間快速增長。

Audit Log Maintenance包括幾個功能部分，可讓您在特定原則下自動執行審核記錄維護。

它實作為可配置的每週維護任務實施，並可通過Operations Dashboard監控控制台訪問。

有關詳細資訊，請參閱[操作儀表板文檔](/help/sites-administering/operations-dashboard.md)。

審核日誌清除選項有三種類型：

1. [頁面審核日誌清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM審核日誌清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [複製審核日誌更新](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每項設定皆可在Web主控台中建AEM立規則。 在配置完這些檔案後，您可以通過轉到&#x200B;**工具——操作——維護——每週維護窗口**&#x200B;並運行&#x200B;**審計日誌維護任務**&#x200B;來觸發它們。

## 配置頁面審核日誌清除{#configure-page-audit-log-purging}

請遵循下列步驟，以配置審核日誌清除：

1. 將您的瀏覽器指向`http://localhost:4502/system/console/configMgr/`，前往「Web Console管理」

1. 搜索名為&#x200B;**頁審計日誌清除規則**&#x200B;的項目，然後按一下它。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接著，根據您的要求配置清除調度程式。 可用的選項包括：

   * **規則名稱：** 審計策略規則的名稱；
   * **內容路徑：** 規則要套用至之內容的路徑；
   * **最低年齡：** 需要保存審計日誌的時間（以天為單位）;
   * **審核日誌類** 型：應清除的審核日誌類型。

   >[!NOTE]
   >
   >內容路徑僅適用於儲存庫中`/var/audit/com.day.cq.wcm.core.page`節點的子節點。

1. 儲存規則。
1. 您剛建立的規則必須在「作業控制面板」中公開，才能執行。 為此，請從「歡迎」螢幕中轉至「工具——操作——維護」AEM。****

1. 按&#x200B;**每週維護窗口**&#x200B;卡。

1. 您將在&#x200B;**AuditLog Maintenance Task**&#x200B;卡下找到已存在的維護任務。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以檢查下次執行的日期、進行設定，或按播放按鈕手動執行。

在AEM6.3中，如果計畫維護窗口在「審核日誌清除」任務完成之前關閉，則任務將自動停止。 下次維護視窗開啟時，它會繼續。

**使用AEM6.5**，您可以通過按一下「停止」表徵圖手動停止正在運行的審核日誌清除 **** 任務。在下次執行時，任務將安全恢復。

>[!NOTE]
>
>停止維護任務意味著暫停其執行，而不丟失對已在進行中的作業的跟蹤。

## 配置DAM審核日誌清除{#configure-dam-audit-log-purging}

1. 導覽至位於&#x200B;*https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*&#x200B;的系統控制台
1. 搜索&#x200B;**DAM審計日誌清除**&#x200B;規則，然後按一下結果。
1. 在下一個視窗中，請據以設定您的規則。 選項包括：

   * **規則名稱：** 審計策略規則的名稱；
   * **內容路徑：** 規則要套用至之內容的路徑
   * **最低年齡：** 需要保留審核日誌的時間（以天為單位）
   * **稽核記錄檔Dam事件類** 型：應清除的DAM稽核事件類型。

1. 按一下&#x200B;**保存**&#x200B;保存配置

## 配置複製審核日誌清除{#configure-replication-audit-log-purging}

1. 導覽至位於&#x200B;*https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*&#x200B;的系統控制台
1. 搜索&#x200B;**複製審計日誌清除調度程式**&#x200B;並按一下結果
1. 在下一個視窗中，請據以設定您的規則。 選項包括：

   * **規則名稱：** 審計策略規則的名稱
   * **內容路徑：** 規則要套用至之內容的路徑
   * **最低年齡：** 需要保留審核日誌的時間（以天為單位）
   * **審核日誌複製事件類** 型：應清除的複製審核事件類型

1. 按一下&#x200B;**保存**&#x200B;保存配置。
