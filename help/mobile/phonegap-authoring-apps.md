---
title: 製作行動應用程式
seo-title: Authoring Mobile Applications
description: AEM Mobile Dashboard可讓您建立、建置和部署行動應用程式、建立、刪除和編輯應用程式中繼資料。 請詳閱本頁以了解更多。
seo-description: he AEM Mobile Dashboard allows you to create, build and deploy your mobile application, create, delete and edit application metadata. Follow this page to learn more.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 製作行動應用程式{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile控制面板可讓您建立、建置和部署行動應用程式、建立、刪除和編輯應用程式中繼資料。 應用程式上線後，您就可以分析應用程式分析，包括生命週期和使用量度，以改善客戶轉換和品牌忠誠度。

若要建置您的AEM Mobile應用程式，請參閱 [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md) 頁面。

若要設定環境並開始使用，請參閱 [管理AEM以使用AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## AEM Mobile應用程式目錄 {#the-aem-mobile-apps-catalog}

此 [AEM Mobile應用程式目錄](http://localhost:4502/aem/apps.html/content/phonegap) 顯示在AEM中管理的所有行動應用程式。

請將此目錄想像為AEM Mobile的「登錄頁面」，管理員可在此處根據範本建立，或上傳行動開發人員已啟動的現有應用程式，以啟動新的AEM Mobile應用程式。

請依照下列步驟前往應用程式目錄登陸頁面：

1. 瀏覽至 **導覽** 然後選擇 **行動**.

1. 選擇 **應用程式** 來開啟應用程式目錄。

![AEM Mobile應用程式目錄](assets/chlimage_1-135.png)

## AEM Mobile應用程式控制面板 {#the-aem-mobile-app-dashboard}

從目錄中選取AEM Mobile應用程式時，將顯示其控制面板。 您可以在此處管理應用程式、檢視統計資料、建立、部署及管理行動應用程式內容。

您可以展開至AEM Mobile控制面板中的每個圖磚，按一下「……」來檢視或編輯詳細資料 在右下角。

![AEM Mobile應用程式指揮中心](assets/chlimage_1-136.png)

### 管理應用程式圖磚 {#the-manage-app-tile}

「管理應用程式圖磚」會顯示您的應用程式圖示、名稱、說明、支援的平台、呼叫首頁以取得更新URL和版本資訊。 您可以深入到此表徵圖以編輯和維護PhoneGap應用程式配置(config.xml)，並準備您的應用程式以提交到變數應用程式儲存庫進行分發。

按一下 [此處](/help/mobile/phonegap-app-details-tile.md) 以取得詳細資訊。

![chlimage_1-137](assets/chlimage_1-137.png)

### 「管理頁面內容」圖磚 {#the-manage-page-content-tile}

在AEM Mobile中建立、更新和刪除內容的方式，與在AEM Sites中執行相同操作的方式大同小異。 此 **管理頁面內容圖磚** 顯示托管內容和上次修改的頁數。 您可以按一下方塊中的每個記錄，深入鑽研內容以建立、複製、移動、刪除和更新頁面。 內容更新後，您可以透過 **「管理內容包」表徵圖。**

![內容拼貼](assets/chlimage_1-138.png)

### 「管理內容包」表徵圖 {#the-manage-content-packages-tile}

透過「管理頁面內容」圖磚新增或修改內容後，您就可以透過「內容發行」更新將這些變更推送至客戶。

「內容套件」可讓AEM應用程式作者管理AEM中的頁面內容，並讓您的開發團隊變更您的PhoneGap Shell應用程式（即應用程式架構或基礎架構），然後快速將這些變更推送至客戶，而無需請開發人員重新提交至各種商店進行發佈。

內容套件會針對每次更新建立ZIP檔案，視為內容發行套件。 這些套件包含轉譯應用程式時產生的html資源和html頁面，且智慧程度足以僅封裝自上次更新以來已修改的檔案。

管理內容包表徵圖的 **類型** 欄會顯示「應用程式」以表示應用程式殼層內容，例如由開發人員管理之應用程式的架構或基礎架構，或顯示「內容」，代表由內容作者管理的頁面內容。

內容可以以語言呈現，或以應用程式特定部分呈現，應用程式會使用多個內容發行套件。 您可以選擇如何捆綁內容，其設計靈活且完全取決於您希望如何管理應用程式的內容。

此 **已修改** 欄會指出最近修改頁面的時間。

此 **已轉移** 欄顯示上次內容更新的建立時間。 若要建立新內容更新並預備變更，請開啟圖磚中的任何記錄並建立新更新。

此 **已發佈** 欄顯示上次內容更新發佈的時間，供客戶使用。 若要發佈內容，您必須先預備該內容，然後透過切入此圖磚並從「內容發行詳細資料」主控台發佈，以發佈更新。

![內容發行圖磚](assets/chlimage_1-139.png) ![應用程式殼層的ContentSync套件](do-not-localize/chlimage_1-5.png)

此圖示代表應用程式殼層的內容發行套件

![](do-not-localize/chlimage_1-6.png)

這些圖示代表應用程式內容的內容發行套件

### PhoneGap Build圖磚 {#the-phonegap-build-tile}

此 **PhoneGap Build圖磚** 連線 [https://build.phonegap.com](https://build.phonegap.com) 來建置和托管遠端buid。 建置後，組建即可供下載使用，或透過QR碼直接供您的裝置使用。

或者，您也可以下載裝置來源，透過 [PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![PhoneGap Build圖磚](assets/chlimage_1-140.png)

### 量度方塊 {#the-metrics-tile}

>[!CAUTION]
>
>「量度」方塊只有在您設定雲端服務後才會顯示。
>
>請參閱 [設定您的AdobeMobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md) 以取得詳細資訊。

AEM Mobile透過與Adobe Analytics整合 [AdobeMobile Services SDK](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html) (AMS)。

控制中心 **量度方塊** 顯示從AMS提取的應用程式摘要分析。 您可以按一下「……」，深入分析控制面板 在右下角。

![量度方塊](assets/chlimage_1-141.png)

### 「管理實體內容」表徵圖 {#the-manage-entity-content-tile}

「管理實體內容」圖磚可讓您新增及管理應用程式定義。 應用程式定義是識別哪些空格（和其他設定）適合應用程式的方法。 如此即可新增空間，而無須重新編譯應用程式。 應用程式定義已更新，其中將包含任何新空格的資訊。

按一下 [此處](/help/mobile/phonegap-app-definitions.md) 來建立和管理應用程式定義。

您可以按一下「……」，深入到管理實體內容控制面板 在右下角。

![chlimage_1-142](assets/chlimage_1-142.png)

#### 其他資源 {#additional-resources}

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [使用AEM為Adobe PhoneGap企業開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
