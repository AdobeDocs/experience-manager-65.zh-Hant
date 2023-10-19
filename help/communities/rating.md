---
title: 使用評等
description: 瞭解如何將「評等」元件新增至頁面，讓登入的社群成員透過評等內容來表達其意見。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# 使用評等 {#using-ratings}

此 `Rating` 元件可獨立使用或搭配其他Communities功能使用。 此元件可讓登入的社群成員透過對內容進行評分來表達其意見。

## 新增評等至頁面 {#adding-a-rating-to-a-page}

若要新增 `Rating` 元件至作者模式下的頁面，找到元件 `Communities / Rating` 並將其拖曳到頁面上的適當位置，例如相對於該特徵的位置，以便成員進行評分。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](rating-basics.md#essentials-for-client-side) 包含，這就是 `Rating` 元件出現。

![評等](assets/rating.png)

## 設定評等 {#configuring-rating}

選取已放置的 `Rating` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文字和標籤]** 索引標籤中，您可以指定「評等」的內部識別碼。

![tallyname](assets/tallyname.png)

**[!UICONTROL 記帳名稱]**
(*必填*)的簡單名稱 `Rating` 唯一地識別此執行個體的識別碼。 必須為存放庫的有效節點名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

每個成員只允許一個評等。 成員可隨時變更其評等。

### 匿名 {#anonymous}

不支援評級的匿名發佈。 網站訪客必須註冊（成為會員）並登入才能參與。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [Rating Essentials](rating-basics.md) 開發人員頁面。
