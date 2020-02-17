---
title: 設定Android studio專案並建立Android應用程式
seo-title: 設定Android studio專案並建立Android應用程式
description: 設定Android studio專案及建立AEM Forms應用程式安裝程式的步驟
seo-description: 設定Android studio專案及建立AEM Forms應用程式安裝程式的步驟
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# 設定Android studio專案並建立Android應用程式 {#set-up-the-android-studio-project-and-build-the-android-app}

本文適用於建立AEM Forms App 6.3.1.1及更新版本。 如需從AEM Forms App 6.3原始碼的原始碼建立應用程式，請參閱「 [Set up the Eclipse project and build the Android™ app](/help/forms/using/setup-eclipse-project-build-installer.md)」。

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始碼存檔是包 `adobe-lc-mobileworkspace-src-<version>.zip` 共用上包的 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 導覽至封裝共用

   URL: `https://<server>:<port>/crx/packageshare`.

1. 下載來源套件。 當您下載套件時，它會新增至您的AEM Forms套件管理員。
1. 下載後，導覽至：和 `https://<server>:<port>/crx/packmgr/index.jsp`安裝 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 若要下載原始碼封存檔，請在您的 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 瀏覽器中開啟。

   來源套件會下載在您的裝置上。

下圖顯示提取的內容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![已擷取壓縮Android™來源的內容](assets/mws-content-1.png)

下圖顯示資料夾中資料夾 `android`的目錄 `src`結構。

![src中android資料夾的目錄結構](assets/android-folder.png)

## 建立標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行下列步驟，在Android™ studio中設定專案並提供簽署識別碼：

   登入已安裝並設定Android™ studio的機器。

1. 將下載的封存 `adobe-lc-mobileworkspace-src-<version>.zip` 複製到：

   **針對MAC使用者**: `[User_Home]/Projects`

   **對於Windows®使用者**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >對於Windows®，建議您將android專案保留在系統磁碟機中。

1. 在以下目錄中解壓縮歸檔檔案：

   **針對MAC使用者**: `[User_Home]/Projects/[your-project]`

   **對於Windows®使用者**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建議您先將擷取的Android專案保留在系統磁碟機中，然後再將專案匯入Android Studio。

1. 啟動Android™ Studio。

   **針對MAC使用者**:更新資 `local.properties` 料夾中的檔案， `[User_Home]/Projects/[your-project]/android` 並將變數指 `sdk.dir` 向案頭 `SDK` 上的位置。

   **對於Windows®使用者**:更新資 `local.properties` 料夾中的檔案， `%HOMEPATH%\Projects\[your-project]\android` 並將變數指 `sdk.dir` 向案頭 `SDK` 上的位置。

1. 按一 **[!UICONTROL 下「完成]** 」以建立專案。

   專案可在ADT專案總管中使用。

   ![建立應用程式後的eclipse專案](assets/eclipsebuildmws.png)

1. 在Android™ studio中，選 **[!UICONTROL 取「匯入專案」（Eclipse ADT、Gradle等）]**。
1. 在項目瀏覽器中，在「根目錄」文本框中選擇要構建的項目的 **根目錄** :

   **** 對於Mac使用者： [User_Home]/Projects/MobileWorkspace/src/android

   **** 對於Windows®使用者：%HOMEPATH%\Projects\MobileWorkspace\src\android

1. 匯入專案後，會出現快顯視窗，內含更新Android™增效模組Gradle的選項。 根據您的需求，按一下適當的按鈕。

   ![dontremindmeagainfoletproject](assets/dontremindmeagainforthisproject.png)

1. 在成功建立Gradle後，會顯示下列畫面。 將適當的裝置或模擬器連接至系統，然後按一 **[!UICONTROL 下「執行Android™]**」。

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ studio顯示連接的裝置和可用的模擬器。 選擇要在其上運行應用程式的設備，然後按一下「確 **定」**。

   ![連接設備](assets/connecteddevice.png)

建立專案後，您可以選擇使用Android™ Debug bridge或Android™ studio安裝應用程式。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以透過 [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) ，使用下列命令將應用程式安裝在Android™裝置上：

**針對MAC使用者**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**對於Windows®使用者**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
