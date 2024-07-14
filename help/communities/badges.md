---
title: 徽章主控台
description: 「社群徽章」主控台可讓您新增自訂徽章，當成員贏取（授予）或在社群中擔任特定角色（已指派）時顯示徽章
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# 徽章主控台 {#badges-console}

## 關於徽章 {#about-badges}

「社群徽章」主控台可讓您新增自訂徽章，當成員贏取（授予）或在社群中擔任特定角色（已指派）時，徽章會針對該成員顯示。

### 徽章可見性 {#badge-visibility}

目前，社群成員獲得或指派的徽章會與其名稱和頭像一起顯示在以下位置：

* 設定檔
* [論壇](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [創意力](/help/communities/ideation-feature.md)

在作者環境中，導覽至「徽章」主控台：

* 從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 徽章]**

此主控台顯示目前可用的徽章，以及可以新增徽章的來源。

![徽章 — 首頁](assets/badges-homepage.png)

## 建立預算 {#create-badge}

徽章是藉由上傳適當小影像（高度範圍從26到32畫素的72 dpi）並提供名稱來建立。 徽章影像儲存在`/libs/settings/community/badging/images`的存放庫中，並自動復寫到發佈環境。

如果發佈環境是發行者的陣列，則必須設定[使用者同步](/help/communities/sync.md)。

![建立徽章](assets/create-badge.png)

* **上傳影像**

  （*必要*）徽章影像，建議大小為32 x 32畫素，以72 dpi為JPEG或PNG格式。

* **名稱**

  （*必要*）徽章名稱。 這是預設`Display Name`和存放庫節點名稱。 如果`Name`不是有效的存放庫節點名稱，則會修改它。

* **顯示名稱**

  （*選擇性*）使用者介面中為徽章顯示的名稱。 預設值是為`Name`輸入的未變更文字。

* **說明**

  （*選擇性*）徽章的說明。

## 其他資訊 {#additional-information}

如需設定評分與徽章規則的詳細資訊，請參閱[評分與徽章](/help/communities/implementing-scoring.md)。

若要管理成員的徽章，請參閱[成員主控台](/help/communities/members.md)。
