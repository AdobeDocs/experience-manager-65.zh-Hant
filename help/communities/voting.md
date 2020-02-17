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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用投票 {#using-voting}

組 `Voting` 件是一個有用的工具，它允許社區成員對特定內容進行評分，例如QnA元件中的答案。 在元件 `Voting` 中，成員選擇向上或向下箭頭以指明其意見。

## 新增投票至頁面 {#adding-voting-to-a-page}

若要在作 `Voting``Communities / Voting` 者模式下將元件新增至頁面，請使用元件瀏覽器來尋找並拖曳元件至頁面上的位置，例如相對於功能的位置，供使用者投票。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](essentials-voting.md#essentials-for-client-side) ，元件的顯示方式 `Voting` 就是這樣。

![chlimage_1-307](assets/chlimage_1-307.png)

## 設定投票 {#configuring-voting}

選擇要訪問 `Voting` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-308](assets/chlimage_1-308.png)

在「文 **[!UICONTROL 字與標籤]** 」索引標籤下，指定用來記錄投票的屬性。

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL 正面回應標籤]**(必&#x200B;*要*)正面回應的內部屬性名稱。

* **[!UICONTROL 負面回應標籤]**(*必要*)負面回應的內部屬性名稱。

* **[!UICONTROL Tally Name]**(*必要*)此投票元件實例的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

會員只能投一次票，但可隨時變更投票。

### 匿名 {#anonymous}

不支援匿名投票。 網站訪客必須註冊（成為會員）並登入以參與投票一次。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的Opting Essentials](essentials-voting.md) （投票基本工具）頁面。
