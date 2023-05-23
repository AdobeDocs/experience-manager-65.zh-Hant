---
title: 使用審閱和審閱摘要（顯示）
seo-title: Using Reviews and Reviews Summary (Display)
description: 將「審閱」和「審閱摘要」元件添加到頁面
seo-description: Adding the Reviews and Reviews Summary components to a page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 2%

---

# 使用審閱和審閱摘要（顯示） {#using-reviews-and-reviews-summary-display}

的 `Reviews` 元件是 [注釋](comments.md) 和 [評級](rating.md) 元件可供使用。

的 `Reviews Summary (Display)` 元件提供活動或關閉實例的摘要 `Reviews` 用於在站點的其他位置顯示的元件。

>[!NOTE]
>
>不支援匿名發佈審閱。 站點訪問者必須註冊（成為成員）並登錄以參與。 已簽署的訪問者可隨時更新其審查。

## 將審閱添加到頁面 {#adding-a-review-to-a-page}

添加 `Reviews` 在作者模式下對頁面的元件，使用元件瀏覽器查找 `Communities / Reviews` 並將其拖到頁面上，如相對於要供用戶查看的功能的位置。

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當 [所需的客戶端庫](reviews-basics.md#essentials-for-client-side) 包括，這是 `Reviews` 元件。

![建立審閱](assets/create-review.png)

## 配置審閱 {#configuring-reviews}

選取已放置的 `Reviews` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置 — 新建](assets/configure-new.png)

在 **[!UICONTROL 允許的評級]** 頁籤，指定要顯示給成員的評級的完整清單。 第一個評級應是總體/一般評級，因為它是提供對 `Review Summary (Display)` 元件。 預設配置中的後兩個分級應指定不同的標題，而不是「分級1」或「分級2」。

![允許評級](assets/configure-review1.png)

* **[!UICONTROL 允許的評等]**

   成員可以從中選擇的評級清單。

   使用上箭頭、下箭頭和刪除按鈕修改可見的選擇。

   按一下 **[!UICONTROL 添加項]** 添加其他評級選項。

在 **[!UICONTROL 所需評級]** 的子菜單。 **[!UICONTROL 允許的評級]** 需要評級的。 如果僅在「允許的評級」頁籤上指定了項，則成員提交時可能不標籤該項。

在網站上，必需評級標有星號。 如果需要某個項，並且未標籤，則會向成員顯示一條消息，並且在標籤所有必需評級之前拒絕提交。

![要求評級](assets/configure-review2.png)

* **[!UICONTROL 必要評等]**

   允許評級的子集，指示需要哪些評級。

   使用上箭頭、下箭頭和刪除按鈕修改可見的選擇。

   按一下 **[!UICONTROL 添加項]** 來添加其他響應選項。

>[!NOTE]
>
>如果在 **[!UICONTROL 所需評級]** 頁籤 **[!UICONTROL 允許的評級]** 頁籤，則不會將其包含在要評級的項目中。

在 **[!UICONTROL 評論]** 頁籤，指定處理審閱的方式。

![評論](assets/configure-review3.png)

* **[!UICONTROL 允許答復]**

   如果選中，則允許回複評論。 未選中預設值。

* **[!UICONTROL 已關閉]**

   如果選中，則審閱將關閉新審閱和回復。 未選中預設值。

* **[!UICONTROL 允許檔案上傳]**

   如果選中，則允許上載檔案附件以供審閱。 未選中預設值。

* **最大檔案大小**

   僅在 **[!UICONTROL 允許檔案上載]** 的子菜單。 此欄位限制上載檔案的大小（以位元組為單位）。 預設為10 MB。

* **[!UICONTROL 訊息長度上限]**

   可輸入到文本框中的最大字元數。 預設為4096個字元。

* **[!UICONTROL 允許的檔案類型]**

   僅在 **[!UICONTROL 允許檔案上載]** 的子菜單。 以逗號分隔的檔案副檔名清單，其中帶有「點」分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許指定那些未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **[!UICONTROL RTF 編輯器]**

   如果選中，則可以使用標籤輸入帖子。 未選中預設值。

* **[!UICONTROL 允許投票]**

   如果選中，則包括主題的投票功能。 未選中預設值。

在 **[!UICONTROL 用戶審核]** 頁籤，指定如何管理已過帳的審閱。 有關詳細資訊，請參見 [調節用戶生成的內容](moderate-ugc.md)。

![用戶審核](assets/configure-review4.png)

* **[!UICONTROL 事先審核]**

   如果選中，則必須先批准審閱，然後才會將審閱顯示在發佈網站上。 未選中預設值。

* **[!UICONTROL 刪除審閱]**

   如果選中，則發佈審閱的成員將能夠刪除審閱。 未選中預設值。

* **[!UICONTROL 拒絕審閱]**

   如果選中，允許審閱人拒絕審閱。 未選中預設值。

* **[!UICONTROL 關閉/重新開啟審閱]**

   如果選中，允許審閱人關閉並重新開啟審閱。 未選中預設值。

* **[!UICONTROL 標籤審閱]**

   如果選中，允許成員將審閱標籤為不適當。 未選中預設值。

* **[!UICONTROL 標誌原因清單]**

   如果選中，則允許成員從下拉清單中選擇將審閱標籤為不適當的原因。 未選中預設值。

* **[!UICONTROL 自定義標誌原因]**

   如果選中，允許成員輸入將審閱標籤為不適當的自己原因。 未選中預設值。

* **[!UICONTROL 審核閾值]**

   輸入成員在通知審閱人之前必須標籤審閱的次數。 預設值為一次(1)。

* **[!UICONTROL 標籤限制]**

   輸入在將審閱隱藏在公共視圖之前必須標籤的次數。 此數字必須大於或等於 **[!UICONTROL 審核閾值]**。 預設值為5。

### 將審閱摘要（顯示）添加到頁面 {#adding-a-review-summary-display-to-a-page}

添加 `Reviews Summary (Display)` 在作者模式下將元件定位到頁面

* `Communities / Reviews Summary (Display)`

並將其拖到要顯示活動或關閉審閱摘要的頁面上。

如需必要資訊，請訪問 [社區元件基礎](basics.md)。

當 [所需的客戶端庫](reviews-basics.md#essentials-for-client-side) 包括，這是 `Reviews Summary (Display)`元件。

![審閱摘要](assets/configure-review5.png)

>[!NOTE]
>
>「平均值」反映匯總的審閱的「允許評級」頁籤上列出的第一項的投票。

### 配置審閱摘要（顯示） {#configuring-reviews-summary-display}

選取已放置的 `Reviews Summary (Display)` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

在 **[!UICONTROL 審閱摘要]** 頁籤

![審閱摘要](assets/configure-review6.png)

* `Review Path`

   輸入或瀏覽至 `reviews`元件，例如，如果添加到的Web頁 [Geometrixx參與網站，](getting-started.md) 路徑是：

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果選中，則包括條形圖的顯示，該條形圖指示摘要中每個星級分數的多少。 未選中預設值。

### 更改為自定義審閱類型 {#changing-to-a-custom-review-type}

「審閱」(Reviews)元件使用「注釋系統」(Comment System)。

通過更改注釋資源類型，注釋系統將不再使用預設值生成注釋實例，而是使用開發人員自定義（擴展）的注釋實例。

在已知自定義資源類型後，輸入 [設計模式](../../help/sites-authoring/default-components-designmode.md) 並按兩下放置的 `Comments` 的子菜單。

在 **[!UICONTROL 資源類型]** 頁籤，為 `Comments or Voting` 元件：

![評語投票](assets/configure-review7.png)

* **[!UICONTROL 評論資源類型]**

   導航到擴展的resourceType `comment`/apps中的元件（單個注釋）。 比如說， `/apps/social/commons/components/hbs/comments/comment`。

   此資源將標識訪問者發佈注釋時建立的UGC的resourceType。

* **[!UICONTROL 投票資源類型]**

   導航到擴展的resourceType `voting`/apps中的元件。 比如說， `/apps/social/components/hbs/voting`。

   此資源將標識訪問者投票時建立的UGC的資源類型。

* **[!UICONTROL 注釋系統資源類型]**

   導航到擴展的resourceType `comments`/apps中的元件（注釋系統）。 除非頁面模板，否則保留為空 [動態包](scf.md#add-or-include-a-communities-component) 在基礎指令碼中添加註釋系統，而不是作為資源（注釋節點）添加到頁面。 通過閱讀 [{{include}} 幫助](handlebars-helpers.md#include)。

## 站點訪問者體驗 {#site-visitor-experience}

### 審閱人和管理員 {#moderators-and-administrators}

當登錄用戶具有版主或管理員權限時，他們能夠執行元件配置允許的審核任務，而不管是誰建立了審閱。

### 成員 {#members}

站點訪問者登錄時，根據配置的不同，他們可以：

* 發佈新審閱
* 編輯自己的審閱
* 刪除其自己的審閱
* 標籤其他審閱評論

每個成員只允許一個分級。 會員可隨時更改其評級。

### 匿名 {#anonymous}

未登錄的站點訪問者只能閱讀已發佈的評論、翻譯（如果支援），但不能添加評級或評論，也不能標籤其他評論評論。

## 其他資訊 {#additional-information}

有關 [審閱基本內容](reviews-basics.md) 頁面。

有關審核已發佈的注釋，請參閱 [調節用戶生成的內容](moderate-ugc.md)。

有關已發佈注釋的翻譯，請參閱 [翻譯用戶生成的內容](translate-ugc.md)。
