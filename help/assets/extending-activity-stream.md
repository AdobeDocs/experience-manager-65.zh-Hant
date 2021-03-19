---
title: 將 [!DNL Assets] 與活動串流整合
description: 說明 [!DNL Experience Manager] 的錄制功能，以及如何設定它來錄制特定事件。
contentOwner: AG
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---


# 將[!DNL Assets]與活動串流{#integrating-assets-with-activity-stream}整合

[!DNL Adobe Experience Manager Assets] 使用者會執行許多動作，例如建立、上傳和刪除資產。您可以記錄這些動作，以便提供使用者所執行動作的記錄。 本節介紹[!DNL Experience Manager]的錄制功能，以及如何設定[!DNL Experience Manager]以記錄特定事件。

## 效能注意事項和預設行為{#performance-considerations-and-default-behavior}

例如，進行批量導入時，此整合可能會佔用CPU和磁碟空間。 因此，預設會停用與活動串流的[!DNL Assets]整合。

## 支援的動作事件{#supported-action-events}

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

## 配置記錄{#configuring-aem-assets-events-recording}的[!DNL Assets]事件

[Web控制台](/help/sites-deploying/configuring-osgi.md)提供對資產事件記錄器調整的訪問。 若要設定資產事件記錄器，請依下列步驟進行：

1. 導航至&#x200B;**[!UICONTROL Web控制台]**

1. 按一下&#x200B;**[!UICONTROL Configuration]**。

1. 連按兩下&#x200B;**[!UICONTROL Day CQ DAM Event Recorder]**。

1. 選中&#x200B;**[!UICONTROL 啟用此服務]**。

1. 檢查您希望在用戶活動流中記錄哪些&#x200B;**[!UICONTROL 事件類型]**。

1. 按一下「**[!UICONTROL 儲存]**」。

## 讀取記錄的事件{#reading-recorded-events}

記錄的事件會儲存為活動。 您可以使用[ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)以程式設計方式讀取它們。
