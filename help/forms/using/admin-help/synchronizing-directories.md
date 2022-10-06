---
title: 同步目錄
seo-title: Synchronizing directories
description: 了解如何使用手動或計畫同步將用戶管理資料庫與源目錄伺服器的更改同步。
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 2a2f8538b6554540b546f4d345c0b3c0d3e706f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# 同步目錄 {#synchronizing-directories}

要同步域，您可以選擇執行手動或計畫的同步。 A *手動同步* 同步任何選定域。 A *排程同步* 同步所有域。

目錄同步用於將您在目錄設定中指定的目錄伺服器的詳細資訊提取到用戶管理資料庫中。 之後，如果目錄伺服器上發生更改或更新，您也可以手動同步。 例如，如果新增了使用者和群組或對使用者帳戶進行了變更，則可以執行手動同步。

您還可以設定每日同步計畫以自動同步用戶管理資料庫與源目錄伺服器的更改或更新。 但請注意，此程式使用網路和伺服器資源。 選擇使用率較低的時段，並避免安排系結系統和網路資源的不必要的同步。 要盡量減少不必要的同步，請改用立即同步選項。

您也可以指定在同步網域時是否將使用者和群組資訊推送至AdobeLiveCycleContent Services 9（已淘汰）。

>[!NOTE]
>
>在進行LDAP目錄同步時，請勿建立多個本地用戶和組。 嘗試此程式可能會導致錯誤。

>[!NOTE]
>
>如果域同步進程被中斷（例如，在進程期間關閉應用程式伺服器），請等待一段時間，然後再嘗試同步該域。 要評估同步的狀態，請查看狀態。 如果用戶管理在關閉前獲得了鎖，請等待10分鐘，以便在伺服器重新啟動後釋放鎖。 如果同步狀態為「正在進行」，但同步被中斷或中止，則用戶管理將在3分鐘後重試同步。 在三次嘗試失敗後，User Management會將同步聲明為失敗並釋放鎖。

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（已過時）是隨LiveCycle安裝的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 內容服務（已過時）支援將於12/31/2014終止。 請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## 啟用增量目錄同步 {#enable-delta-directory-synchronization}

增量目錄同步提高了目錄同步的效率。 啟用增量目錄同步時，用戶管理僅同步自上次同步以來已添加或更新的用戶和組。

啟用增量目錄同步時，用戶管理將執行以下步驟：

* 從目錄伺服器中獲取所有用戶，但只更新時間戳已更改的用戶的用戶管理資料庫。
* 擷取所有群組，但僅更新時間戳記已變更的群組的使用者管理資料庫。
* 僅為時間戳已更改的組提取組成員，並使用該資訊更新用戶管理資料庫。

>[!NOTE]
>
>在執行完整目錄同步之前，從目錄中刪除的用戶和組不會從用戶管理資料庫中刪除。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在「增量同步」(Delta Synch)下，選中複選框，然後按一下「保存」(Save)。
1. 編輯將使用增量目錄同步功能的每個企業域的目錄設定。 在「用戶設定」和「組設定」頁上，找到「修改時間戳」設定並輸入 `modify TimeStamp` 作為值。 如需編輯企業網域的詳細資訊，請參閱 [編輯和轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## 在同步期間啟用或禁用詳細記錄 {#enable-or-disable-detailed-logging-during-synchronization}

依預設，使用者管理會記錄同步程式期間的詳細統計資料。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「配置高級系統屬性」。
1. 在「同步統計記錄」下，取消選中複選框以禁用詳細記錄，或選擇它以啟用記錄，然後按一下「保存」。

## 配置目錄同步重試選項 {#configure-the-directory-synchronization-retry-option}

您可以配置「用戶管理」以定期檢查是否有任何失敗的目錄同步嘗試。 然後，「用戶管理」將嘗試完成失敗的同步。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「配置高級系統屬性」。
1. 在「同步分頁裝訂器Cron表達式」下，輸入一個cron表達式，該表達式表示用戶管理重試失敗同步的間隔。 cron表達式的使用基於Quartz開放源作業調度系統1.4.0版。

   預設值為0 0/13 &amp;ast;? &amp;ast;，這表示每13分鐘會進行一次檢查。

## 手動同步目錄 {#manually-synchronize-directories}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. （可選）若要將使用者和群組資訊推送至內容服務（已淘汰），請選取此選項，將使用者和群組推送至已註冊的外部主要儲存提供者選項。 透過「使用者和群組」頁面新增使用者和群組時，也適用此選項。
1. 為要同步的每個企業域選擇複選框，然後按一下「立即同步」。

   如果選擇多個域，則可以同時運行所有域的域同步。 但是，如果單獨選擇域，則一次只能運行一個域同步。

## 計畫目錄同步 {#schedule-directory-synchronization}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 計畫同步：

   * 要每天啟用自動同步，請在「調度程式」下，選擇「發生」。 從清單中選取「每日」，並在對應方塊中以24小時格式輸入時間。 儲存設定時，此值會轉換為cron運算式，而該運算式會顯示在「cron運算式」方塊中。
   * 若要排程一週或月的特定日或特定月的同步，請選取「Cron運算式」，並在方塊中輸入適當的運算式。 例如，在該月最後一個星期五的凌晨1:30進行同步。

cron表達式的使用基於Quartz開放源作業調度系統1.4.0版。

* 要關閉自動同步，請選擇「發生」並從清單中選擇「從不」。
* （可選）若要將使用者和群組資訊推送至內容服務（已淘汰），請選取此選項，將使用者和群組推送至已註冊的外部主要儲存提供者選項。 透過「使用者和群組」頁面新增使用者和群組時，也適用此選項。
* 按一下「儲存」。

## 停止當前正在進行的所有目錄同步 {#stop-all-directory-synchronizations-currently-in-progress}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「中止」。 只有在進行目錄同步時，才會顯示此按鈕。
