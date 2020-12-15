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
source-git-commit: 871c42ee000eb250c1c6159d9a0c752e8ed4d7b8
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 8%

---


# 論壇功能{#forum-feature}

## 簡介 {#introduction}

論壇功能為登入網站訪客（社群成員）在發佈環境中提供一個區域，供您：

* 建立新主題
* 檢視並回覆主題
* 關注主題
* 搜尋論壇
* 協助協調論壇內容
* 將論壇主題從一個頁面移至另一個頁面

本檔案章節說明：

* 新增論壇功能至AEM網站。
* `Forum`元件的配置設定。

### 將論壇添加到頁面{#adding-a-forum-to-a-page}

若要在作者模式下將`Forum`元件新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Forum`

並將它拖曳至論壇應出現的頁面上。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

當包含[必要的用戶端程式庫](/help/communities/essentials-forum.md#essentials-for-client-side)時，`Forum`元件的顯示方式如下：

![論壇——元件](assets/forum-component.png)

### 配置論壇{#configuring-a-forum}

選擇要訪問的已放置的`Forum`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

![論壇——組態](assets/forum-config.png)

#### 「設定」頁籤{#settings-tab}

在&#x200B;**Settings**&#x200B;標籤下，指定主題和回覆的設定：

* **允許附件縮圖**

   如果勾選，則會建立附加影像的縮圖。

* **附加縮圖最大尺寸**

   附件縮圖影像的最大大小（以像素為單位）。 預設值為800 x 800。

* **縮圖的最小影像大小**
* **最大縮圖尺寸**

   內嵌影像的縮圖影像大小上限（以像素為單位）。 預設值為800 x 800。

* **每頁主題**

   定義每個頁面顯示的主題/帖子數。預設為 10。

* **已審核**

   如果勾選，則必須先核准張貼主題和留言，才會顯示在發佈網站上。 預設為未勾選。

* **已關閉**

   如果勾選，論壇將不會顯示新主題和評論。 預設為未勾選。

* **RTF 編輯器**

   如果選中，則主題和注釋可以與標注一起輸入。 預設為未勾選。

* **允許標記**

   如果勾選，允許成員將標籤標籤新增至其貼文（請參閱&#x200B;**標籤欄位**&#x200B;標籤）。 預設為未勾選。

* **允許檔案上傳**

   如果選中，則允許將檔案附件添加到主題或注釋中。 預設為未勾選。

* **允許關注**

   如果勾選，請為論壇貼文加入下列功能，讓成員能夠收到新貼文的[通知。 ](/help/communities/notifications.md)預設為未勾選。

* **允許釘選**

   如果選中，論壇主題可能會釘選到主題清單的頂部。 預設為未勾選。

* **允許主要內容**

   如果勾選，該構想可識別為[特色內容](/help/communities/featured.md)。 預設為未勾選。

* **允許電子郵件訂閱**

   如果勾選，允許會員透過電子郵件收到新貼文的通知([subscription](/help/communities/subscriptions.md))。 需要檢查`Allow Following`並配置[電子郵件](/help/communities/email.md)。 預設為未勾選。

* **最大檔案大小**

   僅當選中`Allow File Uploads`時相關。 此欄位將限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600(10 Mb)。

* **允許的檔案類型**

   僅當選中`Allow File Uploads`時相關。 以逗號分隔的副檔名清單，並以&quot;dot&quot;分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定任何檔案類型，則不允許上傳未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **最大附加影像檔案大**
小只有在勾選「允許檔案上傳」時，才相關。上傳的影像檔案的位元組數上限。 預設值為2097152(2 Mb)。

* **允許執行緒式回覆**

   如果勾選，則允許回覆張貼至主題的留言。 預設為未勾選。

* **允許投票**

   如果勾選，請將「投票」功能加入主題。 預設為未勾選。

* **允許使用者刪除評論和主題**

   如果勾選，允許成員刪除其張貼的留言和主題。 預設為未勾選。

* **顯示階層連結**

   如果勾選，則在主題頁面上顯示導覽導覽路徑標示。 已勾選預設值。

* **顯示徽章**

   如果勾選，則顯示已獲得且已指派[badges](/help/communities/implementing-scoring.md)及成員的部落格項目。 預設為未勾選。

* **允許有特殊權限的成員**

   如果勾選，則僅允許特權成員建立內容。

* **允許擁有特殊權限的成員**

   添加允許建立內容的特權成員。

* **封鎖使用者在作者編輯模式中產生的內容**

   啟用後，在「作者模式」中編輯時，會封鎖使用者產生的內容。

* **啟用提及功能**

   如果啟用，則允許註冊的社區用戶標識其他已註冊成員（使用名、姓、用戶名），並使用通用的@user-name語法標籤這些成員。 標籤使用者會收到有關其提及次數的通知。

* **最大提及數**

   限制貼文中允許的提及次數上限。 預設值為10。

* **UI 提及模式**

   將已授權的模式字串指定為貼文中已註冊使用者的標籤（@提及）。 例如`~{{familyName}}{{givenName}}`。

>[!NOTE]
>
>可能需要同時檢查`AllowThreaded Replies`和`Allow users to Delete Comments and Topics`以啟用對主題的注釋。

#### 使用者協調標籤{#user-moderation-tab}

在&#x200B;**使用者協調**&#x200B;標籤下，指定如何管理已張貼的主題和回覆（使用者產生的內容）。 如需詳細資訊，請參閱[協調使用者產生的內容](/help/communities/moderate-ugc.md)。

* **拒絕貼文**

   如果勾選，則可讓受信任的會員協調者拒絕貼文，並防止貼文出現在公開論壇。 預設為未勾選。

* **關閉／重新開啟主題**

   如果勾選，受信任的成員協調者可以關閉主題以進一步編輯和留言，也可以重新開啟主題。 預設為未勾選。

* **移動主題**

   如果勾選，允許發佈端協調者移動主題。 已勾選預設值。

* **標籤貼文**

   如果勾選，允許成員將其他主題或注釋標籤為不適當。 預設為未勾選。

* **標籤原因清單**

   如果勾選，允許成員從下拉式清單中選擇其標籤主題或留言的不適當原因。 預設為未勾選。

* **自訂標幟原因**

   如果勾選，允許成員輸入自己將主題或留言標籤為不適當的原因。 預設為未勾選。

* **協調臨界值**

   輸入成員在通知協調者之前必須標籤主題或留言的次數。 預設值為1（一次）。

* **標幟限制**

   輸入主題或留言在公開檢視中隱藏前必須加以標幟的次數。 如果設為-1，則標籤的主題或留言絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於「協調臨界值」。 預設值為5。

#### 標籤欄位標籤{#tag-field-tab}

在&#x200B;**Tag欄位**&#x200B;頁籤下，如果允許在&#x200B;**Settings**&#x200B;頁籤下應用的標籤會根據選擇的名稱空間進行限制。

* **允許的命名空間**

   如果在&#x200B;**Settings**&#x200B;標籤下勾選`Allow Tagging`，則相關。 可套用的標籤僅限於已勾選之命名空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設命名空間）和「包含所有標籤」。 預設值未勾選，表示允許所有命名空間。

* **建議限制**

   輸入要作為建議顯示給發佈到論壇的成員的標籤數。 預設值為**-**1（無限制）。

#### 翻譯頁籤{#translation-tab}

在&#x200B;**Translation**&#x200B;標籤下，如果為社區站點啟用了翻譯，則可以設定翻譯來翻譯整個主題或選定的帖子。

* **全部轉換**

   如果勾選此選項，論壇線程將轉換為用戶首選的語言。 預設為未勾選。

#### 排序設定頁籤{#sort-settings-tab}

在&#x200B;**排序設定**&#x200B;標籤下，指定顯示張貼留言的排序方式。

* **排序方式**

   檢查所有允許的排序選擇：`Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`。 預設值為`Newest, Oldest, Last Updated`。

* **設為預設值**

   下拉式清單以選取其中一個核取的排序選項，以顯示為預設值。 預設值為`Newest`。

* **選取 Analytics 排序的時間選項**

   下拉式選擇下列選項之一：`All, Last 24 Hours, Last 7 Days, Last 30 Days`。

   預設值為`All`。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[Forum Essentials](/help/communities/essentials-forum.md)頁面。

如需協調已張貼主題和留言的資訊，請參閱[協調使用者產生的內容](/help/communities/moderate-ugc.md)。

如需標籤已張貼的主題和留言，請參閱[標籤使用者產生的內容](/help/communities/tag-ugc.md)。

如需已張貼主題和留言的轉譯，請參閱[轉譯使用者產生的內容](/help/communities/translate-ugc.md)。
