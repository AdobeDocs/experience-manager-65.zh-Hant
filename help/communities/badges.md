---
title: 標章主控台
seo-title: 標章主控台
description: 「社群標章」控制台可讓您新增自訂標章，這些標章可在獲得（授與）或在成員擔任社群中特定角色（指派）時顯示給成員
seo-description: 「社群標章」控制台可讓您新增自訂標章，這些標章可在獲得（授與）或在成員擔任社群中特定角色（指派）時顯示給成員
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 標章主控台{#badges-console}

## 關於標章 {#about-badges}

Communities Badges控制台可以添加自定義徽章，這些徽章可在獲得（授予）成員或成員在社區中承擔特定角色（指派）時顯示。

### 徽章可見度 {#badge-visibility}

目前，社群成員所賺取或指派的標章，將連同其姓名和頭像一起出現在下列位置：

* 描述檔
* [論壇](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [意識形態](/help/communities/ideation-feature.md)

在作者環境中，若要進入Badges主控台

* 從全域導覽：工 **具、社群、徽章**

此控制台顯示當前可用的標章，並可從中添加新標章。

![chlimage_1-123](assets/chlimage_1-123.png)

## 建立預算 {#create-badge}

通過上傳合適的小影像（72dpi，高度為26-32像素）並提供名稱來建立徽章。 徽章映像儲存在位於的儲存庫 `/etc/community/badging/images` 中，並自動複製到發佈環境。

如果發佈環境是發佈者的農場，則必須設定使用 [者同步](/help/communities/sync.md)。

![chlimage_1-124](assets/chlimage_1-124.png)

* **上傳影像**(必&#x200B;*要*)建議大小為32 x 32像素、72dpi的JPEG或PNG格式的標章影像。

* **名稱**(*必要*)徽章名稱。 它是預設 `Display Name` 值和儲存庫節點名稱。 如果該 `Name` 節點不是有效的儲存庫節點名稱，則將對其進行修改。

* **顯示名稱**(*可選*)UI中要顯示徽章的名稱。 預設值是為輸入的未更改文本 `Name`。

* **說明**(*可選*)徽章的說明。

## 其他資訊 {#additional-information}

如需設定計分和徽章規則的詳細資訊，請參閱計 [分和徽章](/help/communities/implementing-scoring.md)。

有關管理成員的標章，請參閱「成 [員控制台」](/help/communities/members.md)。
