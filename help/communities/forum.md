---
title: 論壇功能
description: 瞭解如何新增及設定論壇功能，為登入社群成員提供建立、檢視、關注、搜尋或回覆主題的區域。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 8%

---

# 論壇功能{#forum-feature}

## 簡介 {#introduction}

論壇功能為發佈環境中的登入網站訪客（社群成員）提供一個區域，以：

* 建立主題
* 檢視和回覆主題
* 關注主題
* 搜尋論壇
* 協助稽核論壇內容
* 將論壇主題從一個頁面移動到另一個頁面

本檔案的這一節將說明：

* 將論壇功能新增至AEM網站。
* 的組態設定 `Forum` 元件。

### 新增論壇至頁面 {#adding-a-forum-to-a-page}

若要新增 `Forum` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Forum`

並將其拖曳至論壇應出現的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/essentials-forum.md#essentials-for-client-side) 包含，這就是 `Forum` 元件出現：

![論壇 — 元件](assets/forum-component.png)

### 設定論壇 {#configuring-a-forum}

選取已放置的 `Forum` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### 設定標籤 {#settings-tab}

在 **設定** 索引標籤，指定主題和回覆的設定：

* **允許附件縮圖**

  如果勾選，則會建立附加影像的縮圖。

* **附加縮圖最大尺寸**

  附件縮圖影像的最大尺寸（畫素）。 預設值為800 x 800。

* **最小縮圖影像大小**
* **最大縮圖尺寸**

  內嵌影像的最大縮圖影像大小（畫素）。 預設值為800 x 800。

* **每頁主題**

  定義每個頁面顯示的主題/帖子數。預設為 10。

* **已審核**

  如果勾選，則必須先核准發佈主題和註解，才能將其顯示在發佈網站上。 預設為未勾選。

* **已關閉**

  如果勾選，論壇將關閉並顯示新主題和評論。 預設為未勾選。

* **RTF 編輯器**

  如果勾選，主題和註解可能會以標示輸入。 預設為未勾選。

* **允許標記**

  如果勾選，則允許成員將標籤新增至他們的貼文(請參閱 **標籤欄位** 標籤)。 預設為未勾選。

* **允許檔案上傳**

  如果勾選，允許將檔案附件新增至主題或註解。 預設為未勾選。

* **允許關注**

  如果勾選，則為論壇貼文納入以下功能，可讓成員成為 [已通知](/help/communities/notifications.md) 新貼文的。 預設為未勾選。

* **允許釘選**

  如果勾選，論壇主題可以釘選到主題清單的頂端。 預設為未勾選。

* **允許主要內容**

  如果勾選，該創意可識別為 [主要內容](/help/communities/featured.md). 預設為未勾選。

* **允許電子郵件訂閱**

  如果勾選，允許成員透過電子郵件接收新貼文的通知([訂閱](/help/communities/subscriptions.md))。 需要 `Allow Following` 待核取及 [電子郵件已設定](/help/communities/email.md). 預設為未勾選。

* **最大檔案大小**

  只有在 `Allow File Uploads` 已勾選。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600 (10 Mb)。

* **允許的檔案類型**

  只有在 `Allow File Uploads` 已勾選。 以「點」分隔符號的副檔名清單（以逗號分隔）。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則無法上傳未指定的檔案型別。 預設為「無」，因此允許所有檔案型別。

* **附加影像檔案大小上限**
只有在勾選「允許檔案上傳」時才相關。 已上傳影像檔案的最大位元組數。 預設值為2097152 (2 Mb)。

* **允許執行緒式回覆**

  如果勾選，允許回覆張貼至主題的評論。 預設為未勾選。

* **允許投票**

  如果勾選，請包含投票功能與主題。 預設為未勾選。

* **允許使用者刪除評論和主題**

  如果勾選，則允許成員刪除他們張貼的評論和主題。 預設為未勾選。

* **顯示階層連結**

  如果勾選，在主題頁面上顯示導覽階層連結。 預設為已核取。

* **顯示徽章**

  如果勾選，則顯示已習得和已指派 [徽章](/help/communities/implementing-scoring.md) 使用成員的部落格專案。 預設為未勾選。

* **允許有特殊權限的成員**

  如果勾選，則僅允許擁有特殊許可權的成員建立內容。

* **允許擁有特殊權限的成員**

  新增允許建立內容的特殊許可權成員。

* **在作者編輯模式下封鎖使用者產生的內容**

  如果啟用，在作者模式下編輯時會封鎖使用者產生的內容。

* **啟用提及功能**

  啟用後，可讓註冊社群使用者識別其他註冊成員（使用名字、姓氏、使用者名稱），並使用一般的@user-name語法標籤這些成員。 標籤的使用者會收到他們提及的通知。

* **最大提及數**

  限制貼文中允許提及的最大數量。 預設值為10。

* **UI 提及模式**

  指定允許的模式字串，以在貼文中標籤(@mention)已註冊的使用者。 例如，`~{{familyName}}{{givenName}}`。

>[!NOTE]
>
>可能有必要同時檢查兩者 `AllowThreaded Replies` 和 `Allow users to Delete Comments and Topics` 啟用主題上的註解。

#### 「使用者稽核」標籤 {#user-moderation-tab}

在 **使用者稽核** 索引標籤，指定如何管理張貼的主題和回覆（使用者產生的內容）。 如需詳細資訊，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

* **拒絕貼文**

  如果勾選，則允許受信任的成員版主拒絕貼文，並阻止貼文出現在公開論壇上。 預設為未勾選。

* **關閉/重新開啟主題**

  如果勾選，受信任的成員版主可能會關閉主題以進一步編輯和註釋，也可能重新開啟主題。 預設為未勾選。

* **移動主題**

  如果勾選，允許發佈端的版主移動主題。 預設為已核取。

* **標幟帖子**

  如果勾選，則允許成員將其他人的主題或評論標籤為不適當。 預設為未勾選。

* **標幟原因清單**

  如果勾選，則允許成員從下拉式清單中選擇標幟主題或評論為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

  如果勾選，則允許成員輸入將主題或評論標幟為不適當的原因。 預設為未勾選。

* **稽核臨界值**

  輸入在通知版主前，主題或評論必須由成員標幟的次數。 預設值為1 （一次）。

* **標幟限制**

  輸入主題或註解在隱藏於公眾檢視之前必須加上標籤的次數。 如果設為–1，則標幟的主題或註解絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於「稽核臨界值」。 預設值為5。

#### 標籤欄位索引標籤 {#tag-field-tab}

在 **標籤欄位** 標籤中，如果允許的話，則會套用的標籤 **設定** 索引標籤中，會根據選取的名稱空間而有所限制。

* **允許的命名空間**

  相關條件 `Allow Tagging` 已勾選下方的 **設定** 標籤。 可套用的標籤僅限於已核取的名稱空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設名稱空間）和「包含所有標籤」。 預設為未勾選，這表示允許所有名稱空間。

* **建議限制**

  輸入要顯示為論壇成員張貼建議之標籤數目。 預設值為**-**1 （無限制）。

#### 翻譯索引標籤 {#translation-tab}

在 **翻譯** 索引標籤中，如果社群網站已啟用翻譯，則可將翻譯設定為翻譯整個主題或選取的貼文。

* **全部轉換**

  如果勾選，論壇對話串將翻譯成使用者偏好的語言。 預設為未勾選。

#### 排序設定索引標籤 {#sort-settings-tab}

在 **排序設定** 索引標籤，指定張貼的評論在顯示時的排序方式。

* **排序方式**

  檢查所有允許的排序選取專案： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. 預設為 `Newest, Oldest, Last Updated`.

* **設為預設值**

  下拉式選單，選取其中一個核取的排序選項，以顯示為預設值。 預設為 `Newest`.

* **選取 Analytics 排序的時間選項**

  下拉式選單以選取下列其中一個選項： `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  預設為 `All`.

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [論壇要點](/help/communities/essentials-forum.md) 開發人員頁面。

有關張貼主題和評論的稽核，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

若要標籤張貼的主題和評論，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).

如需已張貼主題和評論的翻譯，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).
