---
title: 檔案庫功能
seo-title: 檔案庫功能
description: 「檔案庫」功能可讓登入網站的訪客上傳、管理和下載檔案
seo-description: 「檔案庫」功能可讓登入網站的訪客上傳、管理和下載檔案
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: cdbe098ada0b6c50952284f92cc2063435034a38
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 7%

---


# 檔案庫功能{#file-library-feature}

## 簡介 {#introduction}

檔案庫功能提供登入網站訪客（社群成員）在社群網站上傳、管理和下載檔案的位置。

本檔案章節說明：

* 新增檔案庫功能至AEM網站。
* `File Library`元件的配置設定。

### 將檔案庫添加到頁面{#adding-a-file-library-to-a-page}

要在作者模式下將`File Library`元件添加到頁面，請找到該元件：

* `Communities / File Library`

並將它拖曳至頁面上的位置。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

當包含[必要的用戶端程式庫](/help/communities/essentials-file-library.md#essentials-for-client-side)時，`File Library`元件的顯示方式如下：

![file-library1](assets/file-library1.png)

### 配置檔案庫{#configuring-file-library}

選擇要訪問的已放置的`File Library`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### 「注釋」頁籤{#comments-tab}

在&#x200B;**Comments**&#x200B;標籤下，指定上傳檔案的注釋是否及顯示方式：

* **允許在檔案上填寫意見**

   如果勾選，則允許對已上傳的檔案加上註解。 預設為未勾選。

* **每頁的評論數**

   限制每頁顯示的留言數，以及顯示的回覆數。 預設值為&#x200B;**10**。

* **最大檔案大小**

   此值將限制上傳的檔案大小。 預設限制為104857600(10 Mb)。

* **訊息長度上限**

   文字方塊中可輸入的字元數上限。 預設為4096個字元。

* **允許的檔案類型**

   以逗號分隔的副檔名清單，並以&quot;dot&quot;分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **RTF 編輯器**

   如果選中，則可以使用標注輸入注釋。 預設為未勾選。

* **刪除注釋**

   如果勾選，則允許使用者刪除自己的注釋。 已勾選預設值。

* **允許標記**

   如果勾選，將啟用新增標籤至檔案的功能。 預設為未勾選。

* **允許的命名空間**

   如果勾選「允許標籤」，則可用標籤將限制為勾選的名稱空間。 如果未勾選任何項目，則允許所有項目。 預設值是所有名稱空間。

* **建議限制**

   如果勾選「允許標籤」，此設定會限制要顯示的建議標籤數。 如果設定為-1，則沒有限制。 預設值為-1。

* **允許投票**

   如果勾選，則會啟用檔案的投票能力。 預設為未勾選。

* **允許關注**

   如果勾選，請為部落格文章加入下列功能，讓成員能夠收到新貼文的[通知。 ](/help/communities/notifications.md)預設為未勾選。

* **啟用提及功能**

   如果啟用，則允許註冊的社區用戶標識其他已註冊成員（使用名、姓、用戶名），並使用通用的@user-name語法標籤這些成員。 標籤使用者會收到有關其提及次數的通知。

* **最大提及數**

   限制貼文中允許的提及次數上限。 預設值為10。

* **UI 提及模式**

   將已授權的模式字串指定為貼文中已註冊使用者的標籤（@提及）。 例如~{{familyName}}{{givenName}}。

* **允許執行緒式回覆**

   如果勾選，則允許回覆已張貼的留言。 預設為未勾選。

#### 使用者協調標籤{#user-moderation-tab}

在&#x200B;**使用者協調**&#x200B;標籤下，設定留言的協調（如果允許留言）:

* **事先審核**

   如果勾選，則必須先核准註解，才能顯示在發佈網站上。 預設為未勾選。

* **刪除注釋**

   如果勾選，則張貼留言的訪客可加以刪除。 已勾選預設值。

* **拒絕注釋**

   如果勾選，則允許受信任的成員協調者拒絕注釋。 預設為未勾選。

* **關閉／重新開啟注釋**

   如果勾選，則允許受信任的成員協調者關閉並重新開啟注釋。 預設為未勾選。

* **標籤注釋**

   如果勾選，允許訪客將注釋標示為不當。 預設為未勾選。

* **標籤原因清單**

   如果勾選，允許訪客從下拉式清單中選擇將留言標籤為不適當的理由。 預設為未勾選。

* **自訂標幟原因**

   如果勾選，允許訪客輸入將留言標示為不適當的原因。 預設為未勾選。

* **協調臨界值**

   輸入在通知協調者之前，訪客必須標籤留言的次數。 預設為一次(**1**)。

* **標幟限制**

   輸入留言在公開檢視中隱藏前必須標籤的次數。 此數字必須大於或等於&#x200B;**協調臨界值**。 預設值為5。

### 排序設定頁籤{#sort-settings-tab}

排序方式

設為預設值

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[File Library Essentials](/help/communities/essentials-file-library.md)頁面。

如需協調已張貼主題和留言的資訊，請參閱[協調使用者產生的內容](/help/communities/moderate-ugc.md)。

如需標籤已張貼的主題和留言，請參閱[標籤使用者產生的內容](/help/communities/tag-ugc.md)。
