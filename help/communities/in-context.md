---
title: 內文中稽核
seo-title: In-Context Moderation
description: 如何執行版主動作
seo-description: How to perform moderator actions
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 內文中稽核 {#in-context-moderation}

對於AEM Communities，管理員和受信任的社群成員可直接在發佈社群內容的頁面上執行稽核。

使用 [稽核主控台](moderation.md)，針對內容顯示的資訊包含已發佈頁面的連結，可讓您存取在內容中進行仲裁時可用的其他仲裁動作。

## 稽核動作 {#moderation-actions}

造訪協調概述，瞭解以下專案的說明： [稽核動作](moderate-ugc.md#moderation-actions).

## 稽核UI {#moderation-ui}

在發佈執行個體上向版主顯示的UI包含在用於發佈和管理使用者產生的內容(UGC)的對話方塊中。 UI的元素由網站訪客的狀態決定，無論它們是……

1. 發佈內容的成員。
1. 信任的成員版主。
1. 管理員。
1. 已登入，但不是內容的管理員、版主或作者。
1. 未登入。

## 範例 {#example}

使用 [Geometrixx參與](http://localhost:4503/content/sites/engage/en.html) 網站建立時間 [AEM Communities快速入門](getting-started.md)，您可以在論壇中快速設定對話串，在發佈環境中體驗各種協調活動，如下所示。

Aaron McDonald (aaron.mcdonald@mailinator.com)在建立網站時將其新增至community-engage-moderators群組，因此被識別為信任的社群成員。

Rebekah Larsen (rebekah.larsen@trashymail.com)可透過 [成員主控台](members.md).

如需社群使用者群組的詳細資訊，請造訪 [管理使用者和使用者群組](users.md).

### 建立論壇帖子 {#create-the-forum-posts}

* 以Rebekah Larsen (rebekah.larsen@trashymail.com)登入

   * 選取論壇
   * 選取新貼文
   * 輸入主旨

     蜂鳴送鳥器何時變更花蜜

   * 輸入內文

     我每年都掛一隻蜂鳥餵食器，可不太成功。 他們好像來了一兩天，就是這樣。 我每週變更一次會太長嗎？ 我是否需要更早進行變更？

   * 選取貼文
   * 選取登出

* 以Aaron McDonald (aaron.mcdonald@mailinator.com)登入

   * 選取論壇
   * 蜂鳥主題，請選取閱讀更多
   * 輸入張貼回覆的註解

     我每週都會換一次衣服，從5月到10月都會收到衣服。

   * 選取回覆
   * 選取登出

* 以Andrew Schaeffer身分登入(andrew.schaeffer@trashymail.com)

   * 選取論壇
   * 蜂鳥主題，請選取閱讀更多
   * 輸入張貼回覆的註解

     我銷售花蜜和飼料 — 請造訪https://my.viral.url/

   * 選取回覆
   * 選取登出

### 匿名網站訪客(#5) {#anonymous-site-visitor}

以下是未登入的網站訪客所看到的論壇檢視(5)。

匿名網站訪客僅可檢視論壇，但不得發佈任何內容或執行任何稽核動作。

![社群 — 論壇 — 訪客](assets/community-forum-visitor.png)

### 新成員(#4) {#new-member}

在作者身分登入並使用，將Boyd Larsen (boyd.larsen@dodgit.com)新增為community-engage-members群組的新成員 [成員主控台](members.md)，然後登出。

在發佈上，以Boyd Larsen身分登入，並透過選取以下專案來存取對話串： `Forum`，然後 `Read more` 為蜂鳥貼文。

注意:

* 博伊德尚未參與論壇。
* Boyd無法刪除任何內容。
* Boyd已登入，可以回覆或標幟內容。

讓Boyd選取「標幟」以標幟Andrew張貼的內容。

登出

![community-forum-member](assets/community-forum-member.png)

### 管理員(#3) {#administrator}

以管理員（管理員）身分登入，並選取「論壇」來存取對話串，然後選取貼文的「閱讀更多資訊」。

注意:

* 管理員可以標幟、刪除、編輯、拒絕、剪下、關閉、釘選、功能。
* 管理員可以選取「管理」以存取管理主控台。

![community-admin-forum](assets/community-admin-forum.png)

選取管理功能表專案以存取 [稽核主控台](moderation.md) 從發佈環境。

請注意，對於管理員而言，所有可稽核內容皆可見，而不僅僅是GeometrixxEngage社群網站的內容。

搜尋篩選器是切換開啟或關閉的側面板。

登出.

![moderation-console-publish](assets/moderation-console-publish.png)

### 社群版主(#2) {#community-moderator}

以社群版主Aaron McDonald (aaron.mcdonal@mailinator.com)身分登入，並選取「論壇」，然後選取「瞭解更多」以存取對話串，瞭解蜂鳥貼文的內容。

注意:

* Aaron可以回覆、刪除、編輯或拒絕自己的貼文。
* Aaron也可以標幟/允許、回覆、刪除、編輯、拒絕其他內容。
* Aaron可以剪下論壇主題，將其移至他主持的另一個論壇。
* Aaron可以選取「管理」來存取稽核主控台。

![社群 — 論壇 — 版主](assets/community-forum-moderator.png)

選取管理功能表專案以存取 [稽核主控台](moderation.md) 從發佈環境。

請注意，對於社群版主，只會顯示來自GeometrixxEngage社群網站的可稽核內容。

請注意，社群版主的選項與管理員相同（影像已關閉搜尋側欄），但無法存取其他AEM主控台。

登出.

![版主 — 存取](assets/moderator-access.png)

### 內容作者(#1) {#content-author}

以Rebekah Larsen (rebekah.larsen@mailinator.com)身分登入，此社群成員是啟動對話串，並選取「論壇」，接著選取Hummingbird貼文的「瞭解詳情」以存取對話串。

注意:

* Rebekah可以刪除或編輯自己的貼文。
* Rebekah也可以回覆或標幟其他內容。
* Rebekah無法存取稽核主控台。

![community-forum-author](assets/community-forum-author.png)
