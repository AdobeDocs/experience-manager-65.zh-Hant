---
title: 日曆功能
seo-title: 日曆功能
description: 以日曆格式提供社群活動資訊
seo-description: 以日曆格式提供社群活動資訊
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
source-wordcount: '1170'
ht-degree: 5%

---

# 日曆功能{#calendar-feature}

## 簡介 {#introduction}

日曆功能支援以日曆格式向所有網站訪客或僅登錄網站訪客（社群成員）提供社群事件資訊，而只有授權的成員才能添加事件。

本檔案的本節說明

* 新增日曆功能至AEM網站
* `Calendar`元件的組態設定

## 將日曆添加到頁{#adding-a-calendar-to-a-page}

若要在製作模式中將`Calendar`元件新增至頁面，請使用元件瀏覽器來找出

* `Communities / Calendar`

並將其拖曳至頁面上的位置，例如與功能相對的位置，供使用者檢閱。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

包含[必要的用戶端程式庫](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side)時，會以此方式顯示`Calendar`元件。

![日曆元件](assets/calendar-component.png)

### 配置日曆{#configuring-calendar}

選取要存取的放置`Calendar`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### 設定頁簽{#settings-tab}

在&#x200B;**設定**&#x200B;標籤下，指定是否允許將標籤應用於日曆條目。

* **每個頁面的事件**

   定義每頁顯示的事件數。 預設為10。

* **已審核**

   如果勾選此選項，發佈日曆事件和留言之前必須先獲得核准，才會出現在發佈網站上。 預設為未勾選。

* **已關閉**

   如果選中，日曆將關閉為新事件條目和注釋。 預設為未勾選。

* **RTF 編輯器**

   如果選中，則可以使用標籤輸入日曆事件和注釋。 已勾選預設值。

* **允許標記**

   如果選中此選項，則允許成員將標籤標籤添加到他們發佈的事件（請參閱&#x200B;**標籤欄位**&#x200B;頁簽）。 已勾選預設值。

* **允許檔案上傳**

   如果選中此選項，則允許將檔案附件添加到日曆事件或注釋中。 已勾選預設值。

* **允許關注**

   如果選中此選項，則允許成員遵循發佈到日曆的事件。 已勾選預設值。

* **最大檔案大小**

   僅當檢查`Allow File Uploads`時相關。 此欄位將限制上傳檔案的大小（以位元組為單位）。 預設為104857600(10 Mb)。

* **允許的檔案類型**

   僅當檢查`Allow File Uploads`時相關。 副檔名清單（以逗號分隔）以「點」分隔。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案類型，則不允許上載未指定的檔案類型。 未指定預設值，因此允許所有檔案類型。

* **附加影像檔案最大大小**

   僅在勾選「允許檔案上傳」時相關。 上傳的影像檔案可能具有的最大位元組數。 預設為2097152** **(2 Mb)。

* **允許的封面影像類型**

   以逗號分隔的影像副檔名清單，以「點」分隔符號。 預設值為`.jpg,.jpeg,.png,.gif,.bmp`。

* **允許執行緒式回覆**

   如果選中，則允許對張貼到日曆事件的評論進行回覆。 已勾選預設值。

* **允許使用者刪除評論和事件**

   如果選中此選項，則允許成員刪除他們發佈的評論和日曆事件。 預設為** **勾選。

* **允許投票**

   如果勾選此選項，請加入日曆事件的「投票」功能。 已勾選預設值。

* **顯示階層連結**

   在事件頁面上顯示階層連結. 已勾選預設值。

* **日期範圍篩選**

   定義新增至目前日期的天數，以計算日曆事件清單頁面篩選器的「結束日期」值。 預設數字為30。

* **允許主要內容**

   若勾選，可將構想識別為[精選內容](/help/communities/featured.md)。 預設為未勾選。

在&#x200B;**使用者協調**&#x200B;標籤下，指定如何管理已張貼的主題和回覆（使用者產生的內容）。 如需詳細資訊，請參閱[協調使用者產生的內容](/help/communities/moderate-ugc.md)。

#### 使用者協調標籤{#user-moderation-tab}

* **拒絕貼文**

   若勾選此選項，信任的成員協調者將可拒絕貼文，並防止貼文出現在公開論壇上。 已勾選預設值。

* **關閉 / 重新開啟事件**

   如果選中，受信任的成員協調者可以關閉事件以進一步編輯和注釋，也可以重新開啟事件。 已勾選預設值。

* **標幟貼文**

   如果選中，則允許成員將其他事件或評論標籤為不適當。 已勾選預設值。

* **標誌原因清單**

   如果選中，則允許成員從下拉清單中選擇其標籤事件或注釋為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

   如果選中，則允許成員輸入自己的原因，以標籤事件或注釋不適當。 預設為未勾選。

* **協調臨界值**

   輸入在通知協調者之前，成員必須標籤事件或留言的次數。 預設為1（一次）。

* **標幟限制**

   輸入在從公開檢視隱藏事件或留言之前，必須加以標籤的次數。 如果設為–1，則標籤的主題或評論永遠不會在公共視圖中隱藏。 否則，此數字必須大於或等於協調臨界值。 預設為5。

#### 標籤欄位標籤{#tag-field-tab}

在&#x200B;**標籤欄位**&#x200B;標籤下，如果&#x200B;**設定**&#x200B;標籤下允許，則可以套用的標籤會根據所選的命名空間受到限制。

* **允許的命名空間**

   若已在&#x200B;**Settings**&#x200B;標籤下勾選`Allow Tagging`則相關。 可套用的標籤僅限於所檢查命名空間類別中的標籤。 命名空間清單包含「標準標籤」（預設命名空間）以及「包含所有標籤」。 預設值未勾選，這表示允許所有命名空間。

* **建議限制**

   輸入要作為建議顯示給論壇成員的標籤數。 預設為**-**1（無限制）。

>[!NOTE]
>
>請造訪[管理標籤](/help/sites-administering/tags.md)，了解如何新增標籤命名空間（分類法）。

#### 翻譯標籤{#translation-tab}

在&#x200B;**Translation**&#x200B;標籤下，如果為社群網站啟用了翻譯，則可以設定翻譯來翻譯整個執行緒（事件和留言），而不是特定貼文。

* **全部轉換**

   若勾選此選項，則事件和留言會翻譯成使用者偏好的語言。 已勾選預設值。

## 網站訪客體驗{#site-visitor-experience}

在發佈環境中，日曆功能會顯示一個搜尋欄位，其中包含預設的日期範圍，以及任何落在該範圍內的日曆事件。

選取日曆事件時，會顯示日曆事件詳細資訊、說明和備注。

其他功能取決於網站訪客是版主、管理員、社群成員、有權限的成員還是匿名。

### 協調者和管理員{#moderators-and-administrators}

當登入的使用者擁有版主或管理員權限時，他們就能對發佈至事件的所有日曆事件和留言執行[仲裁任務](/help/communities/moderate-ugc.md)（元件的設定允許）。

![協調者檢視](assets/moderators-view.png)

#### 成員 {#members}

當登入的用戶是社區成員或[特權成員](/help/communities/users.md#privileged-members-group)時（取決於配置），他們可以選擇`New Event`建立並發佈新日曆事件。

具體而言，他們可以：

* 建立新的日曆事件
* 將留言張貼至日曆事件
* 編輯自己的日曆事件或注釋
* 刪除自己的日曆事件或注釋
* 標幟其他人的日曆事件或留言

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### 匿名 {#anonymous}

未登入的網站訪客只能閱讀已張貼的日曆事件、翻譯這些事件（如有支援），但不得新增事件或留言，也不得標籤其他人的事件或留言。

![anonymous-user-view](assets/anonymous-user-view1.png)

## 其他資訊 {#additional-information}

開發人員可在[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)頁面上找到更多資訊。

如需日曆事件和留言的協調，請參閱[協調使用者產生的內容](/help/communities/moderate-ugc.md)。

有關標籤日曆事件和注釋的資訊，請參閱[標籤用戶生成的內容](/help/communities/tag-ugc.md)。

有關日曆事件和注釋的轉換，請參閱[轉換用戶生成的內容](/help/communities/translate-ugc.md)。
