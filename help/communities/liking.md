---
title: 使用連結
description: 瞭解如何新增及設定Liking元件，讓使用者可對特定內容（例如評論）發表意見。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 4%

---

# 使用連結 {#using-liking}

此 `Liking` 元件是實用工具，可讓使用者對特定內容發表意見，例如論壇中的評論。 使用 `Liking` 元件，成員選取心形圖示表示正面意見。

## 新增連結至頁面 {#adding-liking-to-a-page}

若要新增 `Liking` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Liking`

並將其拖曳至頁面上適當的位置，例如與功能相關的位置以供使用者點選。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-liking.md#essentials-for-client-side) 包含，這就是 `Liking` 元件出現。

![liking-component](assets/liking-component.png)

## 設定連結 {#configuring-liking}

選取已放置的 `Liking` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 文字和標籤]** 標籤，指定用來錄製「讚」的屬性。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 正面回應標籤]**

  (*必填*)正面回應的屬性名稱。

* **[!UICONTROL 負面回應標籤]**

  (*必填*)負面回應的屬性名稱。

* **[!UICONTROL 記帳名稱]**

  (*必填*)此投票元件例項的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

成員可隨時變更其「讚」。

### 匿名 {#anonymous}

不支援匿名連結。 網站訪客必須註冊（成為會員）並登入才能參與點讚。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [按一下Essentials](essentials-liking.md) 開發人員頁面。
