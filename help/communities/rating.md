---
title: 使用評級
seo-title: Using Ratings
description: 將分級元件添加到頁面
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

# 使用評級 {#using-ratings}

的 `Rating` 元件是單獨使用的，或與其他社區功能結合使用。 此元件允許登錄的社區成員通過對內容進行評級來表達其意見。

## 向頁面添加分級 {#adding-a-rating-to-a-page}

添加 `Rating` 在作者模式下將元件定位到頁面 `Communities / Rating` 並將其拖到頁面上的位置，如相對於要評級的成員的功能的位置。

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當 [所需的客戶端庫](rating-basics.md#essentials-for-client-side) 包括，這是 `Rating` 元件。

![評等](assets/rating.png)

## 配置評級 {#configuring-rating}

選取已放置的 `Rating` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置 — 新建](assets/configure-new.png)

在 **[!UICONTROL 文本和標籤]** 頁籤，指定評級的內部標識符。

![名](assets/tallyname.png)

**[!UICONTROL 計數名稱]**
(*必需*)的簡單名稱 `Rating` 唯一標識此實例。 必須為儲存庫的有效節點名稱。

## 站點訪問者體驗 {#site-visitor-experience}

### 成員 {#members}

每個成員只允許一個分級。 會員可隨時更改其評級。

### 匿名 {#anonymous}

不支援匿名發佈評級。 站點訪問者必須註冊（成為成員）並登錄以參與。

## 其他資訊 {#additional-information}

有關 [評級基礎](rating-basics.md) 頁面。
