---
title: 使用評等
seo-title: Using Ratings
description: 新增評等元件至頁面
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# 使用評等 {#using-ratings}

此 `Rating` 元件是獨立使用的，或與其他Communities功能搭配使用。 此元件可讓登入的社群成員透過內容分級來表達其意見。

## 新增評等至頁面 {#adding-a-rating-to-a-page}

新增 `Rating` 在製作模式中，找到元件至頁面 `Communities / Rating` 並將其拖動到頁面上的位置，例如與要評級的成員的特徵相對的位置。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的用戶端程式庫](rating-basics.md#essentials-for-client-side) 包含在內，以下為方式 `Rating` 元件隨即顯示。

![評等](assets/rating.png)

## 設定評等 {#configuring-rating}

選取已放置的 `Rating` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文字與標籤]** 索引標籤，以指定評等的內部識別碼。

![tallyname](assets/tallyname.png)

**[!UICONTROL 計數名稱]**
(*必填*)的簡單名稱 `Rating` 唯一識別此例項。 必須是儲存庫的有效節點名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

每個成員僅允許一個評級。 會員可隨時更改其評級。

### 匿名 {#anonymous}

不支援匿名張貼評等。 網站訪客必須註冊（成為會員）並登入以參與。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [評等要點](rating-basics.md) 頁面。
