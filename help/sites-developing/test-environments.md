---
title: 需要哪些測試環境？
description: 在測試中應考慮幾個環境
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 需要哪些測試環境？{#which-test-environments-will-be-needed}

若要定義要測試的設定，您應考量下列事項：

**開發**  — 適用於單位和某些整合測試。

**測試**  — 適用於大部分的測試。

**即時**  — 進行最終效能與壓力測試。 也用於和客戶的驗收測試。

決定您需要哪些執行個體以及執行個體的位置（通常是所有測試層級各至少一個）：

**作者**  — 此例項可讓作者輸入及發佈內容。

**發佈**  — 此執行個體會以已發佈的形式顯示網站，以供訪客存取。

已使用Dispatcher進行測試。

最後，必須考量實際的硬體 — 任何效能測試都應在儘可能接近最終上線環境的組態中進行。 因此，我們也建議將Project Launch分割為：

**軟啟動**  — 降低可用性；可在實際生產環境中進行效能測試、調校和最佳化所需的時間。

**硬啟動**  — 完整可用性。
