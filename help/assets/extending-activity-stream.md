---
title: 將 [!DNL Assets] 與活動資料流整合
description: 說明 [!DNL Experience Manager] 的錄製功能，以及如何設定它以錄製特定事件。
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 將[!DNL Assets]與活動資料流整合 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets]使用者可執行許多動作，例如建立、上傳和刪除Assets。 這些動作可以記錄下來，這樣您就可以提供使用者所做動作的歷史記錄。 本節說明[!DNL Experience Manager]的錄製功能，以及如何設定[!DNL Experience Manager]來錄製特定事件。

## 效能考量事項和預設行為 {#performance-considerations-and-default-behavior}

例如，執行大量匯入時，這項整合可能會耗用CPU和磁碟空間。 基於這些原因，[!DNL Assets]與活動資料流的整合預設為停用。

## 支援的動作事件 {#supported-action-events}

您可以設定要記錄的下列事件：

* 授權已接受（已接受）
* 已建立的資產(ASSET_CREATED)
* 資產已移動(ASSET_MOVED)
* 資產已移除(ASSET_REMOVED)
* 授權已拒絕（已拒絕）
* 資產已下載（已下載）
* 資產版本設定（版本設定）
* 資產版本已還原（已還原）
* 資產中繼資料已更新(METADATA_UPDATED)
* 資產已發佈至外部系統(PUBLISHED_EXTERNAL)
* 資產的原始更新（原始更新）
* 資產轉譯已更新(RENDITION_UPDATED)
* 資產轉譯已移除(RENDITION_REMOVED)
* 子資產已更新(SUBASSET_UPDATED)
* 子資產已移除(SUBASSET_REMOVED)

## 設定[!DNL Assets]個事件記錄 {#configuring-aem-assets-events-recording}

[Web主控台](/help/sites-deploying/configuring-osgi.md)提供存取Assets事件記錄器調整的許可權。 若要設定「Assets事件記錄器」，請依照下列步驟進行：

1. 瀏覽至&#x200B;**[!UICONTROL 網頁主控台]**

1. 按一下&#x200B;**[!UICONTROL 組態]**。

1. 連按兩下&#x200B;**[!UICONTROL Day CQ DAM Event Recorder]**。

1. 檢查&#x200B;**[!UICONTROL 啟用此服務]**。

1. 檢查您要在使用者活動資料流中記錄哪些&#x200B;**[!UICONTROL 事件型別]**。

1. 按一下「**[!UICONTROL 儲存]**」。

## 讀取錄製的事件 {#reading-recorded-events}

記錄的事件會儲存為活動。 您可以使用[ActivityManager API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)以程式設計方式讀取它們。
