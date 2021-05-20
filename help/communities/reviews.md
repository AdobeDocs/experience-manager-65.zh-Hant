---
title: 使用審閱和審閱摘要（顯示）
seo-title: 使用審閱和審閱摘要（顯示）
description: 將「審閱」和「審閱摘要」元件添加到頁面
seo-description: 將「審閱」和「審閱摘要」元件添加到頁面
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 2%

---

# 使用審核和審核摘要（顯示）{#using-reviews-and-reviews-summary-display}

`Reviews`元件是[Comments](comments.md)和[Rating](rating.md)元件的組合，可供使用。

`Reviews Summary (Display)`元件提供`Reviews`元件的活動或關閉實例的摘要，用於顯示站點上其他位置。

>[!NOTE]
>
>不支援匿名發佈審核。 網站訪客必須註冊（成為會員）並登入以參與。 已登入的訪客可隨時更新其審核。

## 將審核添加到頁{#adding-a-review-to-a-page}

若要在製作模式中將`Reviews`元件新增至頁面，請使用元件瀏覽器來找出`Communities / Reviews`並將其拖曳至頁面上的位置，例如與功能相對的位置，供使用者檢閱。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含[必要的用戶端程式庫](reviews-basics.md#essentials-for-client-side)時，會以此方式顯示`Reviews`元件。

![建立審核](assets/create-review.png)

## 配置審核{#configuring-reviews}

選取要存取的放置`Reviews`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 允許的評等]**&#x200B;標籤下，指定要向成員顯示的評等的完整清單。 第一個評等應為整體/一般評等，因為它是提供`Review Summary (Display)`元件平均評等的評等。 預設設定中的後兩個評等應指定不同的標題，而非「Subrating 1」或「Subrating 2」。

![允許評等](assets/configure-review1.png)

* **[!UICONTROL 允許的評等]**

   成員可以從中選擇的評級清單。

   使用上箭頭、下箭頭和刪除按鈕來修改可見的選擇。

   按一下「**[!UICONTROL 新增項目]**」以新增其他評等選擇。

在「**[!UICONTROL 必要評級]**」頁簽下，從需要評級的「**[!UICONTROL 允許評級]**」清單中重新輸入項。 如果僅在「允許的評等」頁簽上指定了某個項，則在成員提交時，該項可能會保留為未標籤。

在網站上，必要的評等會以星號標示。 如果需要某個項，並且未標籤該項，則會向成員顯示消息，並拒絕提交，直到標籤所有必需的評級為止。

![必要評等](assets/configure-review2.png)

* **[!UICONTROL 必要評等]**

   允許的評級的子集，指明需要哪些評級。

   使用上箭頭、下箭頭和刪除按鈕來修改可見的選擇。

   按一下「**[!UICONTROL 新增項目]**」以新增其他回應選項。

>[!NOTE]
>
>如果在&#x200B;**[!UICONTROL 允許評級]**&#x200B;頁簽上未指定的&#x200B;**[!UICONTROL 必需評級]**&#x200B;頁簽上輸入了項，則該項不包含在要評級的項目中。

在&#x200B;**[!UICONTROL Reviews]**&#x200B;標籤下，指定如何處理查看。

![評論](assets/configure-review3.png)

* **[!UICONTROL 允許回覆]**

   如果選中，則允許回復。 預設為未勾選。

* **[!UICONTROL 已關閉]**

   如果選中，則新審閱和回復將關閉審閱。 預設為未勾選。

* **[!UICONTROL 允許檔案上傳]**

   如果選中此選項，則允許上載檔案附件以供審閱。 預設為未勾選。

* **最大檔案大小**

   只有在勾選「**[!UICONTROL 允許檔案上傳]**」時相關。 此欄位會限制上傳之檔案的大小（以位元組為單位）。 預設為10 MB。

* **[!UICONTROL 訊息長度上限]**

   可輸入文本框的字元數上限。 預設為4096個字元。

* **[!UICONTROL 允許的檔案類型]**

   只有在勾選「**[!UICONTROL 允許檔案上傳]**」時相關。 副檔名清單（以逗號分隔）以「點」分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **[!UICONTROL RTF 編輯器]**

   如果勾選此選項，則可以使用標籤輸入貼文。 預設為未勾選。

* **[!UICONTROL 允許投票]**

   如果勾選此選項，請加入主題的「投票」功能。 預設為未勾選。

在&#x200B;**[!UICONTROL 使用者協調]**&#x200B;標籤下，指定如何管理已張貼的審核。 如需詳細資訊，請參閱[協調使用者產生的內容](moderate-ugc.md)。

![使用者協調](assets/configure-review4.png)

* **[!UICONTROL 事先審核]**

   若勾選此選項，審核必須先經過核准，才會顯示在發佈網站上。 預設為未勾選。

* **[!UICONTROL 刪除評論]**

   如果選中，則發佈審核的成員將能夠刪除它。 預設為未勾選。

* **[!UICONTROL 拒絕審核]**

   如果勾選此選項，允許協調者拒絕審核。 預設為未勾選。

* **[!UICONTROL 關閉/重新開啟審核]**

   如果勾選此選項，則允許協調者關閉和重新開啟審核。 預設為未勾選。

* **[!UICONTROL 標幟評論]**

   如果選中，允許成員將審核標籤為不適當。 預設為未勾選。

* **[!UICONTROL 標誌原因清單]**

   如果選中，則允許成員從下拉清單中選擇其將審核標籤為不適當的理由。 預設為未勾選。

* **[!UICONTROL 自訂標幟原因]**

   如果選中，則允許成員輸入自己的理由，將審核標籤為不適當。 預設為未勾選。

* **[!UICONTROL 協調臨界值]**

   輸入在通知協調者之前，成員必須標籤審核的次數。 預設為一次(1)。

* **[!UICONTROL 標幟限制]**

   輸入在從公開檢視中隱藏審核前必須標籤的次數。 此數字必須大於或等於&#x200B;**[!UICONTROL 協調臨界值]**。 預設為5。

### 將審核摘要（顯示）添加到頁{#adding-a-review-summary-display-to-a-page}

若要在製作模式中將`Reviews Summary (Display)`元件新增至頁面，請找出元件

* `Communities / Reviews Summary (Display)`

並將其拖曳至要顯示活動或已結束檢閱摘要的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](reviews-basics.md#essentials-for-client-side)時，會以此方式顯示`Reviews Summary (Display)`元件。

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>「平均值」反映摘要檢閱之「允許的評等」索引標籤上所列第一個項目的投票數。

### 配置審核摘要（顯示）{#configuring-reviews-summary-display}

選取要存取的放置`Reviews Summary (Display)`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

在&#x200B;**[!UICONTROL 查看摘要]**&#x200B;標籤下

![review-summary](assets/configure-review6.png)

* `Review Path`

   輸入或瀏覽至`reviews`元件的放置實例以匯總，例如，如果添加到[Geometrixx參與站點的網頁，](getting-started.md)路徑將是：

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果勾選此選項，則包括橫條圖的顯示，指出摘要中每個星級有多少。 預設為未勾選。

### 更改為自定義審閱類型{#changing-to-a-custom-review-type}

「審閱」元件使用「注釋系統」。

通過更改「注釋資源類型」，注釋系統將不再使用預設值生成注釋的實例，而是由開發人員自定義（擴展）的實例。

在已知自定義資源類型後，輸入[設計模式](../../help/sites-authoring/default-components-designmode.md)並按兩下放置的`Comments`元件以開啟帶有附加頁簽的對話框。

在&#x200B;**[!UICONTROL 資源類型]**&#x200B;標籤下，為`Comments or Voting`元件的新實例指定自定義resourceType:

![留言投票](assets/configure-review7.png)

* **[!UICONTROL 評論資源類型]**

   導覽至/apps中延伸`comment`元件（單一註解）的resourceType。 例如， `/apps/social/commons/components/hbs/comments/comment`。

   此資源會識別訪客發佈留言時所建立之UGC的resourceType。

* **[!UICONTROL 投票資源類型]**

   導覽至/apps中延伸`voting`元件的resourceType。 例如， `/apps/social/components/hbs/voting`。

   此資源會識別訪客張貼投票時建立之UGC的資源類型。

* **[!UICONTROL 注釋系統資源類型]**

   導覽至/apps中延伸`comments`元件（註解系統）的resourceType 。 請保留空白，除非頁面範本[動態地在基礎指令碼中包含](scf.md#add-or-include-a-communities-component)註解系統，而非以資源（註解節點）的形式新增至頁面。 閱讀[{{include}} helper](handlebars-helpers.md#include)以了解更多資訊。

## 網站訪客體驗{#site-visitor-experience}

### 協調者和管理員{#moderators-and-administrators}

當登入的使用者擁有版主或管理員權限時，無論審核的作者為何，他們都能執行元件組態所允許的審核工作。

### 成員 {#members}

網站訪客登入時（視設定而定）可能會：

* 張貼新審核
* 編輯自己的審核
* 刪除自己的審核
* 標幟其他人的審核意見

每個成員僅允許一個評級。 會員可隨時更改其評級。

### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的評論、翻譯（如果支援），但不得新增評分或評論，也不得標籤其他人的評論。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[ Review Essentials](reviews-basics.md)頁面。

如需已張貼留言的調節，請參閱[調節使用者產生的內容](moderate-ugc.md)。

有關已張貼評論的翻譯，請參閱[翻譯用戶生成的內容](translate-ugc.md)。
