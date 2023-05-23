---
title: 更新常規設定
seo-title: Updating general settings
description: 更新AEM Forms應用設定，如「首頁」螢幕和獲取起始點和附件選項
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# 更新常規設定{#updating-general-settings}

AEM Forms應用的常規設定允許您指定設定，如讀取附件、離線模式、登錄螢幕、預設類別和自動保存頻率。

## 更新應用中的常規設定 {#working-with-the-form}

當您將應用與AEM Forms伺服器同步時，所有表單和定義的任務都將下載到您的移動設備。

當您的應用程式同步時，出廠設定的AEM Forms應用程式解決方案不會下載與每個表單關聯的附件。

在「常規」頁籤中，更改下載附件、離線模式、登錄螢幕、自動保存和同步設定。 您可以更改 [主螢幕](../../forms/using/home-screen.md) 你的應用。

**導航到「設定」螢幕上的「常規」頁籤**

1. 要轉到「Setting（設定）」螢幕，請按一下「Home（首頁）」螢幕左上角的「Menu（菜單）」按鈕，然後按一下 **設定**。
1. 在「Settings（設定）」螢幕中，按一下「General（常規）」頁籤。

   ![AEM Forms應用中的常規設定](assets/gen-settings-1.png)

   常規設定螢幕

   >[!NOTE]
   >
   >這些選項可以在不同的移動設備上顯示不同。

### 一般設定 {#general-settings}

你可以對應用的設定進行以下更改。

* **提取任務附件**:指定在將每個任務下載到您的應用時是否下載關聯的附件。
* **離線模式**:啟用或禁用AEM Forms應用的離線服務。 請參閱 [在離線模式下工作](/help/forms/using/work-offline-mode.md) 的雙曲餘切值。
* **落地屏**:設定起始位置([主螢幕](../../forms/using/home-screen.md))。
可用選項：

   * Forms
   * 任務
   * 我的最愛

* **預設類別**:允許您選擇要在主螢幕中顯示的表單類別。 選擇「全部」後，可以在主螢幕中看到所有表單。 類別根據應用中載入的表單進行填充。 Forms可基於AEM Forms伺服器中指定的表單設定在應用中使用。

* **自動保存頻率**:設定頻率 [移動應用保存表單資料](../../forms/using/autosave-data-app.md) 本地。
* **同步頻率**:設定頻率 [移動應用已同步](../../forms/using/sync-app.md) 使AEM Forms伺服器處於聯機模式。
   **清除本地資料**:清除資料庫，包括設備中所有用戶的設定和本地資料以及檔案儲存。

>[!NOTE]
>
>清除快取將立即將你從應用中註銷。
>
>但是，系統將提示您確認清除快取操作。
