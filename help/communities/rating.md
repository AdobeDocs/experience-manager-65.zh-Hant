---
title: 使用評等
description: 瞭解如何將「評等」元件新增至頁面，讓登入的社群成員透過評等內容來表達其意見。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# 使用評等 {#using-ratings}

`Rating`元件是獨立使用或搭配其他Communities功能使用。 此元件可讓登入的社群成員透過對內容進行評分來表達其意見。

## 新增評等至頁面 {#adding-a-rating-to-a-page}

若要在作者模式中新增`Rating`元件至頁面，請找到元件`Communities / Rating`並將其拖曳至頁面上的適當位置，例如相對於要評等成員的功能的位置。

如需必要資訊，請造訪[社群元件基本知識](basics.md)。

當包含[必要的使用者端資料庫](rating-basics.md#essentials-for-client-side)時，`Rating`元件就會以這種方式顯示。

![評等](assets/rating.png)

## 設定評等 {#configuring-rating}

選取置入的`Rating`元件，以便您可以存取並選取開啟編輯對話方塊的`Configure`圖示。

![設定 — 新](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字和標籤]**&#x200B;標籤下，您指定評等的內部識別碼。

![tallyname](assets/tallyname.png)

**[!UICONTROL 記帳名稱]**
（*必要*） `Rating`的簡單名稱，可唯一識別此執行個體。 必須為存放庫的有效節點名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

每個成員只允許一個評等。 成員可隨時變更其評等。

### 匿名 {#anonymous}

不支援評級的匿名發佈。 網站訪客必須註冊（成為會員）並登入才能參與。

## 其他資訊 {#additional-information}

如需開發人員的[Rating Essentials](rating-basics.md)頁面上的詳細資訊。
