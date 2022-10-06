---
title: 檔案庫功能
seo-title: File Library Feature
description: 「檔案庫」功能可讓登入的網站訪客上傳、管理和下載檔案
seo-description: The File Library feature lets signed-in site visitors upload, manage, and download files
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 7%

---

# 檔案庫功能{#file-library-feature}

## 簡介 {#introduction}

檔案庫功能提供一個位置，讓登入網站訪客（社群成員）可以上傳、管理和下載社群網站中的檔案。

本檔案的本節說明：

* 將檔案程式庫功能新增至AEM網站。
* 的組態設定 `File Library` 元件。

### 將檔案庫新增至頁面 {#adding-a-file-library-to-a-page}

新增 `File Library` 在製作模式中，找到元件至頁面：

* `Communities / File Library`

並將其拖曳到頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的用戶端程式庫](/help/communities/essentials-file-library.md#essentials-for-client-side) 包含在內，以下為方式 `File Library` 元件隨即出現：

![file-library1](assets/file-library1.png)

### 配置檔案庫 {#configuring-file-library}

選取已放置的 `File Library` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### 「注釋」頁簽 {#comments-tab}

在 **註解** 索引標籤，指定上傳檔案的註解是否及顯示方式：

* **允許在檔案上填寫意見**

   如果勾選此選項，則允許對上傳的檔案加上註解。 預設為未勾選。

* **每頁的評論數**

   限制每頁顯示的留言數以及顯示的回覆數。 預設為 **10**.

* **最大檔案大小**

   此值將限制上傳的檔案大小。 預設限制為104857600(10 Mb)。

* **訊息長度上限**

   可輸入文本框的字元數上限。 預設為4096個字元。

* **允許的檔案類型**

   副檔名清單（以逗號分隔）以「點」分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入注釋。 預設為未勾選。

* **刪除注釋**

   如果勾選此選項，則允許使用者刪除其自己的留言。 已勾選預設值。

* **允許標記**

   若勾選此選項，系統將會啟用將標籤新增至檔案的功能。 預設為未勾選。

* **允許的命名空間**

   如果勾選「允許標籤」，可用的標籤將僅限於勾選的命名空間。 如果未勾選任何項目，則允許所有項目。 預設值為所有命名空間。

* **建議限制**

   如果勾選「允許標籤」，此設定會限制要顯示的建議標籤數。 如果設為–1，則沒有限制。 預設為–1。

* **允許投票**

   如果勾選此選項，將啟用檔案的投票能力。 預設為未勾選。

* **允許關注**

   若勾選此選項，請為部落格文章加入下列功能，以便讓成員 [通知](/help/communities/notifications.md) 新貼文。 預設為未勾選。

* **啟用提及功能**

   如果啟用，則允許註冊的社區用戶標識其他註冊成員（使用名字、姓氏、用戶名），並使用通用@user-name語法對它們進行標籤。 標籤的使用者會收到其提及次數的通知。

* **最大提及數**

   限制貼文中允許的提及次數上限。 預設為10。

* **UI 提及模式**

   指定允許的模式字串，以標籤(@mention)貼文中已註冊的使用者。 例如~{{familyName}}{{givenName}}.

* **允許執行緒式回覆**

   如果選中，則允許對已發佈的評論進行答復。 預設為未勾選。

#### 使用者協調標籤 {#user-moderation-tab}

在 **使用者協調** ，設定留言的協調（如果允許留言）:

* **事先審核**

   如果勾選此選項，註解必須先經過核准，才會顯示在發佈網站上。 預設為未勾選。

* **刪除注釋**

   若勾選此選項，則張貼留言的訪客將能刪除留言。 已勾選預設值。

* **拒絕評論**

   如果選中，則允許受信任的成員協調者拒絕評論。 預設為未勾選。

* **關閉/重新開啟注釋**

   如果選中，則允許受信任的成員協調者關閉和重新開啟注釋。 預設為未勾選。

* **標幟留言**

   如果勾選此選項，允許訪客將留言標示為不適當。 預設為未勾選。

* **標誌原因清單**

   如果勾選此選項，允許訪客從下拉式清單中選擇將留言標示為不適當的理由。 預設為未勾選。

* **自訂標幟原因**

   若勾選此選項，允許訪客輸入將留言標示為不適當的自己原因。 預設為未勾選。

* **協調臨界值**

   輸入在通知協調者之前，訪客必須標籤留言的次數。 預設為一次(**1**)。

* **標幟限制**

   輸入在從公共視圖中隱藏評論之前必須標籤該評論的次數。 此數字必須大於或等於 **協調臨界值**. 預設為5。

### 排序設定標籤 {#sort-settings-tab}

排序方式

設為預設值

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [檔案庫要點](/help/communities/essentials-file-library.md) 頁面。

如需已張貼主題和留言的協調，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md).

有關標籤已發佈的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).
