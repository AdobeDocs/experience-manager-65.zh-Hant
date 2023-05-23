---
title: 徽章控制台
seo-title: Badges Console
description: 「社區徽章」控制台允許您添加可在獲得（授予）成員或成員在社區中承擔特定角色（已分配）時為成員顯示的自定義徽章
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
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
source-wordcount: '287'
ht-degree: 4%

---

# 徽章控制台 {#badges-console}

## 關於徽章 {#about-badges}

社區徽章控制台提供添加自定義徽章的功能，這些徽章可在獲得（授予）成員或成員在社區中承擔特定角色（已分配）時顯示。

### 徽章可見性 {#badge-visibility}

當前，社區成員掙得或分配的徽章將與其名稱和虛擬形象一起出現在以下位置：

* 設定檔
* [論壇](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [創意力](/help/communities/ideation-feature.md)

在作者環境中，導航到Badges控制台：

* 從全局導航： **[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 徽章]**

此控制台顯示當前可用的徽章，並可從中添加新徽章。

![徽章首頁](assets/badges-homepage.png)

## 建立預算 {#create-badge}

通過上傳合適的小影像（72dpi，高度在26-32像素之間）和提供名稱來建立標籤。 標籤影像儲存在 `/libs/settings/community/badging/images` 並自動複製到發佈環境。

如果發佈環境是發佈伺服器場，則必須配置 [用戶同步](/help/communities/sync.md)。

![建立徽章](assets/create-badge.png)

* **上傳影像**

   (*必需*)建議大小為32 x 32像素(72dpi)的標籤影像，採用JPEG或PNG格式。

* **名稱**

   (*必需*)徽章名稱。 它是預設 `Display Name` 以及儲存庫節點名稱。 如果 `Name` 不是有效的儲存庫節點名稱，將修改它。

* **顯示名稱**

   (*可選*)要在UI中顯示的徽章名稱。 預設值是為 `Name`。

* **說明**

   (*可選*)徽章的說明。

## 其他資訊 {#additional-information}

有關設定評分和標籤規則的詳細資訊，請參閱 [評分和徽章](/help/communities/implementing-scoring.md)。

有關管理成員的徽章，請參閱 [成員控制台](/help/communities/members.md)。
