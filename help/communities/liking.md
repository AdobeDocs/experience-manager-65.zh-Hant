---
title: 使用贊
seo-title: 使用贊
description: 添加和配置按贊元件
seo-description: 添加和配置按贊元件
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---


# 使用按贊{#using-liking}

`Liking`元件是實用的工具，可讓使用者對特定內容（例如論壇中的注釋）發表意見。 使用`Liking`元件，成員選擇心臟圖示以指出正面意見。

## 新增對頁面按贊{#adding-liking-to-a-page}

若要在作者模式下將`Liking`元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Liking`

並將它拖曳至頁面上的位置，例如使用者喜歡的功能相對位置。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](essentials-liking.md#essentials-for-client-side)時，`Liking`元件的顯示方式就是這樣。

![對開元件](assets/liking-component.png)

## 配置按贊{#configuring-liking}

選擇要訪問的已放置的`Liking`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文字與標籤]**&#x200B;標籤下，指定用來記錄按贊的屬性。

![configure-like](assets/configure-liking.png)

* **[!UICONTROL 正面回應標籤]**

   （*必要*）正面回應的屬性名稱。

* **[!UICONTROL 負面回應標籤]**

   （*必要*）負回應的屬性名稱。

* **[!UICONTROL 記帳名稱]**

   (*Required*)此投票元件實例的內部可識別屬性名稱。

## 網站訪客體驗{#site-visitor-experience}

### 成員 {#members}

會員可隨時變更其喜好。

### 匿名 {#anonymous}

不支援匿名按贊。 網站訪客必須註冊（成為會員）並登入才能參與按贊。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[按贊Essentials](essentials-liking.md)頁面。
