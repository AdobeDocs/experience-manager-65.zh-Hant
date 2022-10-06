---
title: 運行狀況監視器概述
seo-title: Overview of Health Monitor
description: 本文檔提供運行狀況監視器的概述，以及有關如何訪問該監視器的詳細資訊。
seo-description: This document provides the overview of the Health monitor, and details about how you can access it.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 運行狀況監視器概述 {#overview-of-health-monitor}

運行狀況監視器提供有關AEM表單系統的關鍵資訊，如伺服器資訊、記憶體使用情況和處理器使用情況。 還提供了Work Manager統計資訊，如隊列中的工作項或作業數及其狀態。 您可以使用運行狀況監視器執行以下任務：

* 驗證系統是否正常運行
* 查看資訊，以幫助在系統問題發生時進行診斷
* 對顯示問題的工作項或作業執行操作
* 從作業管理器資料庫中清除過時記錄

管理控制台中的「運行狀況監視器」頁有三個頁簽：

* 「系統」頁簽顯示資源監視圖表和有關表單伺服器（或群集環境中的節點）的資訊。 (請參閱 [查看系統資訊](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* 「工作管理員」頁簽顯示與工作管理員相關的資料，如工作管理員隊列中的工作項數。 您可以使用各種條件來篩選資訊，或使用操作工具來管理個別工作項目。 (請參閱 [查看與Work Manager相關的統計資訊](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* 使用「作業清除調度程式」頁簽，可以從作業管理器資料庫中清除過時記錄。 (請參閱 [從作業管理員資料庫中清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

健康監視器網頁會填入透過Gemfire API收集的統計資料。 此API會自動探索叢集中的所有節點。 它也可解決從代理伺服器或負載平衡器後面收集統計資料時發生的安全問題。 Java選項可用來微調運行狀況監視器，從而減少對AEM表單環境效能的影響。 (請參閱 [微調運行狀況監視器效能](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**訪問運行狀況監視器**

1. 在管理控制台中，按一下頁面右上角的「健康監視器」。
