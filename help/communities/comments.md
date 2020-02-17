---
title: 使用注釋
seo-title: 使用注釋
description: 「注釋」功能可讓登入網站的訪客分享其意見和知識
seo-description: 「注釋」功能可讓登入網站的訪客分享其意見和知識
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 使用注釋{#using-comments}

## 簡介 {#introduction}

註解功能可讓登入網站的訪客（會員）分享其對網站內容的意見和知識。 此功能通常已存在於其他功能中，但可以新增至任何網站。

本檔案說明：

* 新增 `Comments`至頁面。
* 元件的配置 `Comments`設定。

>[!NOTE]
>
>不支援匿名張貼留言。 網站訪客必須註冊（成為會員）並登入以參與。

### 新增注釋至頁面 {#adding-comments-to-a-page}

若要在作 `Comments`者模式下將元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Comments`

並將它拖曳至頁面上，例如與功能相關的位置，讓使用者在頁面上加上註解，或僅在頁面底部。

如需必要資訊，請造 [訪Communities Components Basics](/help/communities/basics.md)。

當包含 [所需的用戶端程式庫](/help/communities/essentials-comments.md#essentials-for-client-side) ，元件就會以此 `Comments`顯示。

![chlimage_1-143](assets/chlimage_1-143.png)

>[!NOTE]
>
>頁面上 `Comments`只能存在一個元件。 請注意，數個社群功能已包含注釋，例如部落格、行事歷、論壇、QnA和評論。

### 設定注釋 {#configuring-comments}

選擇要訪問 `Comments` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![配置表徵圖](assets/configure.png)![注釋設定](assets/commentssettings.png)

#### 「注釋」頁籤 {#comments-tab}

在「注 **釋** 」標籤下，指定訪客如何輸入注釋。

* **允許回覆**

   如果選中，允許成員回覆現有注釋。 已取消選取預設值。

* **每頁的評論數**

   限制每頁顯示的留言數和顯示的回覆數。 預設值為10。

* **允許檔案上傳**

   如果勾選，則會顯示文字輸入方塊的上傳檔案選項。 已取消選取預設值。

* **最大檔案大小**

   僅在勾選「允許檔案上傳」時相關。 此值會限制上傳的檔案大小。 預設限制為10 MB。

* **訊息長度上限**

   文字方塊中可輸入的字元數上限。 預設為4096個字元。

* **允許的檔案類型**

   僅在勾選「允許檔案上傳」時相關。 以逗號分隔的副檔名清單，並加上&quot;dot&quot;分隔符號。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許** **所有檔案類型。

* **RTF 編輯器**

   如果選中，則輸入注釋並標注。 已取消選取預設值。

* **允許投票**

   如果勾選，則會顯示「上投」或「下投」選項，並顯示文字輸入方塊。 已取消選取預設值。

* **允許關注**

   如果勾選此選項，允許成員遵循注釋。 已取消選取預設值。

* **顯示徽章**

   如果勾選，則允許顯示獎勵和獎勵的徽章。 已取消選取預設值。

#### 使用者協調標籤 {#user-moderation-tab}

在「**使用者協調**」標籤下，指定張貼的留言的管理方式。 如需詳細資訊，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md)。

* **預先協調**：如果勾選，留言必須先經過核准，才能顯示在發佈網站上。 已取消選取預設值。

* **刪除注釋**

   如果勾選，則張貼評論的成員可以刪除評論。 已取消選取預設值。

* **拒絕注釋**

   如果勾選，允許協調者拒絕注釋。 已取消選取預設值。

* **關閉／重新開啟注釋**

   如果勾選，允許協調者關閉並重新開啟注釋。 已取消選取預設值。

* **標籤注釋**

   如果勾選，允許成員將注釋標籤為不適當。 已取消選取預設值。

* **標籤原因清單**

   如果勾選，允許成員從下拉式清單中選擇其標籤註解為不適當的理由。 已取消選取預設值。

* **自訂標幟原因**

   如果勾選，允許成員輸入自己將注釋標籤為不適當的原因。 已取消選取預設值。

* **協調臨界值**

   輸入成員在通知協調者之前必須標籤留言的次數。 預設值為一次(1)。

* **標幟限制**

   輸入留言在公開檢視中隱藏前必須標籤的次數。 此數字必須大於或等於「協調臨界 **值」**。 預設值為5。

#### 「排序設定」頁籤 {#sort-settings-tab}

在「**排序設定**」標籤下，指定張貼的留言在顯示時的排序方式。

* **排序欄位**

   下拉以選取其中一個 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`或 `Most Liked`。

* **排序順序**

   下拉式選取其中一個 `Ascending` 或 `Descending`。

### 變更為自訂註解類型 {#changing-to-a-custom-comment-type}

變更「註解資源類型」後，註解系統不會再使用預設值產生註解的例項，而是由開發人員自訂（擴充）的例項。

在已知自訂資源類型後，進入 [Design Mode](/help/sites-authoring/default-components-designmode.md) ，然後按兩下置入的元 `Comments` 件，以開啟具有額外標籤的對話方塊。

在「**資源類型**」頁籤下，為元件的新實例指定自定義資源 `Comments or Voting`類型：

![chlimage_1-144](assets/chlimage_1-144.png)

* **評論資源類型**

   導覽至/apps中延伸元件( `comment`單一註解)的resourceType。 例如， `/apps/social/commons/components/hbs/comments/comment`

   此資源可識別訪客張貼留言時所建立之UGC的resourceType。

* **投票資源類型**

   導覽至/apps中延伸元件 `voting`的resourceType。 例如， `/apps/social/components/hbs/voting`

   此資源可識別訪客張貼投票時所建立之UGC的資源類型。

* **注釋系統資源類型**

   導覽至/apps中延伸元件( `comments`注釋系統)的resourceType。 保留空白，除非頁面范 [本在基礎指令碼中動態包含](/help/communities/scf.md#add-or-include-a-communities-component) 「注釋系統」，而不是以資源（注釋節點）的形式新增至頁面。 閱讀有關 [{{include}}協助工具的更多資訊](/help/communities/handlebars-helpers.md#include)。

### 網站訪客體驗 {#site-visitor-experience}

#### 協調者與管理員 {#moderators-and-administrators}

當登入的使用者具有協調者或管理員權限時，他們可以執行元件設定所允許的協調工作，不論是誰撰寫了註解。

#### 成員 {#members}

當網站訪客登入時（視設定而定），他們可能會

* 張貼新留言
* 編輯自己的注釋
* 刪除自己的注釋
* 標幟其他人的意見

#### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的留言、翻譯留言（如果受支援），但不得新增留言或標籤其他人的留言。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的「注釋](/help/communities/essentials-comments.md) 」頁面。

如需已張貼留言的協調，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md)。

如需已張貼意見的轉譯，請參閱轉 [譯使用者產生的內容](/help/communities/translate-ugc.md)。
