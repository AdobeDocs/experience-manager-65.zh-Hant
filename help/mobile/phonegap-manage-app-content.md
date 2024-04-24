---
title: 建立及管理應用程式內容
description: 管理應用程式內容需要開發人員、內容作者和管理員共同作出努力。 作者根據應用程式開發人員產生的範本和元件操作頁面。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---

# 建立及管理應用程式內容{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

管理應用程式內容需要來自的集體努力 [開發人員](#developer)，內容 [作者](#author)、和 [管理員](#administrator). 作者根據應用程式開發人員產生的範本和元件操作頁面。

最後，管理員策略性地發佈更新的應用程式內容。

>[!NOTE]
>
>**先決條件**：
>
>在 [部署和維護](/help/sites-deploying/deploy.md)，開發人員已熟悉Adobe Experience Manager (AEM)中的系統元件和範本。

## 「管理頁面內容」表徵圖 {#the-manage-page-content-tile}

>[!CAUTION]
>
>如果您未使用現成可用的應用程式範本，若要在OTA發佈新應用程式內容，您必須設定內容同步處理常式。
>
>另請參閱 [具有內容同步功能的行動裝置](/help/mobile/phonegap-contentsync.md) 如需詳細資訊，請參閱開發人員一節。

在這裡，您可以在AEM Mobile中建立、編輯和刪除內容，其方式與在AEM Sites中大致相同。

此 **「管理頁面內容」圖磚** 顯示受管理內容的頁數以及上次為特定裝載修改的頁數。 您可以按一下圖磚中的每筆記錄，深入鑽研內容以建立、複製、移動、刪除及更新頁面。

內容更新後，管理員可以透過 **「管理內容封裝」圖磚。**

![chlimage_1-161](assets/chlimage_1-161.png)

選取其中一個列出的內容封裝，以建立或編輯內容，例如建立、編輯或移除頁面、變更導覽和頁面順序，以及建立或更新內容，例如複製（文字）和媒體。

注意 *一切都是內容*，表示應用程式樣式、複製（文字）、媒體、頁面、導覽和內容目標定位都可以在OTA中編輯和更新，無須前往應用程式商店。

若要編輯AEM Mobile內容，*AEM作者*需要對AEM內容編輯介面有深入的瞭解： [在AEM中編寫頁面。](/help/sites-authoring/qg-page-authoring.md)

## 「管理內容套件」圖磚 {#the-manage-content-packages-tile}

此處， *AEM管理員* 可以快速輕鬆地更新其應用程式，以提供吸引人的體驗和最新內容，進而促進品牌參與並達成業務目標，完全不需要開發人員或應用程式商店重新提交。

![chlimage_1-162](assets/chlimage_1-162.png)

一次 *AEM作者* 已透過「管理內容圖磚」新增或修改內容， *AEM管理員* 能夠透過內容套件更新將這些變更推送給客戶。

內容套件動作可讓您 *AEM作者* 在開發團隊變更主機應用程式設計與實作時（包括導覽、樣式、伺服器端邏輯、範本和元件），建立及編輯頁面內容，然後將這些變更推送到OTA給客戶，而不需要重新提交至各種商店進行發佈。

**若要發佈新內容或更新內容**

從圖磚中選取內容套件，在此範例中為英文套件。 請注意，內容更新對話方塊會列出相關 *內容同步* 設定。 如果應用程式內容在先前的更新後已修改，則會顯示狀態 *擱置中*，如下所示。

![chlimage_1-163](assets/chlimage_1-163.png)

接下來，選取 **階段** 動作位於正在建立內容更新的右上方。 新增適當的更新資訊，然後按[完成]。

![chlimage_1-164](assets/chlimage_1-164.png)

此 *內容同步* 接著，處理常式會透過形成delta （的套件）來建立所需的套件 *僅限* 已變更的內容)。 完成後，此更新內容套件已暫存，如下所示。

安裝內容更新可讓您在將內容發佈到OTA到行動裝置之前進行多次更新。

>[!NOTE]
>
>階段內容可在發佈前使用AEM Verify應用程式來驗證。
>
>另請參閱 [AEM適用的Mobile Quickstart驗證](/help/mobile/phonegap-mobile-quickstart.md) 以取得有關AEM Verify應用程式的詳細資料。

![chlimage_1-165](assets/chlimage_1-165.png)

準備好透過Content Sync OTA為您的應用程式使用者傳遞新內容時，請選取「 」 **發佈** 如下所示。

![chlimage_1-166](assets/chlimage_1-166.png)

### 後續步驟 {#the-next-steps}

瞭解如何在應用程式控制面板中建立和管理應用程式內容後，請參閱下列資源以取得其他撰寫角色：

* [「管理應用程式」動態磚](/help/mobile/phonegap-app-details-tile.md)
* [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md)
* [應用程式定義](/help/mobile/phonegap-app-definitions.md)
* [使用建立應用程式精靈建立新應用程式](/help/mobile/phonegap-create-new-app.md)
* [匯入現有的混合式應用程式](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
