---
title: 特色內容功能
seo-title: 特色內容功能
description: 「精選內容」功能可讓登入網站的訪客反白顯示內容
seo-description: 「精選內容」功能可讓登入網站的訪客反白顯示內容
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 特色內容功能 {#featured-content-feature}

## 簡介 {#introduction}

精選內容功能提供發佈環境中登入網站訪客（社群成員）的區域，以反白標示

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [論壇](forum.md)
* [構思](ideation-feature.md)
* [QnA](working-with-qna.md)

一旦將內容標示為特色，它就會列在此元件中，而此元件可能會放置在特定的登陸頁面或容易引起社群成員注意的區域。

每個元件可能允許或禁止功能化內容。

本節說明

* 將精選內容新增至社群網站
* 元件的配置設 `Featured Content`置

## 將精選內容新增至頁面 {#adding-featured-content-to-a-page}

若要在作 `Featured Content` 者模式中將元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Featured Content`

並將它拖曳至應出現精選內容的頁面上。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](essentials-featured.md#essentials-for-client-side) ，元件的顯示 `Featured Content`方式如下：

![chlimage_1-13](assets/chlimage_1-13.png)

## 設定精選內容 {#configuring-featured-content}

選擇要訪問 `Featured Content` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-14](assets/chlimage_1-14.png) ![chlimage_1-15](assets/chlimage_1-15.png)

### 「設定」頁籤 {#settings-tab}

在「設 **[!UICONTROL 定]** 」標籤下，識別要具備的內容：

* **[!UICONTROL 顯示名]**&#x200B;稱精選內容清單的標題。 例如 `Featured Questions` 或 `Featured Ideas`。 如果留 `Featured Content` 空，則預設為。

* **[!UICONTROL 主要內容的位置]**
   *（必要）* ，瀏覽至包含可能是功能之內容的頁面（該頁面的元件必須設定為「允許功能內容」）。 例如， `/content/sites/engage/en/forum`

* **[!UICONTROL 顯示限]**&#x200B;制要顯示的精選內容數目上限。 預設值為5。

## 網站訪客體驗 {#site-visitor-experience}

將內容標幟為特色內容的能力需要協調者權限。

協調者檢視張貼的內容時，可存取內容內容協調標幟，其中包含新標 `Feature` 幟。

![chlimage_1-16](assets/chlimage_1-16.png)

標籤為功能後，模型標幟就會變 `Unfeature`成。

包含元件 `Featured Content` 的頁面現在會包含此貼文。

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` 是實際貼文的連結。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發 [人員的「主要內容](essentials-featured.md) 」頁面。

如需將內容標示為特色，請參閱 [協調使用者產生的內容](moderate-ugc.md)。
