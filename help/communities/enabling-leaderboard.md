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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 排行榜功能{#leaderboard-feature}

## 簡介 {#introduction}

該 `Leaderboard` 元件通過根據獲得的點數（基本分數）或其專業知識（高級分數）對成員進行排名，從而獲得成員在社區內如何交互的感知。

在將排行榜元件包括在頁面之前，必須配置社 [區評分和標章](/help/communities/implementing-scoring.md)。

本節說明

* 將元件 `Leaderboard` 添加到社 [區站點](/help/communities/overview.md#community-sites)
* 元件的配置設 `Leaderboard` 置

### 新增排行榜至頁面 {#adding-a-leaderboard-to-a-page}

若要在作 `Leaderboard` 者模式下將元件新增至頁面，請找出元件

* `Communities / Leaderboard`

並將它拖曳至頁面上的位置。

如需必要資訊，請造 [訪Communities Components Basics](/help/communities/basics.md)。

首次放置在社群網站頁面時，元件的顯示方式如下：

![chlimage_1-19](assets/chlimage_1-19.png)

### 配置排行榜 {#configuring-leaderboard}

選擇要訪問 `Leaderboard` 的已放置元件，並選 `Configure` 擇開啟編輯對話框的表徵圖。

![chlimage_1-20](assets/chlimage_1-20.png) ![chlimage_1-21](assets/chlimage_1-21.png)

#### 「設定」頁籤 {#settings-tab}

在**設定**頁籤下，指定將顯示與成員相關的資訊：

* **顯示名稱**

   用於顯示展示板的描述性名稱，反映為顯示標章和分數所選取的規則。
如果未輸 `Leaderboard`入任何內容，則預設為。

* **徽章**

   如果勾選，則排行榜中會包含標誌圖示的欄。
預設為未勾選。

* **徽章名稱**

   如果選中此選項，則標誌名稱的列將包括在排行榜中。
預設為未勾選。

* **使用頭像**

   如果勾選，成員的頭像影像將包含在排行榜中，位於其成員配置檔案的名稱連結旁邊。
預設為未勾選。

#### 規則標籤 {#rules-tab}

在「規 **則** 」索引標籤下，社群網站及其計分和標籤規則

* **規則位置**

   （必要）設定計分／簽章規則的位置。

* **得分規則**

   （必要）產生要顯示的分數的特定規則。

* **徽章規則**

   （必要）產生要顯示之標章的特定規則。

* **顯示限制**

   每頁要顯示的成員數。

   預設值為10。

### 範例：參與者領導委員會 {#example-participants-leaderboard}

此排行榜會報告套用基本計分規則的結果。

Leerboard元件組態：

* 「設定」頁籤：

   * 顯示名稱 = `Participation Board`
   * `checked`:

      * 徽章
      * 徽章名稱
      * 使用頭像

* 規則標籤：

   * 規則位置 = `/content/sites/communities/jcr:content`
   * 得分規則 = `/etc/community/scoring/rules/forums-scoring`
   * 徽章規則 = `/etc/community/badging/rules/reference-badging`
   * 顯示限制 = `10`

![chlimage_1-22](assets/chlimage_1-22.png)

### 範例：專家排行榜 {#example-experts-leaderboard}

此排行榜會報告套用進階計分規則的結果。

Leerboard元件組態：

* 「設定」頁籤：

   * 顯示名稱 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用頭像

* 規則標籤：

   * 規則位置 = `/content/sites/communities/jcr:content`
   * 得分規則 = `/etc/community/scoring/rules/adv-forums-scoring`
   * 徽章規則 = `/etc/community/badging/rules/adv-forums-badging`
   * 顯示限制 = `10`

![chlimage_1-23](assets/chlimage_1-23.png)

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人 [員的Leaderboard](/help/communities/leaderboard.md) Essentials頁面。

管理員的「社群計分與標章」頁面 [中提供建立規則的指示](/help/communities/implementing-scoring.md) 。
