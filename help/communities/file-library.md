---
title: 檔案庫功能
description: 「檔案庫」功能可讓登入的網站訪客上傳、管理和下載檔案。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# 檔案庫功能{#file-library-feature}

## 簡介 {#introduction}

檔案庫功能為登入網站訪客（社群成員）提供在社群網站內上傳、管理和下載檔案的位置。

本檔案的這一節將說明：

* 將檔案庫功能新增至AEM網站。
* 的組態設定 `File Library` 元件。

### 新增檔案庫至頁面 {#adding-a-file-library-to-a-page}

若要新增 `File Library` 將元件移至作者模式下的頁面，找出元件：

* `Communities / File Library`

並將其拖曳至頁面上的適當位置。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/essentials-file-library.md#essentials-for-client-side) 包含，這是如何 `File Library` 元件出現：

![file-library1](assets/file-library1.png)

### 設定檔案庫 {#configuring-file-library}

選取已放置的 `File Library` 元件供您存取及選取 `Configure` 圖示可開啟「編輯」對話方塊。

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### 評論索引標籤 {#comments-tab}

在 **註解** 索引標籤中，指定是否及如何顯示已上傳檔案的註解：

* **允許在檔案上評論**

  如果勾選，允許對已上傳的檔案發表評論。 預設為未勾選。

* **每頁的評論數**

  限制每頁顯示的評論數和顯示的回複數。 預設為 **10**.

* **檔案大小上限**

  此值會限制上傳的檔案大小。 預設限製為104857600 (10 MB)。

* **訊息長度上限**

  可輸入文字方塊的最大字元數。 預設為4096個字元。

* **允許的檔案型別**

  以「點」分隔符號的副檔名清單（以逗號分隔）。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則不允許未指定任何檔案型別。 預設值並未指定，因此允許所有檔案型別。

* **RTF編輯器**

  如果勾選，則可以使用標示輸入註解。 預設為未勾選。

* **刪除註解**

  如果勾選，則允許使用者刪除自己的評論。 預設為已核取。

* **允許標籤**

  如果勾選，則會啟用將標籤新增至檔案的功能。 預設為未勾選。

* **允許的名稱空間**

  如果勾選「允許標籤」 ，則可用標籤會限製為已勾選的名稱空間。 如果未核取任何名稱空間，則會允許所有名稱空間。 預設為所有名稱空間。

* **建議限制**

  如果勾選「允許標籤」，此設定會限制要顯示的建議標籤數量。 如果設為–1，則沒有限制。 預設值為–1。

* **允許投票**

  如果勾選，則會啟用投票給檔案的功能。 預設為未勾選。

* **允許關注**

  如果勾選，請在部落格中加入以下功能，讓成員能夠 [已通知](/help/communities/notifications.md) 新貼文的。 預設為未勾選。

* **啟用提及功能**

  啟用後，可讓註冊社群使用者識別其他註冊成員（使用名字、姓氏、使用者名稱），並使用一般的@user-name語法標籤這些成員。 標籤的使用者會收到他們提及的通知。

* **最大提及次數**

  限制貼文中允許提及的最大數量。 預設值為10。

* **UI提及模式**

  指定允許的樣式字串，以便在貼文中標籤(@mention)已註冊的使用者。 例如，`~{{familyName}}{{givenName}}`。

* **允許執行緒式回覆**

  如果勾選，允許回覆已發佈的評論。 預設為未勾選。

#### 「使用者稽核」標籤 {#user-moderation-tab}

在 **使用者稽核** 索引標籤中，如果允許評論，則設定評論的稽核：

* **預先稽核**

  如果勾選，註解在發佈網站上出現之前必須先經過核准。 預設為未勾選。

* **刪除註解**

  如果勾選，發表評論的訪客可視需求將其刪除。 預設為已核取。

* **拒絕評論**

  如果勾選，則允許受信任的成員版主拒絕評論。 預設為未勾選。

* **關閉/重新開啟註解**

  如果勾選，則允許受信任成員版主關閉和重新開啟註解。 預設為未勾選。

* **標幟評論**

  如果勾選，允許訪客將評論標幟為不適當。 預設為未勾選。

* **標幟原因清單**

  如果勾選，則允許訪客從下拉式清單中選擇將評論標幟為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

  如果勾選，可讓訪客輸入將評論標幟為不適當的原因。 預設為未勾選。

* **稽核臨界值**

  輸入通知版主前，評論必須被訪客標幟的次數。 預設為一次(**1**)。

* **標幟限制**

  輸入將評論從公開檢視隱藏之前必須加以標籤的次數。 此數字必須大於或等於 **稽核臨界值**. 預設值為5。

### 排序設定索引標籤 {#sort-settings-tab}

排序依據

設為預設值

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [檔案程式庫基本需知](/help/communities/essentials-file-library.md) 開發人員頁面。

有關張貼主題和評論的稽核，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

若要標籤張貼的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).
