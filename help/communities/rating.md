---
title: 使用評等
seo-title: 使用評等
description: 新增評等元件至頁面
seo-description: 新增評等元件至頁面
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---

# 使用評級{#using-ratings}

`Rating`元件是獨立的，或與其他Communities功能結合使用。 此元件可讓登入的社群成員透過內容分級來表達其意見。

## 新增評等至頁面{#adding-a-rating-to-a-page}

若要在製作模式中將`Rating`元件新增至頁面，請找出元件`Communities / Rating`並將其拖曳至頁面上的位置，例如與要評分的成員功能相對的位置。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含[必要的用戶端程式庫](rating-basics.md#essentials-for-client-side)時，會以此方式顯示`Rating`元件。

![評等](assets/rating.png)

## 配置評等{#configuring-rating}

選取要存取的放置`Rating`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字與標籤]**&#x200B;標籤下，指定評等的內部識別碼。

![tallyname](assets/tallyname.png)

**[!UICONTROL 計數名稱]**
(*必要*)可唯一識別此例 `Rating` 項的簡單名稱。必須是儲存庫的有效節點名稱。

## 網站訪客體驗{#site-visitor-experience}

### 成員 {#members}

每個成員僅允許一個評級。 會員可隨時更改其評級。

### 匿名 {#anonymous}

不支援匿名張貼評等。 網站訪客必須註冊（成為會員）並登入以參與。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[ Rating Essentials](rating-basics.md)頁面。
