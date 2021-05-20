---
title: 將 [!DNL Assets] 與活動資料流整合
description: 說明 [!DNL Experience Manager] 的記錄功能，以及如何配置它以記錄特定事件。
contentOwner: AG
role: Developer
feature: 資產管理
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 將[!DNL Assets]與活動流{#integrating-assets-with-activity-stream}整合

[!DNL Adobe Experience Manager Assets] 使用者可執行許多動作，例如建立、上傳和刪除資產。您可以記錄這些動作，以便提供使用者所執行動作的歷史記錄。 本節介紹[!DNL Experience Manager]的記錄功能，以及如何配置[!DNL Experience Manager]以記錄特定事件。

## 效能考量事項和預設行為{#performance-considerations-and-default-behavior}

例如，進行批量導入時，此整合可能佔用CPU和磁碟空間。 基於這些原因，預設會停用[!DNL Assets]與活動資料流的整合。

## 支援的動作事件{#supported-action-events}

可將下列事件設定為記錄：

* 已接受許可（已接受）
* 已建立資產(ASSET_CREATED)
* 已移動資產(ASSET_MOVED)
* 已移除資產(ASSET_REMOVED)
* 許可證已拒絕（已拒絕）
* 已下載資產（已下載）
* 資產版本控制（版本控制）
* 資產版本已還原（已還原）
* 已更新資產中繼資料(METADATA_UPDATED)
* 已發佈至外部系統的資產(PUBLISHED_EXTERNAL)
* 資產的原始更新(ORIGINAL_UPDATED)
* 已更新資產轉譯(RENDITION_UPDATED)
* 已移除資產轉譯(RENDITION_REMOVED)
* 子資產已更新(SUBASSET_UPDATED)
* 已移除子資產(SUBASSET_REMOVED)

## 配置記錄{#configuring-aem-assets-events-recording}的[!DNL Assets]事件

[Web控制台](/help/sites-deploying/configuring-osgi.md)提供對資產事件記錄器調整的訪問。 若要設定「資產事件記錄器」，請繼續進行：

1. 導覽至&#x200B;**[!UICONTROL Web主控台]**

1. 按一下&#x200B;**[!UICONTROL Configuration]**。

1. 連按兩下&#x200B;**[!UICONTROL Day CQ DAM事件記錄器]**。

1. 檢查&#x200B;**[!UICONTROL 啟用此服務]**。

1. 檢查您要記錄在使用者活動資料流中的&#x200B;**[!UICONTROL 事件類型]**。

1. 按一下「**[!UICONTROL 儲存]**」。

## 讀取記錄的事件{#reading-recorded-events}

記錄的事件會儲存為活動。 您可以使用[ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)以程式設計方式讀取它們。
