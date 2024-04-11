---
title: Live Copy 概觀主控台
description: 瞭解Live Copy概觀控制檯的基本概念。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 25%

---

# Live Copy 概觀主控台{#live-copy-overview-console}

此 **即時副本概觀** 可讓您：

* 檢視/管理網站上的繼承：

   * 檢視Blueprint樹狀結構和對應的即時副本結構，以及其繼承狀態
   * 變更繼承狀態；例如，暫停、繼續
   * 檢視Blueprint和即時副本屬性

* 執行轉出動作

## 開啟 Live Copy 概觀 {#opening-the-live-copy-overview}

您可以從以下位置開啟 Live Copy 概觀：

* [藍圖頁面的參考側面板 (Sites 主控台)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [藍圖頁面的屬性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 開啟即時副本總覽 — Blueprint頁面的參照 {#opening-live-copy-overview-references-for-a-blueprint-page}

**Live Copy 概觀**&#x200B;可以從 **Sites** 主控台的&#x200B;**參考**&#x200B;側面板開啟：

1. 在 **網站** 主控台， [導覽至您的Blueprint頁面並加以選取](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板並選取 **即時副本**.

   ![「參考」面板 — 即時副本](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您也可以先開啟參照，然後選取Blueprint。

1. 選取 **即時副本概觀** 以顯示及使用與所選Blueprint相關之所有即時副本的概觀。
1. 使用&#x200B;**關閉**&#x200B;以退出並返回 **Sites** 主控台。

### 開啟即時副本概觀 — Blueprint頁面的屬性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

**Live Copy 概觀**&#x200B;可以在檢視藍圖頁面的屬性時開啟：

1. 開啟相關藍圖頁面的&#x200B;**屬性**。
1. 開啟 **Blueprint** 標籤 —  **即時副本概觀** 選項會顯示在頂端工具列中：

   ![Blueprint標籤 — 即時副本概觀](assets/chlimage_1-360.png)

1. 選取 **即時副本概觀** 以顯示及使用與目前Blueprint相關之所有即時副本的概觀。

   >[!NOTE]
   >
   >如需詳細資訊，另請參閱知識庫文章 [即時副本狀態訊息 — 最新/綠色/同步中](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 使用&#x200B;**關閉**&#x200B;以退出並返回 **Sites** 主控台。

## 使用 Live Copy 概觀 {#using-the-live-copy-overview}

此 **即時副本概觀** 也可用於對即時副本執行動作：

1. 開啟 **Live Copy 概觀**。
1. 選取所需的Blueprint或即時副本頁面 — 工具列將更新以顯示可用操作。 此 [動作](/help/sites-administering/msm.md#terms-used) 是否可用取決於您是否選取 [Blueprint](#actions-for-a-blueprint-page) 或 [即時副本](#actions-for-a-live-copy-page) 頁面：

### 藍圖頁面的動作 {#actions-for-a-blueprint-page}

選擇藍圖頁面時，可以執行以下動作：

![已選取Blueprint — 可用動作](assets/chlimage_1-361.png)

* 編輯

   * 開啟Blueprint頁面以進行編輯。

* [推出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 執行轉出以將變更從來源推送到LiveCopy。

### Live Copy 頁面的動作 {#actions-for-a-live-copy-page}

選取即時副本頁面時，以下動作可供使用：

![即時副本頁面已選取 — 動作可用](assets/chlimage_1-362.png)

* 編輯

   * 開啟即時副本頁面以進行編輯。

* [關係狀態](#relationship-status)

   * 檢視有關狀態和繼承的資訊。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步即時副本，以將變更從來源提取到即時副本。

* [重設](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重設即時副本頁面以移除所有繼承取消，並讓頁面回到與來源頁面相同的狀態。

* [暫停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 暫時停用即時副本與其Blueprint頁面之間的即時關係。

* [繼續](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 「繼續」可讓您恢復暫停的關係。

* [分離](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久移除即時副本與其Blueprint頁面之間的即時關係。

## 關係狀態 {#relationship-status}

此 **關係狀態** 主控台有兩個標籤，提供了一系列功能：

* [關係狀態資訊](#relationship-status-information)
* [即時副本資訊](#live-copy-information)

### 關係狀態資訊 {#relationship-status-information}

此標籤提供有關Blueprint與即時副本之間關係狀態的詳細資訊：

![關係狀態資訊](assets/chlimage_1-363.png)

### 即時副本資訊 {#live-copy-information}

此索引標籤可讓您檢視及編輯即時副本設定：

![即時副本資訊](assets/chlimage_1-364.png)
