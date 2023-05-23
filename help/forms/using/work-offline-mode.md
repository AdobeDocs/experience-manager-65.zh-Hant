---
title: 在離線模式下工作
seo-title: Working in the offline mode
description: 使您的移動設備離線，脫離AEM Forms網路範圍或完全離線模式，並在AEM Forms應用上工作
seo-description: Take your mobile device offline outside your AEM Forms network range or in a completely offline mode and work on the AEM Forms app
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# 在離線模式下工作 {#working-in-the-offline-mode}

AEM Forms應用的離線模式使你即使離線也能無縫工作。 您可以開啟、更新和提交表單，而無需任何網路連接。

你開始使用AEM Forms應用，方法是將你的應用與AEM Forms伺服器同步。 分配給您的所有表單都將下載到您的應用中。 對於JEE上的AEM Forms，任務將在任務頁籤中讀取，並在Forms頁籤中為相關表單和其他表單提供起點。 對於OSGi上的AEM Forms，只有Forms被裝在Forms標籤上。

有關如何同步應用的詳細資訊，請參見 [正在同步應用](/help/forms/using/sync-app.md)。

## 使Forms離線可用 {#making-forms-available-offline}

當您將應用與AEM Forms伺服器同步時，表單將下載到您的移動設備。 但是，預設情況下，不下載與表單關聯的附件。 這意味著，如果您處於聯機狀態，則可以查看附件。 但是，為確保您可以在離線模式下查看附件，請更改應用中的預設設定。

為確保關聯附件隨每個表單一起下載，請將「提取附件」設定為「開啟」。 有關詳細資訊，請參閱 [更新常規設定](/help/forms/using/update-general-settings.md)。

由於在移動設備上下載資料可能會影響設備的效能，因此預設情況下，「提取附件」設定設定為OFF。 在將設定更新為ON後，從伺服器下載的任何任務的附件都會被提取到設備。 在離線模式下，用戶可以處理在設定 **提取附件** 選項。

## 為AEM Forms應用配置離線服務 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms應用離線服務標識表單中使用的資源。 AEM Forms應用依靠此服務獲取有關表單依賴項的資訊。 要啟用離線功能，需要有關表單依賴項的資訊。 AEM Forms應用離線服務快取表單中所用資源的路徑或URL。 基於表單中的改變和為離線服務配置的有效期更新快取。 快取表單中使用的資源的路徑或URL可提高伺服器端效能。

配置AEM Forms應用的伺服器端離線元件：

1. 在作者實例中，導航到 **Adobe Experience Manager** >**工具** > **Forms** > **配置Forms應用離線服務**。

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在「常規設定」(General Settings)下，可以執行以下操作：

   * **清除快取**:清除表單依賴項的伺服器端快取。
   * **重置配置**:重置AEM Forms應用離線配置。
   * **快取有效性**:指定伺服器端離線快取的有效期。
   * **資源觀察路徑**:指定離線服務監視資源更改的路徑。 如果指定路徑中發生任何更改，則會更新所有從屬表單的離線快取。 比如說， `/etc/clientlibs/fd,/content/dam/images`。

1. 在 **手動資源快取** 頁籤，指定表單依賴項離線服務無法標識。 可以指定資源，如從JavaScript中載入的映像。 AEM Forms應用也將下載這些資源，以用於離線模式。
