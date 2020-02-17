---
title: 將資產與活動串流整合
description: 說明AEM的錄制功能，以及如何設定AEM以記錄特定事件。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 將資產與活動串流整合 {#integrating-assets-with-activity-stream}

Adobe Experience Manager(AEM)Assets使用者會執行許多動作，例如建立、上傳和刪除資產。 您可以記錄這些動作，以便提供使用者所執行動作的記錄。 本節說明AEM的錄制功能，以及如何設定AEM以記錄特定事件。

## 效能考量事項與預設行為 {#performance-considerations-and-default-behavior}

例如，進行批量導入時，此整合可能會佔用CPU和磁碟空間。 基於這些原因，AEM Assets與「活動串流」的整合預設為停用。

## 支援的動作事件 {#supported-action-events}

可將下列事件設定為記錄：

* 已接受授權（已接受）
* 已建立資產(ASSET_CREATED)
* 已移動資產(ASSET_MOVED)
* 資產已移除(ASSET_REMOVED)
* 已拒絕授權（已拒絕）
* 已下載資產（已下載）
* 資產版本化（版本化）
* 資產版本已還原（已還原）
* 資產中繼資料已更新(METADATA_UPDATED)
* 已發佈至外部系統的資產(PUBLISHED_EXTERNAL)
* 資產的原始已更新(ORIGINAL_UPDATED)
* 資產轉譯已更新(RENDITION_UPDATED)
* 資產轉譯已移除(RENDITION_REMOVED)
* 已更新子資產(SUBASSET_UPDATED)
* 已移除子資產(SUBASSET_REMOVED)

## 設定AEM Assets事件錄制 {#configuring-aem-assets-events-recording}

Web主 [控台](/help/sites-deploying/configuring-osgi.md) ，可讓您存取AEM Assets事件記錄器微調。 若要設定AEM Assets事件記錄器，請依下列步驟進行：

1. 導覽至 **[!UICONTROL Web Console]**

1. 按一下 **[!UICONTROL 設定]**。

1. 連按兩 **[!UICONTROL 下Day CQ DAM Event Recorder]**。

1. 選中 **[!UICONTROL 啟用此服務]**。

1. 檢查您 **** 要在使用者活動串流中記錄哪些事件類型。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 閱讀錄制的事件 {#reading-recorded-events}

記錄的事件會儲存為活動。 您可以使用 [ActivityManager API以程式設計方式讀取它們](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)。
