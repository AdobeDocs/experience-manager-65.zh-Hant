---
title: Live Copy 概觀主控台
seo-title: Live Copy Overview Console
description: 瞭解Live Copy概述控制台的基本知識。
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 29%

---

# Live Copy 概觀主控台{#live-copy-overview-console}

的 **即時複製概述** 允許您：

* 查看/管理跨站點的繼承：

   * 查看藍圖樹和相應的即時複製結構及其繼承狀態
   * 更改繼承狀態；例如，掛起，繼續
   * 查看藍圖和即時複製屬性

* 執行推廣操作

## 開啟 Live Copy 概觀 {#opening-the-live-copy-overview}

您可以從以下位置開啟 Live Copy 概觀：

* [藍圖頁面的參考側面板 (Sites 主控台)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [藍圖頁面的屬性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 開啟即時複製概述 — 藍圖頁的參考 {#opening-live-copy-overview-references-for-a-blueprint-page}

**Live Copy 概觀**&#x200B;可以從 **Sites** 主控台的&#x200B;**參考**&#x200B;側面板開啟：

1. 在 **站點** 控制台， [導航到您的藍圖頁面並選擇](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟 **[引用](/help/sites-authoring/basic-handling.md#references)** 選擇 **即時拷貝**。

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >也可先開啟「參照」(References)，然後選取藍圖。

1. 選擇 **即時複製概述** 顯示和使用與所選藍圖相關的所有即時副本的概覽。
1. 使用&#x200B;**關閉**&#x200B;以退出並返回 **Sites** 主控台。

### 開啟即時複製概述 — 藍圖頁的屬性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

**Live Copy 概觀**&#x200B;可以在檢視藍圖頁面的屬性時開啟：

1. 開啟相關藍圖頁面的&#x200B;**屬性**。
1. 開啟&#x200B;**藍圖**&#x200B;索引標籤 - **Live Copy 概觀** 選項將顯示在頂端工具列中：

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. 選擇 **即時複製概述** 顯示和使用與當前藍圖相關的所有即時副本的概覽。

   >[!NOTE]
   >
   >有關詳細資訊，另請參閱知識庫文章 [Livecopy狀態消息 — 最新/綠色/同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html)。

1. 使用&#x200B;**關閉**&#x200B;以退出並返回 **Sites** 主控台。

## 使用 Live Copy 概觀 {#using-the-live-copy-overview}

的 **即時複製概述** 也可用於執行即時副本上的操作：

1. 開啟 **Live Copy 概觀**。
1. 選擇所需的藍圖或即時複製頁面 — 工具欄將更新以顯示可用操作。 的 [動作](/help/sites-administering/msm.md#terms-used) 可用取決於是否選擇 [藍圖](#actions-for-a-blueprint-page) 或 [即時拷貝](#actions-for-a-live-copy-page) 頁：

### 藍圖頁面的動作 {#actions-for-a-blueprint-page}

選擇藍圖頁面時，可以執行以下動作：

![chlimage_1-361](assets/chlimage_1-361.png)

* 編輯

   * 開啟藍圖頁面進行編輯。

* [推出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 執行推出，將更改從源推送到livecopy。

### Live Copy 頁面的動作 {#actions-for-a-live-copy-page}

選擇即時複製頁時，可以執行以下操作：

![chlimage_1-362](assets/chlimage_1-362.png)

* 編輯

   * 開啟即時複製頁面進行編輯。

* [關係狀態](#relationship-status)

   * 查看有關狀態和繼承的資訊。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步即時副本以將更改從源拉到livecopy。

* [重設](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重置即時複製頁以刪除所有繼承取消項，並將頁返回到與源頁相同的狀態。

* [暫停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 臨時停用即時副本與其藍圖頁面之間的即時關係。

* [繼續](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 恢復允許您恢復掛起的關係。

* [分離](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久刪除即時副本與其藍圖頁面之間的即時關係。

## 關係狀態 {#relationship-status}

的 **關係狀態** console有兩個頁籤，提供一系列功能：

* [關係狀態資訊](#relationship-status-information)
* [即時拷貝資訊](#live-copy-information)

### 關係狀態資訊 {#relationship-status-information}

此頁籤提供有關藍圖和即時副本之間關係狀態的詳細資訊：

![chlimage_1-363](assets/chlimage_1-363.png)

### 即時拷貝資訊 {#live-copy-information}

此頁籤允許您查看和編輯即時複製配置：

![chlimage_1-364](assets/chlimage_1-364.png)
