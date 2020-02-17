---
title: 論壇功能
seo-title: 論壇功能
description: 如何新增和設定論壇功能
seo-description: 如何新增和設定論壇功能
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 論壇功能{#forum-feature}

## 簡介 {#introduction}

論壇功能提供發佈環境中登入網站訪客（社群成員）的區域，讓您：

* 建立新主題
* 檢視和回覆主題
* 關注主題
* 搜尋論壇
* 協助協調論壇內容
* 將論壇主題從一頁移至另一頁

本節說明

* 新增論壇功能至AEM網站
* 元件的配置設 `Forum`置

### 新增論壇至頁面 {#adding-a-forum-to-a-page}

若要在作 `Forum` 者模式中將元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Forum`

並將它拖曳至論壇應出現的頁面上。

如需必要資訊，請造 [訪Communities Components Basics](/help/communities/basics.md)。

當包含 [所需的用戶端程式庫](/help/communities/essentials-forum.md#essentials-for-client-side) ，元件的顯示 `Forum`方式如下：

![chlimage_1-104](assets/chlimage_1-104.png)

### 設定論壇 {#configuring-a-forum}

選擇要訪問 `Forum` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-105](assets/chlimage_1-105.png) ![forum-config](assets/forum-config.png)

#### 「設定」頁籤 {#settings-tab}

在「**設定**」標籤下，指定主題和回覆的設定：

* **允許附件縮圖**如果勾選，則會建立附加影像的縮圖。
* **附加縮圖大小**&#x200B;附加縮圖影像的最大大小（以像素為單位）。 預設值為800 x 800。

* **縮圖的最小影像大小**
* **最大縮圖大**&#x200B;小內嵌影像縮圖影像的最大大小（以像素為單位）。 預設值為800 x 800。

* **每頁主題**定義每頁顯示的主題／貼文數。 預設值為10。
* **已協調**：如果勾選，則必須先核准張貼主題和留言，才會顯示在發佈網站上。 預設為未勾選。

* **關閉**&#x200B;如果勾選此選項，論壇將關閉新主題和注釋。 預設為未勾選。

* **富格文本編輯**&#x200B;器如果選中，則可以使用標注輸入主題和注釋。 預設為未勾選。

* **允許標籤**：如果勾選，允許成員將標籤標籤新增至其貼文(請參 **閱標籤欄位** 標籤)。 預設為未勾選。

* **允許檔案上載**&#x200B;如果選中此選項，則允許將檔案附件添加到主題或注釋中。 預設為未勾選。

* **允許下**&#x200B;列：如果勾選，請加入論壇貼文的下列功能，讓成員 [收到](/help/communities/notifications.md) 新貼文的通知。 預設為未勾選。

* **允許釘選**&#x200B;如果勾選，論壇主題可能會釘選至主題清單的頂端。 預設為未勾選。

* **如果勾選**「允許特色內容」，即可將構想識別為 [特色內容](/help/communities/featured.md)。 預設為未勾選。

* **允許電子郵件**&#x200B;訂閱如果勾選，允許會員透過電子郵件（訂閱）收到新[貼文](/help/communities/subscriptions.md)。 需要 `Allow Following` 檢查並設定電 [子郵件](/help/communities/email.md)。 預設為未勾選。

* **最大檔案大小**&#x200B;僅在勾選時 `Allow File Uploads` 相關。 此欄位將限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600(10 Mb)。

* **允許的檔案類型**&#x200B;僅在選中時 `Allow File Uploads` 相關。 以逗號分隔的副檔名清單，並以&quot;dot&quot;分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定任何檔案類型，則不允許上傳未指定的檔案類型。 未指定預設值，因此允許** **所有檔案類型。

* **僅當勾選「允許上傳檔案**」時，附加影像檔案大小的上限才相關。 上傳的影像檔案的位元組數上限。 預設值為2097152****(2 Mb)。

* **允許線程化回**&#x200B;覆如果勾選，則允許回覆張貼至主題的留言。 預設為未勾選。

* **允許投票**&#x200B;如果選中，請將「投票」功能與主題一起包含。 預設為未勾選。

* **允許用戶刪除注釋和主題**&#x200B;如果選中，允許成員刪除他們發佈的注釋和主題。 預設為未勾選。

* **顯示Breadcrumbs**&#x200B;如果勾選，則顯示主題頁面上的導覽Breadcrumbs。 已勾選預設值。

* **顯示標章**&#x200B;如果勾選，請使用成員的 [部落格項目](/help/communities/implementing-scoring.md) ，顯示已獲得和已指派的標章。 預設為未勾選。

* **允許特權成**&#x200B;員如果選中此選項，則僅允許特權成員建立內容。

* **允許的特權成員**添加允許建立內容的特權成員。
* **在作者編輯模式中封鎖使用者產生的內容**&#x200B;如果啟用，在作者模式中編輯時會封鎖使用者產生的內容。

* **啟用提及** If enabled, allows registered community users to identify other registered members(using first name, last name, user name), and tag them usen @user-name syntax. 標籤使用者會收到有關其提及次數的通知。

* **最大提及**&#x200B;次數限制貼文中允許的提及次數上限。 預設值為10。

* **UI提及模式**：在貼文中指定已註冊使用者的標籤（@提及）的已授權模式字串。 例如 `~{{familyName}}{{givenName}}`。

>[!NOTE]
>
>可能需要同時檢查和 `AllowThreaded Replies` 啟 `Allow users to Delete Comments and Topics` 用對主題的注釋。

#### 使用者協調標籤 {#user-moderation-tab}

在「**使用者協調**」標籤下，指定如何管理已張貼的主題和回覆（使用者產生的內容）。 如需詳細資訊，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md)。

* **拒絕貼文**&#x200B;如果勾選，可信任的會員協調者將可拒絕貼文，並防止貼文出現在公開論壇。 預設為未勾選。

* **關閉／重新開啟主**&#x200B;題如果勾選，受信任的成員協調者可以關閉主題以進一步編輯和留言，也可以重新開啟主題。 預設為未勾選。

* **移動主題**&#x200B;如果勾選，則允許發佈端協調者移動主題。 已勾選預設值。

* **標幟貼文**&#x200B;如果勾選，允許成員將其他主題或留言標幟為不適當。 預設為未勾選。

* **標幟原因清**&#x200B;單如果勾選，允許成員從下拉式清單中選擇其標籤主題或留言的不適當原因。 預設為未勾選。

* **自訂標幟原**&#x200B;因如果勾選，允許成員輸入自己將主題或留言標籤為不適當的原因。 預設為未勾選。

* **協調臨**&#x200B;界值輸入在通知協調者之前，成員必須標籤主題或留言的次數。 預設值為1（一次）。

* **標籤限**&#x200B;制輸入主題或留言在公開檢視中隱藏之前必須標籤的次數。 如果設為-1，則標籤的主題或留言永遠不會隱藏在公開檢視中。 否則，此數字必須大於或等於「協調臨界值」。 預設值為5。

#### 「標籤」欄位頁籤 {#tag-field-tab}

在「標 **記」欄位** (Tag field)標籤下，可套用的標籤（如果允許）會根據選擇的名稱空間加以限制。

* **允許的名**&#x200B;稱空間相 `Allow Tagging` 關（如果已勾選「**設定**」標籤）。 可套用的標籤僅限於已勾選之命名空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設命名空間）和「包含所有標籤」。 預設值未勾選，表示允許所有命名空間。

* **建議限**&#x200B;制輸入要作為建議顯示給發佈到論壇的成員的標籤數。 預設值為**-**1（無限制）。

#### 翻譯標籤 {#translation-tab}

在**翻譯**頁籤下，如果為社區站點啟用翻譯，則可以設定翻譯來翻譯整個主題或選定的帖子。

* **Translate All**（全部翻譯）如果選中，論壇線程將翻譯為用戶首選的語言。 預設為未勾選。

#### 「排序設定」頁籤 {#sort-settings-tab}

在「**排序設定**」標籤下，指定張貼的留言在顯示時的排序方式。

* **排序依據**&#x200B;檢查所有允許的排序選擇： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`。 預設為 `Newest, Oldest, Last Updated`。

* **設定為「預設**」(Default)下拉式選項，以選擇一個選定的排序選項作為預設選項顯示。 預設為 `Newest`。

* **選取「Analytics排序下拉式**&#x200B;的時間選項」以選取其中一 `All, Last 24 Hours, Last 7 Days, Last 30 Days`個。 預設為 `All`。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員適用的論壇](/help/communities/essentials-forum.md) Essentials頁面。

如需協調已張貼主題和留言的資訊，請參 [閱協調使用者產生的內容](/help/communities/moderate-ugc.md)。

如需標籤已張貼的主題和留言，請參 [閱標籤使用者產生的內容](/help/communities/tag-ugc.md)。

如需已張貼主題和留言的轉譯，請參閱轉 [譯使用者產生的內容](/help/communities/translate-ugc.md)。
