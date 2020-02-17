---
title: 需要哪些測試環境？
seo-title: 需要哪些測試環境？
description: 測試時應考慮使用多種環境
seo-description: 測試時應考慮使用多種環境
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 需要哪些測試環境？{#which-test-environments-will-be-needed}

要定義測試的配置，您應考慮以下事項：

**開發** -針對設備和某些整合測試。

**測試** -適用於大多數測試。

**即時** -用於最終效能和壓力測試。 也適用於客戶的驗收測試。

您也需要決定您需要哪些執行個體（通常每個執行個體中至少有一個執行個體，用於所有測試層級）:

**作者** -此例項可讓作者輸入和發佈內容。

**Publish** —— 此例項以其發佈的表單呈現網站，供訪客存取。

應與Dispatcher一起測試。

最後，必須考慮實際硬體——應盡可能在接近最終即時環境的配置中對系統進行任何效能測試。 因此，建議將「專案啟動」分割為：

**軟啟動** -降低可用性；這為生產環境的實際條件下的效能測試、調整和優化提供了時間。

**硬啟動** -完全可用。
