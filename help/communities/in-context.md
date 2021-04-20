---
title: 內容協調
seo-title: 內容協調
description: 如何執行協調者動作
seo-description: 如何執行協調者動作
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---


# 內容協調{#in-context-moderation}

對於AEM Communities，管理員和受信任的社群成員可直接在發佈社群內容的發佈頁面上執行協調。

當使用[協調控制台](moderation.md)時，針對內容顯示的資訊包括發佈頁面的連結，以允許存取在協調內容時可用的其他協調動作。

## 協調動作{#moderation-actions}

請造訪協調概述，以取得[協調動作](moderate-ugc.md#moderation-actions)的說明。

## 協調UI {#moderation-ui}

發佈實例上提供給協調者的UI包含在用於發佈和管理用戶生成內容(UGC)的對話框中。 UI的元素由網站訪客的狀態決定——不論他們是……

1. 張貼內容的成員。
1. 受信任的成員協調者。
1. 管理員。
1. 已登入，但管理員、協調者和內容的作者都未登入。
1. 未登入。

## 範例 {#example}

使用[[開始使用AEM Communities](getting-started.md)時建立的Geometrixx參與](http://localhost:4503/content/sites/engage/en.html)網站，可快速設定論壇中的執行緒，以便在發佈環境中體驗各種協調活動，如下所示。

Aaron McDonald(aaron.mcdonald@mailinator.com)在建立網站時，將他加入社群參與協調者群組，成為值得信賴的社群成員。

Rebekah Larsen(rebekah.larsen@trashymail.com)可使用[Members console](members.md)新增為社群參與成員群組的成員。

有關社群使用者群組的詳細資訊，請造訪[管理使用者和使用者群組](users.md)。

### 建立論壇貼文{#create-the-forum-posts}

* 以麗貝卡·拉森(rebekah.larsen@trashymail.com)的身分登入

   * 選擇論壇
   * 選取新貼文
   * 輸入主旨

      蜂鳥餵食器中的花蜜

   * 輸入正文文本

      每年我掛一隻蜂鳥餵食器時，我並沒有取得什麼成功。 看來他們來了一兩天就到了。 我每週換一次，這樣太長了嗎？ 我需要早點改變嗎？

   * 選取貼文
   * 選擇註銷

* 以Aaron McDonald的身分登入(aaron.mcdonald@mailinator.com)

   * 選擇論壇
   * 對於Hummingbird主題，選擇「閱讀更多」
   * 輸入貼文回覆的留言

      我每週換一次，從5月到10月。

   * 選擇回覆
   * 選擇註銷

* 以Andrew Schaeffer(andrew.schaeffer@trashymail.com)身分登入

   * 選擇論壇
   * 對於Hummingbird主題，選擇「閱讀更多」
   * 輸入貼文回覆的留言

      我銷售花蜜和餵食者——請造訪https://my.viral.url/

   * 選擇回覆
   * 選擇註銷

### 匿名網站訪客(#5){#anonymous-site-visitor}

以下是未登入(5)的網站訪客所檢視的論壇檢視。

匿名網站訪客只能檢視論壇，但我不會張貼任何內容，也不會執行任何協調動作。

![社群論壇——訪客](assets/community-forum-visitor.png)

### 新成員(#4){#new-member}

在作者中，以管理員身分登入，並使用[Members console](members.md)，然後登出，將Boyd Larsen(boyd.larsen@dodgit.com)新增為社群參與成員群組的新成員。

在發佈時，請以Boyd Larsen身份登入，然後選擇`Forum`，然後選擇`Read more`作為蜂鳥貼文，以存取線程。

注意:

* 博伊德沒有參加過論壇。
* 博伊德不能刪除任何東西。
* Boy已登入，可以回覆或標幟內容。

讓Boyd選取「標幟」來標幟Andrew張貼的內容。

登出

![社群論壇成員](assets/community-forum-member.png)

### 管理員(#3){#administrator}

以管理員（管理員）身分登入，並透過選取論壇，然後選取貼文的詳細資訊來存取執行緒。

注意:

* 管理員可以標幟、刪除、編輯、拒絕、剪下、關閉、釘選、功能。
* 管理員可選擇「管理」以存取協調主控台。

![社群——管理——論壇](assets/community-admin-forum.png)

選擇「管理」功能表項目，從發佈環境存取[協調控制台](moderation.md)。

請注意，對於管理員，所有可協調的內容都可見，而不只是「Geometrixx參與」社群網站的內容。

搜尋篩選器是可切換開啟或關閉的側面板。

登出.

![協調控制台——發佈](assets/moderation-console-publish.png)

### 社群協調者(#2){#community-moderator}

以社群協調者Aaron McDonald(aaron.mcdonal@mailinator.com)的身分登入，然後選取「論壇」，然後針對蜂鳥貼文「閱讀更多」，以存取主題。

注意:

* Aaron可以回覆、刪除、編輯或拒絕他自己的貼文。
* Aaron還可以標幟／允許、回覆、刪除、編輯、拒絕其他內容。
* Aaron can Cut將論壇話題轉移到他主持的另一個論壇。
* Aaron可以選擇「管理」來存取協調主控台。

![社群論壇——主持者](assets/community-forum-moderator.png)

選擇「管理」功能表項目，從發佈環境存取[協調控制台](moderation.md)。

請注意，對於社群協調者，只會顯示「Geometrixx參與」社群網站中可協調的內容。

請注意，社群協調者有與管理員相同的選項(影像已關閉搜尋邊欄，但無法存取其他控AEM制台。

登出.

![協調者存取](assets/moderator-access.png)

### 內容作者(#1){#content-author}

以Rebekah Larsen(rebekah.larsen@mailinator.com)的身分登入，他是社群成員，負責啟動主題，並透過選取論壇，然後針對蜂鳥貼文閱讀詳細資訊來存取主題。

注意:

* 麗貝卡可以刪除或編輯自己的帖子。
* Rebekah也可以「回覆」或「標籤其他內容」。
* Rebekah無法存取協調主控台。

![社群論壇作者](assets/community-forum-author.png)

