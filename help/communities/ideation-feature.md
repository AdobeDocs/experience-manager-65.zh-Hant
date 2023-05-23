---
title: 標識特徵
seo-title: Ideation Feature
description: 添加和配置標識功能
seo-description: Adding and configuring the Ideation feature
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 9%

---

# 標識特徵 {#ideation-feature}

## 簡介 {#introduction}

該標識功能為發佈環境中的登錄站點訪問者（社區成員）提供了一個區域，以：

* 建立想法與社區共用。
* 查看和評論觀點。
* 跟著一個主意。
* 投一票。

文檔的本節介紹：

* 正在將建立功能添加AEM到站點。
* 標識元件的配置設定。

### 向頁面添加標識 {#adding-a-ideation-to-a-page}

添加 `Ideation` 在作者模式下對頁面的元件，使用元件瀏覽器查找

* `Communities / Ideation`

並將其拖到應該出現想法的頁面上。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

當 [所需的客戶端庫](/help/communities/ideation.md#essentials-for-client-side) 包括，這是 `Ideation` 元件將出現：

![識別](assets/ideation.png)

### 配置標識 {#configuring-an-ideation}

選取已放置的 `Ideation` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置 — 新建](assets/configure-new.png)

![標識設定](assets/ideation-settings.png)

#### 「設定」頁籤 {#settings-tab}

在 **[!UICONTROL 設定]** 頁籤，指定想法和注釋的設定：

* **允許附件縮圖**
* **附加縮圖最大尺寸**
* **最小縮圖影像大小**
* **最大縮圖尺寸**
* **允許有特殊權限的成員**
* **允許擁有特殊權限的成員**
* **封鎖使用者在作者編輯模式中產生的內容**
* **創意力標題**

* 想法的顯示標題。 預設值為 `Ideation`。
* **創意力說明**

   要顯示為該想法的子標題的說明。 預設值是沒有說明。

* **每頁主題**

   定義每頁顯示的想法/帖子數。 預設值為10。

* **已審核**

   如果選中，則必須先批准發佈思想和評論，然後才能將其顯示在發佈網站上。 未選中預設值。

* **已關閉**

   如果選中，則建立論壇將不會顯示新思想和評論。 未選中預設值。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入思想和注釋。 未選中預設值。

* **允許標記**

   如果選中，允許成員將標籤標籤添加到其帖子(請參見 **[!UICONTROL 標籤欄位]** )的正平方根。 未選中預設值。

* **允許檔案上傳**

   如果選中，則允許將檔案附件添加到思想或注釋中。 未選中預設值。

* **最大檔案大小**

   僅在 `Allow File Uploads` 的子菜單。 此欄位將限制上載檔案的大小（以位元組為單位）。 預設為104857600(10 Mb)。

* **允許的檔案類型**

   僅在 `Allow File Uploads` 的子菜單。 以逗號分隔的檔案副檔名清單，其中帶有「點」分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許上載未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **附加影像檔案最大大小**

   僅當選中「允許檔案上載」時相關。 上載的影像檔案可能具有的最大位元組數。 預設為2097152(2 Mb)。

* **允許答復**

   如果選中，則允許對發佈到該想法的注釋進行答復。 未選中預設值。

* **允許投票**

   如果選中，則允許對某個想法的注釋進行投票。 未選中預設值。

* **允許使用者刪除評論和主題**

   如果選中，則允許成員刪除他們發佈的注釋和想法。 未選中預設值。

* **允許關注**

   如果選中，則包括下列概念帖子功能，允許成員 [通知](/help/communities/notifications.md) 新職位。 未選中預設值。

* **允許電子郵件訂閱**

   如果選中，則允許通過電子郵件通知成員新帖子([訂閱](/help/communities/subscriptions.md))。 需要 `Allow Following` 要檢查和 [電子郵件配置](/help/communities/email.md)。 未選中預設值。

* **允許投票**

   如果選中，則允許對某個想法的注釋進行投票。 未選中預設值。

* **顯示徽章**

   如果選中，則顯示已獲得和已分配 [徽章](/help/communities/implementing-scoring.md) 會員的想法。 未選中預設值。

* **不在清單頁上獲取答復**

* **允許主要內容**

   如果選中，該思想可被識別為 [特色內容](/help/communities/featured.md)。 未選中預設值。

* **啟用提及功能**
* **最大提及數**
* **UI 提及模式**

#### 「用戶審核」頁籤 {#user-moderation-tab}

在 **[!UICONTROL 用戶審核]** 頁籤，指定如何管理已發佈的想法和注釋（用戶生成的內容）。 有關詳細資訊，請參見 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

* **拒絕帖子**

   如果選中，則允許受信任的成員審核人拒絕帖子並阻止帖子出現在公共論壇中。 未選中預設值。

* **關閉/重新開啟主題**

   如果選中，受信任的成員審閱人可以關閉主題以進一步編輯和注釋，也可以重新開啟主題。 未選中預設值。

* **標誌帖子**

   如果選中，允許成員將其他主題或注釋標籤為不恰當。 未選中預設值。

* **標誌原因清單**

   如果選中，則允許成員從下拉清單中選擇將主題或注釋標籤為不適當的原因。 未選中預設值。

* **自定義標誌原因**

   如果選中，允許成員輸入將主題或注釋標籤為不適當的自己原因。 未選中預設值。

* **審核閾值**

   輸入在通知審閱人之前必須由成員標籤主題或評論的次數。 預設值為1（一次）。

* **標籤限制**

   輸入主題或注釋在隱藏於公共視圖之前必須標籤的次數。 如果設定為–1，則標籤的主題或注釋永遠不會隱藏在公共視圖中。 否則，此數字必須大於或等於「審核閾值」。 預設值為5。

#### 「標籤」欄位頁籤 {#tag-field-tab}

在 **[!UICONTROL 標籤欄位]** 頁籤，如果允許，可應用的標籤 **[!UICONTROL 設定]** 頁籤，根據選擇的命名空間進行限制。

* **允許的命名空間**

   相關(如果 `Allow Tagging` 在 **[!UICONTROL 設定]** 頁籤。 可應用的標籤僅限於所檢查的命名空間類別中的標籤。 命名空間清單包括「標準標籤」（預設命名空間）和「包括所有標籤」。 預設值未選中，這意味著允許所有命名空間。

* **建議限制**

   輸入要作為對論壇成員過帳的建議顯示的標籤數。 值 **-1** 意味著沒有限制。 預設值為0。

#### 「排序設定」頁籤 {#sort-settings-tab}

在 **[!UICONTROL 排序設定]** 頁籤，指定在顯示已過帳注釋時如何排序。

* **排序方式**

   檢查所有允許的排序選擇： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`。 預設值為 `Newest, Oldest, Last Updated`。

* **設為預設值**

   下拉以選擇一個選中的排序選項作為預設值顯示。 預設值為 `Newest`。

* **選取 Analytics 排序的時間選項**

   下拉以選擇其中一個 `All, Last 24 Hours, Last 7 Days, Last 30 Days`。 預設值為 `All`。

## 站點訪問者體驗 {#site-visitor-experience}

### 建立思想 {#creating-idea}

與所有社區功能一樣，如果未登錄，站點訪問者只能閱讀觀點並查看其他意見（通過評論和投票/喜歡）。

登錄後，成員可以建立新想法。

![建立新思想](assets/create-new-idea.png)

在提交想法之前，成員可以保存草稿。

通過選擇 `Save as Draft` 按鈕。

![保存思想](assets/save-idea.png)

在 `My Drafts` 頁籤 `Read More` 要重新進入編輯模式：

![編輯思想](assets/edit-idea.png)

#### 提供反饋 {#providing-feedback}

一旦發佈該想法，其他成員就可以登錄並開啟該想法( `Read More`)，像這樣加票，發表意見。

![反饋](assets/feedback-idea.png)

### 其他資訊 {#additional-information}

有關 [Ideation Essentials](/help/communities/ideation.md) 頁面。

有關已發佈主題和評論的審核，請參閱 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

有關為已發佈主題和注釋添加標籤，請參見 [標籤用戶生成的內容](/help/communities/tag-ugc.md)。
