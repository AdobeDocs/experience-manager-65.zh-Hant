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
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---


# 精選內容功能{#featured-content-feature}

## 簡介 {#introduction}

特色內容功能為登入網站訪客（社群成員）在發佈環境中提供一個區域，以反白標示下列內容：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [論壇](forum.md)
* [構思](ideation-feature.md)
* [QnA](working-with-qna.md)

一旦將內容標示為特色，它就會列在此元件中，而此元件可能會放置在特定的登陸頁面或容易引起社群成員注意的區域。

每個元件可能允許或禁止功能化內容。

本檔案章節說明：

* 將精選內容新增至社群網站。
* `Featured Content`元件的配置設定。

## 新增精選內容至頁面{#adding-featured-content-to-a-page}

若要在作者模式下將`Featured Content`元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Featured Content`

並將它拖曳至應出現精選內容的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](essentials-featured.md#essentials-for-client-side)時，`Featured Content`元件的顯示方式如下：

![功能內容](assets/featuredcontent.png)

## 設定精選內容{#configuring-featured-content}

選擇要訪問的已放置的`Featured Content`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

![功能內容1](assets/featuredcontent1.png)

### 「設定」頁籤{#settings-tab}

在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤下，識別要使用的內容：

* **[!UICONTROL 顯示名稱]**

   精選內容清單的標題。 例如`Featured Questions`或`Featured Ideas`。 如果保留空白，預設值為`Featured Content`。

* **[!UICONTROL 主要內容的位置]**

   *（必要）瀏* 覽至包含可能是功能之內容的頁面（該頁面的元件必須設定為「允許功能內容」）。例如，`/content/sites/engage/en/forum`。

* **[!UICONTROL 顯示限制]**

   要顯示的特色內容數上限。 預設值為5。

## 網站訪客體驗{#site-visitor-experience}

將內容標幟為特色內容的能力需要協調者權限。

協調者檢視張貼的內容時，可存取內容內容協調標幟，其中包含新的`Feature`標幟。

![網站——訪客——體驗](assets/site-visitor-experience.png)

標籤為功能後，模型標幟就會變成`Unfeature`。

包含`Featured Content`元件的頁面現在會包含此貼文。

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 是實際貼文的連結。

## 其他資訊 {#additional-information}

開發人員可在[精選內容](essentials-featured.md)頁面上找到更多資訊。

如需將內容標幟為特色，請參閱[協調使用者產生的內容](moderate-ugc.md)。
