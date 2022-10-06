---
title: 構思功能
seo-title: Ideation Feature
description: 新增和設定構想功能
seo-description: Adding and configuring the Ideation feature
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 9%

---

# 構思功能 {#ideation-feature}

## 簡介 {#introduction}

構想功能提供發佈環境中登入網站訪客（社群成員）的區域，以執行下列作業：

* 建立想法以與社群共用。
* 檢視和評論意見。
* 遵循一個想法。
* 投票。

本檔案的本節說明：

* 將構思功能新增至AEM網站。
* Identation元件的組態設定。

### 新增構想至頁面 {#adding-a-ideation-to-a-page}

新增 `Ideation` 在製作模式中，使用元件瀏覽器來尋找

* `Communities / Ideation`

並將其拖曳至應該出現構想的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的用戶端程式庫](/help/communities/ideation.md#essentials-for-client-side) 包含在內，以下為方式 `Ideation` 元件隨即出現：

![識別](assets/ideation.png)

### 設定構想 {#configuring-an-ideation}

選取已放置的 `Ideation` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![configure-new](assets/configure-new.png)

![視覺設定](assets/ideation-settings.png)

#### 設定標籤 {#settings-tab}

在 **[!UICONTROL 設定]** 索引標籤，指定想法和留言的設定：

* **允許附件縮圖**
* **附加縮圖最大尺寸**
* **最小縮圖影像大小**
* **最大縮圖尺寸**
* **允許有特殊權限的成員**
* **允許擁有特殊權限的成員**
* **封鎖使用者在作者編輯模式中產生的內容**
* **創意力標題**

* 構想的顯示標題。 預設為 `Ideation`.
* **創意力說明**

   要顯示為構想子標題的說明。 預設值為無說明。

* **每頁主題**

   定義每頁顯示的構想/貼文數量。 預設為10。

* **已審核**

   若勾選此選項，張貼意見和留言必須經過核准，才會顯示在發佈網站上。 預設為未勾選。

* **已關閉**

   若勾選此選項，將不會顯示新想法和意見。 預設為未勾選。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入構想和注釋。 預設為未勾選。

* **允許標記**

   若勾選此選項，允許成員將標籤新增至其貼文(請參閱 **[!UICONTROL 標籤欄位]** 標籤)。 預設為未勾選。

* **允許檔案上傳**

   如果選中，則允許將檔案附件添加到思想或注釋中。 預設為未勾選。

* **最大檔案大小**

   只有在 `Allow File Uploads` 已勾選。 此欄位將限制上傳檔案的大小（以位元組為單位）。 預設為104857600(10 Mb)。

* **允許的檔案類型**

   只有在 `Allow File Uploads` 已勾選。 副檔名清單（以逗號分隔）以「點」分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許上載未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **附加影像檔案最大大小**

   僅在勾選「允許檔案上傳」時相關。 上傳的影像檔案可能具有的最大位元組數。 預設為2097152(2 Mb)。

* **允許回覆**

   如果勾選此選項，則允許對張貼至構想的留言進行回覆。 預設為未勾選。

* **允許投票**

   如果勾選，則允許對構想的意見進行投票。 預設為未勾選。

* **允許使用者刪除評論和主題**

   如果勾選此選項，允許成員刪除其張貼的留言和想法。 預設為未勾選。

* **允許關注**

   若勾選此選項，請為構想貼文加入下列功能，以便讓成員 [通知](/help/communities/notifications.md) 新貼文。 預設為未勾選。

* **允許電子郵件訂閱**

   若勾選此選項，可允許成員透過電子郵件([訂閱](/help/communities/subscriptions.md))。 需要 `Allow Following` 要檢查和 [電子郵件已設定](/help/communities/email.md). 預設為未勾選。

* **允許投票**

   如果勾選，則允許對構想的意見進行投票。 預設為未勾選。

* **顯示徽章**

   如果選中，則顯示已獲得和已分配 [徽章](/help/communities/implementing-scoring.md) 會員的想法。 預設為未勾選。

* **清單頁面上不獲得回覆**

* **允許主要內容**

   若勾選，可將構想識別為 [精選內容](/help/communities/featured.md). 預設為未勾選。

* **啟用提及功能**
* **最大提及數**
* **UI 提及模式**

#### 使用者協調標籤 {#user-moderation-tab}

在 **[!UICONTROL 使用者協調]** 索引標籤，指定如何管理已張貼的意見和留言（使用者產生的內容）。 如需詳細資訊，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md).

* **拒絕貼文**

   若勾選此選項，信任的成員協調者將可拒絕貼文，並防止貼文出現在公開論壇上。 預設為未勾選。

* **關閉/重新開啟主題**

   如果選中，受信任的成員協調者可以關閉主題以進一步編輯和評論，也可以重新開啟主題。 預設為未勾選。

* **標幟貼文**

   如果選中，則允許成員將其他主題或評論標籤為不適當。 預設為未勾選。

* **標誌原因清單**

   如果選中，則允許成員從下拉清單中選擇其標籤主題或注釋為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

   如果選中，則允許成員輸入自己的原因，將主題或評論標籤為不適當。 預設為未勾選。

* **協調臨界值**

   輸入在通知協調者之前，成員必須標籤主題或評論的次數。 預設為1（一次）。

* **標幟限制**

   輸入主題或留言在從公共視圖中隱藏之前必須標籤的次數。 如果設為–1，則標籤的主題或評論永遠不會在公共視圖中隱藏。 否則，此數字必須大於或等於協調臨界值。 預設為5。

#### 標籤欄位標籤 {#tag-field-tab}

在 **[!UICONTROL 標籤欄位]** 標籤中，如果允許，則可套用的標籤 **[!UICONTROL 設定]** 標籤，會根據所選的命名空間而受到限制。

* **允許的命名空間**

   若 `Allow Tagging` 在 **[!UICONTROL 設定]** 標籤。 可套用的標籤僅限於所檢查命名空間類別中的標籤。 命名空間清單包含「標準標籤」（預設命名空間）以及「包含所有標籤」。 預設值未勾選，這表示允許所有命名空間。

* **建議限制**

   輸入要作為建議顯示給論壇成員的標籤數。 值 **-1** 表示沒有限制。 預設為0。

#### 排序設定標籤 {#sort-settings-tab}

在 **[!UICONTROL 排序設定]** 頁簽，指定在顯示張貼的留言時排序的方式。

* **排序方式**

   檢查所有允許的排序選擇： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. 預設為 `Newest, Oldest, Last Updated`.

* **設為預設值**

   下拉式清單以選取其中一個核取的排序選項，以顯示為預設值。 預設為 `Newest`.

* **選取 Analytics 排序的時間選項**

   下拉式清單以選取其中一個 `All, Last 24 Hours, Last 7 Days, Last 30 Days`. 預設為 `All`.

## 網站訪客體驗 {#site-visitor-experience}

### 建立構想 {#creating-idea}

與所有Communities功能一樣，如果未登入，網站訪客只能閱讀意見並檢視其他意見（透過留言和投票/按贊）。

登入後，成員可以建立新的構想。

![建立 — 新構想](assets/create-new-idea.png)

在提交構想之前，成員可以保存草稿。

選取 `Save as Draft` 按鈕，將保存草稿。

![儲存構想](assets/save-idea.png)

在 `My Drafts` 索引標籤，選取 `Read More` 要重新進入編輯模式，請執行以下操作：

![編輯構想](assets/edit-idea.png)

#### 提供意見反應 {#providing-feedback}

構想發佈後，其他成員即可登入，開啟構想( `Read More`)和想法一樣，這樣就會增加選票數，並發表評論。

![反饋](assets/feedback-idea.png)

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [構想要點](/help/communities/ideation.md) 頁面。

如需已張貼主題和留言的協調，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md).

有關標籤已發佈的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).
