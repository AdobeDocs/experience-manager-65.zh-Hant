---
title: 使用連結
description: 瞭解如何新增及設定Liking元件，讓使用者可對特定內容（例如評論）發表意見。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# 使用連結 {#using-liking}

`Liking`元件是實用工具，可讓使用者表達對特定內容的意見，例如論壇內的評論。 使用`Liking`元件時，成員會選取心形圖示來表示正面意見。

## 新增連結至頁面 {#adding-liking-to-a-page}

若要將`Liking`元件新增至作者模式的頁面，請使用元件瀏覽器來尋找

* `Communities / Liking`

並將其拖曳至頁面上適當的位置，例如與功能相關的位置以供使用者點選。

如需必要資訊，請造訪[社群元件基本知識](basics.md)。

當包含[必要的使用者端資料庫](essentials-liking.md#essentials-for-client-side)時，`Liking`元件就會以這種方式顯示。

![liking-component](assets/liking-component.png)

## 設定連結 {#configuring-liking}

選取置入的`Liking`元件，以便您可以存取並選取開啟編輯對話方塊的`Configure`圖示。

![設定 — 新](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字和標籤]**&#x200B;標籤下，指定用來錄製「讚」的內容。

![設定連結](assets/configure-liking.png)

* **[!UICONTROL 正面回應標籤]**

  （*必要*）正面回應的屬性名稱。

* **[!UICONTROL 負面回應標籤]**

  （*必要*）負面回應的屬性名稱。

* **[!UICONTROL 記帳名稱]**

  （*必要*）此投票元件執行個體的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

成員可隨時變更其「讚」。

### 匿名 {#anonymous}

不支援匿名連結。 網站訪客必須註冊（成為會員）並登入才能參與點讚。

## 其他資訊 {#additional-information}

如需開發人員的[按一下Essentials](essentials-liking.md)頁面以取得詳細資訊。
