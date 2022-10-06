---
title: 管理應用程式圖磚
seo-title: Manage App Tile
description: 請依照本頁面了解應用程式控制面板上的「管理應用程式圖磚」，該圖磚可供修改應用程式的詳細資訊。
seo-description: Follow this page to learn about the Manage App Tile on the app dashboard that provides the ability to modify details about the Application.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 1%

---

# 管理應用程式圖磚{#manage-app-tile}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

此 **管理應用程式** 「應用程式控制面板」上的圖磚可讓您修改應用程式的詳細資訊。 若要開啟「詳細資料」頁面，請按一下「管理應用程式」圖磚的詳細資料連結。 從「管理應用程式」頁面，您可以編輯PhoneGap應用程式設定(config.xml)設定，並準備您的應用程式以提交至各種應用程式商店。

![chlimage_1-116](assets/chlimage_1-116.png)

## 了解管理應用程式圖磚 {#understanding-the-manage-app-tile}

您可以切入 **管理應用程式** 按一下「……」即可檢視或編輯詳細資料 在右下角。

### 基本標籤 {#the-basic-tab}

您可以編輯 **名稱**, **作者**, **簡短說明**，和 **說明** 的URL。

![chlimage_1-117](assets/chlimage_1-117.png)

### 進階標籤 {#the-advanced-tab}

每個行動應用程式平台說明要收集哪些資料，並特別針對每個應用程式存放區。

顯示的平台由PhoneGap config.xml內容驅動：

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

例如，每個廠商應用程式商店(例如Apple App Store或Google Play Store)都需要一或多個行動應用程式的螢幕擷取畫面，以便向客戶顯示您的應用程式詳細資訊。 這些螢幕擷取畫面在維度和內容方面可能有嚴格的要求（基本上，它們必須真正代表應用程式）。 AEM應用程式支援選取和管理所支援平台的這些螢幕擷取畫面，並依每個廠商的應用程式商店的需求檢視連接埠維度。

>[!NOTE]
>
>AEM Verify應用程式可讓您直接在AEM中將螢幕擷取畫面傳送至應用程式詳細資訊。
>
>請參閱 [AEM適用的行動快速入門驗證](/help/mobile/phonegap-mobile-quickstart.md) 以取得更多詳細資訊。

![chlimage_1-118](assets/chlimage_1-118.png)

### 中繼資料 {#metadata}

>[!NOTE]
>
>在您熟悉 **管理應用程式** 標題，請參閱 [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md) 檢視及編輯中繼資料。

#### 常見中繼資料 {#common-metadata}

每個應用程式都應具有關聯的元資料，這些元資料有助於配置應用程式的不同方面。 「管理應用程式」頁面會分為兩個與中繼資料集合相關的不同區域。 平台特定中繼資料和通用中繼資料。

所有平台都有共同的設定和中繼資料。

在本節中，您定義了內容更新伺服器URL、行動應用程式的登陸頁面、要編譯的PhoneGap版本、應用程式版本、名稱、說明等。

**應用程式版本** 是您應用程式的有效版本。 常見的最佳實務是使用三進位記號，並在首次發行前從1.0.0以下開始。

**PhoneGap版本** 是您希望使用PhoneGap編譯應用程式的版本。 最佳實務是跟上最新版本，以確保您獲得最新且最佳的功能和錯誤修正。

**內容更新伺服器URL** 是您的應用程式將用來呼叫ContentSync更新的URL。 它必須設為您的Dispatcher URL，或（如果不使用Dispatcher）設為您其中一個將用來向應用程式提供ContentSync更新的發佈例項。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>除非有資料填入欄位，否則此區段可能會顯示為空白。
>
>在詳細資訊檢視的頂端，您會看到「應用程式版本」、「PhoneGap版本」和「更新URL」，這些值都可在「通用中繼資料」區段內設定。 但無法編輯應用程式ID。

#### 平台中繼資料 {#platform-metadata}

PhoneGap config.xml中定義的每個平台都可包含自訂平台屬性。 AEM開發人員必須貢獻內容結構才能擷取這些屬性。 可以找到iOS的平台特定屬性的提供範例。

所有已設定平台的中繼資料現在會同時顯示在「管理應用程式」方塊的「進階」標籤上。

>[!NOTE]
>
>在CLI或Remote PhoneGap構建期間，PhoneGap不會使用平台元資料部分，而是AEM會嘗試捕獲平台的元資料，以便以後在提交到目標供應商的應用程式儲存時使用這些元資料。

對於AEM不了解的平台，AEM開發人員仍可擴充UI來擷取此中繼資料，稍後這些中繼資料可在應用程式提交程式中匯出及使用。

#### iOS 中繼資料 {#ios-metadata}

Apple AppStore需要其他中繼資料，才能提交您的應用程式以供發佈。 iOS中繼資料區段會嘗試收集Apple iTMSTransporter工具可使用的必要資訊，以將中繼資料發佈至相關聯的Apple開發人員帳戶。

若要取得Apple特定中繼資料，您必須先在上建立應用程式 [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). 如果您想使用Apple iTMSTransporter工具來驗證中繼資料並將中繼資料上傳至itunesconnect.apple.com，建立應用程式時，Apple將產生iOS中繼資料區段所需的中繼資料。 如果您只想取得要收集的中繼資料，不必填寫iOS特定中繼資料。 您仍可以匯出中繼資料，將iOS和通用中繼資料合併，並將所有螢幕擷取畫面收集到zip檔案中，以便隨時下載。

下載的zip檔案包含一個itmsp檔案，您可以檢查該檔案是否有metadata.xml。 itmsp檔案包含導出的元資料（在metadata.xml檔案內）以及所有相關的螢幕截圖。

導出功能用於提供收集螢幕截圖和元資料的便利方式，這些螢幕截圖和元資料可以傳遞到應用發佈商，以輸入到供應商特定的應用商店。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android 中繼資料 {#android-metadata}

選取Android平台時，此時沒有可設定的自訂中繼資料。 按一下下載按鈕時，郵遞區號檔案會以包含所有中繼資料和相關螢幕擷取畫面的屬性檔案產生。

導出功能用於提供收集螢幕截圖和元資料的便利方式，這些螢幕截圖和元資料可以傳遞到應用發佈商，以輸入到供應商特定的應用商店。

![chlimage_1-121](assets/chlimage_1-121.png)

### 內容更新伺服器 URL {#content-update-server-url}

AEM應用程式的其中一項主要功能，是能夠讓行動應用程式透過ContentSync要求新內容，內容可以是html資源、頁面、影片、影像、文字等。 內容作者更新內容後，伺服器就會發佈該內容，讓內容更新可供行動應用程式下載。

內容更新伺服器URL屬性是必須指向發佈執行個體的URL;直接或透過dispatcher或CDN。 URL的格式很簡單：

`https://[hostname]:[port]`

>[!NOTE]
>
>如果您的製作伺服器例項正在複製到多個發佈伺服器例項(AEM的通用架構)，每個發佈伺服器都會有相同的更新內容，因為更新是建置在製作上，並複製到所有發佈例項。 基本上，完全支援負載平衡和故障切換。

### 外掛程式標籤 {#the-plugins-tab}

此 **外掛程式** 索引標籤說明與您應用程式相關聯的外掛程式。 此資訊將用於在建置期間擷取適當的外掛程式。

![chlimage_1-122](assets/chlimage_1-122.png)

### 「螢幕截圖」頁簽 {#the-screenshots-tab}

此 **螢幕截圖** 標籤會顯示不同平台上支援的螢幕截圖解析度。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>若要新增和移除螢幕擷取畫面，請參閱 [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md).

### 驗證索引標籤 {#the-authentication-tab}

此 **驗證** 標籤可讓您選取與您的應用程式相關聯的OAuth用戶端，並讓開發人員運用Adobe Experience Manager的OAuth驗證。

![chlimage_1-124](assets/chlimage_1-124.png)

### 後續步驟 {#the-next-steps}

在您了解「管理應用程式控制面板中的應用程式圖磚」後，請參閱下列資源以取得其他編寫角色：

* [編輯應用程式中繼資料](/help/mobile/phonegap-editmetadata.md)
* [應用程式定義](/help/mobile/phonegap-app-definitions.md)
* [使用建立應用程式精靈建立新應用程式](/help/mobile/phonegap-create-new-app.md)
* [匯入現有的混合應用程式](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 其他資源 {#additional-resources}

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [使用AEM為Adobe PhoneGap企業開發](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
