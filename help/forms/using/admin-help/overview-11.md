---
title: Overview of Health Monitor
seo-title: Overview of Health Monitor
description: 本檔案提供健康狀況監視程式的概述，以及如何存取它的詳細資訊。
seo-description: 本檔案提供健康狀況監視程式的概述，以及如何存取它的詳細資訊。
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Overview of Health Monitor {#overview-of-health-monitor}

Health Monitor提供有關AEM表單系統的重要資訊，例如伺服器資訊、記憶體使用狀況和處理器使用狀況。 此外，還提供了Work manager統計資訊，如隊列中的工作項目或作業數及其狀態。 您可以使用Health Monitor執行以下任務：

* 驗證系統是否正常運行
* 查看資訊，幫助診斷系統問題
* 對顯示問題的工作項或任務執行操作
* 從作業管理器資料庫中清除過時記錄

管理控制台中的「Health Monitor」（運行狀況監視程式）頁面有三個頁籤：

* 「系統」頁籤顯示資源監視圖表和有關表單伺服器（或群集環境中的節點）的資訊。 (請參閱 [查看系統資訊](/help/forms/using/admin-help/view-system-information.md#view-system-information)。)
* 「工作管理器」頁籤顯示與「工作管理器」相關的資料，如「工作管理器」隊列中的工作項數。 您可以使用各種標準來篩選資訊，或使用操作工具管理單個工作項目。 (請參 [閱查看與Work manager相關的統計資訊](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)。)
* 通過「作業清除調度程式」頁籤，您可以從作業管理器資料庫中清除過時記錄。 (請參 [閱從作業管理器資料庫清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)。)

Health Monitor網頁會填入透過Gemfire API收集的統計資料。 此API會自動發現群集中的所有節點。 它也可解決從代理伺服器或負載平衡器後面收集統計資料時發生的安全性問題。 Java選項可用來微調Health Monitor，降低對AEM表單環境效能的影響。 (請參 [閱Fine-tuning Health Monitor performance](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance))。

**Access Health Monitor**

1. 在管理控制台中，按一下頁面右上角的Health Monitor。

