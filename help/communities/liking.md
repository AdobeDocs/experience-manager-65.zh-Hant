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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用贊 {#using-liking}

此 `Liking`元件是有用的工具，可讓使用者對特定內容（例如論壇中的注釋）發表意見。 使用元 `Liking`件時，成員會選擇心臟圖示以指出正面意見。

## 新增對頁面按贊 {#adding-liking-to-a-page}

若要在作 `Liking` 者模式中將元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Liking`

並將它拖曳至頁面上的位置，例如使用者喜歡的功能相對位置。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](essentials-liking.md#essentials-for-client-side) ，元件的顯示方式 `Liking` 就是這樣。

![chlimage_1-93](assets/chlimage_1-93.png)

## 設定贊 {#configuring-liking}

選擇要訪問 `Liking` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-94](assets/chlimage_1-94.png)

在「文 **[!UICONTROL 字與標籤]** 」索引標籤下，指定用來記錄按贊的屬性。

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL 正面回應標籤]**(必&#x200B;*要*)正面回應的屬性名稱。

* **[!UICONTROL 負面回應標籤]**(*必要*)負面回應的屬性名稱。

* **[!UICONTROL Tally Name]**(*必要*)此投票元件實例的內部可識別屬性名稱。

## 網站訪客體驗 {#site-visitor-experience}

### 成員 {#members}

會員可隨時變更其喜好。

### 匿名 {#anonymous}

不支援匿名按贊。 網站訪客必須註冊（成為會員）並登入才能參與按贊。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的「按贊基本功能](essentials-liking.md) 」頁面。
