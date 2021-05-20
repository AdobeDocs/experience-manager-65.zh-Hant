---
title: 建立和管理應用程式內容
seo-title: 建立和管理應用程式內容
description: 管理應用程式內容需要開發人員、內容作者和管理員共同努力。  作者操作頁面，而頁面則是根據應用程式開發人員產生的範本和元件操作。
seo-description: 管理應用程式內容需要開發人員、內容作者和管理員共同努力。  作者操作頁面，而頁面則是根據應用程式開發人員產生的範本和元件操作。
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# 建立和管理應用程式內容{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

管理應用程式內容需要[開發人員](#developer)、內容[作者](#author)和[管理員](#administrator)的集體努力。 作者操作頁面，而頁面則是根據應用程式開發人員產生的範本和元件操作。

最後，管理員會策略性地發佈更新的應用程式內容。

>[!NOTE]
>
>**必備條件**:
>
>在[部署和維護](/help/sites-deploying/deploy.md)中，開發人員熟悉了AEM的元件和模板系統。

## 「管理頁面內容」表徵圖{#the-manage-page-content-tile}

>[!CAUTION]
>
>如果您未使用現成可用的應用程式範本，若要啟用要發佈OTA的新應用程式內容，您需要設定內容同步處理常式。
>
>如需詳細資訊，請參閱開發人員區段中的[具有內容同步的行動裝置](/help/mobile/phonegap-contentsync.md)。

在此，您可以在AEM Mobile中建立、編輯和刪除內容，方式與在AEM Sites中相同。

**「管理頁面內容」方塊**&#x200B;顯示受管理內容的頁數，以及上次針對特定裝載修改的頁數。 您可以按一下方塊中的每個記錄，深入鑽研內容以建立、複製、移動、刪除和更新頁面。

內容更新後，管理員可以通過&#x200B;**管理內容包表徵圖向客戶發佈內容更新裝載(OTA)。**

![chlimage_1-161](assets/chlimage_1-161.png)

選擇列出的內容包之一，以建立或編輯內容，如建立、編輯或刪除頁面、更改導航和頁面順序、建立或更新內容，如複製（文本）和媒體。

注意&#x200B;*所有內容都是內容*，這表示應用程式樣式、複製（文字）、媒體、頁面、導覽和目標定位內容，都可以在OTA中編輯和更新，無需造訪應用程式商店。

若要編輯AEM Mobile內容，*AEM作者*需對AEM內容編輯介面有深入的了解：[在AEM中編寫頁面。](/help/sites-authoring/qg-page-authoring.md)

## 「管理內容包」表徵圖{#the-manage-content-packages-tile}

在此，*AEM管理員*&#x200B;可快速且輕鬆地更新其應用程式，以提供吸引人的體驗和最新內容，以促進品牌參與並達成業務目標，而無需開發人員或應用程式商店重新提交。

![chlimage_1-162](assets/chlimage_1-162.png)

一旦&#x200B;*AEM作者*&#x200B;透過「管理內容」方塊新增或修改內容，*AEM管理員*&#x200B;便能透過「內容套件」更新將這些變更推送給客戶。

「內容包」動作可讓&#x200B;*AEM作者*&#x200B;在開發團隊變更主機應用程式設計與實作（包括導覽、樣式、伺服器端邏輯、範本和元件）時建立和編輯頁面內容，然後將這些變更推送至客戶，而無須重新提交至各種商店進行發佈。

**發佈新內容或更新內容的方式**

從圖磚中選取內容套件，在此範例中為英文套件。 請注意，內容更新對話方塊會列出相關的&#x200B;*內容同步*&#x200B;設定。 如果應用程式內容自上次更新後已修改，狀態將顯示&#x200B;*Pending*，如下所示。

![chlimage_1-163](assets/chlimage_1-163.png)

接下來，選擇右上角的&#x200B;**Stage**&#x200B;動作，以建立新內容更新。 添加相應的更新資訊，然後按Done。

![chlimage_1-164](assets/chlimage_1-164.png)

然後，*內容同步*&#x200B;處理程式通過形成差值(*僅*&#x200B;的包（已更改）來建立所需的包。 完成後，系統會暫存此更新內容套件，如下所示。

預先測試內容更新，可在將內容發佈至OTA至行動裝置之前進行數項更新。

>[!NOTE]
>
>發佈前，可使用AEM Verify應用程式驗證階段內容。
>
>如需AEM Verify應用程式的詳細資訊，請參閱[AEM Verify的Mobile Quickstart](/help/mobile/phonegap-mobile-quickstart.md) 。

![chlimage_1-165](assets/chlimage_1-165.png)

準備好透過內容同步OTA將新內容傳送給您的應用程式使用者時，請選取&#x200B;**發佈**，如下所示。

![chlimage_1-166](assets/chlimage_1-166.png)

### 後續步驟{#the-next-steps}

了解如何在應用程式控制面板中建立和管理應用程式內容後，請參閱下列資源以了解其他製作角色：

* [管理應用程式圖磚](/help/mobile/phonegap-app-details-tile.md)
* [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md)
* [應用程式定義](/help/mobile/phonegap-app-definitions.md)
* [使用建立應用程式精靈建立新應用程式](/help/mobile/phonegap-create-new-app.md)
* [匯入現有的混合應用程式](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他資源 {#additional-resources}

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [使用AEM為Adobe PhoneGap企業開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
