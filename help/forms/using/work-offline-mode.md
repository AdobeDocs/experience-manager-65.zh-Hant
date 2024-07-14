---
title: 在離線模式下工作
description: 讓您的行動裝置在AEM Forms網路範圍以外或完全離線模式下離線，然後使用AEM Forms應用程式
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# 在離線模式下工作 {#working-in-the-offline-mode}

AEM Forms應用程式的離線模式可讓您順暢地工作，即使應用程式離線亦然。 您可以開啟、更新和提交表單，而不需要任何網路連線。

您一開始會使用AEM Forms應用程式，方法是將應用程式與AEM Forms伺服器同步。 指派給您的所有表單都會在您的應用程式中下載。 若為JEE上的AEM Forms，任務會在「任務」標籤中擷取，而起點會與Forms標籤中的表單和其他表單相關聯。 若為OSGi上的AEM Forms，只有Forms會在Forms標籤中載入。

如需如何同步應用程式的詳細資訊，請參閱[同步應用程式](/help/forms/using/sync-app.md)。

## 讓Forms可離線使用 {#making-forms-available-offline}

當您將應用程式與AEM Forms伺服器同步時，表單會下載至您的行動裝置。 不過，預設不會下載與表單相關聯的附件。 這表示如果您線上上，則可以檢視附件。 不過，若要確保您能夠以離線模式檢視附件，請變更應用程式中的預設設定。

若要確保隨每個表單一起下載關聯的附件，請將「擷取附件」設定為「開啟」。 如需詳細資訊，請參閱[更新一般設定](/help/forms/using/update-general-settings.md)。

由於從行動裝置下載資料可能會影響裝置的效能，依預設，擷取附件設定會設為「關閉」。 當設定更新為「開啟」後，任何從伺服器下載的工作的附件都會擷取到裝置。 在離線模式中，使用者將&#x200B;**擷取附件**&#x200B;選項設定為「開啟」後，即可處理下載至裝置的所有工作。

## 為AEM Forms應用程式設定離線服務 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms app離線服務可識別表單中使用的資源。 AEM Forms應用程式依賴此服務來取得表單相依性的相關資訊。 啟用離線功能需要表單相依性的相關資訊。 AEM Forms應用程式離線服務會快取表單中所使用資源的路徑或URL。 快取會根據表單中的變更以及為離線服務設定的有效期而更新。 快取表單中使用的資源的路徑或URL可改善伺服器端效能。

若要設定AEM Forms應用程式的伺服器端離線元件：

1. 在作者執行個體中，瀏覽至&#x200B;**Adobe Experience Manager** >**工具** > **Forms** > **設定Forms App離線服務**。

   URL： `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 在「一般設定」下，您可以執行下列動作：

   * **清除快取**：清除表單相依性的伺服器端快取。
   * **重設設定**：重設AEM Forms app離線設定。
   * **快取有效期間**：指定伺服器端離線快取的有效期間。
   * **資源觀察路徑**：指定離線服務監視資源變更的路徑。 如果指定路徑發生任何變更，則會更新所有相依表單的離線快取。 例如，`/etc/clientlibs/fd,/content/dam/images`。

1. 在&#x200B;**手動資源快取**&#x200B;索引標籤中，指定表單相依性離線服務無法識別。 您可以指定資源，例如從JavaScript內載入的影像。 AEM Forms應用程式也將針對離線模式下載這些資源。
