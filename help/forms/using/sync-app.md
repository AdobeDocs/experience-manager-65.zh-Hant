---
title: 正在同步應用
seo-title: Synchronizing the app
description: 將移動設備上的AEM Forms應用與AEM Forms伺服器同步。
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 正在同步應用{#synchronizing-the-app}

## 正在同步應用 {#synchronizing-the-app-1}

您應用中的表單將從AEM Forms伺服器下載。 表單下載在「任務」和「Forms」頁籤下。 從表單建立的草稿將在「草稿」頁籤下載，從任務建立的草稿將在「任務」頁籤下載。 對於OSGi伺服器上的獨立表單，表單和草稿分別下載在Forms和草稿頁籤中。

當您完成並提交表單時，如果應用程式處於聯機狀態，表單將立即上載回AEM Forms伺服器。 同步應用程式時，會從伺服器讀取表單。 但是，如果應用程式處於聯機狀態，則草稿將立即與伺服器同步。

當您與AEM Forms伺服器聯機時，預設情況下，每15分鐘同步一次您的應用。 但是，您可以選擇更改同步頻率。 或者，您可以隨時手動同步應用。

**手動同步應用程式**

按一下「同步」按鈕 ![同步應用](assets/sync-app.png) 在主螢幕的右下角。

**更改同步頻率**

1. 要轉到「Setting（設定）」螢幕，請按一下「Home（首頁）」螢幕左上角的菜單按鈕，然後按一下 **設定**。
1. 在「Settings（設定）」螢幕中，按一下「General（常規）」頁籤。

   ![「常規設定」窗口中的同步頻率設定](assets/gen-settings-2.png)

1. 在「Sync frequency（同步頻率）」選項上，按一下「Sync frequency（同步頻率）」右側的值。
1. 在下拉清單中，選擇新的同步頻率。

### 技術規格 {#technical-specifications}

* 將離線應用資料提交到AEM Forms伺服器的主要邏輯包含在runtime/offline/util/offline.js中。
* 在.js中，調用processOfflineSubmittedSavedTasks(...)函式，將已保存/已提交的任務發送到伺服器。 它還處理同步過程中的任何錯誤或衝突。 如果提交任務失敗，則應用上的任務將標籤為失敗。 此外，任務仍保留在發件箱中。
* syncSubmittedTask()和syncSavedTask()函式對單個任務執行操作。
* 當用戶選擇將離線狀態與伺服器同步或後台線程自動同步後，任務清單元件將啟動對processOfflineSubmittedSavedTasks()函式的調用。
