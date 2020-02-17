---
title: 即時副本概述主控台
seo-title: 即時副本概述主控台
description: 瞭解即時副本概觀主控台的基本資訊。
seo-description: 瞭解即時副本概觀主控台的基本資訊。
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 即時副本概述主控台{#live-copy-overview-console}

即時 **副本概述** ，可讓您：

* 檢視／管理整個網站的繼承：

   * 檢視藍圖樹和對應的即時副本結構，以及其繼承狀態
   * 更改繼承狀態；例如，暫停，繼續
   * 檢視Blueprint和即時副本屬性

* 執行轉出動作

## 開啟即時副本概述 {#opening-the-live-copy-overview}

您可以從以下位置開啟即時副本概述：

* [藍圖頁面的參考側面板（網站主控台）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint頁面的屬性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 開啟即時副本概述- Blueprint頁面的參考 {#opening-live-copy-overview-references-for-a-blueprint-page}

您可 **以從Sites主控台的「參考」側面板開啟「即時複製概觀** 」(Live Copy Overview ******** ):

1. 在Sites控 **制台** ，導 [覽至您的Blueprint頁面並加以選取](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟「參 **[照](/help/sites-authoring/basic-handling.md#references)**」面板並選&#x200B;**取「即時副本」**。

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您也可以先開啟「參照」，然後選取藍圖。

1. 選擇 **即時副本概述** ，以顯示並使用與所選藍圖相關的所有即時副本的概述。
1. 使用 **Close** 退出並返回 **Sites** 主控台。

### 開啟即時副本概述- Blueprint頁面的屬性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

檢視 **藍圖頁面的屬性時** ，可以開啟即時副本概述：

1. 開啟適 **當藍圖** 頁面的屬性。
1. 開啟「 **Blueprint** 」標籤-「即時 **副本概述** 」選項會顯示在頂端工具列中：

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. 選擇 **即時副本概述** ，以顯示並使用與目前藍圖相關的所有即時副本的概述。

   >[!NOTE]
   >
   >如需詳細資訊，另請參閱知識文 [庫文章Livecopy狀態訊息——最新／綠色／同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html)。

1. 使用 **Close** 退出並返回 **Sites** 主控台。

## 使用即時副本概觀 {#using-the-live-copy-overview}

「即 **時副本概述** 」也可用於執行即時副本上的動作：

1. 開啟即 **時副本概觀**。
1. 選擇所需的藍圖或即時副本頁面——工具列將會更新以顯示可用的動作。 可用 [的動作](/help/sites-administering/msm.md#terms-used) ，取決於您選擇的是Blueprint [](#actions-for-a-blueprint-page)[，還](#actions-for-a-live-copy-page) 是即時復本：

### Blueprint頁面的動作 {#actions-for-a-blueprint-page}

當您選取Blueprint頁面時，可執行下列動作：

![chlimage_1-361](assets/chlimage_1-361.png)

* 編輯

   * 開啟藍圖頁面進行編輯。

* [轉出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 執行轉出，將變更從來源推送至即時副本。

### 即時副本頁面的動作 {#actions-for-a-live-copy-page}

當您選取即時複製頁面時，可執行下列動作：

![chlimage_1-362](assets/chlimage_1-362.png)

* 編輯

   * 開啟即時副本頁面進行編輯。

* [關係狀態](#relationship-status)

   * 查看有關狀態和繼承的資訊。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步即時副本，將更改從源位置提取到即時副本。

* [重設](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重設即時副本頁面，移除所有繼承取消，並將頁面傳回至與來源頁面相同的狀態。

* [擱置](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 暫時停用即時副本與其藍圖頁面之間的即時關係。

* [繼續](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 恢復允許您恢復暫停的關係。

* [分離](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久移除即時副本與其藍圖頁面之間的即時關係。

## 關係狀態 {#relationship-status}

「關 **系狀態** 」控制台有兩個標籤，提供一系列功能：

* [關係狀態資訊](#relationship-status-information)
* [即時副本資訊](#live-copy-information)

### 關係狀態資訊 {#relationship-status-information}

此標籤提供藍圖與即時副本之間關係狀態的詳細資訊：

![chlimage_1-363](assets/chlimage_1-363.png)

### 即時副本資訊 {#live-copy-information}

此標籤可讓您檢視和編輯即時副本設定：

![chlimage_1-364](assets/chlimage_1-364.png)

