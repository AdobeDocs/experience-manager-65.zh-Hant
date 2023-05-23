---
title: 日曆功能
seo-title: Calendar Feature
description: 以日曆格式提供社區事件資訊
seo-description: Provides community event information in a calendar format
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 5%

---

# 日曆功能 {#calendar-feature}

## 簡介 {#introduction}

日曆功能支援以日曆格式向所有站點訪問者或僅登錄站點訪問者（社區成員）提供社區事件資訊，而只有授權成員可以添加事件。

文檔的本節介紹

* 將日曆功能添加到站AEM點
* 配置設定 `Calendar` 元件

## 將日曆添加到頁面 {#adding-a-calendar-to-a-page}

添加 `Calendar` 在作者模式下對頁面的元件，使用元件瀏覽器查找

* `Communities / Calendar`

並將其拖到頁面上，如相對於要供用戶查看的功能的位置。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

當 [所需的客戶端庫](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) 包括，這是 `Calendar` 元件。

![日曆元件](assets/calendar-component.png)

### 配置日曆 {#configuring-calendar}

選取已放置的 `Calendar` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

![配置日曆](assets/configure-calendar1.png)

#### 「設定」頁籤 {#settings-tab}

在 **設定** 頁籤，指定是否允許將標籤應用於日曆條目。

* **每個頁面的事件**

   定義每頁顯示的事件數。 預設值為10。

* **已審核**

   如果選中，則必須先批准日曆事件和注釋的發佈，然後才會將其顯示在發佈站點上。 未選中預設值。

* **已關閉**

   如果選中，則日曆將關閉到新事件條目和注釋。 未選中預設值。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入日曆事件和注釋。 選中預設值。

* **允許標記**

   如果選中，允許成員將標籤標籤添加到他們發佈的事件(請參見 **標籤欄位** )的正平方根。 選中預設值。

* **允許檔案上傳**

   如果選中，則允許將檔案附件添加到日曆事件或注釋中。 選中預設值。

* **允許關注**

   如果選中，允許成員跟蹤發佈到日曆的事件。 選中預設值。

* **最大檔案大小**

   僅在 `Allow File Uploads` 的子菜單。 此欄位將限制上載檔案的大小（以位元組為單位）。 預設為104857600(10 Mb)。

* **允許的檔案類型**

   僅在 `Allow File Uploads` 的子菜單。 以逗號分隔的檔案副檔名清單，其中帶有「點」分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許上載未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **附加影像檔案最大大小**

   僅當選中「允許檔案上載」時相關。 上載的影像檔案可能具有的最大位元組數。 預設值為2097152** **(2 Mb)。

* **允許的封面影像類型**

   影像檔案副檔名的逗號分隔清單，其中「點」分隔符。 預設值為 `.jpg,.jpeg,.png,.gif,.bmp`。

* **允許執行緒式回覆**

   如果選中，則允許對發佈到日曆事件的注釋進行答復。 選中預設值。

* **允許使用者刪除評論和事件**

   如果選中，則允許成員刪除其發佈的注釋和日曆事件。 預設值為** **選中。

* **允許投票**

   如果選中，則將「投票」功能與日曆事件一起包含。 選中預設值。

* **顯示階層連結**

   在事件頁面上顯示階層連結. 選中預設值。

* **日期範圍篩選**

   定義添加到當前日期的天數，以便計算日曆事件清單頁篩選器的「至」值。 預設數字為30。

* **允許主要內容**

   如果選中，該思想可被識別為 [特色內容](/help/communities/featured.md)。 未選中預設值。

在 **用戶審核** 頁籤，指定如何管理已發佈的主題和回復（用戶生成的內容）。 有關詳細資訊，請參見 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

#### 「用戶審核」頁籤 {#user-moderation-tab}

* **拒絕帖子**

   如果選中，則允許受信任的成員審核人拒絕帖子並阻止帖子出現在公共論壇中。 選中預設值。

* **關閉 / 重新開啟事件**

   如果選中，受信任的成員審閱人可以關閉事件以進一步編輯和注釋，也可以重新開啟事件。 選中預設值。

* **標誌帖子**

   如果選中，允許成員將其他事件或注釋標籤為不恰當。 選中預設值。

* **標誌原因清單**

   如果選中，則允許成員從下拉清單中選擇將事件或注釋標籤為不適當的原因。 未選中預設值。

* **自定義標誌原因**

   如果選中，允許成員輸入將事件或注釋標籤為不適當的自己原因。 未選中預設值。

* **審核閾值**

   輸入在通知審閱人之前必須由成員標籤事件或評論的次數。 預設值為1（一次）。

* **標籤限制**

   輸入事件或注釋在隱藏於公共視圖之前必須標籤的次數。 如果設定為–1，則標籤的主題或注釋永遠不會隱藏在公共視圖中。 否則，此數字必須大於或等於「審核閾值」。 預設值為5。

#### 「標籤」欄位頁籤 {#tag-field-tab}

在 **標籤欄位** 頁籤，如果允許，可應用的標籤 **設定** 頁籤，根據選擇的命名空間進行限制。

* **允許的命名空間**

   相關(如果 `Allow Tagging` 在 **設定** 頁籤。 可應用的標籤僅限於所檢查的命名空間類別中的標籤。 命名空間清單包括「標準標籤」（預設命名空間）和「包括所有標籤」。 預設值未選中，這意味著允許所有命名空間。

* **建議限制**

   輸入要作為對論壇成員過帳的建議顯示的標籤數。 預設值為**-**1（無限制）。

>[!NOTE]
>
>訪問 [管理標籤](/help/sites-administering/tags.md) 瞭解如何添加新標籤命名空間（分類）。

#### 翻譯頁籤 {#translation-tab}

在 **翻譯** 頁籤，如果為社區站點啟用了翻譯，則可以設定翻譯以翻譯整個線程（事件和注釋），而不是翻譯特定帖子。

* **全部轉換**

   如果選中，則事件和注釋將翻譯為用戶的首選語言。 選中預設值。

## 站點訪問者體驗 {#site-visitor-experience}

在發佈環境中，日曆功能將顯示一個搜索欄位，其中包含預設日期範圍以及該範圍內的任何日曆事件。

選擇日曆事件時，將顯示日曆事件詳細資訊、說明和注釋。

其他能力取決於站點訪問者是版主、管理員、社區成員、特權成員還是匿名。

### 審閱人和管理員 {#moderators-and-administrators}

當登錄用戶具有版主或管理員權限時，他們能夠執行 [緩和任務](/help/communities/moderate-ugc.md) （元件配置允許）上所有日曆事件和發佈到事件的注釋。

![版主視圖](assets/moderators-view.png)

#### 成員 {#members}

當登錄用戶是社區成員或 [特權成員](/help/communities/users.md#privileged-members-group) （視配置而定），他們可以選擇 `New Event` 建立和發佈新日曆事件。

具體而言，它們可：

* 建立新日曆事件
* 將注釋發佈到日曆事件
* 編輯自己的日曆事件或注釋
* 刪除其自己的日曆事件或注釋
* 標籤其他日曆事件或注釋

![建立事件](assets/configure-calendar2.png)

![事件後](assets/configure-calendar3.png)

#### 匿名 {#anonymous}

未登錄的站點訪問者只能閱讀已發佈的日曆事件，如果支援，可翻譯這些事件，但不能添加事件或評論，也不能標籤其他事件或評論。

![匿名用戶視圖](assets/anonymous-user-view1.png)

## 其他資訊 {#additional-information}

有關 [日曆要件](/help/communities/calendar-basics-for-developers.md) 頁面。

有關日曆事件和注釋的審核，請參閱 [調節用戶生成的內容](/help/communities/moderate-ugc.md)。

有關為日曆事件和注釋添加標籤，請參見 [標籤用戶生成的內容](/help/communities/tag-ugc.md)。

有關日曆事件和注釋的翻譯，請參閱 [翻譯用戶生成的內容](/help/communities/translate-ugc.md)。
