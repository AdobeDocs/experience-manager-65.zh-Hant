---
title: 正在同步目錄
seo-title: Synchronizing directories
description: 瞭解如何使用手動或計畫同步將用戶管理資料庫與對源目錄伺服器所做的更改同步。
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

# 正在同步目錄 {#synchronizing-directories}

要同步域，您可以選擇手動或計畫同步。 A *手動同步* 同步任何選定域。 A *調度同步* 同步所有域。

目錄同步用於將您在目錄設定中指定的目錄伺服器的詳細資訊納入用戶管理資料庫。 以後，如果目錄伺服器上發生更改或更新，也可以手動同步。 例如，如果添加了用戶和組或更改了用戶帳戶，則可以手動同步。

您還可以設定每日同步計畫，以自動將用戶管理資料庫與源目錄伺服器的更改或更新同步。 但請注意，此過程使用網路和伺服器資源。 選擇使用率較低的時間段，並避免安排不必要的同步，從而將系統和網路資源關聯起來。 要最小化不必要的同步，請改用「立即同步」選項。

還可以指定在同步域時是否將用戶和組資訊推送到AdobeLiveCycleContent Services 9（不建議使用）。

>[!NOTE]
>
>在LDAP目錄同步過程中不要建立多個本地用戶和組。 嘗試此進程可能會導致錯誤。

>[!NOTE]
>
>如果域同步進程被中斷（例如，應用程式伺服器在進程期間被關閉），請等待一段時間，然後再嘗試同步域。 要評估同步的狀態，請查看該狀態。 如果用戶管理在關閉之前獲取了鎖，請等待10分鐘，以便在伺服器重新啟動後釋放鎖。 如果同步狀態為「正在進行」，但同步被中斷或停止，則用戶管理將在3分鐘後重試同步。 嘗試三次失敗後，用戶管理會聲明同步失敗並釋放鎖。

>[!NOTE]
>
>Adobe®LiveCycle®內容服務ES（已棄用）是安裝有LiveCycle的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 Content Services（已棄用）支援在12/31/2014結束。 請參閱 [Adobe產品生命週期文檔](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。

## 啟用增量目錄同步 {#enable-delta-directory-synchronization}

增量目錄同步提高了目錄同步的效率。 啟用增量目錄同步後，用戶管理將僅同步自上次同步以來添加或更新的用戶和組。

啟用增量目錄同步時，用戶管理將執行以下步驟：

* 從目錄伺服器獲取所有用戶，但只使用時間戳已更改的用戶更新用戶管理資料庫。
* 獲取所有組，但只使用時間戳已更改的組更新用戶管理資料庫。
* 僅為時間戳已更改的組提取組成員，並使用該資訊更新用戶管理資料庫。

>[!NOTE]
>
>從目錄中刪除的用戶和組在執行完整目錄同步之前不會從用戶管理資料庫中刪除。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 在「增量同步」(Delta Synch)下，選中複選框，然後按一下「保存」(Save)。
1. 編輯將使用增量目錄同步功能的每個企業域的目錄設定。 在「用戶設定」和「組設定」頁上，找到「修改時間戳」設定並輸入 `modify TimeStamp` 值。 有關編輯企業域的詳細資訊，請參閱 [編輯和轉換現有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)。

## 在同步期間啟用或禁用詳細記錄 {#enable-or-disable-detailed-logging-during-synchronization}

預設情況下，用戶管理會在同步過程中記錄詳細的統計資訊。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「配置高級系統屬性」。
1. 在「同步統計記錄」下，取消選中複選框以禁用詳細記錄，或選擇它以啟用記錄，然後按一下保存。

## 配置目錄同步重試選項 {#configure-the-directory-synchronization-retry-option}

您可以配置用戶管理以定期檢查是否有失敗的目錄同步嘗試。 然後，用戶管理會嘗試完成失敗的同步。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「配置高級系統屬性」。
1. 在同步分頁裝訂器Cron表達式下，輸入cron表達式，該表達式表示用戶管理重試失敗同步的間隔。 cron表達式的使用基於Quartz開源作業調度系統1.4.0版。

   預設值為0 0/13 &amp;ast;? &amp;ast;這意味著每13分鐘檢查一次。

## 手動同步目錄 {#manually-synchronize-directories}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. （可選）要將用戶和組資訊推送到Content Services（已棄用），請選擇「選擇此選項以將用戶和組推入註冊的外部主體儲存提供程式」選項。 通過「用戶和組」頁添加新用戶和組時，此選項也適用。
1. 選中要同步的每個企業域的複選框，然後按一下「立即同步」。

   如果選擇多個域，則可以同時運行所有域的域同步。 但是，如果單獨選擇域，則一次只能運行一個域同步。

## 計畫目錄同步 {#schedule-directory-synchronization}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 計畫同步：

   * 要每天啟用自動同步，請在「計畫程式」下選擇「發生」。 從清單中選擇「每日」，然後在相應框中鍵入24小時格式的時間。 保存設定時，此值將轉換為cron表達式，該表達式顯示在「cron表達式」(Cron Expression)框中。
   * 要安排在一週或月的特定日或特定月的同步，請選擇「Cron表達式」，然後在框中鍵入相應的表達式。 例如，在凌晨1:30同步。在本月最後一個星期五。

cron表達式的使用基於Quartz開源作業調度系統1.4.0版。

* 要關閉自動同步，請選擇「發生」，然後從清單中選擇「從不」。
* （可選）要將用戶和組資訊推送到Content Services（已棄用），請選擇「選擇此選項以將用戶和組推入註冊的外部主體儲存提供程式」選項。 通過「用戶和組」頁添加新用戶和組時，此選項也適用。
* 按一下「儲存」。

## 停止當前正在進行的所有目錄同步 {#stop-all-directory-synchronizations-currently-in-progress}

1. 在管理控制台中，按一下「設定」>「用戶管理」>「域管理」。
1. 按一下「中止」。 僅當目錄同步正在進行時才顯示此按鈕。
