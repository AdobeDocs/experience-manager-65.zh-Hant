---
title: 編譯Test計畫
seo-title: Compiling your Test Plan
description: 各個test案例合併到您的Test計畫中
seo-description: The individual test cases are amalgamated into your Test Plan
uuid: d83ef902-e0ef-4f84-9477-be12dfe91742
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 82b8a5f4-583b-47ba-9579-b47364b56aa2
docset: aem65
exl-id: ee5df2c8-ab31-4be9-8ede-3c96f26fc626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 編譯Test計畫{#compiling-your-test-plan}

然後，各個test案例將合併到您的Test計畫中，該計畫還將定義：

**優先順序**

某些test比其他人更有意義，因此最好說明其優先順序。

例如，某些test可能會影響Go/No-Go決策，因此必須在測試每個中期版本時予以確認。

**迭代**

如果項目使用任何形式的開發小版本（涉及多個版本可用），則可能需要或希望為每個小版本提供結果的指示。 這可用於指示：

* 將包含哪些test。
* test的結果在不同的迭代中重複。
* 對基本特徵的優先test和test按定期間隔重複。

**測試器**

在某一時刻，您可以指派適當的test團隊或特定的test人（可能取決於可用性和/或經驗）。

**摘要或概述**

為了報告目的，您需要提供測試結果的概述：

* 已覆蓋的test百分比。
* 成功/失敗百分比。
* 與優先test有關的具體數字。
