---
title: 管理應用程式動態磚
description: 請詳閱本頁面，瞭解應用程式控制面板上的「管理應用程式標題」，該控制面板提供修改應用程式詳細資訊的功能。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 2%

---

# 管理應用程式動態磚{#manage-app-tile}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

此 **管理應用程式** 「應用程式控制面板」上的圖磚可讓您修改應用程式的詳細資訊。 若要開啟「詳細資訊」頁面，請按一下「管理應用程式」圖磚的詳細資訊連結。 在「管理應用程式」頁面中，您可以編輯PhoneGap應用程式組態(config.xml)設定，並準備應用程式以提交至各種應用程式商店。

![chlimage_1-116](assets/chlimage_1-116.png)

## 瞭解「管理應用程式」標題 {#understanding-the-manage-app-tile}

您可以深入探討 **管理應用程式** 按一下右下角的「……」以檢視或編輯詳細資訊。

### 基本索引標籤 {#the-basic-tab}

您可以編輯 **名稱**， **作者**， **簡短說明**，以及 **說明** 以取得您的應用程式。

![chlimage_1-117](assets/chlimage_1-117.png)

### 進階索引標籤 {#the-advanced-tab}

每個行動應用程式平台會說明要收集哪些資料，並明確鎖定每個應用程式商店。

顯示的平台是由PhoneGap config.xml內容所驅動：

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

每個廠商應用程式商店(例如Apple App Store或Google Play Store)都需要一或多個行動應用程式的熒幕擷取畫面，才能向客戶顯示您的應用程式詳細資料。 這些熒幕擷取畫面可能會對維度和內容有嚴格的要求（基本上必須真正代表應用程式）。 AEM Apps可支援針對支援的平台選取和管理這些熒幕擷取畫面，並依各供應商應用程式商店的需求檢視連線埠維度。

>[!NOTE]
>
>AEM Verify應用程式可讓您在AEM中直接傳送熒幕擷取畫面至應用程式詳細資料。
>
>另請參閱 [AEM適用的Mobile Quickstart驗證](/help/mobile/phonegap-mobile-quickstart.md) 以取得更多詳細資料。

![chlimage_1-118](assets/chlimage_1-118.png)

### 中繼資料 {#metadata}

>[!NOTE]
>
>在您熟悉 **管理應用程式** 圖磚，請參閱 [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md) 以檢視和編輯中繼資料。

#### 常見中繼資料 {#common-metadata}

每個應用程式都應該有關聯的中繼資料，以協助設定應用程式的不同層面。 「管理應用程式」頁面會分隔成兩個與中繼資料收集相關的不同區域。 平台專屬中繼資料和常見中繼資料。

所有平台都有通用設定和中繼資料。

在此區段中，您可以定義內容更新伺服器URL、行動應用程式的登陸頁面、要編譯的PhoneGap版本、應用程式版本、名稱、說明等。

**應用程式版本** 是您應用程式的有效版本。 常見的最佳實務是在首次發行前使用3位小數點標籤法，且開頭必須低於1.0.0。

**PhoneGap版本** 是您要使用PhoneGap編譯應用程式的版本。 最佳實務是與最新版本保持同步，以確保您取得最新和最大的功能和錯誤修正。

**內容更新伺服器URL** 是您的應用程式用來呼叫ContentSync更新的URL。 您必須將其設定為您的Dispatcher URL，或者，如果不使用Dispatcher，則設定為將用於為應用程式提供ContentSync更新的其中一個發佈執行個體。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>除非有資料填入欄位，否則此區段可能顯示為空白。
>
>在詳細資料檢視的頂端，您會看到「應用程式版本」、「PhoneGap版本」和「更新URL」，這些值都可以在「一般中繼資料」區段中設定。 不過，無法編輯應用程式ID。

#### 平台中繼資料 {#platform-metadata}

PhoneGap config.xml中定義的每個平台都可以包含自訂平台屬性。 AEM開發人員必須貢獻內容結構才能擷取這些屬性。 您可以找到iOS的平台特定屬性範例。

「管理應用程式」圖磚的「進階」標籤上現在會同時顯示所有已設定平台的中繼資料。

>[!NOTE]
>
>PhoneGap在CLI或遠端PhoneGap Build期間不會使用平台中繼資料區段，而是AEM會嘗試擷取平台的中繼資料，以便稍後在提交至目標廠商的應用程式存放區時使用。

對於AEM不瞭解的平台，AEM開發人員仍可以擴充UI，以擷取此中繼資料，以便稍後在應用程式提交流程中匯出和使用。

#### iOS 中繼資料 {#ios-metadata}

Apple AppStore需要其他中繼資料，才能提交您的應用程式以供分發。 iOS中繼資料區段會嘗試收集Apple的iTMSTransporter工具可用來將中繼資料發佈至相關Apple開發人員帳戶的所需資訊。

若要取得Apple特定的中繼資料，您首先需要在其上建立應用程式 [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). 如果您想要使用Apple iTMSTransporter工具來驗證中繼資料並上傳至itunesconnect.apple.com，建立應用程式後，Apple將會產生iOS中繼資料區段所需的中繼資料。 如果您只想取得要收集的中繼資料，則不必填寫iOS專屬的中繼資料。 您仍然可以匯出中繼資料，這些中繼資料會合併iOS和通用中繼資料，並將所有熒幕擷取畫面收集到可隨時下載的zip檔案中。

下載的zip檔案包含可檢查metadata.xml的itmsp檔案。 itmsp檔案包含轉存的中繼資料（在metadata.xml檔案中），以及所有相關的熒幕擷取畫面。

匯出功能是用來提供收集熒幕擷取畫面和中繼資料的便利方式，這些擷取畫面和中繼資料可以傳遞至應用程式發佈者，以輸入至廠商專屬的應用程式存放區。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android™中繼資料 {#android-metadata}

選取Android™平台時，目前沒有可設定的自訂中繼資料。 按一下下載按鈕時，會產生zip檔案，其中包含所有中繼資料和相關熒幕擷取畫面的屬性檔案。

匯出功能是用來提供收集熒幕擷取畫面和中繼資料的便利方式，這些擷取畫面和中繼資料可以傳遞至應用程式發佈者，以輸入至廠商專屬的應用程式存放區。

![chlimage_1-121](assets/chlimage_1-121.png)

### 內容更新伺服器 URL {#content-update-server-url}

AEM應用程式的一項重要功能是可讓行動應用程式透過ContentSync請求新內容，其中內容可以是html資源、頁面、影片、影像、文字等。 內容作者更新內容並發佈該內容後，伺服器會讓內容更新可供行動應用程式下載。

內容更新伺服器URL屬性是必須指向發佈執行個體的URL；直接或透過Dispatcher或CDN。 URL的格式很簡單：

`https://[hostname]:[port]`

>[!NOTE]
>
>如果您的作者伺服器執行個體複製到多個發佈伺服器執行個體(AEM的共同架構)，則每個發佈伺服器將具有相同的更新內容，因為更新是建置在作者上並複製到所有發佈執行個體。 基本上完全支援負載平衡和容錯移轉。

### 外掛程式標籤 {#the-plugins-tab}

此 **外掛程式** 標籤說明與應用程式相關聯的外掛程式。 在建置期間，此資訊將用於擷取適當的外掛程式。

![chlimage_1-122](assets/chlimage_1-122.png)

### 熒幕擷圖示籤 {#the-screenshots-tab}

此 **熒幕擷圖** tab會顯示不同平台上支援的熒幕擷圖解析度。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>若要新增和移除熒幕擷取畫面，請參閱 [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md).

### 驗證標籤 {#the-authentication-tab}

此 **驗證** 索引標籤可讓您選取要與您的應用程式建立關聯的OAuth使用者端，並讓開發人員能夠使用Adobe Experience Manager的OAuth驗證。

![chlimage_1-124](assets/chlimage_1-124.png)

### 後續步驟 {#the-next-steps}

瞭解如何在應用程式控制面板中管理應用程式動態磚後，請參閱下列資源以取得其他撰寫角色：

* [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md)
* [應用程式定義](/help/mobile/phonegap-app-definitions.md)
* [使用建立應用程式精靈建立新應用程式](/help/mobile/phonegap-create-new-app.md)
* [匯入現有的混合式應用程式](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 其他資源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
