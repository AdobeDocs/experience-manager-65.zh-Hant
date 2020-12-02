---
title: 使用投票
seo-title: 使用投票
description: 將投票元件添加到頁面
seo-description: 將投票元件添加到頁面
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# 使用投票{#using-voting}

`Voting`元件是一個有用的工具，它允許社區成員對特定內容評分，如QnA元件中的答案。 在`Voting`元件中，成員選擇向上或向下箭頭以指出其意見。

## 新增投票至頁面{#adding-voting-to-a-page}

若要在作者模式下將`Voting`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Voting`並將它拖曳至頁面上，例如使用者投票時相對於該功能的位置。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](essentials-voting.md#essentials-for-client-side)時，`Voting`元件的顯示方式就是這樣。

![投票元件](assets/voting-component.png)

## 配置投票{#configuring-voting}

選擇要訪問的已放置的`Voting`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字與標籤]**&#x200B;標籤下，指定用來記錄投票的屬性。

![投票標籤](assets/voting-label.png)

* **[!UICONTROL 正面回應標籤]**

   （*必要*）正面回應的內部屬性名稱。

* **[!UICONTROL 負面回應標籤]**

   （*必要*）負面回應的內部屬性名稱。

* **[!UICONTROL 記帳名稱]**

   (*Required*)此投票元件實例的內部可識別屬性名稱。

## 網站訪客體驗{#site-visitor-experience}

### 成員 {#members}

會員只能投一次票，但可隨時變更投票。

### 匿名 {#anonymous}

不支援匿名投票。 網站訪客必須註冊（成為會員）並登入以參與投票一次。

## 其他資訊 {#additional-information}

開發人員的[Opting Essentials](essentials-voting.md)頁面中有更多資訊。
