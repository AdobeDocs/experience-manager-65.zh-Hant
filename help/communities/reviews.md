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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用審閱和審閱摘要（顯示） {#using-reviews-and-reviews-summary-display}

元 `Reviews`件是可供使用的 [ 和 `Comments`](comments.md) 元件 [`Rating`](rating.md) 的組合。

元 `Reviews Summary (Display)` 件提供元件的作用中或關閉例項的摘要，以 `Reviews` 便顯示在網站的其他位置。

>[!NOTE]
>
>不支援匿名張貼審核。 網站訪客必須註冊（成為會員）並登入以參與。 已登入的訪客可隨時更新其審核。

## 新增審核至頁面 {#adding-a-review-to-a-page}

若要在作 `Reviews``Communities / Reviews` 者模式下將元件新增至頁面，請使用元件瀏覽器來尋找並拖曳元件至頁面上的位置，例如與功能相關的位置，供使用者檢視。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](reviews-basics.md#essentials-for-client-side) ，元件的顯示 `Reviews`方式就是這樣。

![chlimage_1-340](assets/chlimage_1-340.png)

## 設定審核 {#configuring-reviews}

選擇要訪問 `Reviews` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-341](assets/chlimage_1-341.png)

在「允 **[!UICONTROL 許的評分]** 」標籤下，指定要顯示給成員的評分完整清單。 第一個評分應是整體／一般評分，因為它是提供元件平均評分的評 `Review Summary (Display)` 分。 預設設定中的後兩個分級應指定不同的標題，而非「Subrating 1」或「Subrating 2」。

![chlimage_1-342](assets/chlimage_1-342.png)

* **[!UICONTROL 允許的評等]**

   成員可以選擇的評級清單。

   使用向上箭頭、向下箭頭和刪除按鈕來修改可見的選項。

   按一 **[!UICONTROL 下「新增項目]** 」以新增其他評等選擇。

在「必 **[!UICONTROL 要評分]** 」標籤下，從「允許評分」清單中重新輸入 **** 必須評分的項目。 如果項目僅在「允許的評分」標籤上指定，則成員提交時可能會保持未標籤狀態。

在網站上，必要的分級標有星號。 如果項目是必要項目，但未標籤，則會向成員顯示一條消息，並拒絕提交，直到所有必需的評級都標籤為止。

![chlimage_1-343](assets/chlimage_1-343.png)

* **[!UICONTROL 必要評等]**

   允許的評等子集，指出需要哪些評等。

   使用向上箭頭、向下箭頭和刪除按鈕來修改可見的選項。

   按一 **[!UICONTROL 下「新增項目]** 」以新增其他回應選擇。

>[!NOTE]
>
>如果項目是在「必要 **[!UICONTROL 評分]****** 」標籤上輸入，但未在「允許的評分」標籤上指定，則它不會包含在要評分的項目中。

在「審 **[!UICONTROL 核]** 」標籤下，指定如何處理審核。

![chlimage_1-344](assets/chlimage_1-344.png)

* **[!UICONTROL 允許回覆]**&#x200B;如果勾選，則允許回覆至審核。 預設為未勾選。

* **[!UICONTROL 已關閉]**&#x200B;如果勾選，則新審核和回覆將關閉審核。 預設為未勾選。

* **[!UICONTROL 允許上傳檔案]**&#x200B;如果勾選此選項，則允許上傳檔案附件以供審核。 預設為未勾選。

* **最大檔案大小&#x200B;**僅在勾選「允**[!UICONTROL 許檔案上傳&#x200B;]**」時相關。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為10 MB。

* **[!UICONTROL 最大消息長]**&#x200B;度可輸入到文本框中的最大字元數。 預設為4096個字元。

* **[!UICONTROL 僅在勾選「允]**&#x200B;許檔案上傳 **[!UICONTROL 」時，允許的檔案類型]** 「相關」。 以逗號分隔的副檔名清單，並以&quot;dot&quot;分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **[!UICONTROL Rich Text Editor]**&#x200B;如果勾選，則可輸入含有標籤的貼文。 預設為未勾選。

* **[!UICONTROL 允許投票]**&#x200B;如果選中，則包含主題的「投票」功能。 預設為未勾選。

在「使用 **[!UICONTROL 者協調]** 」標籤下，指定如何管理已張貼的審核。 如需詳細資訊，請參閱 [協調使用者產生的內容](moderate-ugc.md)。

![chlimage_1-345](assets/chlimage_1-345.png)

* **[!UICONTROL 預先協調]**：如果勾選，審核必須先經過核准，才會顯示在發佈網站上。 預設為未勾選。

* **[!UICONTROL 刪除審]**&#x200B;核如果選中，則發佈審核的成員將能夠刪除它。 預設為未勾選。

* **[!UICONTROL 拒絕審核]**&#x200B;如果勾選，則允許協調者拒絕審核。 預設為未勾選。

* **[!UICONTROL 關閉／重新開啟審核]**&#x200B;如果勾選，則允許協調者關閉並重新開啟審核。 預設為未勾選。

* **[!UICONTROL 標幟審核]**&#x200B;如果勾選，允許成員將審核標籤為不適當。 預設為未勾選。

* **[!UICONTROL 標幟原因清]**&#x200B;單如果勾選，允許成員從下拉式清單中選擇將審核標籤為不適當的原因。 預設為未勾選。

* **[!UICONTROL 自訂標幟原]**&#x200B;因如果勾選，允許成員輸入自己將審核標籤為不適當的原因。 預設為未勾選。

* **[!UICONTROL 協調臨]**&#x200B;界值輸入成員在通知協調者之前必須標籤審核的次數。 預設值為一次(1)。

* **[!UICONTROL 標籤限]**&#x200B;制輸入審核在隱藏於公開檢視之前必須標籤的次數。 此數字必須大於或等於「協調臨界 **[!UICONTROL 值」]**。 預設值為5。

### 將審核摘要（顯示）添加到頁面 {#adding-a-review-summary-display-to-a-page}

若要在作 `Reviews Summary (Display)` 者模式下將元件新增至頁面，請找出元件

* `Communities / Reviews Summary (Display)`

並將其拖曳至要顯示活動或已關閉審核摘要的頁面上。

如需必要資訊，請造 [訪Communities Components Basics](basics.md)。

當包含 [所需的用戶端程式庫](reviews-basics.md#essentials-for-client-side) ，元件的顯示 `Reviews Summary (Display)`方式就是這樣。

![chlimage_1-346](assets/chlimage_1-346.png)

>[!NOTE]
>
>「平均值」會反映摘要審閱「允許評分」標籤上所列第一個項目的投票數。

### 設定審核摘要（顯示） {#configuring-reviews-summary-display}

選擇要訪問 `Reviews Summary (Display)` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-347](assets/chlimage_1-347.png)

在「查看摘 **[!UICONTROL 要」頁籤下]**

![chlimage_1-348](assets/chlimage_1-348.png)

* `Review Path`

   輸入或瀏覽至元件的置入 `reviews`例項以進行摘要，例如，如果新增至 [Geometrixx Engage網站的網頁，路徑會是](getting-started.md) :

   /content/sites/engage/tw/page/jcr:content/content/primary/reviews

* `Include histogram`

   如果勾選，請加入橫條圖的顯示，指出要匯總的審核中每個星號分數的多少。 預設為未勾選。

### 變更為自訂審核類型 {#changing-to-a-custom-review-type}

Reviews元件使用注釋系統。

變更「註解資源類型」後，註解系統將不再使用預設值產生註解的例項，而是開發人員自訂（擴充）的例項。

在已知自訂資源類型後，進入 [Design Mode](../../help/sites-authoring/default-components-designmode.md) ，然後連按兩下置入的元 `Comments` 件，以開啟具有其他標籤的對話方塊。

在「資 **[!UICONTROL 源類型]** 」頁籤下，為元件的新實例指定自定義資源 `Comments or Voting`類型：

![chlimage_1-349](assets/chlimage_1-349.png)

* **[!UICONTROL 評論資源類型]**

   導覽至/apps中延伸元件( `comment`單一註解)的resourceType。 例如， `/apps/social/commons/components/hbs/comments/comment`

   此資源將識別訪客張貼留言時所建立之UGC的resourceType。

* **[!UICONTROL 投票資源類型]**

   導覽至/apps中延伸元件 `voting`的resourceType。 例如， `/apps/social/components/hbs/voting`

   此資源將識別訪客張貼投票時所建立之UGC的資源類型。

* **[!UICONTROL 注釋系統資源類型]**

   導覽至/apps中延伸元件( `comments`注釋系統)的resourceType。 保留空白，除非頁面范 [本在基礎指令碼中動態包含](scf.md#add-or-include-a-communities-component) 「注釋系統」，而不是以資源（注釋節點）的形式新增至頁面。 閱讀有關 [{{include}}協助工具的更多資訊](handlebars-helpers.md#include)

## 網站訪客體驗 {#site-visitor-experience}

### 協調者與管理員 {#moderators-and-administrators}

當登入的使用者具有協調者或管理員權限時，他們可以執行元件設定所允許的協調工作，不論是誰撰寫審核。

### 成員 {#members}

當網站訪客登入時（視設定而定），他們可能會

* 張貼新審核
* 編輯其自己的審核
* 刪除其自己的審核
* 標籤其他人的審閱注釋

每個成員僅允許一個分級。 會員可隨時變更其評級。

### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的審核、翻譯（如果支援），但不得新增評分或審核，也不得標籤其他人的審核意見。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的Review Essentials](reviews-basics.md) （檢閱基本工具）頁面。

如需已張貼留言的協調，請參閱 [協調使用者產生的內容](moderate-ugc.md)。

如需已張貼意見的轉譯，請參閱轉 [譯使用者產生的內容](translate-ugc.md)。
