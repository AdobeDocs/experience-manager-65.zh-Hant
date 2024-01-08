---
title: 編寫行動應用程式
description: AEM Mobile Dashboard可讓您建立、建置和部署行動應用程式、建立、刪除和編輯應用程式中繼資料。 請依照此頁面瞭解更多資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 編寫行動應用程式{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

AEM Mobile Dashboard可讓您建立、建置和部署行動應用程式、建立、刪除和編輯應用程式中繼資料。 一旦您的應用程式上線，您就可以分析應用程式分析，包括生命週期和使用量度，以改善客戶轉換和品牌忠誠度。

若要建置AEM Mobile應用程式，請參閱 [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md) 頁面。

若要設定環境並開始使用，請參閱 [管理AEM以使用AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## AEM Mobile應用程式目錄 {#the-aem-mobile-apps-catalog}

此 [AEM Mobile應用程式目錄](http://localhost:4502/aem/apps.html/content/phonegap) 顯示AEM中管理的所有行動應用程式。

將此目錄視為AEM Mobile的「登陸頁面」，管理員可依據範本建立，或上傳行動開發人員已啟動的現有應用程式，藉此啟動新的AEM Mobile應用程式。

請依照下列步驟前往應用程式目錄登陸頁面：

1. 瀏覽至 **導覽** 然後選擇 **行動**.

1. 選擇 **應用程式** 以開啟應用程式目錄。

![AEM Mobile應用程式目錄](assets/chlimage_1-135.png)

## AEM Mobile應用程式控制面板 {#the-aem-mobile-app-dashboard}

從目錄中選取AEM Mobile應用程式會顯示其控制面板。 您可以在此處管理應用程式、檢視統計資料、建置、部署及管理行動應用程式內容。

您可以按一下右下角的「……」，展開至AEM Mobile控制面板中的每個圖磚，以檢視或編輯詳細資訊。

![AEM Mobile應用程式指揮中心](assets/chlimage_1-136.png)

### 「管理應用程式」動態磚 {#the-manage-app-tile}

「管理應用程式動態磚」會顯示您的應用程式圖示、名稱、說明、支援的平台、呼叫總部以取得更新URL和版本資訊。 您可以鑽研至此圖磚，以編輯及維護「PhoneGap應用程式設定」(config.xml)，並準備應用程式以提交至各種應用程式存放區以供分發。

按一下 [此處](/help/mobile/phonegap-app-details-tile.md) 以取得詳細資訊。

![chlimage_1-137](assets/chlimage_1-137.png)

### 「管理頁面內容」表徵圖 {#the-manage-page-content-tile}

您可以在AEM Mobile中建立、更新和刪除內容，其方式與您在AEM Sites中執行相同操作的方式相同。 此 **管理頁面內容圖磚** 顯示受管理內容和上次修改的頁數。 您可以按一下圖磚中的每筆記錄，深入鑽研內容以建立、複製、移動、刪除及更新頁面。 內容更新後，您可以透過 **「管理內容封裝」圖磚。**

![內容拼貼](assets/chlimage_1-138.png)

### 「管理內容套件」圖磚 {#the-manage-content-packages-tile}

透過「管理頁面內容」方塊新增或修改內容後，您就可以透過「內容版本」更新，將這些變更推送給客戶。

內容套件可讓AEM App Author管理AEM中的頁面內容，且讓開發團隊變更您的PhoneGap Shell應用程式（即應用程式架構或基礎架構），然後快速將這些變更推送給您的客戶，而不需要徵詢開發人員以重新提交至各種商店進行發佈。

「內容套件」會為每次更新建立ZIP檔案（視為內容發行套件）。 這些套件包含轉譯應用程式時產生的html資源和html頁面，而且具備足夠的智慧，可僅封裝自上次更新以來已修改的檔案。

管理內容套件圖磚的 **型別** 欄會顯示「應用程式」以表示應用程式殼層內容，例如開發人員所管理應用程式的框架或基礎架構，或顯示「內容」（代表內容作者所管理的頁面內容）。

內容可以語言形式表示，或是作為應用程式使用多個內容發行套件的特定部分表示。 您如何套裝內容的選擇是有彈性的，而且完全取決於您想要如何管理應用程式的內容。

此 **已修改** 欄指出最近修改頁面的時間。

此 **已分段** 欄顯示上次建立內容更新的時間。 若要建立內容更新並暫存變更，請開啟圖磚中的任何記錄並建立更新。

此 **已發佈** 欄會顯示上次內容更新的發佈時間，可供您的客戶使用。 若要發佈內容，您必須先暫存該內容，然後透過鑽研此圖磚並從「內容發行詳細資料」主控台發佈來發佈更新。

![內容版本動態磚](assets/chlimage_1-139.png) ![應用程式殼層的ContentSync套件](do-not-localize/chlimage_1-5.png)

此圖示代表應用程式殼層的內容發行套件

![內容發行套件圖示由兩個重疊的方形套件符號表示。](do-not-localize/chlimage_1-6.png)

這些圖示代表應用程式內容的內容發行套件

### PhoneGap Build圖磚 {#the-phonegap-build-tile}

此 **PhoneGap Build拼貼** 連線方式 `https://build.phonegap.com` 建置並託管遠端組建。 建置後，即可下載此組建版本，或直接透過二維碼將組建版本提供給您的裝置。

或者，您可以下載裝置來源，透過PhoneGap CLI在本機建置(`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`)。

![PhoneGap Build拼貼](assets/chlimage_1-140.png)

### 量度圖磚 {#the-metrics-tile}

>[!CAUTION]
>
>只有在您設定雲端服務後，才會顯示「量度」圖磚。
>
>另請參閱 [設定您的Adobe Mobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md) 以取得詳細資訊。

AEM Mobile透過與Adobe Analytics整合 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html) (AMS)。

控制中心 **量度圖磚** 顯示從AMS為您的應用程式提取的摘要分析。 您可以按一下右下方的「……」，深入分析控制面板。

![量度圖磚](assets/chlimage_1-141.png)

### 「管理實體內容」圖磚 {#the-manage-entity-content-tile}

「管理實體內容」表徵圖可讓您新增和管理應用程式定義。 應用程式定義可讓您識別哪些空間（和其他設定）適合應用程式。 如此一來，您就可以新增空間，而不必重新編譯應用程式。 應用程式定義已更新，且包含任何新空間的資訊。

按一下 [此處](/help/mobile/phonegap-app-definitions.md) 以建立及管理您的應用程式定義。

您可以按一下右下角的「……」，鑽研至管理實體內容控制面板。

![chlimage_1-142](assets/chlimage_1-142.png)

#### 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
