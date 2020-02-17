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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用評分 {#using-ratings}

該組 `Rating`件是單獨使用的，或與其他Communities功能一起使用。 此元件可讓登入的社群成員透過內容分級來表達意見。

## 新增評分至頁面 {#adding-a-rating-to-a-page}

若要在作 `Rating`者模式下將元件新增至頁面，請找出元件並 `Communities / Rating` 將其拖曳至頁面上，例如與功能相關的位置，讓成員評分。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](rating-basics.md#essentials-for-client-side) ，元件的顯示方式 `Rating` 就是這樣。

![chlimage_1-493](assets/chlimage_1-493.png)

## 設定評分 {#configuring-rating}

選擇要訪問 `Rating` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-494](assets/chlimage_1-494.png)

在「文 **[!UICONTROL 字與標籤]** 」索引標籤下，指定「評分」的內部識別碼。

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Tally Name]**(*必要*)唯一識別此例項 `Rating`的簡單名稱。 必須為儲存庫的有效節點名。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

每個成員僅允許一個分級。 會員可隨時變更其評級。

### 匿名 {#anonymous}

不支援匿名張貼評分。 網站訪客必須註冊（成為會員）並登入以參與。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的Rating Essentials](rating-basics.md) （評分基本工具）頁面。
