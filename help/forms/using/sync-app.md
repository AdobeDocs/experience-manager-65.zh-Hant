---
title: 同步應用程式
description: 將行動裝置上的AEM Forms應用程式與AEM Forms伺服器同步。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%
---
# 同步應用程式{#synchronizing-the-app}

>[!NOTE]
>
>AEM Forms應用程式目前已棄用。 如有疑問或需要協助，請連絡[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)。

## 同步應用程式 {#synchronizing-the-app-1}

應用程式中的表單可從AEM Forms伺服器下載。 這些表單會下載至「工作」和「Forms」標籤下。 從表單建立的草稿會下載到「草稿」索引標籤中，而從任務建立的草稿則會下載到「任務」索引標籤中。 對於OSGi伺服器上的獨立表單，表單和草稿會分別在Forms和草稿索引標籤中下載。

完成並提交表單後，如果應用程式上線，表單會立即上傳回AEM Forms伺服器。 應用程式進行同步處理時，系統會從伺服器擷取表單。 不過，如果應用程式上線，草稿會立即與伺服器同步。

當您與AEM Forms伺服器連線時，應用程式預設會每15分鐘同步一次。 不過，您可以選擇變更同步化頻率。 或者，您可以隨時手動同步應用程式。

**手動同步應用程式**

選取主畫面右下角的[同步處理]按鈕![sync-app](assets/sync-app.png)。

**變更同步處理頻率**

1. 若要移至[設定]畫面，請選取[首頁]畫面左上角的功能表按鈕，然後選取[**設定**]。
1. 在「設定」畫面中，選取「一般」標籤。

   ![一般設定視窗中的同步頻率設定](assets/gen-settings-2.png)

1. 在「同步頻率」選項上，選取「同步頻率」右邊的值。
1. 在下拉式清單中，選取新的同步化頻率。

### 技術規格 {#technical-specifications}

* 將離線應用程式資料提交至AEM Forms伺服器的主要邏輯包含在runtime/offline/util/offline.js中。
* 在.js中，呼叫processOfflineSubmittedSavedTasks(...) 函式中，將已儲存/已提交的工作傳送至伺服器。 它也會處理同步處理過程中的任何錯誤或衝突。 如果任務提交失敗，應用程式上的任務會標示為失敗。 此外，任務仍會保留在寄件匣中。
* syncSubmittedTask()和syncSavedTask()函式會針對個別工作執行作業。
* 在使用者選擇同步處理伺服器的離線狀態或背景執行緒自動同步之後，工作清單元件會起始對processOfflineSubmittedSavedTasks()函式的呼叫。
