---
title: 創意力功能
description: 瞭解如何新增及設定構思功能，該功能可讓社群成員針對與社群共用的構思進行建立、檢視、關注、投票及評論。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 9%

---

# 創意力功能 {#ideation-feature}

## 簡介 {#introduction}

創意力功能為發佈環境中的登入網站訪客（社群成員）提供一個區域，以：

* 建立想法並與社群分享。
* 檢視和評論創意。
* 遵循構想。
* 投票支援一個想法。

本檔案的這一節將說明：

* 將創意力功能新增至AEM網站。
* 創意力元件的組態設定。

### 將構思新增至頁面 {#adding-a-ideation-to-a-page}

若要新增 `Ideation` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Ideation`

並將其拖曳至應顯示創意的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/ideation.md#essentials-for-client-side) 包含，這就是 `Ideation` 元件出現：

![創意力](assets/ideation.png)

### 設定構思 {#configuring-an-ideation}

選取已放置的 `Ideation` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![configure-new](assets/configure-new.png)

![創意力設定](assets/ideation-settings.png)

#### 設定標籤 {#settings-tab}

在 **[!UICONTROL 設定]** 索引標籤，指定想法和評論的設定：

* **允許附件縮圖**
* **附加縮圖最大尺寸**
* **最小縮圖影像大小**
* **最大縮圖尺寸**
* **允許有特殊權限的成員**
* **允許擁有特殊權限的成員**
* **封鎖使用者在作者編輯模式中產生的內容**
* **創意力標題**

* 想法的顯示標題。 預設為 `Ideation`.
* **創意力說明**

  要顯示為創意副標題的說明。 預設為無說明。

* **每頁主題**

  定義每個頁面顯示的想法/貼文數。 預設值為10。

* **已審核**

  如果勾選，則必須先核准發佈想法和評論，才能將其顯示在發佈網站上。 預設為未勾選。

* **已關閉**

  如果勾選，創意力論壇將關閉以接受新的想法和評論。 預設為未勾選。

* **RTF 編輯器**

  如果勾選，便可使用標籤輸入想法和評論。 預設為未勾選。

* **允許標記**

  如果勾選，則允許成員將標籤新增至他們的貼文(請參閱 **[!UICONTROL 標籤欄位]** 標籤)。 預設為未勾選。

* **允許檔案上傳**

  如果勾選，允許將檔案附件新增至創意或註解中。 預設為未勾選。

* **最大檔案大小**

  只有在 `Allow File Uploads` 已勾選。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600 (10 Mb)。

* **允許的檔案類型**

  只有在 `Allow File Uploads` 已勾選。 以「點」分隔符號的副檔名清單（以逗號分隔）。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則無法上傳未指定的檔案型別。 預設為「無」，因此允許所有檔案型別。

* **附加影像檔案最大大小**

  只有在勾選「允許檔案上傳」時才相關。 已上傳影像檔案的最大位元組數。 預設值為2097152 (2 Mb)。

* **允許回覆**

  如果勾選，允許回覆張貼至創意的評論。 預設為未勾選。

* **允許投票**

  如果勾選，則允許對創意的評論進行投票。 預設為未勾選。

* **允許使用者刪除評論和主題**

  如果勾選，則允許成員刪除他們發表的評論和想法。 預設為未勾選。

* **允許關注**

  如果勾選，在創意貼文中加入以下功能，讓成員能夠 [已通知](/help/communities/notifications.md) 新貼文的。 預設為未勾選。

* **允許電子郵件訂閱**

  如果勾選，允許成員透過電子郵件接收新貼文的通知([訂閱](/help/communities/subscriptions.md))。 需要 `Allow Following` 待核取及 [電子郵件已設定](/help/communities/email.md). 預設為未勾選。

* **允許投票**

  如果勾選，則允許對創意的評論進行投票。 預設為未勾選。

* **顯示徽章**

  如果勾選，則顯示已習得和已指派 [徽章](/help/communities/implementing-scoring.md) 依成員的想法。 預設為未勾選。

* **不在清單頁面上取得回覆**

* **允許主要內容**

  如果勾選，該創意可識別為 [主要內容](/help/communities/featured.md). 預設為未勾選。

* **啟用提及功能**
* **最大提及數**
* **UI 提及模式**

#### 「使用者稽核」標籤 {#user-moderation-tab}

在 **[!UICONTROL 使用者稽核]** 索引標籤中，指定如何管理已發佈的想法和評論（使用者產生的內容）。 如需詳細資訊，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

* **拒絕貼文**

  如果勾選，受信任的成員版主可以拒絕貼文，並防止貼文出現在公開論壇上。 預設為未勾選。

* **關閉/重新開啟主題**

  如果勾選，受信任的成員版主可能會關閉主題以進一步編輯和註釋，也可能重新開啟主題。 預設為未勾選。

* **標幟帖子**

  如果勾選，則允許成員將其他人的主題或評論標籤為不適當。 預設為未勾選。

* **標幟原因清單**

  如果勾選，則允許成員從下拉式清單中選擇標幟主題或評論為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

  如果勾選，則允許成員輸入將主題或評論標幟為不適當的原因。 預設為未勾選。

* **稽核臨界值**

  輸入在通知版主前，主題或評論必須由成員標幟的次數。 預設值為1 （一次）。

* **標幟限制**

  輸入主題或註解在隱藏於公眾檢視之前必須加上標籤的次數。 如果設為–1，則標幟的主題或註解絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於「稽核臨界值」。 預設值為5。

#### 標籤欄位索引標籤 {#tag-field-tab}

在 **[!UICONTROL 標籤欄位]** 標籤中，如果允許的話，則會套用的標籤 **[!UICONTROL 設定]** 索引標籤中，會根據選取的名稱空間而有所限制。

* **允許的命名空間**

  相關條件 `Allow Tagging` 已勾選下方的 **[!UICONTROL 設定]** 標籤。 可套用的標籤僅限於已核取的名稱空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設名稱空間）和「包含所有標籤」。 預設為未勾選，這表示允許所有名稱空間。

* **建議限制**

  輸入要顯示為論壇成員張貼建議之標籤數目。 值 **-1** 表示沒有限制。 預設值為0。

#### 排序設定索引標籤 {#sort-settings-tab}

在 **[!UICONTROL 排序設定]** 索引標籤，指定張貼的評論在顯示時的排序方式。

* **排序方式**

  檢查所有允許的排序選擇： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. 預設為 `Newest, Oldest, Last Updated`.

* **設為預設值**

  下拉式選單，選取其中一個核取的排序選項，以顯示為預設值。 預設為 `Newest`.

* **選取 Analytics 排序的時間選項**

  下拉以選取其中一項 `All, Last 24 Hours, Last 7 Days, Last 30 Days`. 預設為 `All`.

## 網站訪客體驗 {#site-visitor-experience}

### 建立構想 {#creating-idea}

如同所有Communities功能，網站訪客若未登入，可能只能讀取想法並檢視其他意見（透過評論和投票/點讚）。

登入後，成員可能會建立想法。

![create-new-idea](assets/create-new-idea.png)

在提交構想之前，成員可以儲存草稿。

藉由選取 `Save as Draft` 按鈕，草稿即會儲存。

![儲存構想](assets/save-idea.png)

在中檢視已儲存的草稿時 `My Drafts` 索引標籤，選取 `Read More` 若要重新進入編輯模式，請執行下列動作：

![編輯 — 創意](assets/edit-idea.png)

#### 提供意見回饋 {#providing-feedback}

當想法發佈後，其他成員可以登入，開啟想法( `Read More`)並加上註解，因此可增加票數並發表評論。

![意見反應](assets/feedback-idea.png)

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [創意力基本要素](/help/communities/ideation.md) 開發人員頁面。

有關張貼主題和評論的稽核，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

若要標籤張貼的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).
