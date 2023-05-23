---
title: 管理應用程式磁貼
seo-title: Manage App Tile
description: 按照此頁瞭解有關應用程式儀表板上管理應用程式磁貼的資訊，該儀表板提供了修改應用程式詳細資訊的功能。
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
ht-degree: 2%

---

# 管理應用程式磁貼{#manage-app-tile}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

的 **管理應用** 應用儀表板上的磁貼提供了修改應用程式詳細資訊的功能。 要開啟「詳細資訊」頁，請按一下「管理應用程式磁貼的詳細資訊」連結。 在「管理應用程式」頁中，您可以編輯PhoneGap應用程式配置(config.xml)設定，並準備應用程式提交到各種應用程式儲存。

![chlimage_1-116](assets/chlimage_1-116.png)

## 瞭解管理應用程式磁貼 {#understanding-the-manage-app-tile}

您可以鑽入 **管理應用** 通過按一下「……」來查看或編輯詳細資訊。 右下角。

### 基本頁籤 {#the-basic-tab}

可以編輯 **名稱**。 **作者**。 **簡短說明**&#x200B;的 **說明** 的子目錄。

![chlimage_1-117](assets/chlimage_1-117.png)

### 「高級」頁籤 {#the-advanced-tab}

每個移動應用程式平台都描述收集哪些資料，具體針對每個應用程式儲存。

顯示的平台由PhoneGap config.xml內容驅動：

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

例如，每個供應商應用程式商店(如AppleApp Store或Google Play商店)都需要您的移動應用程式的一個或多個螢幕截圖，以便向客戶顯示您的應用程式詳細資訊。 這些螢幕抓圖可以對尺寸和內容有嚴格要求（基本上它們必須真正代表應用程式）。 應AEM用程式支援為支援的平台選擇和管理這些螢幕快照，並根據每個供應商的應用程式商店的要求查看埠維。

>[!NOTE]
>
>「驗AEM證」應用提供了將螢幕截圖直接發送到應用程式詳細資訊的AEM功能。
>
>請參閱 [用於驗證的移動快AEM速啟動](/help/mobile/phonegap-mobile-quickstart.md) 的子菜單。

![chlimage_1-118](assets/chlimage_1-118.png)

### 中繼資料 {#metadata}

>[!NOTE]
>
>一旦你熟悉了 **管理應用** 磁貼，請參閱 [編輯應用元資料](/help/mobile/phonegap-editmetadata.md) 查看和編輯元資料。

#### 常見中繼資料 {#common-metadata}

每個應用程式都應具有關聯的元資料，這些元資料有助於配置應用程式的不同方面。 「管理應用」頁分為兩個與元資料收集相關的不同區域。 平台特定的元資料和通用元資料。

所有平台都有通用的配置和元資料。

在本節中，您定義了Content Update Server URL、移動應用程式的登錄頁、用於編譯的PhoneGap版本、應用程式版本、名稱、說明等。

**應用程式版本** 是應用程式的工作版本。 通常的最佳做法是使用3小數表示法，在第1.0.0版之前從下面開始。

**PhoneGap版本** 是您希望使用PhoneGap編譯應用程式的版本。 最佳做法是跟上當前版本，以確保您獲得最新、最好的功能和錯誤修復。

**內容更新伺服器URL** 是應用程式將用於調用ContentSync更新的URL。 它必須設定為您的調度程式URL，或者，如果不使用調度程式，則必須設定為您的某個發佈實例，這些實例將用於向您的應用程式提供ContentSync更新。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>除非有資料填充欄位，否則此部分可能顯示為空。
>
>在詳細資訊視圖的頂部，您將看到應用程式版本、PhoneGap版本和更新URL，這些值都可以在公共元資料部分中設定。 但是，無法編輯應用程式ID。

#### 平台元資料 {#platform-metadata}

在PhoneGap config.xml中定義的每個平台都可以包含自定義平台屬性。 開發AEM人員必須提供內容結構才能捕獲這些屬性。 可以找到為iOS提供的平台特定屬性示例。

現在，所有已配置平台的元資料都同時顯示在「管理應用」磁貼的「高級」頁籤上。

>[!NOTE]
>
>在CLI或Remote PhoneGap生成期間，PhoneGap不會使用平台元資料節，而是會嘗試捕獲平台的元資料AEM，以便在稍後提交到目標供應商的應用程式儲存時使用這些元資料。

對於不能理解AEM的平台，開發人員仍可AEM以擴展UI以捕獲此元資料，稍後可以在應用程式提交過程中導出和使用此元資料。

#### iOS 中繼資料 {#ios-metadata}

Apple應用商店需要其他元資料才能提交您的應用程式以供分發。 iOS元資料部分試圖收集Apple的iTMSTransporter工具可使用的所需資訊，以便將元資料發佈到相關的Apple開發人員的帳戶。

要獲取Apple特定的元資料，您首先需要在 [https://itunesconnect.apple.com](https://itunesconnect.apple.com/)。 建立應用程式後，如果您希望使用AppleiTMSTransporter工具驗證元資料並將元資料上載到itunesconnect.apple.com,Apple將生成iOS元資料部分所需的元資料。 如果只想獲取要收集的元資料，就不必填寫iOS特定的元資料。 您仍然可以導出元資料，將iOS元資料和常用元資料合併，並將所有螢幕截圖收集到一個zip檔案中，該檔案可以隨時下載。

下載的zip檔案包含一個itmsp檔案，可以檢查該metadata.xml。 itmsp檔案包含導出的元資料（在metadata.xml檔案中）以及所有關聯的螢幕截圖。

導出功能用於提供收集螢幕截圖和元資料的方便方法，所述螢幕截圖和元資料可以被傳遞到應用程式發佈者，用於輸入到供應商特定的應用程式儲存中。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android 中繼資料 {#android-metadata}

選擇Android平台時，此時沒有可設定的自定義元資料。 當按一下下載按鈕作為zip檔案時，將生成包含所有元資料和相關螢幕快照的屬性檔案。

導出功能用於提供收集螢幕截圖和元資料的方便方法，所述螢幕截圖和元資料可以被傳遞到應用程式發佈者，用於輸入到供應商特定的應用程式儲存中。

![chlimage_1-121](assets/chlimage_1-121.png)

### 內容更新伺服器 URL {#content-update-server-url}

Apps的關鍵功能之一是AEM能夠讓移動應用程式通過ContentSync請求新內容，其中的內容可以是html資源、頁面、視頻、影像、文本等。 一旦內容作者已經更新了內容，然後發佈該內容，伺服器就使內容更新可供移動應用程式下載。

Content Update Server URL屬性是必須指向發佈實例的URL;直接或通過分發程式或CDN。 URL的格式很簡單：

`https://[hostname]:[port]`

>[!NOTE]
>
>如果「作者」伺服器實例正在複製到多個發佈伺服器實例(公共體系結構AEM)，則每個發佈伺服器將具有相同的更新內容，因為更新是在作者上構建的，並複製到所有發佈實例。 基本上，完全支援負載平衡和故障切換。

### 「插件」標籤 {#the-plugins-tab}

的 **插件** 標籤描述了與您的應用關聯的插件。 此資訊將用於在生成期間檢索相應的插件。

![chlimage_1-122](assets/chlimage_1-122.png)

### 螢幕截圖頁籤 {#the-screenshots-tab}

的 **截屏** 頁籤顯示不同平台上支援的螢幕快照解析度。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>要添加和刪除螢幕截圖，請參閱 [編輯應用元資料](/help/mobile/phonegap-editmetadata.md)。

### 驗證頁籤 {#the-authentication-tab}

的 **驗證** 頁籤允許您選擇與應用程式關聯的OAuth客戶端，並使開發人員能夠利用Adobe Experience Manager的OAuth身份驗證。

![chlimage_1-124](assets/chlimage_1-124.png)

### 後續步驟 {#the-next-steps}

在應用程式儀表板中瞭解了管理應用程式磁貼後，請參閱以下其他創作角色的資源：

* [編輯應用元資料](/help/mobile/phonegap-editmetadata.md)
* [應用定義](/help/mobile/phonegap-app-definitions.md)
* [使用「建立應用程式嚮導」建立新應用程式](/help/mobile/phonegap-create-new-app.md)
* [導入現有混合應用](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 其他資源 {#additional-resources}

要瞭解管理員和開發人員的角色和職責，請參閱以下資源：

* [Adobe PhoneGap企業AEM發展](/help/mobile/developing-in-phonegap.md)
* [為Adobe PhoneGap企業管理內AEM容](/help/mobile/administer-phonegap.md)
