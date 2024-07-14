---
title: 創意力功能
description: 瞭解如何新增及設定構思功能，該功能可讓社群成員針對與社群共用的構思進行建立、檢視、關注、投票及評論。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---

# 創意力功能 {#ideation-feature}

## 簡介 {#introduction}

創意力功能為Publish環境中的登入網站訪客（社群成員）提供一個區域，以：

* 建立想法並與社群分享。
* 檢視和評論創意。
* 遵循構想。
* 投票支援一個想法。

本檔案的這一節將說明：

* 將創意力功能新增至AEM網站。
* 創意力元件的組態設定。

### 將構思新增至頁面 {#adding-a-ideation-to-a-page}

若要將`Ideation`元件新增至作者模式的頁面，請使用元件瀏覽器來尋找

* `Communities / Ideation`

並將其拖曳至應顯示創意的頁面上。

如需必要資訊，請造訪[社群元件基本知識](/help/communities/basics.md)。

納入[必要的使用者端資料庫](/help/communities/ideation.md#essentials-for-client-side)時，`Ideation`元件的顯示方式如下：

![構思](assets/ideation.png)

### 設定構思 {#configuring-an-ideation}

選取置入的`Ideation`元件，以便您可以存取並選取開啟編輯對話方塊的`Configure`圖示。

![設定 — 新](assets/configure-new.png)

![創意力設定](assets/ideation-settings.png)

#### 設定標籤 {#settings-tab}

在&#x200B;**[!UICONTROL 設定]**&#x200B;標籤下，指定想法和評論的設定：

* **允許附件縮圖**
* **附加縮圖大小上限**
* 縮圖的最小影像大小&#x200B;**分鐘**
* **最大縮圖尺寸**
* **允許有特殊許可權的成員**
* **允許的有特殊許可權的成員**
* **封鎖使用者在作者編輯模式中產生的內容**
* **創意力標題**

* 想法的顯示標題。 預設值為`Ideation`。
* **創意力說明**

  要顯示為創意副標題的說明。 預設為無說明。

* 每頁&#x200B;**個主題**

  定義每個頁面顯示的想法/貼文數。 預設值為10。

* **已稽核**

  如果勾選，則必須先核准發佈想法和評論，才能將其顯示在發佈網站上。 預設為未勾選。

* **已關閉**

  如果勾選，創意力論壇將關閉以接受新的想法和評論。 預設為未勾選。

* **RTF編輯器**

  如果勾選，便可使用標籤輸入想法和評論。 預設為未勾選。

* **允許標籤**

  如果勾選，則允許成員將標籤新增至他們的貼文（請參閱&#x200B;**[!UICONTROL 標籤欄位]**&#x200B;標籤）。 預設為未勾選。

* **允許檔案上傳**

  如果勾選，允許將檔案附件新增至創意或註解中。 預設為未勾選。

* **檔案大小上限**

  只有在勾選`Allow File Uploads`時才相關。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600 (10 Mb)。

* **允許的檔案型別**

  只有在勾選`Allow File Uploads`時才相關。 以「點」分隔符號的副檔名清單（以逗號分隔）。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則無法上傳未指定的檔案型別。 預設為「無」，因此允許所有檔案型別。

* **附加影像檔案大小上限**

  只有在勾選「允許檔案上傳」時才相關。 已上傳影像檔案的最大位元組數。 預設值為2097152 (2 Mb)。

* **允許回覆**

  如果勾選，允許回覆張貼至創意的評論。 預設為未勾選。

* **允許投票**

  如果勾選，則允許對創意的評論進行投票。 預設為未勾選。

* **允許使用者刪除評論和主題**

  如果勾選，則允許成員刪除他們發表的評論和想法。 預設為未勾選。

* **允許關注**

  如果勾選，在創意貼文中加入下列功能，讓會員收到[新貼文的通知](/help/communities/notifications.md)。 預設為未勾選。

* **允許電子郵件訂閱**

  如果勾選，允許成員透過電子郵件（[訂閱](/help/communities/subscriptions.md)）接收新貼文的通知。 需要檢查`Allow Following`，並設定[電子郵件](/help/communities/email.md)。 預設為未勾選。

* **允許投票**

  如果勾選，則允許對創意的評論進行投票。 預設為未勾選。

* **顯示徽章**

  如果勾選，則顯示已取得及指派的[徽章](/help/communities/implementing-scoring.md)與成員的想法。 預設為未勾選。

* **清單頁面上未收到回覆**

* **允許主要內容**

  如果勾選，此想法可識別為[精選內容](/help/communities/featured.md)。 預設為未勾選。

* **啟用提及功能**
* **最大提及次數**
* **UI提及模式**

#### 「使用者稽核」標籤 {#user-moderation-tab}

在「**[!UICONTROL 使用者稽核]**」標籤下，指定如何管理張貼的創意和評論（使用者產生的內容）。 如需詳細資訊，請參閱[仲裁使用者產生的內容](/help/communities/moderate-ugc.md)。

* **拒絕貼文**

  如果勾選，受信任的成員版主可以拒絕貼文，並防止貼文出現在公開論壇上。 預設為未勾選。

* **關閉/重新開啟主題**

  如果勾選，受信任的成員版主可能會關閉主題以進一步編輯和註釋，也可能重新開啟主題。 預設為未勾選。

* **標幟貼文**

  如果勾選，則允許成員將其他人的主題或評論標籤為不適當。 預設為未勾選。

* **標幟原因清單**

  如果勾選，則允許成員從下拉式清單中選擇標幟主題或評論為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

  如果勾選，則允許成員輸入將主題或評論標幟為不適當的原因。 預設為未勾選。

* **稽核閾值**

  輸入在通知版主前，主題或評論必須由成員標幟的次數。 預設值為1 （一次）。

* **標幟限制**

  輸入主題或註解在隱藏於公眾檢視之前必須加上標籤的次數。 如果設為–1，則標幟的主題或註解絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於「稽核臨界值」。 預設值為5。

#### 標籤欄位索引標籤 {#tag-field-tab}

在&#x200B;**[!UICONTROL 標籤欄位]**&#x200B;標籤下，如果允許在&#x200B;**[!UICONTROL 設定]**&#x200B;標籤下，則可能套用的標籤會根據所選的名稱空間而受限。

* **允許的名稱空間**

  如果已在&#x200B;**[!UICONTROL 設定]**&#x200B;標籤下勾選`Allow Tagging`，則為相關。 可套用的標籤僅限於已核取的名稱空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設名稱空間）和「包含所有標籤」。 預設為未勾選，這表示允許所有名稱空間。

* **建議限制**

  輸入要顯示為論壇成員張貼建議之標籤數目。 值&#x200B;**-1**&#x200B;表示沒有限制。 預設值為0。

#### 排序設定索引標籤 {#sort-settings-tab}

在&#x200B;**[!UICONTROL 排序設定]**&#x200B;標籤下，指定張貼的評論在顯示時的排序方式。

* **排序依據**

  檢查所有允許的排序選取專案： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`。 預設值為`Newest, Oldest, Last Updated`。

* **設定為預設值**

  下拉式選單，選取其中一個核取的排序選項，以顯示為預設值。 預設值為`Newest`。

* **選取Analytics排序的時間選項**

  下拉以選取`All, Last 24 Hours, Last 7 Days, Last 30 Days`之一。 預設值為`All`。

## 網站訪客體驗 {#site-visitor-experience}

### 建立構想 {#creating-idea}

如同所有Communities功能，網站訪客若未登入，可能只能讀取想法並檢視其他意見（透過評論和投票/點讚）。

登入後，成員可能會建立想法。

![create-new-idea](assets/create-new-idea.png)

在提交構想之前，成員可以儲存草稿。

選取`Save as Draft`按鈕即可儲存草稿。

![儲存想法](assets/save-idea.png)

在`My Drafts`標籤中檢視儲存的草稿時，選取`Read More`以重新進入編輯模式：

![編輯 — 想法](assets/edit-idea.png)

#### 提供意見回饋 {#providing-feedback}

當想法發佈後，其他成員可以登入、開啟想法( `Read More`)並點讚該想法，從而增加票數並發表評論。

![意見反應](assets/feedback-idea.png)

### 其他資訊 {#additional-information}

如需開發人員的[Ideation Essentials](/help/communities/ideation.md)頁面上的詳細資訊。

如需稽核張貼的主題和評論，請參閱[稽核使用者產生的內容](/help/communities/moderate-ugc.md)。

若要標籤張貼的主題和評論，請參閱[標籤使用者產生的內容](/help/communities/tag-ugc.md)。
