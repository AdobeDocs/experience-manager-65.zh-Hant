---
title: 部落格功能
seo-title: 部落格功能
description: 以日誌格式提供社群資訊
seo-description: 以日誌格式提供社群資訊
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# 部落格功能 {#blog-feature}

## 簡介 {#introduction}

AEM Communities的部落格功能已從編寫活動轉變為真正的社群活動，並在發佈環境中進行。

部落格功能支援以日誌格式提供社區資訊。 部落格項目是由授權會員（已註冊、已登入的使用者）在發佈環境中建立的。

部落格功能提供：

* 發佈端建立部落格文章和留言
* 豐富式文字編輯
* 內嵌影像（支援拖放）
* 內嵌社交網路內容([內嵌支援](/help/communities/blog-developer-basics.md#allowing-rich-media))
* 草稿模式
* 排程發佈
* 代表撰寫(特權 [會員](/help/communities/users.md#privileged-members-group) ，可以代表不同社群成員建立內容)
* [部落格文章與留言的內容內容](/help/communities/moderate-ugc.md) ，以及大量協調

本檔案章節說明：

* 新增部落格功能至AEM網站
* 部落格元件的組態設定

>[!NOTE]
>
>元件 `Journal`和 `Journal Sidebar` 的標題 `Blog` 為和 `Blog Sidebar`。
>
>AEM 6.0及舊版中的部落格功能現在已移除。 它以範本為基礎，僅允許作者在作者環境中建立內容。

## 將部落格元件新增至頁面 {#adding-blog-components-to-a-page}

如果想要以作者模式將部落格新增至頁面，請使用元件瀏覽器來尋找

* `Communities / Blog`
* `Communities / Blog Sidebar`

並將它們拖曳至應該出現部落格的頁面上。

如需必要資訊，請造 [訪Communities Components Basics](/help/communities/basics.md)。

當包含 [所需的用戶端程式庫](/help/communities/blog-developer-basics.md#essentials-for-client-side) ，元件的顯示 `Blog`方式如下：

![chlimage_1-229](assets/chlimage_1-229.png)

以及將如何 `Blog Sidebar` 顯示：

![chlimage_1-230](assets/chlimage_1-230.png)

### 設定部落格 {#configuring-blog}

選擇要訪問 `Blog` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-231部落格](assets/chlimage_1-231.png)![設定](assets/blog-configure.png)

#### 「設定」頁籤 {#settings-tab}

在「設 **定** 」標籤下，指定部落格的基本功能：

* **允許附件縮圖**

   如果勾選，則會建立附加影像的縮圖。

* **附加縮圖最大尺寸**

   附件縮圖影像的最大大小（以像素為單位）。 預設值為800 x 800。

* **最小縮圖影像大小**

   產生內嵌影像縮圖的影像最小大小（以位元組為單位）。 預設值為100000位元組(100kb)。

* **最大縮圖尺寸**

   內嵌影像的縮圖影像大小上限（以像素為單位）。 預設值為800 x 800。

* **允許有特殊權限的成員**

   如果勾選，則僅允許特權成員建立內容。

* **允許擁有特殊權限的成員**

   添加允許建立內容的特權成員。

* **封鎖使用者在作者編輯模式中產生的內容**

   啟用後，在「作者模式」中編輯時，會封鎖使用者產生的內容。

* **日誌標題**

   要顯示在頁面上的部落格標題。

>[!NOTE]
>
>「日誌標題」用於自動建立部落格的URL。
>您在此處指定的日誌標題中，最多使用50個字元（另外還有5個字元）來建立部落格的URL。

* **日誌說明**

   部落格說明。

* **每頁主題**

   定義每頁顯示的部落格項目／留言數。 預設值為10。

* **已審核**

   如果勾選，則必須先核准張貼部落格項目和留言，才能顯示在發佈的網站上。 預設為未勾選。

* **已關閉**

   如果勾選，則部落格將關閉到新的部落格條目和注釋。 預設為未勾選。

* **RTF 編輯器**

   如果勾選此選項，則可以使用標籤輸入部落格條目和注釋。 已勾選預設值。

* **允許標記**

   如果勾選，允許成員將標籤標籤新增至其貼文(請參 **閱「標籤欄位** 」標籤)。 預設為未勾選。

* **允許檔案上傳**

   如果選中，則允許將檔案附件添加到部落格條目或注釋中。 預設為未勾選。

* **最大檔案大小**

   僅在勾選時 `Allow File Uploads` 相關。 此欄位將限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600(10 Mb)。

* **允許的檔案類型**

   僅在勾選時 `Allow File Uploads` 相關。 以逗號分隔的副檔名清單，並以&quot;dot&quot;分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定任何檔案類型，則不允許上傳未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **附加影像檔案最大大小**

   僅在勾選「允許檔案上傳」時相關。 上傳的影像檔案的位元組數上限。 預設值為2097152(2 Mb)。

* **允許回覆**

   如果勾選，則允許回覆張貼至部落格項目的留言。 預設為未勾選。

* **允許投票**

   如果勾選，請將「投票」功能與部落格項目一起加入。 預設為未勾選。

* **允許使用者刪除評論和主題**

   如果勾選，允許成員刪除他們張貼的留言和部落格項目。 預設值為** **uncebled。

* **允許關注**

   如果勾選，請為部落格文章加入下列功能，讓成員得 [到](/help/communities/notifications.md) 新貼文的通知。 預設為未勾選。

* **允許電子郵件訂閱**

   如果勾選，允許會員透過電子郵件（訂閱）收到新貼文[的通](/help/communities/subscriptions.md)知。 需要 `Allow Following` 檢查並設定電 [子郵件](/help/communities/email.md)。 預設為未勾選。

* **顯示徽章**

   如果勾選，則使用成員的 [部落格項目](/help/communities/implementing-scoring.md) ，顯示已獲得和已指派的徽章。 預設為未勾選。

* **不在清單頁面上取得回覆**

* **允許主要內容**

   如果勾選，此構想就可識別為特 [色內容](/help/communities/featured.md)。 預設為未勾選。

* **啟用提及功能**

   如果啟用，則允許註冊的社區用戶標識其他已註冊成員（使用名、姓、用戶名），並使用通用的@user-name語法標籤這些成員。 標籤使用者會收到有關其提及次數的通知。

* **最大提及數**

   限制貼文中允許的提及次數上限。 預設值為10。

* **UI 提及模式**

   將已授權的模式字串指定為貼文中已註冊使用者的標籤（@提及）。 例如~{{familyName}}{{givenName}}。

#### 使用者協調標籤 {#user-moderation-tab}

在「使用 **者協調** 」標籤下，指定協調設定：

* **拒絕貼文**

   如果勾選，則可讓受信任的會員協調者拒絕貼文，並防止貼文出現在公開論壇。 預設為未勾選。

* **關閉／重新開啟主題**

   如果勾選，受信任的成員協調者可以關閉主題以進一步編輯和留言，也可以重新開啟主題。 預設為未勾選。

* **標籤貼文**

   如果勾選，允許成員將其他主題或注釋標籤為不適當。 預設為未勾選**。**

* **標籤原因清單**

   如果勾選，允許成員從下拉式清單中選擇其標籤主題或留言的不適當原因。 預設為未勾選。

* **自訂標幟原因**

   如果勾選，允許成員輸入自己將主題或留言標籤為不適當的原因。 預設為未勾選**。**

* **協調臨界值**

   輸入成員在通知協調者之前必須標籤主題或留言的次數。 預設值為1（一次）。

* **標幟限制**

   輸入主題或留言在公開檢視中隱藏前必須加以標幟的次數。 如果設為-1，則標籤的主題或留言永遠不會隱藏在公開檢視中。 否則，此數字必須大於或等於「協調臨界值」。 預設值為5。

#### 「標籤」欄位頁籤 {#tag-field-tab}

在「標 **簽欄位** 」標籤下，指定如果「設定」標籤上勾選「允許標籤 **」，可套用哪些標** 簽 **** :

* **允許的命名空間**

   如果在** `Allow Tagging` 設定**標籤下勾選，則相關。 可套用的標籤僅限於已勾選之命名空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設命名空間）和「包含所有標籤」。 預設值未勾選，表示允許所有命名空間。

* **建議限制**

   輸入要作為建議顯示給發佈到論壇的成員的標籤數。 值-1表示無限制。 預設值為0。

### 配置部落格側欄 {#configuring-blog-sidebar}

按兩下元件時，將 `Blog Sidebar` 開啟編輯對話框。

在「日記 **帳側欄設定** 」標籤下，指定封存的日期格式以及要在側邊欄中顯示的項目類型：

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **日期格式**

   用於部落格條目存檔的顯示格式。 格式使用遵循Java約定的佔位符。

   * yyyy:全年，就像2015年一樣
   * yy:短年，比如15年。
   * MMMMMM:整月，就像6月
   * MMM:短月，就像6月
   * MM:月數，例如06
   預設值為&quot;yyyy MMMMM&quot;，會顯示例如&quot;2015 June&quot;

* **視圖類型**

   要顯示在側欄中的部落格項目的標題和類型。 選擇是

   * 作者
   * 類別
   * 封存

* **Blopg元件路徑**

   *（可選）* ，列出部落格文章的部落格資源位置。 如果保留為空白，將使用顯示在同一頁 `social/journal/components/hbs/journal` 上的resourceType元件。

   * 例如， `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **建議限制**

   要顯示的部落格文章數目。 值-1表示無限制。 預設值為-1。

## 網站訪客體驗 {#site-visitor-experience}

在發佈環境中，部落格功能會以遞減順序顯示最近的部落格文章，接著是較舊的部落格文章。 部落格側邊欄可讓網站訪客套用篩選器，以限制所顯示的部落格文章選擇。

在部落格文章後面會加上貼文或檢視留言的連結。

選取部落格文章時，會顯示部落格文章和註解（如果已啟用）。

其他功能取決於網站訪客是協調者、管理員、社群成員、特權成員還是匿名。

### 使用文章 {#working-with-articles}

建立新部落格文章時，您可以選擇：

1. 立即發佈
1. 發佈草稿
1. 在排程的日期和時間發佈

部落格文章會出現在適當的標籤（「已發佈」、「草稿」或「已排程」）下方，供能夠在發佈時撰寫的成員使用。

#### 協調者與管理員 {#moderators-and-administrators}

當登入的使用者具有協調者或管理員權限時，他們可以對張貼至部落格的所有部落格文章和留言執行 [協調任務](/help/communities/moderate-ugc.md) （依照元件組態的許可）。

![chlimage_1-232](assets/chlimage_1-232.png)

#### 成員 {#members}

當登入使用者是社群成員或特權 [成員](/help/communities/users.md#privileged-members-group) （視設定而定）時，他們可以選 `New Article` 擇建立並張貼新的部落格文章。

具體而言，他們可能：

* 建立新的部落格文章
* 代表其他會員張貼新部落格文章
* 將評論張貼至部落格文章
* 編輯其自己的部落格文章或評論
* 刪除其自己的部落格或評論
* 標籤其他人的部落格文章或留言

![chlimage_1-233](assets/chlimage_1-233.png) ![chlimage_1-234](assets/chlimage_1-234.png)

#### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的部落格文章和留言、在受支援時加以翻譯，但不得新增部落格文章或留言，也不得為其他人的文章或留言加上旗標。

![chlimage_1-235](assets/chlimage_1-235.png)

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的 [Blog Essentials](/help/communities/blog-developer-basics.md) （部落格基本功能）頁面。

如需部落格項目和留言的協調，請參閱 [協調使用者產生的內容](/help/communities/moderate-ugc.md)。

如需標籤部落格項目和注釋，請參 [閱標籤使用者產生的內容](/help/communities/tag-ugc.md)。

有關部落格條目和注釋的翻譯，請參 [閱翻譯用戶生成的內容](/help/communities/translate-ugc.md)。
