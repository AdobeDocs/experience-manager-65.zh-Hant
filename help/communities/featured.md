---
title: 主要內容功能
description: 「精選內容」功能可讓登入的網站訪客強調顯示內容
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

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
* `Featured Content`元件的組態設定。

## 新增精選內容至頁面 {#adding-featured-content-to-a-page}

若要將`Featured Content`元件新增至作者模式的頁面，請使用元件瀏覽器來尋找

* `Communities / Featured Content`

並將其拖曳至主要內容應出現的頁面上。

如需必要資訊，請造訪[社群元件基本知識](basics.md)。

納入[必要的使用者端資料庫](essentials-featured.md#essentials-for-client-side)時，`Featured Content`元件的顯示方式如下：

![featuredcontent](assets/featuredcontent.png)

## 設定精選內容 {#configuring-featured-content}

選取置入的`Featured Content`元件，以便您可以存取並選取開啟編輯對話方塊的`Configure`圖示。

![設定 — 新](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 設定標籤 {#settings-tab}

在&#x200B;**[!UICONTROL 設定]**&#x200B;標籤下，識別要功能的內容：

* **[!UICONTROL 顯示名稱]**

  主要內容清單的標題。 例如，`Featured Questions`或`Featured Ideas`。 如果留空，預設值為`Featured Content`。

* **[!UICONTROL 主要內容的位置]**

  *（必要）*&#x200B;瀏覽至包含可精選內容的頁面（該頁面的元件必須設定為「允許精選內容」）。 例如，`/content/sites/engage/en/forum`。

* **[!UICONTROL 顯示限制]**

  可顯示的最大精選內容數量。 預設值為5。

## 網站訪客體驗 {#site-visitor-experience}

將內容標幟為精選內容的功能需要版主許可權。

當版主檢視張貼的內容時，可以存取內容內控仲裁旗標，其中包括新的`Feature`旗標。

![網站訪客體驗](assets/site-visitor-experience.png)

在標籤為功能後，稽核旗標會變成`Unfeature`。

包含`Featured Content`元件的頁面現在包含此貼文。

![網站訪客體驗1](assets/site-visitor-experience1.png)

`Read More`連結到實際的貼文。

## 其他資訊 {#additional-information}

如需開發人員的[精選內容](essentials-featured.md)頁面上的詳細資訊，請參閱。

若要將內容標示為精選，請參閱[仲裁使用者產生的內容](moderate-ugc.md)。
