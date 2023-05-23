---
title: 使用投票
seo-title: Using Voting
description: 將投票元件添加到頁
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# 使用投票 {#using-voting}

的 `Voting` 元件是一種有用的工具，它允許社區成員對特定內容（如QnA元件中的答案）進行分級。 使用 `Voting` 元件，成員選擇向上或向下箭頭以指示其意見。

## 向頁面添加投票 {#adding-voting-to-a-page}

添加 `Voting` 在作者模式下對頁面的元件，使用元件瀏覽器查找 `Communities / Voting` 並將其拖到頁面上，如相對於功能的位置，供用戶投票。

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當 [所需的客戶端庫](essentials-voting.md#essentials-for-client-side) 包括，這是 `Voting` 元件。

![投票分量](assets/voting-component.png)

## 配置投票 {#configuring-voting}

選取已放置的 `Voting` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

在 **[!UICONTROL 文本和標籤]** 頁籤，指定用於記錄投票的屬性。

![投票標籤](assets/voting-label.png)

* **[!UICONTROL 正面回應標籤]**

   (*必需*)正響應的內部屬性名稱。

* **[!UICONTROL 負面回應標籤]**

   (*必需*)負響應的內部屬性名稱。

* **[!UICONTROL 記帳名稱]**

   (*必需*)此投票元件實例的內部、可識別屬性名稱。

## 站點訪問者體驗 {#site-visitor-experience}

### 成員 {#members}

成員只能投一票，但可隨時更改投票。

### 匿名 {#anonymous}

不支援匿名投票。 站點訪問者必須註冊（成為成員）並登錄一次以參與投票。

## 其他資訊 {#additional-information}

有關 [投票要點](essentials-voting.md) 頁面。
