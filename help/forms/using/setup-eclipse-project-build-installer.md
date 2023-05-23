---
title: 構建AEM FormsAndroid應用
seo-title: Build the AEM Forms Android app
description: 設定Android Studio項目和為AEM FormsAndroid應用程式生成.apk檔案的步驟
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 5%

---

# 構建AEM FormsAndroid應用 {#build-the-aem-forms-android-app}

按照建議的順序執行以下步驟，為AEM Forms構建Android應用。

1. [下載AEM Forms應用原始碼包](#download-android-zip)
1. [設定環境變數](#set-environment-variable-android)
1. [構建標準AEM Forms應用](#set-up-the-xcode-project)

## 下載AEM Forms應用原始碼包 {#download-android-zip}

AEM Forms應用原始碼包是指 `adobe-lc-mobileworkspace-src-<version>.zip` 存檔。 此存檔包括生成自定義AEM Forms應用所需的原始碼。 存檔包含在 `adobe-aemfd-forms-app-src-pkg-<version>.zip`軟體包在軟體分發中提供。

執行以下步驟下載 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 檔案：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。
1. 要下載原始碼存檔，請開啟 **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** 的子菜單。 Android應用.zip檔案已下載到您的設備上。
1. 將.zip檔案的內容解壓到本地檔案系統上的資料夾。 比如說， *C:\&lt;folder structure=&quot;&quot;>\adobe lc-mobileworkspace-src-2.4.20*

下圖顯示 `adobe-lc-mobileworkspace-src-<version>.zip\android`的子菜單。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 設定環境變數 {#set-environment-variable-android}

在啟動AEM Forms應用的生成過程之前設定以下環境變數：

* 將JAVA_HOME環境變數設定為本地檔案系統上JDK軟體的位置。 例如，C:\Program Files\Java\jdk1.8.0_181
* 設定 `ANDROID_SDK_ROOT` 系統環境變數到Android的SDK位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 設定 `Path` 系統環境變數，包括平台工具和工具資料夾的Android位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools。

## 構建標準AEM Forms應用 {#set-up-the-xcode-project}

保存adobe-lc-mobileworkspace-src後 — &lt;version>在本地檔案系統上的.zip檔案並設定環境變數，使用以下任何選項構建標準的AEM FormsAndroid應用：

* [使用Android Studio構建AEM Forms應用](#using-android-studio)
* [使用Android Studio生成.apk檔案](#generate-apk-android-studio)

### 使用Android Studio構建AEM Forms應用 {#using-android-studio}

執行以下步驟，使用Android Studio構建AEM Forms應用：

1. 在您的電腦上啟動Android Studio應用程式。
1. 按一下 **開啟現有Android Studio項目**。 如果開啟現有項目的對話框未自動顯示，請選擇 **檔案** > **開啟**。
1. 導航到 *adobe lc-mobileworkspace-src&lt;version>.zip/android* 在本地檔案系統上，按一下 **確定**。

   的 **安卓** 選項。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 選擇 **安卓** 按一下 **運行** > **運行「android」**。
1. 從「選擇部署目標」對話框的「已連接設備」部分選擇Android設備，然後按一下「確定」。

   成功構建開發環境後，現在可以在應用上應用自定義項。 使用以下文章自定義應用：

   * [品牌自訂](/help/forms/using/branding-customization.md)
   * [主題自定義](/help/forms/using/theme-customization.md)
   * [手勢自定義](/help/forms/using/gesture-customization.md)

   將適當的自定義項應用程式後，可以生成.apk檔案進行分發。

### 使用Android Studio生成.apk檔案 {#generate-apk-android-studio}

執行以下步驟，使用Android Studio生成.apk檔案：

1. 在您的電腦上啟動Android Studio應用程式。
1. 選擇 **開啟現有Android Studio項目**。 如果開啟現有項目的對話框未自動顯示，請選擇 **檔案** > **開啟**。
1. 導航到 *adobe lc-mobileworkspace-src&lt;version>.zip/android* 在本地檔案系統上，按一下 **確定**。

   android選項顯示在左窗格中。

1. 選擇 **生成** > **生成APK** 生成.apk檔案。

   （可選）選擇 **生成** > **生成簽名APK** 生成 [簽名版本](https://developer.android.com/studio/publish/app-signing) 的子菜單。

## 使用Android調試網橋 {#build-android-debug-bridge}

生成.apk檔案後，執行以下命令，使用 [Android調試橋](https://developer.android.com/tools/help/adb.html)。

**Windows用戶：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac用戶：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
