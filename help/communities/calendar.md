---
title: 行事曆功能
description: 瞭解行事曆功能如何以行事曆格式提供社群活動資訊。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# 行事曆功能 {#calendar-feature}

## 簡介 {#introduction}

行事曆功能支援以行事曆格式提供社群事件資訊給所有網站訪客或僅登入網站訪客（社群成員），而只有授權成員才能新增事件。

本檔案的此章節說明

* 將行事曆功能新增到AEM網站
* 的組態設定 `Calendar` 元件

## 新增行事曆至頁面 {#adding-a-calendar-to-a-page}

若要新增 `Calendar` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Calendar`

並將其拖曳到頁面上某個位置，例如與功能相對的位置以供使用者檢閱。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) 包含，這就是 `Calendar` 元件出現。

![calendar-component](assets/calendar-component.png)

### 設定日曆 {#configuring-calendar}

選取已放置的 `Calendar` 元件供您存取及選取 `Configure` 圖示可開啟編輯對話方塊。

![設定](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### 設定標籤 {#settings-tab}

在 **設定** 標籤，指定是否允許將標籤套用至行事曆專案。

* **每頁事件數**

  定義每個頁面顯示的事件數。 預設值為10。

* **已稽核**

  如果勾選，行事曆事件和註解的張貼必須先經過核准，才會出現在發佈網站上。 預設為未勾選。

* **已關閉**

  如果勾選，則行事曆將對新事件專案和註解關閉。 預設為未勾選。

* **RTF編輯器**

  如果勾選，則可使用標示輸入行事曆事件和註解。 預設為已核取。

* **允許標籤**

  如果勾選，則允許成員將標籤新增至他們張貼的事件(請參閱 **標籤欄位** 標籤)。 預設為已核取。

* **允許檔案上傳**

  如果勾選，允許將檔案附件新增至行事曆事件或註解。 預設為已核取。

* **允許關注**

  如果勾選，則允許成員關注發佈至行事曆的事件。 預設為已核取。

* **檔案大小上限**

  只有在 `Allow File Uploads` 已勾選。 此欄位會限制已上傳檔案的大小（以位元組為單位）。 預設值為104857600 (10 Mb)。

* **允許的檔案型別**

  只有在 `Allow File Uploads` 已勾選。 以「點」分隔符號的副檔名清單（以逗號分隔）。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何檔案型別，則無法上傳未指定的檔案型別。 預設為「無」，因此允許所有檔案型別。

* **附加影像檔案大小上限**

  只有在勾選「允許檔案上傳」時才相關。 已上傳影像檔案的最大位元組數。 預設值為2097152** **(2 Mb)。

* **允許的封面影像型別**

  以「點」分隔符號的影像副檔名清單（以逗號分隔）。 預設為 `.jpg,.jpeg,.png,.gif,.bmp`.

* **允許執行緒式回覆**

  如果勾選，則允許回覆發佈至行事曆事件的評論。 預設為已核取。

* **允許使用者刪除評論和事件**

  如果勾選，則允許成員刪除他們張貼的評論和行事曆事件。 預設為已核取。

* **允許投票**

  如果勾選，請將「投票」功能與行事曆事件包含在內。 預設為已核取。

* **顯示階層連結**

  在事件頁面上顯示階層連結。 預設為已核取。

* **日期範圍篩選**

  定義新增至目前日期的天數，以計算列於頁面篩選之行事曆事件的「結束日期」值。 預設數字為30。

* **允許主要內容**

  如果勾選，該創意可識別為 [主要內容](/help/communities/featured.md). 預設為未勾選。

在 **使用者稽核** 索引標籤，指定如何管理張貼的主題和回覆（使用者產生的內容）。 如需詳細資訊，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

#### 「使用者稽核」標籤 {#user-moderation-tab}

* **拒絕貼文**

  如果勾選，受信任的成員版主可以拒絕貼文，並防止貼文出現在公開論壇上。 預設為已核取。

* **關閉/重新開啟事件**

  如果勾選，受信任的成員版主可以關閉事件以進一步編輯和註釋，也可以重新開啟事件。 預設為已核取。

* **標幟帖子**

  如果勾選，則允許成員將其他人的活動或評論標籤為不適當。 預設為已核取。

* **標幟原因清單**

  如果勾選，則允許成員從下拉式清單中選擇標幟事件或評論為不適當的原因。 預設為未勾選。

* **自訂標幟原因**

  如果勾選，則允許成員輸入將事件或評論標幟為不適當的原因。 預設為未勾選。

* **稽核臨界值**

  輸入通知版主前，事件或評論必須由成員標幟的次數。 預設值為1 （一次）。

* **標幟限制**

  輸入事件或註解在隱藏於公眾檢視前必須加上標籤的次數。 如果設為–1，則標幟的主題或註解絕不會從公開檢視中隱藏。 否則，此數字必須大於或等於「稽核臨界值」。 預設值為5。

#### 標籤欄位索引標籤 {#tag-field-tab}

在 **標籤欄位** 標籤中，如果允許的話，則會套用的標籤 **設定** 索引標籤中，會根據選取的名稱空間而有所限制。

* **允許的名稱空間**

  相關條件 `Allow Tagging` 已勾選下方的 **設定** 標籤。 可套用的標籤僅限於已核取的名稱空間類別中的標籤。 名稱空間清單包含「標準標籤」（預設名稱空間）和「包含所有標籤」。 預設為未勾選，這表示允許所有名稱空間。

* **建議限制**

  輸入要顯示為論壇成員張貼建議之標籤數目。 預設值為**-**1 （無限制）。

>[!NOTE]
>
>造訪 [管理標籤](/help/sites-administering/tags.md) 您可以在此處瞭解如何新增標籤名稱空間（分類法）。

#### 翻譯索引標籤 {#translation-tab}

在 **翻譯** 索引標籤中，如果社群網站已啟用翻譯，則可將翻譯設定為翻譯整個對話串（事件和評論），而非特定貼文。

* **全部翻譯**

  如果勾選，事件和註解會轉換為使用者偏好的語言。 預設為已核取。

## 網站訪客體驗 {#site-visitor-experience}

在發佈環境中，行事曆功能會顯示具有預設日期範圍的搜尋欄位，以及屬於該範圍的任何行事曆事件。

選取行事曆事件時，會顯示行事曆事件詳細資訊、說明和註解。

其他功能取決於網站訪客是版主、管理員、社群成員、有特殊許可權的成員或匿名。

### 版主和管理員 {#moderators-and-administrators}

當登入使用者具有版主或管理員許可權時，他們就可以執行 [稽核任務](/help/communities/moderate-ugc.md) （如元件的設定所允許）發佈至事件之所有日曆事件和評論上的事件。

![版主 — 檢視](assets/moderators-view.png)

#### 成員 {#members}

當登入使用者是社群成員或 [有特殊許可權的成員](/help/communities/users.md#privileged-members-group) （視設定而定），他們可以選取 `New Event` 建立和張貼新的行事曆事件。

具體而言，他們可能：

* 建立日曆事件
* 發表評論至行事曆事件
* 編輯他們自己的行事曆事件或評論
* 刪除自己的行事曆事件或評論
* 標幟其他人的行事曆活動或評論

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### 匿名 {#anonymous}

未登入的網站訪客只能讀取張貼的行事曆事件，並在支援時進行翻譯，但不得新增事件或評論，亦不得標示其他人的事件或評論。

![anonymous-user-view](assets/anonymous-user-view1.png)

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [行事曆要點](/help/communities/calendar-basics-for-developers.md) 開發人員頁面。

如需行事曆活動和評論的稽核資訊，請參閱 [稽核使用者產生的內容](/help/communities/moderate-ugc.md).

若要標籤行事曆事件和註解，請參閱 [標籤使用者產生的內容](/help/communities/tag-ugc.md).

如需日曆事件和註解的翻譯，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).
