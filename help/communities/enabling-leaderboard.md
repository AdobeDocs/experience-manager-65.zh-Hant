---
title: 排行榜功能
seo-title: 排行榜功能
description: 將Leaderboard元件添加到頁面
seo-description: 將Leaderboard元件添加到頁面
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 9%

---


# 排行榜功能{#leaderboard-feature}

## 簡介 {#introduction}

`Leaderboard`元件可根據獲得的點數（基本分數）或其專業知識（進階分數）對成員進行排名，以獲得成員在社群內互動的感覺。

在將排行榜元件包括在頁面之前，必須配置[社群評分和標章](/help/communities/implementing-scoring.md)。

本檔案章節說明：

* 將`Leaderboard`元件添加到[社區站點](/help/communities/overview.md#community-sites)。
* `Leaderboard`元件的配置設定。

### 將排行榜添加到頁面{#adding-a-leaderboard-to-a-page}

若要在作者模式下將`Leaderboard`元件新增至頁面，請找出該元件

* `Communities / Leaderboard`

並將它拖曳至頁面上的位置。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

首次放置在社群網站頁面時，元件的顯示方式如下：

![領導者](assets/leaderboard.png)

### 配置Leaderboard {#configuring-leaderboard}

選擇要訪問的已放置的`Leaderboard`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![configure-new](assets/configure-new.png)

![配置排行榜](assets/configure-leaderboard.png)

#### 「設定」頁籤{#settings-tab}

在&#x200B;**[!UICONTROL Settings]**&#x200B;標籤下，指定顯示與成員相關的資訊：

* **顯示名稱**

   用於顯示展示板的描述性名稱，反映為顯示標章和分數所選取的規則。
預設值為`Leaderboard`，如果未輸入。

* **徽章**

   如果勾選，則排行榜中會包含標誌圖示的欄。
預設為未勾選。

* **徽章名稱**

   如果選中此選項，則標誌名稱的列將包括在排行榜中。
預設為未勾選。

* **使用頭像**

   如果勾選，成員的頭像影像將包含在排行榜中，位於其成員配置檔案的名稱連結旁邊。
預設為未勾選。

#### 規則標籤{#rules-tab}

在&#x200B;**規則**&#x200B;標籤下，社群網站及其計分和標籤規則

* **規則位置**

   （必要）設定計分／簽章規則的位置。

* **得分規則**

   （必要）產生要顯示的分數的特定規則。

* **徽章規則**

   （必要）產生要顯示的徽章的特定規則。

* **顯示限制**

   每頁要顯示的成員數。預設值為10。

### 範例：參與者排行榜{#example-participants-leaderboard}

此排行榜會報告套用基本計分規則的結果。

Leaderboard元件配置：

* 「設定」頁籤：

   * 顯示名稱 = `Participation Board`
   * `checked`:

      * 徽章
      * 徽章名稱
      * 使用頭像

* 規則標籤：

   * 規則位置 = `/content/sites/<site name>/jcr:content`
   * 得分規則 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 徽章規則 = `/libs/settings/community/badging/rules//reference-badging`
   * 顯示限制 = `10`

![參與者領導委員會](assets/participants-leaderboard.png)

### 範例：專家排行榜{#example-experts-leaderboard}

此排行榜會報告套用進階計分規則的結果。

Leaderboard元件配置：

* 「設定」頁籤：

   * 顯示名稱 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用頭像

* 規則標籤：

   * 規則位置 = `/content/sites/<site name>/jcr:content`
   * 得分規則 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 徽章規則 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 顯示限制 = `10`

![專家領導委員會](assets/experts-leaderboard.png)

### 其他資訊 {#additional-information}

有關詳細資訊，請參閱開發人員的[ Leaderboard Essentials](/help/communities/leaderboard.md)頁。

管理員可在[Communities Scoring and Badges](/help/communities/implementing-scoring.md)頁面上提供建立規則的指示。
