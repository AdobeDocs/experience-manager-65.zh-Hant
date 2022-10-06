---
title: 使用投票
seo-title: Using Voting
description: 將投票元件新增至頁面
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

此 `Voting` 元件是一種有用的工具，它允許社區成員對特定內容片段（如QnA元件內的答案）進行評分。 使用 `Voting` 元件，成員選擇向上或向下箭頭以指示其意見。

## 新增投票至頁面 {#adding-voting-to-a-page}

新增 `Voting` 在製作模式中，使用元件瀏覽器來尋找 `Communities / Voting` 並將其拖曳至頁面上的位置，例如與功能相對的位置，供使用者投票。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的用戶端程式庫](essentials-voting.md#essentials-for-client-side) 包含在內，以下為方式 `Voting` 元件隨即顯示。

![投票元件](assets/voting-component.png)

## 配置投票 {#configuring-voting}

選取已放置的 `Voting` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![設定](assets/configure-new.png)

在 **[!UICONTROL 文字與標籤]** 頁簽，指定用於記錄投票的屬性。

![投票標籤](assets/voting-label.png)

* **[!UICONTROL 正面回應標籤]**

   (*必填*)正面回應的內部屬性名稱。

* **[!UICONTROL 負面回應標籤]**

   (*必填*)負回應的內部屬性名稱。

* **[!UICONTROL 記帳名稱]**

   (*必填*)此投票元件例項的內部、可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

成員只能投一票，但可隨時更改其投票。

### 匿名 {#anonymous}

不支援匿名投票。 網站訪客必須註冊（成為會員）並登入以參與一次投票。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [投票要點](essentials-voting.md) 頁面。
