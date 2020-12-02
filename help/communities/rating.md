---
title: 使用評分
seo-title: 使用評分
description: 新增評分元件至頁面
seo-description: 新增評分元件至頁面
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---


# 使用評分{#using-ratings}

`Rating`元件是獨立使用的，或與其他Communities功能搭配使用。 此元件可讓登入的社群成員透過內容分級來表達意見。

## 新增評分至頁面{#adding-a-rating-to-a-page}

若要在作者模式下將`Rating`元件新增至頁面，請找出元件`Communities / Rating`並將其拖曳至頁面上，例如與功能相對的位置，讓成員評分。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](rating-basics.md#essentials-for-client-side)時，`Rating`元件的顯示方式就是這樣。

![評等](assets/rating.png)

## 設定評等{#configuring-rating}

選擇要訪問的已放置的`Rating`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字與標籤]**&#x200B;標籤下，您會指定評分的內部識別碼。

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**
(*必要*)唯一識別此例項 `Rating` 的簡單名稱。必須為儲存庫的有效節點名。

## 網站訪客體驗{#site-visitor-experience}

### 成員 {#members}

每個成員僅允許一個分級。 會員可隨時變更其評級。

### 匿名 {#anonymous}

不支援匿名張貼評分。 網站訪客必須註冊（成為會員）並登入以參與。

## 其他資訊 {#additional-information}

開發人員的[ Rating Essentials](rating-basics.md)頁面中有更多資訊。
