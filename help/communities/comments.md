---
title: 使用註解
description: 「註解」功能可讓登入的網站訪客分享他們的意見和知識
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: c667a1658e43bb5b61daede5f94256dae582a4fc
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 4%

---

# 使用註解 {#using-comments}

## 簡介 {#introduction}

「註解」功能是用來允許登入的網站訪客（成員）分享他們對於網站內容的意見與知識。 此功能通常已存在於其他功能中，但可新增至任何網站。

本檔案說明：

* 新增 `Comments` 至頁面。
* 的組態設定 `Comments` 元件。

>[!NOTE]
>
>不支援評論的匿名張貼。 網站訪客必須註冊（成為會員）並登入才能參與。

### 新增註解至頁面 {#adding-comments-to-a-page}

若要新增 `Comments` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Comments`

並將其拖曳至頁面上的適當位置，例如與功能相關的位置（可供使用者評論），或僅拖曳至頁面底部。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/essentials-comments.md#essentials-for-client-side) 包含，這就是 `Comments` 元件出現。

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>只有一個 `Comments` 元件可能存在於頁面上。 請注意，若干Communities功能已包含評論，例如部落格、行事曆、論壇、QnA和評論。

### 設定註解 {#configuring-comments}

選取已放置的 `Comments` 元件以存取和選取 `Configure` 圖示可開啟編輯對話方塊。

![設定圖示](assets/configure.png)

![註解設定](assets/commentssettings.png)

#### 評論索引標籤 {#comments-tab}

在 **註解** 索引標籤，指定訪客輸入註解的方式。

* **允許回覆**

  如果勾選，則允許成員回覆現有註解。 預設為取消選取。

* **每頁的評論數**

  限制每頁顯示的評論數和顯示的回複數。 預設值為10。

* **允許檔案上傳**

  如果勾選，上傳檔案的選項會顯示文字輸入方塊。 預設為取消選取。

* **最大檔案大小**

  只有在勾選「允許檔案上傳」時才相關。 此值會限制上傳的檔案大小。 預設限製為10 MB。

* **訊息長度上限**

  可輸入文字方塊的最大字元數。 預設為4096個字元。

* **允許的檔案類型**

  只有在勾選「允許檔案上傳」時才相關。 以「點」分隔符號的副檔名清單（以逗號分隔）。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則不允許未指定的檔案型別。 預設為「無」，因此允許所有檔案型別。

* **RTF 編輯器**

  如果勾選，則會以標示輸入註解。 預設為取消選取。

* **允許投票**

  如果勾選，會以文字輸入方塊顯示向上或向下投票的選項。 預設為取消選取。

* **允許關注**

  如果勾選，則允許成員關注註解。 預設為取消選取。

* **顯示徽章**

  如果勾選，允許顯示已贏取和已授與的徽章。 預設為取消選取。

#### 「使用者稽核」標籤 {#user-moderation-tab}

在 **使用者稽核** 索引標籤，指定如何管理張貼的評論。 如需詳細資訊，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

* **事先審核**

  如果勾選，註解在發佈網站上出現之前必須先經過核准。 預設為取消選取。

* **刪除注釋**

  如果勾選，發表評論的成員將獲得刪除評論的功能。 預設為取消選取。

* **拒絕評論**

  如果勾選，則允許版主拒絕評論。 預設為取消選取。

* **關閉/重新開啟註解**

  如果勾選，則允許版主關閉和重新開啟註解。 預設為取消選取。

* **標幟評論**

  如果勾選，則允許成員將評論標籤為不適當。 預設為取消選取。

* **標幟原因清單**

  如果勾選，則允許成員從下拉式清單中選擇將評論標幟為不適當的原因。 預設為取消選取。

* **自訂標幟原因**

  如果勾選，則允許成員輸入將評論標幟為不適當的原因。 預設為取消選取。

* **稽核臨界值**

  輸入在通知版主前，評論必須由成員標幟的次數。 預設為一次(1)。

* **標幟限制**

  輸入將評論從公開檢視隱藏之前必須加以標籤的次數。 此數字必須大於或等於 **稽核臨界值**. 預設值為5。

#### 排序設定索引標籤 {#sort-settings-tab}

在 **排序設定** 索引標籤，指定張貼的評論在顯示時的排序方式。

* **排序欄位**

  下拉以選取其中一項 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`，或 `Most Liked`.

* **排序順序**

  下拉以選取其中一項 `Ascending` 或 `Descending`.

### 變更為自訂註解型別 {#changing-to-a-custom-comment-type}

透過變更註解資源型別，註解系統不再使用預設值產生註解的執行個體，而是由開發人員自訂（延伸）的執行個體。

知道自訂資源型別後，請輸入 [設計模式](/help/sites-authoring/default-components-designmode.md) 並連按兩下置入的 `Comments` 元件以開啟具有額外索引標籤的對話方塊。

在 **資源型別** 頁簽，為的新執行個體指定自訂resourceType `Comments or Voting` 元件：

![resource-type](assets/resource-type.png)

* **評論資源類型**

  導覽至擴充功能的resourceType `comment` /apps中的元件（單一註釋）。 例如 `/apps/social/commons/components/hbs/comments/comment`

  此資源可識別訪客發表評論時建立的UGC的resourceType。

* **投票資源類型**

  導覽至擴充功能的resourceType `voting` /apps中的元件。 例如 `/apps/social/components/hbs/voting`

  此資源會識別訪客張貼投票時建立的UGC資源型別。

* **註解系統資源型別**

  導覽至擴充功能的resourceType `comments`/apps中的元件（註解系統）。 除非頁面範本，否則保留空白 [動態包含](/help/communities/scf.md#add-or-include-a-communities-component) 基礎指令碼中的「註解系統」，而非以資源（註解節點）的形式新增至頁面。 閱讀以下內容，瞭解更多： [`{{include}}` 協助程式](/help/communities/handlebars-helpers.md#include).

### 網站訪客體驗 {#site-visitor-experience}

#### 版主和管理員 {#moderators-and-administrators}

當登入的使用者具有版主或管理員許可權時，無論評論的作者是誰，他們都能執行元件設定所允許的版主任務。

#### 成員 {#members}

網站訪客登入時，根據設定，他們可能

* 發表新評論
* 編輯自己的評論
* 刪除自己的評論
* 標幟其他人的評論

#### 匿名 {#anonymous}

未登入的網站訪客只能讀取張貼的評論，並在支援時進行翻譯，但不得新增評論或標示其他人的評論。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [Comments Essentials](/help/communities/essentials-comments.md) 開發人員頁面。

有關張貼的評論的稽核，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

如需已發表評論的翻譯，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).
