---
title: 設定Android Studio項目並構建Android應用
seo-title: Set up the Android studio project and build the Android app
description: 設定Android Studio項目和為AEM Forms應用程式生成安裝程式的步驟
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 6%

---

# 設定Android Studio項目並構建Android應用 {#set-up-the-android-studio-project-and-build-the-android-app}

本文用於構建AEM Forms應用6.3.1.1及更高版本。 有關從AEM FormsApp 6.3的原始碼生成應用，請參見 [設定Eclipse項目並構建Android™應用](/help/forms/using/setup-eclipse-project-build-installer.md)。

AEM Forms提供AEM Forms應用的完整原始碼。 源包含構建自定義AEM Forms應用的所有元件。 原始碼存檔， `adobe-lc-mobileworkspace-src-<version>.zip` 是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 軟體分發上的軟體包。

要獲取AEM Forms應用程式源，請執行以下步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

下圖顯示 `adobe-lc-mobileworkspace-src-<version>.zip`。

![已解壓Android™源的內容](assets/mws-content-1.png)

下圖顯示 `android`資料夾 `src`的子菜單。

![src中android資料夾的目錄結構](assets/android-folder.png)

## 構建標準AEM Forms應用 {#set-up-the-xcode-project}

1. 執行以下步驟以在Android™ Studio中設定項目並提供簽名標識：

   登錄到已安裝和配置Android™ Studio的電腦。

1. 複製下載的 `adobe-lc-mobileworkspace-src-<version>.zip` 存檔到：

   **對於MAC用戶**: `[User_Home]/Projects`

   **對於Windows®用戶**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >對於Windows®，建議您將android項目保留在系統驅動器中。

1. 解壓縮以下目錄中的存檔：

   **對於MAC用戶**: `[User_Home]/Projects/[your-project]`

   **對於Windows®用戶**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建議在將項目導入Android Studio之前，將提取的Android項目保留在系統驅動器中。

1. 啟動Android™ Studio。

   **對於MAC用戶**:更新 `local.properties` 檔案 `[User_Home]/Projects/[your-project]/android` 資料夾並指向 `sdk.dir` 變數 `SDK` 在案頭上的位置。

   **對於Windows®用戶**:更新 `local.properties` 檔案 `%HOMEPATH%\Projects\[your-project]\android` 資料夾並指向 `sdk.dir` 變數 `SDK` 在案頭上的位置。

1. 按一下 **[!UICONTROL 完成]** 來構建項目。

   項目在ADT項目瀏覽器中可用。

   ![構建應用程式後的eclipse項目](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，選擇 **[!UICONTROL 導入項目（Eclipse ADT、Gradle等）]**。
1. 在項目資源管理器中，選擇要在 **根目錄** 文本框：

   **對於Mac用戶：** [用戶首頁]/Projects/MobileWorkspace/src/android

   **對於Windows®用戶：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 導入項目後，將出現一個彈出窗口，其中包含更新Android™插件Gradle的選項。 根據您的要求按一下相應的按鈕。

   ![多特林姆馬加福爾特項目](assets/dontremindmeagainforthisproject.png)

1. 成功生成緩衝區後，將顯示以下螢幕。 將適當的設備或模擬器與系統連接，然後按一下 **[!UICONTROL 運行Android™]**。

   ![格拉克龍索](assets/gradleconsole.png)

1. Android™ Studio顯示連接的設備和可用的模擬器。 選擇要在其上運行應用程式的設備，然後按一下 **確定**。

   ![連接設備](assets/connecteddevice.png)

建立項目後，您可以選擇使用Android™ Debug Bridge或Android™ Studio安裝應用。

### 使用Android™調試網橋 {#andriod-debug-bridge}

您可以通過以下方式在Android™設備上安裝應用程式： [Android™調試橋](https://developer.android.com/tools/help/adb.html) 命令：

**對於MAC用戶**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**對於Windows®用戶**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
