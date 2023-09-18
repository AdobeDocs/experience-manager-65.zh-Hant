---
title: 主要內容功能
description: 「精選內容」功能可讓登入的網站訪客強調顯示內容
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# 主要內容功能 {#featured-content-feature}

## 簡介 {#introduction}

精選內容功能為發佈環境中的登入網站訪客（社群成員）提供一個區域，以反白顯示以下內容：

* [部落格](blog-feature.md)
* [行事曆](calendar.md)
* [論壇](forum.md)
* [構思](ideation-feature.md)
* [QnA](working-with-qna.md)

將內容標示為精選內容後，即會在此元件中列出，並放置在容易引起社群成員注意的特定登陸頁面或區域。

每個元件可允許或不允許特色內容的功能。

本檔案的這一節將說明：

* 新增精選內容至社群網站。
* 的組態設定 `Featured Content` 元件。

## 新增精選內容至頁面 {#adding-featured-content-to-a-page}

若要新增 `Featured Content` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Featured Content`

並將其拖曳至主要內容應出現的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-featured.md#essentials-for-client-side) 包含，這就是 `Featured Content` 元件出現：

![功能內容](assets/featuredcontent.png)

## 設定精選內容 {#configuring-featured-content}

選取已放置的 `Featured Content` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 設定標籤 {#settings-tab}

在 **[!UICONTROL 設定]** 索引標籤中，識別要功能的內容：

* **[!UICONTROL 顯示名稱]**

  主要內容清單的標題。 例如， `Featured Questions` 或 `Featured Ideas`. 預設為 `Featured Content` 若留空。

* **[!UICONTROL 主要內容的位置]**

  *（必要）* 瀏覽至包含精選內容的頁面（該頁面的元件必須設定為「允許精選內容」）。 例如，`/content/sites/engage/en/forum`。

* **[!UICONTROL 顯示限制]**

  可顯示的最大精選內容數量。 預設值為5。

## 網站訪客體驗 {#site-visitor-experience}

將內容標幟為精選內容的功能需要版主許可權。

版主檢視張貼的內容時，可存取內容內文版主旗標，包括新的 `Feature` 標幟。

![site-visitor-experience](assets/site-visitor-experience.png)

標籤為功能後，稽核旗標會變成 `Unfeature`.

包含 `Featured Content` 元件，現在包含此貼文。

![site-visitor-experience1](assets/site-visitor-experience1.png)

此 `Read More` 實際貼文的連結。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [主要內容](essentials-featured.md) 開發人員頁面。

若要將內容標幟為精選，請參閱 [稽核使用者產生的內容](moderate-ugc.md).
