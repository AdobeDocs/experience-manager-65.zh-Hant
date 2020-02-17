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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 檔案庫功能{#file-library-feature}

## 簡介 {#introduction}

檔案庫功能提供登入網站訪客（社群成員）在社群網站上傳、管理和下載檔案的位置。

本節說明

* 新增檔案庫功能至AEM網站
* 元件的配置設 `File Library` 置

### 新增檔案庫至頁面 {#adding-a-file-library-to-a-page}

若要在作 `File Library` 者模式下將元件新增至頁面，請找出元件

* `Communities / File Library`

並將它拖曳至頁面上的位置。

如需必要資訊，請造 [訪Communities Components Basics](/help/communities/basics.md)。

當包含 [所需的用戶端程式庫](/help/communities/essentials-file-library.md#essentials-for-client-side) ，元件的顯示方式 `File Library` 如下：

![chlimage_1-145](assets/chlimage_1-145.png)

### 配置檔案庫 {#configuring-file-library}

選擇要訪問 `File Library` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### 「注釋」頁籤 {#comments-tab}

在**Comments **tab下，指定上傳檔案的注釋是否及其顯示方式：

* **允許對檔案加上注**&#x200B;釋如果勾選，則允許對上傳的檔案加上注釋。 預設為未勾選。

* **每頁留言**&#x200B;數限制每頁顯示的留言數，以及顯示的回覆數。 預設值 **為10**。

* **檔案大小上**&#x200B;限此值將限制上傳的檔案大小。 預設限制為104857600(10 Mb)。

* **最大消息長**&#x200B;度可輸入到文本框中的最大字元數。 預設為4096個字元。

* **允許的檔案類**&#x200B;型以逗號分隔的副檔名清單，其中&quot;dot&quot;分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許** **所有檔案類型。

* **富格文本編輯**&#x200B;器如果選中此選項，則可以使用標注輸入注釋。 預設為未勾選。

* **刪除注釋**&#x200B;如果勾選此選項，則允許用戶刪除自己的注釋。 已勾選預設值。

* **允許標籤**：如果勾選此選項，將啟用將標籤添加到檔案的功能。 預設為未勾選。

* **允許的名稱**&#x200B;空間如果選中「允許標籤」，則可用的標籤將限制為選中的名稱空間。 如果未勾選任何項目，則允許所有項目。 預設值是所有名稱空間。

* **建議限制**&#x200B;如果勾選「允許標籤」，此設定會限制要顯示的建議標籤數。 如果設定為-1，則沒有限制。 預設值為-1。

* **允許投票**&#x200B;如果勾選，則會啟用檔案的投票能力。 預設為未勾選。

* **允許下**&#x200B;列：如果勾選，請為部落格文章加入下列功能，讓成員 [收到](/help/communities/notifications.md) 新貼文的通知。 預設為未勾選。

* **啟用提及** If enabled, allows registered community users to identify other registered members(using first name, last name, user name), and tag them usen @user-name syntax. 標籤使用者會收到有關其提及次數的通知。

* **最大提及**&#x200B;次數限制貼文中允許的提及次數上限。 預設值為10。

* **UI提及模式**：在貼文中指定已註冊使用者的標籤（@提及）的已授權模式字串。 例如~{{familyName}}{{givenName}}。

* **允許線程化回**&#x200B;覆如果勾選，則允許回覆張貼的留言。 預設為未勾選。

#### 使用者協調標籤 {#user-moderation-tab}

在「使用 **者協調** 」標籤下，設定留言的協調（如果允許留言）:

* **預先協調**：如果勾選，留言必須先經過核准，才會顯示在發佈網站上。 預設為未勾選。

* **刪除留言**&#x200B;如果勾選，則張貼留言的訪客可加以刪除。 已勾選預設值。

* **拒絕注釋**&#x200B;如果選中，則允許受信任成員協調者拒絕注釋。 預設為未勾選。

* **關閉／重新開啟注**&#x200B;釋如果選中，則允許受信任的成員協調者關閉並重新開啟注釋。 預設為未勾選。

* **標籤注**&#x200B;釋如果勾選，允許訪客將注釋標籤為不適當。 預設為未勾選。

* **標幟原因清**&#x200B;單如果勾選，允許訪客從下拉式清單中選擇將留言標籤為不適當的原因。 預設為未勾選。

* **自訂標幟原**&#x200B;因：如果勾選，允許訪客輸入自己將留言標籤為不適當的原因。 預設為未勾選。

* **協調臨**&#x200B;界值輸入在通知協調者之前，訪客必須標籤留言的次數。 預設值為一次(**1**)。

* **標籤限**&#x200B;制輸入留言在隱藏於公開檢視之前必須標籤的次數。 此數字必須大於或等於「協調臨界 **值」**。 預設值為5。

### 「排序設定」頁籤 {#sort-settings-tab}

排序方式

設為預設值

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員 [的「檔案庫](/help/communities/essentials-file-library.md) 」 Essentials頁面。

如需協調已張貼主題和留言的資訊，請參 [閱協調使用者產生的內容](/help/communities/moderate-ugc.md)。

如需標籤已張貼的主題和留言，請參 [閱標籤使用者產生的內容](/help/communities/tag-ugc.md)。
