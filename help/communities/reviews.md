---
title: 使用審閱和審閱摘要（顯示）
seo-title: 使用審閱和審閱摘要（顯示）
description: 將「審核和審核摘要」元件添加到頁面
seo-description: 將「審核和審核摘要」元件添加到頁面
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 2%

---


# 使用審閱和審閱摘要（顯示）{#using-reviews-and-reviews-summary-display}

`Reviews`元件是[Comments](comments.md)和[Rating](rating.md)元件的組合，可供使用。

`Reviews Summary (Display)`元件提供`Reviews`元件的活動實例或關閉實例的摘要，以便顯示在站點的其他位置。

>[!NOTE]
>
>不支援匿名張貼審核。 網站訪客必須註冊（成為會員）並登入以參與。 已登入的訪客可隨時更新其審核。

## 將審核添加到頁面{#adding-a-review-to-a-page}

若要在作者模式下將`Reviews`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Reviews`並將它拖曳至頁面上，例如使用者可檢視的功能相對位置。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](reviews-basics.md#essentials-for-client-side)時，`Reviews`元件的顯示方式就是這樣。

![create-review](assets/create-review.png)

## 配置審核{#configuring-reviews}

選擇要訪問的已放置的`Reviews`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 允許的評分]**&#x200B;標籤下，指定要向成員顯示的評分的完整清單。 第一個評分應是整體／一般評分，因為它是提供`Review Summary (Display)`元件平均評分的評分。 預設設定中的後兩個分級應指定不同的標題，而非「Subrating 1」或「Subrating 2」。

![允許評分](assets/configure-review1.png)

* **[!UICONTROL 允許的評等]**

   成員可以選擇的評級清單。

   使用向上箭頭、向下箭頭和刪除按鈕來修改可見的選項。

   按一下「新增項目&#x200B;**[!UICONTROL 」以新增其他評等選擇。]**

在&#x200B;**[!UICONTROL 必要評級]**&#x200B;標籤下，從&#x200B;**[!UICONTROL 允許評級]**&#x200B;清單中重新輸入需要評級的項目。 如果項目僅在「允許的評分」標籤上指定，則成員提交時可能會保持未標籤狀態。

在網站上，必要的分級標有星號。 如果項目是必要項目，但未標籤，則會向成員顯示一條消息，並拒絕提交，直到所有必需的評級都標籤為止。

![必要評等](assets/configure-review2.png)

* **[!UICONTROL 必要評等]**

   允許的評等子集，指出需要哪些評等。

   使用向上箭頭、向下箭頭和刪除按鈕來修改可見的選項。

   按一下&#x200B;**[!UICONTROL 添加項目]**&#x200B;以添加另一個響應選項。

>[!NOTE]
>
>如果在&#x200B;**[!UICONTROL 必要評分]**&#x200B;標籤上輸入項目，但未在&#x200B;**[!UICONTROL 允許評分]**&#x200B;標籤上指定，則該項目不會包含在要評分的項目中。

在&#x200B;**[!UICONTROL Reviews]**&#x200B;標籤下，指定如何處理審核。

![評論](assets/configure-review3.png)

* **[!UICONTROL 允許回覆]**

   如果勾選，則允許回覆審核。 預設為未勾選。

* **[!UICONTROL 已關閉]**

   如果勾選，則新審核和回覆將關閉審核。 預設為未勾選。

* **[!UICONTROL 允許檔案上傳]**

   如果勾選，允許上傳檔案附件以供審核。 預設為未勾選。

* **最大檔案大小**

   僅當選中「允許檔案上載」**[!UICONTROL 時相關。]**&#x200B;此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為10 MB。

* **[!UICONTROL 訊息長度上限]**

   文字方塊中可輸入的字元數上限。 預設為4096個字元。

* **[!UICONTROL 允許的檔案類型]**

   僅當選中「允許檔案上載」**[!UICONTROL 時相關。]**&#x200B;以逗號分隔的副檔名清單，並以&quot;dot&quot;分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **[!UICONTROL RTF 編輯器]**

   如果勾選，則可輸入貼文並加上標籤。 預設為未勾選。

* **[!UICONTROL 允許投票]**

   如果勾選，請加入主題的「投票」功能。 預設為未勾選。

在&#x200B;**[!UICONTROL 使用者協調]**&#x200B;標籤下，指定如何管理張貼的審核。 如需詳細資訊，請參閱[協調使用者產生的內容](moderate-ugc.md)。

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 事先審核]**

   如果勾選，審核必須先經過核准，才會顯示在發佈網站上。 預設為未勾選。

* **[!UICONTROL 刪除評論]**

   如果勾選，則張貼審核的成員可以刪除它。 預設為未勾選。

* **[!UICONTROL 拒絕審核]**

   如果勾選，允許協調者拒絕審核。 預設為未勾選。

* **[!UICONTROL 關閉／重新開啟審核]**

   如果勾選，允許協調者關閉並重新開啟審核。 預設為未勾選。

* **[!UICONTROL 標籤審核]**

   如果勾選，允許成員將審核標籤為不適當。 預設為未勾選。

* **[!UICONTROL 標籤原因清單]**

   如果勾選，允許成員從下拉式清單中選擇將審核標籤為不適當的理由。 預設為未勾選。

* **[!UICONTROL 自訂標幟原因]**

   如果勾選，允許成員輸入自己將審核標籤為不適當的原因。 預設為未勾選。

* **[!UICONTROL 協調臨界值]**

   輸入成員在通知協調者之前必須標籤審核的次數。 預設值為一次(1)。

* **[!UICONTROL 標幟限制]**

   輸入在公開檢視中隱藏審核前必須標幟的次數。 此數字必須大於或等於&#x200B;**[!UICONTROL 協調臨界值]**。 預設值為5。

### 將審核摘要（顯示）添加到頁面{#adding-a-review-summary-display-to-a-page}

若要在作者模式下將`Reviews Summary (Display)`元件新增至頁面，請找出該元件

* `Communities / Reviews Summary (Display)`

並將其拖曳至要顯示活動或已關閉審核摘要的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[所需的客戶端庫](reviews-basics.md#essentials-for-client-side)時，`Reviews Summary (Display)`元件將如此顯示。

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>「平均值」會反映摘要審閱「允許評分」標籤上所列第一個項目的投票數。

### 設定審核摘要（顯示）{#configuring-reviews-summary-display}

選擇要訪問的已放置的`Reviews Summary (Display)`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL Review Summary]**&#x200B;頁籤下

![review-summary](assets/configure-review6.png)

* `Review Path`

   輸入或瀏覽至`reviews`元件的置入例項以進行總結，例如，如果新增至[Geometrixx Engage網站的「網頁」，則路徑應為：](getting-started.md)

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果勾選，請加入橫條圖的顯示，指出要匯總的審核中每個星號分數的多少。 預設為未勾選。

### 變更為自訂審核類型{#changing-to-a-custom-review-type}

Reviews元件使用注釋系統。

變更「註解資源類型」後，註解系統將不再使用預設值產生註解的例項，而是開發人員自訂（擴充）的例項。

在確定自定義資源類型後，輸入[設計模式](../../help/sites-authoring/default-components-designmode.md)並按兩下已放置的`Comments`元件以開啟帶有附加頁籤的對話框。

在&#x200B;**[!UICONTROL 資源類型]**&#x200B;頁籤下，為`Comments or Voting`元件的新實例指定自定義resourceType:

![留言投票](assets/configure-review7.png)

* **[!UICONTROL 評論資源類型]**

   導覽至/apps中延伸`comment`元件的resourceType（單一註解）。 例如，`/apps/social/commons/components/hbs/comments/comment`。

   此資源將識別訪客張貼留言時所建立之UGC的resourceType。

* **[!UICONTROL 投票資源類型]**

   導覽至/apps中延伸`voting`元件的resourceType。 例如，`/apps/social/components/hbs/voting`。

   此資源將識別訪客張貼投票時所建立之UGC的資源類型。

* **[!UICONTROL 注釋系統資源類型]**

   導覽至/apps中延伸`comments`元件（注釋系統）的resourceType。 保留空白，除非頁面範本[動態地在基礎指令碼中包含](scf.md#add-or-include-a-communities-component)注釋系統，而不是以資源（注釋節點）的形式新增至頁面。 閱讀[{{include}} helper](handlebars-helpers.md#include)，瞭解更多資訊。

## 網站訪客體驗{#site-visitor-experience}

### 協調者和管理員{#moderators-and-administrators}

當登入的使用者具有協調者或管理員權限時，他們可以執行元件設定所允許的協調工作，不論是誰撰寫審核。

### 成員 {#members}

網站訪客登入時（視設定而定），可能會：

* 張貼新審核
* 編輯其自己的審核
* 刪除其自己的審核
* 標籤其他人的審閱注釋

每個成員僅允許一個分級。 會員可隨時變更其評級。

### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的審核、翻譯（如果支援），但不得新增評分或審核，也不得標籤其他人的審核意見。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[ Review Essentials](reviews-basics.md)頁面。

如需已張貼留言的協調，請參閱[協調使用者產生的內容](moderate-ugc.md)。

有關已張貼留言的轉譯，請參閱[轉譯使用者產生的內容](translate-ugc.md)。
