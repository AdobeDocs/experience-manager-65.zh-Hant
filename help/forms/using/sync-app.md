---
title: 同步化應用程式
seo-title: 同步化應用程式
description: 將您行動裝置上的AEM Forms應用程式與AEM Forms伺服器同步。
seo-description: 將您行動裝置上的AEM Forms應用程式與AEM Forms伺服器同步。
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 同步化應用程式{#synchronizing-the-app}

## 同步化應用程式 {#synchronizing-the-app-1}

您應用程式中的表格會從AEM Forms伺服器下載。 表單會下載在「工作」和「表單」標籤下。 從表單建立的草稿會下載到「草稿」索引標籤中，從工作建立的草稿則會下載到「工作」索引標籤中。 對於OSGi伺服器上的獨立表單，表單和草稿會分別下載在「表單」和「草稿」標籤中。

當您完成並送出表格時，如果應用程式線上，表格會立即上傳回AEM Forms伺服器。 當應用程式同步時，會從伺服器擷取表格。 不過，如果應用程式線上，草稿會立即與伺服器同步。

當您與AEM Forms伺服器連線時，依預設，您的應用程式會每15分鐘同步一次。 但是，您可以選擇更改同步頻率。 或者，您可以隨時手動同步應用程式。

**若要手動同步應用程式**

點選主畫面 ![右下角的](assets/sync-app.png) 「同步」按鈕sync-app。

**更改同步頻率**

1. 若要前往「Setting（設定）」畫面，請點選「Home（首頁）」畫面左上角的功能表按鈕，然後點選「 **Settings（設定）**」。
1. 在「設定」畫面中，點選「一般」標籤。

   ![「常規設定」窗口中的同步頻率設定](assets/gen-settings-2.png)

1. 在「同步頻率」選項上，點選「同步頻率」右側的值。
1. 在下拉清單中，選擇新的同步頻率。

### 技術規格 {#technical-specifications}

* 將離線應用程式資料送出至AEM Forms伺服器的主要邏輯包含在runtime/offline/util/offline.js中。
* 在。js中，對processOfflineSubmittedSavedTasks(...)函式的調用將已保存／已提交的任務發送到伺服器。 它還可處理同步過程中的任何錯誤或衝突。 如果提交任務失敗，應用程式上的任務會標示為失敗。 此外，該任務仍保留在您的Outbox中。
* syncSubmittedTask()和syncSavedTask()函式對單個任務執行操作。
* 當用戶選擇將離線狀態同步到伺服器或通過後台線程自動同步後，任務清單元件將啟動對processOfflineSubmittedSavedTasks()函式的調用。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
