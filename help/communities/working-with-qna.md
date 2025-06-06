---
title: 問答論壇功能
description: 瞭解如何將QnA論壇功能新增到頁面，讓登入社群成員提問或回答問題。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 0%

---

# 問答論壇功能{#q-a-forum-feature}

## 簡介 {#introduction}

QnA （問題與回答）論壇功能為社群成員提供詢問與回答問題的區域。 它允許成員：

* 建立問題
* 新增內嵌影像（支援拖放）
* 檢視和回答問題
* 搜尋問題
* 協助稽核QnA內容
* 找出最佳答案
* 將QnA問題從一個頁面移至另一個頁面

本檔案說明：

* 將QnA論壇功能新增至AEM網站。
* `QnA`元件的組態設定。

## 將Q&amp;A論壇新增至頁面 {#adding-a-q-a-forum-to-a-page}

若要將`QnA`元件新增至作者模式的頁面，請使用元件瀏覽器來找到`Communities / QnA`，並將其拖曳至應顯示QnA論壇的頁面上。

如需必要資訊，請造訪[社群元件基本知識](/help/communities/basics.md)。

納入[必要的使用者端資料庫](/help/communities/qna-essentials.md#essentials-for-client-side)時，`QnA`元件的顯示方式如下：

![qna-component](assets/qna-component.png)

### 設定QnA {#configuring-qna}

選取置入的`QnA`元件，以便您可以存取並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### 設定標籤 {#settings-tab}

在&#x200B;**設定**&#x200B;標籤下，指定主題（問題）和回覆（回答）的設定：

* **允許附件縮圖**

  如果勾選，則會建立附加影像的縮圖。

* **附加縮圖大小上限**

  附件縮圖影像的最大尺寸（畫素）。 預設值為800 x 800。

* 縮圖的最小影像大小&#x200B;**分鐘**

  產生內嵌影像縮圖的最小影像大小（單位為位元組）。 預設值為100000位元組(100 kb)。

* **最大縮圖尺寸**

  內嵌影像的最大縮圖影像大小（畫素）。 預設值為800 x 800。

* 每頁&#x200B;**個主題**

  定義每個頁面顯示的問題/帖子數。 預設值為10。

* **已稽核**

  如果勾選，則必須先核准發佈主題和註解，才能將其顯示在發佈網站上。 預設為取消選取。

* **已關閉**

  如果勾選，論壇將關閉，並出現新的問題和評論。 預設為取消選取。

* **RTF編輯器**

  如果勾選，則可使用標籤輸入主題和註解。 預設為取消選取。

* **允許標籤**

  如果勾選，則允許成員將標籤新增至他們的貼文（請參閱&#x200B;**標籤欄位**&#x200B;標籤）。 預設為取消選取。

* **允許檔案上傳**

  如果勾選，允許將檔案附件新增至問題或註解。 預設為取消選取。

* **允許關注**

  如果勾選，則為論壇貼文納入下列功能，此功能可讓成員收到[新貼文的通知](/help/communities/notifications.md)。 預設為取消選取。

* **允許釘選**

  如果勾選，論壇主題可以釘選到主題清單的頂端。 預設為取消選取。

* **允許電子郵件訂閱**

  如果勾選，允許成員透過電子郵件（[訂閱](/help/communities/subscriptions.md)）接收新貼文的通知。 需要檢查允許下列專案，並設定[電子郵件](/help/communities/email.md)。 預設為取消選取。

* **檔案大小上限**

  只有在勾選`Allow File Uploads`時才相關。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600 (10 Mb)。

* **允許的檔案型別**

  只有在勾選`Allow File Uploads`時才相關。 以「點」分隔符號的副檔名清單（以逗號分隔）。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則無法上傳未指定的檔案型別。 預設為none，因此允許所有&#x200B;**個**&#x200B;檔案型別。

* **附加影像檔案大小上限**

  只有在勾選「允許檔案上傳」時才相關。 已上傳影像檔案的最大位元組數。 預設值為2097152 (2 Mb)。

* **允許回覆**

  如果勾選，允許回覆張貼至問題的評論。 預設為取消選取。

* **允許投票**

  如果勾選，請包含「投票」功能及問題。 預設為取消選取。

* **允許使用者刪除評論和主題**

  如果勾選，則允許成員刪除他們張貼的評論和問題。 預設為取消選取。

* **允許有特殊許可權的成員**

  如果勾選，則僅允許擁有特殊許可權的成員建立內容。

* **封鎖使用者在作者編輯模式中產生的內容**

  如果啟用，在作者模式下編輯時會封鎖使用者產生的內容。

* **將選取的答案移至頂端**

  如果勾選，則顯示的第一個答案為已選取的答案。 預設為取消選取。
* **顯示徽章**

  如果勾選，則顯示已取得及指派的[徽章](/help/communities/implementing-scoring.md)與成員的部落格專案。 預設為取消選取。

* **允許主要內容**

  如果勾選，此想法可識別為[精選內容](/help/communities/featured.md)。 預設為取消選取。

* **啟用提及功能**

  啟用後，可讓註冊社群使用者識別其他註冊成員（使用名字、姓氏、使用者名稱），並使用一般的@user-name語法標籤這些成員。 標籤的使用者會收到他們提及的通知。

* **最大提及次數**

  限制貼文中允許提及的最大數量。 預設值為10。

* **UI提及模式**

  指定允許的模式字串，以在貼文中標籤(@mention)已註冊的使用者。 例如，`~{{familyName}}{{givenName}}`。

#### 「使用者稽核」標籤 {#user-moderation-tab}

在&#x200B;**使用者稽核**&#x200B;標籤下，指定如何管理張貼的主題（問題）和答案（使用者產生的內容）。 如需詳細資訊，請參閱[仲裁使用者產生的內容](/help/communities/moderate-ugc.md)。

* **拒絕回答**

  如果勾選，則允許受信任的成員版主拒絕已發佈的答案，並防止這些答案顯示在公開的問答論壇上。 預設為取消選取。

* **關閉/重新開啟主題**

  如果勾選，受信任的成員版主可以關閉問題（主題）以進一步編輯和回答，也可以重新開啟問題。 預設為取消選取。

* **移動主題**
如果勾選，允許發佈方版主移動問題。 預設為取消選取。

* **標幟貼文**

  如果勾選，則允許成員將其他人的問題或答案標籤為不適當。 預設為取消選取。

* **標幟原因清單**

  如果勾選，則允許成員從下拉式清單中選擇標示問題或答案為不適當的原因。 預設為取消選取。

* **自訂標幟原因**

  如果勾選，則允許成員輸入自己將問題或答案標示為不適當的原因。 預設為取消選取。

* **稽核閾值**

  輸入在通知版主前，成員必須標示問題或答案的次數。 預設值為1 （一次）。

* **標幟限制**

  輸入問題或答案在隱藏於公眾檢視之前必須標幟的次數。 若設為–1，標示的問題或答案絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於「稽核臨界值」。 預設值為5。

#### 標籤欄位索引標籤 {#tag-field-tab}

在&#x200B;**標籤欄位**&#x200B;索引標籤下，如果允許在&#x200B;**設定**&#x200B;索引標籤下，則可套用的標籤會根據所選的名稱空間而受限。

* **允許的名稱空間**

  如果已在&#x200B;**設定**&#x200B;標籤下勾選`Allow Tagging`，則為相關。 可套用的標籤僅限於已核取的名稱空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設名稱空間）和「包含所有標籤」。 預設為未勾選，這表示允許所有名稱空間。

* **建議限制**

  輸入要顯示為論壇成員張貼建議之標籤數目。 **-**&#x200B;1的值表示沒有限制。 預設值為0。

#### 排序設定索引標籤 {#sort-settings-tab}

在&#x200B;**排序設定**&#x200B;標籤下，指定張貼的評論在顯示時的排序方式。

* **排序依據**

  檢查所有允許的排序選取專案： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`。 預設值為`Newest, Oldest, Last Updated`。

* **設定為預設值**

  下拉式選單，選取其中一個核取的排序選項，以顯示為預設值。 預設值為`Newest`。

* **選取Analytics排序的時間選項**

  下拉式清單以選取`All, Last 24 Hours, Last 7 Days, Last 30 Days`之一。 預設值為`All`。

## 網站訪客體驗 {#site-visitor-experience}

### 識別答案 {#identifying-answers}

使用`Select Answer`按鈕可將一個答案標籤為正確或有用的答案。 一旦問題被標示為[已回答]，則除非使用`Unmark Chosen Answer`按鈕取消選取第一個答案，否則無法選取其他答案。

選取為可行答案後，可使用`Unmark Chosen Answer`按鈕取消選取它。

一旦選取了一個答案作為可行答案，主要QnA頁面上的問題主題旁邊會顯示問題已`Answered`的指示。

#### 版主和管理員 {#moderators-and-administrators}

當登入的使用者具有版主或管理員許可權時，他們能夠執行元件設定所允許的版主任務，無論問題或答案的作者是誰。

他們還可以找出答案。

#### 成員 {#members}

網站訪客登入時，根據設定，他們可以：

* Post新問題。
* 編輯或刪除他們所編寫的問題。
* 標示其他成員的問題或答案。
* 找出他們所編寫問題的答案。

#### 匿名 {#anonymous}

未登入的網站訪客只能讀取張貼的問題和答案，如果支援的話，可將其翻譯，但無法新增問題或答案，也無法標示其他人的帖子。

## 其他資訊 {#additional-information}

如需開發人員的[QnA Essentials](/help/communities/qna-essentials.md)頁面上的詳細資訊。

如需稽核張貼的主題和評論，請參閱[稽核使用者產生的內容](/help/communities/moderate-ugc.md)。

若要標籤張貼的主題和評論，請參閱[標籤使用者產生的內容](/help/communities/tag-ugc.md)。
