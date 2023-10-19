---
title: 使用投票
description: 瞭解如何將投票元件新增到頁面，讓登入的社群成員對特定內容（例如答案）進行評分。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

# 使用投票 {#using-voting}

此 `Voting` 元件是實用工具，可讓社群成員為特定內容評分，例如QnA元件中的答案。 使用 `Voting` 元件，成員會選取向上或向下箭頭來表示其意見。

## 新增投票至頁面 {#adding-voting-to-a-page}

若要新增 `Voting` 元件至作者模式下的頁面，請使用元件瀏覽器。 尋找 `Communities / Voting` 並將其拖曳至頁面上適當的位置，例如與功能相對以供使用者投票的位置。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-voting.md#essentials-for-client-side) 包含，這就是 `Voting` 元件出現。

![投票元件](assets/voting-component.png)

## 設定投票 {#configuring-voting}

選取已放置的 `Voting` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 文字和標籤]** 標籤，指定用來記錄投票的屬性。

![voting-label](assets/voting-label.png)

* **[!UICONTROL 正面回應標籤]**

  (*必填*)正面回應的內部屬性名稱。

* **[!UICONTROL 負面回應標籤]**

  (*必填*)負面回應的內部屬性名稱。

* **[!UICONTROL 記帳名稱]**

  (*必填*)此投票元件例項的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

成員只能投票一次，但可隨時變更投票。

### 匿名 {#anonymous}

不支援匿名投票。 網站訪客必須註冊（成為會員）並登入才能參與投票一次。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [Voting Essentials](essentials-voting.md) 開發人員頁面。
