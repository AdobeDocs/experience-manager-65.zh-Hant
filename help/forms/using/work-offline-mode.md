---
title: 在離線模式下工作
seo-title: 在離線模式下工作
description: 讓行動裝置離線至AEM Forms網路範圍以外，或完全離線模式，並在AEM Forms應用程式上工作
seo-description: 讓行動裝置離線至AEM Forms網路範圍以外，或完全離線模式，並在AEM Forms應用程式上工作
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在離線模式下工作 {#working-in-the-offline-mode}

AEM Forms應用程式的離線模式可讓您順暢地工作，即使應用程式離線亦然。 您可以開啟、更新和提交表格，而不需要任何網路連線。

您可以先將應用程式與AEM Forms伺服器同步化，開始使用AEM Forms應用程式。 指派給您的所有表格都會下載到您的應用程式中。 對於JEE上的AEM Forms，會在Tasks標籤頁中擷取工作，並在Forms標籤中擷取關聯的表單和其他表單。 對於OSGi上的AEM Forms,「表單」索引標籤中只會載入「表單」。

如需如何同步應用程式的詳細資訊，請參閱「同 [步應用程式」](/help/forms/using/sync-app.md)。

## 讓表單離線可用 {#making-forms-available-offline}

當您將應用程式與AEM Forms伺服器同步時，表單會下載到您的行動裝置。 但是，預設情況下，不會下載與表單關聯的附件。 這表示如果您線上，您可以查看附件。 不過，為了確保您可以離線模式檢視附件，請變更應用程式中的預設設定。

為確保關聯附件隨每個表單一起下載，請將「提取附件」設定為「開啟」。 如需詳細資訊，請參 [閱更新一般設定](/help/forms/using/update-general-settings.md)。

由於在行動裝置上下載資料可能會影響裝置的效能，因此依預設，「擷取附件」設定會設為「關閉」。 在將設定更新為ON後，將附件從伺服器下載到設備中的任何任務。 在離線模式下，用戶可以在將「提取附件」選項設定為「開啟」後，處理所有下載到 **設備的任務** 。

## 設定AEM Forms應用程式的離線服務 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms應用程式離線服務可識別表單中使用的資源。 AEM Forms應用程式依賴此服務來取得表單相依性的相關資訊。 需要有關表單相依性的資訊，才能啟用離線功能。 AEM Forms應用程式離線服務會快取表單中使用之資源的路徑或URL。 根據表單中的改變和為離線服務配置的有效期間更新快取。 快取表單中使用之資源的路徑或URL可改善伺服器端效能。

若要設定AEM Forms應用程式的伺服器端離線元件：

1. 在作者例項中，導覽至 **Adobe Experience Manager** >工具&#x200B;**>表** 單 ********>設定Forms App Offline Service。

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在「一般設定」下，您可以執行下列動作：

   * **清除快取**:清除表單相關性的伺服器端快取。
   * **重設配置**:重設AEM Forms應用程式離線設定。
   * **快取有效性**:指定伺服器端離線快取的有效期。
   * **資源觀察路徑**:指定離線服務監視資源更改的路徑。 如果指定路徑中發生任何變更，則會更新所有相依表單的離線快取。 例如， `/etc/clientlibs/fd,/content/dam/images`。

1. 在「手動資 **源快取** 」頁籤中，指定無法標識的表單相關性離線服務。 您可以指定資源，例如從JavaScript中載入的影像。 AEM Forms應用程式也會針對離線模式下載這些資源。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
