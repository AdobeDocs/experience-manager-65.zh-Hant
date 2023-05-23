---
title: 需要哪些Test環境？
seo-title: Which Test Environments are needed?
description: 應將幾個環境視為測試的一部分
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 需要哪些Test環境？{#which-test-environments-will-be-needed}

要定義測試的配置，應考慮以下內容：

**開發**  — 用於Unit和某些整合test。

**測試**  — 大多數test。

**實況**  — 用於最終效能和壓力test。 也用於與客戶的接受test。

您還需要確定需要哪些實例（通常每個實例中至少有一個用於所有測試級別）:

**作者**  — 此實例允許作者輸入和發佈內容。

**發佈**  — 此實例以其發佈的形式顯示網站供訪問者訪問。

應與Dispatcher一起測試。

最後，必須考慮實際硬體 — 任何效能test都應在與最終即時環境盡可能接近的配置中對系統進行。 因此，還建議將項目啟動拆分為：

**軟啟動**  — 降低可用性；它允許在生產環境的實際條件下進行效能test、調整和優化。

**硬啟動**  — 完全可用。
