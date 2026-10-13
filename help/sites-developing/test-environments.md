---
title: 需要哪些測試環境？
description: 在測試中應考慮幾個環境
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%
---
# 需要哪些測試環境？{#which-test-environments-will-be-needed}

若要定義要測試的設定，您應考量下列事項：

**開發** — 適用於單位和某些整合測試。

**測試** — 適用於大部分測試。

**即時** — 進行最終效能和壓力測試。 也用於和客戶的驗收測試。

決定您需要哪些執行個體以及執行個體的位置（通常是所有測試層級各至少一個）：

**作者** — 此執行個體可讓作者輸入及發佈內容。

**發佈** — 此執行個體會以已發佈的形式顯示網站，以供訪客存取。

透過Dispatcher測試。

最後，必須考量實際的硬體 — 任何效能測試都應在儘可能接近最終上線環境的組態中進行。 因此，我們也建議將Project Launch分割為：

**軟啟動** — 降低可用性；可在實際生產環境中進行效能測試、調校和最佳化所需的時間。

**硬式啟動** — 完整可用性。
