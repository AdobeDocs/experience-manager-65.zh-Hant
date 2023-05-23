---
title: 檔案庫功能
seo-title: File Library Feature
description: 「檔案庫」功能允許登錄站點訪問者上載、管理和下載檔案
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

檔案庫功能為登錄站點訪問者（社區成員）提供了上載、管理和下載社區站點內檔案的位置。

文檔的本節介紹：

* 將檔案庫功能添加到AEM站點。
* 的配置設定 `File Library` 元件。

### 將檔案庫添加到頁面 {#adding-a-file-library-to-a-page}

添加 `File Library` 在作者模式下將元件定位到頁面中，找到元件：

* `Communities / File Library`

然後拖到頁面上。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

當 [所需的客戶端庫](/help/communities/essentials-file-library.md#essentials-for-client-side) 包括，這是 `File Library` 元件將出現：

![file-library1](assets/file-library1.png)

### 配置檔案庫 {#configuring-file-library}

選取已放置的 `File Library` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置 — 新建](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### 「注釋」頁籤 {#comments-tab}

在 **注釋** 頁籤，指定上載檔案的注釋的顯示方式和顯示方式：

* **允許在檔案上填寫意見**

   如果選中，則允許對上載的檔案發表評論。 未選中預設值。

* **每頁的評論數**

   限制每頁顯示的注釋數以及顯示的答複數。 預設值為 **10**。

* **最大檔案大小**

   此值將限制上載的檔案大小。 預設限制為104857600(10 Mb)。

* **訊息長度上限**

   可輸入到文本框中的最大字元數。 預設為4096個字元。

* **允許的檔案類型**

   以逗號分隔的檔案副檔名清單，其中帶有「點」分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入注釋。 未選中預設值。

* **刪除注釋**

   如果選中，則允許用戶刪除其自己的注釋。 選中預設值。

* **允許標記**

   如果選中，將啟用向檔案添加標籤的功能。 未選中預設值。

* **允許的命名空間**

   如果選中「允許標籤」，則可用標籤將限於選中的命名空間。 如果未選中任何項，則允許所有項。 預設值是所有命名空間。

* **建議限制**

   如果選中「允許標籤」，則此設定將限制要顯示的建議標籤數。 如果設定為–1，則無限制。 預設值為–1。

* **允許投票**

   如果選中，將啟用選定檔案的功能。 未選中預設值。

* **允許關注**

   如果選中，則為部落格包括以下功能，允許成員 [通知](/help/communities/notifications.md) 新職位。 未選中預設值。

* **啟用提及功能**

   如果啟用，則允許註冊的社區用戶標識其他已註冊成員（使用名、姓、用戶名），並使用公用@user-name語法標籤他們。 標籤用戶收到有關其提及的通知。

* **最大提及數**

   限制帖子中允許的最大提及數。 預設值為10。

* **UI 提及模式**

   指定帖子中註冊用戶的標籤(@mention)所允許的模式字串。 例如~{{familyName}}{{givenName}}。

* **允許執行緒式回覆**

   如果選中，則允許對已發佈的注釋進行答復。 未選中預設值。

#### 「用戶審核」頁籤 {#user-moderation-tab}

在 **用戶審核** 頁籤，配置注釋的審核，如果允許注釋：

* **事先審核**

   如果選中，則必須先批准注釋，然後注釋才會顯示在發佈站點上。 未選中預設值。

* **刪除注釋**

   如果選中，則發佈評論的訪問者將能夠刪除評論。 選中預設值。

* **拒絕注釋**

   如果選中，則允許受信任的成員審閱人拒絕評論。 未選中預設值。

* **關閉/重新開啟注釋**

   如果選中，則允許受信任的成員審閱人關閉並重新開啟注釋。 未選中預設值。

* **標籤注釋**

   如果選中，允許訪問者將注釋標籤為不恰當。 未選中預設值。

* **標誌原因清單**

   如果選中，允許訪問者從下拉清單中選擇將注釋標籤為不恰當的理由。 未選中預設值。

* **自定義標誌原因**

   如果選中，允許訪問者輸入將注釋標籤為不恰當的自己原因。 未選中預設值。

* **審核閾值**

   輸入訪問者在通知審閱人之前必須標籤評論的次數。 預設值為一次(**1**)。

* **標籤限制**

   輸入注釋在公共視圖中隱藏之前必須標籤的次數。 此數字必須大於或等於 **審核閾值**。 預設值為5。

### 「排序設定」頁籤 {#sort-settings-tab}

排序方式

設為預設值

### 其他資訊 {#additional-information}

有關 [檔案庫軟體包](/help/communities/essentials-file-library.md) 頁面。

有關已發佈主題和評論的審核，請參閱 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

有關為已發佈主題和注釋添加標籤，請參見 [標籤用戶生成的內容](/help/communities/tag-ugc.md)。
