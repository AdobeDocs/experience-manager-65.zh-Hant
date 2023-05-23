---
title: 整合 [!DNL Assets] 使用活動流
description: 描述的錄制功能 [!DNL Experience Manager] 以及如何配置它以記錄特定事件。
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 整合 [!DNL Assets] 使用活動流 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] 用戶執行建立、上載和刪除資產等許多操作。 可以記錄這些操作，以便您能夠提供用戶所做操作的歷史記錄。 本節介紹了 [!DNL Experience Manager] 以及如何配置 [!DNL Experience Manager] 以記錄特定事件。

## 效能注意事項和預設行為 {#performance-considerations-and-default-behavior}

例如，進行批量導入時，此整合可能會佔用CPU和磁碟空間。 出於這些原因 [!DNL Assets] 預設情況下，將禁用與活動流的整合。

## 支援的操作事件 {#supported-action-events}

可以將以下事件配置為記錄：

* 已接受許可（已接受）
* 已建立資產(ASSET_CREATED)
* 移動資產(ASSET_MOVED)
* 資產已刪除(ASSET_REMOVED)
* 許可證被拒絕（已拒絕）
* 已下載資產（已下載）
* 資產版本化（版本化）
* 資產版本已還原（已還原）
* 資產元資料已更新(METADATA_UPDATED)
* 已發佈到外部系統的資產(PUBLISHED_EXTERNAL)
* 資產的原始更新(ORIGINAL_UPDATED)
* 資產格式副本已更新(RENDITION_UPDATED)
* 已刪除資產格式副本(RENDITION_REMOVED)
* 子資產已更新(SUBASSET_UPDATED)
* 已刪除子資產(SUBASSET_REMOVED)

## 配置 [!DNL Assets] 事件記錄 {#configuring-aem-assets-events-recording}

的 [Web控制台](/help/sites-deploying/configuring-osgi.md) 提供對資產事件記錄器調整的訪問。 要配置資產事件記錄器，請按如下步驟進行：

1. 導航到 **[!UICONTROL Web控制台]**

1. 按一下 **[!UICONTROL 配置]**。

1. 按兩下 **[!UICONTROL 第CQ天大壩事件記錄器]**。

1. 檢查 **[!UICONTROL 啟用此服務]**。

1. 檢查 **[!UICONTROL 事件類型]** 要在用戶活動流中記錄。

1. 按一下「**[!UICONTROL 儲存]**」。

## 讀取錄制的事件 {#reading-recorded-events}

記錄的事件被儲存為活動。 可以使用 [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)。
