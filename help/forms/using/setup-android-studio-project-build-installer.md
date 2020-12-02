---
title: 設定Android Studio專案並建立Android應用程式
seo-title: 設定Android Studio專案並建立Android應用程式
description: 設定Android Studio專案及建立AEM Forms應用程式安裝程式的步驟
seo-description: 設定Android Studio專案及建立AEM Forms應用程式安裝程式的步驟
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# 設定Android Studio專案並建立Android應用程式{#set-up-the-android-studio-project-and-build-the-android-app}

本文適用於建立AEM Forms App 6.3.1.1及更新版本。 如需從AEM Forms App 6.3原始碼的原始碼建立應用程式，請參閱[「設定Eclipse專案並建立Android™應用程式](/help/forms/using/setup-eclipse-project-build-installer.md)」。

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始碼存檔`adobe-lc-mobileworkspace-src-<version>.zip`是軟體分發上`adobe-aemfd-forms-app-src-pkg-<version>.zip`軟體包的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟[軟體分發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
1. 點選頁首功能表中的「Adobe Experience Manager **[!UICONTROL 」。]**
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然後按一下&#x200B;**[!UICONTROL 上載包]**&#x200B;來上載包。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

下圖顯示`adobe-lc-mobileworkspace-src-<version>.zip`的提取內容。

![已擷取壓縮Android™來源的內容](assets/mws-content-1.png)

下圖顯示`src`資料夾中`android`資料夾的目錄結構。

![src中android資料夾的目錄結構](assets/android-folder.png)

## 建立標準AEM Forms應用程式{#set-up-the-xcode-project}

1. 執行下列步驟，在Android™ Studio中設定專案並提供簽署識別碼：

   登入已安裝並設定Android™ Studio的機器。

1. 將下載的`adobe-lc-mobileworkspace-src-<version>.zip`存檔複製到：

   **針對MAC使用者**:  `[User_Home]/Projects`

   **對於Windows®使用者**:  `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >對於Windows®，建議您將android專案保留在系統磁碟機中。

1. 在以下目錄中解壓縮歸檔檔案：

   **針對MAC使用者**:  `[User_Home]/Projects/[your-project]`

   **對於Windows®使用者**:  `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建議您先將擷取的Android專案保留在系統磁碟機中，然後再將專案匯入Android Studio。

1. 啟動Android™ Studio。

   **針對MAC使用者**:更新資 `local.properties` 料夾中的檔 `[User_Home]/Projects/[your-project]/android` 案，並將變 `sdk.dir` 數指 `SDK` 向案頭上的位置。

   **對於Windows®使用者**:更新資 `local.properties` 料夾中的檔 `%HOMEPATH%\Projects\[your-project]\android` 案，並將變 `sdk.dir` 數指 `SDK` 向案頭上的位置。

1. 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;構建項目。

   專案可在ADT專案總管中使用。

   ![建立應用程式後的eclipse專案](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，選擇&#x200B;**[!UICONTROL 匯入專案（Eclipse ADT、Gradle等）]**。
1. 在項目瀏覽器的&#x200B;**根目錄**&#x200B;文本框中，選擇要構建的項目的根目錄：

   **針對Mac使用者：** [User_Home]/Projects/MobileWorkspace/src/android

   **對於Windows®用戶：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 匯入專案後，會出現快顯視窗，內含更新Android™增效模組Gradle的選項。 根據您的需求，按一下適當的按鈕。

   ![dontremindmeagainfoletproject](assets/dontremindmeagainforthisproject.png)

1. 在成功建立Gradle後，會顯示下列畫面。 將適當的裝置或模擬器連接至系統，然後按一下「執行Android™**[!UICONTROL 」。]**

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio顯示連接的裝置和可用的模擬器。 選擇要運行應用程式的設備，然後按一下&#x200B;**確定**。

   ![連接設備](assets/connecteddevice.png)

建立專案後，您可以選擇使用Android™ Debug Bridge或Android™ Studio安裝應用程式。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以透過[Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html)在Android™裝置上安裝應用程式，並使用下列命令：

**針對MAC使用者**:  `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**對於Windows®使用者**:  `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
