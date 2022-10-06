---
title: 在離線模式下工作
seo-title: Working in the offline mode
description: 將行動裝置離線至AEM Forms網路範圍以外或完全離線模式，並在AEM Forms應用程式中運作
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

AEM Forms應用程式的離線模式可讓您即使應用程式離線，也能順暢地運作。 您可以開啟、更新和提交表單，無需任何網路連接。

您可以將應用程式與AEM Forms伺服器同步，以開始使用AEM Forms應用程式。 指派給您的所有表單都會下載到應用程式中。 若是JEE版的AEM Forms，工作會擷取至「工作」標籤中，並從Forms標籤中擷取相關表單和其他表單的起始點。 若是OSGi上的AEM Forms,Forms標籤中只會載入Forms。

如需如何同步應用程式的詳細資訊，請參閱 [同步應用程式](/help/forms/using/sync-app.md).

## 讓Forms離線可用 {#making-forms-available-offline}

當您將應用程式與AEM Forms伺服器同步時，表單會下載至您的行動裝置。 但是，預設情況下不會下載與表單相關聯的附件。 這意味著，如果您聯機，則可以查看附件。 不過，為了確保您可以以離線模式檢視附件，請變更應用程式中的預設設定。

為確保每個表單都下載了關聯的附件，請將「提取附件」設定為「開啟」。 如需詳細資訊，請參閱 [更新一般設定](/help/forms/using/update-general-settings.md).

由於在行動裝置上下載資料可能會影響裝置的效能，因此依預設，擷取附件設定會設為「關閉」。 將設定更新為「開啟」後，從伺服器下載的任何任務都會將附件提取到設備。 在離線模式中，使用者可在設定 **擷取附件** 選項開啟。

## 為AEM Forms應用程式設定離線服務 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms應用程式離線服務可識別表單中使用的資源。 AEM Forms應用程式仰賴此服務來取得表單相依性的相關資訊。 啟用離線功能需要表單相依性的相關資訊。 AEM Forms應用程式離線服務會快取表單中使用之資源的路徑或URL。 快取根據表單中的更改和為離線服務配置的有效期更新。 快取表單中所使用資源的路徑或URL可改善伺服器端效能。

若要設定AEM Forms應用程式的伺服器端離線元件：

1. 在製作例項中，導覽至 **Adobe Experience Manager** >**工具** > **Forms** > **設定Forms App Offline Service**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在「一般設定」下，您可以執行下列動作：

   * **清除快取**:清除表單相依性的伺服器端快取。
   * **重置配置**:重設AEM Forms應用程式離線設定。
   * **快取有效性**:指定伺服器端離線快取的有效期。
   * **資源觀察路徑**:指定離線服務監視資源更改的路徑。 如果指定路徑中發生任何變更，則會更新所有相依表單的離線快取。 例如， `/etc/clientlibs/fd,/content/dam/images`.

1. 在 **手動資源快取** 頁簽，指定離線服務無法識別的表單依賴項。 您可以指定資源，例如從JavaScript內載入的影像。 AEM Forms應用程式也會下載這些資源以進行離線模式。
