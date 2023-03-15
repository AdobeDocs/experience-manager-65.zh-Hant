---
title: 使用注釋
seo-title: Using Comments
description: 「注釋」功能可讓登入的網站訪客分享其意見和知識
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 4%

---

# 使用注釋 {#using-comments}

## 簡介 {#introduction}

評論功能可讓登入的網站訪客（成員）分享其對網站內容的意見和知識。 此功能通常已存在於其他功能中，但可新增至任何網站。

文檔描述：

* 新增 `Comments` 到頁面。
* 的組態設定 `Comments` 元件。

>[!NOTE]
>
>不支援匿名發佈評論。 網站訪客必須註冊（成為會員）並登入以參與。

### 新增註解至頁面 {#adding-comments-to-a-page}

新增 `Comments` 在製作模式中，使用元件瀏覽器來尋找

* `Communities / Comments`

並將其拖曳至頁面上的位置，例如與功能相對的位置，供使用者註解，或只是拖曳至頁面底部。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的用戶端程式庫](/help/communities/essentials-comments.md#essentials-for-client-side) 包含在內，以下為方式 `Comments` 元件隨即出現。

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>只有一個 `Comments` 元件可能存在於頁面上。 請注意，幾個Communities功能已包括注釋，如部落格、日曆、論壇、QnA和評論。

### 配置注釋 {#configuring-comments}

選取已放置的 `Comments` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![配置表徵圖](assets/configure.png)

![注釋設定](assets/commentssettings.png)

#### 「注釋」頁簽 {#comments-tab}

在 **註解** 頁簽，指定訪客如何輸入留言。

* **允許回覆**

   如果選中，則允許成員答復現有評論。 已取消選取預設值。

* **每頁的評論數**

   限制每頁顯示的留言數和顯示的回覆數。 預設為10。

* **允許檔案上傳**

   如果勾選此選項，上傳檔案的選項會顯示文字輸入方塊。 已取消選取預設值。

* **最大檔案大小**

   僅在勾選「允許檔案上傳」時相關。 此值會限制上傳的檔案大小。 預設限制為10 MB。

* **訊息長度上限**

   可輸入文本框的字元數上限。 預設為4096個字元。

* **允許的檔案類型**

   僅在勾選「允許檔案上傳」時相關。 以逗號分隔的副檔名清單，並帶有&quot;dot&quot;分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **RTF 編輯器**

   如果選中，則輸入帶有標注的注釋。 已取消選取預設值。

* **允許投票**

   如果選中，則會顯示「上下投票」選項和文本輸入框。 已取消選取預設值。

* **允許關注**

   如果選中，則允許成員遵循注釋。 已取消選取預設值。

* **顯示徽章**

   如果選中，則允許顯示已獲得和已獲得徽章。 已取消選取預設值。

#### 使用者協調標籤 {#user-moderation-tab}

在 **使用者協調** 頁簽，指定如何管理已發佈的留言。 如需詳細資訊，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md).

* **事先審核**

   如果勾選此選項，留言必須先經過核准，才會顯示在發佈網站上。 已取消選取預設值。

* **刪除注釋**

   如果選中，則發佈評論的成員將能夠刪除評論。 已取消選取預設值。

* **拒絕評論**

   如果勾選此選項，允許協調者拒絕留言。 已取消選取預設值。

* **關閉/重新開啟注釋**

   如果勾選此選項，則允許協調者關閉和重新開啟留言。 已取消選取預設值。

* **標幟留言**

   如果選中，允許成員將注釋標籤為不適當。 已取消選取預設值。

* **標誌原因清單**

   如果選中，則允許成員從下拉清單中選擇其標籤注釋為不適當的原因。 已取消選取預設值。

* **自訂標幟原因**

   如果選中，則允許成員輸入自己的理由，以將評論標籤為不適當。 已取消選取預設值。

* **協調臨界值**

   輸入通知協調者前，成員必須標籤評論的次數。 預設為一次(1)。

* **標幟限制**

   輸入在從公共視圖中隱藏評論之前必須標籤該評論的次數。 此數字必須大於或等於 **協調臨界值**. 預設為5。

#### 排序設定標籤 {#sort-settings-tab}

在 **排序設定** 頁簽，指定在顯示張貼的留言時排序的方式。

* **排序欄位**

   下拉式清單以選取其中一個 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`，或 `Most Liked`.

* **排序順序**

   下拉式清單以選取其中一個 `Ascending` 或 `Descending`.

### 更改為自定義注釋類型 {#changing-to-a-custom-comment-type}

通過更改「注釋資源類型」，注釋系統不再使用預設值生成注釋實例，而是由開發人員自定義（擴展）的實例。

知道自訂資源類型後，請輸入 [設計模式](/help/sites-authoring/default-components-designmode.md) 並按兩下已放置 `Comments` 元件，以開啟含有額外索引標籤的對話方塊。

在 **資源類型** 頁簽中，指定新實例的自定義資源類型 `Comments or Voting` 元件：

![資源類型](assets/resource-type.png)

* **評論資源類型**

   導覽至延伸功能的resourceType `comment` /apps中的元件（單條注釋）。 例如, `/apps/social/commons/components/hbs/comments/comment`

   此資源可識別訪客發佈留言時所建立之UGC的resourceType。

* **投票資源類型**

   導覽至延伸功能的resourceType `voting` 元件。 例如, `/apps/social/components/hbs/voting`

   此資源可識別訪客張貼投票時所建立之UGC的資源類型。

* **注釋系統資源類型**

   導覽至延伸功能的resourceType `comments`/apps中的元件（注釋系統）。 除非頁面範本，否則保留空白 [動態包含](/help/communities/scf.md#add-or-include-a-communities-component) 基礎指令碼中的「註解系統」，而非以資源（註解節點）的形式新增至頁面。 閱讀 [{{include}} 協助者](/help/communities/handlebars-helpers.md#include).

### 網站訪客體驗 {#site-visitor-experience}

#### 協調者與管理員 {#moderators-and-administrators}

當登入的使用者擁有版主或管理員權限時，無論是誰編寫評論，他們都能執行元件組態所允許的協調工作。

#### 成員 {#members}

網站訪客登入時（視設定而定），可能會

* 張貼新留言
* 編輯自己的注釋
* 刪除自己的評論
* 標幟其他人的留言

#### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的留言、翻譯留言（如有支援），但不得新增留言，也不得標籤其他人的留言。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [注釋要點](/help/communities/essentials-comments.md) 頁面。

如需已張貼留言的協調，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md).

如需已張貼留言的翻譯，請參閱 [轉譯使用者產生的內容](/help/communities/translate-ugc.md).
