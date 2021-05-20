---
title: 精選內容功能
seo-title: 精選內容功能
description: 「精選內容」功能可讓登入的網站訪客反白標示內容
seo-description: 「精選內容」功能可讓登入的網站訪客反白標示內容
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# 精選內容功能{#featured-content-feature}

## 簡介 {#introduction}

精選內容功能提供發佈環境中登入網站訪客（社群成員）的區域，突顯下列內容：

* [部落格](blog-feature.md)
* [日曆](calendar.md)
* [論壇](forum.md)
* [構思](ideation-feature.md)
* [QnA](working-with-qna.md)

一旦將內容標示為特色內容，就會列在此元件中，這些內容可能會放置在特定登陸頁面或容易吸引社群成員注意的區域中。

每個元件可能允許或不允許使用特徵內容的功能。

本檔案的本節說明：

* 將精選內容新增至社群網站。
* `Featured Content`元件的組態設定。

## 將精選內容新增至頁面{#adding-featured-content-to-a-page}

若要在製作模式中將`Featured Content`元件新增至頁面，請使用元件瀏覽器來找出

* `Communities / Featured Content`

並將其拖曳至應出現精選內容的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含[必要的用戶端程式庫](essentials-featured.md#essentials-for-client-side)時，以下是`Featured Content`元件的顯示方式：

![功能內容](assets/featuredcontent.png)

## 設定精選內容{#configuring-featured-content}

選取要存取的放置`Featured Content`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 設定頁簽{#settings-tab}

在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤下，識別要功能的內容：

* **[!UICONTROL 顯示名稱]**

   精選內容清單的標題。 例如`Featured Questions`或`Featured Ideas`。 如果保留為空，則預設為`Featured Content`。

* **[!UICONTROL 主要內容的位置]**

   *（必要）* 瀏覽至包含可能是功能之內容的頁面（該頁面的元件必須設為「允許精選內容」）。例如， `/content/sites/engage/en/forum`。

* **[!UICONTROL 顯示限制]**

   要顯示的精選內容數量上限。 預設為5。

## 網站訪客體驗{#site-visitor-experience}

將內容標幟為精選內容的功能需要版主權限。

版主檢視張貼內容時，可存取內容內協調旗標，其中包含新的`Feature`標幟。

![網站 — 訪客 — 體驗](assets/site-visitor-experience.png)

一旦標幟為功能，模型標幟就會變成`Unfeature`。

包含`Featured Content`元件的頁面現在會包含此貼文。

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 是實際貼文的連結。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[精選內容](essentials-featured.md)頁面。

如需將內容標幟為特色，請參閱[協調使用者產生的內容](moderate-ugc.md)。
