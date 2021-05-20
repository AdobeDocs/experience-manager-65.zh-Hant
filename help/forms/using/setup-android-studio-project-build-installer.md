---
title: 設定Android Studio專案並建置Android應用程式
seo-title: 設定Android Studio專案並建置Android應用程式
description: 設定Android Studio專案和建立AEM Forms應用程式安裝程式的步驟
seo-description: 設定Android Studio專案和建立AEM Forms應用程式安裝程式的步驟
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 7%

---

# 設定Android Studio專案並建置Android應用程式{#set-up-the-android-studio-project-and-build-the-android-app}

本文內容適用於建置AEM Forms App 6.3.1.1及更新版本。 如需從AEM Forms應用程式6.3原始碼的原始碼建立應用程式，請參閱[設定Eclipse專案和建立Android™應用程式](/help/forms/using/setup-eclipse-project-build-installer.md)。

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含所有元件，可建置自訂AEM Forms應用程式。 原始碼存檔`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取套件的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

下圖顯示提取的`adobe-lc-mobileworkspace-src-<version>.zip`內容。

![擷取壓縮的Android™來源內容](assets/mws-content-1.png)

下圖顯示`src`資料夾中`android`資料夾的目錄結構。

![src中android資料夾的目錄結構](assets/android-folder.png)

## 建立標準AEM Forms應用程式{#set-up-the-xcode-project}

1. 執行下列步驟以在Android™ Studio中設定專案並提供簽署身分識別：

   登入已安裝並設定Android™ Studio的電腦。

1. 將下載的`adobe-lc-mobileworkspace-src-<version>.zip`存檔複製到：

   **對於MAC用戶**:  `[User_Home]/Projects`

   **對於Windows®用戶**:  `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >若是Windows®，建議您將android專案保留在系統磁碟機中。

1. 解壓縮以下目錄中的封存：

   **對於MAC用戶**:  `[User_Home]/Projects/[your-project]`

   **對於Windows®用戶**:  `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建議您先將擷取的android專案保留在系統硬碟中，再將專案匯入Android Studio。

1. 啟動Android™ Studio。

   **對於MAC用戶**:更新資 `local.properties` 料夾中的檔 `[User_Home]/Projects/[your-project]/android` 案，並將變 `sdk.dir` 數指向案 `SDK` 頭上的位置。

   **對於Windows®用戶**:更新資 `local.properties` 料夾中的檔 `%HOMEPATH%\Projects\[your-project]\android` 案，並將變 `sdk.dir` 數指向案 `SDK` 頭上的位置。

1. 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;以建立專案。

   專案可在ADT專案總管中使用。

   ![建置應用程式後的eclipse專案](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，選取&#x200B;**[!UICONTROL 匯入專案（Eclipse ADT、Gradle等）]**。
1. 在項目資源管理器中，在&#x200B;**根目錄**&#x200B;文本框中選擇要構建的項目的根目錄：

   **Mac使用者：** [User_Home]/Projects/MobileWorkspace/src/android

   **對於Windows®用戶：**  %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 匯入專案後，會出現快顯視窗，其中包含更新Android™外掛程式Gradle的選項。 根據您的需求，按一下適當的按鈕。

   ![dontremindmeagainfortproject](assets/dontremindmeagainforthisproject.png)

1. 成功建立Gradle後，會顯示下列畫面。 將適當的設備或模擬器與系統連接，然後按一下「運行Android™]**」。**[!UICONTROL 

   ![格拉克萊孔索萊](assets/gradleconsole.png)

1. Android™ Studio顯示連接的設備和可用的模擬器。 選擇要運行應用程式的設備，然後按一下&#x200B;**確定**。

   ![connecteddevice](assets/connecteddevice.png)

建置專案後，您可以選擇使用Android™ Debug Bridge或Android™ Studio安裝應用程式。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以透過[Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html)，在Android™裝置上安裝應用程式，並使用下列命令：

**對於MAC用戶**:  `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**對於Windows®用戶**:  `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
