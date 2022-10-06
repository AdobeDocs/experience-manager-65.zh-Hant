---
title: 同步應用程式
seo-title: Synchronizing the app
description: 將行動裝置上的AEM Forms應用程式與AEM Forms伺服器同步。
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

# 同步應用程式{#synchronizing-the-app}

## 同步應用程式 {#synchronizing-the-app-1}

應用程式中的表單會從AEM Forms伺服器下載。 表單會下載至「工作」和「Forms」標籤下。 從表單建立的草稿會下載到「草稿」標籤中，而從任務建立的草稿則會下載到「任務」標籤中。 若是OSGi伺服器上的獨立表單，表單和草稿會分別在Forms和草稿標籤中下載。

當您完成表單並提交時，如果應用程式上線，表單會立即上傳回AEM Forms伺服器。 應用程式同步時，系統會從伺服器擷取表單。 不過，如果應用程式上線，草稿會立即同步至伺服器。

依預設，當您與AEM Forms伺服器上線時，您的應用程式會每15分鐘同步一次。 但是，您可以選擇更改同步頻率。 或者，您可以隨時手動同步應用程式。

**手動同步應用程式的方式**

點選「同步」按鈕 ![sync-app](assets/sync-app.png) 在主螢幕的右下角。

**更改同步頻率**

1. 若要前往「設定」畫面，請點選「主畫面」左上角的功能表按鈕，然後點選 **設定**.
1. 在「設定」畫面中，點選「一般」標籤。

   ![「常規設定」窗口中的同步頻率設定](assets/gen-settings-2.png)

1. 在「同步頻率」選項上，點選「同步頻率」右側的值。
1. 在下拉式清單中，選取新的同步頻率。

### 技術規格 {#technical-specifications}

* runtime/offline/util/offline.js中包含將離線應用程式資料提交至AEM Forms伺服器的主要邏輯。
* 在.js中，對processOfflineSubmittedSavedTasks(...)函式的調用將已保存/已提交的任務發送到伺服器。 它也可處理同步過程中的任何錯誤或衝突。 如果提交任務失敗，應用程式上的任務會標示為失敗。 此外，任務仍保留在您的發件箱中。
* syncSubmittedTask()和syncSavedTask()函式對單個任務執行操作。
* 當用戶選擇將離線狀態同步到伺服器或由後台線程自動同步後，任務清單元件將啟動對processOfflineSubmittedSavedTasks()函式的調用。
