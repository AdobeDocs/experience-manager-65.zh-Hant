---
title: 徽章主控台
seo-title: 徽章主控台
description: 「社群徽章」控制台可讓您新增自訂徽章，這些徽章可在獲得（授予）或成員在社群中承擔特定角色（已指派）時顯示給成員
seo-description: 「社群徽章」控制台可讓您新增自訂徽章，這些徽章可在獲得（授予）或成員在社群中承擔特定角色（已指派）時顯示給成員
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# 徽章主控台 {#badges-console}

## 關於徽章 {#about-badges}

「社區徽章」控制台提供添加自定義徽章的功能，這些徽章可以在獲得（授予）成員或成員在社區中承擔特定角色（已分配）時顯示。

### 徽章可見性 {#badge-visibility}

目前，社群成員所掙得或獲指派的徽章，將與其名稱和頭像一起顯示在下列位置：

* 設定檔
* [論壇](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [創意力](/help/communities/ideation-feature.md)

在製作環境中，導覽至「徽章」主控台：

* 從全局導航：**[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 徽章]**

此主控台會顯示目前可用的徽章，以及可從中新增徽章。

![徽章 — 首頁](assets/badges-homepage.png)

## 建立預算 {#create-badge}

通過上傳合適的小影像（72dpi，高度在26-32像素之間）並提供名稱來建立徽章。 徽章影像儲存在`/libs/settings/community/badging/images`的存放庫中，並自動複製到發佈環境。

如果發佈環境是發佈者的伺服器陣列，則必須配置[用戶同步](/help/communities/sync.md)。

![建立徽章](assets/create-badge.png)

* **上傳影像**

   （*必要*）JPEG或PNG格式中，建議大小為32 x 32像素、72dpi的徽章影像。

* **名稱**

   （*必要*）徽章名稱。 它是預設的`Display Name`以及儲存庫節點名稱。 如果`Name`不是有效的儲存庫節點名稱，則會修改該名稱。

* **顯示名稱**

   （*選用*）要在UI中顯示徽章的名稱。 預設值為`Name`輸入的未更改文本。

* **說明**

   （*選用*）徽章的說明。

## 其他資訊 {#additional-information}

有關設定評分和徽章規則的詳細資訊，請參閱[評分和徽章](/help/communities/implementing-scoring.md)。

有關管理成員的徽章，請參閱[成員控制台](/help/communities/members.md)。
