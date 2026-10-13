---
title: 使用投票
description: 瞭解如何將投票元件新增到頁面，讓登入的社群成員對特定內容（例如答案）進行評分。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%
---
# 使用投票 {#using-voting}

`Voting`元件是實用的工具，可讓社群成員為特定內容評分，例如QnA元件中的答案。 使用`Voting`元件時，成員會選取向上或向下箭頭來表示其意見。

## 新增投票至頁面 {#adding-voting-to-a-page}

若要將`Voting`元件新增至作者模式的頁面，請使用元件瀏覽器。 找到`Communities / Voting`並將其拖曳到頁面上某個位置，例如與功能相對的位置以供使用者投票。

如需必要資訊，請造訪[社群元件基本知識](basics.md)。

當包含[必要的使用者端資料庫](essentials-voting.md#essentials-for-client-side)時，`Voting`元件就會以這種方式顯示。

![投票元件](assets/voting-component.png)

## 設定投票 {#configuring-voting}

選取置入的`Voting`元件，以便您可以存取並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字和標籤]**&#x200B;標籤下，指定用來記錄投票的屬性。

![投票標籤](assets/voting-label.png)

* **[!UICONTROL 正面回應標籤]**

  （*必要*）正面回應的內部屬性名稱。

* **[!UICONTROL 負面回應標籤]**

  （*必要*）負面回應的內部屬性名稱。

* **[!UICONTROL 記帳名稱]**

  （*必要*）此投票元件執行個體的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

成員只能投票一次，但可隨時變更投票。

### 匿名 {#anonymous}

不支援匿名投票。 網站訪客必須註冊（成為會員）並登入才能參與投票一次。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[投票要點](essentials-voting.md)頁面。
