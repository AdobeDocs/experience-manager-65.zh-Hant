---
title: 排行榜功能
seo-title: Leaderboard Feature
description: 將排行榜元件添加到頁面
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# 排行榜功能 {#leaderboard-feature}

## 簡介 {#introduction}

的 `Leaderboard` 元件提供了通過根據所得分數（基本評分）或其專業知識（高級評分）對成員進行排名來瞭解成員在社區內如何交互的能力。

在將排行榜元件包含在頁面之前，必須配置 [社區評分和徽章](/help/communities/implementing-scoring.md)。

文檔的本節介紹：

* 添加 `Leaderboard` 元件 [社區站點](/help/communities/overview.md#community-sites)。
* 的配置設定 `Leaderboard` 元件。

### 將排行榜添加到頁面 {#adding-a-leaderboard-to-a-page}

添加 `Leaderboard` 在作者模式下將元件定位到頁面

* `Communities / Leaderboard`

然後拖到頁面上。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

首次放置在社區站點的頁面上時，元件的顯示方式如下：

![領導](assets/leaderboard.png)

### 配置排行榜 {#configuring-leaderboard}

選取已放置的 `Leaderboard` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置 — 新建](assets/configure-new.png)

![配置領導板](assets/configure-leaderboard.png)

#### 「設定」頁籤 {#settings-tab}

在 **[!UICONTROL 設定]** 頁籤，指定顯示與成員相關的資訊：

* **顯示名稱**

   用於顯示主板的描述性名稱，反映為顯示徽章和分數而選擇的規則。
預設值為 `Leaderboard`，則不輸入。

* **徽章**

   如果選中，則標籤表徵圖的列將包括在排行榜中。
未選中預設值。

* **徽章名稱**

   如果選中，則標籤名稱的列將包括在排行榜中。
未選中預設值。

* **使用虛擬形象**

   如果選中，成員的虛擬形象影像將包含在排行榜中，位於其成員配置檔案的名稱連結旁邊。
未選中預設值。

#### 「規則」頁籤 {#rules-tab}

在 **規則** 頁籤、社區網站及其評分和標籤規則

* **規則位置**

   （必需）配置「評分/簽名」規則的位置。

* **得分規則**

   （必需）生成要顯示的分數的特定規則。

* **徽章規則**

   （必需）生成要顯示的徽章的特定規則。

* **顯示限制**

   每頁要顯示的成員數。預設值為10。

### 示例：參加者領導委員會 {#example-participants-leaderboard}

此排行榜報告應用基本評分規則的結果。

排行榜元件配置：

* 設定頁籤：

   * 顯示名稱 = `Participation Board`
   * `checked`:

      * 徽章
      * 徽章名稱
      * 使用虛擬形象

* 規則頁籤：

   * 規則位置 = `/content/sites/<site name>/jcr:content`
   * 得分規則 = `/libs/settings/community/scoring/rules/forums-scoring`
   * 徽章規則 = `/libs/settings/community/badging/rules//reference-badging`
   * 顯示限制 = `10`

![參與者領導委員會](assets/participants-leaderboard.png)

### 示例：專家領導委員會 {#example-experts-leaderboard}

此排行榜會報告應用高級評分規則後的結果。

排行榜元件配置：

* 設定頁籤：

   * 顯示名稱 = `Expertise Board`
   * `checked`:

      * 徽章
      * 使用虛擬形象

* 規則頁籤：

   * 規則位置 = `/content/sites/<site name>/jcr:content`
   * 得分規則 = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * 徽章規則 = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 顯示限制 = `10`

![專家領導委員會](assets/experts-leaderboard.png)

### 其他資訊 {#additional-information}

有關 [排行榜要點](/help/communities/leaderboard.md) 頁面。

有關建立規則的說明，請參見 [社區評分和徽章](/help/communities/implementing-scoring.md) 頁面。
